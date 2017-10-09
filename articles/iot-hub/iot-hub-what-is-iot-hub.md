---
title: "aaaAzure vue d’ensemble de IoT Hub | Documents Microsoft"
description: "Vue d’ensemble de hello Azure IoT Hub service : nouveautés IoT Hub, la connectivité d’appareils, internet de modèles de communication de choses, les passerelles et modèle de communication d’assistance de service hello"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Vue d’ensemble de hello Azure IoT Hub service

Bienvenue dans tooAzure IoT Hub. Cet article fournit une vue d’ensemble de Azure IoT Hub et explique pourquoi vous devez utiliser cette tooimplement service une solution Internet of Things (IoT). Azure IoT Hub est un service entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils IoT et un serveur principal de solution. Azure IoT Hub :

* Fournit plusieurs options de communication appareil vers cloud et cloud vers appareil, y compris la messagerie unidirectionnelle, le transfert de fichiers et les méthodes de demande-réponse.
* Fournit des services Azure tooother de routage de message déclarative intégré.
* Fournit un stockage utilisable dans une requête pour les métadonnées d’appareil et les informations d’état synchronisées.
* Assure la sécurité des communications et le contrôle d’accès grâce aux clés de sécurité par appareil ou aux certificats X.509.
* Fournit une surveillance complète de la connectivité des appareils et des événements de gestion de l’identité des appareils.
* Inclut des bibliothèques de périphérique pour les plateformes et les langues les plus populaires hello.

article de Hello [comparaison de IoT Hub et les concentrateurs d’événements] [ lnk-compare] décrit hello les principales différences entre ces deux services et met en évidence les avantages de hello de l’utilisation de IoT Hub dans vos solutions IoT.

Pour plus d’informations sur la façon dont Azure IoT Hub et sécuriser votre solution IoT, consultez [hello d’arrière-plan la sécurité Internet of Things][lnk-security-ground-up].

![Azure IoT Hub comme passerelle cloud dans une solution Internet des objets][img-architecture]

> [!NOTE]
> Pour une discussion détaillée de l’architecture de IoT, consultez hello [Architecture de référence de Microsoft Azure IoT][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>Défis liés à la connectivité des appareils IoT

Bibliothèques de périphérique IoT Hub et hello vous aider à défis de hello toomeet de façon tooreliably et connectez-vous en toute sécurité des appareils toohello solution back-end. Les appareils IoT :

* sont souvent des systèmes intégrés, qui ne font appel à aucun opérateur humain ;
* peuvent être situés sur des sites distants avec un accès physique coûteux ;
* Peut être uniquement accessible via une hello solution back-end.
* peuvent avoir des performances et/ou des ressources de traitement limitées ;
* peuvent avoir une connectivité réseau intermittente, lente ou coûteuse ;
* Protocoles d’application propriétaire, personnalisées ou spécifiques au secteur toouse peut-être.
* peuvent être créés à l’aide d’un large éventail de plateformes matérielles et logicielles populaires.

En outre toohello les spécifications ci-dessus, n’importe quelle solution IoT doit également fournir l’échelle, la sécurité et fiabilité. jeu Hello d’exigences de connectivité est difficile et long tooimplement lorsque vous utilisez des technologies traditionnelles, telles que les conteneurs de web et des répartiteurs de messagerie.

## <a name="why-use-azure-iot-hub"></a>Pourquoi utiliser Azure IoT Hub ?

En outre tooa riche ensemble de [appareil-à-cloud] [ lnk-d2c-guidance] et [cloud-à-appareil] [ lnk-c2d-guidance] les options de communication, y compris la messagerie, de fichiers les transferts et méthodes de demande-réponse, Azure IoT Hub adresses hello connectivité des périphériques défis Bonjour suivant façons :

* **Représentations d’appareil physique**. À l’aide de [représentations d’appareil physique][lnk-twins], vous pouvez stocker, synchroniser et interroger les informations de métadonnées et d’état de l’appareil. Les représentations d’appareil sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions). IoT Hub conserve un double du périphérique pour chaque périphérique que vous vous connectez tooIoT Hub.

* **Authentification par appareil et connectivité sécurisée**. Vous pouvez configurer chaque périphérique avec sa propre [clé de sécurité] [ lnk-devguide-security] tooenable il tooconnect tooIoT Hub. Hello [Registre des identités IoT Hub] [ lnk-devguide-identityregistry] stocke les identités des appareils et des clés dans une solution. Un principal de la solution peut ajouter des périphériques individuels tooallow ou refuser des listes tooenable un contrôle complet sur l’accès à l’appareil.

* **Itinéraire appareil-à-cloud services tooAzure basées sur des règles déclaratives des messages**. IoT Hub permet de message toodefine vous itinéraires en fonction de routage toocontrol règles où votre concentrateur envoie les messages appareil-à-cloud. Règles de routage ne nécessitent pas de vous toowrite n’importe quel code et peuvent avoir lieu hello de répartiteurs de message après réception personnalisé.

* **Surveillance des opérations de connectivité des appareils**. Vous pouvez recevoir des journaux d’opérations détaillés sur les opérations de gestion de l’identité des appareils et sur les événements de connectivité des appareils. Cette fonctionnalité d’analyse permet à vos problèmes de connectivité IoT solution tooidentify, telles que les périphériques qui tentent de tooconnect avec les informations d’identification incorrectes, envoyer des messages trop fréquemment ou rejeter tous les messages cloud-à-appareil.

* **Un ensemble complet de bibliothèques d’appareils**. Les [Kits de développement logiciel (SDK) d’appareils Azure IoT][lnk-device-sdks] sont disponibles et pris en charge pour différents langages et plateformes : C pour de nombreuses distributions Linux, Windows et les systèmes d’exploitation en temps réel. Les Kits de développement logiciel (SDK) d’appareil Azure IoT prennent également en charge les langages gérés tels que C#, Java et JavaScript.

