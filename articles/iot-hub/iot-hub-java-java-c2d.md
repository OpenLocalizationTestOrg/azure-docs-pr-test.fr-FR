---
title: "messages aaaCloud sur l’appareil avec Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment toosend cloud-à-appareil messages appareil tooa à partir d’un hub IoT d’Azure à l’aide de kits de développement IoT hello Azure pour Java. Modifier une application appareil simulé tooreceive les messages cloud-à-appareil et de modifier une application de serveur principal toosend hello cloud-à-appareil les messages."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="df5e2-104">Envoi de messages cloud à appareil avec IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="df5e2-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="df5e2-105">Azure IoT Hub est un service entièrement géré qui permet d’autoriser des communications bidirectionnelles fiables et sécurisées entre des millions d’appareils et un serveur principal de solution.</span><span class="sxs-lookup"><span data-stu-id="df5e2-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="df5e2-106">Hello [prise en main IoT Hub] didacticiel montre comment toocreate un IoT hub, configurer une identité d’appareil qu’il contient et code d’une application d’appareil simulé qui envoie des messages de l’appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="df5e2-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="df5e2-107">Ce didacticiel s’appuie sur l’article [prise en main IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="df5e2-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="df5e2-108">Cette rubrique vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="df5e2-108">It shows you how to:</span></span>

