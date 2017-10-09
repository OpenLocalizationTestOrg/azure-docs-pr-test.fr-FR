---
title: "métadonnées d’informations aaaDevice Bonjour solution de surveillance à distance | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT préconfiguré son architecture et surveillance à distance de la solution."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Métadonnées d’informations de périphérique Bonjour solution préconfigurée de surveillance à distance

Bonjour Azure IoT Suite solution préconfigurée de surveillance à distance illustre une approche pour la gestion des métadonnées de l’appareil. Cet article décrit l’approche de hello cette solution prend tooenable toounderstand vous :

* Quelle solution hello de métadonnées appareil stocke.
* Comment les solutions hello gère les métadonnées de périphérique hello.

## <a name="context"></a>Context

Hello surveillance à distance préconfiguré solution utilise [Azure IoT Hub] [ lnk-iot-hub] tooenable votre toohello de données de périphériques toosend de cloud computing. solution de Hello stocke des informations sur les périphériques dans trois emplacements différents :

| Lieu | Informations stockées | Implémentation |
| -------- | ------------------ | -------------- |
| Registre des identités | ID de l’appareil, clés d’authentification, état Activé | TooIoT intégré Hub |
| Jumeaux d’appareil | Métadonnées : propriétés signalées, propriétés souhaitées, balises | TooIoT intégré Hub |
| Cosmos DB | Historique des commandes et méthodes | Personnalisé pour la solution |

IoT Hub inclut un [Registre des identités] [ lnk-identity-registry] toomanage accéder tooan IoT hub et utilise [jumeaux de périphérique] [ lnk-device-twin] toomanage les métadonnées de périphérique . Il inclut également un *registre des appareils* spécifique à la solution de surveillance à distance qui stocke l’historique des commandes et méthodes. Hello utilise de la solution de surveillance à distance un [Cosmos DB] [ lnk-docdb] tooimplement de base de données un magasin personnalisé pour l’historique de commande et de la méthode.

> [!NOTE]
> Hello solution préconfigurée de surveillance à distance conserve Registre des identités hello périphérique synchronisé avec les informations de hello dans la base de données de la base de données Cosmos hello. Les deux utilisent hello même toouniquely d’id de périphérique identifient chaque périphérique connecté tooyour IoT hub.

## <a name="device-metadata"></a>Métadonnées de l’appareil

IoT Hub conserve un [double de l’appareil] [ lnk-device-twin] pour chaque appareil simulé et physique connecté tooa solution de surveillance à distance. solution de Hello utilise appareil jumeaux toomanage hello métadonnées associées aux périphériques. Un double de l’appareil est un document JSON maintenu par IoT Hub et les solutions hello utilise hello IoT Hub API toointeract avec jumeaux de périphérique.

Un jumeau d’appareil stocke trois types de métadonnées :

- *Signalé propriétés* sont envoyés tooan IoT hub par un périphérique. Bonjour solution de surveillance à distance, simulés périphériques les envoient les propriétés déclarées au démarrage et en réponse trop**modifier l’état de l’appareil** les méthodes et les commandes. Vous pouvez afficher les propriétés déclarées dans hello **liste des appareils** et **détails de l’appareil** dans le portail de solution hello. Les propriétés signalées sont en lecture seule.
- *Propriétés souhaitée* sont récupérés à partir du hub IoT de hello par les appareils. Il incombe hello toomake de périphérique hello aucune configuration nécessaire modifier sur l’appareil de hello. Il incombe également hello du concentrateur de hello appareil tooreport hello modification toohello arrière comme propriété signalée. Vous pouvez définir une valeur de propriété de votre choix via le portail de solution hello.
- *Balises* existe uniquement deux conteneurs de périphérique hello et ne sont jamais synchronisés avec un périphérique. Vous pouvez définir des valeurs de balise dans le portail de solution hello et les utiliser lorsque vous filtrez la liste des appareils hello. solution de Hello utilise également une toodisplay icône de balise tooidentify hello pour un périphérique dans le portail de solution hello.

Exemple a signalé de propriétés à partir d’appareils de hello simulée incluent le fabricant, le numéro de modèle, latitude et longitude. Appareils simulé hello également retour liste des méthodes prises en charge comme une propriété signalée.

> [!NOTE]
> Hello appareil simulé code utilise uniquement hello **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** hello tooupdate de propriétés souhaitées signalé a renvoyé des propriétés tooIoT concentrateur. Toutes les autres demandes de modification de propriétés souhaitées sont ignorées.

