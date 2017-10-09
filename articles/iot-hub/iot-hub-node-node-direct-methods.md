---
title: "aaaAzure IoT Hub direct de méthodes (nœud) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez hello Azure IoT SDK pour Node.js tooimplement une application d’appareil simulé qui inclut une méthode directe et une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="f09ec-104">Utilisation de méthodes directes sur votre appareil IoT avec Node.js</span><span class="sxs-lookup"><span data-stu-id="f09ec-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="f09ec-105">À la fin de hello de ce didacticiel, vous avez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="f09ec-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="f09ec-106">**CallMethodOnDevice.js**, qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="f09ec-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="f09ec-107">**SimulatedDevice.js**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et répond méthode toohello appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f09ec-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="f09ec-108">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="f09ec-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="f09ec-109">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f09ec-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f09ec-110">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f09ec-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="f09ec-111">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="f09ec-111">An active Azure account.</span></span> <span data-ttu-id="f09ec-112">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="f09ec-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f09ec-113">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="f09ec-113">Create a simulated device app</span></span>
<span data-ttu-id="f09ec-114">Dans cette section, vous créez une application console Node.js qui répond méthode tooa appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f09ec-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="f09ec-115">Créez un dossier vide appelé **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="f09ec-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="f09ec-116">Bonjour **simulateddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="f09ec-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f09ec-117">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f09ec-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f09ec-118">Votre invite de commandes Bonjour **simulateddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** package SDK de l’appareil et **azure-iot-périphérique-mqtt**package :</span><span class="sxs-lookup"><span data-stu-id="f09ec-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="f09ec-119">À l’aide d’un éditeur de texte, créez un nouveau **SimulatedDevice.js** fichier Bonjour **simulateddevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="f09ec-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="f09ec-120">Ajoutez hello suivant `require` instructions au hello démarrent Hello **SimulatedDevice.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="f09ec-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="f09ec-121">Ajouter un **connectionString** variable et l’utiliser toocreate un **DeviceClient** instance.</span><span class="sxs-lookup"><span data-stu-id="f09ec-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="f09ec-122">Remplacez **{chaîne de connexion de périphérique}** avec chaîne de connexion de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="f09ec-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="f09ec-123">Ajoutez hello suivant fonction tooimplement hello (méthode) sur l’appareil de hello :</span><span class="sxs-lookup"><span data-stu-id="f09ec-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="f09ec-124">Ouvrez tooyour IoT hub hello connexion et démarrer l’écouteur de méthode initialize hello :</span><span class="sxs-lookup"><span data-stu-id="f09ec-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="f09ec-125">Enregistrez et fermez hello **SimulatedDevice.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="f09ec-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="f09ec-126">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="f09ec-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f09ec-127">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, les tentatives de connexion), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="f09ec-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="f09ec-128">Appeler une méthode sur un appareil</span><span class="sxs-lookup"><span data-stu-id="f09ec-128">Call a method on a device</span></span>
<span data-ttu-id="f09ec-129">Dans cette section, vous créez une application de console Node.js qui appelle une méthode dans l’application d’appareil simulé hello et affiche ensuite la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="f09ec-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="f09ec-130">Créez un dossier vide nommé **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="f09ec-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="f09ec-131">Bonjour **callmethodondevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="f09ec-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="f09ec-132">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f09ec-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="f09ec-133">Votre invite de commandes Bonjour **callmethodondevice** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :</span><span class="sxs-lookup"><span data-stu-id="f09ec-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="f09ec-134">À l’aide d’un éditeur de texte, créez un **CallMethodOnDevice.js** fichier Bonjour **callmethodondevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="f09ec-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="f09ec-135">Ajoutez hello suivant `require` instructions au hello démarrent Hello **CallMethodOnDevice.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="f09ec-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="f09ec-136">Ajouter hello après la déclaration de variable et remplacer la valeur d’espace réservé de hello par hello chaîne de connexion de IoT Hub pour votre concentrateur :</span><span class="sxs-lookup"><span data-stu-id="f09ec-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="f09ec-137">Créez hello client tooopen hello connexion tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f09ec-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="f09ec-138">Ajoutez hello suivant fonction tooinvoke hello (méthode) et impression hello appareil réponse toohello console de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="f09ec-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="f09ec-139">Enregistrez et fermez hello **CallMethodOnDevice.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="f09ec-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="f09ec-140">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="f09ec-140">Run hello apps</span></span>
<span data-ttu-id="f09ec-141">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="f09ec-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="f09ec-142">À l’invite de commande Bonjour **simulateddevice** dossier, exécutez hello suivant toostart commande écoute les appels de méthode à partir de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="f09ec-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="f09ec-143">À l’invite de commande Bonjour **callmethodondevice** dossier, exécutez hello suivant toobegin commande analyse votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="f09ec-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="f09ec-144">Vous verrez l’appareil de hello réagir toohello méthode par l’impression de message de type hello et application hello appelée réponse de hello hello méthode affichage à partir de l’appareil de hello :</span><span class="sxs-lookup"><span data-stu-id="f09ec-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="f09ec-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f09ec-145">Next steps</span></span>
<span data-ttu-id="f09ec-146">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="f09ec-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="f09ec-147">Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="f09ec-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="f09ec-148">Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="f09ec-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="f09ec-149">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="f09ec-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="f09ec-150">[Prise en main d’IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="f09ec-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="f09ec-151">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f09ec-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f09ec-152">toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f09ec-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md
