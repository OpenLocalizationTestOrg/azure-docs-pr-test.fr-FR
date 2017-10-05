---
title: "Sécuriser votre déploiement de l’Internet des objets | Microsoft Docs"
description: "Cet article explique comment sécuriser votre déploiement IoT"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 95c23341-16b0-4954-b3f2-d2e82ab7b367
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: d752dd13b138cdae80dac5c0b2f84a19fe0aa670
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-your-iot-deployment"></a>Sécuriser votre déploiement IoT
Cet article fournit davantage de détails sur la sécurisation de l’infrastructure Internet des objets (IoT) basée sur Azure IoT. Il est lié à la procédure au niveau de l’implémentation pour la configuration et le déploiement de chaque composant. Il fournit également des comparaisons et des choix entre les différentes méthodes.

La sécurisation du déploiement Azure IoT peut être divisée selon les trois zones de sécurité suivantes :

* **Sécurité de l’appareil**: sécurisation de l’appareil IoT alors que celui-ci est déployé dans la nature.
* **Sécurité de la connexion**: s’assurer que toutes les données transmises entre l’appareil IoT et IoT Hub sont confidentielles et protégées contre la falsification.
* **Sécurité du cloud**: fournir un moyen de sécuriser les données lorsque celles-ci transitent par le cloud ou sont stockées sur celui-ci.

