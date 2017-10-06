---
title: aaaAzure glossaire IoT Hub | Documents Microsoft
description: "Guide du développeur - un glossaire des termes courants relatifs tooAzure IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>Glossaire des termes d’IoT Hub
Cet article présente certains des termes courants de hello utilisés Bonjour les articles IoT Hub.

## <a name="advanced-message-queueing-protocol"></a>Advanced Message Queuing Protocol
[Advanced Message Queuing Protocol (AMQP)](https://www.amqp.org/) est un des échanges de hello protocoles que [IoT Hub](#iot-hub) prend en charge pour communiquer avec les appareils. Pour plus d’informations sur hello protocoles IoT Hub prend en charge de messagerie, consultez [envoyer et recevoir des messages avec IoT Hub](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>Interface de ligne de commande Azure
Hello [CLI d’Azure](../cli-install-nodejs.md) est un outil de commande multiplateforme open source, basée sur l’interpréteur de commandes pour créer et gérer des ressources de Microsoft Azure. Cette version de hello CLI est implémentée à l’aide de Node.js.

## <a name="azure-cli-20"></a>Azure CLI 2.0
Hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) est un outil de commande multiplateforme open source, basée sur l’interpréteur de commandes pour créer et gérer des ressources de Microsoft Azure. Cette version préliminaire du hello CLI est implémentée à l’aide de Python.


