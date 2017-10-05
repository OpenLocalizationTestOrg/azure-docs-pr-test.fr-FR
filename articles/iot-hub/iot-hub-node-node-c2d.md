---
title: "Messages cloud-à-appareil avec Azure IoT Hub (Node) | Microsoft Docs"
description: "Envoi de messages cloud-à-appareil vers un appareil depuis un Azure IoT Hub à l’aide des kits de développement logiciel Azure IoT pour Node.js. Vous modifiez une application d’appareil simulé pour recevoir des messages cloud-à-appareil et modifiez une application principale pour envoyer des messages cloud-à-appareil."
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
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="1ecdf-104">Envoi de messages cloud à appareil avec IoT Hub (Node)</span><span class="sxs-lookup"><span data-stu-id="1ecdf-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="1ecdf-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="1ecdf-105">Introduction</span></span>
<span data-ttu-id="1ecdf-106">Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="1ecdf-107">Le didacticiel [Prise en main d’IoT Hub] explique comment créer un concentrateur IoT, l’utiliser pour configurer une identité d’appareil et coder une simulation d’application d’appareil qui envoie des messages d’appareils à cloud.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="1ecdf-108">Ce didacticiel s’appuie sur l’article [Prise en main d’IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="1ecdf-109">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-109">It shows you how to:</span></span>

* <span data-ttu-id="1ecdf-110">À partir du serveur principal de votre application, envoyez des messages cloud-à-appareil vers un appareil unique via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="1ecdf-111">Recevez des messages cloud-à-appareil sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="1ecdf-112">À partir du serveur principal de votre application, demandez l’accusé de réception (*commentaires*) pour les messages envoyés à un appareil depuis IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="1ecdf-113">Vous trouverez des informations supplémentaires sur les messages du cloud vers les appareils dans le [Guide du développeur d’IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="1ecdf-114">À la fin de ce didacticiel, vous exécuterez deux applications de console Node.js :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="1ecdf-115">**SimulatedDevice**, une version modifiée de l’application créée dans [Prise en main d’IoT Hub]qui se connecte à votre hub IoT et reçoit les messages entre cloud et appareils.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="1ecdf-116">**SendCloudToDeviceMessage**, qui envoie un message cloud-à-appareil à l’application pour appareil simulée par le biais d’IoT Hub, puis reçoit son accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="1ecdf-117">IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="1ecdf-118">Pour obtenir des instructions détaillées sur la façon de connecter votre appareil au code de ce didacticiel, et à Azure IoT Hub de manière générale, consultez le [Centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="1ecdf-119">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1ecdf-120">Node.js version 0.10.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="1ecdf-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-121">An active Azure account.</span></span> <span data-ttu-id="1ecdf-122">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="1ecdf-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="1ecdf-123">Recevoir des messages dans l’application d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="1ecdf-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="1ecdf-124">Dans cette section, vous modifiez l’application pour appareil simulée que vous avez créée dans [Prise en main d’IoT Hub] pour recevoir des messages cloud-à-appareil à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="1ecdf-125">À l’aide d’un éditeur de texte, ouvrez le fichier SimulatedDevice.js.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="1ecdf-126">Modifiez la fonction **connectCallback** pour gérer les messages envoyés à partir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="1ecdf-127">Dans cet exemple, l’appareil appelle toujours la fonction **complete** afin de notifier IoT Hub qu’il a traité le message.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="1ecdf-128">La nouvelle version de la fonction **connectCallback** ressemble à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
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
        // Create a message and send it to the IoT Hub every second
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
   > <span data-ttu-id="1ecdf-129">Si vous utilisez HTTP au lieu de MQTT ou d’AMQP comme moyen de transport, l’instance **DeviceClient** vérifie les messages à partir d’IoT Hub peu fréquemment (moins de toutes les 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="1ecdf-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="1ecdf-130">Pour plus d’informations sur les différences entre la prise en charge de MQTT, d’AMQP et de HTTP et la limitation d’IoT Hub, voir le [Guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="1ecdf-131">Envoi d’un message cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="1ecdf-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="1ecdf-132">Dans cette section, vous allez créer une application de console Node.js qui envoie des messages cloud-à-appareil à l’application de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="1ecdf-133">Vous avez besoin de l’ID de l’appareil que vous avez ajouté dans le didacticiel [Prise en main d’IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="1ecdf-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="1ecdf-134">Vous avez également besoin de la chaîne de connexion pour votre hub que vous trouverez dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="1ecdf-135">Créez un dossier vide appelé **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="1ecdf-136">Dans le dossier **sendcloudtodevicemessage** , créez un fichier package.json à l’aide de la commande ci-dessous, à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="1ecdf-137">Acceptez toutes les valeurs par défaut :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="1ecdf-138">À l’invite de commandes, dans le dossier **sendcloudtodevicemessage**, exécutez la commande suivante pour installer le package **azure-iothub** :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="1ecdf-139">À l’aide d’un éditeur de texte, créez un fichier **SendCloudToDeviceMessage.js** dans le dossier **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="1ecdf-140">Ajoutez les instructions `require` ci-dessous au début du fichier **SendCloudToDeviceMessage.js** :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="1ecdf-141">Ajoutez le code suivant au fichier **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="1ecdf-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="1ecdf-142">Remplacez la valeur d’espace réservé « {iot hub connection string} » par la chaîne de connexion pour le IoT Hub créé dans le didacticiel [Prise en main d’IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="1ecdf-143">Remplacez l’espace réservé « {device id} » par l’ID de l’appareil ajouté dans le didacticiel [Prise en main d’IoT Hub] :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="1ecdf-144">Ajoutez la fonction suivante pour imprimer les résultats de l’opération sur la console :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="1ecdf-145">Ajoutez la fonction suivante pour imprimer les messages d’accusé de réception sur la console :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="1ecdf-146">Ajoutez le code suivant pour envoyer un message à votre appareil et gérer le message de commentaires lorsque l’appareil accuse réception d’un message cloud-à-appareil :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="1ecdf-147">Enregistrez et fermez le fichier **SendCloudToDeviceMessage.js** .</span><span class="sxs-lookup"><span data-stu-id="1ecdf-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="1ecdf-148">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="1ecdf-148">Run the applications</span></span>
<span data-ttu-id="1ecdf-149">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="1ecdf-150">À l’invite de commandes du dossier **simulateddevice** , exécutez la commande suivante pour envoyer la télémétrie à IoT hub et écouter les messages cloud-à-appareil :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![Exécution de l’application de périphérique simulé][img-simulated-device]
2. <span data-ttu-id="1ecdf-152">À l’invite de commandes dans le dossier **sendcloudtodevicemessage**, exécutez la commande suivante pour envoyer un message cloud-à-appareil, puis attendez de recevoir l’accusé de réception :</span><span class="sxs-lookup"><span data-stu-id="1ecdf-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Exécutez l’application pour envoyer la commande cloud-à-appareil][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="1ecdf-154">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1ecdf-155">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Transient Fault Handling](Gestion des erreurs temporaires).</span><span class="sxs-lookup"><span data-stu-id="1ecdf-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="1ecdf-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ecdf-156">Next steps</span></span>
<span data-ttu-id="1ecdf-157">Dans ce didacticiel, vous avez appris à envoyer et recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="1ecdf-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="1ecdf-158">Pour voir des exemples de solutions de bout en bout qui utilisent IoT Hub, consultez [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="1ecdf-159">Pour en savoir plus sur le développement de solutions avec IoT Hub, consultez le [Guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="1ecdf-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="1ecdf-160">[Prise en main d’IoT Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="1ecdf-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="1ecdf-161">[Guide du développeur IoT Hub]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="1ecdf-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="1ecdf-162">[Centre de développement Azure IoT]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="1ecdf-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="1ecdf-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="1ecdf-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="1ecdf-164">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="1ecdf-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="1ecdf-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="1ecdf-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
