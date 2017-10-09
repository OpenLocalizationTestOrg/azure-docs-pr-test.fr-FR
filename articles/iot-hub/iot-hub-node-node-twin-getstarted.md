---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez hello kits de développement logiciel Azure IoT pour l’application d’appareil simulé Node.js tooimplement hello et une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Prise en main des représentations d’appareils (Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

À la fin de hello de ce didacticiel, vous aurez deux applications de console Node.js :

* **AddTagsAndQuery.js**, application Node.js qui ajoute des balises et interroge des représentations d’appareil.
* **TwinSimulatedDevice.js**, une application Node.js qui simule un appareil qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et signale l’état de connectivité.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.
> 
> 

toocomplete ce didacticiel, vous devez suivant de hello :

* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Créer l’application de service hello
Dans cette section, vous créez une application de console Node.js qui ajoute le double d’appareil emplacement métadonnées toohello associé **myDeviceId**. Il interroge ensuite jumeaux de périphérique hello stockées dans hello IoT hub en sélectionnant les appareils hello situés dans hello nous et puis hello ceux qui signalent une connexion cellulaire.

1. Créez un dossier vide nommé **addtagsandqueryapp**. Bonjour **addtagsandqueryapp** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **addtagsandqueryapp** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :
   
    ```
    npm install azure-iothub --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **AddTagsAndQuery.js** fichier Bonjour **addtagsandqueryapp** dossier.
4. Ajouter hello suivant code toohello **AddTagsAndQuery.js** de fichiers et remplacez-le par hello **{chaîne de connexion de hub iot}** espace réservé par hello chaîne de connexion de IoT Hub vous avez copié lorsque vous avez créé votre hub :
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello. code précédent de Hello initialise tout d’abord hello **Registre** de l’objet, puis récupère hello double de périphérique pour **myDeviceId**et enfin met à jour ses balises avec les informations d’emplacement hello souhaité.
   
    Après avoir hello hello de mise à jour des balises il hello d’appels **queryTwins** (fonction).
5. Ajouter hello suivant du code à la fin de hello de **AddTagsAndQuery.js** tooimplement hello **queryTwins** (fonction) :
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    code de précédent Hello exécute deux requêtes : hello sélectionne tout d’abord uniquement les jumeaux appareil hello des périphériques situés dans hello **Redmond43** usine et hello deuxième affine hello requête tooselect uniquement hello pour les appareils qui sont également connectés via réseau cellulaire.
   
    Notez que hello le code précédent, lorsqu’il crée hello **requête** d’objet, spécifie un nombre maximal de documents renvoyés. Hello **requête** objet contient un **hasMoreResults** propriété booléenne que vous pouvez utiliser tooinvoke hello **nextAsTwin** méthodes tooretrieve tous les résultats de plusieurs fois. Une méthode appelée **next** est disponible pour les résultats qui ne sont pas des représentations d’appareil, par exemple, les résultats de requêtes d’agrégation.
6. Exécutez l’application hello avec :
   
        node AddTagsAndQuery.js
   
    Vous devez voir un périphérique dans les résultats de hello pour poser des requêtes hello pour tous les appareils qui se trouve dans **Redmond43** et none pour les requêtes hello qui restreint hello toodevices qui utilisent un réseau cellulaire.
   
    ![][1]

Dans la section suivante de hello vous créez une application de périphérique qui fournit des informations de connectivité hello et modifications hello résultat de requête hello dans la section précédente de hello.

## <a name="create-hello-device-app"></a>Créer l’application hello
Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**et ensuite les mises à jour son double de l’appareil de signalé toocontain hello informations sur les propriétés qu’il est connecté à l’aide d’un réseau cellulaire.

> [!NOTE]
> À ce stade, jumeaux de périphérique est accessibles uniquement à partir d’appareils qui se connectent tooIoT concentrateur à l’aide du protocole MQTT hello. Reportez-vous toohello [prise en charge MQTT] [ lnk-devguide-mqtt] article pour obtenir des instructions sur la façon de tooconvert existant appareil application toouse MQTT.
> 
> 

1. Créez un dossier vide nommé **reportconnectivity**. Bonjour **reportconnectivity** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```
2. Votre invite de commandes Bonjour **reportconnectivity** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil**, et **azure-iot-périphérique-mqtt** package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. À l’aide d’un éditeur de texte, créez un nouveau **ReportConnectivity.js** fichier Bonjour **reportconnectivity** dossier.
4. Ajouter hello suivant code toohello **ReportConnectivity.js** de fichiers et remplacez-le par hello **{chaîne de connexion de périphérique}** espace réservé avec la chaîne de connexion de périphérique hello vous avez copié lors de la création de hello **myDeviceId** identité d’appareil :
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello. Hello le code précédent, une fois qu’il initialise hello **Client** de l’objet, récupère hello double de périphérique pour **myDeviceId** et met à jour sa propriété signalée avec les informations de connectivité hello.
5. Exécutez l’application hello
   
        node ReportConnectivity.js
   
    Vous devez voir le message de type hello `twin state reported`.
6. Maintenant que hello appareil signalé ses informations de connectivité, il doit s’afficher dans les deux requêtes. Accédez à hello **addtagsandqueryapp** hello et exécutez à nouveau des requêtes :
   
        node AddTagsAndQuery.js
   
    Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.
   
    ![][3]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil simulé application tooreport appareil connectivité des informations en double du périphérique hello. Vous avez également appris tooquery ces informations à l’aide du langage de requête de type SQL IoT Hub hello.

Hello utilisation suivant comment les ressources toolearn à :

* envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),
* configurer des appareils à l’aide des propriétés de votre choix du double de l’appareil avec hello [utilisation souhaitée propriétés tooconfigure dispositifs] [ lnk-twin-how-to-configure] (didacticiel),
* contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur), avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
