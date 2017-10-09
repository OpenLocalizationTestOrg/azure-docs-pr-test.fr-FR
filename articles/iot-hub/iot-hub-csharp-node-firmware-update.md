---
title: "mise à jour de microprogramme aaaDevice avec Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment mettre à jour toouse la gestion des appareils sur Azure IoT Hub tooinitiate un microprogramme de l’appareil. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et hello Azure IoT service SDK pour .NET tooimplement une application de service qui déclenche la mise à jour du microprogramme hello."
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
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a><span data-ttu-id="72ac3-104">Utiliser la gestion de périphérique tooinitiate une mise à jour du microprogramme de périphérique (nœud/.NET)</span><span class="sxs-lookup"><span data-stu-id="72ac3-104">Use device management tooinitiate a device firmware update (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="72ac3-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="72ac3-105">Introduction</span></span>
<span data-ttu-id="72ac3-106">Bonjour [prise en main la gestion des appareils] [ lnk-dm-getstarted] didacticiel, vous avez vu comment toouse hello [double de l’appareil] [ lnk-devtwin] et [directe méthodes] [ lnk-c2dmethod] tooremotely de primitives redémarrer un appareil.</span><span class="sxs-lookup"><span data-stu-id="72ac3-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="72ac3-107">Ce didacticiel utilise hello mêmes primitives IoT Hub et vous montre comment toodo un bout en bout simulée mise à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="72ac3-107">This tutorial uses hello same IoT Hub primitives and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="72ac3-108">Ce modèle est utilisé dans l’implémentation de mise à jour du microprogramme hello pour hello [exemple d’implémentation framboises Pi appareil][lnk-rpi-implementation].</span><span class="sxs-lookup"><span data-stu-id="72ac3-108">This pattern is used in hello firmware update implementation for hello [Raspberry Pi device implementation sample][lnk-rpi-implementation].</span></span>

<span data-ttu-id="72ac3-109">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="72ac3-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="72ac3-110">Créer une application console .NET qui appelle la méthode directe de hello firmwareUpdate dans l’application d’appareil simulé hello via votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="72ac3-110">Create a .NET console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="72ac3-111">Créez un appareil simulé qui implémente une méthode directe **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="72ac3-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="72ac3-112">Cette méthode lance un processus en plusieurs étapes qui attend l’image de microprogramme toodownload hello, télécharge l’image de microprogramme hello et enfin applique image de microprogramme hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="72ac3-113">Lors de chaque étape de mise à jour hello, hello périphérique utilise hello signalée tooreport de propriétés sur la progression.</span><span class="sxs-lookup"><span data-stu-id="72ac3-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="72ac3-114">À la fin de hello de ce didacticiel, vous avez une application console Node.js et une principal d’application console .NET (c#) :</span><span class="sxs-lookup"><span data-stu-id="72ac3-114">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="72ac3-115">**dmpatterns_fwupdate_service.js**, qui appelle une méthode directe dans l’application d’appareil simulé hello, réponse de hello s’affiche et périodiquement (chaque 500 ms) hello affiche mis à jour signalés propriétés.</span><span class="sxs-lookup"><span data-stu-id="72ac3-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="72ac3-116">**TriggerFWUpdate**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe firmwareUpdate, s’exécute via un toosimulate plusieurs États de processus pour une mise à jour de microprogramme, y compris : en attente de téléchargement de l’image hello, Télécharger la nouvelle image de hello et enfin application hello image.</span><span class="sxs-lookup"><span data-stu-id="72ac3-116">**TriggerFWUpdate**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="72ac3-117">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="72ac3-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="72ac3-118">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="72ac3-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="72ac3-119">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="72ac3-119">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="72ac3-120">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="72ac3-120">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="72ac3-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="72ac3-121">An active Azure account.</span></span> <span data-ttu-id="72ac3-122">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="72ac3-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="72ac3-123">Suivez hello [prise en main la gestion des appareils](iot-hub-csharp-node-device-management-get-started.md) article toocreate votre IoT hub et obtenir votre chaîne de connexion de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="72ac3-123">Follow hello [Get started with device management](iot-hub-csharp-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="72ac3-124">Déclencher une mise à jour de microprogramme à distance sur l’appareil hello à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="72ac3-124">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="72ac3-125">Dans cette section, vous créez une application de console .NET (à l’aide de C#) qui lance une mise à jour de microprogramme à distance sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="72ac3-125">In this section, you create a .NET console app (using C#) that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="72ac3-126">application Hello utilise une mise à jour de méthode directe tooinitiate hello et utilise appareil double requêtes tooperiodically obtenir l’état de hello de mise à jour du microprogramme active hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-126">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="72ac3-127">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="72ac3-127">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="72ac3-128">Projet de hello nom **TriggerFWUpdate**.</span><span class="sxs-lookup"><span data-stu-id="72ac3-128">Name hello project **TriggerFWUpdate**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

1. <span data-ttu-id="72ac3-130">Dans l’Explorateur de solutions, cliquez sur hello **TriggerFWUpdate** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="72ac3-130">In Solution Explorer, right-click hello **TriggerFWUpdate** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="72ac3-131">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-131">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="72ac3-132">Cette procédure télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="72ac3-132">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="72ac3-134">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="72ac3-134">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. <span data-ttu-id="72ac3-135">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="72ac3-135">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="72ac3-136">Remplacez hello plusieurs valeurs d’espace réservé avec hello la chaîne de connexion de IoT Hub pour le hub hello que vous avez créé dans la section précédente de hello et hello Id de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="72ac3-136">Replace hello multiple placeholder values with hello IoT Hub connection string for hello hub that you created in hello previous section and hello Id of your device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. <span data-ttu-id="72ac3-137">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="72ac3-137">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. <span data-ttu-id="72ac3-138">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="72ac3-138">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="72ac3-139">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="72ac3-139">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. <span data-ttu-id="72ac3-140">Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **TriggerFWUpdate** projet est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="72ac3-140">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **TriggerFWUpdate** project is **Start**.</span></span>

1. <span data-ttu-id="72ac3-141">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-141">Build hello solution.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="72ac3-142">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="72ac3-142">Run hello apps</span></span>
<span data-ttu-id="72ac3-143">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="72ac3-143">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="72ac3-144">Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-144">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="72ac3-145">Dans Visual Studio, cliquez sur hello **TriggerFWUpdate** projectRun toohello c# application console, sélectionnez **déboguer** et **démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="72ac3-145">In Visual Studio, right-click on hello **TriggerFWUpdate** projectRun toohello C# console app, select **Debug** and **Start new instance**.</span></span>

3. <span data-ttu-id="72ac3-146">Vous consultez hello appareil réponse toohello méthode directe dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-146">You see hello device response toohello direct method in hello console.</span></span>

    ![Le microprogramme a été mis à jour][img-fwupdate]

## <a name="next-steps"></a><span data-ttu-id="72ac3-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72ac3-148">Next steps</span></span>
<span data-ttu-id="72ac3-149">Dans ce didacticiel, vous avez utilisé un tootrigger méthode directe à une distance mise à jour de microprogramme sur un appareil et un hello utilisé signalé progression de hello toofollow propriétés de mise à jour du microprogramme hello.</span><span class="sxs-lookup"><span data-stu-id="72ac3-149">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="72ac3-150">toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="72ac3-150">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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