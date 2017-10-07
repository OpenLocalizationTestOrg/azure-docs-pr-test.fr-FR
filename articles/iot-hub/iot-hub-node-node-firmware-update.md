---
title: "mise à jour de microprogramme aaaDevice avec Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment mettre à jour toouse la gestion des appareils sur Azure IoT Hub tooinitiate un microprogramme de l’appareil. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé et une application de service qui déclenche la mise à jour du microprogramme hello."
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
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="c5551-104">Utiliser la gestion de périphérique tooinitiate une mise à jour du microprogramme de périphérique (nœud)</span><span class="sxs-lookup"><span data-stu-id="c5551-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="c5551-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="c5551-105">Introduction</span></span>
<span data-ttu-id="c5551-106">Bonjour [prise en main la gestion des appareils] [ lnk-dm-getstarted] didacticiel, vous avez vu comment toouse hello [double de l’appareil] [ lnk-devtwin] et [directe méthodes] [ lnk-c2dmethod] tooremotely de primitives redémarrer un appareil.</span><span class="sxs-lookup"><span data-stu-id="c5551-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="c5551-107">Ce didacticiel utilise hello mêmes primitives IoT Hub et fournit des conseils et vous montre comment toodo un bout en bout simulée mise à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="c5551-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="c5551-108">Ce modèle est utilisé dans l’implémentation de mise à jour du microprogramme hello pour exemple de périphérique Intel Edison hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="c5551-109">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="c5551-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="c5551-110">Créer une application de console Node.js qui appelle la méthode directe de hello firmwareUpdate dans l’application d’appareil simulé hello via votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5551-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="c5551-111">Créez un appareil simulé qui implémente une méthode directe **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="c5551-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="c5551-112">Cette méthode lance un processus en plusieurs étapes qui attend l’image de microprogramme toodownload hello, télécharge l’image de microprogramme hello et enfin applique image de microprogramme hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="c5551-113">Lors de chaque étape de mise à jour hello, hello périphérique utilise hello signalée tooreport de propriétés sur la progression.</span><span class="sxs-lookup"><span data-stu-id="c5551-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="c5551-114">À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="c5551-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="c5551-115">**dmpatterns_fwupdate_service.js**, qui appelle une méthode directe dans l’application d’appareil simulé hello, réponse de hello s’affiche et périodiquement (chaque 500 ms) hello affiche mis à jour signalés propriétés.</span><span class="sxs-lookup"><span data-stu-id="c5551-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="c5551-116">**dmpatterns_fwupdate_device.js**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe firmwareUpdate, s’exécute via un toosimulate plusieurs États de processus pour une mise à jour de microprogramme, y compris : en attente de hello image de téléchargement, télécharger la nouvelle image de hello et enfin application de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="c5551-117">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c5551-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c5551-118">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c5551-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="c5551-119">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c5551-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c5551-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c5551-120">An active Azure account.</span></span> <span data-ttu-id="c5551-121">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="c5551-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="c5551-122">Suivez hello [prise en main la gestion des appareils](iot-hub-node-node-device-management-get-started.md) article toocreate votre IoT hub et obtenir votre chaîne de connexion de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c5551-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="c5551-123">Déclencher une mise à jour de microprogramme à distance sur l’appareil hello à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="c5551-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="c5551-124">Dans cette section, vous créez une application console Node.js qui lance une mise à jour de microprogramme à distance sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="c5551-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="c5551-125">application Hello utilise une mise à jour de méthode directe tooinitiate hello et utilise appareil double requêtes tooperiodically obtenir l’état de hello de mise à jour du microprogramme active hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="c5551-126">Créez un dossier vide nommé **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="c5551-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="c5551-127">Bonjour **triggerfwupdateondevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="c5551-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="c5551-128">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="c5551-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c5551-129">Votre invite de commandes Bonjour **triggerfwupdateondevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-concentrateur** et **azure-iot-périphérique-mqtt** périphérique Packages du Kit de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="c5551-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="c5551-130">À l’aide d’un éditeur de texte, créez un **dmpatterns_getstarted_service.js** fichier Bonjour **triggerfwupdateondevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="c5551-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="c5551-131">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_service.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="c5551-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="c5551-132">Ajouter hello après les déclarations de variable et remplacez les valeurs d’espace réservé hello :</span><span class="sxs-lookup"><span data-stu-id="c5551-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="c5551-133">Ajouter suivant de hello fonction toofind et affiche la valeur hello hello firmwareUpdate a signalé de propriété.</span><span class="sxs-lookup"><span data-stu-id="c5551-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="c5551-134">Ajoutez hello suivant fonction tooinvoke hello firmwareUpdate méthode tooreboot hello équipement :</span><span class="sxs-lookup"><span data-stu-id="c5551-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="c5551-135">Enfin, suivant de hello Ajouter fonction de séquence de mise à jour du microprogramme toocode toostart hello et démarrer régulièrement montrant hello signalé propriétés :</span><span class="sxs-lookup"><span data-stu-id="c5551-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="c5551-136">Enregistrez et fermez hello **dmpatterns_fwupdate_service.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="c5551-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="c5551-137">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="c5551-137">Run hello apps</span></span>
<span data-ttu-id="c5551-138">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="c5551-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="c5551-139">Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="c5551-140">Invite de commandes hello Bonjour **triggerfwupdateondevice** dossier, exécutez hello suivant à distance de commande tootrigger hello redémarrer et pour Bonjour appareil double toofind Bonjour redémarrez dernière heure de la requête.</span><span class="sxs-lookup"><span data-stu-id="c5551-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="c5551-141">Vous consultez hello appareil réponse toohello méthode directe dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5551-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5551-142">Next steps</span></span>
<span data-ttu-id="c5551-143">Dans ce didacticiel, vous avez utilisé un tootrigger méthode directe à une distance mise à jour de microprogramme sur un appareil et un hello utilisé signalé progression de hello toofollow propriétés de mise à jour du microprogramme hello.</span><span class="sxs-lookup"><span data-stu-id="c5551-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="c5551-144">toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c5551-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