## <a name="azure-iot-device-sdks"></a>Kits Azure IoT device SDK
Il n’y _appareil kits de développement logiciel_ disponible pour plusieurs langages qui vous permettent de toocreate [des applications pour appareil](#device-app) qui interagissent avec un hub IoT. Hello IoT Hub didacticiels montrent comment toouse ces SDK de l’appareil. Vous trouverez plus d’informations sur l’appareil hello kits de développement logiciel et de code source de hello dans cette GitHub [référentiel](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
IoT bord vous permet aux applications toowrite activer toocommunicate appareils connectés à la passerelle avec [IoT Hub](#iot-hub). Hello IoT bord didacticiels montrent comment toouse ce service. Vous trouverez plus d’informations sur Azure IoT bord et de code source de hello dans cette GitHub [référentiel](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>Kits Azure IoT service SDK
Il n’y _kits de développement logiciel de service_ disponible pour plusieurs langages qui vous permettent de toocreate [principal applications](#back-end-app) qui interagissent avec un hub IoT. Hello IoT Hub didacticiels montrent comment toouse ces services SDK. Vous trouverez plus d’informations sur le service hello kits de développement logiciel et de code source de hello dans cette GitHub [référentiel](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Portail Azure
Hello [portail Microsoft Azure](https://portal.azure.com) est un emplacement central où vous pouvez configurer et gérer vos ressources Azure. Son contenu est organisé à l’aide de _panneaux_. Dans certains des didacticiels de Hub IoT hello, vous devrez peut-être toouse hello [portail Azure classic](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) est une collection d’applets de commande, vous pouvez utiliser toomanage Azure avec Windows PowerShell. Vous pouvez utiliser hello applets de commande toocreate, tester, déployer et gérer des solutions et services fournis par le biais hello plateforme Azure.

## <a name="azure-resource-manager"></a>Azure Resource Manager
[Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) vous permet de toowork des ressources de hello dans votre solution en tant que groupe. Vous pouvez déployer, mettre à jour ou supprimer des ressources de hello pour votre solution dans une opération unique et coordonnée.

## <a name="azure-service-bus"></a>Azure Service Bus
[Service Bus](../service-bus/index.md) fournit activé pour le cloud les communications avec la messagerie d’entreprise et relayée qui vous permet de connectent des solutions sur site avec le cloud de hello. Certains didacticiels concernant IoT Hub utilisent des [files d’attente](../service-bus-messaging/service-bus-messaging-overview.md) Service Bus.

## <a name="azure-storage"></a>Stockage Azure
Le service [Stockage Azure](../storage/common/storage-introduction.md) est une solution de stockage cloud. Il inclut le service de stockage d’objets Blob hello que vous pouvez utiliser toostore non structurée l’objet de données. Certains didacticiels concernant IoT Hub utilisent le service Stockage Blob.

## <a name="back-end-app"></a>Application principale
Dans le contexte de hello de [IoT Hub](#iot-hub), une application back-end est une application qui se connecte tooone de points de terminaison de service côté hello sur un hub IoT. Par exemple, une application back-end peut extraire [appareil-à-cloud](#device-to-cloud)messages ou gérer hello [Registre des identités](#identity-registry). En règle générale, une application principale s’exécute dans le cloud de hello, mais dans la plupart des didacticiels de hello hello principal applications sont des applications de console en cours d’exécution sur votre ordinateur de développement local.

## <a name="built-in-endpoints"></a>Points de terminaison intégrés
Chaque hub IoT inclut un [point de terminaison](iot-hub-devguide-endpoints.md) intégré compatible avec Event Hub. Vous pouvez utiliser n’importe quel mécanisme qui fonctionne avec des concentrateurs d’événements tooread appareil-à-cloud messages à partir de ce point de terminaison.

## <a name="cloud-gateway"></a>Passerelle cloud
Une passerelle de cloud permet de connecter des périphériques qui ne peut pas se connecter directement trop[IoT Hub](#iot-hub). Une passerelle de cloud est hébergée dans le cloud hello dans contraste tooa [passerelle de champ](#field-gateway) qui exécute les appareils tooyour local. Un cas d’utilisation classiques pour une passerelle de cloud est la traduction de protocole tooimplement pour vos appareils.

## <a name="cloud-to-device"></a>Cloud-à-appareil
Fait référence toomessages envoyés à partir d’un équipement tooa IoT hub. Souvent, ces messages sont des commandes qui commandent aux hello appareil tootake une action. Pour plus d’informations, consultez [Envoyer et recevoir des messages avec IoT Hub](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Chaîne de connexion
Vous utilisez des chaînes de connexion dans votre application code tooencapsulate hello informations requises tooconnect tooan point de terminaison. Une chaîne de connexion comprend généralement hello l’adresse de point de terminaison hello et les informations de sécurité, mais les services varient selon les formats de chaîne de connexion. Il existe deux types de chaîne de connexion associée hello IoT Hub service :
- *Chaînes de connexion de périphérique* activer les périphériques tooconnect toohello périphérique points de terminaison sur un hub IoT.
- *Chaînes de connexion de IoT Hub* activer des applications du serveur principal tooconnect toohello orientées service points de terminaison sur un hub IoT.

## <a name="custom-endpoints"></a>Points de terminaison personnalisés
Vous pouvez créer personnalisé [points de terminaison](iot-hub-devguide-endpoints.md) sur une toodeliver de hub IoT messages distribués par un [règle de routage](#routing-rules). Points de terminaison personnalisés vous connecter directement tooan concentrateur d’événements, une file d’attente Service Bus ou une rubrique Service Bus.

## <a name="custom-gateway"></a>Passerelle personnalisée
Une passerelle permet de connecter des périphériques qui ne peut pas se connecter directement trop[IoT Hub](#iot-hub). Vous pouvez utiliser [Azure IoT bord](#azure-iot-edge) toobuild passerelles personnalisées qui implémentent la logique personnalisée toohandle messages, les conversions de protocole personnalisé et autres traitements sur hello edge.

## <a name="data-point-message"></a>Message de point de données
Un message de point de données est un message [appareil-à-cloud](#device-to-cloud) qui contient des données de [télémétrie](#telemetry) telles que la vitesse du vent ou la température.

## <a name="desired-configuration"></a>Configuration souhaitée
Dans le contexte de hello d’un [double de l’appareil](iot-hub-devguide-device-twins.md), souhaitée de configuration fait référence l’ensemble des propriétés et des métadonnées en double périphérique hello qui doit être synchronisée avec le périphérique de hello toohello.

## <a name="desired-properties"></a>Propriétés souhaitées
Dans le contexte de hello d’un [double de l’appareil](iot-hub-devguide-device-twins.md), souhaité de propriétés est une sous-section de double périphérique hello qui est utilisé avec [signalé propriétés](#reported-properties) toosynchronize configuration de l’appareil ou d’une condition. Propriétés souhaitées peuvent uniquement être définies un [applications principal](#back-end-app) et sont respectées par hello [application pour appareil](#device-app).

## <a name="device-to-cloud"></a>Appareil-à-cloud
Fait référence toomessages envoyés à partir d’un appareil connecté trop[IoT Hub](#iot-hub). Ces messages peuvent être des messages de [point de données](#data-point-message) ou [interactifs](#interactive-message). Pour plus d’informations, consultez [Envoyer et recevoir des messages avec IoT Hub](iot-hub-devguide-messaging.md).

## <a name="device"></a>Appareil
Dans le contexte de hello de IoT, une unité est en général un appareil informatique autonome à petite échelle, qui peut collecter des données ou un contrôle d’autres périphériques. Par exemple, un périphérique peut être un dispositif de surveillance de l’environnement ou d’un contrôleur pour les systèmes de ventilation et d’abreuvement hello dans une occurrence. Hello [catalogue périphérique](https://catalog.azureiotsuite.com/) fournit une liste de toowork certifiés de périphériques matériels avec [IoT Hub](#iot-hub).

## <a name="device-app"></a>Application pour appareil
Une application s’exécute sur votre [périphérique](#device) et handles hello communication avec votre [IoT hub](#iot-hub). En règle générale, vous utilisez une des hello [Azure IoT appareil kits de développement logiciel](#azure-iot-device-sdks) lorsque vous implémentez une application de périphérique. Dans la plupart des didacticiels de IoT hello, vous utilisez un [appareil simulé](#simulated-device) pour des raisons pratiques.

## <a name="device-condition"></a>Condition d’appareil
Fait référence à des informations d’état de toodevice, par exemple, méthode de connectivité hello en cours d’utilisation, comme indiqué par une [application](#device-app). Des [applications pour appareil](#device-app) peuvent également signaler leurs capacités. Vous pouvez interroger des informations de condition et de capacité en utilisant des jumeaux d’appareil.

## <a name="device-data"></a>Données d’appareil
Données de l’appareil fait référence les données de chaque appareil toohello stockées Bonjour IoT Hub [Registre des identités](#identity-registry). Il est possible de tooimport et exporter ces données.

## <a name="device-explorer"></a>Explorateur d’appareils
Hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) est un outil qui s’exécute sur Windows et permet de vous toomanage vos appareils Bonjour [Registre des identités](#identity-registry).hello outil permettre également envoyer et recevoir des périphériques tooyour de messages.

## <a name="device-identities-rest-api"></a>API REST des identités des appareils
Hello [Device identités REST API](https://docs.microsoft.com/rest/api/iothub/iothubresource) vous permet de toomanage vos appareils inscrits dans hello [Registre des identités](#identity-registry) à l’aide d’une API REST. En règle générale, vous devez utiliser un des hello de niveau supérieur [kits de développement logiciel de service](#azure-iot-service-sdks) comme Bonjour didacticiels de IoT Hub.

## <a name="device-identity"></a>Identité d’appareil
Hello identité d’appareil hello identificateur unique affecté tooevery appareil est inscrite dans hello [Registre des identités](#identity-registry).

## <a name="device-management"></a>Gestion des appareils
Gestion des appareils englobe hello complète du cycle de vie associé à la gestion des appareils hello dans votre solution IoT, y compris la planification, la configuration, configuration, analyse et mise hors service.

## <a name="device-management-patterns"></a>Modèle de gestion des appareils
[Hub IoT](#iot-hub) permet d’effectuer les opérations courantes de gestion des appareils, dont le redémarrage, les réinitialisations aux paramètres d’usine et les mises à jour de microprogramme.

## <a name="device-messaging-rest-api"></a>API REST de messagerie des appareils
Vous pouvez utiliser hello [périphérique l’API REST de messagerie](https://docs.microsoft.com/rest/api/iothub/httpruntime) tooan IoT hub des messages à partir d’un appareil toosend appareil-à-cloud et recevoir [cloud-à-appareil](#cloud-to-device) messages à partir d’un hub IoT. En règle générale, vous devez utiliser un des hello de niveau supérieur [appareil kits de développement logiciel](#azure-iot-device-sdks) comme Bonjour didacticiels de IoT Hub.

## <a name="device-provisioning"></a>Approvisionnement des appareils
La configuration de périphériques consiste à hello ajout initial de hello [données de l’appareil](#device-data) toohello stocke dans votre solution. tooenable un nouveau concentrateur de tooyour tooconnect de périphérique, vous devez ajouter un toohello de ID et les clés des appareils IoT Hub [Registre des identités](#identity-registry). Dans le cadre du processus d’approvisionnement de hello, vous devrez peut-être tooinitialize des données dans d’autres banques de la solution.

## <a name="device-twin"></a>Jumeau d’appareil
Un [jumeau d’appareil](iot-hub-devguide-device-twins.md) est un document JSON contenant des informations d’état d’appareil telles que des métadonnées, des configurations et des conditions. [IoT Hub](#iot-hub) conserve une représentation d’appareil pour chaque appareil que vous configurez dans votre IoT Hub. Jumeaux du périphérique permettre de toosynchronize [conditions de périphérique](#device-condition) et configurations entre l’appareil de hello et solution de hello back-end. Vous pouvez interroger les périphériques jumeaux toolocate spécifiques et les périphériques et interroger le statut d’opérations de longue hello.

## <a name="device-twin-queries"></a>Requêtes de jumeaux d’appareil
[Requêtes de double périphérique](iot-hub-devguide-query-language.md) utilisez hello les informations de jumeaux de votre appareil tooretrieve de la langue de requête de type SQL IoT Hub. Vous pouvez utiliser hello même IoT Hub requête informations de langue tooretrieve sur [travaux](#job) en cours d’exécution dans votre hub IoT.

## <a name="device-twin-rest-api"></a>API REST Jumeau d’appareil
Vous pouvez utiliser hello [Device double REST API](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) à partir de la solution de hello en principale toomanage jumeaux de votre appareil. Hello API vous permet de mise à jour et tooretrieve [double de l’appareil](#device-twin) propriétés et appeler [direct de méthodes](#direct-method). En règle générale, vous devez utiliser un des hello de niveau supérieur [kits de développement logiciel de service](#azure-iot-service-sdks) comme Bonjour didacticiels de IoT Hub.

## <a name="device-twin-synchronization"></a>Synchronisation de jumeau d’appareil
Synchronisation du périphérique double utilise hello [propriétés souhaitée](#desired-properties) dans votre tooconfigure jumeaux de périphérique vos appareils et les récupérer [a signalé des propriétés](#reported-properties) à partir de votre toostore de périphériques en double de périphérique hello.

## <a name="direct-method"></a>Méthode directe
A [méthode directe](iot-hub-devguide-direct-methods.md) est un moyen de vous tootrigger un tooexecute de méthode sur un appareil en appelant une API sur votre hub IoT.

## <a name="endpoint"></a>Point de terminaison
Un hub IoT expose plusieurs [points de terminaison](iot-hub-devguide-endpoints.md) qui permettent à votre hub IoT d’applications tooconnect toohello. Périphérique de point de terminaison qui autorisent des opérations de tooperform des périphériques tels que l’envoi de [appareil-à-cloud](#device-to-cloud) messages et la réception [cloud-à-appareil](#cloud-to-device) messages. Points de terminaison côté service management qui sont [principal applications](#back-end-app) tooperform des opérations telles que [identité d’appareil](#device-identity) administration et gestion des périphériques double. Des [points de terminaison intégrés](#built-in-endpoints) visibles par le service permettent de lire des messages appareil-à-cloud. Vous pouvez créer [points de terminaison personnalisés](#custom-endpoints) tooreceive les messages appareil-à-cloud distribués par un [règle de routage](#routing-rules).

## <a name="event-hubs-service"></a>Service Event Hubs
[Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) est un service d’entrée de données hautement extensible, capable d’ingérer des millions d’événements par seconde. service de Hello vous tooprocess et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications. Pour obtenir une comparaison avec hello IoT Hub service, consultez [comparaison d’Azure IoT Hub et Azure Event Hubs](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Point de terminaison compatible Event Hub
tooread [appareil-à-cloud](#device-to-cloud) messages envoyés tooyour IoT hub, vous pouvez connecter le point de terminaison de tooan sur votre concentrateur et utiliser n’importe quel tooread de méthode de concentrateur d’événements compatibles ces messages. Incluent des méthodes compatibles avec le concentrateur d’événements à l’aide de hello [SDK concentrateurs d’événements](../event-hubs/event-hubs-programming-guide.md) et [Analytique de flux de données Azure](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Passerelle de champ
Une passerelle de champ permet de connecter des périphériques qui ne peut pas se connecter directement trop[IoT Hub](#iot-hub) et est généralement déployé localement avec vos appareils. Pour plus d’informations, voir [Qu’est-ce qu’Azure IoT Hub ?](iot-hub-what-is-iot-hub.md).

## <a name="free-account"></a>Compte gratuit
Vous pouvez créer un [libre compte Azure](https://azure.microsoft.com/pricing/free-trial/) toocomplete hello les didacticiels IoT Hub et faire des essais avec hello IoT Hub service (et autres services Azure).

## <a name="gateway"></a>Passerelle
Une passerelle permet de connecter des périphériques qui ne peut pas se connecter directement trop[IoT Hub](#iot-hub). Voir aussi [Passerelle de champ](#field-gateway), [Passerelle cloud](#cloud-gateway) et [Passerelle personnalisée](#custom-gateway).

## <a name="identity-registry"></a>Registre des identités
Hello [Registre des identités](iot-hub-devguide-identity-registry.md) est le composant intégré de hello d’un IoT hub qui stocke des informations sur les périphériques individuels hello autorisés tooconnect tooan IoT hub.

## <a name="interactive-message"></a>Message interactif
Un message interactif est un [cloud-à-appareil](#cloud-to-device) message qui déclenche une action immédiate dans hello solution back-end. Par exemple, un appareil peut envoyer une alerte sur un échec qui doit être enregistré automatiquement dans le système CRM tooa.

## <a name="iot-hub"></a>IoT Hub
IoT Hub est un service Azure entièrement géré qui permet des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un back-end de solution. Pour plus d’informations, voir [Qu’est-ce qu’Azure IoT Hub ?](iot-hub-what-is-iot-hub.md). À l’aide de votre [abonnement Azure](#subscription), vous pouvez créer des IoT hubs toohandle votre IoT les charges de travail de messagerie.

## <a name="iot-hub-metrics"></a>Métriques IoT Hub
[Métriques de IoT Hub](iot-hub-metrics.md) vous donne des données sur l’état de hello de hello IoT hubs dans votre [abonnement Azure](#subscription). Activer les mesures de IoT Hub vous tooassess hello l’intégrité globale du service de hello et les appareils de hello connecté tooit. Les métriques IoT Hub peuvent vous aider à voir ce qui se passe votre IoT hub et résoudre les problèmes de causes sans avoir besoin de toocontact prise en charge Azure.

## <a name="iot-hub-query-language"></a>Langage de requête IoT Hub
Hello [langage de requête IoT Hub](iot-hub-devguide-query-language.md) est un langage de type SQL qui vous permet de tooquery votre [travaux](#job) et jumeaux de périphérique.

## <a name="iot-hub-resource-provider-rest-api"></a>API REST de fournisseur de ressources IoT Hub
Vous pouvez utiliser hello [API REST de fournisseur de ressources IoT Hub](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage hello des IoT hubs dans votre [abonnement Azure](#subscription) opérations telles que la création, la mise à jour et la suppression des concentrateurs.

## <a name="iot-suite"></a>IoT Suite
Azure IoT Suite inclut plusieurs services Azure et des solutions préconfigurées. Ces solutions préconfigurées activer tooget rapidement opérationnel avec des implémentations de bout en bout pour des scénarios courants de IoT. Pour plus d’informations, voir [Qu’est-ce qu’Azure IoT Suite ?](../iot-suite/iot-suite-overview.md).

## <a name="iothub-explorer"></a>iothub-explorer
Hello [iothub-explorer](https://github.com/azure/iothub-explorer) est un outil de ligne de commande multiplateforme. outil de Hello permet à vos appareils Bonjour vous toomanage [Registre des identités](#identity-registry), envoyer et recevoir des messages et des fichiers à partir de vos appareils et surveiller vos opérations de hub IoT.

## <a name="job"></a>Travail
Back-end votre solution peut utiliser [travaux](iot-hub-devguide-jobs.md) tooschedule et suivre les activités sur un ensemble d’appareils inscrits avec votre IoT hub. Ces activités comprennent la mise à jour des [propriétés souhaitées](#desired-properties) de l’appareil, la mise à jour des [balises](#tags) de jumeau d’appareil et l’appel de [méthodes directes](#direct-method). [IoT Hub](#iot-hub) utilise également les travaux trop[importer tooand exportation](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) de hello [Registre des identités](#identity-registry).

## <a name="jobs-rest-api"></a>API REST Travaux
Hello [API REST de travaux](https://docs.microsoft.com/rest/api/iothub/jobapi) vous permet de toomanage [travaux](#job) en cours d’exécution dans votre hub IoT.

## <a name="module"></a>Module
Dans [Azure IoT Edge](iot-hub-linux-iot-edge-get-started.md), un [module](iot-hub-linux-iot-edge-get-started.md) est un composant qui effectue une tâche spécifique. Tâches peuvent inclure la réception d’un message à partir d’un appareil, la transformation d’un message ou l’envoi d’un IoT hub de message tooan. Un répartiteur est chargé du transfert des messages entre les modules. Azure IoT Edge inclut un ensemble d’exemples de modules. Vous pouvez également créer vos propres modules personnalisés.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) est un des échanges de hello protocoles que [IoT Hub](#iot-hub) prend en charge pour communiquer avec les appareils. Pour plus d’informations sur hello protocoles IoT Hub prend en charge de messagerie, consultez [envoyer et recevoir des messages avec IoT Hub](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>Surveillance des opérations
IoT Hub [surveillance des opérations](iot-hub-operations-monitoring.md) vous permet d’état de hello toomonitor des opérations sur votre IoT hub en temps réel. [IoT Hub](#iot-hub) suit les événements liés à différentes catégories d’opérations. Vous pouvez choisir d’envoyer des événements à partir d’une ou plusieurs catégories tooan point de terminaison IoT Hub pour le traitement. Vous pouvez analyser les données hello pour les erreurs ou configurer un traitement plus complexe basé sur des modèles de données.

## <a name="physical-device"></a>Appareil physique
Une unité physique est un appareil réel, par exemple un Pi framboises qui se connecte tooan IoT hub. Pour des raisons pratiques, la plupart des didacticiels de Hub IoT hello utilisent [simulée appareils](#simulated-device) tooenable vous toorun exemples sur votre ordinateur local.

## <a name="primary-and-secondary-keys"></a>Clés primaires et secondaires
Lorsque vous vous connectez exposés à tooa appareil ou le point de terminaison de service côté sur un hub IoT, votre [chaîne de connexion](#connection-string) inclut la clé toogrant vous accédez à. Lorsque vous ajoutez un périphérique toohello [Registre des identités](#identity-registry) ou ajouter un [stratégie d’accès partagé](#shared-access-policy) tooyour concentrateur, service de hello génère une clé primaire et secondaire. Avoir deux clés vous permet de tooroll sur à partir d’un tooanother clé lorsque vous mettez à jour une clé sans perdre de hub IoT de toohello accès.

## <a name="protocol-gateway"></a>Passerelle de protocole
Une passerelle de protocole est généralement déployée dans le cloud de hello et fournit des services de traduction pour les appareils qui se connectent trop de protocole[IoT Hub](#iot-hub). Pour plus d’informations, voir [Qu’est-ce qu’Azure IoT Hub ?](iot-hub-what-is-iot-hub.md).

## <a name="quotas-and-throttling"></a>Quotas et limitation
Il existe différentes [quotas](iot-hub-devguide-quotas-throttling.md) qui s’appliquent à utiliser tooyour [IoT Hub](#iot-hub), la plupart des hello quotas varient en fonction de la couche hello de hub IoT de hello. [IoT Hub](#iot-hub) s’applique également [limite](iot-hub-devguide-quotas-throttling.md) tooyour utiliser service de hello en cours d’exécution.

## <a name="reported-configuration"></a>Configuration signalée
Dans le contexte de hello d’un [double de l’appareil](iot-hub-devguide-device-twins.md), signalée configuration fait référence toohello le jeu complet des propriétés et métadonnées dans double périphérique hello qui doit être signalés principal toohello solution.

## <a name="reported-properties"></a>Propriétés signalées
Dans le contexte de hello d’un [double de l’appareil](iot-hub-devguide-device-twins.md), propriétés est une sous-section de hello appareil double est utilisé avec [propriétés souhaitée](#desired-properties) toosynchronize configuration de l’appareil ou d’une condition. Signalé propriétés peuvent uniquement être définies par hello [application](#device-app) et peut être lue et interrogé par un [applications principal](#back-end-app).

## <a name="resource-group"></a>Groupe de ressources
[Le Gestionnaire de ressources Azure](#azure-resource-manager) toogroup de groupes de ressources utilise les ressources associées ensemble. Vous pouvez utiliser une ressource groupe tooperform les opérations sur toutes les ressources hello sur le groupe de hello simultanément.

## <a name="retry-policy"></a>Stratégie de nouvelle tentative
Vous utilisez un toohandle de stratégie de nouvelle tentative [erreurs temporaires](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) lorsque vous vous connectez tooa le service cloud.

## <a name="routing-rules"></a>Règles de routage
Vous configurez [les règles de routage](iot-hub-devguide-messages-read-custom.md) dans votre tooa de messages appareil-à-cloud IoT hub tooroute [intégré](#built-in-endpoints) ou trop[points de terminaison personnalisés](#custom-endpoints) pour le traitement en arrière de votre solution fin.

## <a name="sasl-plain"></a>SAPL PLAIN
SASL brut est un protocole hello [AMQP](#advanced-message-queue-protocol) protocole utilise des jetons de sécurité tootransfer.

## <a name="shared-access-signature"></a>Signature d’accès partagé
Les signatures d’accès partagé (SAP) sont des mécanismes d’authentification basés sur des hachages sécurisés SHA-256 ou des URI. Une authentification par SAP comporte deux composants : une _stratégie d’accès partagé_ et une _signature d’accès partagé_ (souvent appelée jeton). Un périphérique utilise SAS tooauthenticate avec un hub IoT. [Les applications de serveur principal](#back-end-app) également utiliser SAS tooauthenticate avec des points de terminaison de service côté hello sur un hub IoT. En règle générale, vous incluez un jeton SAS hello Bonjour [chaîne de connexion](#connection-string) qu’une application utilise tooestablish un IoT hub de connexion tooan.

## <a name="shared-access-policy"></a>Stratégie d’accès partagé
Une stratégie d’accès partagé définit des autorisations hello tooanyone ayant une validité [clé primaire ou secondaire](#primary-and-secondary-keys) associé à cette stratégie. Vous pouvez gérer les stratégies d’accès hello partagé et des clés pour votre concentrateur hello [portal](#azure-portal).

## <a name="simulated-device"></a>Appareil simulé
Pour plus de commodité, nombreux hello IoT Hub didacticiels utilisent simulés tooenable périphériques vous toorun exemples sur votre ordinateur local. En revanche, un [périphérique physique](#physical-device) est un appareil réel, par exemple un Pi framboises qui se connecte tooan IoT hub.

## <a name="solution"></a>Solution
A _solution_ peuvent faire référence à des solutions de Visual Studio tooa qui inclut un ou plusieurs projets. A _solution_ peut également faire référence de solution IoT tooan qui inclut les éléments tels que des appareils, [des applications pour appareil](#device-app), un hub IoT, d’autres services Azure, et [principal applications](#back-end-app).

## <a name="subscription"></a>Abonnement
L’abonnement est le mode de facturation d’Azure. Chaque ressource ou service Azure que vous créez ou utilisez est associé à un abonnement unique. De nombreux quotas s’appliquent également au niveau de hello d’un abonnement.

## <a name="system-properties"></a>Propriétés système
Dans le contexte de hello d’un [double de l’appareil](iot-hub-devguide-device-twins.md), les propriétés système sont en lecture seule et inclure des informations concernant l’utilisation du dispositif hello comme dernier état de temps et de la connexion de l’activité.

## <a name="tags"></a>Tags
Dans le contexte de hello d’un [double de l’appareil](iot-hub-devguide-device-twins.md), les balises sont des métadonnées de périphérique stockés et récupérés par hello solution back-end sous forme de hello d’un document JSON. Les balises ne sont pas visibles tooapps sur un appareil.

## <a name="telemetry"></a>Télémétrie
Collecter les données de télémétrie, telles que la vitesse du vent ou température, de périphériques et utiliser [messages de point de données](#data-point-messages) le hub IoT tooan toosend hello télémétrie.

## <a name="token-service"></a>Service d’émission de jeton
Vous pouvez utiliser un service de jeton de tooimplement un mécanisme d’authentification pour vos appareils. Il utilise un IoT Hub [stratégie d’accès partagé](#shared-access-policy) avec **DeviceConnect** autorisations toocreate *étendue de périphérique* jetons. Ces jetons activer un hub IoT de périphérique tooconnect tooyour. Un appareil utilise un tooauthenticate du mécanisme d’authentification personnalisé avec un service de jeton de hello. Si l’appareil de hello est correctement authentifié, service de jeton de hello émet un jeton SAP pour hello appareil toouse tooaccess votre hub IoT.

## <a name="x509-client-certificate"></a>Certificat client X.509
Un périphérique peut utiliser un tooauthenticate de certificat X.509 avec [IoT Hub](#iot-hub). À l’aide d’un certificat X.509 est un autre toousing un [jeton SAS](#shared-access-signature).
