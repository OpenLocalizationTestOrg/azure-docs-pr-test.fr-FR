---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez du SDK de périphérique Azure IoT hello pour l’application d’appareil simulé Node.js tooimplement hello et hello Azure IoT service SDK pour .NET tooimplement une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a>Prise en main des représentations d’appareils (.NET/Node)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

À la fin hello de ce didacticiel, vous disposez .NET et une application de console Node.js :

* **AddTagsAndQuery.sln**, application .NET qui ajoute des balises et interroge des représentations d’appareil.
* **TwinSimulatedDevice.js**, une application Node.js qui simule un appareil qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et signale l’état de connectivité.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.
> 
> 

toocomplete ce didacticiel, vous devez suivant de hello :

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Créer l’application de service hello
Dans cette section, vous créez .NET application console (à l’aide de c#) ajoute double d’appareil emplacement métadonnées toohello associé **myDeviceId**. Il interroge ensuite jumeaux de périphérique hello stockées dans hello IoT hub en sélectionnant les appareils hello situés dans hello nous et puis hello ceux qui a signalé une connexion cellulaire.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **AddTagsAndQuery**.
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. Dans l’Explorateur de solutions, cliquez sur hello **AddTagsAndQuery** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices**. Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices;
1. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Ajouter hello suivant de méthode toohello **programme** classe :
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    Hello **RegistryManager** classe expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello. code précédent de Hello initialise tout d’abord hello **registryManager** de l’objet, puis récupère hello double de périphérique pour **myDeviceId**et enfin met à jour ses balises avec les informations d’emplacement hello souhaité.
   
    Après la mise à jour, il exécute deux requêtes : hello sélectionne tout d’abord uniquement les jumeaux appareil hello des périphériques situés dans hello **Redmond43** usine et hello deuxième affine hello requête tooselect uniquement hello pour les appareils qui sont également connectés via réseau cellulaire.
   
    Notez que hello le code précédent, lorsqu’il crée hello **requête** d’objet, spécifie un nombre maximal de documents renvoyés. Hello **requête** objet contient un **HasMoreResults** propriété booléenne que vous pouvez utiliser tooinvoke hello **GetNextAsTwinAsync** méthodes tooretrieve plusieurs fois tous les résultats. Une méthode appelée **GetNextAsJson** est disponible pour les résultats qui ne sont pas des jumeaux d’appareil, par exemple, les résultats de requêtes d’agrégation.
1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **AddTagsAndQuery** projet est **Démarrer**. Générez la solution de hello.
1. Exécution de cette application en cliquant sur hello **AddTagsAndQuery** projet et en sélectionnant **déboguer**, suivi par **démarrer une nouvelle instance**. Vous devez voir un périphérique dans les résultats de hello pour poser des requêtes hello pour tous les appareils qui se trouve dans **Redmond43** et none pour les requêtes hello qui restreint hello toodevices qui utilisent un réseau cellulaire.
   
    ![Résultats de requête dans la fenêtre][img-addtagapp]

Dans la section suivante de hello, vous créez une application de périphérique qui fournit des informations de connectivité hello et modifications hello résultat de requête hello dans la section précédente de hello.

## <a name="create-hello-device-app"></a>Créer l’application hello
Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**, puis met à jour ses informations de hello toocontain propriétés signalé qu’il est connecté à l’aide d’un réseau cellulaire.

1. Créez un dossier vide nommé **reportconnectivity**. Bonjour **reportconnectivity** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello.
   
    ```
    npm init
    ```
1. Votre invite de commandes Bonjour **reportconnectivity** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil**, et **azure-iot-périphérique-mqtt** package :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. À l’aide d’un éditeur de texte, créez un nouveau **ReportConnectivity.js** fichier Bonjour **reportconnectivity** dossier.
1. Ajouter hello suivant code toohello **ReportConnectivity.js** de fichier et remplacez l’espace réservé de hello pour la chaîne de connexion de périphérique avec hello vous copié lors de la création de hello **myDeviceId** périphérique identité :
   
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
1. Exécutez l’application hello
   
        node ReportConnectivity.js
   
    Vous devez voir le message de type hello `twin state reported`.
1. Maintenant que hello appareil signalé ses informations de connectivité, il doit s’afficher dans les deux requêtes. Exécutez hello .NET **AddTagsAndQuery** hello de toorun application interroge à nouveau. Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.
   
    ![][img-addtagapp2]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil simulé application tooreport appareil connectivité des informations en double du périphérique hello. Vous avez également appris tooquery ces informations à l’aide du langage de requête de type SQL IoT Hub hello.

Hello utilisation suivant comment les ressources toolearn à :

* envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),
* configurer des appareils à l’aide des propriétés de votre choix du double de l’appareil avec hello [utilisation souhaitée propriétés tooconfigure dispositifs] [ lnk-twin-how-to-configure] (didacticiel),
* contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

