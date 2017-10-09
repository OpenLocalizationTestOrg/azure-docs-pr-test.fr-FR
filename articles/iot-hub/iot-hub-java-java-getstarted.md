---
title: aaaGet en main Azure IoT Hub (Java) | Documents Microsoft
description: "Découvrez comment toosend appareil-à-cloud messages tooAzure IoT Hub à l’aide de kits de développement logiciel IoT pour Java. Créer appareil simulé et tooregister des applications de service de votre appareil, envoyer des messages et lire les messages de hub IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="17c25-104">Connectez votre concentrateur de IoT tooyour périphérique à l’aide de Java</span><span class="sxs-lookup"><span data-stu-id="17c25-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="17c25-105">À la fin de hello de ce didacticiel, vous avez trois applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="17c25-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="17c25-106">**identité du périphérique créer**, ce qui crée une identité d’appareil et clé de sécurité associés tooconnect votre application.</span><span class="sxs-lookup"><span data-stu-id="17c25-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="17c25-107">**en lecture-d2c-messages**, qui affiche la télémétrie hello envoyée par votre application.</span><span class="sxs-lookup"><span data-stu-id="17c25-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="17c25-108">**APPAREIL simulé**, qui se connecte tooyour IoT hub avec l’identité de l’appareil hello créée précédemment et envoie un message de télémétrie chaque seconde à l’aide de hello le protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="17c25-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="17c25-109">article de Hello [kits de développement logiciel Azure IoT] [ lnk-hub-sdks] fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild toorun de deux applications sur les périphériques et votre principal de la solution.</span><span class="sxs-lookup"><span data-stu-id="17c25-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="17c25-110">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="17c25-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="17c25-111">Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="17c25-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="17c25-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="17c25-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="17c25-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="17c25-113">An active Azure account.</span></span> <span data-ttu-id="17c25-114">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="17c25-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="17c25-115">Dans la dernière étape, prenez note de hello **clé primaire** valeur.</span><span class="sxs-lookup"><span data-stu-id="17c25-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="17c25-116">Puis cliquez sur **points de terminaison** et hello **événements** intégré.</span><span class="sxs-lookup"><span data-stu-id="17c25-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="17c25-117">Sur hello **propriétés** panneau, notez hello **nom du concentrateur d’événements compatibles** et hello **point de terminaison de Hub d’événements compatibles** adresse.</span><span class="sxs-lookup"><span data-stu-id="17c25-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="17c25-118">Ces trois valeurs sont nécessaires pour créer votre application **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="17c25-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Panneau de messagerie IoT Hub du portail Azure][6]

