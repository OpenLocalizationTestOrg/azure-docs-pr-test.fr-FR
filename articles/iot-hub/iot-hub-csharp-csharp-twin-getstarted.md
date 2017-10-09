---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (.NET/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez du SDK de périphérique Azure IoT hello pour application d’appareil simulé .NET tooimplement hello et hello Azure IoT service SDK pour .NET tooimplement une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a>Bien démarrer avec les jumeaux d’appareils (.NET/.NET)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

À la fin de hello de ce didacticiel, vous disposerez ces applications de console .NET :

* **CreateDeviceIdentity**, une application .NET qui crée une identité de l’appareil et la sécurité associés clé tooconnect votre application d’appareil simulé.
* **AddTagsAndQuery**, application principale .NET qui ajoute des balises et interroge des jumeaux d’appareil.
* **ReportConnectivity**, une périphérique d’application .NET qui simule un appareil qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et signale l’état de connectivité.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.
> 
> 

toocomplete ce didacticiel, vous devez suivant de hello :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si vous souhaitez identité d’appareil toocreate hello par programme à la place, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour appareil simulé à l’aide de .NET] [ lnk-device-identity-csharp] l’article.

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
Dans cette section, vous créez une application console .NET qui se connecte concentrateur tooyour **myDeviceId**, puis met à jour ses informations de hello toocontain propriétés signalé qu’il est connecté à l’aide d’un réseau cellulaire.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **ReportConnectivity**.
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]
    
1. Dans l’Explorateur de solutions, cliquez sur hello **ReportConnectivity** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices.client**. Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT appareil SDK] [ lnk-nuget-client-sdk] NuGet package et ses dépendances.
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. Ajouter hello suivant champs toohello **programme** classe. Remplacez la valeur d’espace réservé hello avec la chaîne de connexion de périphérique hello que vous avez noté dans la section précédente de hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Ajouter hello suivant de méthode toohello **programme** classe :

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    Hello **Client** objet expose toutes les méthodes hello nécessitent de toointeract avec jumeaux de périphérique à partir de l’appareil de hello. Hello code ci-dessus, initialise hello **Client** objet, puis récupère hello appareil double pour **myDeviceId**.

1. Ajouter hello suivant de méthode toohello **programme** classe :
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   Hello code au-dessus de mises à jour **myDeviceId**de signalé propriété avec les informations de connectivité hello.

1. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **ReportConnectivity** projet est **Démarrer**. Générez la solution de hello.
1. Exécution de cette application en cliquant sur hello **ReportConnectivity** projet et en sélectionnant **déboguer**, suivi par **démarrer une nouvelle instance**. Vous devez le voir obtention des informations sur le double hello et connectivité que d’envoyer un *signalé propriété*.
   
    ![Exécuter une connexion de périphérique application tooreport][img-rundeviceapp]
    
    
1. Maintenant que hello appareil signalé ses informations de connectivité, il doit s’afficher dans les deux requêtes. Exécutez hello .NET **AddTagsAndQuery** hello de toorun application interroge à nouveau. Cette fois, **myDeviceId** doit apparaître dans les résultats des deux requêtes.
   
    ![Connectivité des appareils signalée avec succès][img-tagappsuccess]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil simulé application tooreport appareil connectivité des informations en double du périphérique hello. Vous avez également appris tooquery ces informations à l’aide du langage de requête de type SQL IoT Hub hello.

Hello utilisation suivant comment les ressources toolearn à :

* envoyer la télémétrie des appareils avec hello [prise en main IoT Hub] [ lnk-iothub-getstarted] (didacticiel),
* configurer des appareils à l’aide des propriétés de votre choix du double de l’appareil avec hello [utilisation souhaitée propriétés tooconfigure dispositifs] [ lnk-twin-how-to-configure] (didacticiel),
* contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes] [ lnk-methods-tutorial] didacticiel.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

