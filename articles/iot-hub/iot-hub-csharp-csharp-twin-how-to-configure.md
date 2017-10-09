---
title: "propriétés de double de l’appareil Azure IoT Hub aaaUse (.NET/.NET) | Documents Microsoft"
description: "Comment jumeaux dispositif de Azure IoT Hub toouse tooconfigure périphériques. Vous utilisez hello Azure IoT SDK pour .NET tooimplement une application d’appareil simulé et hello Azure IoT service SDK pour .NET tooimplement une application de service qui modifie une configuration de l’appareil à l’aide d’un double de l’appareil."
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Utiliser les propriétés souhaitées tooconfigure périphériques
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

À la fin de hello de ce didacticiel, vous aurez deux applications de console .NET :

* **SimulateDeviceConfiguration**, une application d’appareil simulé qui attend une mise à jour de la configuration souhaitée et signale l’état hello d’un processus de mise à jour de configuration simulé.
* **SetDesiredConfigurationAndQuery**, une application back-end, qui définit hello souhaitée de configuration sur un appareil et requêtes hello le processus de mise à jour de configuration.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.
> 
> 

toocomplete ce didacticiel, vous devez suivant de hello :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.

Si vous avez suivi hello [prise en main jumeaux de périphérique] [ lnk-twin-tutorial] didacticiel, vous disposez déjà d’un IoT hub et une identité d’appareil appelé **myDeviceId**. Dans ce cas, vous pouvez ignorer toohello [Create hello appareil simulé app] [ lnk-how-to-configure-createapp] section.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Créer l’application d’appareil simulé hello
Dans cette section, vous créez une application console .NET qui se connecte concentrateur tooyour **myDeviceId**et attend une mise à jour de la configuration souhaitée et signale ensuite les mises à jour sur le processus de mise à jour de configuration hello simulé.

1. Dans Visual Studio, créez un nouveau projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **SimulateDeviceConfiguration**.
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]

1. Dans l’Explorateur de solutions, cliquez sur hello **SimulateDeviceConfiguration** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices.client**. Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT appareil SDK] [ lnk-nuget-client-sdk] NuGet package et ses dépendances.
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Ajouter hello suivant champs toohello **programme** classe. Remplacez la valeur d’espace réservé hello avec la chaîne de connexion de périphérique hello que vous avez noté dans la section précédente de hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. Ajouter hello suivant de méthode toohello **programme** classe :
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello. Hello code ci-dessus, initialise hello **Client** objet, puis récupère hello appareil double pour **myDeviceId**.

1. Ajouter hello suivant de méthode toohello **programme** classe. Cette méthode définit les valeurs d’initiale de hello de télémétrie sur l’appareil local de hello, puis les mises à jour hello double de l’appareil.

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Ajouter hello suivant de méthode toohello **programme** classe. Il s’agit d’un rappel qui détecte une modification de *propriétés souhaitée* deux conteneurs de périphérique hello.

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Cette hello de mises à jour de méthode signalé propriétés sur l’objet de double hello périphérique local avec une configuration hello mises à jour demande et définit l’état de hello trop**en attente**, puis les mises à jour hello double du périphérique sur le service de hello. Après la mise à jour de double de périphérique hello, il termine hello modification de la configuration en appelant la méthode hello `CompleteConfigChange` décrite au point suivant de hello.

1. Ajouter hello suivant de méthode toohello **programme** classe. Cette méthode simule une réinitialisation du périphérique, puis les mises à jour hello propriétés signalées local définir le statut de hello trop**réussite** et supprime hello **pendingConfig** élément. Il met ensuite à jour le double de périphérique hello sur le service de hello. 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. Ajoutez enfin hello suivant lignes toohello **Main** méthode :

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > Ce didacticiel ne simule pas de comportement pour des mises à jour de configuration simultanées. Certains processus de mise à jour de configuration peuvent être en mesure de tooaccommodate des modifications de configuration de la cible pendant l’exécution de mise à jour hello, certaines peuvent comporter des tooqueue et certains peuvent rejeter les avec une condition d’erreur. Assurez-vous que tooconsider hello le comportement souhaité pour votre processus de configuration spécifique et ajouter une logique approprié de hello avant le lancement de la modification de configuration hello.
   > 
   > 
1. Générez la solution de hello et puis exécutez l’application hello à partir de Visual Studio en cliquant sur **F5**. Dans la console de sortie hello, vous devez voir des messages hello indiquant que votre appareil simulé est la récupération de double de périphérique hello, la définition des données de télémétrie hello et en attente de la modification de la propriété souhaitée. Gardez à l’application hello en cours d’exécution.

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
   
    Hello **Registre** objet expose tous les hello méthodes requis toointeract avec jumeaux de périphérique à partir du service de hello. Ce code initialise hello **Registre** de l’objet, récupère hello double de périphérique pour **myDeviceId**, puis met à jour ses propriétés souhaitées par un nouvel objet de configuration de télémétrie.
    Après cela, elle interroge jumeaux de périphérique hello stockées dans le hub IoT de hello toutes les 10 secondes et commander des photos hello souhaité et a signalé des configurations de télémétrie. Consultez toohello [langage de requête IoT Hub] [ lnk-query] toolearn comment toogenerate enrichi les rapports sur tous vos appareils.
   
   > [!IMPORTANT]
   > Cette application interroge IoT Hub toutes les 10 secondes à titre d’exemple. Utilisez des requêtes toogenerate orientés utilisateur rapports entre plusieurs appareils et pas les modifications toodetect. Si votre solution nécessite des notifications d’événements d’appareil en temps réel, utilisez des [notifications jumelles][lnk-twin-notifications].
   > 
   > 
1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **SetDesiredConfigurationAndQuery** projet est **Démarrer**. Générez la solution de hello.
1. Avec **SimulateDeviceConfiguration** en cours d’exécution application appareil, application de service de hello exécution à partir de Visual Studio à l’aide **F5**. Vous devez voir configuration signalé de hello modifier à partir de **en attente** trop**réussite** avec active de nouveau hello fréquence d’envoi des cinq minutes au lieu de 24 heures.

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
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