<span data-ttu-id="17c25-120">Votre IoT Hub est maintenant créé.</span><span class="sxs-lookup"><span data-stu-id="17c25-120">You have now created your IoT hub.</span></span> <span data-ttu-id="17c25-121">Vous avez hello nom d’hôte IoT Hub, chaîne de connexion de IoT Hub, IoT Hub Primary Key, nom du concentrateur d’événements compatibles et le point de terminaison de Hub d’événements compatibles vous devez toocomplete ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="17c25-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="17c25-122">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="17c25-122">Create a device identity</span></span>
<span data-ttu-id="17c25-123">Dans cette section, vous créez une application de console Java qui crée une identité d’appareil dans le Registre des identités hello dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17c25-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="17c25-124">Un appareil ne peut pas se connecter à tooIoT concentrateur sauf si elle possède une entrée dans le Registre des identités hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="17c25-125">Pour plus d’informations, consultez hello **Registre des identités** section Hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="17c25-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="17c25-126">Lorsque vous exécutez cette application console, il génère un ID d’appareil unique et clé que votre appareil peut utiliser tooidentify lui-même lorsqu’il envoie l’appareil-à-cloud messages tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="17c25-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="17c25-127">Créez un dossier vide appelé iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="17c25-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="17c25-128">Dans le dossier d’iot-java-get-started hello, créez un projet de Maven appelé **identité du périphérique créer** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="17c25-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="17c25-129">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="17c25-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="17c25-130">Votre invite de commandes, accédez à dossier d’identité du périphérique créer toohello.</span><span class="sxs-lookup"><span data-stu-id="17c25-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="17c25-131">À l’aide d’un éditeur de texte, ouvrez le fichier de pom.xml de hello dans le dossier d’identité du périphérique créer hello et ajouter hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="17c25-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="17c25-132">Cette dépendance permet de vous toouse hello iot-service-package du client dans votre application :</span><span class="sxs-lookup"><span data-stu-id="17c25-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="17c25-133">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="17c25-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="17c25-134">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="17c25-135">À l’aide d’un éditeur de texte, d’ouvrir le fichier de create-device-identity\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="17c25-136">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="17c25-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="17c25-137">Ajouter hello suivant des variables de niveau classe toohello **application** classe, en remplaçant **{yourhubconnectionstring}** avec hello valeur votre indiqués précédemment :</span><span class="sxs-lookup"><span data-stu-id="17c25-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="17c25-138">Modifier la signature hello Hello **principal** méthode tooinclude hello exceptions comme suit :</span><span class="sxs-lookup"><span data-stu-id="17c25-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="17c25-139">Ajouter hello après le code en tant que corps hello Hello **principal** (méthode).</span><span class="sxs-lookup"><span data-stu-id="17c25-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="17c25-140">Si ce n’est déjà fait, ce code crée un appareil appelé *javadevice* dans votre registre d’identités IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="17c25-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="17c25-141">Il affiche ensuite l’ID de périphérique hello et la clé dont vous avez besoin ultérieurement :</span><span class="sxs-lookup"><span data-stu-id="17c25-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="17c25-142">Enregistrez et fermez le fichier de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="17c25-143">toobuild hello **identité du périphérique créer** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’identité du périphérique créer hello suivante :</span><span class="sxs-lookup"><span data-stu-id="17c25-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="17c25-144">toorun hello **identité du périphérique créer** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’identité du périphérique créer hello suivante :</span><span class="sxs-lookup"><span data-stu-id="17c25-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="17c25-145">Prenez note de hello **ID de périphérique** et **clé de périphérique**.</span><span class="sxs-lookup"><span data-stu-id="17c25-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="17c25-146">Vous avez besoin de ces valeurs lorsque vous créez une application qui se connecte tooIoT Hub en tant que périphérique.</span><span class="sxs-lookup"><span data-stu-id="17c25-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="17c25-147">Hello Registre des identités IoT Hub stocke uniquement toohello IoT hub de périphérique identités tooenable un accès sécurisé.</span><span class="sxs-lookup"><span data-stu-id="17c25-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="17c25-148">Il stocke toouse ID et les clés de périphérique en tant qu’informations d’identification de sécurité et d’un indicateur activée/désactivée que vous pouvez utiliser l’accès toodisable pour un périphérique.</span><span class="sxs-lookup"><span data-stu-id="17c25-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="17c25-149">Si votre application doit toostore autres métadonnées spécifiques au périphérique, elle doit utiliser un magasin spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="17c25-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="17c25-150">Pour plus d’informations, consultez hello [guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="17c25-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="17c25-151">Recevoir des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="17c25-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="17c25-152">Dans cette section, vous allez créer une application console Java qui lit les messages des appareils vers le cloud dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="17c25-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="17c25-153">Un hub IoT expose un [concentrateur d’événements][lnk-event-hubs-overview]-point de terminaison compatible tooenable vous tooread les messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="17c25-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="17c25-154">tookeep les choses simples, ce didacticiel crée un lecteur de base qui n’est pas approprié pour un déploiement d’un débit élevé.</span><span class="sxs-lookup"><span data-stu-id="17c25-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="17c25-155">Hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel vous montre comment les messages tooprocess appareil-à-cloud à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="17c25-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="17c25-156">Hello [prise en main les concentrateurs d’événements] [ lnk-eventhubs-tutorial] didacticiel fournit des informations supplémentaires sur le tooprocess des messages à partir de concentrateurs d’événements et est applicable toohello points de terminaison de Hub IoT Hub événement compatible.</span><span class="sxs-lookup"><span data-stu-id="17c25-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="17c25-157">Hello point de terminaison de Hub d’événements compatibles pour la lecture des messages appareil-à-cloud toujours utilise le protocole AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="17c25-158">Dans le dossier d’iot-java-get-started hello que vous avez créé dans hello *créer une identité d’appareil* section, créez un projet Maven appelé **en lecture-d2c-messages** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="17c25-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="17c25-159">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="17c25-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="17c25-160">Votre invite de commandes, accédez à dossier en lecture-d2c-messages de toohello.</span><span class="sxs-lookup"><span data-stu-id="17c25-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="17c25-161">À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier de lecture-d2c-messages hello et ajouter hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="17c25-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="17c25-162">Cette dépendance permet toouse du package eventhubs-client hello dans tooread de votre application à partir du point de terminaison de Hub d’événements compatibles hello :</span><span class="sxs-lookup"><span data-stu-id="17c25-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="17c25-163">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="17c25-164">À l’aide d’un éditeur de texte, d’ouvrir le fichier de read-d2c-messages\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="17c25-165">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="17c25-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="17c25-166">Ajouter hello suivant toohello de variable de niveau classe **application** classe.</span><span class="sxs-lookup"><span data-stu-id="17c25-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="17c25-167">Remplacez **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, et **{youreventhubcompatiblename}** avec les valeurs hello notées précédemment :</span><span class="sxs-lookup"><span data-stu-id="17c25-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="17c25-168">Ajoutez hello suivant **receiveMessages** méthode toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="17c25-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="17c25-169">Cette méthode crée un **EventHubClient** tooconnect toohello compatible concentrateur d’événements point de terminaison d’instance et puis crée de façon asynchrone un **PartitionReceiver** tooread d’instance à partir d’un concentrateur d’événements partition.</span><span class="sxs-lookup"><span data-stu-id="17c25-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="17c25-170">Il en continu et imprime les détails du message hello jusqu'à l’arrêt de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="17c25-171">Cette méthode utilise un filtre lorsqu’il crée le récepteur de hello afin que hello récepteur lit uniquement les messages envoyés tooIoT Hub après que le récepteur de hello commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="17c25-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="17c25-172">Cette technique est utile dans un environnement de test afin de voir l’ensemble actuel de hello de messages.</span><span class="sxs-lookup"><span data-stu-id="17c25-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="17c25-173">Dans un environnement de production, votre code doit vous assurer qu’elle traite tous les messages hello - pour plus d’informations, consultez hello [comment tooprocess les messages appareil-à-cloud IoT Hub] [ lnk-process-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="17c25-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="17c25-174">Modifier la signature hello Hello **principal** méthode tooinclude hello exception comme suit :</span><span class="sxs-lookup"><span data-stu-id="17c25-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="17c25-175">Ajouter hello suivant code toohello **principal** méthode Bonjour **application** classe.</span><span class="sxs-lookup"><span data-stu-id="17c25-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="17c25-176">Ce code crée deux de hello **EventHubClient** et **PartitionReceiver** instances et vous permet de tooclose hello application lorsque vous avez terminé le traitement des messages :</span><span class="sxs-lookup"><span data-stu-id="17c25-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="17c25-177">Ce code suppose que vous avez créé votre hub IoT dans la couche de hello F1 (gratuit).</span><span class="sxs-lookup"><span data-stu-id="17c25-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="17c25-178">Un IoT Hub gratuit comporte deux partitions nommées « 0 » et « 1 ».</span><span class="sxs-lookup"><span data-stu-id="17c25-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="17c25-179">Enregistrez et fermez le fichier de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="17c25-180">toobuild hello **en lecture-d2c-messages** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier de lecture-d2c-messages hello suivante :</span><span class="sxs-lookup"><span data-stu-id="17c25-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="17c25-181">Créer une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="17c25-181">Create a device app</span></span>
<span data-ttu-id="17c25-182">Dans cette section, vous créez une application console Java qui simule un appareil qui envoie l’IoT hub tooan de messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="17c25-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="17c25-183">Dans le dossier d’iot-java-get-started hello que vous avez créé dans hello *créer une identité d’appareil* section, créez un projet Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="17c25-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="17c25-184">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="17c25-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="17c25-185">Votre invite de commandes, accédez à dossier d’appareil simulé toohello.</span><span class="sxs-lookup"><span data-stu-id="17c25-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="17c25-186">À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier d’appareil simulé hello et ajouter hello suivant dépendances toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="17c25-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="17c25-187">Cette dépendance permet de vous toouse hello iothub-java-package client dans votre toocommunicate d’application avec votre IoT hub et la tooserialize tooJSON d’objets Java :</span><span class="sxs-lookup"><span data-stu-id="17c25-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="17c25-188">Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="17c25-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="17c25-189">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="17c25-190">À l’aide d’un éditeur de texte, d’ouvrir le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="17c25-191">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="17c25-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="17c25-192">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="17c25-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="17c25-193">En remplaçant **{youriothubname}** avec votre nom de hub IoT, et **{yourdevicekey}** avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="17c25-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="17c25-194">Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet.</span><span class="sxs-lookup"><span data-stu-id="17c25-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="17c25-195">Vous pouvez utiliser soit toocommunicate de protocole hello MQTT, AMQP ou HTTP avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="17c25-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="17c25-196">Ajoutez suit hello imbriqués **TelemetryDataPoint** classe à l’intérieur de hello **application** classe les données de télémétrie hello toospecify votre appareil envoie tooyour IoT hub :</span><span class="sxs-lookup"><span data-stu-id="17c25-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="17c25-197">Ajoutez suit hello imbriqués **EventCallback** classe à l’intérieur de hello **application** état classe toodisplay hello accusé de réception qui hello IoT hub retourne lorsqu’il traite un message à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="17c25-198">Cette méthode signale également thread principal de hello dans l’application hello hello message a été traité :</span><span class="sxs-lookup"><span data-stu-id="17c25-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="17c25-199">Ajoutez suit hello imbriqués **MessageSender** classe à l’intérieur de hello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="17c25-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="17c25-200">Hello **exécuter** méthode dans cette classe génère tooyour IoT hub pour exemple télémétrie données toosend et attend un accusé de réception avant d’envoyer le message de type hello suivant :</span><span class="sxs-lookup"><span data-stu-id="17c25-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    <span data-ttu-id="17c25-201">Cette méthode envoie un nouveau message de l’appareil-à-cloud une seconde après que le précédent message de type hello accuse réception de hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="17c25-202">message de salutation contient un objet JSON sérialisé avec hello deviceId et généré de façon aléatoire les numéros toosimulate un capteur de température et un capteur humidité.</span><span class="sxs-lookup"><span data-stu-id="17c25-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="17c25-203">Remplacez hello **principal** méthode avec hello suivant le code qui crée un hub IoT de tooyour thread toosend messages appareil-à-cloud :</span><span class="sxs-lookup"><span data-stu-id="17c25-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="17c25-204">Enregistrez et fermez le fichier de App.java hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="17c25-205">toobuild hello **appareil simulé** application à l’aide de Maven, exécutez hello commande à l’invite de commandes hello dans le dossier d’appareil simulé hello suivante :</span><span class="sxs-lookup"><span data-stu-id="17c25-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="17c25-206">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="17c25-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="17c25-207">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="17c25-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="17c25-208">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="17c25-208">Run hello apps</span></span>

<span data-ttu-id="17c25-209">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="17c25-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="17c25-210">À une invite de commandes dans le dossier en lecture-d2c de hello, exécutez hello suivant toobegin commande analyse la première partition de hello dans votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="17c25-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Messages appareil-à-cloud toomonitor d’application du service Java IoT Hub][7]

