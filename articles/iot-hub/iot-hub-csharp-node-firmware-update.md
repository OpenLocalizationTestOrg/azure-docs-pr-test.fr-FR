---
title: "Mise à jour d’un microprogramme d’appareil avec Azure IoT Hub (.NET/Node) | Microsoft Docs"
description: "Guide d’utilisation de la gestion des appareils sur Azure IoT Hub pour lancer une mise à jour du microprogramme d’un appareil. Vous utilisez Azure IoT device SDK pour Node.js afin d’implémenter une application d’appareil simulé et Azure IoT service SDK pour .NET afin d’implémenter une application de service qui déclenche la mise à jour du microprogramme."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: c2192328a152e955d182c4a07b391c98a5960964
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-netnode"></a><span data-ttu-id="44034-104">Utilisation de la gestion des appareils pour lancer une mise à jour du microprogramme d’un appareil (.NET/Node)</span><span class="sxs-lookup"><span data-stu-id="44034-104">Use device management to initiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="44034-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="44034-105">Introduction</span></span>
<span data-ttu-id="44034-106">Dans le didacticiel [Prise en main de la gestion d’appareils][lnk-dm-getstarted], vous avez vu comment utiliser les primitives de [représentation d’appareil physique][lnk-devtwin] et de [méthodes directives][lnk-c2dmethod] pour redémarrer à distance un appareil.</span><span class="sxs-lookup"><span data-stu-id="44034-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="44034-107">Ce didacticiel utilise les mêmes primitives IoT Hub et montre comment effectuer une mise à jour du microprogramme simulée de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="44034-107">This tutorial uses the same IoT Hub primitives and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="44034-108">Ce modèle est utilisé dans l’implémentation de la mise à jour du microprogramme de l’exemple [d’implémentation d’appareil Raspberry Pi][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="44034-108">This pattern is used in the firmware update implementation for the [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="44034-109">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="44034-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="44034-110">Créez une application console .NET qui appelle une méthode directe firmwareUpdate sur l’application d’appareil simulé via votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="44034-110">Create a .NET console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="44034-111">Créez un appareil simulé qui implémente une méthode directe **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="44034-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="44034-112">Cette méthode lance un processus en plusieurs étapes qui attend de télécharger l’image du microprogramme, la télécharge et enfin, l’applique.</span><span class="sxs-lookup"><span data-stu-id="44034-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="44034-113">À chaque étape du processus de mise à jour, l’appareil utilise les propriétés signalées pour mettre à jour la progression.</span><span class="sxs-lookup"><span data-stu-id="44034-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="44034-114">À la fin de ce didacticiel, vous avez une application d’appareil de console Node.js et une application principale de console .NET (c#) :</span><span class="sxs-lookup"><span data-stu-id="44034-114">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="44034-115">**dmpatterns_fwupdate_service.js**, qui appelle une méthode directe sur l’application d’appareil simulé, affiche la réponse, et affiche périodiquement (toutes les 500 ms) les propriétés signalées mises à jour.</span><span class="sxs-lookup"><span data-stu-id="44034-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="44034-116">**TriggerFWUpdate**, qui se connecte à votre IoT Hub avec l’identité d’appareil créée précédemment, reçoit une méthode directe firmwareUpdate, s’exécute pour simuler une mise à jour du microprogramme dans un processus à plusieurs états, consistant à attendre avant de télécharger l’image, à télécharger celle-ci, puis finalement à l’appliquer.</span><span class="sxs-lookup"><span data-stu-id="44034-116">**TriggerFWUpdate**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="44034-117">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44034-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="44034-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="44034-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="44034-119">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="44034-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="44034-120">L’article [Préparer votre environnement de développement][lnk-dev-setup] décrit l’installation de Node.js pour ce didacticiel sur Windows ou sur Linux.</span><span class="sxs-lookup"><span data-stu-id="44034-120">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="44034-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="44034-121">An active Azure account.</span></span> <span data-ttu-id="44034-122">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="44034-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="44034-123">Pour créer votre IoT Hub et obtenir votre chaîne de connexion, procédez de la manière décrite dans [Prise en main de la gestion d’appareils](iot-hub-csharp-node-device-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44034-123">Follow the [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="44034-124">Déclencher une mise à jour du microprogramme à distance sur l’appareil à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="44034-124">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="44034-125">Dans cette section, vous créez une application de console .NET (à l’aide de C#) qui lance une mise à jour de microprogramme à distance sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="44034-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="44034-126">L’application utilise une méthode directe pour lancer la mise à jour et des requêtes de jumeau d’appareil pour obtenir régulièrement l’état de la mise à jour du microprogramme actif.</span><span class="sxs-lookup"><span data-stu-id="44034-126">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="44034-127">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="44034-127">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="44034-128">Nommez le projet **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="44034-128">Name the project **TriggerFWUpdate**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

1. <span data-ttu-id="44034-130">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **TriggerFWUpdate** puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="44034-130">In Solution Explorer, right-click the **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="44034-131">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **microsoft.azure.devices**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="44034-131">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="44034-132">Cette procédure lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="44034-132">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="44034-134">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="44034-134">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="44034-135">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="44034-135">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="44034-136">Remplacez la valeur des espaces réservés par la chaîne de connexion pour le IoT Hub créé dans la section précédente et l’ID de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="44034-136">Replace the multiple placeholder values with the IoT Hub connection string for the hub that you created in the previous section and the Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="44034-137">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="44034-137">Add the following method to the **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="44034-138">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="44034-138">Add the following method to the **Program** class:</span></span>

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. <span data-ttu-id="44034-139">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="44034-139">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
1. <span data-ttu-id="44034-140">Dans l’Explorateur de solutions, sélectionnez **Définir les projets de démarrage...** et vérifiez que l’**Action** définie pour le projet **TriggerFWUpdate** est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="44034-140">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="44034-141">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="44034-141">Build the solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="44034-142">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="44034-142">Run the apps</span></span>
<span data-ttu-id="44034-143">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="44034-143">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="44034-144">À l’invite de commandes, dans le dossier **manageddevice**, exécutez la commande suivante pour commencer à écouter la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="44034-144">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="44034-145">Dans Visual Studio, cliquez avec le bouton droit sur le projet **TriggerFWUpdate**. Exécutez l’application console C#, sélectionnez **Déboguer** et **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="44034-145">In Visual Studio, right-click on the **TriggerFWUpdate** projectRun to the C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="44034-146">La réponse de l’appareil à la méthode directe s’affiche dans la console.</span><span class="sxs-lookup"><span data-stu-id="44034-146">You see the device response to the direct method in the console.</span></span>

    ![Le microprogramme a été mis à jour][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="44034-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44034-148">Next steps</span></span>
<span data-ttu-id="44034-149">Dans ce didacticiel, vous avez utilisé une méthode directe pour déclencher une mise à jour du microprogramme à distance sur un appareil, et utilisé les propriétés signalées pour suivre la progression de la mise à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="44034-149">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="44034-150">Pour savoir comment étendre votre solution IoT et planifier des appels de méthode sur plusieurs appareils, voir le didacticiel [Planifier et diffuser des travaux][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="44034-150">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/