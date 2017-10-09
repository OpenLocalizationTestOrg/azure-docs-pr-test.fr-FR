---
title: "aaaUse Azure IoT Hub directe des méthodes (.NET/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez des appareils Azure IoT de hello Kit de développement logiciel pour .NET tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour .NET tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Utilisation des méthodes directes (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Dans ce didacticiel, nous sommes continu toodevelop deux applications console .NET :

* **CallMethodOnDevice**, une application back-end, qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.
* **SimulateDeviceMethods**, une application console qui simule un appareil de connexion tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et répond méthode toohello appelée par le cloud de hello.

> [!NOTE]
> article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.
> 
> 

toocomplete ce didacticiel, vous devez :

* Visual Studio 2015 ou Visual Studio 2017.
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si vous souhaitez identité d’appareil toocreate hello par programme à la place, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour appareil simulé à l’aide de .NET] [ lnk-device-identity-csharp] l’article.


## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous créez une application console .NET qui répond méthode tooa appelée par solution hello retour de fin.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Projet de hello nom **SimulateDeviceMethods**.
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]
    
1. Dans l’Explorateur de solutions, cliquez sur hello **SimulateDeviceMethods** de projet, puis cliquez sur **gérer les Packages NuGet...** .
1. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices.client**. Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT appareil SDK] [ lnk-nuget-client-sdk] NuGet package et ses dépendances.
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Ajouter hello suivant champs toohello **programme** classe. Remplacez la valeur d’espace réservé hello avec la chaîne de connexion de périphérique hello que vous avez noté dans la section précédente de hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Ajoutez hello suivant de méthode directe de hello tooimplement de périphérique de hello :

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Enfin, ajoutez hello suivant code toohello **Main** méthode tooopen hello connexion tooyour IoT hub et initialiser hello méthode écouteur :
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. Dans l’Explorateur de solutions Visual Studio de hello, avec le bouton droit de votre solution, puis cliquez sur **définir les projets de démarrage...** . Sélectionnez **projet de démarrage unique**, puis sélectionnez hello **SimulateDeviceMethods** projet dans le menu déroulant de hello.        

> [!NOTE]
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, les tentatives de connexion), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Appeler une méthode directe sur un appareil
Dans cette section, vous créez une application de console .NET qui appelle une méthode dans l’application d’appareil simulé hello et affiche ensuite la réponse de hello.

1. Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet. Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure. Projet de hello nom **CallMethodOnDevice**.
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createserviceapp]
2. Dans l’Explorateur de solutions, cliquez sur hello **CallMethodOnDevice** de projet, puis cliquez sur **gérer les Packages NuGet...** .
3. Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello. Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]

4. Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Ajouter hello suivant champs toohello **programme** classe. Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Ajouter hello suivant de méthode toohello **programme** classe :
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Cette méthode appelle une méthode directe avec le nom `writeLine` sur hello `myDeviceId` appareil. Ensuite, il écrit la réponse hello fournie par périphérique hello sur la console de hello. Notez qu’il est possible toospecify une valeur de délai d’attente pour hello périphérique toorespond.
7. Enfin, ajoutez hello suivant lignes toohello **Main** méthode :
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. Dans l’Explorateur de solutions Visual Studio de hello, avec le bouton droit de votre solution, puis cliquez sur **définir les projets de démarrage...** . Sélectionnez **projet de démarrage unique**, puis sélectionnez hello **CallMethodOnDevice** projet dans le menu déroulant de hello.

## <a name="run-hello-applications"></a>Exécuter des applications de hello
Vous êtes maintenant prêt toorun les applications hello.

1. Exécuter l’application d’appareil hello .NET **SimulateDeviceMethods**. Elle doit commencer à écouter les appels de méthode provenant de votre IoT Hub : 

    ![Exécution de l’application d’appareil][img-deviceapprun]
1. Maintenant que hello est connectée et en attente d’appels de méthode, exécutez hello .NET **CallMethodOnDevice** méthode hello de tooinvoke d’application dans l’application d’appareil simulé hello. Vous devez voir la réponse du périphérique hello écrite dans la console hello.
   
    ![Exécution de l’application de service][img-serviceapprun]
1. Appareil de Hello réagit puis toohello méthode par à l’impression de ce message :
   
    ![Méthode directe appelée sur un périphérique de hello][img-directmethodinvoked]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub. Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello. Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello. 

toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :

* [Prise en main d’IoT Hub]
* [Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]

toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md