![Trois zones de sécurité][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Approvisionnement et authentification sécurisés des appareils
Azure IoT Suite sécurise les appareils IoT à l’aide des deux méthodes suivantes :

* En fournissant une clé d’identité unique (jetons de sécurité) pour chaque appareil, qui peut être utilisée par l’appareil pour communiquer avec IoT Hub.
* À l’aide d’un [certificat X.509][lnk-x509] et d’une clé privée sur l’appareil en vue d’authentifier l’appareil auprès de l’IoT Hub. Cette méthode d’authentification permet de s’assurer que la clé privée sur l’appareil reste confidentielle à tout moment, offrant ainsi un niveau de sécurité plus élevé.

La méthode du jeton de sécurité fournit une authentification pour chaque appel effectué par l’appareil à IoT Hub en associant la clé symétrique à chaque appel. L’authentification basée sur le certificat X.509 permet l’authentification d’un appareil IoT au niveau physique dans le cadre de l’établissement d’une connexion TLS. La méthode basée sur le jeton de sécurité peut être utilisée sans l’authentification X.509 qui constitue un modèle moins sécurisé. Le choix entre les deux méthodes dépend principalement du niveau requis pour l’authentification de l’appareil et de la disponibilité d’un stockage sécurisé sur l’appareil (pour stocker la clé privée en toute sécurité).

## <a name="iot-hub-security-tokens"></a>Jetons de sécurité IoT Hub
IoT Hub utilise des jetons de sécurité pour authentifier les appareils et les services afin d’éviter d’envoyer des clés sur le réseau. En outre, la validité et la portée des jetons sont limitées dans le temps. Les Kits de développement logiciel (SDK) Azure IoT Hub génèrent automatiquement les jetons sans configuration spéciale. Certains scénarios requièrent toutefois que l’utilisateur génère et utilise directement des jetons de sécurité. Par exemple, il peut s’agir de l’utilisation directe des surfaces MQTT, AMQP ou HTTP, ou de l’implémentation du modèle de service de jeton.

Vous trouverez plus d’informations sur la structure du jeton de sécurité et son utilisation dans les articles suivants :

* [Structure du jeton de sécurité][lnk-security-tokens]
* [Utilisation de jetons SAP comme appareil][lnk-sas-tokens]

Chaque IoT Hub dispose d’un [registre d’identité][lnk-identity-registry] servant à créer des ressources par appareil dans le service, par exemple, une file d’attente contenant des messages actuels envoyés du cloud vers l’appareil. En outre, il autorise l’accès aux points de terminaison des appareils. Le registre des identités IoT Hub stocke de manière sécurisée les identités des appareils et les clés de sécurité d’une solution. Des identités d’appareil peuvent être ajoutées à une liste verte ou une liste rouge, individuellement ou en groupe, permettant un contrôle total de l’accès à l’appareil. Les articles suivants fournissent plus de détails sur la structure du registre d’identité et les opérations prises en charge.

[IoT Hub prend en charge les protocoles tels que MQTT, AMQP, and HTTP][lnk-protocols]. Chacun de ces protocoles utilise des jetons de sécurité à partir de l’appareil IoT vers IoT Hub différemment :

* AMQP : sécurité basée sur des revendications AMQP et SASL PLAIN ({policyName}@sas.root.{iothubName} dans le cas de jetons de niveau IoT hub ; {deviceId} dans le cas de jetons à l’échelle de l’appareil).
* MQTT : le paquet CONNECT utilise {deviceId} en tant que {ClientId}, {IoThubhostname}/{deviceId} dans le champ **Nom d’utilisateur** et un jeton SAS dans le champ **Mot de passe**.
* HTTP : le jeton valide se trouve dans l’en-tête de la requête d’autorisation.

Vous pouvez utiliser le registre d’identité IoT Hub pour configurer les informations d’identification de sécurité et le contrôle d’accès par appareil. Cependant, si une solution IoT représente déjà un investissement significatif dans un [registre d’identité des appareils personnalisé et/ou un schéma d’authentification][lnk-custom-auth], vous pouvez intégrer cette infrastructure existante à IoT Hub en créant un service de jeton.

### <a name="x509-certificate-based-device-authentication"></a>Authentification des appareils basée sur un certificat X.509
L’utilisation d’un [certificat X.509 basé sur un appareil][lnk-protocols] et sa paire de clés privée et publique associée permet d’obtenir une authentification supplémentaire au niveau de la couche physique. La clé privée est stockée en toute sécurité dans l’appareil et n’est pas détectable en dehors de l’appareil. Le certificat X.509 contient des informations sur l’appareil, telles que l’identifiant de l’appareil et d’autres détails organisationnels. Une signature du certificat est générée à l’aide de la clé privée.

Flux d’approvisionnement des appareils de haut niveau :

* Associer un identificateur à un appareil physique : identité de l’appareil et/ou certificat X.509 associés à l’appareil lors de la fabrication ou de la mise en service de l’appareil.
* Créer une entrée d’identité correspondante dans IoT Hub : identité de l’appareil et informations connexes sur l’appareil dans le Registre d’identité IoT Hub.
* Stocker en toute sécurité l’empreinte numérique du certificat X.509 dans le Registre d’identité IoT Hub.

### <a name="root-certificate-on-device"></a>Certificat racine sur un appareil
Lors de l’établissement d’une connexion TLS sécurisée avec IoT Hub, l’appareil IoT authentifie IoT Hub à l’aide d’un certificat racine qui fait partie du Kit de développement logiciel (SDK) de l’appareil. Pour le Kit de développement logiciel (SDK) du client C, le certificat se trouve dans le dossier « \\c\\certs » sous la racine du référentiel. Bien que ces certificats racine soient de longue durée, ils peuvent malgré tout expirer ou être révoqués. S’il n’existe aucun moyen de mettre à jour le certificat sur l’appareil, il est possible que celui-ci ne puisse pas se connecter ultérieurement à IoT Hub (ou tout autre service cloud). Pour minimiser ce risque, nous vous conseillons de disposer d’un moyen de mettre à jour le certificat racine une fois l’appareil IoT déployé.

## <a name="securing-the-connection"></a>Sécurisation de la connexion
La connexion Internet entre l’appareil IoT et IoT Hub est sécurisée à l’aide de la norme TLS (Transport Layer Security). Azure IoT prend en charge [TLS 1.2][lnk-tls12], TLS 1.1 et TLS 1.0, dans cet ordre. La prise en charge de TLS 1.0 est fournie uniquement à des fins de compatibilité descendante. Il est recommandé d’utiliser TLS 1.2, qui fournit la meilleure sécurité.

Azure IoT Suite prend en charge les suites de chiffrement suivantes, dans cet ordre.

| Suite de chiffrement | Longueur |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. 7680 bits RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. 3072 bits RSA) FS |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. 7680 bits RSA) FS |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. 3072 bits RSA) FS |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-the-cloud"></a>Sécurisation du cloud
Azure IoT Hub permet la définition de [stratégies de contrôle d’accès][lnk-protocols] pour chaque clé de sécurité. Azure IoT Hub utilise l’ensemble d’autorisations qui suit pour accorder l’accès à chaque point de terminaison IoT Hub. Les autorisations limitent l’accès à un IoT Hub selon la fonctionnalité.

* **RegistryRead**. Accorde l’accès en lecture au registre des identités. Pour plus d’informations, consultez la rubrique dédiée au [registre des identités][lnk-identity-registry].
* **RegistryReadWrite**. Accorde l’accès en lecture et en écriture au registre des identités. Pour plus d’informations, consultez la rubrique dédiée au [registre des identités][lnk-identity-registry].
* **ServiceConnect**. Accorde l’accès à la communication de services cloud et à la surveillance des points de terminaison. Par exemple, elle permet aux services cloud principaux de recevoir des messages appareil-à-cloud, d’envoyer des messages cloud-à-appareil et de récupérer les accusés de remise correspondants.
* **DeviceConnect**. Accorde l’accès aux points de terminaison côté appareil. Par exemple, elle permet d’envoyer des messages appareil-à-cloud et de recevoir des messages cloud-à-appareil. Cette autorisation est utilisée par les appareils.

