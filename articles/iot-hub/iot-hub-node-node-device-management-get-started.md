---
title: "aaaGet a démarré avec la gestion des appareils Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment toouse tooinitiate de gestion des appareils IoT Hub un périphérique distant du redémarrage. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et une application de service qui appelle la méthode directe hello."
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
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="04657-104">Prise en main de la gestion d’appareils (Node)</span><span class="sxs-lookup"><span data-stu-id="04657-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="04657-105">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="04657-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="04657-106">Utilisez hello toocreate portail Azure un IoT Hub et créer une identité d’appareil dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="04657-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="04657-107">Créer une application d’appareil simulé disposant d’une méthode directe permettant le redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="04657-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="04657-108">Méthodes directes sont appelés à partir du cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="04657-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="04657-109">Créer une application de console Node.js qui appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello via votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="04657-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="04657-110">À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="04657-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="04657-111">**dmpatterns_getstarted_device.js**, qui connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment, reçoit une méthode directe de redémarrage, simule un redémarrage physique et indique le temps de hello pour le dernier redémarrage de hello.</span><span class="sxs-lookup"><span data-stu-id="04657-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="04657-112">**dmpatterns_getstarted_service.js**, qui appelle une méthode directe dans l’application d’appareil simulé hello, affiche les réponse hello et hello affiche mis à jour a signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="04657-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="04657-113">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="04657-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="04657-114">Node.js version 0.12.x ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="04657-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="04657-115">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Node.js pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="04657-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="04657-116">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="04657-116">An active Azure account.</span></span> <span data-ttu-id="04657-117">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="04657-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="04657-118">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="04657-118">Create a simulated device app</span></span>
<span data-ttu-id="04657-119">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="04657-119">In this section, you will</span></span>

* <span data-ttu-id="04657-120">Créer une application de console Node.js qui répond tooa de méthode directe appelé par le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="04657-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="04657-121">Déclencher un redémarrage d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="04657-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="04657-122">Hello d’utilisation signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils dernier redémarrage</span><span class="sxs-lookup"><span data-stu-id="04657-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="04657-123">Créez un dossier vide nommé **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="04657-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="04657-124">Bonjour **manageddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="04657-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="04657-125">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="04657-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="04657-126">Votre invite de commandes Bonjour **manageddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :</span><span class="sxs-lookup"><span data-stu-id="04657-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="04657-127">À l’aide d’un éditeur de texte, créez un **dmpatterns_getstarted_device.js** fichier Bonjour **manageddevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="04657-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="04657-128">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_device.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="04657-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="04657-129">Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="04657-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="04657-130">Remplacez la chaîne de connexion hello avec la chaîne de connexion de votre périphérique.</span><span class="sxs-lookup"><span data-stu-id="04657-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="04657-131">Ajouter hello suivant de méthode directe de fonction tooimplement hello de périphérique de hello</span><span class="sxs-lookup"><span data-stu-id="04657-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
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
7. <span data-ttu-id="04657-132">Ouvrez tooyour IoT hub hello connexion et démarrer l’écouteur de méthode directe hello :</span><span class="sxs-lookup"><span data-stu-id="04657-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="04657-133">Enregistrez et fermez hello **dmpatterns_getstarted_device.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="04657-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="04657-134">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="04657-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="04657-135">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="04657-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="04657-136">Déclencher un arrêt à distance sur l’appareil hello à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="04657-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="04657-137">Dans cette section, vous créez une application console Node.js qui lance un redémarrage à distance sur un appareil avec une méthode directe.</span><span class="sxs-lookup"><span data-stu-id="04657-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="04657-138">application Hello utilise hello de toodiscover requêtes appareil double dernier redémarrage de cet appareil.</span><span class="sxs-lookup"><span data-stu-id="04657-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="04657-139">Créez un dossier vide nommé **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="04657-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="04657-140">Bonjour **triggerrebootondevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="04657-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="04657-141">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="04657-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="04657-142">Votre invite de commandes Bonjour **triggerrebootondevice** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package SDK de l’appareil et **azure-iot-périphérique-mqtt** package :</span><span class="sxs-lookup"><span data-stu-id="04657-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="04657-143">À l’aide d’un éditeur de texte, créez un **dmpatterns_getstarted_service.js** fichier Bonjour **triggerrebootondevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="04657-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="04657-144">Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_getstarted_service.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="04657-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="04657-145">Ajouter hello après les déclarations de variable et remplacez les valeurs d’espace réservé hello :</span><span class="sxs-lookup"><span data-stu-id="04657-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="04657-146">Ajoutez hello suivant fonction tooinvoke hello méthode tooreboot hello cible un périphérique :</span><span class="sxs-lookup"><span data-stu-id="04657-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="04657-147">Ajouter suivant de hello la fonction tooquery pour appareil de hello et obtenir hello dernière heure de redémarrage :</span><span class="sxs-lookup"><span data-stu-id="04657-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="04657-148">Ajoutez hello suivant code toocall hello fonctions qui déclenchent hello redémarrer méthode directe et de requête pour hello redémarrer dernière heure :</span><span class="sxs-lookup"><span data-stu-id="04657-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="04657-149">Enregistrez et fermez hello **dmpatterns_getstarted_service.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="04657-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="04657-150">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="04657-150">Run hello apps</span></span>
<span data-ttu-id="04657-151">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="04657-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="04657-152">Invite de commandes hello Bonjour **manageddevice** dossier, exécutez hello suivant toobegin de commande à l’écoute de méthode directe de redémarrage hello.</span><span class="sxs-lookup"><span data-stu-id="04657-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="04657-153">Invite de commandes hello Bonjour **triggerrebootondevice** dossier, exécutez hello suivant à distance de commande tootrigger hello redémarrer et pour Bonjour appareil double toofind Bonjour redémarrez dernière heure de la requête.</span><span class="sxs-lookup"><span data-stu-id="04657-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="04657-154">Vous consultez hello appareil réponse toohello méthode directe dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="04657-154">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
