---
title: Planification des travaux avec Azure IoT Hub (Node) | Microsoft Docs
description: "Procédure de planification d’une tâche Azure IoT Hub pour appeler une méthode directe sur plusieurs appareils. Vous pouvez utiliser les kits de développement logiciel (SDK) Azure IoT pour Node.js afin d’implémenter les applications d’appareil simulé et une application de service pour exécuter la tâche."
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
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 42e594dc6a8a8be619b5652bf8e44cf883650489
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="39e8a-104">Planifier et diffuser des travaux (Node)</span><span class="sxs-lookup"><span data-stu-id="39e8a-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="39e8a-105">Azure IoT Hub est un service entièrement géré qui permet à une application principale de créer et de suivre des travaux qui planifient et mettent à jour des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="39e8a-105">Azure IoT Hub is a fully managed service that enables a back-end app to create and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="39e8a-106">Les travaux peuvent être utilisés pour les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="39e8a-106">Jobs can be used for the following actions:</span></span>

* <span data-ttu-id="39e8a-107">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="39e8a-107">Update desired properties</span></span>
* <span data-ttu-id="39e8a-108">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="39e8a-108">Update tags</span></span>
* <span data-ttu-id="39e8a-109">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="39e8a-109">Invoke direct methods</span></span>

<span data-ttu-id="39e8a-110">Sur le plan conceptuel, un travail encapsule l’une de ces actions et suit la progression de l’exécution par rapport à un ensemble d’appareils, défini par une requête de représentation d’appareil.</span><span class="sxs-lookup"><span data-stu-id="39e8a-110">Conceptually, a job wraps one of these actions and tracks the progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="39e8a-111">Par exemple, à l’aide d’un travail, une application principale peut appeler une méthode de redémarrage sur 10 000 appareils, spécifiée par une requête de représentation d’appareil et planifiée dans l’avenir.</span><span class="sxs-lookup"><span data-stu-id="39e8a-111">For example, a back-end app can use a job to invoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="39e8a-112">Cette application peut ensuite suivre la progression à mesure que chacun de ces appareils reçoit et exécute la méthode de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="39e8a-112">That application can then track progress as each of those devices receive and execute the reboot method.</span></span>

