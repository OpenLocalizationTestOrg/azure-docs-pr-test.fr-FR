---
title: "travaux aaaSchedule avec Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment tooschedule un Azure IoT Hub travail tooinvoke une méthode directe sur plusieurs appareils. Vous utilisez IoT kits de développement Azure hello pour les applications pour appareil Node.js tooimplement hello simulé et un travail de service application toorun hello."
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
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="631b8-104">Planifier et diffuser des travaux (Node)</span><span class="sxs-lookup"><span data-stu-id="631b8-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="631b8-105">IoT Hub Azure est un service entièrement géré qui permet une toocreate d’applications principal et les travaux suivi planifier et mettre à jour des millions d’appareils.</span><span class="sxs-lookup"><span data-stu-id="631b8-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="631b8-106">Travaux peuvent être utilisés pour hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="631b8-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="631b8-107">Mettre à jour les propriétés souhaitées</span><span class="sxs-lookup"><span data-stu-id="631b8-107">Update desired properties</span></span>
* <span data-ttu-id="631b8-108">Mettre à jour les balises</span><span class="sxs-lookup"><span data-stu-id="631b8-108">Update tags</span></span>
* <span data-ttu-id="631b8-109">Appeler des méthodes directes</span><span class="sxs-lookup"><span data-stu-id="631b8-109">Invoke direct methods</span></span>

