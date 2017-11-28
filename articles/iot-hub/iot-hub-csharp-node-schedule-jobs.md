---
title: "travaux aaaSchedule avec Azure IoT Hub (nœud/.NET) | Documents Microsoft"
description: "Comment tooschedule un Azure IoT Hub travail tooinvoke une méthode directe sur plusieurs appareils. Vous utilisez du SDK de périphérique Azure IoT hello pour les applications pour appareil Node.js tooimplement hello simulée et hello Azure IoT service SDK pour .NET tooimplement un travail de service application toorun hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="f302b-104">Planifier et diffuser des travaux (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="f302b-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="f302b-105">Utilisez les Azure IoT Hub tooschedule et suivre les travaux qui mettent à jour des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="f302b-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="f302b-106">Utilisez les travaux pour :</span><span class="sxs-lookup"><span data-stu-id="f302b-106">Use jobs to:</span></span>

* <span data-ttu-id="f302b-107">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="f302b-107">Update desired properties</span></span>
* <span data-ttu-id="f302b-108">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="f302b-108">Update tags</span></span>
* <span data-ttu-id="f302b-109">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="f302b-109">Invoke direct methods</span></span>

<span data-ttu-id="f302b-110">Une tâche encapsule une de ces actions et pistes hello d’exécution par rapport à un ensemble d’appareils qui est défini par une requête de double de périphérique.</span><span class="sxs-lookup"><span data-stu-id="f302b-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="f302b-111">Par exemple, une application back-end peut utiliser un tooinvoke de travail une méthode directe sur 10 000 appareils qui redémarre les appareils hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="f302b-112">Vous spécifiez ensemble hello d’appareils avec une requête de double de périphérique et que vous planifiez hello travail toorun à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="f302b-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="f302b-113">progression assure le suivi des travaux Hello en tant que chacun des périphériques de hello recevoir et exécuter la méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="f302b-114">toolearn savoir plus sur chacune de ces fonctionnalités, consultez :</span><span class="sxs-lookup"><span data-stu-id="f302b-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="f302b-115">Double de l’appareil et les propriétés : [prise en main jumeaux de périphérique] [ lnk-get-started-twin] et [didacticiel : comment toouse appareil à deux propriétés][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="f302b-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="f302b-116">Méthodes directes : [Guide du développeur IoT Hub - Méthodes directes][lnk-dev-methods] et [Tutorial: Use direct methods][lnk-c2d-methods] (Didacticiel : utilisation des méthodes directes)</span><span class="sxs-lookup"><span data-stu-id="f302b-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="f302b-117">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="f302b-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="f302b-118">Créer une application de périphérique qui implémente une méthode directe appelée **lockDoor** qui peut être appelée par l’application back-end de hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="f302b-119">application d’appareil Hello reçoit également les modifications de propriété de votre choix à partir de l’application back-end de hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="f302b-120">Créer une application de serveur principal qui crée un Bonjour toocall de travail **lockDoor** méthode directe sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="f302b-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="f302b-121">Une autre tâche envoie la propriété désirée toomultiple périphériques des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f302b-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="f302b-122">À la fin de hello de ce didacticiel, vous avez une application console Node.js et une principal d’application console .NET (c#) :</span><span class="sxs-lookup"><span data-stu-id="f302b-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="f302b-123">**simDevice.js** qui se connecte tooyour IoT hub, implémente hello **lockDoor** direct de méthode et les handles de modifications apportées aux propriétés souhaité.</span><span class="sxs-lookup"><span data-stu-id="f302b-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="f302b-124">**ScheduleJob** qui utilise hello toocall de travaux **lockDoor** direct double périphérique hello (méthode) et mise à jour des propriétés de la sur plusieurs appareils souhaitée.</span><span class="sxs-lookup"><span data-stu-id="f302b-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="f302b-125">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f302b-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f302b-126">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f302b-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="f302b-127">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f302b-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="f302b-128">article de Hello [préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="f302b-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="f302b-129">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="f302b-129">An active Azure account.</span></span> <span data-ttu-id="f302b-130">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="f302b-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="f302b-131">Planifier des travaux pour appeler une méthode directe et envoyer des mises à jour de jumeaux d’appareils</span><span class="sxs-lookup"><span data-stu-id="f302b-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="f302b-132">Dans cette section, vous créez .NET application console (à l’aide de c#) utilise hello toocall de travaux **lockDoor** méthode directe et envoyer la propriété désirée toomultiple périphériques des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f302b-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="f302b-133">Dans Visual Studio, ajoutez une solution d’actuel toohello de projet Visual c# bureau classique de Windows à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="f302b-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="f302b-134">Projet de hello nom **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="f302b-134">Name hello project **ScheduleJob**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

1. <span data-ttu-id="f302b-136">Dans l’Explorateur de solutions, cliquez sur hello **ScheduleJob** de projet, puis cliquez sur **gérer les Packages NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="f302b-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f302b-137">Bonjour **Gestionnaire de Package NuGet** fenêtre, sélectionnez **Parcourir**, recherchez **microsoft.azure.devices**, sélectionnez **installer** tooinstall Hello **Microsoft.Azure.Devices** empaqueter et accepter les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="f302b-138">Cette étape télécharge, installe et ajoute une référence toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet package et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="f302b-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="f302b-140">Ajoutez hello suivant `using` instructions haut hello hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="f302b-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="f302b-141">Ajoutez hello suit `using` instruction si elle est déjà présent dans les instructions par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="f302b-142">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="f302b-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="f302b-143">Remplacer l’espace réservé de hello avec hello chaîne de connexion de IoT Hub hub hello que vous avez créé dans la section précédente de hello de.</span><span class="sxs-lookup"><span data-stu-id="f302b-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="f302b-144">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="f302b-144">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. <span data-ttu-id="f302b-145">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="f302b-145">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. <span data-ttu-id="f302b-146">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="f302b-146">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. <span data-ttu-id="f302b-147">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="f302b-147">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="f302b-148">Dans l’Explorateur de solutions de hello, ouvrez hello **projets de définir le démarrage...**  et assurez-vous que hello **Action** pour **ScheduleJob** projet est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="f302b-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="f302b-149">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f302b-150">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="f302b-150">Create a simulated device app</span></span>

<span data-ttu-id="f302b-151">Dans cette section, vous créez une application console Node.js qui répond tooa de méthode directe appelé par le cloud hello, qui déclenche un redémarrage de l’appareil simulé et utilise hello signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="f302b-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="f302b-152">Créez un dossier vide appelé **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="f302b-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="f302b-153">Bonjour **simDevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="f302b-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="f302b-154">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f302b-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="f302b-155">Votre invite de commandes Bonjour **simDevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt** packages :</span><span class="sxs-lookup"><span data-stu-id="f302b-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="f302b-156">À l’aide d’un éditeur de texte, créez un nouveau **simDevice.js** fichier Bonjour **simDevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="f302b-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="f302b-157">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **simDevice.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="f302b-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="f302b-158">Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="f302b-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="f302b-159">Rendre des espaces réservés de hello tooreplace que le programme d’installation de valeurs tooyour approprié.</span><span class="sxs-lookup"><span data-stu-id="f302b-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="f302b-160">Ajouter hello suivant hello toohandle de fonction **lockDoor** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f302b-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="f302b-161">Ajouter hello suivant du Gestionnaire de hello code tooregister pour hello **lockDoor** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f302b-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="f302b-162">Enregistrez et fermez hello **simDevice.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="f302b-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="f302b-163">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="f302b-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f302b-164">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="f302b-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="f302b-165">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="f302b-165">Run hello apps</span></span>

<span data-ttu-id="f302b-166">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="f302b-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="f302b-167">Invite de commandes hello Bonjour **simDevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="f302b-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="f302b-168">Application de console hello exécution c# **ScheduleJob** en cliquant sur hello **ScheduleJob** projet, puis en sélectionnant **déboguer** et **démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="f302b-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="f302b-169">Vous voyez la sortie hello à partir de périphériques et les applications de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="f302b-169">You see hello output from both device and back-end apps.</span></span>

    ![Exécuter des applications de hello tooschedule travaux][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="f302b-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f302b-171">Next steps</span></span>

<span data-ttu-id="f302b-172">Dans ce didacticiel, vous avez utilisé un travail tooschedule un appareil de tooa méthode directe et la mise à jour de hello des propriétés du double hello appareil.</span><span class="sxs-lookup"><span data-stu-id="f302b-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="f302b-173">toocontinue mise en route avec les modèles de gestion des IoT Hub et de périphérique tel que distant sur hello air microprogramme mise à jour, consultez [didacticiel : comment toodo un microprogramme mettre à jour][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="f302b-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="f302b-174">toocontinue mise en route avec IoT Hub, consultez [mise en route avec IoT bord][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="f302b-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