<span data-ttu-id="39e8a-113">Pour en savoir plus sur chacune de ces fonctionnalités, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="39e8a-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="39e8a-114">Représentation d’appareil et propriétés : [Prise en main des représentations d’appareil][lnk-get-started-twin] et [Tutorial: How to use device twin properties][lnk-twin-props] (Didacticiel : Utilisation des propriétés de représentation d’appareil)</span><span class="sxs-lookup"><span data-stu-id="39e8a-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How to use device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="39e8a-115">méthodes directes : [Guide du développeur IoT Hub - Méthodes directes][lnk-dev-methods] et [Didacticiel : méthodes directes][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="39e8a-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="39e8a-116">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="39e8a-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="39e8a-117">Créer une application d’appareil simulé disposant d’une méthode directe permettant **lockDoor** qui peut être appelé par le serveur de solutions principal.</span><span class="sxs-lookup"><span data-stu-id="39e8a-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by the solution back end.</span></span>
* <span data-ttu-id="39e8a-118">Créer une application console Node.js qui appelle la méthode directe **lockDoor** sur l’application d’appareil simulé à l’aide d’un travail et met à jour les propriétés souhaitées à l’aide d’un travail d’appareil.</span><span class="sxs-lookup"><span data-stu-id="39e8a-118">Create a Node.js console app that calls the **lockDoor** direct method in the simulated device app using a job and updates the desired properties using a device job.</span></span>

<span data-ttu-id="39e8a-119">À la fin de ce didacticiel, vous disposerez de deux applications console Node.js :</span><span class="sxs-lookup"><span data-stu-id="39e8a-119">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="39e8a-120">**simDevice.js**, qui se connecte à IoT Hub avec l’identité de l’appareil et reçoit une méthode directe **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-120">**simDevice.js**, which connects to your IoT hub with the device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="39e8a-121">**scheduleJobService.js**, qui appelle une méthode directe sur l’application d’appareil simulé et met à jour les propriétés souhaitées de la représentation d’appareil à l’aide d’un travail.</span><span class="sxs-lookup"><span data-stu-id="39e8a-121">**scheduleJobService.js**, which calls a direct method in the simulated device app and update the device twin's desired properties using a job.</span></span>

<span data-ttu-id="39e8a-122">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="39e8a-122">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="39e8a-123">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="39e8a-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="39e8a-124">L’article [Préparer votre environnement de développement][lnk-dev-setup] décrit l’installation de Node.js pour ce didacticiel sur Windows ou sur Linux.</span><span class="sxs-lookup"><span data-stu-id="39e8a-124">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="39e8a-125">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="39e8a-125">An active Azure account.</span></span> <span data-ttu-id="39e8a-126">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="39e8a-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="39e8a-127">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="39e8a-127">Create a simulated device app</span></span>
<span data-ttu-id="39e8a-128">Dans cette section, vous créez une application console Node.js qui répond à une méthode directe appelée par le cloud, qui déclenche un redémarrage de l’appareil simulé et utilise les propriétés signalées pour permettre aux requêtes de la représentation d’appareil d’identifier des appareils et de déterminer le moment de leur dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="39e8a-128">In this section, you create a Node.js console app that responds to a direct method called by the cloud, which triggers a simulated device reboot and uses the reported properties to enable device twin queries to identify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="39e8a-129">Créez un dossier vide appelé **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="39e8a-130">Dans le dossier **simDevice** , créez un fichier package.json à l’aide de la commande ci-dessous, à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="39e8a-130">In the **simDevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="39e8a-131">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="39e8a-131">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="39e8a-132">À l’invite de commandes, dans le dossier **simDevice**, exécutez la commande suivante pour installer les packages Kit de développement logiciel (SDK) pour appareils **azure-iot-device** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="39e8a-132">At your command prompt in the **simDevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="39e8a-133">Dans un éditeur de texte, créez un fichier **simDevice.js** dans le dossier **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-133">Using a text editor, create a new **simDevice.js** file in the **simDevice** folder.</span></span>
4. <span data-ttu-id="39e8a-134">Ajoutez les instructions ’require’ ci-dessous au début du fichier **simDevice.js** :</span><span class="sxs-lookup"><span data-stu-id="39e8a-134">Add the following 'require' statements at the start of the **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="39e8a-135">Ajoutez une variable **connectionString** et utilisez-la pour créer une instance de **Client**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-135">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="39e8a-136">Ajoutez la fonction suivante pour gérer la méthode **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-136">Add the following function to handle the **lockDoor** method.</span></span>
   
    ```
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
7. <span data-ttu-id="39e8a-137">Ajoutez le code suivant pour inscrire le gestionnaire de la méthode **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-137">Add the following code to register the handler for the **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect to IotHub client.');
        }  else {
            console.log('Client connected to IoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="39e8a-138">Enregistrez et fermez le fichier **simDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-138">Save and close the **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="39e8a-139">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="39e8a-139">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="39e8a-140">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="39e8a-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="39e8a-141">Planifier des travaux pour appeler une méthode directe et mettre à jour les propriétés d’une représentation d’appareil</span><span class="sxs-lookup"><span data-stu-id="39e8a-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="39e8a-142">Dans cette section, vous créez une application console Node.js qui lance **lockDoor** à distance sur un appareil à l’aide d’une méthode directe et met à jour les propriétés de représentation d’appareil.</span><span class="sxs-lookup"><span data-stu-id="39e8a-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update the device twin's properties.</span></span>

1. <span data-ttu-id="39e8a-143">Créez un dossier vide appelé **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="39e8a-144">Dans le dossier **scheduleJobService**, créez un fichier package.json à l’aide de la commande ci-dessous, à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="39e8a-144">In the **scheduleJobService** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="39e8a-145">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="39e8a-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="39e8a-146">À l’invite de commandes, dans le dossier **scheduleJobService**, exécutez la commande suivante pour installer les packages Kit de développement logiciel (SDK) pour appareils **azure-iothub** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="39e8a-146">At your command prompt in the **scheduleJobService** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="39e8a-147">À l’aide d’un éditeur de texte, créez un nouveau fichier **scheduleJobService.js** dans le dossier **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-147">Using a text editor, create a new **scheduleJobService.js** file in the **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="39e8a-148">Ajoutez les instructions ’require’ suivantes au début du fichier **dmpatterns_gscheduleJobServiceetstarted_service.js** :</span><span class="sxs-lookup"><span data-stu-id="39e8a-148">Add the following 'require' statements at the start of the **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="39e8a-149">Ajoutez les déclarations de variable suivantes et remplacez les valeurs d’espace réservé :</span><span class="sxs-lookup"><span data-stu-id="39e8a-149">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="39e8a-150">Ajoutez la fonction suivante qui permet de surveiller l’exécution du travail :</span><span class="sxs-lookup"><span data-stu-id="39e8a-150">Add the following function that will be used to monitor the execution of the job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="39e8a-151">Ajoutez le code suivant pour planifier le travail qui appelle la méthode de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="39e8a-151">Add the following code to schedule the job that calls the device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable to process method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="39e8a-152">Ajoutez le code suivant pour planifier le travail de mise à jour de la représentation d’appareil :</span><span class="sxs-lookup"><span data-stu-id="39e8a-152">Add the following code to schedule the job to update the device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="39e8a-153">Enregistrez et fermez le fichier **scheduleJobService.js**.</span><span class="sxs-lookup"><span data-stu-id="39e8a-153">Save and close the **scheduleJobService.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="39e8a-154">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="39e8a-154">Run the applications</span></span>
<span data-ttu-id="39e8a-155">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="39e8a-155">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="39e8a-156">À l’invite de commandes, dans le dossier **simDevice**, exécutez la commande suivante pour commencer à écouter la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="39e8a-156">At the command prompt in the **simDevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="39e8a-157">À l’invite de commandes dans le dossier **scheduleJobService**, exécutez la commande suivante pour déclencher les travaux afin de verrouiller la porte et de mettre à jour le jumeau</span><span class="sxs-lookup"><span data-stu-id="39e8a-157">At the command prompt in the **scheduleJobService** folder, run the following command to trigger the jobs to lock the door and update the twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="39e8a-158">La réponse de l’appareil à la méthode directe s’affiche dans la console.</span><span class="sxs-lookup"><span data-stu-id="39e8a-158">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39e8a-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39e8a-159">Next steps</span></span>
<span data-ttu-id="39e8a-160">Dans ce didacticiel, vous avez utilisé un travail pour planifier une méthode directe sur un appareil et la mise à jour des propriétés de représentation de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="39e8a-160">In this tutorial, you used a job to schedule a direct method to a device and the update of the device twin's properties.</span></span>

<span data-ttu-id="39e8a-161">Pour approfondir la prise en main d’IoT Hub et des modèles de gestion d’appareils, comme la mise à jour du microprogramme à distance, consultez :</span><span class="sxs-lookup"><span data-stu-id="39e8a-161">To continue getting started with IoT Hub and device management patterns such as remote over the air firmware update, see:</span></span>

<span data-ttu-id="39e8a-162">[Didacticiel : Mettre à jour un microprogramme][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="39e8a-162">[Tutorial: How to do a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="39e8a-163">Afin d’approfondir l’apprentissage de IoT Hub, consultez [Getting started with Azure IoT Edge][lnk-iot-edge] (Bien démarrer avec Azure IoT Edge).</span><span class="sxs-lookup"><span data-stu-id="39e8a-163">To continue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