Un document de JSON appareil informations métadonnées stocké dans hello Registre Cosmos DB cette base de données a hello suivant structure :

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Informations sur l’appareil peuvent également inclure des métadonnées toodescribe hello télémétrie hello appareil envoie tooIoT Hub. solution de surveillance à distance Hello utilise cette toocustomize de métadonnées de télémétrie affichage tableau de bord hello [télémétrie dynamique][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Cycle de vie

Lorsque vous créez un périphérique dans le portail de solution hello, solution de hello crée une entrée Bonjour commande toostore de base de données Cosmos DB et l’historique de la méthode. À ce stade, les solutions hello crée également une entrée pour le périphérique de hello dans hello identité du Registre du périphérique, ce qui génère hello clés hello périphérique utilise tooauthenticate avec IoT Hub. Elle crée également un jumeau d’appareil.

Lorsqu’un périphérique connecte toohello solution d’abord, il envoie les propriétés déclarées et un message d’informations de périphérique. Hello a signalé des valeurs de propriété sont automatiquement enregistrées dans double du périphérique hello. Hello signalé propriétés incluent le fabricant du périphérique hello, numéro de modèle, numéro de série et une liste de méthodes prises en charge. message d’information Hello appareil inclut la liste hello des commandes hello prend en charge de l’appareil de hello notamment des informations sur les paramètres de commande. Lors de la solution de hello reçoit ce message, il met à jour les informations de périphérique hello dans la base de données de la base de données Cosmos hello.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Afficher et modifier les informations de périphérique dans le portail de solution hello

liste des périphériques dans le portail de solution hello Hello affiche hello suivant des propriétés de l’appareil en tant que colonnes par défaut : **état**, **DeviceId**, **fabricant**, **Numéro de modèle**, **numéro de série**, **microprogramme**, **plateforme**, **processeur**et  **Installé RAM**. Vous pouvez personnaliser les colonnes de hello en cliquant sur **éditeur colonne**. Hello des propriétés de l’appareil **Latitude** et **Longitude** lecteur emplacement hello Bonjour Bing Map sur le tableau de bord hello.

![Éditeur de colonne dans la liste des appareils][img-device-list]

Bonjour **détails de l’appareil** volet dans le portail de solution hello, vous pouvez modifier les propriétés souhaitées et des balises (signalées propriétés sont en lecture seule).

![Volet d’informations sur l’appareil][img-device-edit]

Vous pouvez utiliser hello solution tooremove portail un périphérique à partir de votre solution. Lorsque vous supprimez un appareil, les solutions hello supprime l’entrée du périphérique hello à partir du Registre des identités, puis supprime double du périphérique hello. solution de Hello supprime également le dispositif toohello connexes d’informations à partir de la base de données de la base de données Cosmos hello. Avant de pouvoir supprimer un appareil, vous devez le désactiver.

![Supprimer l’appareil][img-device-remove]

## <a name="device-information-message-processing"></a>Traitement des messages d’information d’appareil

Les messages d’information d’appareil envoyés par un appareil sont différents des messages de télémétrie. Messages d’information de périphérique incluent des commandes hello à qu'un appareil peut répondre et aucun historique de commande. IoT Hub lui-même n’a aucune connaissance des métadonnées hello contenues dans un message d’informations de périphérique et processus hello message Bonjour même manière qu’il traite les messages appareil-à-cloud. Bonjour solution de surveillance à distance un [Analytique de flux de données Azure] [ lnk-stream-analytics] travail (ASA) lit les messages hello IoT Hub. Hello **DeviceInfo** analytique de flux de travail pour les messages qui contiennent des filtres **« ObjectType » : « DeviceInfo »** et les transfère toohello **EventProcessorHost** hôte instance qui s’exécute dans une tâche web. Logique Bonjour **EventProcessorHost** instance utilise enregistrement de hello périphérique id toofind hello Cosmos DB hello mise à jour et périphérique hello enregistrement spécifique.

> [!NOTE]
> Un message d’information d’appareil est un message appareil-à-cloud standard. solution de Hello fait la distinction entre les messages d’information de périphérique et les messages de télémétrie à l’aide de requêtes ASA.

## <a name="next-steps"></a>Étapes suivantes

Maintenant vous avez fini d’apprendre comment vous pouvez personnaliser les solutions hello préconfiguré, vous pouvez découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]
* [Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]
* [IoT hello d’arrière-plan la sécurité][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
