---
title: "Utilisation des méthodes directes Azure IoT Hub (.NET/Node) | Microsoft Docs"
description: "Utilisation des méthodes directes Azure IoT Hub. Vous utilisez Azure IoT device SDK pour Node.js afin d’implémenter une application d’appareil simulé qui inclut une méthode directe et Azure IoT service SDK pour .NET afin d’implémenter une application de service qui appelle la méthode directe."
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
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="faf62-104">Utilisation des méthodes directes (NET/Node)</span><span class="sxs-lookup"><span data-stu-id="faf62-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="faf62-105">Dans ce didacticiel, nous allons développer une application console .NET et Node.js :</span><span class="sxs-lookup"><span data-stu-id="faf62-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="faf62-106">**CallMethodOnDevice.js**, une application principale .NET qui appelle une méthode dans l’application d’appareil simulé et affiche la réponse.</span><span class="sxs-lookup"><span data-stu-id="faf62-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="faf62-107">**SimulatedDevice.js**, une application Node.js qui simule un appareil se connectant à votre IoT Hub avec l’identité d’appareil créée précédemment, et répond à la méthode appelée par le cloud.</span><span class="sxs-lookup"><span data-stu-id="faf62-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="faf62-108">L’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks] fournit des informations sur les kits de développement logiciel Azure IoT que vous pouvez utiliser pour générer les deux applications qui s’exécutent sur les appareils et sur le serveur de solution principal.</span><span class="sxs-lookup"><span data-stu-id="faf62-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="faf62-109">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="faf62-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="faf62-110">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="faf62-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="faf62-111">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="faf62-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="faf62-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="faf62-112">An active Azure account.</span></span> <span data-ttu-id="faf62-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="faf62-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="faf62-114">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="faf62-114">Create a simulated device app</span></span>
<span data-ttu-id="faf62-115">Dans cette section, vous créez une application console Node.js qui répond à une méthode appelée par le serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="faf62-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="faf62-116">Créez un dossier vide appelé **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="faf62-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="faf62-117">Dans le dossier **simulateddevice** , créez un fichier package.json à l’aide de la commande ci-dessous, à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="faf62-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="faf62-118">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="faf62-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="faf62-119">À l’invite de commandes, dans le dossier **simulateddevice**, exécutez la commande suivante pour installer les packages **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="faf62-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="faf62-120">Dans un éditeur de texte, créez un fichier dans le dossier **simulateddevice** et nommez-le **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="faf62-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="faf62-121">Ajoutez les instructions `require` ci-dessous au début du fichier **SimulatedDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="faf62-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="faf62-122">Ajoutez une variable **connectionString** et utilisez-la pour créer une instance de **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="faf62-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="faf62-123">Remplacez **{device connection string}** par la chaîne connexion de l’appareil que vous avez générée dans la section *Créer une identité d’appareil* :</span><span class="sxs-lookup"><span data-stu-id="faf62-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="faf62-124">Ajoutez la fonction suivante pour implémenter la méthode directe sur l’appareil :</span><span class="sxs-lookup"><span data-stu-id="faf62-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="faf62-125">Ouvrez la connexion à votre IoT Hub et initialisez l’écouteur de la méthode :</span><span class="sxs-lookup"><span data-stu-id="faf62-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="faf62-126">Enregistrez et fermez le fichier **SimulatedDevice.js** .</span><span class="sxs-lookup"><span data-stu-id="faf62-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="faf62-127">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="faf62-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="faf62-128">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une nouvelle tentative de connexion), comme suggéré dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="faf62-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="faf62-129">Appeler une méthode directe sur un appareil</span><span class="sxs-lookup"><span data-stu-id="faf62-129">Call a direct method on a device</span></span>
<span data-ttu-id="faf62-130">Dans cette section, vous créez une application console .NET qui appelle une méthode sur l’application d’appareil simulé, puis affiche la réponse.</span><span class="sxs-lookup"><span data-stu-id="faf62-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="faf62-131">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="faf62-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="faf62-132">Assurez-vous que la version du .NET Framework est définie sur 4.5.1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="faf62-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="faf62-133">Nommez le projet **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="faf62-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nouveau projet Visual C# Bureau classique Windows][10]
2. <span data-ttu-id="faf62-135">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **CallMethodOnDevice**, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="faf62-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="faf62-136">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **microsoft.azure.devices**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="faf62-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="faf62-137">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="faf62-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Fenêtre du gestionnaire de package NuGet][11]

4. <span data-ttu-id="faf62-139">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="faf62-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="faf62-140">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="faf62-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="faf62-141">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="faf62-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="faf62-142">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="faf62-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="faf62-143">Cette méthode appelle une méthode directe avec le nom `writeLine` sur l’appareil `myDeviceId`.</span><span class="sxs-lookup"><span data-stu-id="faf62-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="faf62-144">Ensuite, elle écrit la réponse fournie par l’appareil sur la console.</span><span class="sxs-lookup"><span data-stu-id="faf62-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="faf62-145">Notez qu’il est possible de spécifier une valeur de délai d’attente pour la réponse de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="faf62-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="faf62-146">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="faf62-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="faf62-147">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="faf62-147">Run the applications</span></span>
<span data-ttu-id="faf62-148">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="faf62-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="faf62-149">Dans l’Explorateur de solutions de Visual Studio, cliquez avec le bouton droit sur votre solution, puis sur **Définir les projets de démarrage...**.</span><span class="sxs-lookup"><span data-stu-id="faf62-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="faf62-150">Sélectionnez **Projet de démarrage unique**, puis sélectionnez le projet **CallMethodOnDevice** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="faf62-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="faf62-151">À l’invite de commandes, dans le dossier **simulateddevice**, exécutez la commande suivante pour commencer à écouter les appels de méthode à partir de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="faf62-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="faf62-152">Attendez que l’appareil simulé s’ouvre : ![][7]</span><span class="sxs-lookup"><span data-stu-id="faf62-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="faf62-153">Maintenant que l’appareil est connecté et en attente d’appels de méthode, exécutez l’application .NET **CallMethodOnDevice** pour appeler la méthode dans l’application pour appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="faf62-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="faf62-154">Vous devriez voir la réponse de l’appareil écrite dans la console.</span><span class="sxs-lookup"><span data-stu-id="faf62-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="faf62-155">L’appareil réagit ensuite à la méthode en affichant ce message :</span><span class="sxs-lookup"><span data-stu-id="faf62-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="faf62-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="faf62-156">Next steps</span></span>
<span data-ttu-id="faf62-157">Dans ce didacticiel, vous avez configuré un nouveau IoT Hub dans le portail Azure, puis créé une identité d’appareil dans le registre des identités de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="faf62-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="faf62-158">Vous avez utilisé cette identité d’appareil pour permettre à l’application d’appareil simulé de réagir à des méthodes appelées par le cloud.</span><span class="sxs-lookup"><span data-stu-id="faf62-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="faf62-159">Vous avez également créé une application qui appelle des méthodes sur l’appareil et affiche la réponse de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="faf62-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="faf62-160">Pour continuer la prise en main de IoT Hub et explorer les autres scénarios IoT, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="faf62-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="faf62-161">[Prise en main d’IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="faf62-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="faf62-162">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="faf62-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="faf62-163">Pour savoir comment étendre votre solution IoT et planifier des appels de méthode sur plusieurs appareils, voir le didacticiel [Planifier et diffuser des travaux][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="faf62-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
<span data-ttu-id="faf62-164">[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="faf62-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