2. <span data-ttu-id="17c25-212">À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande envoi tooyour IoT hub de télémétrie des données :</span><span class="sxs-lookup"><span data-stu-id="17c25-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Messages appareil-à-cloud toosend Java IoT Hub appareil application][8]

3. <span data-ttu-id="17c25-214">Hello **utilisation** vignette Bonjour [portail Azure] [ lnk-portal] affiche hello le nombre de messages envoyés toohello IoT hub :</span><span class="sxs-lookup"><span data-stu-id="17c25-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portail d’utilisation vignette affichage du nombre de messages envoyés tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="17c25-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17c25-216">Next steps</span></span>
<span data-ttu-id="17c25-217">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="17c25-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="17c25-218">Vous avez utilisé ce périphérique identité tooenable hello appareil application toosend messages appareil-à-cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17c25-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="17c25-219">Vous avez créé également une application qui affiche les messages hello reçus par IoT hub de hello.</span><span class="sxs-lookup"><span data-stu-id="17c25-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="17c25-220">toocontinue mise en route avec IoT Hub et tooexplore autres scénarios IoT, consultez :</span><span class="sxs-lookup"><span data-stu-id="17c25-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="17c25-221">[Connexion de votre appareil][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="17c25-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="17c25-222">[Prise en main de la gestion d’appareils][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="17c25-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="17c25-223">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)</span><span class="sxs-lookup"><span data-stu-id="17c25-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="17c25-224">toolearn tooextend vos messages IoT solution et des processus de périphérique dans le cloud à grande échelle, voir hello [traiter les messages appareil-à-cloud] [ lnk-process-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="17c25-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
