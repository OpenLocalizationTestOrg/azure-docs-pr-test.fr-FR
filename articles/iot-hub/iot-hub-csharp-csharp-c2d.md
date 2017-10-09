---
title: "les messages aaaCloud sur l’appareil avec Azure IoT Hub (.NET) | Documents Microsoft"
description: "Comment toosend cloud-à-appareil messages appareil tooa à partir d’un hub IoT d’Azure à l’aide de kits de développement IoT hello Azure pour .NET. Modifier une application appareil tooreceive les messages cloud-à-appareil et de modifier une application de serveur principal toosend hello cloud-à-appareil les messages."
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
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a><span data-ttu-id="53f3d-104">Envoyer des messages à partir de l’appareil de tooyour hello cloud avec IoT Hub (.NET)</span><span class="sxs-lookup"><span data-stu-id="53f3d-104">Send messages from hello cloud tooyour device with IoT Hub (.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="53f3d-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="53f3d-105">Introduction</span></span>
<span data-ttu-id="53f3d-106">Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="53f3d-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="53f3d-107">Hello [prise en main IoT Hub] didacticiel montre comment toocreate un IoT hub, configurer une identité d’appareil qu’il contient et code d’une application de périphérique qui envoie des messages de l’appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="53f3d-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="53f3d-108">Ce didacticiel s’appuie sur l’article [prise en main IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="53f3d-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="53f3d-109">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="53f3d-109">It shows you how to:</span></span>

* <span data-ttu-id="53f3d-110">À partir de votre solution back-end, envoyer des messages cloud-à-appareil tooa seule unité via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53f3d-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="53f3d-111">Recevez des messages cloud-à-appareil sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="53f3d-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="53f3d-112">À partir de votre solution back-end demande l’accusé de réception (*commentaires*) pour tooa appareil les messages envoyés à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53f3d-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="53f3d-113">Vous trouverez plus d’informations sur les messages cloud-à-appareil Bonjour [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="53f3d-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="53f3d-114">À la fin de hello de ce didacticiel, vous exécutez deux applications de console .NET :</span><span class="sxs-lookup"><span data-stu-id="53f3d-114">At hello end of this tutorial, you run two .NET console apps:</span></span>

* <span data-ttu-id="53f3d-115">**SimulatedDevice**, une version modifiée de l’application hello créée dans [prise en main IoT Hub], qui se connecte tooyour IoT hub et reçoit des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="53f3d-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="53f3d-116">**SendCloudToDevice**, qui envoie une application de périphérique toohello cloud-à-appareil message via IoT Hub et reçoit ensuite son accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="53f3d-116">**SendCloudToDevice**, which sends a cloud-to-device message toohello device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="53f3d-117">IoT Hub offre la prise en charge de Kits de développement logiciel (SDK) pour plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des [Kits Azure IoT device SDK].</span><span class="sxs-lookup"><span data-stu-id="53f3d-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through [Azure IoT device SDKs].</span></span> <span data-ttu-id="53f3d-118">Pour obtenir des instructions sur tooconnect du votre appareil toothis didacticiel code et généralement tooAzure IoT Hub, voir hello [guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="53f3d-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [IoT Hub developer guide].</span></span>
> 
> 

<span data-ttu-id="53f3d-119">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="53f3d-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="53f3d-120">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="53f3d-120">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="53f3d-121">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="53f3d-121">An active Azure account.</span></span> <span data-ttu-id="53f3d-122">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="53f3d-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-device-app"></a><span data-ttu-id="53f3d-123">Recevoir des messages dans une application de périphérique hello</span><span class="sxs-lookup"><span data-stu-id="53f3d-123">Receive messages in hello device app</span></span>
<span data-ttu-id="53f3d-124">Dans cette section, vous allez modifier créé à l’application pour appareil hello [prise en main IoT Hub] tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-124">In this section, you'll modify hello device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="53f3d-125">Dans Visual Studio, Bonjour **SimulatedDevice** de projet, ajoutez hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="53f3d-125">In Visual Studio, in hello **SimulatedDevice** project, add hello following method toohello **Program** class.</span></span>
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
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
   
    <span data-ttu-id="53f3d-126">Hello `ReceiveAsync` méthode renvoie de manière asynchrone message de salutation reçu au moment de hello est reçue par le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-126">hello `ReceiveAsync` method asynchronously returns hello received message at hello time that it is received by hello device.</span></span> <span data-ttu-id="53f3d-127">Elle retourne *null* après une période de délai d’attente pouvant être précisés (dans ce cas, est utilisé par défaut de hello d’une minute).</span><span class="sxs-lookup"><span data-stu-id="53f3d-127">It returns *null* after a specifiable timeout period (in this case, hello default of one minute is used).</span></span> <span data-ttu-id="53f3d-128">Lorsque application hello reçoit un *null*, il doit continuer toowait pour les nouveaux messages.</span><span class="sxs-lookup"><span data-stu-id="53f3d-128">When hello app receives a *null*, it should continue toowait for new messages.</span></span> <span data-ttu-id="53f3d-129">Cette exigence est la raison de hello hello `if (receivedMessage == null) continue` ligne.</span><span class="sxs-lookup"><span data-stu-id="53f3d-129">This requirement is hello reason for hello `if (receivedMessage == null) continue` line.</span></span>
   
    <span data-ttu-id="53f3d-130">Hello appel trop`CompleteAsync()` notifie IoT Hub ce message de salutation n’a pas été correctement traité.</span><span class="sxs-lookup"><span data-stu-id="53f3d-130">hello call too`CompleteAsync()` notifies IoT Hub that hello message has been successfully processed.</span></span> <span data-ttu-id="53f3d-131">message de type Hello peut être supprimé à partir de la file d’attente de hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-131">hello message can be safely removed from hello device queue.</span></span> <span data-ttu-id="53f3d-132">Si un problème est survenu cette application de périphérique a empêché hello à partir de la fin du traitement de hello de message de type hello, IoT Hub le remet à nouveau.</span><span class="sxs-lookup"><span data-stu-id="53f3d-132">If something happened that prevented hello device app from completing hello processing of hello message, IoT Hub delivers it again.</span></span> <span data-ttu-id="53f3d-133">Il est important de cette logique dans l’application hello de traitement des messages sont puis *idempotent*, de sorte que la réception hello même message plusieurs fois produit hello même résultat.</span><span class="sxs-lookup"><span data-stu-id="53f3d-133">It is then important that message processing logic in hello device app is *idempotent*, so that receiving hello same message multiple times produces hello same result.</span></span> <span data-ttu-id="53f3d-134">Une application peut abandonner également temporairement un message, ce qui entraîne l’IoT hub en conservant le message de type hello dans la file d’attente hello de sa consommation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="53f3d-134">An application can also temporarily abandon a message, which results in IoT hub retaining hello message in hello queue for future consumption.</span></span> <span data-ttu-id="53f3d-135">Ou bien, application hello capable de rejeter un message, ce qui supprime définitivement le message de type hello à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-135">Or, hello application can reject a message, which permanently removes hello message from hello queue.</span></span> <span data-ttu-id="53f3d-136">Pour plus d’informations sur le cycle de vie des cloud-à-appareil message hello, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="53f3d-136">For more information about hello cloud-to-device message lifecycle, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="53f3d-137">Lorsque vous utilisez HTTP au lieu de MQTT ou AMQP comme transport, hello `ReceiveAsync` méthode est retournée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="53f3d-137">When using HTTP instead of MQTT or AMQP as a transport, hello `ReceiveAsync` method returns immediately.</span></span> <span data-ttu-id="53f3d-138">modèle Hello pris en charge pour les messages cloud-à-appareil avec HTTP est connectés en permanence pour les appareils qui vérifient pour les messages rarement (inférieur à 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="53f3d-138">hello supported pattern for cloud-to-device messages with HTTP is intermittently connected devices that check for messages infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="53f3d-139">Émission plus HTTP reçoit les résultats dans les demandes de hello limitation IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53f3d-139">Issuing more HTTP receives results in IoT Hub throttling hello requests.</span></span> <span data-ttu-id="53f3d-140">Pour plus d’informations sur les différences de hello entre la prise en charge MQTT, AMQP et HTTP et de limitation IoT Hub, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="53f3d-140">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 
2. <span data-ttu-id="53f3d-141">Ajouter hello méthode Bonjour **principal** méthode, juste avant hello `Console.ReadLine()` ligne :</span><span class="sxs-lookup"><span data-stu-id="53f3d-141">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>
   
        ReceiveC2dAsync();

> [!NOTE]
> <span data-ttu-id="53f3d-142">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="53f3d-142">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="53f3d-143">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="53f3d-143">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="53f3d-144">Envoi d’un message cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="53f3d-144">Send a cloud-to-device message</span></span>
<span data-ttu-id="53f3d-145">Dans cette section, vous écrivez une application console .NET qui envoie des messages cloud-à-appareil toohello appareil application.</span><span class="sxs-lookup"><span data-stu-id="53f3d-145">In this section, you write a .NET console app that sends cloud-to-device messages toohello device app.</span></span>

1. <span data-ttu-id="53f3d-146">Dans la solution de Visual Studio en cours de hello, créer un projet d’application de bureau Visual c# à l’aide de hello **Application Console** modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="53f3d-146">In hello current Visual Studio solution, create a Visual C# Desktop App project by using hello **Console Application** project template.</span></span> <span data-ttu-id="53f3d-147">Projet de hello nom **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="53f3d-147">Name hello project **SendCloudToDevice**.</span></span>
   
    ![Nouveau projet dans Visual Studio][20]
2. <span data-ttu-id="53f3d-149">Dans l’Explorateur de solutions, cliquez sur la solution de hello, puis cliquez sur **gérer les Packages NuGet pour la Solution...** .</span><span class="sxs-lookup"><span data-stu-id="53f3d-149">In Solution Explorer, right-click hello solution, and then click **Manage NuGet Packages for Solution...**.</span></span> 
   
    <span data-ttu-id="53f3d-150">Cette action ouvre hello **gérer les Packages NuGet** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="53f3d-150">This action opens hello **Manage NuGet Packages** window.</span></span>
3. <span data-ttu-id="53f3d-151">Recherchez **Microsoft.Azure.Devices**, cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-151">Search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span> 
   
    <span data-ttu-id="53f3d-152">Il télécharge, installe et ajoute une référence toohello [package NuGet du SDK du service Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="53f3d-152">This downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package].</span></span>

4. <span data-ttu-id="53f3d-153">Ajoutez hello suivant `using` instruction début hello Hello **Program.cs** fichier :</span><span class="sxs-lookup"><span data-stu-id="53f3d-153">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="53f3d-154">Ajouter hello suivant champs toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="53f3d-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="53f3d-155">Valeur d’espace réservé hello avec hello IoT hub chaîne de connexion de remplacement [prise en main IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="53f3d-155">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="53f3d-156">Ajouter hello suivant de méthode toohello **programme** classe :</span><span class="sxs-lookup"><span data-stu-id="53f3d-156">Add hello following method toohello **Program** class:</span></span>
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    <span data-ttu-id="53f3d-157">Cette méthode envoie un nouveau périphérique de toohello cloud-à-appareil message avec l’ID de hello, `myFirstDevice`.</span><span class="sxs-lookup"><span data-stu-id="53f3d-157">This method sends a new cloud-to-device message toohello device with hello ID, `myFirstDevice`.</span></span> <span data-ttu-id="53f3d-158">Modifiez ce paramètre uniquement si vous l’avez modifié à partir de hello celui utilisé dans [prise en main IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="53f3d-158">Change this parameter only if you modified it from hello one used in [Get started with IoT Hub].</span></span>
7. <span data-ttu-id="53f3d-159">Enfin, ajoutez hello suivant lignes toohello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="53f3d-159">Finally, add hello following lines toohello **Main** method:</span></span>
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="53f3d-160">Dans Visual Studio, cliquez avec le bouton droit sur votre solution et sélectionnez **Définir les projets de démarrage...**. Sélectionnez **plusieurs projets de démarrage**, puis sélectionnez hello **Démarrer** action pour **ReadDeviceToCloudMessages**, **SimulatedDevice**, et **SendCloudToDevice**.</span><span class="sxs-lookup"><span data-stu-id="53f3d-160">From within Visual Studio, right-click your solution, and select **Set StartUp projects...**. Select **Multiple startup projects**, then select hello **Start** action for **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **SendCloudToDevice**.</span></span>
9. <span data-ttu-id="53f3d-161">Appuyez sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="53f3d-161">Press **F5**.</span></span> <span data-ttu-id="53f3d-162">Les trois applications doivent démarrer.</span><span class="sxs-lookup"><span data-stu-id="53f3d-162">All three applications should start.</span></span> <span data-ttu-id="53f3d-163">Sélectionnez hello **SendCloudToDevice** windows, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="53f3d-163">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="53f3d-164">Vous devez voir le message de salutation reçu par l’application d’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-164">You should see hello message being received by hello device app.</span></span>
   
   ![Application recevant le message][21]

## <a name="receive-delivery-feedback"></a><span data-ttu-id="53f3d-166">Réception des commentaires de remise</span><span class="sxs-lookup"><span data-stu-id="53f3d-166">Receive delivery feedback</span></span>
<span data-ttu-id="53f3d-167">Il est possible de toorequest remise (ou expiration) des accusés de réception IoT Hub pour chaque message cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="53f3d-167">It is possible toorequest delivery (or expiration) acknowledgements from IoT Hub for each cloud-to-device message.</span></span> <span data-ttu-id="53f3d-168">Cette tooeasily back-end de solution option active hello informe la logique de nouvelle tentative ou de compensation.</span><span class="sxs-lookup"><span data-stu-id="53f3d-168">This option enables hello solution back end tooeasily inform retry or compensation logic.</span></span> <span data-ttu-id="53f3d-169">Pour plus d’informations sur les évaluations du cloud sur l’appareil, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="53f3d-169">For more information about cloud-to-device feedback, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="53f3d-170">Dans cette section, vous modifiez hello **SendCloudToDevice** commentaires concernant l’application toorequest et recevoir d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="53f3d-170">In this section, you modify hello **SendCloudToDevice** app toorequest feedback, and receive it from IoT Hub.</span></span>

1. <span data-ttu-id="53f3d-171">Dans Visual Studio, Bonjour **SendCloudToDevice** de projet, ajoutez hello suivant de méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="53f3d-171">In Visual Studio, in hello **SendCloudToDevice** project, add hello following method toohello **Program** class.</span></span>
   
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
   
    <span data-ttu-id="53f3d-172">Remarque : ce modèle de réception est hello les mêmes messages cloud-à-appareil tooreceive utilisé un à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="53f3d-172">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>
2. <span data-ttu-id="53f3d-173">Ajouter hello méthode Bonjour **principal** méthode, juste après hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` ligne :</span><span class="sxs-lookup"><span data-stu-id="53f3d-173">Add hello following method in hello **Main** method, right after hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` line:</span></span>
   
        ReceiveFeedbackAsync();
3. <span data-ttu-id="53f3d-174">commentaires toorequest pour la remise de hello de votre message cloud-à-appareil, vous avez toospecify une propriété Bonjour **SendCloudToDeviceMessageAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="53f3d-174">toorequest feedback for hello delivery of your cloud-to-device message, you have toospecify a property in hello **SendCloudToDeviceMessageAsync** method.</span></span> <span data-ttu-id="53f3d-175">Ajouter hello suivant de ligne, juste après hello `var commandMessage = new Message(...);` ligne :</span><span class="sxs-lookup"><span data-stu-id="53f3d-175">Add hello following line, right after hello `var commandMessage = new Message(...);` line:</span></span>
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. <span data-ttu-id="53f3d-176">Exécuter des applications de hello en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="53f3d-176">Run hello apps by pressing **F5**.</span></span> <span data-ttu-id="53f3d-177">Les trois applications doivent démarrer.</span><span class="sxs-lookup"><span data-stu-id="53f3d-177">You should see all three applications start.</span></span> <span data-ttu-id="53f3d-178">Sélectionnez hello **SendCloudToDevice** windows, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="53f3d-178">Select hello **SendCloudToDevice** windows, and press **Enter**.</span></span> <span data-ttu-id="53f3d-179">Vous devez voir hello de message reçus par l’application hello et après quelques secondes, hello message des commentaires reçu par votre **SendCloudToDevice** application.</span><span class="sxs-lookup"><span data-stu-id="53f3d-179">You should see hello message being received by hello device app, and after a few seconds, hello feedback message being received by your **SendCloudToDevice** application.</span></span>
   
   ![Application recevant le message][22]

> [!NOTE]
> <span data-ttu-id="53f3d-181">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="53f3d-181">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="53f3d-182">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="53f3d-182">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="53f3d-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53f3d-183">Next steps</span></span>
<span data-ttu-id="53f3d-184">Dans ce didacticiel, vous avez appris comment toosend et recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="53f3d-184">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="53f3d-185">exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="53f3d-185">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="53f3d-186">toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="53f3d-186">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[package NuGet du SDK du service Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[guide du développeur IoT Hub]: iot-hub-devguide.md
[prise en main IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[Kits Azure IoT device SDK]: iot-hub-devguide-sdks.md