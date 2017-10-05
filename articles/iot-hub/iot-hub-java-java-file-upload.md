---
title: "Charger des fichiers sur Azure IoT Hub à partir d’appareils en Java | Microsoft Docs"
description: "Guide pratique pour charger des fichiers sur le cloud à partir d’un appareil avec Azure IoT device SDK pour Java. Les fichiers téléchargés sont stockés dans un conteneur d’objets blob de stockage Azure."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: c917a3b3e16f1e84f202d6c87a04faf642266701
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="34ff1-104">Charger des fichiers sur le cloud à partir d’un appareil avec IoT Hub</span><span class="sxs-lookup"><span data-stu-id="34ff1-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="34ff1-105">Ce didacticiel s’appuie sur le code du didacticiel [Envoyer des messages du cloud vers un appareil avec IoT Hub](iot-hub-java-java-c2d.md) pour montrer comment utiliser les [fonctions de chargement de fichiers d’IoT Hub](iot-hub-devguide-file-upload.md) afin de charger un fichier sur le [Stockage Blob Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="34ff1-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="34ff1-106">Ce didacticiel explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="34ff1-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="34ff1-107">Fournissez en toute sécurité à un appareil un URI d’objet blob Azure pour le chargement d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="34ff1-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="34ff1-108">Utilisez les notifications de chargement de fichier IoT Hub pour déclencher le traitement du fichier dans votre serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="34ff1-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="34ff1-109">Les didacticiels [Bien démarrer avec IoT Hub](iot-hub-java-java-getstarted.md) et [Envoyer des messages du cloud vers un appareil avec IoT Hub](iot-hub-java-java-c2d.md) illustrent les fonctionnalités de base de la messagerie d’un appareil vers le cloud et du cloud vers un appareil offertes par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34ff1-109">The [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="34ff1-110">Le didacticiel [Traiter les messages appareil-à-cloud](iot-hub-java-java-process-d2c.md) décrit un moyen de stocker en toute fiabilité les messages appareil-à-cloud dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="34ff1-110">The [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="34ff1-111">Toutefois, dans certains scénarios, vous ne pouvez pas facilement mapper les données que vos appareils envoient dans des messages appareil-à-cloud relativement petits et acceptés par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34ff1-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="34ff1-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="34ff1-112">For example:</span></span>

* <span data-ttu-id="34ff1-113">Fichiers volumineux qui contiennent des images</span><span class="sxs-lookup"><span data-stu-id="34ff1-113">Large files that contain images</span></span>
* <span data-ttu-id="34ff1-114">Vidéos</span><span class="sxs-lookup"><span data-stu-id="34ff1-114">Videos</span></span>
* <span data-ttu-id="34ff1-115">Données de vibration échantillonnées à une fréquence élevée</span><span class="sxs-lookup"><span data-stu-id="34ff1-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="34ff1-116">Un certain type de données prétraitées.</span><span class="sxs-lookup"><span data-stu-id="34ff1-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="34ff1-117">Ces fichiers sont généralement traités par lot dans le cloud à l’aide d’outils tels que [Azure Data Factory](../data-factory/index.md) ou de la pile [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="34ff1-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="34ff1-118">Lorsque vous avez besoin de charger des fichiers à partir d’un appareil, vous pouvez quand même exploiter la sécurité et la fiabilité d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34ff1-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="34ff1-119">À la fin de ce didacticiel, vous exécuterez deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="34ff1-119">At the end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="34ff1-120">**simulated-device**, version modifiée de l’application créée dans le cadre du didacticiel [Envoyer des messages du cloud vers un appareil avec IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="34ff1-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="34ff1-121">Cette application charge un fichier de stockage à l’aide d’un URI SAP fourni par votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34ff1-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="34ff1-122">**read-file-upload-notification**, qui reçoit les notifications de chargement de fichiers envoyées par le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="34ff1-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="34ff1-123">IoT Hub prend en charge de nombreuses plateformes d’appareils et de nombreux langages (notamment C, .NET et JavaScript) par le biais des kits Azure IoT device SDK.</span><span class="sxs-lookup"><span data-stu-id="34ff1-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="34ff1-124">Pour obtenir des instructions pas à pas expliquant comment connecter votre appareil à Azure IoT Hub, voir le [Centre de développement Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="34ff1-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="34ff1-125">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="34ff1-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="34ff1-126">La version la plus récente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="34ff1-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="34ff1-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="34ff1-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="34ff1-128">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="34ff1-128">An active Azure account.</span></span> <span data-ttu-id="34ff1-129">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)</span><span class="sxs-lookup"><span data-stu-id="34ff1-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="34ff1-130">Charger un fichier à partir d’une application pour appareils</span><span class="sxs-lookup"><span data-stu-id="34ff1-130">Upload a file from a device app</span></span>

<span data-ttu-id="34ff1-131">Dans cette section, vous allez modifier l’application pour appareils que vous avez créée dans [Envoyer des messages du cloud vers un appareil avec IoT Hub](iot-hub-java-java-c2d.md) pour charger un fichier sur IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34ff1-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="34ff1-132">Copiez un fichier image dans le dossier `simulated-device` et renommez-le `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="34ff1-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="34ff1-133">Ouvrez le fichier `simulated-device\src\main\java\com\mycompany\app\App.java` dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="34ff1-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="34ff1-134">Ajoutez la déclaration de variable à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-134">Add the variable declaration to the **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="34ff1-135">Pour traiter les messages de rappel d’état du chargement de fichiers, ajoutez la classe imbriquée suivante à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-135">To process file upload status callback messages, add the following nested class to the **App** class:</span></span>

    ```java
    // Define a callback method to print status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to file upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="34ff1-136">Pour charger des images sur IoT Hub, ajoutez la méthode suivante à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span></span>

    ```java
    // Use IoT Hub to upload a file asynchronously to Azure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="34ff1-137">Modifiez la méthode **main** de façon à appeler la méthode **uploadFile**, comme dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="34ff1-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get the filename and start the upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="34ff1-138">Utilisez la commande suivante pour générer l’application **simulated-device** et vérifiez l’absence d’erreurs :</span><span class="sxs-lookup"><span data-stu-id="34ff1-138">Use the following command to build the **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="34ff1-139">Recevoir une notification de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="34ff1-139">Receive a file upload notification</span></span>

<span data-ttu-id="34ff1-140">Dans cette section, vous allez créer une application console Java qui reçoit des messages de notification de chargement de fichiers envoyés par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="34ff1-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="34ff1-141">Vous avez besoin de la chaîne de connexion **iothubowner** de votre hub IoT pour suivre cette section.</span><span class="sxs-lookup"><span data-stu-id="34ff1-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span></span> <span data-ttu-id="34ff1-142">Vous trouverez la chaîne de connexion sur le panneau **Stratégie d’accès partagé** du [Portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="34ff1-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="34ff1-143">Créez un projet Maven nommé **read-file-upload-notification** en lançant la commande ci-dessous dans votre invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="34ff1-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span></span> <span data-ttu-id="34ff1-144">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="34ff1-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="34ff1-145">Dans votre invite de commandes, accédez au nouveau dossier `read-file-upload-notification`.</span><span class="sxs-lookup"><span data-stu-id="34ff1-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="34ff1-146">Dans un éditeur de texte, ouvrez le fichier `pom.xml` dans le dossier `read-file-upload-notification` et ajoutez la dépendance suivante au nœud **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="34ff1-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="34ff1-147">L’ajout de la dépendance vous permet d’utiliser le package **iothub-java-service-client** dans votre application pour communiquer avec votre service d’IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="34ff1-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="34ff1-148">Vous pouvez rechercher la dernière version de **iot-service-client** avec la [recherche Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="34ff1-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="34ff1-149">Enregistrez et fermez le fichier `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="34ff1-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="34ff1-150">Ouvrez le fichier `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="34ff1-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="34ff1-151">Ajoutez les instructions **import** suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="34ff1-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="34ff1-152">Ajoutez les variables de niveau classe ci-après à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-152">Add the following class-level variables to the **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="34ff1-153">Pour imprimer des informations sur le chargement de fichiers dans la console, ajoutez la classe imbriquée suivante à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Create a thread to receive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="34ff1-154">Pour démarrer le thread qui écoute les notifications de chargement de fichiers, ajoutez le code suivant à la méthode **main** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from the ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start the thread to receive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER to exit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="34ff1-155">Enregistrez et fermez le fichier `read-file-upload-notification\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="34ff1-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="34ff1-156">Utilisez la commande suivante pour générer l’application **read-file-upload-notification** et vérifiez l’absence d’erreurs :</span><span class="sxs-lookup"><span data-stu-id="34ff1-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="34ff1-157">Exécution des applications</span><span class="sxs-lookup"><span data-stu-id="34ff1-157">Run the applications</span></span>

<span data-ttu-id="34ff1-158">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="34ff1-158">Now you are ready to run the applications.</span></span>

<span data-ttu-id="34ff1-159">Dans une invite de commandes, exécutez la commande suivante dans le dossier `read-file-upload-notification` :</span><span class="sxs-lookup"><span data-stu-id="34ff1-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="34ff1-160">Dans une invite de commandes, exécutez la commande suivante dans le dossier `simulated-device` :</span><span class="sxs-lookup"><span data-stu-id="34ff1-160">At a command prompt in the `simulated-device` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="34ff1-161">La capture d’écran suivante montre la sortie de l’application **simulated-device** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-161">The following screenshot shows the output from the **simulated-device** app:</span></span>

![Sortie de l’application simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="34ff1-163">La capture d’écran suivante montre la sortie de l’application **read-file-upload-notification** :</span><span class="sxs-lookup"><span data-stu-id="34ff1-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span></span>

![Sortie de l’application read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="34ff1-165">Vous pouvez utiliser le portail pour afficher le fichier chargé dans le conteneur de stockage que vous avez configuré :</span><span class="sxs-lookup"><span data-stu-id="34ff1-165">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![Fichier chargé](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="34ff1-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34ff1-167">Next steps</span></span>

<span data-ttu-id="34ff1-168">Dans ce didacticiel, vous avez appris à utiliser les fonctionnalités de téléchargement de fichier d’IoT Hub pour simplifier les chargements de fichiers à partir d’appareils.</span><span class="sxs-lookup"><span data-stu-id="34ff1-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="34ff1-169">Vous pouvez continuer à explorer les scénarios et fonctionnalités d’IoT Hub avec les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="34ff1-169">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="34ff1-170">[Créer un IoT Hub par programme][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="34ff1-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="34ff1-171">[Présentation du Kit de développement logiciel (SDK) C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="34ff1-171">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="34ff1-172">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="34ff1-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="34ff1-173">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="34ff1-173">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="34ff1-174">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="34ff1-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Centre de développement Azure IoT]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


