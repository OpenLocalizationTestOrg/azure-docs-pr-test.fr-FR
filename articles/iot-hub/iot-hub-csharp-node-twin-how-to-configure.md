---
title: "propriétés de double de l’appareil Azure IoT Hub aaaUse (nœud/.NET) | Documents Microsoft"
description: "Comment jumeaux dispositif de Azure IoT Hub toouse tooconfigure périphériques. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et hello Azure IoT service SDK pour .NET tooimplement une application de service qui modifie une configuration de l’appareil à l’aide d’un double de l’appareil."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Utiliser les propriétés souhaitées tooconfigure périphériques
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

À la fin de hello de ce didacticiel, vous aurez deux applications console :

* **SimulateDeviceConfiguration.js**, une application d’appareil simulé qui attend une mise à jour de la configuration souhaitée et signale l’état hello d’un processus de mise à jour de configuration simulé.
* **SetDesiredConfigurationAndQuery**, une application de serveur principal .NET, qui définit hello souhaitée de configuration sur un appareil et requêtes hello le processus de mise à jour de configuration.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.
> 
> 

toocomplete ce didacticiel, vous devez suivant de hello :

* Visual Studio 2015 ou Visual Studio 2017.
* Node.js version 0.10.x ou ultérieure.
* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.

Si vous avez suivi hello [prise en main jumeaux de périphérique] [ lnk-twin-tutorial] didacticiel, vous disposez déjà d’un IoT hub et une identité d’appareil appelé **myDeviceId**. Dans ce cas, vous pouvez ignorer toohello [Create hello appareil simulé app] [ lnk-how-to-configure-createapp] section.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Créer l’application d’appareil simulé hello
Dans cette section, vous créez une application de console Node.js qui connecte le concentrateur tooyour **myDeviceId**et attend une mise à jour de la configuration souhaitée et signale ensuite les mises à jour sur le processus de mise à jour de configuration hello simulé.

1. Créez un dossier vide nommé **simulatedeviceconfiguration**. Bonjour **simulatedeviceconfiguration** dossier, créez un nouveau fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello.
   
    ```
    npm init
    ```
1. Votre invite de commandes Bonjour **simulatedeviceconfiguration** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt**packages :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. À l’aide d’un éditeur de texte, créez un nouveau **SimulateDeviceConfiguration.js** fichier Bonjour **simulatedeviceconfiguration** dossier.
1. Ajouter hello suivant code toohello **SimulateDeviceConfiguration.js** de fichiers et remplacez-le par hello **{chaîne de connexion de périphérique}** espace réservé avec la chaîne de connexion de périphérique hello vous avez copié quand vous créé hello **myDeviceId** identité d’appareil :
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hello **Client** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir de l’appareil de hello. Ce code initialise hello **Client** de l’objet, récupère hello double de périphérique pour **myDeviceId**, puis l’attache un gestionnaire de mise à jour hello sur *propriétés souhaitée*. Gestionnaire de Hello vérifie qu’une demande de modification de configuration en comparant hello configIds, puis appelle une méthode qui démarre la modification de la configuration hello.
   
    Notez que pour des raisons de hello de simplicité, ce code utilise une valeur par défaut codées en dur pour la configuration initiale hello. Une application réelle chargerait probablement la configuration à partir d’un stockage local.
   
   > [!IMPORTANT]
   > Les événements de modification de propriété souhaités sont toujours émis une seule fois lors de la connexion de l’appareil. Assurez-vous que toocheck qu’il existe une modification réelle dans hello souhaité propriétés avant d’effectuer une action.
   > 
   > 
