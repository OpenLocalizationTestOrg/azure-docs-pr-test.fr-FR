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
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="d3509-104">Utilisation des méthodes directes (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="d3509-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="d3509-105">Dans ce didacticiel, nous sommes continu toodevelop deux applications console .NET :</span><span class="sxs-lookup"><span data-stu-id="d3509-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="d3509-106">**CallMethodOnDevice**, une application back-end, qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="d3509-107">**SimulateDeviceMethods**, une application console qui simule un appareil de connexion tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et répond méthode toohello appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="d3509-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="d3509-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="d3509-109">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d3509-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="d3509-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d3509-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d3509-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d3509-111">An active Azure account.</span></span> <span data-ttu-id="d3509-112">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="d3509-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="d3509-113">Si vous souhaitez identité d’appareil toocreate hello par programme à la place, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour appareil simulé à l’aide de .NET] [ lnk-device-identity-csharp] l’article.</span><span class="sxs-lookup"><span data-stu-id="d3509-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="d3509-114">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="d3509-114">Create a simulated device app</span></span>
<span data-ttu-id="d3509-115">Dans cette section, vous créez une application console .NET qui répond méthode tooa appelée par solution hello retour de fin.</span><span class="sxs-lookup"><span data-stu-id="d3509-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="d3509-116">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="d3509-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="d3509-117">Projet de hello nom **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="d3509-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Nouvelle application pour appareil Windows classique Visual C#][img-createdeviceapp]
    
1. <span data-ttu-id="d3509-119">Dans l’Explorateur de solutions, cliquez sur hello **SimulateDeviceMethods** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d3509-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="d3509-120">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir** et recherchez **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="d3509-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="d3509-121">Sélectionnez **installer** tooinstall hello **Microsoft.Azure.Devices.Client** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="d3509-122">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT appareil SDK] [ lnk-nuget-client-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="d3509-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![Application cliente dans la fenêtre du gestionnaire de package NuGet][img-clientnuget]
1. <span data-ttu-id="d3509-124">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="d3509-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="d3509-125">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="d3509-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d3509-126">Remplacez la valeur d’espace réservé hello avec la chaîne de connexion de périphérique hello que vous avez noté dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="d3509-127">Ajoutez hello suivant de méthode directe de hello tooimplement de périphérique de hello :</span><span class="sxs-lookup"><span data-stu-id="d3509-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="d3509-128">Enfin, ajoutez hello suivant code toohello **Main** méthode tooopen hello connexion tooyour IoT hub et initialiser hello méthode écouteur :</span><span class="sxs-lookup"><span data-stu-id="d3509-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
        
1. <span data-ttu-id="d3509-129">Dans l’Explorateur de solutions Visual Studio de hello, avec le bouton droit de votre solution, puis cliquez sur **définir les projets de démarrage...** . Sélectionnez **projet de démarrage unique**, puis sélectionnez hello **SimulateDeviceMethods** projet dans le menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="d3509-130">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="d3509-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d3509-131">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, les tentatives de connexion), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d3509-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="d3509-132">Appeler une méthode directe sur un appareil</span><span class="sxs-lookup"><span data-stu-id="d3509-132">Call a direct method on a device</span></span>
<span data-ttu-id="d3509-133">Dans cette section, vous créez une application de console .NET qui appelle une méthode dans l’application d’appareil simulé hello et affiche ensuite la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="d3509-134">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="d3509-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="d3509-135">Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d3509-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d3509-136">Projet de hello nom **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="d3509-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][img-createserviceapp]
2. <span data-ttu-id="d3509-138">Dans l’Explorateur de solutions, cliquez sur hello **CallMethodOnDevice** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="d3509-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="d3509-139">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="d3509-140">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="d3509-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]

4. <span data-ttu-id="d3509-142">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="d3509-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="d3509-143">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="d3509-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d3509-144">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="d3509-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="d3509-145">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="d3509-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="d3509-146">Cette méthode appelle une méthode directe avec le nom `writeLine` sur hello `myDeviceId` appareil.</span><span class="sxs-lookup"><span data-stu-id="d3509-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="d3509-147">Ensuite, il écrit la réponse hello fournie par périphérique hello sur la console de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="d3509-148">Notez qu’il est possible toospecify une valeur de délai d’attente pour hello périphérique toorespond.</span><span class="sxs-lookup"><span data-stu-id="d3509-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="d3509-149">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="d3509-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="d3509-150">Dans l’Explorateur de solutions Visual Studio de hello, avec le bouton droit de votre solution, puis cliquez sur **définir les projets de démarrage...** . Sélectionnez **projet de démarrage unique**, puis sélectionnez hello **CallMethodOnDevice** projet dans le menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="d3509-151">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="d3509-151">Run hello applications</span></span>
<span data-ttu-id="d3509-152">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="d3509-153">Exécuter l’application d’appareil hello .NET **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="d3509-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="d3509-154">Elle doit commencer à écouter les appels de méthode provenant de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="d3509-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Exécution de l’application d’appareil][img-deviceapprun]
1. <span data-ttu-id="d3509-156">Maintenant que hello est connectée et en attente d’appels de méthode, exécutez hello .NET **CallMethodOnDevice** méthode hello de tooinvoke d’application dans l’application d’appareil simulé hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="d3509-157">Vous devez voir la réponse du périphérique hello écrite dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-157">You should see hello device response written in hello console.</span></span>
   
    ![Exécution de l’application de service][img-serviceapprun]
1. <span data-ttu-id="d3509-159">Appareil de Hello réagit puis toohello méthode par à l’impression de ce message :</span><span class="sxs-lookup"><span data-stu-id="d3509-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Méthode directe appelée sur un périphérique de hello][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="d3509-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3509-161">Next steps</span></span>
<span data-ttu-id="d3509-162">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d3509-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d3509-163">Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="d3509-164">Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="d3509-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="d3509-165">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="d3509-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d3509-166">[Prise en main d’IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="d3509-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="d3509-167">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="d3509-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="d3509-168">toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d3509-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
