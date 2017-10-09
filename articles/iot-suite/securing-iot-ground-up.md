---
title: "aaaSecuring votre Internet des objets à partir de hello d’arrière-plan des | Documents Microsoft"
description: "Cet article décrit les fonctionnalités de sécurité intégrée hello Hello Microsoft Azure IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 10252dfa-8313-4a97-9bd6-a3f1345dd3be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: a97e8cea753641e1e3c895f44e3fde1e5739d665
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-from-hello-ground-up"></a>Hello d’arrière-plan la sécurité Internet des objets
Hello Internet of Things (IoT) constitue un unique sécurité, confidentialité et la conformité défis toobusinesses dans le monde entier. Contrairement à la technologie cyber traditionnel où ces problèmes sont axés sur les logiciels et la façon dont il est implémenté, IoT concerne que se passe-t-il quand les cyber hello et des mondes physique hello convergent. Protection IoT solutions requiert vous être assuré de la configuration sécurisée des appareils, une connectivité sécurisée entre ces appareils et hello cloud et protection des données sécurisées dans le cloud de hello pendant le traitement et de stockage. Cependant, les appareils avec contraintes de ressources, la répartition géographique des déploiements et le grand nombre d’appareils inclus au sein d’une solution vont à l’encontre de ces fonctionnalités.

Cet article explore comment hello Microsoft Azure IoT Suite offre une solution de cloud Internet des objets de sécurité et la confidentialité. Hello Azure IoT Suite offre une solution de bout en bout complète, avec la sécurité intégrée à chaque étape de hello d’arrière-plan. Chez Microsoft, le développement de logiciels sécurisés fait partie des pratiques d’ingénierie logicielle hello, enracinée dans notre décennies longue expérience de développement de logiciels sécurisés. tooensure, du cycle de vie de développement de sécurité (SDL) est hello fondamentaux méthodologie de développement, associée à un ordinateur hôte au niveau de l’infrastructure de services de sécurité tels que garantie de sécurité opérationnel (OSA) et hello Digital Crimes Unit, Microsoft Security Response Center et le centre de Protection Microsoft contre les programmes malveillants. 

Bonjour Azure IoT Suite offre des fonctionnalités uniques, qui rendent l’approvisionnement, la connexion à et le stockage des données à partir des appareils IoT faciles et transparents, et, le plus sûr. Dans cet article, nous examinerons des fonctionnalités de sécurité Azure IoT Suite hello et déploiement stratégies tooensure sécurité, confidentialité et la conformité de la solution est traitée. 

## <a name="introduction"></a>Introduction
Hello Internet of Things (IoT) wave hello Hello future, proposant ainsi aux entreprises immédiats et les coûts de tooreduce opportunités réelles, augmenter le chiffre d’affaires, transformer leur entreprise. De nombreuses entreprises, cependant, sont toodeploy hésitent IoT dans leur organisation échéance tooconcerns sur la sécurité, confidentialité et la conformité. Un point important posant problème provient de l’unicité de hello de l’infrastructure de IoT hello, qui fusionne les cyber hello et mondes physiques ensemble, des risques inhérents à ces deux mondes de composition. Sécurité de IoT concernant l’intégrité de hello tooensuring de code en cours d’exécution sur les appareils, en fournissant l’authentification utilisateur et appareil, définition claire de la propriété des périphériques (ainsi que les données générées par ces appareils) et en cours toocyber résilient et les attaques physiques. 

Ensuite, il est problème hello de confidentialité. Les entreprises exigent de la transparence vis-à-vis de la collecte de données. Elles veulent savoir ce qui est collecté, pourquoi, qui peut voir les données, qui en contrôle l’accès, etc. Enfin, il existe des problèmes de sécurité générale de l’équipement de hello, ainsi que les personnes hello leur fonctionnement et conservation des normes de conformité.

