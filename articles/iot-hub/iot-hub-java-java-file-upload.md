---
title: "les fichiers à partir d’appareils tooAzure IoT Hub avec Java aaaUpload | Documents Microsoft"
description: "Comment tooupload les fichiers à partir d’un appareil cloud toohello à l’aide du SDK de périphérique Azure IoT pour Java. Les fichiers téléchargés sont stockés dans un conteneur d’objets blob de stockage Azure."
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
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="96f0e-104">Télécharger des fichiers à partir de votre appareil toohello cloud avec IoT Hub</span><span class="sxs-lookup"><span data-stu-id="96f0e-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="96f0e-105">Ce didacticiel s’appuie sur le code hello Bonjour [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-java-java-c2d.md) tooshow didacticiel vous comment toouse hello [fichier capacités de téléchargement de IoT Hub](iot-hub-devguide-file-upload.md) tooupload un fichier trop[ Stockage d’objets blob Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="96f0e-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="96f0e-106">didacticiel de Hello vous montre comment procéder pour :</span><span class="sxs-lookup"><span data-stu-id="96f0e-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="96f0e-107">Fournissez en toute sécurité à un appareil un URI d’objet blob Azure pour le chargement d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="96f0e-108">Utilisez hello IoT Hub fichier téléchargement notifications tootrigger traitement du fichier hello dans votre principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="96f0e-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="96f0e-109">Hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) et [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-java-java-c2d.md) didacticiels montrent hello appareil-à-cloud et cloud-à-appareil messagerie fonctionnalités de base d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96f0e-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="96f0e-110">Hello [messages processus appareil-à-Cloud](iot-hub-java-java-process-d2c.md) didacticiel décrit une façon tooreliably stocker appareil-à-cloud les messages dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="96f0e-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="96f0e-111">Toutefois, dans certains scénarios vous ne peut pas mapper facilement les données de hello que vos appareils envoient en messages appareil-à-cloud relativement faible hello qui accepte une IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96f0e-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="96f0e-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="96f0e-112">For example:</span></span>