<span data-ttu-id="631b8-110">Point de vue conceptuel, une tâche encapsule l’un de ces actions et assure le suivi hello la progression de l’exécution par rapport à un ensemble d’appareils, qui est défini par une requête de double du périphérique.</span><span class="sxs-lookup"><span data-stu-id="631b8-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="631b8-111">Par exemple, une application back-end peut utiliser un tooinvoke de travail une méthode de redémarrage sur 10 000 périphériques, spécifié par une requête de double dispositif et planifiées à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="631b8-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="631b8-112">Cette application peut puis suivent la progression que chacun de ces périphériques de réception et exécuter la méthode de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="631b8-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="631b8-113">Pour en savoir plus sur chacune de ces fonctionnalités, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="631b8-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="631b8-114">Double de l’appareil et les propriétés : [prise en main jumeaux de périphérique] [ lnk-get-started-twin] et [didacticiel : comment toouse appareil à deux propriétés][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="631b8-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="631b8-115">méthodes directes : [Guide du développeur IoT Hub - Méthodes directes][lnk-dev-methods] et [Didacticiel : méthodes directes][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="631b8-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="631b8-116">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="631b8-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="631b8-117">Créer une application d’appareil simulé qui possède une méthode directe qui permet de **lockDoor** qui peut être appelé par hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="631b8-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="631b8-118">Créer une application de console Node.js que hello appels **lockDoor** méthode directe dans l’application d’appareil simulé hello à l’aide d’un Bonjour de travail et les mises à jour souhaitée des propriétés à l’aide d’un travail de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="631b8-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="631b8-119">À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="631b8-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="631b8-120">**simDevice.js**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello et reçoit un **lockDoor** méthode directe.</span><span class="sxs-lookup"><span data-stu-id="631b8-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="631b8-121">**scheduleJobService.js**, qui appelle une méthode directe périphérique hello hello appareil simulé application et mise à jour les propriétés souhaitées de double à l’aide d’un travail.</span><span class="sxs-lookup"><span data-stu-id="631b8-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="631b8-122">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="631b8-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="631b8-123">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="631b8-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="631b8-124">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="631b8-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="631b8-125">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="631b8-125">An active Azure account.</span></span> <span data-ttu-id="631b8-126">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="631b8-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="631b8-127">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="631b8-127">Create a simulated device app</span></span>
<span data-ttu-id="631b8-128">Dans cette section, vous créez une application console Node.js qui répond tooa de méthode directe appelé par le cloud hello, qui déclenche un redémarrage de l’appareil simulé et utilise hello signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="631b8-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="631b8-129">Créez un dossier vide appelé **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="631b8-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="631b8-130">Bonjour **simDevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="631b8-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="631b8-131">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="631b8-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="631b8-132">Votre invite de commandes Bonjour **simDevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt** package :</span><span class="sxs-lookup"><span data-stu-id="631b8-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="631b8-133">À l’aide d’un éditeur de texte, créez un nouveau **simDevice.js** fichier Bonjour **simDevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="631b8-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="631b8-134">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **simDevice.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="631b8-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="631b8-135">Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="631b8-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="631b8-136">Ajouter hello suivant hello toohandle de fonction **lockDoor** (méthode).</span><span class="sxs-lookup"><span data-stu-id="631b8-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
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
7. <span data-ttu-id="631b8-137">Ajouter hello suivant du Gestionnaire de hello code tooregister pour hello **lockDoor** (méthode).</span><span class="sxs-lookup"><span data-stu-id="631b8-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="631b8-138">Enregistrez et fermez hello **simDevice.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="631b8-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="631b8-139">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="631b8-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="631b8-140">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="631b8-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="631b8-141">Planifier des travaux pour appeler une méthode directe et mettre à jour les propriétés d’une représentation d’appareil</span><span class="sxs-lookup"><span data-stu-id="631b8-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="631b8-142">Dans cette section, vous créez une application de console Node.js qui lance une distance **lockDoor** sur un périphérique à l’aide des propriétés d’un directe mise à jour et la méthode hello appareil double.</span><span class="sxs-lookup"><span data-stu-id="631b8-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="631b8-143">Créez un dossier vide appelé **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="631b8-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="631b8-144">Bonjour **scheduleJobService** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="631b8-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="631b8-145">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="631b8-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="631b8-146">Votre invite de commandes Bonjour **scheduleJobService** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :</span><span class="sxs-lookup"><span data-stu-id="631b8-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="631b8-147">À l’aide d’un éditeur de texte, créez un nouveau **scheduleJobService.js** fichier Bonjour **scheduleJobService** dossier.</span><span class="sxs-lookup"><span data-stu-id="631b8-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="631b8-148">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_gscheduleJobServiceetstarted_service.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="631b8-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="631b8-149">Ajouter hello après les déclarations de variable et remplacez les valeurs d’espace réservé hello :</span><span class="sxs-lookup"><span data-stu-id="631b8-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="631b8-150">Ajoutez hello suivant fonction qui sera utilisé toomonitor l’exécution de hello du travail de hello :</span><span class="sxs-lookup"><span data-stu-id="631b8-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
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
7. <span data-ttu-id="631b8-151">Ajoutez hello suivant code tooschedule hello travail qui appelle la méthode de périphérique hello :</span><span class="sxs-lookup"><span data-stu-id="631b8-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
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
8. <span data-ttu-id="631b8-152">Ajoutez hello suivant double périphérique de code tooschedule hello travail tooupdate hello :</span><span class="sxs-lookup"><span data-stu-id="631b8-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
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
9. <span data-ttu-id="631b8-153">Enregistrez et fermez hello **scheduleJobService.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="631b8-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="631b8-154">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="631b8-154">Run hello applications</span></span>
<span data-ttu-id="631b8-155">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="631b8-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="631b8-156">Invite de commandes hello Bonjour **simDevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="631b8-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="631b8-157">Invite de commandes hello Bonjour **scheduleJobService** dossier, exécutez hello suivant commande tootrigger hello travaux toolock hello porte et mise à jour hello double</span><span class="sxs-lookup"><span data-stu-id="631b8-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="631b8-158">Vous consultez hello appareil réponse toohello méthode directe dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="631b8-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="631b8-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="631b8-159">Next steps</span></span>
<span data-ttu-id="631b8-160">Dans ce didacticiel, vous avez utilisé un travail tooschedule un appareil de tooa méthode directe et la mise à jour de hello des propriétés du double hello appareil.</span><span class="sxs-lookup"><span data-stu-id="631b8-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="631b8-161">toocontinue mise en route avec IoT Hub et les modèles de gestion des appareils tels qu’à distance sur la mise à jour de microprogramme hello air, consultez :</span><span class="sxs-lookup"><span data-stu-id="631b8-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="631b8-162">[Didacticiel : Comment toodo un microprogramme mettre à jour][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="631b8-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="631b8-163">toocontinue mise en route avec IoT Hub, consultez [prise en main d’Azure IoT bord][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="631b8-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
