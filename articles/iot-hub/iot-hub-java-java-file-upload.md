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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Télécharger des fichiers à partir de votre appareil toohello cloud avec IoT Hub

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Ce didacticiel s’appuie sur le code hello Bonjour [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-java-java-c2d.md) tooshow didacticiel vous comment toouse hello [fichier capacités de téléchargement de IoT Hub](iot-hub-devguide-file-upload.md) tooupload un fichier trop[ Stockage d’objets blob Azure](../storage/index.md). didacticiel de Hello vous montre comment procéder pour :

- Fournissez en toute sécurité à un appareil un URI d’objet blob Azure pour le chargement d’un fichier.
- Utilisez hello IoT Hub fichier téléchargement notifications tootrigger traitement du fichier hello dans votre principal de l’application.

Hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) et [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-java-java-c2d.md) didacticiels montrent hello appareil-à-cloud et cloud-à-appareil messagerie fonctionnalités de base d’IoT Hub. Hello [messages processus appareil-à-Cloud](iot-hub-java-java-process-d2c.md) didacticiel décrit une façon tooreliably stocker appareil-à-cloud les messages dans le stockage blob Azure. Toutefois, dans certains scénarios vous ne peut pas mapper facilement les données de hello que vos appareils envoient en messages appareil-à-cloud relativement faible hello qui accepte une IoT Hub. Par exemple :

* Fichiers volumineux qui contiennent des images
* Vidéos
* Données de vibration échantillonnées à une fréquence élevée
* Un certain type de données prétraitées.

Ces fichiers sont généralement traitées dans le cloud hello à l’aide des outils tels que par lots [Azure Data Factory](../data-factory/index.md) ou hello [Hadoop](../hdinsight/index.md) pile. Lorsque vous avez besoin des fichiers tooupland à partir d’un appareil, vous pouvez toujours utiliser sécurité de hello et la fiabilité de IoT Hub.

À la fin de hello de ce didacticiel, vous exécutez deux applications de console Java :

* **APPAREIL simulé**, une version modifiée de l’application hello créée dans le didacticiel de hello [messages envoi Cloud-à-appareil avec IoT Hub]. Cette application télécharge une toostorage de fichier à l’aide d’un URI SAS fournie par votre hub IoT.
* **read-file-upload-notification**, qui reçoit les notifications de chargement de fichiers envoyées par le hub IoT.

> [!NOTE]
> IoT Hub prend en charge de nombreuses plateformes d’appareils et de nombreux langages (notamment C, .NET et JavaScript) par le biais des kits Azure IoT device SDK. Consultez toohello [centre de développement Azure IoT] pour obtenir des instructions sur la façon de tooconnect votre tooAzure appareil IoT Hub.

toocomplete ce didacticiel, vous devez hello suivant :

* Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un compte Azure actif. (Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Charger un fichier à partir d’une application d’appareil

Dans cette section, vous modifiez l’application d’appareil hello vous avez créé dans [envoyer des messages Cloud-à-appareil avec IoT Hub](iot-hub-java-java-c2d.md) tooupload un concentrateur de tooIoT de fichier.

1. Copier un toohello de fichier image `simulated-device` dossier et renommez-le `myimage.png`.

1. À l’aide d’un éditeur de texte, ouvrez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.

1. Ajouter hello déclaration de variable toohello **application** classe :

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess messages de rappel d’état du téléchargement de fichiers, ajoutez hello imbriqués classe toohello **application** classe :

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload images tooIoT Hub, ajouter hello suivant de méthode toohello **application** tooupload de classe images tooIoT Hub :

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

1. Modifier hello **principal** hello toocall de méthode **uploadFile** illustré hello suivant extrait la méthode :

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

1. Suivant de hello utilisez commande toobuild hello **appareil simulé** application et recherchez les erreurs :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Recevoir une notification de téléchargement de fichier

Dans cette section, vous allez créer une application console Java qui reçoit des messages de notification de chargement de fichiers envoyés par IoT Hub.

Vous devez hello **iothubowner** chaîne de connexion de votre toocomplete IoT Hub de cette section. Vous trouverez la chaîne de connexion hello Bonjour [portail Azure](https://portal.azure.com/) sur hello **la stratégie d’accès partagé** panneau.

1. Créez un projet Maven appelé **-fichier-téléchargement-notification de lecture** à l’aide de hello, la commande suivante à l’invite suivante. Il s’agit d’une commande unique et longue :

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. À l’invite de commandes, accédez toohello nouvelle `read-file-upload-notification` dossier.

1. À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `read-file-upload-notification` dossier et ajoutez hello suivant dépendance toohello **dépendances** nœud. Ajout de la dépendance de hello vous permet de toouse hello **iothub-java-service-client** package dans toocommunicate de votre application avec votre service de hub IoT :

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Enregistrez et fermez hello `pom.xml` fichier.

1. À l’aide d’un éditeur de texte, ouvrez hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` fichier.

1. Ajoutez hello suivant **importer** fichier de toohello instructions :

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Ajouter hello suivant des variables de niveau classe toohello **application** classe :

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint des informations sur la console de toohello de téléchargement de fichier de hello, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :

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

1. thread de hello toostart qui écoute les notifications de téléchargement de fichier, ajoutez hello suivant code toohello **principal** méthode :

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

1. Enregistrez et fermez hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` fichier.

1. Suivant de hello utilisez commande toobuild hello **-fichier-téléchargement-notification de lecture** application et recherchez les erreurs :

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Exécuter des applications de hello

Vous êtes maintenant prêt toorun les applications hello.

À l’invite de commande Bonjour `read-file-upload-notification` dossier, exécutez hello de commande suivante :

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

À l’invite de commande Bonjour `simulated-device` dossier, exécutez hello de commande suivante :

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Hello capture d’écran suivante illustre la hello sortie de hello **appareil simulé** application :

![Sortie de l’application simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

Hello capture d’écran suivante illustre la hello sortie de hello **-fichier-téléchargement-notification de lecture** application :

![Sortie de l’application read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

Vous pouvez utiliser hello tooview portail hello téléchargé fichier dans le conteneur de stockage hello que vous avez configuré :

![Fichier chargé](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris comment toouse hello téléchargement fonctionnalités du IoT Hub toosimplify fichier télécharge à partir d’appareils. Vous pouvez poursuivre scénarios et fonctionnalités de hub IoT tooexplore hello suivant des articles :

* [Créer un IoT Hub par programme][lnk-create-hub]
* [Introduction tooC SDK][lnk-c-sdk]
* [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]

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


