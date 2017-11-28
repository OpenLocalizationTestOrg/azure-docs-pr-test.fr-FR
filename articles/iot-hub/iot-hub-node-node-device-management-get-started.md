---
title: "Bien démarrer avec la gestion des appareils Azure IoT Hub (Node) | Microsoft Docs"
description: "Découvrez comment utiliser la gestion des appareils IoT Hub pour lancer un redémarrage d’appareil à distance. Vous utilisez le SDK Azure IoT pour Node.js afin d’implémenter une application d’appareil simulé qui inclut une méthode directe et une application de service qui appelle la méthode directe."
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
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="2281c-104">Prise en main de la gestion d’appareils (Node)</span><span class="sxs-lookup"><span data-stu-id="2281c-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="2281c-105">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="2281c-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2281c-106">Utiliser le portail Azure pour créer un IoT Hub et une identité d’appareil dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2281c-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="2281c-107">Créer une application d’appareil simulé disposant d’une méthode directe permettant le redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="2281c-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="2281c-108">Les méthodes directes sont appelées à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="2281c-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="2281c-109">Créer une application console Node.js qui appelle une méthode directe de redémarrage sur l’application d’appareil simulé via votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2281c-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="2281c-110">À la fin de ce didacticiel, vous disposerez de deux applications console Node.js :</span><span class="sxs-lookup"><span data-stu-id="2281c-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="2281c-111">**dmpatterns_getstarted_device.js**, qui se connecte à votre IoT Hub avec l’identité d’appareil créée précédemment, reçoit une méthode directe de redémarrage, simule un redémarrage physique et indique l’heure du dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="2281c-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="2281c-112">**dmpatterns_getstarted_service.js**, qui appelle une méthode directe sur l’application de l’appareil simulé, affiche la réponse et affiche les propriétés signalées pour la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="2281c-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="2281c-113">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2281c-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2281c-114">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2281c-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="2281c-115">L’article [Préparer votre environnement de développement][lnk-dev-setup] décrit l’installation de Node.js pour ce didacticiel sur Windows ou sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2281c-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="2281c-116">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="2281c-116">An active Azure account.</span></span> <span data-ttu-id="2281c-117">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="2281c-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2281c-118">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="2281c-118">Create a simulated device app</span></span>
<span data-ttu-id="2281c-119">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="2281c-119">In this section, you will</span></span>

* <span data-ttu-id="2281c-120">Créer une application console Node.js qui répond à une méthode directe appelée par le cloud</span><span class="sxs-lookup"><span data-stu-id="2281c-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="2281c-121">Déclencher un redémarrage d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="2281c-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="2281c-122">Utiliser les propriétés signalées pour activer les requêtes sur le jumeau d’appareil afin d’identifier les appareils et l’heure de leur dernier redémarrage</span><span class="sxs-lookup"><span data-stu-id="2281c-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="2281c-123">Créez un dossier vide nommé **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2281c-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="2281c-124">Dans le dossier **simulateddevice**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="2281c-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="2281c-125">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="2281c-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2281c-126">À l’invite de commandes, dans le dossier **manageddevice**, exécutez la commande suivante pour installer le package du kit Device SDK **azure-iot-device** et le package **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="2281c-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2281c-127">À l’aide d’un éditeur de texte, créez un fichier **dmpatterns_getstarted_device.js** dans le dossier **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="2281c-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="2281c-128">Ajoutez les instructions 'require' suivantes au début du fichier **dmpatterns_getstarted_device.js** :</span><span class="sxs-lookup"><span data-stu-id="2281c-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="2281c-129">Ajoutez une variable **connectionString** et utilisez-la pour créer une instance de **Client**.</span><span class="sxs-lookup"><span data-stu-id="2281c-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="2281c-130">Remplacez la chaîne de connexion par la chaîne de connexion de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="2281c-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="2281c-131">Ajoutez la fonction suivante pour implémenter la méthode directe sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="2281c-131">Add the following function to implement the direct method on the device</span></span>
   
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
7. <span data-ttu-id="2281c-132">Ouvrez la connexion à votre hub IoT et démarrez l’écouteur de la méthode directe :</span><span class="sxs-lookup"><span data-stu-id="2281c-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="2281c-133">Enregistrez et fermez le fichier **dmpatterns_getstarted_device.js**.</span><span class="sxs-lookup"><span data-stu-id="2281c-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="2281c-134">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="2281c-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2281c-135">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="2281c-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="2281c-136">Déclencher un redémarrage à distance sur l’appareil à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="2281c-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="2281c-137">Dans cette section, vous créez une application console Node.js qui lance un redémarrage à distance sur un appareil avec une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="2281c-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="2281c-138">L’application utilise des requêtes du jumeau d’appareil pour déterminer l’heure du dernier redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="2281c-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="2281c-139">Créez un dossier vide nommé **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="2281c-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="2281c-140">Dans le dossier **triggerrebootondevice**, créez un fichier package.json en utilisant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="2281c-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="2281c-141">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="2281c-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2281c-142">À l’invite de commandes, dans le dossier **triggerrebootondevice**, exécutez la commande suivante pour installer le package du kit Device SDK **azure-iothub** et le package **azure-iot-device-mqtt** :</span><span class="sxs-lookup"><span data-stu-id="2281c-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2281c-143">À l’aide d’un éditeur de texte, créez un fichier **dmpatterns_getstarted_service.js** dans le dossier **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="2281c-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="2281c-144">Ajoutez les instructions ’require’ suivantes au début du fichier **dmpatterns_getstarted_service.js** :</span><span class="sxs-lookup"><span data-stu-id="2281c-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="2281c-145">Ajoutez les déclarations de variable suivantes et remplacez les valeurs d’espace réservé :</span><span class="sxs-lookup"><span data-stu-id="2281c-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="2281c-146">Ajoutez la fonction suivante pour appeler la méthode device afin de redémarrer l’appareil cible :</span><span class="sxs-lookup"><span data-stu-id="2281c-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="2281c-147">Ajoutez la fonction suivante pour interroger l’appareil et obtenir l’heure du dernier redémarrage :</span><span class="sxs-lookup"><span data-stu-id="2281c-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="2281c-148">Ajoutez le code suivant pour appeler les fonctions qui déclenchent la méthode directe de redémarrage et la requête sur le dernier redémarrage :</span><span class="sxs-lookup"><span data-stu-id="2281c-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="2281c-149">Enregistrez et fermez le fichier **dmpatterns_getstarted_service.js**.</span><span class="sxs-lookup"><span data-stu-id="2281c-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="2281c-150">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="2281c-150">Run the apps</span></span>
<span data-ttu-id="2281c-151">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="2281c-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="2281c-152">À l’invite de commandes, dans le dossier **manageddevice**, exécutez la commande suivante pour commencer à écouter la méthode directe de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="2281c-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="2281c-153">À l’invite de commandes, dans le dossier **triggerrebootondevice**, exécutez la commande suivante pour déclencher le redémarrage à distance et interroger le jumeau d’appareil pour déterminer l’heure du dernier redémarrage.</span><span class="sxs-lookup"><span data-stu-id="2281c-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="2281c-154">La réponse de l’appareil à la méthode directe s’affiche dans la console.</span><span class="sxs-lookup"><span data-stu-id="2281c-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
