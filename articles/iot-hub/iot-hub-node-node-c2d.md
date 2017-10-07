---
title: "messages aaaCloud sur l’appareil avec Azure IoT Hub (nœud) | Documents Microsoft"
description: "Comment toosend cloud-à-appareil messages appareil tooa à partir d’un hub IoT d’Azure à l’aide de kits de développement IoT hello Azure pour Node.js. Modifier une application appareil simulé tooreceive les messages cloud-à-appareil et de modifier une application de serveur principal toosend hello cloud-à-appareil les messages."
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="d9e76-104">Envoi de messages cloud à appareil avec IoT Hub (Node)</span><span class="sxs-lookup"><span data-stu-id="d9e76-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="d9e76-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="d9e76-105">Introduction</span></span>
<span data-ttu-id="d9e76-106">Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="d9e76-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="d9e76-107">Hello [prise en main IoT Hub] didacticiel montre comment toocreate un IoT hub, configurer une identité d’appareil qu’il contient et code d’une application d’appareil simulé qui envoie des messages de l’appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="d9e76-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="d9e76-108">Ce didacticiel s’appuie sur l’article [prise en main IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="d9e76-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="d9e76-109">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9e76-109">It shows you how to:</span></span>

* <span data-ttu-id="d9e76-110">À partir de votre solution back-end, envoyer des messages cloud-à-appareil tooa seule unité via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9e76-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="d9e76-111">Recevez des messages cloud-à-appareil sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="d9e76-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="d9e76-112">À partir de votre solution back-end demande l’accusé de réception (*commentaires*) pour tooa appareil les messages envoyés à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9e76-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="d9e76-113">Vous trouverez plus d’informations sur les messages cloud-à-appareil Bonjour [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d9e76-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="d9e76-114">À la fin de hello de ce didacticiel, vous exécutez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="d9e76-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="d9e76-115">**SimulatedDevice**, une version modifiée de l’application hello créée dans [prise en main IoT Hub], qui se connecte tooyour IoT hub et reçoit des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="d9e76-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="d9e76-116">**SendCloudToDeviceMessage**, qui envoie une application d’appareil simulé toohello cloud-à-appareil message via IoT Hub et reçoit ensuite son accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="d9e76-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="d9e76-117">IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d9e76-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="d9e76-118">Pour obtenir des instructions sur tooconnect du votre appareil toothis didacticiel code et généralement tooAzure IoT Hub, voir hello [centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="d9e76-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="d9e76-119">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="d9e76-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d9e76-120">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d9e76-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="d9e76-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d9e76-121">An active Azure account.</span></span> <span data-ttu-id="d9e76-122">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="d9e76-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="d9e76-123">Recevoir des messages dans une application d’appareil simulé hello</span><span class="sxs-lookup"><span data-stu-id="d9e76-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="d9e76-124">Dans cette section, vous modifiez l’application d’appareil simulé hello vous avez créé dans [prise en main IoT Hub] tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="d9e76-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="d9e76-125">À l’aide d’un éditeur de texte, d’ouvrir le fichier de SimulatedDevice.js hello.</span><span class="sxs-lookup"><span data-stu-id="d9e76-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="d9e76-126">Modifier hello **connectCallback** fonction toohandle les messages envoyés à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d9e76-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="d9e76-127">Dans cet exemple, les appareils hello appelant toujours hello **complète** toonotify IoT Hub qu’il a traité le message d’appel de fonction.</span><span class="sxs-lookup"><span data-stu-id="d9e76-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="d9e76-128">La nouvelle version de hello **connectCallback** fonction ressemble à hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="d9e76-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > <span data-ttu-id="d9e76-129">Si vous utilisez HTTP au lieu de MQTT ou AMQP comme couche de transport hello, hello **DeviceClient** instance vérifie les messages à partir du IoT Hub rarement (inférieur à 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="d9e76-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="d9e76-130">Pour plus d’informations sur les différences de hello entre la prise en charge MQTT, AMQP et HTTP et de limitation IoT Hub, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="d9e76-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="d9e76-131">Envoi d’un message cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="d9e76-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="d9e76-132">Dans cette section, vous créez une application console Node.js qui envoie des messages cloud-à-appareil toohello appareil simulé application.</span><span class="sxs-lookup"><span data-stu-id="d9e76-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="d9e76-133">Vous devez hello ID de périphérique périphérique hello vous avez ajouté dans hello [prise en main IoT Hub] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9e76-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="d9e76-134">Vous devez également hello chaîne de connexion IoT Hub pour votre concentrateur que vous pouvez trouver Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="d9e76-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="d9e76-135">Créez un dossier vide appelé **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="d9e76-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="d9e76-136">Bonjour **sendcloudtodevicemessage** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="d9e76-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="d9e76-137">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="d9e76-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="d9e76-138">Votre invite de commandes Bonjour **sendcloudtodevicemessage** dossier, exécutez hello suivant commande tooinstall hello **azure-iothub** package :</span><span class="sxs-lookup"><span data-stu-id="d9e76-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="d9e76-139">À l’aide d’un éditeur de texte, créez un **SendCloudToDeviceMessage.js** fichier Bonjour **sendcloudtodevicemessage** dossier.</span><span class="sxs-lookup"><span data-stu-id="d9e76-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="d9e76-140">Ajoutez hello suivant `require` instructions au hello démarrent Hello **SendCloudToDeviceMessage.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="d9e76-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="d9e76-141">Ajouter hello suivant code trop**SendCloudToDeviceMessage.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="d9e76-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="d9e76-142">Remplacer la valeur d’espace réservé hello « {iot hub chaîne de connexion} » avec hello chaîne de connexion de IoT Hub hub hello vous avez créé dans hello de [prise en main IoT Hub] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d9e76-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="d9e76-143">Remplacez espace réservé de hello « {id d’appareil} » avec l’ID de périphérique hello du périphérique hello vous avez ajouté dans hello [prise en main IoT Hub] didacticiel :</span><span class="sxs-lookup"><span data-stu-id="d9e76-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="d9e76-144">Ajoutez hello suivant fonction tooprint résultats toohello console Opérateur :</span><span class="sxs-lookup"><span data-stu-id="d9e76-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="d9e76-145">Ajoutez hello suivant console toohello de fonction tooprint remise commentaires messages :</span><span class="sxs-lookup"><span data-stu-id="d9e76-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="d9e76-146">Ajoutez suivante de hello toosend un dispositif de tooyour de messages de code et gérer le message de commentaires de hello lors de l’appareil de hello accuse réception de message de type hello cloud sur l’appareil :</span><span class="sxs-lookup"><span data-stu-id="d9e76-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="d9e76-147">Enregistrez et fermez le fichier **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="d9e76-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="d9e76-148">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="d9e76-148">Run hello applications</span></span>
<span data-ttu-id="d9e76-149">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="d9e76-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="d9e76-150">Invite de commandes hello Bonjour **simulateddevice** dossier, exécutez hello commande toosend télémétrie tooIoT Hub et toolisten pour les messages cloud-à-appareil :</span><span class="sxs-lookup"><span data-stu-id="d9e76-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Exécutez l’application d’appareil simulé hello][img-simulated-device]
2. <span data-ttu-id="d9e76-152">À l’invite de commande Bonjour **sendcloudtodevicemessage** dossier, exécutez hello suivant commande toosend un message cloud-à-appareil et attendez les commentaires d’accusé de réception hello :</span><span class="sxs-lookup"><span data-stu-id="d9e76-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Exécutez hello application toosend hello cloud-à-appareil commande][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="d9e76-154">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="d9e76-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d9e76-155">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="d9e76-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="d9e76-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9e76-156">Next steps</span></span>
<span data-ttu-id="d9e76-157">Dans ce didacticiel, vous avez appris comment toosend et recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="d9e76-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="d9e76-158">exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="d9e76-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="d9e76-159">toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="d9e76-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[prise en main IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[guide du développeur IoT Hub]: iot-hub-devguide.md
[centre de développement Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portail Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
