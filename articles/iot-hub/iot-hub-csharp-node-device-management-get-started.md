---
title: Prise en main de la gestion des appareils Azure IoT Hub (.NET/Node) | Microsoft Docs
description: "Guide d’utilisation de la gestion des appareils Azure IoT Hub pour lancer un redémarrage d’appareil à distance. Vous utilisez Azure IoT device SDK pour Node.js afin d’implémenter une application d’appareil simulé qui inclut une méthode directe et Azure IoT service SDK pour .NET afin d’implémenter une application de service qui appelle la méthode directe."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="1afa2-104">Prise en main de la gestion d’appareils (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="1afa2-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="1afa2-105">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="1afa2-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="1afa2-106">Utiliser le portail Azure pour créer un IoT Hub et une identité d’appareil dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1afa2-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="1afa2-107">Créer une application d’appareil simulé disposant d’une méthode directe permettant le redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="1afa2-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="1afa2-108">Les méthodes directes sont appelées à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="1afa2-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="1afa2-109">Créer une application console .NET qui appelle une méthode directe de redémarrage sur l’application d’appareil simulé via votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1afa2-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="1afa2-110">À la fin de ce didacticiel, vous avez une application d’appareil de console Node.js et une application principale de console .NET (c#) :</span><span class="sxs-lookup"><span data-stu-id="1afa2-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="1afa2-111">**dmpatterns_getstarted_device.js**, qui se connecte à votre IoT Hub avec l’identité d’appareil créée précédemment, reçoit une méthode directe de redémarrage, simule un redémarrage physique et indique l’heure du dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="1afa2-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="1afa2-112">**TriggerReboot**, qui appelle une méthode directe sur l’application d’appareil simulé, affiche la réponse et les propriétés signalées mises à jour.</span><span class="sxs-lookup"><span data-stu-id="1afa2-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="1afa2-113">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1afa2-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1afa2-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1afa2-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="1afa2-115">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1afa2-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="1afa2-116">L’article [Préparer votre environnement de développement][lnk-dev-setup] décrit l’installation de Node.js pour ce didacticiel sur Windows ou sur Linux.</span><span class="sxs-lookup"><span data-stu-id="1afa2-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="1afa2-117">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1afa2-117">An active Azure account.</span></span> <span data-ttu-id="1afa2-118">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="1afa2-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="1afa2-119">Déclencher un redémarrage à distance sur l’appareil à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="1afa2-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="1afa2-120">Dans cette section, vous créez une application console .NET (à l’aide de C#) qui lance un redémarrage à distance sur un appareil avec une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="1afa2-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="1afa2-121">L’application utilise des requêtes du jumeau d’appareil pour déterminer l’heure du dernier redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="1afa2-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="1afa2-122">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à une nouvelle solution en utilisant le modèle de projet **Application console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="1afa2-123">Assurez-vous que la version du .NET Framework est définie sur 4.5.1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="1afa2-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="1afa2-124">Nommez le projet **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-124">Name the project **TriggerReboot**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

2. <span data-ttu-id="1afa2-126">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **TriggerReboot**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="1afa2-127">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **microsoft.azure.devices**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1afa2-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="1afa2-128">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="1afa2-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
4. <span data-ttu-id="1afa2-130">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="1afa2-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="1afa2-131">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="1afa2-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="1afa2-132">Remplacez la valeur d’espace réservé par la chaîne de connexion pour le IoT Hub créé dans la section précédente et l’appareil cible.</span><span class="sxs-lookup"><span data-stu-id="1afa2-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="1afa2-133">Ajoutez la méthode suivante à la classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="1afa2-134">Ce code obtient la représentation d’appareil pour le redémarrage de l’appareil et renvoie les propriétés signalées.</span><span class="sxs-lookup"><span data-stu-id="1afa2-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="1afa2-135">Ajoutez la méthode suivante à la classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="1afa2-136">Ce code lance un redémarrage à distance sur l’appareil à l’aide d’une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="1afa2-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="1afa2-137">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="1afa2-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="1afa2-138">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="1afa2-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="1afa2-139">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="1afa2-139">Create a simulated device app</span></span>
<span data-ttu-id="1afa2-140">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="1afa2-140">In this section, you will</span></span>

* <span data-ttu-id="1afa2-141">Créer une application console Node.js qui répond à une méthode directe appelée par le cloud</span><span class="sxs-lookup"><span data-stu-id="1afa2-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="1afa2-142">Déclencher un redémarrage d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="1afa2-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="1afa2-143">Utiliser les propriétés signalées pour activer les requêtes sur la représentation d’appareil afin d’identifier les appareils et l’heure de leur dernier redémarrage</span><span class="sxs-lookup"><span data-stu-id="1afa2-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="1afa2-144">Créez un dossier vide nommé **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="1afa2-145">Dans le dossier **simulateddevice**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="1afa2-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="1afa2-146">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="1afa2-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="1afa2-147">À l’invite de commandes, dans le dossier **manageddevice**, exécutez la commande suivante pour installer les packages Kit de développement logiciel (SDK) pour appareils **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="1afa2-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="1afa2-148">À l’aide d’un éditeur de texte, créez un fichier **dmpatterns_getstarted_device.js** dans le dossier **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="1afa2-149">Ajoutez les instructions 'require' suivantes au début du fichier **dmpatterns_getstarted_device.js** :</span><span class="sxs-lookup"><span data-stu-id="1afa2-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="1afa2-150">Ajoutez une variable **connectionString** et utilisez-la pour créer une instance de **Client**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="1afa2-151">Remplacez la chaîne de connexion par la chaîne de connexion de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="1afa2-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="1afa2-152">Ajoutez la fonction suivante pour implémenter la méthode directe sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="1afa2-152">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. <span data-ttu-id="1afa2-153">Ajoutez le code suivant pour ouvrir la connexion à votre IoT Hub et démarrez l’écouteur de la méthode directe :</span><span class="sxs-lookup"><span data-stu-id="1afa2-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. <span data-ttu-id="1afa2-154">Enregistrez et fermez le fichier **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="1afa2-155">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="1afa2-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1afa2-156">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1afa2-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="1afa2-157">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="1afa2-157">Run the apps</span></span>
<span data-ttu-id="1afa2-158">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="1afa2-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="1afa2-159">À l’invite de commandes, dans le dossier **manageddevice**, exécutez la commande suivante pour commencer à écouter la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="1afa2-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="1afa2-160">Exécutez l’application console C# **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="1afa2-161">Cliquez avec le bouton droit sur le projet **TriggerReboot**, puis sélectionnez **Debug** et **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="1afa2-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="1afa2-162">La réponse de l’appareil à la méthode directe s’affiche dans la console.</span><span class="sxs-lookup"><span data-stu-id="1afa2-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/