1. Ajouter hello suivant les méthodes avant hello `client.open()` invocation :
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hello **initConfigChange** hello de mises à jour de méthode signalé propriétés sur l’objet de double hello périphérique local avec une configuration hello mises à jour demande et définit l’état de hello trop**en attente**, puis hello de mises à jour double du périphérique sur le service de hello. Après la mise à jour de double de périphérique hello, elle simule un processus à long terme qui arrête l’exécution de hello de **completeConfigChange**. Cette méthode met à jour les propriétés locales signalé hello définir le statut de hello trop**réussite** et suppression hello **pendingConfig** objet. Il met ensuite à jour le double de périphérique hello sur le service de hello.
   
    À noter que, la bande passante toosave indiqué propriétés sont mises à jour en spécifiant uniquement les toobe hello propriétés modifiées (nommé **correctif** Bonjour au-dessus de code), au lieu de remplacer l’ensemble du document hello.
   
   > [!NOTE]
   > Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées. Certains processus de mise à jour de configuration peuvent être en mesure de tooaccommodate des modifications de configuration de la cible pendant l’exécution de mise à jour hello, certaines peuvent comporter des tooqueue et certains peuvent rejeter les avec une condition d’erreur. Assurez-vous que tooconsider hello le comportement souhaité pour votre processus de configuration spécifique et ajouter une logique approprié de hello avant le lancement de la modification de configuration hello.
   > 
   > 
1. Exécutez l’application hello :
   
        node SimulateDeviceConfiguration.js
   
    Vous devez voir le message de type hello `retrieved device twin`. Gardez à l’application hello en cours d’exécution.

## <a name="create-hello-service-app"></a>Créer l’application de service hello
Dans cette section, vous allez créer une application de console .NET qui hello mises à jour *propriétés souhaitée* sur hello double de périphérique associé **myDeviceId** avec un nouvel objet de configuration de télémétrie. Il interroge jumeaux de périphérique hello stockées dans le hub IoT de hello et montre la différence hello entre hello souhaitée et a signalé des configurations de périphérique de hello.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **SetDesiredConfigurationAndQuery**.
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]
1. Dans l’Explorateur de solutions, cliquez sur hello **SetDesiredConfigurationAndQuery** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Ajouter hello suivant de méthode toohello **programme** classe :
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello. Ce code initialise hello **Registre** de l’objet, récupère hello double de périphérique pour **myDeviceId**, puis met à jour ses propriétés souhaitées par un nouvel objet de configuration de télémétrie.
    Après cela, elle interroge jumeaux de périphérique hello stockées dans le hub IoT de hello toutes les 10 secondes et commander des photos hello souhaité et a signalé des configurations de télémétrie. Consultez toohello [langage de requête IoT Hub] [ lnk-query] toolearn comment toogenerate enrichi les rapports sur tous vos appareils.
   
   > [!IMPORTANT]
   > Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple. Utilisez des requêtes toogenerate orientés utilisateur rapports entre plusieurs appareils et pas les modifications toodetect. Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].
   > 
   > 
1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **SetDesiredConfigurationAndQuery** projet est **Démarrer**. Générez la solution de hello.
1. Avec **SimulateDeviceConfiguration.js** , exécuter application .NET de hello à partir de Visual Studio en utilisant **F5** et vous devez voir configuration signalé de hello modifier à partir de **deréussite** trop**en attente** trop**réussite** à nouveau avec active de nouveau hello fréquence d’envoi des cinq minutes au lieu de 24 heures.

 ![Appareil configuré correctement][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Il existe un délai d’une minute tooa entre l’opération de rapport d’appareil hello et le résultat de la requête hello. Il s’agit de tooenable hello requête infrastructure toowork à très grande échelle. tooretrieve des vues cohérentes d’un double d’appareil unique utilisent hello **getDeviceTwin** méthode Bonjour **Registre** classe.
   > 
   > 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous définissez la configuration souhaitée en tant que *propriétés souhaitée* à partir de la solution de hello back-end et a écrit un toodetect application de périphérique qui changent et simuler un processus de mise à jour de plusieurs étapes son état hello signalé par le biais de création de rapports Propriétés.

Hello utilisation suivant comment les ressources toolearn à :

* envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),
* planifier ou exécuter des opérations sur les grands ensembles de périphériques Voir hello [planification et les tâches de diffusion] [ lnk-schedule-jobs] didacticiel.
* contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur), avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