Il existe deux façons d’obtenir des autorisations **DeviceConnect** avec IoT Hub avec [jetons de sécurité][lnk-sas-tokens] : avec une clé d’identité d’appareil ou une clé d’accès partagé. En outre, il est important de noter que toutes les fonctionnalités accessibles à partir des appareils sont exposées dès le départ sur les points de terminaison avec le préfixe `/devices/{deviceId}`.

Les [composants de service peuvent uniquement créer des jetons de sécurité][lnk-service-tokens] utilisant des stratégies d’accès partagé pour accorder les autorisations adaptées.

Azure IoT Hub et d’autres services pouvant faire partie de la solution autorisent la gestion des utilisateurs à l’aide d’Azure Active Directory.

Les données reçues par Azure IoT Hub peuvent être utilisées par une variété de services comme Azure Stream Analytics et le stockage d’objets blob. Ces services permettent un accès en gestion. En savoir plus sur ces services et les options disponibles ci-dessous :

* [Azure Cosmos DB][lnk-docdb] : service de base de données évolutif et entièrement indexé pour données semi-structurées, qui gère les métadonnées (attributs, configuration, propriétés de sécurité, etc.) des appareils que vous approvisionnez. Cosmos DB assure un traitement hautes performances et à débit élevé, ainsi qu’une indexation des données indépendante du schéma. Ce service offre également une interface de requête SQL enrichie.
* [Azure Stream Analytics][lnk-asa] : traitement des flux en temps réel dans le cloud, permettant de développer et de déployer rapidement une solution d’analyse à faible coût pour obtenir des informations en temps réel de la part des appareils, capteurs, infrastructures et applications. Les données de ce service entièrement géré peuvent être mises à l’échelle selon n’importe quel volume. Vous continuez à bénéficier d’un débit élevé, d’une faible latence et de la résilience.
* [Azure App Services][lnk-appservices] : plateforme cloud permettant de créer de puissantes applications web et mobiles qui se connectent aux données n’importe où, que ce soit localement ou dans le cloud. Créez des applications mobiles attrayantes pour iOS, Android et Windows. Assurez l’intégration avec vos applications SaaS (Software as a Service) et d’entreprise grâce à une connectivité prête à l’emploi à des dizaines d’applications et services basés sur le cloud. Encodez dans votre environnement de développement intégré et votre langage favoris (.NET, Node.js, PHP, Python ou Java) pour créer rapidement des applications web et des API.
* [Logic Apps][lnk-logicapps] : fonctionnalité Azure App Service qui vous aide à intégrer votre solution IoT dans vos systèmes métier existants et à automatiser les processus de flux de travail. Logic Apps permet aux développeurs de concevoir des flux de travail qui démarrent à partir d’un déclencheur et exécutent une série d’étapes — des règles et actions utilisant des connecteurs puissants pour l’intégration à vos processus d’entreprise. Logic Apps offre une connectivité prête à l’emploi vers un vaste écosystème d’applications SaaS, basées sur le cloud et locales.
* [Blob Storage][lnk-blob] : stockage cloud fiable et économique pour les données que vos appareils envoient au cloud.

## <a name="conclusion"></a>Conclusion
Cet article fournit une vue d’ensemble des détails au niveau de l’implémentation pour concevoir et déployer une infrastructure IoT à l’aide d’Azure IoT. La configuration de chaque composant afin qu’il soit sécurisé est essentielle pour sécuriser l’infrastructure IoT dans son ensemble. Les choix de conception disponibles dans Azure IoT offrent un certain degré de souplesse et de choix. Toutefois, chaque choix peuvent avoir des implications en matière de sécurité. Nous vous recommandons d’évaluer chacun de ces choix à l’aide d’une évaluation des risques et du coût.

## <a name="see-also"></a>Voir aussi
Vous pouvez également explorer certaines des autres fonctionnalités et capacités des solutions préconfigurées IoT Suite :

* [Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]
* [Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]

Pour en savoir plus sur la sécurité d’IoT Hub, consultez la rubrique [Contrôler l’accès à IoT Hub][lnk-devguide-security] du guide du développeur IoT Hub.


[img-overview]: media/iot-suite-security-deployment/overview.png

[lnk-security-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