* **Protocoles et possibilités d’extension IoT**. Si votre solution ne peut pas utiliser les bibliothèques d’appareil hello, IoT Hub expose un protocole publique qui permet des périphériques toonatively utilisation hello MQTT v3.1.1, HTTP 1.1 ou AMQP 1.0 protocoles. Vous pouvez également étendre toosupport IoT Hub pour les protocoles personnalisés par :

  * Création d’une passerelle de champ avec [Azure IoT bord] [ lnk-iot-edge] qui convertit votre tooone de protocole personnalisé de hello trois protocoles compris par IoT Hub.
  * Personnalisation hello [passerelle de protocole Azure IoT][protocol-gateway], un composant open source qui s’exécute dans le cloud de hello.

* **Mettant à l’échelle**. IoT Hub Azure redimensionne toomillions des périphériques connectés simultanément des millions d’événements par seconde.

## <a name="gateways"></a>Passerelles

Une passerelle dans une solution IoT est généralement un [passerelle de protocole] [ lnk-iotedge] qui est déployé dans le cloud de hello ou un [passerelle de champ] [ lnk-field-gateway] qui est déployé localement avec vos appareils. Une passerelle de protocole effectue la traduction de protocole, par exemple MQTT tooAMQP. Une passerelle de champ peut exécuter l’analytique sur les bords de hello, des décisions temps tooreduce latence, fournir des services de gestion de périphérique, appliquer des contraintes de la confidentialité et de sécurité et également effectuer la traduction de protocole. Les deux types de passerelle agissent comme intermédiaire entre vos appareils et votre IoT Hub.

Une passerelle de champ est différente d’un appareil de routage de trafic simple, par exemple un pare-feu ou un appareil de traduction d’adresses réseau, car elle a généralement un rôle actif dans la gestion de l’accès et du flux des informations dans votre solution.

Une solution peut inclure des passerelles de protocole et de champ.

## <a name="how-does-iot-hub-work"></a>Comment IoT Hub fonctionne-t-il ?

IoT Hub Azure implémente hello [assistée par le service de communication] [ lnk-service-assisted-pattern] interactions de hello toomediate modèle entre vos appareils et votre solution back-end. Hello assistée par le service de communication vise tooestablish digne de confiance, chemins de communication bidirectionnelle entre un système de contrôle, tels que IoT Hub et les appareils à usage spécial qui sont déployés dans un espace physique non approuvé. modèle de Hello établit hello suivant principes :

* La sécurité est prioritaire sur toutes les autres fonctionnalités.

* Les appareils n’acceptent pas les informations réseau non sollicitées. Un appareil établit tous les itinéraires et connexions pour le trafic sortant uniquement. Pour un périphérique tooreceive une commande à partir de hello solution back-end, les appareil de hello doit lancer régulièrement un toocheck de connexion pour n’importe quel tooprocess de commandes en attente.

* Les appareils doivent se connecter uniquement tooor établir des services de toowell connue d’itinéraires qu’ils sont appariés, telles que IoT Hub.

* voie de communication Hello entre l’appareil et le service ou entre périphérique et de la passerelle est sécurisé au niveau de la couche de protocole d’application hello.

* L’authentification et l’autorisation au niveau du système sont basées sur les identités par appareil. Les autorisations et informations d’identification sont ainsi révocables presque instantanément.

* La communication bidirectionnelle pour les appareils qui se connectent toopower échéance sporadique ou des problèmes de connectivité est facilitée par contenant les commandes et les notifications de périphérique jusqu'à ce qu’un périphérique connecte tooreceive les. IoT Hub conserve les files d’attente spécifique à l’appareil pour qu’il envoie des commandes de hello.

* Données de charge utile d’application sont sécurisées séparément pour le transit protégé via le service de passerelles tooa particulier.

Hello secteur mobile a utilisé modèle de communication d’assistance de service hello au niveau des services de notification push de montée en puissance énorme tooimplement comme [Services de notifications Push Windows][lnk-wns], [Messagerie Cloud Google][lnk-google-messaging], et [Apple Push Notification Service][lnk-apple-push].

IoT Hub est pris en charge sur le chemin d’accès d’homologation publique ExpressRoute.

## <a name="next-steps"></a>Étapes suivantes

toolearn comment toosend des messages à partir d’un appareil et les recevoir d’IoT Hub, ainsi que comment tooconfigure message route, consultez [envoyer et recevoir des messages avec IoT Hub][lnk-send-messages].

toolearn IoT Hub permet la gestion de périphérique basé sur des normes pour vous tooremotely gérer, configurer et mettre à jour vos appareils, voir [vue d’ensemble de gestion des appareils avec IoT Hub][lnk-device-management].

tooimplement les applications clientes sur un large éventail de plateformes d’appareils matériels et les systèmes d’exploitation, vous pouvez utiliser le dispositif de Azure IoT hello kits de développement logiciel. Appareil de Hello SDK inclut des bibliothèques qui facilitent l’envoi télémétrie tooan IoT hub et la réception messages cloud-à-appareil. Lorsque vous utilisez le périphérique hello kits de développement logiciel, vous pouvez choisir parmi différentes toocommunicate de protocoles de réseau avec IoT Hub. toolearn, voir hello [plus d’informations sur les kits de développement logiciel de périphérique][lnk-device-sdks].

tooget route écrire du code et en cours d’exécution des exemples, consultez hello [prise en main IoT Hub] [ lnk-get-started] didacticiel.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Communication de service assistée, billet de blog de Clemens Vasters"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