* <span data-ttu-id="df5e2-109">À partir de votre solution back-end, envoyer des messages cloud-à-appareil tooa seule unité via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="df5e2-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="df5e2-110">Recevez des messages cloud-à-appareil sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="df5e2-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="df5e2-111">À partir de votre solution back-end demande l’accusé de réception (*commentaires*) pour tooa appareil les messages envoyés à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="df5e2-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="df5e2-112">Vous trouverez plus d’informations sur les messages cloud-à-appareil Bonjour [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="df5e2-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="df5e2-113">À la fin de hello de ce didacticiel, vous exécutez deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="df5e2-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="df5e2-114">**APPAREIL simulé**, une version modifiée de l’application hello créée dans [prise en main IoT Hub], qui se connecte tooyour IoT hub et reçoit des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="df5e2-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="df5e2-115">**envoi de messages de c2d**, qui envoie une application d’appareil simulé toohello cloud-à-appareil message via IoT Hub et reçoit ensuite son accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="df5e2-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="df5e2-116">IoT Hub offre la prise en charge de plusieurs plateformes d’appareils et plusieurs langages (notamment C, Java et Javascript) par le biais des Kits de développement logiciel (SDK) d’appareils Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="df5e2-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="df5e2-117">Pour obtenir des instructions sur tooconnect du votre appareil toothis didacticiel code et généralement tooAzure IoT Hub, voir hello [centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="df5e2-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="df5e2-118">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="df5e2-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="df5e2-119">Une version complète de travail de hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) ou [les messages appareil-à-cloud processus IoT Hub](iot-hub-java-java-process-d2c.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5e2-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="df5e2-120">Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="df5e2-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="df5e2-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="df5e2-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="df5e2-122">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="df5e2-122">An active Azure account.</span></span> <span data-ttu-id="df5e2-123">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="df5e2-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="df5e2-124">Recevoir des messages dans une application d’appareil simulé hello</span><span class="sxs-lookup"><span data-stu-id="df5e2-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="df5e2-125">Dans cette section, vous modifiez l’application d’appareil simulé hello vous avez créé dans [prise en main IoT Hub] tooreceive les messages cloud-à-appareil à partir du hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="df5e2-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="df5e2-126">À l’aide d’un éditeur de texte, d’ouvrir le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="df5e2-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="df5e2-127">Ajoutez hello suivant **MessageCallback** classe comme une classe imbriquée dans hello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="df5e2-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="df5e2-128">Hello **exécuter** méthode est appelée lors de l’appareil de hello reçoit un message d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="df5e2-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="df5e2-129">Dans cet exemple, les appareils hello notifie toujours hub IoT de hello qu’il a complété le message de type hello :</span><span class="sxs-lookup"><span data-stu-id="df5e2-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="df5e2-130">Modifier hello **principal** méthode toocreate une **AppMessageCallback** hello instance et appelez **setMessageCallback** méthode avant d’ouvrir les client hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="df5e2-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="df5e2-131">Si vous utilisez HTTP au lieu de MQTT ou AMQP comme couche de transport hello, hello **DeviceClient** instance vérifie les messages à partir du IoT Hub rarement (inférieur à 25 minutes).</span><span class="sxs-lookup"><span data-stu-id="df5e2-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="df5e2-132">Pour plus d’informations sur les différences de hello entre la prise en charge MQTT, AMQP et HTTP et de limitation IoT Hub, consultez hello [guide du développeur IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="df5e2-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="df5e2-133">toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :</span><span class="sxs-lookup"><span data-stu-id="df5e2-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="df5e2-134">Envoi d’un message cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="df5e2-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="df5e2-135">Dans cette section, vous créez une application console Java qui envoie des messages cloud-à-appareil toohello appareil simulé application.</span><span class="sxs-lookup"><span data-stu-id="df5e2-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="df5e2-136">Vous devez hello ID de périphérique périphérique hello vous avez ajouté dans hello [prise en main IoT Hub] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="df5e2-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="df5e2-137">Vous devez également hello chaîne de connexion IoT Hub pour votre concentrateur que vous pouvez trouver Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="df5e2-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="df5e2-138">Créez un projet Maven appelé **-c2d-envoyer des messages** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="df5e2-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="df5e2-139">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="df5e2-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="df5e2-140">À l’invite de commandes, accédez toohello nouveau dossier d’envoi de messages de c2d.</span><span class="sxs-lookup"><span data-stu-id="df5e2-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="df5e2-141">À l’aide d’un éditeur de texte, ouvrez le fichier de pom.xml de hello dans le dossier d’envoi-c2d-messages hello et ajouter hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="df5e2-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="df5e2-142">Ajout de la dépendance de hello vous permet de toouse hello **iothub-java-service-client** package dans toocommunicate de votre application avec votre service de hub IoT :</span><span class="sxs-lookup"><span data-stu-id="df5e2-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="df5e2-143">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="df5e2-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="df5e2-144">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="df5e2-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="df5e2-145">À l’aide d’un éditeur de texte, d’ouvrir le fichier de send-c2d-messages\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="df5e2-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="df5e2-146">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="df5e2-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="df5e2-147">Ajouter hello suivant des variables de niveau classe toohello **application** classe, en remplaçant **{yourhubconnectionstring}** et **{yourdeviceid}** avec hello des valeurs votre indiqués précédemment :</span><span class="sxs-lookup"><span data-stu-id="df5e2-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="df5e2-148">Remplacez hello **principal** méthode avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="df5e2-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="df5e2-149">Ce code connecte tooyour IoT hub, envoie un périphérique tooyour de message et attend un accusé de réception que message hello reçus et traités d’appareil hello :</span><span class="sxs-lookup"><span data-stu-id="df5e2-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="df5e2-150">Par souci de simplicité, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="df5e2-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="df5e2-151">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, d’interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires].</span><span class="sxs-lookup"><span data-stu-id="df5e2-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="df5e2-152">toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :</span><span class="sxs-lookup"><span data-stu-id="df5e2-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="df5e2-153">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="df5e2-153">Run hello applications</span></span>

<span data-ttu-id="df5e2-154">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="df5e2-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="df5e2-155">À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande envoi IoT hub tooyour de télémétrie et toolisten pour les messages cloud-à-appareil envoyés à partir de votre hub :</span><span class="sxs-lookup"><span data-stu-id="df5e2-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Exécutez l’application d’appareil simulé hello][img-simulated-device]

2. <span data-ttu-id="df5e2-157">À une invite de commandes dans le dossier d’envoi-c2d-messages hello, exécutez hello suivant commande toosend un message du cloud sur l’appareil et l’attendre un accusé de réception de commentaires :</span><span class="sxs-lookup"><span data-stu-id="df5e2-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Exécuter le message de salutation commande toosend hello cloud-à-appareil][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="df5e2-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df5e2-159">Next steps</span></span>

<span data-ttu-id="df5e2-160">Dans ce didacticiel, vous avez appris comment toosend et recevoir des messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="df5e2-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="df5e2-161">exemples de toosee des solutions de bout en bout complets qui utilisent l’IoT Hub, consultez [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="df5e2-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="df5e2-162">toolearn savoir plus sur le développement de solutions avec IoT Hub, consultez hello [guide du développeur IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="df5e2-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[prise en main IoT Hub]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[guide du développeur IoT Hub]: iot-hub-devguide.md
[centre de développement Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[gestion des pannes temporaires]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portail Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22