* <span data-ttu-id="96f0e-113">Fichiers volumineux qui contiennent des images</span><span class="sxs-lookup"><span data-stu-id="96f0e-113">Large files that contain images</span></span>
* <span data-ttu-id="96f0e-114">Vidéos</span><span class="sxs-lookup"><span data-stu-id="96f0e-114">Videos</span></span>
* <span data-ttu-id="96f0e-115">Données de vibration échantillonnées à une fréquence élevée</span><span class="sxs-lookup"><span data-stu-id="96f0e-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="96f0e-116">Un certain type de données prétraitées.</span><span class="sxs-lookup"><span data-stu-id="96f0e-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="96f0e-117">Ces fichiers sont généralement traitées dans le cloud hello à l’aide des outils tels que par lots [Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pile.</span><span class="sxs-lookup"><span data-stu-id="96f0e-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="96f0e-118">Lorsque vous avez besoin des fichiers tooupland à partir d’un appareil, vous pouvez toujours utiliser sécurité de hello et la fiabilité de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96f0e-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="96f0e-119">À la fin de hello de ce didacticiel, vous exécutez deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="96f0e-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="96f0e-120">**APPAREIL simulé**, une version modifiée de l’application hello créée dans le didacticiel de hello [messages envoi Cloud-à-appareil avec IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="96f0e-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="96f0e-121">Cette application télécharge une toostorage de fichier à l’aide d’un URI SAS fournie par votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="96f0e-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="96f0e-122">**read-file-upload-notification**, qui reçoit les notifications de chargement de fichiers envoyées par le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="96f0e-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="96f0e-123">IoT Hub prend en charge de nombreuses plateformes d’appareils et de nombreux langages (notamment C, .NET et JavaScript) par le biais des kits Azure IoT device SDK.</span><span class="sxs-lookup"><span data-stu-id="96f0e-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="96f0e-124">Consultez toohello [centre de développement Azure IoT] pour obtenir des instructions sur la façon de tooconnect votre tooAzure appareil IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96f0e-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="96f0e-125">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="96f0e-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="96f0e-126">Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="96f0e-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="96f0e-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="96f0e-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="96f0e-128">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="96f0e-128">An active Azure account.</span></span> <span data-ttu-id="96f0e-129">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)</span><span class="sxs-lookup"><span data-stu-id="96f0e-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="96f0e-130">Charger un fichier à partir d’une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="96f0e-130">Upload a file from a device app</span></span>

<span data-ttu-id="96f0e-131">Dans cette section, vous modifiez l’application d’appareil hello vous avez créé dans [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-java-java-c2d.md) tooupload un concentrateur de tooIoT de fichier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="96f0e-132">Copier un toohello de fichier image `simulated-device` dossier et renommez-le `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="96f0e-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="96f0e-133">À l’aide d’un éditeur de texte, ouvrez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="96f0e-134">Ajouter hello déclaration de variable toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="96f0e-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="96f0e-135">tooprocess messages de rappel d’état du téléchargement de fichiers, ajoutez hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="96f0e-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="96f0e-136">tooupload images tooIoT Hub, ajouter hello suivant de méthode toohello **application** tooupload de classe images tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="96f0e-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="96f0e-137">Modifier hello **principal** hello toocall de méthode **uploadFile** illustré hello suivant extrait la méthode :</span><span class="sxs-lookup"><span data-stu-id="96f0e-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
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

1. <span data-ttu-id="96f0e-138">Suivant de hello utilisez commande toobuild hello **appareil simulé** application et recherchez les erreurs :</span><span class="sxs-lookup"><span data-stu-id="96f0e-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="96f0e-139">Recevoir une notification de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="96f0e-139">Receive a file upload notification</span></span>

<span data-ttu-id="96f0e-140">Dans cette section, vous allez créer une application console Java qui reçoit des messages de notification de chargement de fichiers envoyés par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="96f0e-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="96f0e-141">Vous devez hello **iothubowner** chaîne de connexion de votre toocomplete IoT Hub de cette section.</span><span class="sxs-lookup"><span data-stu-id="96f0e-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="96f0e-142">Vous trouverez la chaîne de connexion hello Bonjour [portail Azure](https://portal.azure.com/) sur hello **la stratégie d’accès partagé** panneau.</span><span class="sxs-lookup"><span data-stu-id="96f0e-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="96f0e-143">Créez un projet Maven appelé **-fichier-téléchargement-notification de lecture** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="96f0e-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="96f0e-144">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="96f0e-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="96f0e-145">À l’invite de commandes, accédez toohello nouvelle `read-file-upload-notification` dossier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="96f0e-146">À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `read-file-upload-notification` dossier et ajoutez hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="96f0e-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="96f0e-147">Ajout de la dépendance de hello vous permet de toouse hello **iothub-java-service-client** package dans toocommunicate de votre application avec votre service de hub IoT :</span><span class="sxs-lookup"><span data-stu-id="96f0e-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="96f0e-148">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="96f0e-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="96f0e-149">Enregistrez et fermez hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="96f0e-150">À l’aide d’un éditeur de texte, ouvrez hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="96f0e-151">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="96f0e-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="96f0e-152">Ajouter hello suivant des variables de niveau classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="96f0e-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="96f0e-153">tooprint des informations sur la console de toohello de téléchargement de fichier de hello, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="96f0e-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
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

1. <span data-ttu-id="96f0e-154">thread de hello toostart qui écoute les notifications de téléchargement de fichier, ajoutez hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="96f0e-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="96f0e-155">Enregistrez et fermez hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="96f0e-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="96f0e-156">Suivant de hello utilisez commande toobuild hello **-fichier-téléchargement-notification de lecture** application et recherchez les erreurs :</span><span class="sxs-lookup"><span data-stu-id="96f0e-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="96f0e-157">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="96f0e-157">Run hello applications</span></span>

<span data-ttu-id="96f0e-158">Vous êtes maintenant prêt toorun les applications hello.</span><span class="sxs-lookup"><span data-stu-id="96f0e-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="96f0e-159">À l’invite de commande Bonjour `read-file-upload-notification` dossier, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="96f0e-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="96f0e-160">À l’invite de commande Bonjour `simulated-device` dossier, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="96f0e-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="96f0e-161">Hello capture d’écran suivante illustre la hello sortie de hello **appareil simulé** application :</span><span class="sxs-lookup"><span data-stu-id="96f0e-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Sortie de l’application simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="96f0e-163">Hello capture d’écran suivante illustre la hello sortie de hello **-fichier-téléchargement-notification de lecture** application :</span><span class="sxs-lookup"><span data-stu-id="96f0e-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Sortie de l’application read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="96f0e-165">Vous pouvez utiliser hello tooview portail hello téléchargé fichier dans le conteneur de stockage hello que vous avez configuré :</span><span class="sxs-lookup"><span data-stu-id="96f0e-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![Fichier chargé](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="96f0e-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="96f0e-167">Next steps</span></span>

<span data-ttu-id="96f0e-168">Dans ce didacticiel, vous avez appris comment toouse hello téléchargement fonctionnalités du IoT Hub toosimplify fichier télécharge à partir d’appareils.</span><span class="sxs-lookup"><span data-stu-id="96f0e-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="96f0e-169">Vous pouvez poursuivre scénarios et fonctionnalités de hub IoT tooexplore hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="96f0e-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="96f0e-170">[Créer un IoT Hub par programme][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="96f0e-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="96f0e-171">[Introduction tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="96f0e-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="96f0e-172">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="96f0e-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="96f0e-173">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="96f0e-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="96f0e-174">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="96f0e-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[centre de développement Azure IoT]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


