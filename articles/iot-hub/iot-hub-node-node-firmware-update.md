---
title: "Mise à jour d’un microprogramme d’appareil avec Azure IoT Hub (Node) | Microsoft Docs"
description: "Guide d’utilisation de la gestion des appareils sur Azure IoT Hub pour lancer une mise à jour du microprogramme d’un appareil. Vous utilisez les SDK Azure IoT pour Node.js afin d’implémenter une application d’appareil simulé et une application de service qui déclenche la mise à jour du microprogramme."
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
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="8c5cb-104">Utilisation de la gestion des appareils pour lancer une mise à jour du microprogramme d’un appareil (Node/Node)</span><span class="sxs-lookup"><span data-stu-id="8c5cb-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="8c5cb-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="8c5cb-105">Introduction</span></span>
<span data-ttu-id="8c5cb-106">Dans le didacticiel [Prise en main de la gestion d’appareils][lnk-dm-getstarted], vous avez vu comment utiliser les primitives de [représentation d’appareil physique][lnk-devtwin] et de [méthodes directives][lnk-c2dmethod] pour redémarrer à distance un appareil.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="8c5cb-107">Ce didacticiel utilise les mêmes primitives IoT Hub, fournit des conseils, et montre comment effectuer une mise à jour du microprogramme simulée de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="8c5cb-108">Ce modèle est utilisé dans l’implémentation de la mise à jour du microprogramme de l’exemple d’appareil Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="8c5cb-109">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="8c5cb-110">Créez une application console Node.js qui appelle une méthode directe firmwareUpdate sur l’application d’appareil simulé via votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="8c5cb-111">Créez une application d’appareil simulé qui implémente une méthode directe **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="8c5cb-112">Cette méthode lance un processus en plusieurs étapes qui attend de télécharger l’image du microprogramme, la télécharge et enfin, l’applique.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="8c5cb-113">À chaque étape du processus de mise à jour, l’appareil utilise les propriétés signalées pour mettre à jour la progression.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="8c5cb-114">À la fin de ce didacticiel, vous disposerez de deux applications console Node.js :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="8c5cb-115">**dmpatterns_fwupdate_service.js**, qui appelle une méthode directe sur l’application d’appareil simulé, affiche la réponse, et affiche périodiquement (toutes les 500 ms) les propriétés signalées mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="8c5cb-116">**dmpatterns_fwupdate_device.js**, qui se connecte à votre IoT Hub avec l’identité d’appareil créée précédemment, reçoit une méthode directe firmwareUpdate, s’exécute pour simuler une mise à jour du microprogramme dans un processus à plusieurs états, consistant à attendre avant de télécharger l’image, à télécharger celle-ci, puis finalement à l’appliquer.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="8c5cb-117">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8c5cb-118">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="8c5cb-119">L’article [Préparer votre environnement de développement][lnk-dev-setup] décrit l’installation de Node.js pour ce didacticiel sur Windows ou sur Linux.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8c5cb-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-120">An active Azure account.</span></span> <span data-ttu-id="8c5cb-121">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="8c5cb-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="8c5cb-122">Pour créer votre IoT Hub et obtenir votre chaîne de connexion, procédez de la manière décrite dans [Prise en main de la gestion d’appareils](iot-hub-node-node-device-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8c5cb-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="8c5cb-123">Déclencher une mise à jour du microprogramme à distance sur l’appareil à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="8c5cb-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="8c5cb-124">Dans cette section, vous créez une application console Node.js qui lance une mise à jour de microprogramme à distance sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="8c5cb-125">L’application utilise une méthode directe pour lancer la mise à jour et des requêtes de jumeau d’appareil pour obtenir régulièrement l’état de la mise à jour du microprogramme actif.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="8c5cb-126">Créez un dossier vide nommé **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="8c5cb-127">Dans le dossier **triggerfwupdateondevice**, créez un fichier package.json à l’aide de la commande ci-dessous, à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="8c5cb-128">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="8c5cb-129">À l’invite de commandes, dans le dossier **triggerfwupdateondevice**, exécutez la commande suivante pour installer les packages de kit de développement logiciel (SDK) pour appareils **azure-iothub** et **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="8c5cb-130">À l’aide d’un éditeur de texte, créez un fichier **dmpatterns_getstarted_service.js** dans le dossier **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="8c5cb-131">Ajoutez les instructions ’require’ suivantes au début du fichier **dmpatterns_getstarted_service.js** :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="8c5cb-132">Ajoutez les déclarations de variable suivantes et remplacez les valeurs d’espace réservé :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="8c5cb-133">Ajoutez la fonction suivante pour rechercher et afficher la valeur de la propriété signalée firmwareUpdate.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="8c5cb-134">Ajoutez la fonction suivante pour appeler la méthode firmwareUpdate afin de redémarrer l’appareil cible :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
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
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="8c5cb-135">Enfin, ajoutez la fonction suivante au code pour démarrer la séquence de mise à jour du microprogramme et commencer périodiquement à afficher les propriétés signalées :</span><span class="sxs-lookup"><span data-stu-id="8c5cb-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="8c5cb-136">Enregistrez et fermez le fichier **dmpatterns_fwupdate_service.js**.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="8c5cb-137">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="8c5cb-137">Run the apps</span></span>
<span data-ttu-id="8c5cb-138">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="8c5cb-139">À l’invite de commandes, dans le dossier **manageddevice**, exécutez la commande suivante pour commencer à écouter la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="8c5cb-140">À l’invite de commandes, dans le dossier **triggerfwupdateondevice**, exécutez la commande suivante pour déclencher le redémarrage à distance et interroger la représentation d’appareil pour déterminer le moment du dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="8c5cb-141">La réponse de l’appareil à la méthode directe s’affiche dans la console.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c5cb-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c5cb-142">Next steps</span></span>
<span data-ttu-id="8c5cb-143">Dans ce didacticiel, vous avez utilisé une méthode directe pour déclencher une mise à jour du microprogramme à distance sur un appareil, et utilisé les propriétés signalées pour suivre la progression de la mise à jour du microprogramme.</span><span class="sxs-lookup"><span data-stu-id="8c5cb-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="8c5cb-144">Pour savoir comment étendre votre solution IoT et planifier des appels de méthode sur plusieurs appareils, voir le didacticiel [Planifier et diffuser des travaux][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="8c5cb-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
