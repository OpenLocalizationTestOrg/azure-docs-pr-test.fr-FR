---
title: "Messages cloud-à-appareil avec Azure IoT Hub (.NET) | Microsoft Docs"
description: "Envoi de messages cloud-à-appareil vers un appareil depuis un Azure IoT Hub à l’aide des kits de développement logiciel Azure IoT pour .NET. Vous modifiez une application d’appareil pour recevoir des messages cloud-à-appareil et modifiez une application principale pour envoyer des messages cloud-à-appareil."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: 3f5f83671054c30afde3d7f18ff0edcdb8f78a01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a><span data-ttu-id="e4feb-104">Envoyer des messages du cloud à votre appareil avec IoT Hub (.NET)</span><span class="sxs-lookup"><span data-stu-id="e4feb-104">Send messages from the cloud to your device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="e4feb-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="e4feb-105">Introduction</span></span>
<span data-ttu-id="e4feb-106">Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="e4feb-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="e4feb-107">Le didacticiel [Prise en main d’Azure IoT Hub] explique comment créer un IoT Hub, l’utiliser pour configurer une identité d’appareil et coder une application d’appareil qui envoie des messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="e4feb-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="e4feb-108">Ce didacticiel s’appuie sur l’article [Prise en main d’Azure IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="e4feb-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="e4feb-109">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4feb-109">It shows you how to:</span></span>

* <span data-ttu-id="e4feb-110">À partir du serveur principal de votre application, envoyez des messages cloud-à-appareil vers un appareil unique via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e4feb-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="e4feb-111">Recevez des messages cloud-à-appareil sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="e4feb-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="e4feb-112">À partir du serveur principal de votre application, demandez l’accusé de réception (*commentaires*) pour les messages envoyés à un appareil depuis IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e4feb-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="e4feb-113">Vous trouverez des informations supplémentaires sur les messages du cloud vers les appareils dans le [Guide du développeur d’IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e4feb-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="e4feb-114">À la fin de ce didacticiel, vous exécutez deux applications console .NET :</span><span class="sxs-lookup"><span data-stu-id="e4feb-114">At the end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="e4feb-115">**SimulatedDevice**, une version modifiée de l’application créée dans [Prise en main d’Azure IoT Hub]qui se connecte à votre hub IoT et reçoit les messages entre cloud et appareils.</span><span class="sxs-lookup"><span data-stu-id="e4feb-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="e4feb-116">**SendCloudToDevice**, qui envoie un message cloud-à-appareil à l’application d’appareil par le biais d’IoT Hub, puis reçoit son accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="e4feb-116">**SendCloudToDevice**, which sends a cloud-to-device message to the device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="e4feb-117">IoT Hub offre la prise en charge de Kits de développement logiciel (SDK) pour plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des [Kits Azure IoT device SDK].</span><span class="sxs-lookup"><span data-stu-id="e4feb-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="e4feb-118">Pour obtenir des instructions détaillées sur la façon de connecter votre appareil au code de ce didacticiel et à Azure IoT Hub de manière générale, consultez le [Guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="e4feb-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="e4feb-119">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e4feb-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e4feb-120">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e4feb-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="e4feb-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="e4feb-121">An active Azure account.</span></span> <span data-ttu-id="e4feb-122">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="e4feb-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-device-app"></a><span data-ttu-id="e4feb-123">Recevoir des messages dans l’application d’appareil</span><span class="sxs-lookup"><span data-stu-id="e4feb-123">Receive messages in the device app</span></span>
<span data-ttu-id="e4feb-124">Dans cette section, vous allez modifier l’application d’appareil que créée dans [Prise en main d’Azure IoT Hub] pour recevoir des messages cloud-à-appareil à partir de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e4feb-124">In this section, you'll modify the device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="e4feb-125">Dans Visual Studio, dans le projet **SimulatedDevice**, ajoutez la méthode suivante à la classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-125">In Visual Studio, in the **SimulatedDevice** project, add the following method to the **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    <span data-ttu-id="e4feb-126">La méthode `ReceiveAsync` renvoie de façon asynchrone le message reçu au moment où l’appareil le reçoit.</span><span class="sxs-lookup"><span data-stu-id="e4feb-126">The `ReceiveAsync` method asynchronously returns the received message at the time that it is received by the device.</span></span> <span data-ttu-id="e4feb-127">Elle renvoie *null* après un délai d’attente pouvant être précisé (dans ce cas, la valeur par défaut est une minute).</span><span class="sxs-lookup"><span data-stu-id="e4feb-127">It returns *null* after a specifiable timeout period (in this case, the default of one minute is used).</span></span> <span data-ttu-id="e4feb-128">Lorsque l’application reçoit une valeur *null*, elle doit continuer à attendre de nouveaux messages.</span><span class="sxs-lookup"><span data-stu-id="e4feb-128">When the app receives a *null*, it should continue to wait for new messages.</span></span> <span data-ttu-id="e4feb-129">C’est pour répondre à cette exigence que la ligne `if (receivedMessage == null) continue` est insérée.</span><span class="sxs-lookup"><span data-stu-id="e4feb-129">This requirement is the reason for the `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="e4feb-130">L’appel à `CompleteAsync()` notifie IoT Hub que le message a été traité avec succès.</span><span class="sxs-lookup"><span data-stu-id="e4feb-130">The call to `CompleteAsync()` notifies IoT Hub that the message has been successfully processed.</span></span> <span data-ttu-id="e4feb-131">Le message peut être supprimé en toute sécurité de la file d’attente d’appareils.</span><span class="sxs-lookup"><span data-stu-id="e4feb-131">The message can be safely removed from the device queue.</span></span> <span data-ttu-id="e4feb-132">Si l’application de périphérique n’a pas été en mesure de terminer le traitement du message, IoT Hub le remet à nouveau.</span><span class="sxs-lookup"><span data-stu-id="e4feb-132">If something happened that prevented the device app from completing the processing of the message, IoT Hub delivers it again.</span></span> <span data-ttu-id="e4feb-133">Il est alors important que la logique de traitement du message de l’application d’appareil soit *idempotente*, afin qu’un message identique reçu plusieurs fois produise le même résultat.</span><span class="sxs-lookup"><span data-stu-id="e4feb-133">It is then important that message processing logic in the device app is *idempotent*, so that receiving the same message multiple times produces the same result.</span></span> <span data-ttu-id="e4feb-134">Une application peut également abandonner temporairement un message. IoT hub en conserve alors le message dans la file d’attente pour un traitement ultérieur.</span><span class="sxs-lookup"><span data-stu-id="e4feb-134">An application can also temporarily abandon a message, which results in IoT hub retaining the message in the queue for future consumption.</span></span> <span data-ttu-id="e4feb-135">Une application peut également rejeter un message, ce qui le supprime définitivement de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="e4feb-135">Or, the application can reject a message, which permanently removes the message from the queue.</span></span> <span data-ttu-id="e4feb-136">Pour plus d’informations sur le cycle de vie des messages cloud-à-appareil, consultez le [Guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e4feb-136">For more information about the cloud-to-device message lifecycle, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4feb-137">Lorsque vous utilisez HTTP comme moyen de transport au lieu de MQTT ou AMQP, la méthode `ReceiveAsync` est immédiatement renvoyée.</span><span class="sxs-lookup"><span data-stu-id="e4feb-137">When using HTTP instead of MQTT or AMQP as a transport, the `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="e4feb-138">Le modèle de prise en charge des messages cloud-à-appareil avec HTTP est représenté par des appareils connectés par intermittence qui vérifient rarement les messages (moins de toutes les 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="e4feb-138">The supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="e4feb-139">L’émission d’un nombre plus élevé de réceptions HTTP conduit IoT Hub à limiter les demandes.</span><span class="sxs-lookup"><span data-stu-id="e4feb-139">Issuing more HTTP receives results in IoT Hub throttling the requests.</span></span> <span data-ttu-id="e4feb-140">Pour plus d’informations sur les différences entre la prise en charge de MQTT, d’AMQP et de HTTP et la limitation d’IoT Hub, voir le [Guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e4feb-140">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="e4feb-141">Ajoutez la méthode suivante à la méthode **Main** juste avant la ligne `Console.ReadLine()` :</span><span class="sxs-lookup"><span data-stu-id="e4feb-141">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="e4feb-142">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="e4feb-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e4feb-143">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Transient Fault Handling](Gestion des erreurs temporaires).</span><span class="sxs-lookup"><span data-stu-id="e4feb-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="e4feb-144">Envoi d’un message cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="e4feb-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="e4feb-145">Dans cette section, vous écrivez une application console .NET qui envoie des messages cloud-à-appareil à l’application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="e4feb-145">In this section, you write a .NET console app that sends cloud-to-device messages to the device app.</span></span>

1. <span data-ttu-id="e4feb-146">Dans la solution Visual Studio actuelle, créez un projet d’application de bureau Visual C# à l’aide du modèle de projet **d’application de console** .</span><span class="sxs-lookup"><span data-stu-id="e4feb-146">In the current Visual Studio solution, create a Visual C# Desktop App project by using the **Console Application** project template.</span></span> <span data-ttu-id="e4feb-147">Nommez le projet **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-147">Name the project **SendCloudToDevice**.</span></span>
   
    ![Nouveau projet dans Visual Studio][20]
2. <span data-ttu-id="e4feb-149">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur la solution, puis cliquez sur **Gérer les packages NuGet pour la solution...**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-149">In Solution Explorer, right-click the solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="e4feb-150">La fenêtre **Gérer les packages NuGet** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e4feb-150">This action opens the **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="e4feb-151">Recherchez **Microsoft.Azure.Devices**, cliquez sur **Installer**, puis acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="e4feb-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span> 
   
    <span data-ttu-id="e4feb-152">Cette opération lance le téléchargement, l’installation et ajoute une référence au [package Azure IoT - Service SDK NuGet].</span><span class="sxs-lookup"><span data-stu-id="e4feb-152">This downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="e4feb-153">Ajoutez l'instruction `using` suivante en haut du fichier **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="e4feb-153">Add the following `using` statement at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="e4feb-154">Ajoutez les champs suivants à la classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="e4feb-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e4feb-155">Remplacez la valeur d’espace réservé par la chaîne de connexion du concentrateur IoT de la section [Prise en main d’Azure IoT Hub] :</span><span class="sxs-lookup"><span data-stu-id="e4feb-155">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="e4feb-156">Ajoutez la méthode suivante à la classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="e4feb-156">Add the following method to the **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="e4feb-157">Cette méthode envoie un nouveau message cloud-à-appareil à l’appareil avec l’ID `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="e4feb-157">This method sends a new cloud-to-device message to the device with the ID, `myFirstDevice`.</span></span> <span data-ttu-id="e4feb-158">Modifiez ce paramètre uniquement si vous avez modifié celui utilisé dans [Prise en main d’Azure IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="e4feb-158">Change this parameter only if you modified it from the one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="e4feb-159">Enfin, ajoutez les lignes suivantes à la méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="e4feb-159">Finally, add the following lines to the **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="e4feb-160">Dans Visual Studio, cliquez avec le bouton droit sur votre solution et sélectionnez **Définir les projets de démarrage...**. Sélectionnez **Plusieurs projets de démarrage**, puis l’action **Démarrer** pour les applications **ReadDeviceToCloudMessages**, **SimulatedDevice** et **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select the **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="e4feb-161">Appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-161">Press **F5**.</span></span> <span data-ttu-id="e4feb-162">Les trois applications doivent démarrer.</span><span class="sxs-lookup"><span data-stu-id="e4feb-162">All three applications should start.</span></span> <span data-ttu-id="e4feb-163">Sélectionnez les fenêtres **SendCloudToDevice**, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-163">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="e4feb-164">Vous devez voir le message reçu par l’application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="e4feb-164">You should see the message being received by the device app.</span></span>
   
   ![Application recevant le message][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="e4feb-166">Réception des commentaires de remise</span><span class="sxs-lookup"><span data-stu-id="e4feb-166">Receive delivery feedback</span></span>
<span data-ttu-id="e4feb-167">Il est possible de demander des accusés de réception (ou d’expiration) à IoT Hub pour chaque message cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="e4feb-167">It is possible to request delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="e4feb-168">Cette option permet au serveur principal de solution d’informer facilement d’une nouvelle tentative ou d’une logique de compensation.</span><span class="sxs-lookup"><span data-stu-id="e4feb-168">This option enables the solution back end to easily inform retry or compensation logic.</span></span> <span data-ttu-id="e4feb-169">Pour plus d’informations sur les commentaires de messages cloud-à-appareil, consultez le [Guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="e4feb-169">For more information about cloud-to-device feedback, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="e4feb-170">Dans cette section, vous modifiez l’application **SendCloudToDevice** de manière à exiger des commentaires et à en recevoir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e4feb-170">In this section, you modify the **SendCloudToDevice** app to request feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="e4feb-171">Dans Visual Studio, dans le projet **SendCloudToDevice**, ajoutez la méthode suivante à la classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-171">In Visual Studio, in the **SendCloudToDevice** project, add the following method to the **Program** class.</span></span>
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    <span data-ttu-id="e4feb-172">Notez que ce modèle de réception est le même que celui utilisé pour recevoir des messages cloud-à-appareil à partir de l’application de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="e4feb-172">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>
2. <span data-ttu-id="e4feb-173">Ajoutez la méthode suivante dans la méthode **Main** juste après la ligne `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` :</span><span class="sxs-lookup"><span data-stu-id="e4feb-173">Add the following method in the **Main** method, right after the `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="e4feb-174">Pour obtenir des commentaires sur la remise de votre message cloud-à-appareil, vous devez spécifier une propriété dans la méthode **SendCloudToDeviceMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="e4feb-174">To request feedback for the delivery of your cloud-to-device message, you have to specify a property in the **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="e4feb-175">Ajoutez la ligne suivante, immédiatement après la ligne `var commandMessage = new Message(...);` :</span><span class="sxs-lookup"><span data-stu-id="e4feb-175">Add the following line, right after the `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="e4feb-176">Exécutez les applications en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-176">Run the apps by pressing **F5**.</span></span> <span data-ttu-id="e4feb-177">Les trois applications doivent démarrer.</span><span class="sxs-lookup"><span data-stu-id="e4feb-177">You should see all three applications start.</span></span> <span data-ttu-id="e4feb-178">Sélectionnez les fenêtres **SendCloudToDevice**, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-178">Select the **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="e4feb-179">Vous devez voir le message reçu par l’application d’appareil et, après quelques secondes, le message de commentaires reçu par votre application **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="e4feb-179">You should see the message being received by the device app, and after a few seconds, the feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Application recevant le message][22]

> [!NOTE]
> <span data-ttu-id="e4feb-181">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="e4feb-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e4feb-182">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Transient Fault Handling](Gestion des erreurs temporaires).</span><span class="sxs-lookup"><span data-stu-id="e4feb-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e4feb-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e4feb-183">Next steps</span></span>
<span data-ttu-id="e4feb-184">Dans ce didacticiel, vous avez appris à envoyer et recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="e4feb-184">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="e4feb-185">Pour voir des exemples de solutions de bout en bout qui utilisent IoT Hub, consultez [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="e4feb-185">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="e4feb-186">Pour en savoir plus sur le développement de solutions avec IoT Hub, consultez le [Guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="e4feb-186">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[package Azure IoT - Service SDK NuGet]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guide du développeur IoT Hub]: iot-hub-devguide.md
[Prise en main d’Azure IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Kits Azure IoT device SDK]: iot-hub-devguide-sdks.md