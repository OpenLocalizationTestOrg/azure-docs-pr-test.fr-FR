---
title: "aaaUse Azure IoT Hub direct de méthodes (nœud/.NET) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez du SDK de périphérique Azure IoT hello pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour .NET tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="99cd2-104">Utilisation des méthodes directes (NET/Node)</span><span class="sxs-lookup"><span data-stu-id="99cd2-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="99cd2-105">Dans ce didacticiel, nous allons toodevelop .NET et une application de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="99cd2-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="99cd2-106">**CallMethodOnDevice.sln**, une application de serveur principal .NET, qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="99cd2-107">**SimulatedDevice.js**, une application Node.js, ce qui simule un appareil de connexion tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et répond méthode toohello appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="99cd2-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="99cd2-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="99cd2-109">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="99cd2-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="99cd2-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="99cd2-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="99cd2-111">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="99cd2-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="99cd2-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="99cd2-112">An active Azure account.</span></span> <span data-ttu-id="99cd2-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="99cd2-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="99cd2-114">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="99cd2-114">Create a simulated device app</span></span>
<span data-ttu-id="99cd2-115">Dans cette section, vous créer une application de console Node.js qui répond méthode tooa appelée par solution hello retour de fin.</span><span class="sxs-lookup"><span data-stu-id="99cd2-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="99cd2-116">Créez un dossier vide appelé **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="99cd2-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="99cd2-117">Bonjour **simulateddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="99cd2-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="99cd2-118">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="99cd2-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="99cd2-119">Votre invite de commandes Bonjour **simulateddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt** packages :</span><span class="sxs-lookup"><span data-stu-id="99cd2-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="99cd2-120">À l’aide d’un éditeur de texte, créez un fichier Bonjour **simulateddevice** dossier et nommez-le **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="99cd2-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="99cd2-121">Ajoutez hello suivant `require` instructions au hello démarrent Hello **SimulatedDevice.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="99cd2-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="99cd2-122">Ajouter un **connectionString** variable et l’utiliser toocreate un **DeviceClient** instance.</span><span class="sxs-lookup"><span data-stu-id="99cd2-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="99cd2-123">Remplacez **{chaîne de connexion de périphérique}** avec chaîne de connexion de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="99cd2-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="99cd2-124">Ajoutez hello suivant de méthode directe de fonction tooimplement hello de périphérique de hello :</span><span class="sxs-lookup"><span data-stu-id="99cd2-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="99cd2-125">Ouvrez tooyour IoT hub hello connexion et initialiser l’écouteur de méthode hello :</span><span class="sxs-lookup"><span data-stu-id="99cd2-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="99cd2-126">Enregistrez et fermez hello **SimulatedDevice.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="99cd2-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="99cd2-127">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="99cd2-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="99cd2-128">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, les tentatives de connexion), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="99cd2-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="99cd2-129">Appeler une méthode directe sur un appareil</span><span class="sxs-lookup"><span data-stu-id="99cd2-129">Call a direct method on a device</span></span>
<span data-ttu-id="99cd2-130">Dans cette section, vous créez une application de console .NET qui appelle une méthode dans l’application d’appareil simulé hello et affiche ensuite la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="99cd2-131">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="99cd2-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="99cd2-132">Assurez-vous que la version du .NET Framework hello est 4.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="99cd2-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="99cd2-133">Projet de hello nom **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="99cd2-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][10]
2. <span data-ttu-id="99cd2-135">Dans l’Explorateur de solutions, cliquez sur hello **CallMethodOnDevice** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="99cd2-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="99cd2-136">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="99cd2-137">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="99cd2-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][11]

4. <span data-ttu-id="99cd2-139">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="99cd2-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="99cd2-140">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="99cd2-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="99cd2-141">Remplacer la valeur d’espace réservé hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="99cd2-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="99cd2-142">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="99cd2-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="99cd2-143">Cette méthode appelle une méthode directe avec le nom `writeLine` sur hello `myDeviceId` appareil.</span><span class="sxs-lookup"><span data-stu-id="99cd2-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="99cd2-144">Ensuite, il écrit la réponse hello fournie par périphérique hello sur la console de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="99cd2-145">Notez qu’il est possible toospecify une valeur de délai d’attente pour hello périphérique toorespond.</span><span class="sxs-lookup"><span data-stu-id="99cd2-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="99cd2-146">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="99cd2-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="99cd2-147">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="99cd2-147">Run hello applications</span></span>
<span data-ttu-id="99cd2-148">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="99cd2-149">Dans l’Explorateur de solutions Visual Studio de hello, avec le bouton droit de votre solution, puis cliquez sur **définir les projets de démarrage...** . Sélectionnez **projet de démarrage unique**, puis sélectionnez hello **CallMethodOnDevice** projet dans le menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="99cd2-150">À l’invite de commande Bonjour **simulateddevice** dossier, exécutez hello suivant toostart commande écoute les appels de méthode à partir de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="99cd2-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="99cd2-151">Attendez hello simulée périphérique tooopen :![][7]</span><span class="sxs-lookup"><span data-stu-id="99cd2-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="99cd2-152">Maintenant que hello est connectée et en attente d’appels de méthode, exécutez hello .NET **CallMethodOnDevice** méthode hello de tooinvoke d’application dans l’application d’appareil simulé hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="99cd2-153">Vous devez voir la réponse du périphérique hello écrite dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="99cd2-154">Appareil de Hello réagit puis toohello méthode par à l’impression de ce message :</span><span class="sxs-lookup"><span data-stu-id="99cd2-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="99cd2-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="99cd2-155">Next steps</span></span>
<span data-ttu-id="99cd2-156">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="99cd2-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="99cd2-157">Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="99cd2-158">Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="99cd2-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="99cd2-159">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="99cd2-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="99cd2-160">[Prise en main d’IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="99cd2-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="99cd2-161">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="99cd2-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="99cd2-162">toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="99cd2-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md
