---
title: Planification des travaux avec Azure IoT Hub (.NET/Node) | Microsoft Docs
description: "Procédure de planification d’une tâche Azure IoT Hub pour appeler une méthode directe sur plusieurs appareils. Vous utilisez Azure IoT device SDK pour Node.js afin d’implémenter les applications d’appareil simulé et Azure IoT service SDK pour .NET afin d’implémenter une application de service qui exécute la tâche."
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
ms.openlocfilehash: a8f4f34aa99c4a9966957cac213ec9170de80a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="97a50-104">Planifier et diffuser des travaux (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="97a50-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="97a50-105">Utilisez Azure IoT Hub pour planifier et suivre des travaux qui mettent à jour des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="97a50-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="97a50-106">Utilisez les travaux pour :</span><span class="sxs-lookup"><span data-stu-id="97a50-106">Use jobs to:</span></span>

* <span data-ttu-id="97a50-107">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="97a50-107">Update desired properties</span></span>
* <span data-ttu-id="97a50-108">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="97a50-108">Update tags</span></span>
* <span data-ttu-id="97a50-109">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="97a50-109">Invoke direct methods</span></span>

<span data-ttu-id="97a50-110">Un travail encapsule l’une de ces actions et suit l’exécution sur un ensemble d’appareils, défini par une requête de jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="97a50-110">A job wraps one of these actions and tracks the execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="97a50-111">Par exemple, une application principale peut utiliser un travail pour appeler une méthode directe sur 10 000 appareils, qui les redémarre.</span><span class="sxs-lookup"><span data-stu-id="97a50-111">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="97a50-112">Vous spécifiez l’ensemble des appareils avec une requête de jumeau d’appareil et planifiez le travail à exécuter ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="97a50-112">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="97a50-113">Le travail suit la progression à mesure que chacun de ces appareils reçoit et exécute la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="97a50-113">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="97a50-114">Pour plus d’informations sur chacune de ces fonctionnalités, consultez les pages :</span><span class="sxs-lookup"><span data-stu-id="97a50-114">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="97a50-115">Représentation d’appareil et propriétés : [Prise en main des représentations d’appareil][lnk-get-started-twin] et [Tutorial: How to use device twin properties][lnk-twin-props] (Didacticiel : Utilisation des propriétés de représentation d’appareil)</span><span class="sxs-lookup"><span data-stu-id="97a50-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="97a50-116">Méthodes directes : [Guide du développeur IoT Hub - Méthodes directes][lnk-dev-methods] et [Tutorial: Use direct methods][lnk-c2d-methods] (Didacticiel : utilisation des méthodes directes)</span><span class="sxs-lookup"><span data-stu-id="97a50-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="97a50-117">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="97a50-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="97a50-118">Créer une application pour appareils implémentant une méthode directe nommée **lockDoor**, qui peut être appelée par l’application principale.</span><span class="sxs-lookup"><span data-stu-id="97a50-118">Create a device app that implements a direct method called **lockDoor** that can be called by the back-end app.</span></span> <span data-ttu-id="97a50-119">L’application pour appareils reçoit également les modifications de propriétés souhaitées envoyées par l’application principale.</span><span class="sxs-lookup"><span data-stu-id="97a50-119">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="97a50-120">Créer une application principale qui crée un travail pour appeler la méthode directe **lockDoor** sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="97a50-120">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="97a50-121">Un autre travail envoie les mises à jour de propriétés souhaitées à plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="97a50-121">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="97a50-122">À la fin de ce didacticiel, vous avez une application d’appareil de console Node.js et une application principale de console .NET (c#) :</span><span class="sxs-lookup"><span data-stu-id="97a50-122">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="97a50-123">**simDevice.js** qui se connecte au hub IoT, implémente la méthode directe **lockDoor** et gère les modifications de propriétés souhaitées.</span><span class="sxs-lookup"><span data-stu-id="97a50-123">**simDevice.js** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="97a50-124">**ScheduleJob** qui utilise les travaux pour appeler la méthode directe **lockDoor** et mettre à jour les propriétés souhaitées du jumeau de plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="97a50-124">**ScheduleJob** that uses jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="97a50-125">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="97a50-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="97a50-126">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="97a50-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="97a50-127">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="97a50-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="97a50-128">L’article [Préparer votre environnement de développement][lnk-dev-setup] décrit l’installation de Node.js pour ce didacticiel sur Windows ou sur Linux.</span><span class="sxs-lookup"><span data-stu-id="97a50-128">The article [Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="97a50-129">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="97a50-129">An active Azure account.</span></span> <span data-ttu-id="97a50-130">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="97a50-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="97a50-131">Planifier des travaux pour appeler une méthode directe et envoyer des mises à jour de jumeaux d’appareils</span><span class="sxs-lookup"><span data-stu-id="97a50-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="97a50-132">Dans cette section, vous allez créer une application console .NET (en C#) qui utilise des travaux pour appeler la méthode directe **lockDoor** et envoyer les mises à jour des propriétés souhaitées à plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="97a50-132">In this section, you create a .NET console app (using C#) that uses jobs to call the **lockDoor** direct method and send desired property updates to multiple devices.</span></span>

1. <span data-ttu-id="97a50-133">Dans Visual Studio, ajoutez un projet Visual C# Bureau classique Windows à la solution actuelle en utilisant le modèle de projet **Application Console** .</span><span class="sxs-lookup"><span data-stu-id="97a50-133">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="97a50-134">Nommez le projet **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="97a50-134">Name the project **ScheduleJob**.</span></span>

    ![Nouveau projet Visual C# Bureau classique Windows][img-createapp]

1. <span data-ttu-id="97a50-136">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **ScheduleJob**, puis cliquez sur **Gérer les packages NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="97a50-136">In Solution Explorer, right-click the **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="97a50-137">Dans la fenêtre **Gestionnaire de package NuGet**, cliquez sur **Parcourir**, puis recherchez **microsoft.azure.devices**. Cliquez ensuite sur **Installer** pour installer le package **Microsoft.Azure.Devices**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="97a50-137">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="97a50-138">Cette étape lance le téléchargement et l’installation et ajoute une référence au [package Azure IoT Service SDK NuGet][lnk-nuget-service-sdk] et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="97a50-138">This step downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Fenêtre du gestionnaire de package NuGet][img-servicenuget]
1. <span data-ttu-id="97a50-140">Ajoutez les instructions `using` suivantes en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="97a50-140">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="97a50-141">Ajoutez l’instruction `using` suivante si elle ne figure pas déjà dans les instructions par défaut.</span><span class="sxs-lookup"><span data-stu-id="97a50-141">Add the following `using` statement if not already present in the default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="97a50-142">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="97a50-142">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="97a50-143">Remplacez la valeur d’espace réservé par la chaîne de connexion IoT Hub pour le hub créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="97a50-143">Replace the placeholder with the IoT Hub connection string for the hub that you created in the previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="97a50-144">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="97a50-144">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="97a50-145">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="97a50-145">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="97a50-146">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="97a50-146">Add the following method to the **Program** class:</span></span>

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

1. <span data-ttu-id="97a50-147">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="97a50-147">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER to run the next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER to exit.");
    Console.ReadLine();
    ```

1. <span data-ttu-id="97a50-148">Dans l’Explorateur de solutions, sélectionnez **Définir les projets de démarrage...** et vérifiez que l’**Action** définie pour le projet **ScheduleJob** est **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="97a50-148">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="97a50-149">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="97a50-149">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="97a50-150">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="97a50-150">Create a simulated device app</span></span>

<span data-ttu-id="97a50-151">Dans cette section, vous créez une application console Node.js qui répond à une méthode directe appelée par le cloud, qui déclenche un redémarrage de l’appareil simulé et utilise les propriétés signalées pour permettre aux requêtes de la représentation d’appareil d’identifier des appareils et de déterminer le moment de leur dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="97a50-151">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="97a50-152">Créez un dossier vide appelé **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="97a50-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="97a50-153">Dans le dossier **simDevice** , créez un fichier package.json à l’aide de la commande ci-dessous, à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="97a50-153">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="97a50-154">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="97a50-154">Accept all the defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="97a50-155">À l’invite de commandes, dans le dossier **simDevice**, exécutez la commande suivante pour installer les packages **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="97a50-155">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="97a50-156">Dans un éditeur de texte, créez un fichier **simDevice.js** dans le dossier **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="97a50-156">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>

1. <span data-ttu-id="97a50-157">Ajoutez les instructions ’require’ ci-dessous au début du fichier **simDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="97a50-157">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="97a50-158">Ajoutez une variable **connectionString** et utilisez-la pour créer une instance de **Client**.</span><span class="sxs-lookup"><span data-stu-id="97a50-158">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="97a50-159">Veillez à remplacer les espaces réservés par des valeurs appropriées à votre installation.</span><span class="sxs-lookup"><span data-stu-id="97a50-159">Make sure to replace the placeholders with values appropriate to your setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="97a50-160">Ajoutez la fonction suivante pour gérer la méthode **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="97a50-160">Add the following function to handle the **lockDoor** method.</span></span>

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. <span data-ttu-id="97a50-161">Ajoutez le code suivant pour inscrire le gestionnaire de la méthode **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="97a50-161">Add the following code to register the handler for the **lockDoor** method.</span></span>

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. <span data-ttu-id="97a50-162">Enregistrez et fermez le fichier **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="97a50-162">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="97a50-163">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="97a50-163">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="97a50-164">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="97a50-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="97a50-165">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="97a50-165">Run the apps</span></span>

<span data-ttu-id="97a50-166">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="97a50-166">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="97a50-167">À l’invite de commandes, dans le dossier **simDevice**, exécutez la commande suivante pour commencer à écouter la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="97a50-167">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="97a50-168">Exécutez l’application console C# **ScheduleJob** en cliquant avec le bouton droit sur le projet **ScheduleJob**, puis en sélectionnant **Débogage** et **Démarrer une nouvelle instance**.</span><span class="sxs-lookup"><span data-stu-id="97a50-168">Run the C# console app **ScheduleJob** by right-clicking on the **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="97a50-169">La sortie de l’appareil et des applications principales s’affiche.</span><span class="sxs-lookup"><span data-stu-id="97a50-169">You see the output from both device and back-end apps.</span></span>

    ![Exécuter les applications pour planifier des tâches][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="97a50-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="97a50-171">Next steps</span></span>

<span data-ttu-id="97a50-172">Dans ce didacticiel, vous avez utilisé un travail pour planifier une méthode directe sur un appareil et la mise à jour des propriétés de représentation de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="97a50-172">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="97a50-173">Pour approfondir la prise en main d’IoT Hub et des modèles de gestion d’appareils, comme la mise à jour du microprogramme à distance, consultez le [Didacticiel : Mettre à jour un microprogramme][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="97a50-173">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, read [Tutorial: How to do a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="97a50-174">Afin d’approfondir l’apprentissage de IoT Hub, consultez [Getting started with IoT Edge][lnk-iot-edge] (Bien démarrer avec IoT Edge).</span><span class="sxs-lookup"><span data-stu-id="97a50-174">To continue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