Étant donné les problèmes de conformité, de confidentialité, de transparence et de sécurité de hello, en choisissant le bon fournisseur de solutions IoT hello demeure un défi. Assemblage des éléments individuels de IoT logiciel et les services fournis par plusieurs fournisseurs introduit des lacunes dans la sécurité, de confidentialité, de transparence et de conformité qui peut-être être toodetect dur, sans parler de résoudre. choix de Hello de droite de hello IoT fournisseur de service et du logiciel est basé sur la recherche de fournisseurs qui possèdent une grande expérience exécutant les services qui s’étendent sur verticales et des zones géographiques différentes, mais sont également en mesure de tooscale de manière sécurisée et transparente. De même, il est utile pour hello sélectionné fournisseur toohave ans d’expérience de développement de logiciels sécurisés en cours d’exécution sur des milliards d’ordinateurs dans le monde entier, et paysage des menaces hello capacité tooappreciate hello posées par ce nouveau monde de hello Internet de Choses.

## <a name="secure-infrastructure-from-hello-ground-up"></a>Infrastructure de sécurité à partir de hello d’arrière-plan
Hello [Microsoft Cloud](https://www.microsoft.com/enterprise/microsoftcloud/default.aspx#fbid=WzBsRQi6aGk) infrastructure prend en charge les clients de plus d’un milliard de 127 pays. Dessiner sur notre expérience décennies de longueur de création de logiciels d’entreprise et en cours d’exécution des hello plus grands services en ligne dans Bonjour, nous fournissons des niveaux plus élevés de sécurité renforcée, confidentialité, conformité et de pratiques de prévention que la plupart des clients pourrait obtenir sur leurs propres.

Notre [du cycle de vie de développement de sécurité (SDL)](https://www.microsoft.com/sdl/) fournit un processus de développement de société obligatoire qui incorpore les exigences de sécurité dans toute hello du cycle de vie. toohelp vous assurer que les activités opérationnelles suivent hello même niveau de pratiques de sécurité, nous utilisons les instructions de sécurité rigoureux disposées dans nos processus opérationnels sécurité Assurance (OSA). Nous travaillons également avec des entreprises d’audit tiers pour la vérification en cours que nous répondent à nos obligations de conformité, et nous prendre part aux efforts d’étendue de sécurité via la création de hello de centres d’excellence, y compris hello Digital Crimes Unit, Microsoft Security Centre de réponse et centre de Protection Microsoft contre les programmes malveillants.

## <a name="microsoft-azure---secure-iot-infrastructure-for-your-business"></a>Microsoft Azure : une infrastructure IoT sécurisée pour votre entreprise
Microsoft Azure offre une solution complète du cloud, qui associe une collection constamment des services cloud intégré — analytique, apprentissage, stockage, sécurité, mise en réseau et web, avec une meilleure protection du toohello engagement et la confidentialité de vos données. Notre [supposent violation](https://azure.microsoft.com/blog/red-teaming-using-cutting-edge-threat-simulation-to-harden-the-microsoft-enterprise-cloud/) stratégie utilise « rouge d’une équipe « experts en sécurité logiciels qui simuler des attaques, test de capacité hello de Azure toodetect, protection contre les menaces émergentes et récupérer à partir de violations. Notre [réponse aux incidents global](https://www.microsoft.com/TrustCenter/Security/DesignOpSecurity) équipe travaille autour hello d’horloge toomitigate les effets de hello des attaques malveillantes. équipe de Hello suit les procédures établies pour la gestion des incidents, de communication et de récupération et utilise les interfaces détectables et prévisibles avec des partenaires internes et externes.

Nos systèmes assurent une détection des intrusions et une prévention continues, une prévention contre les attaques de service et des tests d’intrusion réguliers. Ils offrent également des outils d’investigation qui permettent d’identifier et d’atténuer les menaces. [L’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication.md) fournit une couche supplémentaire de sécurité pour les utilisateurs finaux tooaccess hello réseau. Et pour l’application hello et le fournisseur d’hébergement hello, nous proposons de contrôle d’accès, la surveillance, logiciels anti-programme malveillant, analyse de la vulnérabilité, correctifs et gestion de la configuration.

Hello Microsoft Azure IoT Suite tire parti de la sécurité de hello et confidentialité intégrée hello plateforme Azure, ainsi que nos processus SDL et OSA pour développement sécurisé et l’opération de tous les logiciels Microsoft. Ces procédures fournissent la protection de l’infrastructure, la protection du réseau et gestion des identités et sécurité toohello fondamental de fonctionnalités d’une solution. 

Hello [Azure IoT Hub](../iot-hub/iot-hub-what-is-iot-hub.md) dans hello [IoT Suite](iot-suite-what-is-azure-iot.md) propose un service entièrement géré qui permet de fiable et sécurisée des communications bidirectionnelles entre les appareils IoT et services Azure tels que [Azure Machine Learning](../machine-learning/machine-learning-what-is-machine-learning.md) et [Analytique de flux de données Azure](../stream-analytics/stream-analytics-introduction.md) à l’aide des informations d’identification de sécurité par périphérique et de contrôle d’accès.

toobest communiquer des fonctionnalités de sécurité et confidentialité intégrées hello Azure IoT Suite, nous avons divisé suite hello en trois zones de sécurité principal hello. 

![Azure IoT Suite](media/securing-iot-ground-up/securing-iot-ground-up-fig3.png)

### <a name="secure-device-provisioning-and-authentication"></a>Approvisionnement et authentification sécurisés des appareils
Hello Azure IoT Suite permet de sécuriser les appareils pendant qu’elles sont dans le champ de hello en fournissant une clé d’identité unique pour chaque périphérique, ce qui peut être utilisé par hello IoT infrastructure toocommunicate avec l’appareil de hello lorsqu’il est en opération. processus de Hello est rapide et facile tooset haut. Hello clé générée à base hello ID formulaires sélectionnés par l’utilisateur de périphérique d’un jeton utilisé dans toutes les communications entre le périphérique de hello et hello Azure IoT Hub.

Les ID d’appareil peuvent être associés à un appareil lors de la fabrication (flashés dans un module matériel de confiance) ou utiliser une identité fixe existante en tant que proxy (par exemple, les numéros de série de processeur). Étant donné que la modification de ces périphérique de hello des informations d’identification n’est pas simple, il est important toointroduce ID de périphérique logique hello sous-jacent périphérique matériel modifications, mais reste d’unité logique hello hello identiques. Dans certains cas, association hello d’une identité d’appareil peut se produire au moment du déploiement appareil (par exemple, un ingénieur authentifié physiquement configure un nouvel appareil lors de la communication avec le serveur principal solution hello). Hello [Registre des identités Azure IoT Hub](../iot-hub/iot-hub-devguide.md) fournit le stockage sécurisé des identités des appareils et des clés de sécurité pour une solution. Individuelles ou des groupes d’identités d’appareil peuvent être ajoutés tooan autorise la liste ou une liste de blocs, l’activation du contrôle total sur l’accès à l’appareil.

Stratégies de contrôle d’accès Azure IoT Hub dans le cloud de hello activer l’activation et désactivation de toute identité de l’appareil, en fournissant un moyen toodisassociate un appareil à partir d’un déploiement IoT à la demande. Cette association et cette dissociation d’appareils sont basées sur l’identité de chaque appareil.

Fonctionnalités de sécurité d’appareil supplémentaires hello suivants :

* Les appareils n’acceptent pas les connexions réseau non sollicitées. Ils établissent tous les itinéraires et connexions pour le trafic sortant uniquement. Pour un périphérique tooreceive une commande à partir du serveur principal de hello, appareil de hello doit lancer une toocheck de connexion pour n’importe quel tooprocess de commandes en attente. Une fois qu’une connexion entre l’appareil de hello et IoT Hub est établie en toute sécurité, de messagerie à partir de hello cloud toohello appareil et de périphérique toohello cloud peut être envoyé en toute transparence.  
* Périphériques de connectent uniquement tooor établir des services de toowell connue d’itinéraires avec lequel ils sont appariés, par exemple un Azure IoT Hub.
* L’autorisation et l’authentification au niveau du système utilisent des identités par appareil. Les informations d’identification et autorisations d’accès sont ainsi révocables quasi instantanément.

### <a name="secure-connectivity"></a>Connectivité sécurisée
La durabilité de la messagerie est une fonctionnalité importante de toute solution IoT. Hello devez toodurably distribution des commandes et/ou recevoir des données à partir d’appareils est souligné par fait hello que les appareils IoT sont connectés via hello Internet ou d’autres réseaux similaire qui permettre ne pas être fiables. IoT Hub Azure offre la durabilité de la messagerie entre le cloud et aux appareils via un système d’accusés de réception dans la réponse toomessages. Une durabilité supplémentaire pour la messagerie est obtenue par les messages Bonjour IoT Hub pour les jours tooseven de télémétrie et de deux jours pour les commandes de mise en cache.

L’efficacité est conservation tooensure importante des ressources et d’opération dans un environnement de ressources limitées. HTTPS (HTTP sécurisé), version sécurisée de norme hello du protocole http populaire hello est pris en charge par Azure IoT Hub, l’activation d’une communication efficace. Les protocoles AMQP (Advanced Message Queuing Protocol) et MQTT (Message Queuing Telemetry Transport), pris en charge par Azure IoT Hub, sont conçus non seulement pour leur efficacité en termes d’utilisation des ressources, mais également pour leur fiabilité en matière de remise des messages. 

L’évolutivité nécessite toosecurely de capacité hello interagir avec un large éventail de périphériques. IoT hub Azure permet aux périphériques connexion sécurisée tooboth IP activé et non compatible IP. Périphériques IP sont toodirectly en mesure de se connecter et communiquer avec hello IoT Hub via une connexion sécurisée. Les appareils non-IP présentent des contraintes de ressources et se connectent uniquement avec des protocoles de communication de courte distance, tels que Zwave, ZigBee et Bluetooth. Une passerelle de champ est tooaggregate utilisé ces périphériques et exécute le protocole traduction tooenable sécuriser la communication bidirectionnelle avec le cloud de hello.

Les fonctionnalités de sécurité de connexion supplémentaires hello suivants :

* Hello voie de communication entre les périphériques et Azure IoT Hub, ou entre les passerelles et Azure IoT Hub, sécurisée à l’aide de la norme sécurité TLS (Transport Layer) avec Azure IoT Hub est authentifié à l’aide du protocole X.509.
* Dans les appareils tooprotect ordre à partir des connexions entrantes non sollicitées, Azure IoT Hub n’ouvre pas de n’importe quel appareil toohello de connexion. Appareil de Hello démarre toutes les connexions. 
* IoT Hub Azure stocke les messages pour les appareils durablement et attend que hello périphérique tooconnect. Ces commandes sont stockées pendant deux jours, l’activation des appareils qui se connectent par intermittence, en raison de problèmes de connectivité ou toopower, tooreceive ces commandes. Azure IoT Hub gère une file d’attente spécifique pour chaque appareil.

### <a name="secure-processing-and-storage-in-hello-cloud"></a>Traitement sécurisé et stockage dans le cloud de hello
À partir des données de tooprocessing les communications chiffrées dans le cloud de hello, hello Azure IoT Suite permet de sécuriser les données. Il fournit le chiffrement supplémentaire tooimplement de flexibilité et de gestion de clés de sécurité. À l’aide d’Azure Active Directory (AAD) pour l’autorisation et l’authentification des utilisateurs, Azure IoT Suite peut fournir un modèle d’autorisation basée sur une stratégie pour les données dans le cloud de hello, activation de la gestion d’un accès facile pouvant être auditée et examinée. Ce modèle permet également de révocation quasi instantanée de toodata d’accès dans le cloud de hello et toohello connecté d’appareils Azure IoT Suite.

Une fois que les données sont dans le cloud de hello, peuvent être traitée et stockée dans les flux de travail définis par l’utilisateur. Partie de tooeach d’accès de données de hello est contrôlée avec Azure Active Directory, en fonction du service de stockage hello utilisé.

Toutes les clés utilisées par l’infrastructure de IoT hello sont stockés dans le cloud hello dans le stockage sécurisé, avec tooroll de capacité hello au cas où les clés doivent toobe redéployée. Données peuvent être stockées dans [base de données Azure Cosmos](../documentdb/documentdb-introduction.md) ou dans [bases de données SQL](../sql-database/sql-database-faq.md), l’activation de la définition du niveau de hello de sécurité souhaité. En outre, Azure fournit un moyen toomonitor et d’audit de tous les accès tooyour données tooalert vous de toute intrusion ou d’un accès non autorisé.

## <a name="conclusion"></a>Conclusion
Hello Internet of Things commence par votre choses : hello choses qui vous intéressent. la plupart des toobusinesses. IoT peut offrir de fantastiques tooa métiers en réduisant les coûts, l’augmentation de chiffre d’affaires et transformation d’entreprise. Réussite de cette transformation dépend en grande partie hello droite IoT et du service fournisseur de choix. Il s’agit de trouver un fournisseur qui va non seulement déclencher cette transformation en comprenant les besoins et les exigences de l’entreprise, mais également fournir des services et des logiciels intégrant la sécurité, la confidentialité, la transparence et la conformité comme éléments de conception essentiels. Microsoft possède une grande expérience de développement et de déploiement de services et logiciels sécurisés et continue toobe leader à l’ère de l’Internet des objets. 

Hello Microsoft Azure IoT Suite génère dans les mesures de sécurité par conception, l’activation de la surveillance sécurisé de l’efficacité de tooimprove actifs, stimuler l’innovation tooenable des performances, et emploient avancé analytique des données tootransform entreprises. Avec son approche en couches pour la sécurité, plusieurs fonctionnalités de sécurité et les modèles de conception, Azure IoT Suite permet de déployer une infrastructure qui peut être approuvée tootransform toute entreprise. 

## <a name="additional-information"></a>Informations supplémentaires
Chaque solution préconfigurée Azure IoT Suite crée des instances des services Azure, tels que les suivants hello :

* [**IoT Hub Azure**](https://azure.microsoft.com/services/iot-hub/): votre passerelle qui se connecte de cloud de hello trop « éléments ». Vous pouvez adapter toomillions de connexions par concentrateur et processus des volumes importants de données avec prise en charge de l’authentification par périphérique qui permet de sécuriser votre solution.
* [**Base de données Azure Cosmos**](https://azure.microsoft.com/services/documentdb/): un service de base de données évolutives et entièrement indexés pour des données semi-structurées qui gère les métadonnées pour les appareils hello vous configurez, telles que des attributs, la configuration et les propriétés de sécurité. Cosmos DB assure un traitement hautes performances et à débit élevé, ainsi qu’une indexation des données indépendante du schéma. Ce service offre également une interface de requête SQL enrichie.
* [**Analytique de flux de données Azure**](https://azure.microsoft.com/services/stream-analytics/): flux en temps réel de traitement dans le cloud hello toorapidly vous permet de développer et déployer un informations économiques analytique solution toouncover en temps réel à partir d’appareils, capteurs, l’infrastructure et applications. les données de salutation à partir de ce service entièrement géré peuvent évoluer tooany volume tout en atteignant un débit élevé, une latence faible et résilience.
* [**Services d’application Azure**](https://azure.microsoft.com/services/app-service/): un cloud platform toobuild puissantes applications web et mobiles qui se connectent toodata n’importe où ; dans le cloud de hello ou localement. Créez des applications mobiles attrayantes pour iOS, Android et Windows. Intégrer avec votre logiciel comme un Service (SaaS) et d’entreprise des applications avec toodozens out of box connectivité des services basés sur le cloud et applications d’entreprise. Le code dans votre langage favori et l’IDE : .NET, Node.js, PHP, Python ou Java : toobuild les applications web et API plus vite que jamais.
* [**Logique d’applications**](https://azure.microsoft.com/services/app-service/logic/): fonctionnalité de Logic Apps hello du Service d’applications Azure permet d’intégrer vos systèmes métier-IoT solution tooyour existants et d’automatiser les processus de flux de travail. Logique d’applications permet aux développeurs toodesign des flux de travail qui démarrent à partir d’un déclencheur, puis exécutent une série d’étapes, les règles et les actions qui utilisent des connecteurs puissant toointegrate avec vos processus d’entreprise. Logique d’applications offre d’emploi connectivité tooa vaste écosystème de SaaS, basé sur le cloud et des applications sur site.
* [**Stockage d’objets blob Azure**](https://azure.microsoft.com/services/storage/): stockage cloud fiable et économique pour les données hello que vos appareils envoient toohello cloud.

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la sécurisation de votre solution IoT, consultez :

* [Meilleures pratiques relatives à la sécurité IoT][lnk-security-best-practices]
* [Architecture de la sécurité IoT][lnk-security-architecture]
* [Sécuriser votre déploiement IoT][lnk-security-deployment]

[lnk-security-best-practices]: iot-security-best-practices.md
[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md

Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]
* [Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]

Vous pouvez lire sur la sécurité IoT Hub dans [tooIoT d’accès contrôle Hub] [ lnk-devguide-security] Bonjour guide du développeur IoT Hub.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
