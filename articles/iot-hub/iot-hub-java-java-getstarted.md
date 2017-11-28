---
title: Prise en main avec Azure IoT Hub pour Java | Microsoft Docs
description: "Découvrez comment envoyer des messages appareil-vers-cloud à Azure IoT Hub à l’aide des kits SDK Azure IoT pour Java. Créez un appareil simulé et des applications de service pour inscrire votre appareil, envoyer des messages et lire des messages d’IoT Hub."
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
ms.openlocfilehash: 707356a49970bcd76a55ee1b8a6fbddf6a6ba390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a><span data-ttu-id="6e25f-104">Connecter votre appareil à votre IoT Hub à l’aide de Java</span><span class="sxs-lookup"><span data-stu-id="6e25f-104">Connect your device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="6e25f-105">À la fin de ce didacticiel, vous disposerez de trois applications console Java :</span><span class="sxs-lookup"><span data-stu-id="6e25f-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="6e25f-106">**create-device-identity**, qui crée une identité d’appareil et une clé de sécurité associée pour connecter votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="6e25f-106">**create-device-identity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="6e25f-107">**read-d2c-messages**, qui affiche les données de télémétrie envoyées par votre application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="6e25f-107">**read-d2c-messages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="6e25f-108">**simulated-device**, qui se connecte à votre IoT Hub avec l’identité d’appareil créée précédemment et envoie un message de télémétrie chaque seconde en utilisant le protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="6e25f-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="6e25f-109">L’article [Kits de développement logiciel (SDK) Azure IoT][lnk-hub-sdks] fournit des informations sur les kits de développement logiciel Azure IoT que vous pouvez utiliser pour générer les deux applications qui s’exécutent sur les appareils et sur le serveur de solution principal.</span><span class="sxs-lookup"><span data-stu-id="6e25f-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>

<span data-ttu-id="6e25f-110">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6e25f-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6e25f-111">La version la plus récente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="6e25f-111">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="6e25f-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="6e25f-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="6e25f-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6e25f-113">An active Azure account.</span></span> <span data-ttu-id="6e25f-114">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.)</span><span class="sxs-lookup"><span data-stu-id="6e25f-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="6e25f-115">Dans la dernière étape, prenez note de la valeur de la **Clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-115">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="6e25f-116">Cliquez sur **Points de terminaison**, puis sur le point de terminaison intégré **Événements**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-116">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="6e25f-117">Dans le panneau **Propriétés**, notez le **Nom compatible avec le hub d’événements** et l’**adresse du point de terminaison compatible avec le hub d’événements**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-117">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="6e25f-118">Ces trois valeurs sont nécessaires pour créer votre application **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Panneau de messagerie IoT Hub du portail Azure][6]

<span data-ttu-id="6e25f-120">Votre IoT Hub est maintenant créé.</span><span class="sxs-lookup"><span data-stu-id="6e25f-120">You have now created your IoT hub.</span></span> <span data-ttu-id="6e25f-121">Vous disposez du nom d’hôte IoT Hub, de la chaîne de connexion IoT Hub, de la clé primaire IoT Hub, du nom compatible avec le hub d’événements et du point de terminaison compatible avec le hub d’événements, dont vous avez besoin pour terminer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6e25f-121">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="6e25f-122">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="6e25f-122">Create a device identity</span></span>
<span data-ttu-id="6e25f-123">Dans cette section, vous allez créer une application console Java qui crée une identité d’appareil dans le registre d’identités de votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-123">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="6e25f-124">Un appareil ne peut pas se connecter à IoT Hub, à moins de posséder une entrée dans le registre des identités.</span><span class="sxs-lookup"><span data-stu-id="6e25f-124">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="6e25f-125">Reportez-vous à la section **Registre d’identité** du [Guide du développeur IoT Hub][lnk-devguide-identity] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6e25f-125">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="6e25f-126">Lorsque vous exécutez cette application de console, elle génère un ID d’appareil et une clé uniques que votre appareil peut utiliser pour s’identifier pour lorsqu’il envoie des messages appareil-à-cloud à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-126">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="6e25f-127">Créez un dossier vide appelé iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="6e25f-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="6e25f-128">Dans le dossier iot-java-get-started, créez un projet Maven nommé **create-device-identity** en entrant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="6e25f-128">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="6e25f-129">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="6e25f-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="6e25f-130">À l’invite de commandes, accédez au dossier create-device-identity.</span><span class="sxs-lookup"><span data-stu-id="6e25f-130">At your command prompt, navigate to the create-device-identity folder.</span></span>

3. <span data-ttu-id="6e25f-131">Dans un éditeur de texte, ouvrez le fichier pom.xml situé dans le dossier create-device-identity et ajoutez la dépendance suivante au nœud **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="6e25f-131">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="6e25f-132">Cette dépendance permet d’utiliser le package client du service IoT dans votre application :</span><span class="sxs-lookup"><span data-stu-id="6e25f-132">This dependency enables you to use the iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6e25f-133">Vous pouvez rechercher la dernière version de **iot-service-client** avec la [recherche Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="6e25f-133">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="6e25f-134">Enregistrez et fermez le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="6e25f-134">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="6e25f-135">À l’aide d’un éditeur de texte, ouvrez le fichier create-device-identity\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="6e25f-135">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="6e25f-136">Ajoutez les instructions **import** suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="6e25f-136">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="6e25f-137">Ajoutez les variables de niveau classe suivantes à la classe **App**, en remplaçant **{yourhubconnectionstring}** par la valeur que vous avez notée précédemment :</span><span class="sxs-lookup"><span data-stu-id="6e25f-137">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="6e25f-138">Modifiez la signature de la méthode **main** pour inclure les exceptions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e25f-138">Modify the signature of the **main** method to include the exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="6e25f-139">Ajoutez le code suivant comme corps de la méthode **main** .</span><span class="sxs-lookup"><span data-stu-id="6e25f-139">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="6e25f-140">Si ce n’est déjà fait, ce code crée un appareil appelé *javadevice* dans votre registre d’identités IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="6e25f-141">Il affiche ensuite l’ID et la clé de l’appareil dont vous aurez besoin par la suite :</span><span class="sxs-lookup"><span data-stu-id="6e25f-141">It then displays the device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
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
      // If the device already exists.
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

10. <span data-ttu-id="6e25f-142">Enregistrez et fermez le fichier App.java.</span><span class="sxs-lookup"><span data-stu-id="6e25f-142">Save and close the App.java file.</span></span>

11. <span data-ttu-id="6e25f-143">Pour générer l’application **create-device-identity** à l’aide de Maven, exécutez la commande suivante à l’invite de commandes dans le dossier create-device-identity :</span><span class="sxs-lookup"><span data-stu-id="6e25f-143">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="6e25f-144">Pour exécuter l’application **create-device-identity** à l’aide de Maven, exécutez la commande suivante à l’invite de commandes dans le dossier create-device-identity :</span><span class="sxs-lookup"><span data-stu-id="6e25f-144">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="6e25f-145">Prenez note de **l’ID de l’appareil** et de la **clé de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-145">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="6e25f-146">Vous aurez besoin de ces valeurs ultérieurement lorsque vous créerez une application qui se connecte à IoT Hub en tant qu’appareil.</span><span class="sxs-lookup"><span data-stu-id="6e25f-146">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="6e25f-147">Le registre des identités IoT Hub stocke uniquement les identités des appareils pour permettre un accès sécurisé à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-147">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="6e25f-148">Il stocke les ID et les clés des appareils à utiliser comme informations d’identification de sécurité, et un indicateur activé/désactivé que vous pouvez utiliser pour désactiver l’accès pour un appareil individuel.</span><span class="sxs-lookup"><span data-stu-id="6e25f-148">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="6e25f-149">Si votre application a besoin de stocker d’autres métadonnées spécifiques aux appareils, elle doit utiliser un magasin spécifique aux applications.</span><span class="sxs-lookup"><span data-stu-id="6e25f-149">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="6e25f-150">Pour plus d’informations, reportez-vous au [Guide du développeur IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="6e25f-150">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="6e25f-151">Recevoir des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="6e25f-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="6e25f-152">Dans cette section, vous allez créer une application console Java qui lit les messages des appareils vers le cloud dans l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="6e25f-153">Un IoT Hub expose un point de terminaison compatible avec les [hubs d’événements][lnk-event-hubs-overview] pour vous permettre de lire les messages des appareils vers le cloud.</span><span class="sxs-lookup"><span data-stu-id="6e25f-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="6e25f-154">Pour simplifier les choses, ce didacticiel crée un lecteur de base qui ne convient pas dans le cas d’un déploiement à débit élevé.</span><span class="sxs-lookup"><span data-stu-id="6e25f-154">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="6e25f-155">Le didacticiel [Traiter les messages des appareils vers le cloud IoT Hub][lnk-process-d2c-tutorial] vous indique comment traiter les messages Appareil vers cloud à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="6e25f-155">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="6e25f-156">Le didacticiel [Prise en main des hubs d’événements][lnk-eventhubs-tutorial] fournit des informations complémentaires sur la façon de traiter les messages à partir d’Event Hubs et s’applique aux points de terminaison compatibles Event Hubs exposés par l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-156">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="6e25f-157">Le point de terminaison compatible Event Hub pour lire des messages de l’appareil vers le cloud utilise toujours le protocole AMQP.</span><span class="sxs-lookup"><span data-stu-id="6e25f-157">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="6e25f-158">Dans le dossier iot-java-get-started que vous avez créé à la section *Création d’une identité d’appareil*, créez un projet Maven appelé **read-d2c-messages** en entrant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="6e25f-158">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="6e25f-159">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="6e25f-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="6e25f-160">À l’invite de commandes, accédez au dossier read-d2c-messages.</span><span class="sxs-lookup"><span data-stu-id="6e25f-160">At your command prompt, navigate to the read-d2c-messages folder.</span></span>

3. <span data-ttu-id="6e25f-161">Dans un éditeur de texte, ouvrez le fichier pom.xml dans le dossier read-d2c-messages et ajoutez la dépendance suivante au nœud **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="6e25f-161">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="6e25f-162">Cette dépendance vous permet d’utiliser le package eventhubs-client dans votre application pour effectuer la lecture à partir du point de terminaison compatible Event Hub :</span><span class="sxs-lookup"><span data-stu-id="6e25f-162">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="6e25f-163">Enregistrez et fermez le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="6e25f-163">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="6e25f-164">À l’aide d’un éditeur de texte, ouvrez le fichier read-d2c-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="6e25f-164">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="6e25f-165">Ajoutez les instructions **import** suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="6e25f-165">Add the following **import** statements to the file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="6e25f-166">Ajoutez les variables de niveau classe suivantes à la classe **App** .</span><span class="sxs-lookup"><span data-stu-id="6e25f-166">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="6e25f-167">Remplacez les chaînes **{youriothubkey}**, **{youreventhubcompatibleendpoint}** et **{youreventhubcompatiblename}** par les valeurs que vous avez notées précédemment :</span><span class="sxs-lookup"><span data-stu-id="6e25f-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="6e25f-168">Ajoutez la méthode **receiveMessages** suivante à la classe **App**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-168">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="6e25f-169">Cette méthode crée une instance **EventHubClient** permettant de vous connecter au point de terminaison compatible Event Hub, puis crée une instance **PartitionReceiver** de façon asynchrone pour lire les données à partir d’une partition Event Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-169">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="6e25f-170">La méthode boucle en continu et imprime les détails du message jusqu’à ce que l’application s’arrête.</span><span class="sxs-lookup"><span data-stu-id="6e25f-170">It loops continuously and prints the message details until the app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
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
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="6e25f-171">Cette méthode utilise un filtre lorsqu’elle crée le récepteur afin que ce dernier lise uniquement les messages envoyés à l’IoT Hub une fois que le récepteur a commencé à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="6e25f-171">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="6e25f-172">Dans un environnement de test, cette technique permet de voir l’ensemble des messages en cours.</span><span class="sxs-lookup"><span data-stu-id="6e25f-172">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="6e25f-173">Dans un environnement de production, votre code doit vérifier qu’il traite la totalité des messages. Pour plus d’informations, consultez le didacticiel [Traiter les messages des appareils vers le cloud IoT Hub][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="6e25f-173">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="6e25f-174">Modifiez la signature de la méthode **main** en y incluant l’exception suivante :</span><span class="sxs-lookup"><span data-stu-id="6e25f-174">Modify the signature of the **main** method to include the exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="6e25f-175">Ajoutez le code suivant à la méthode **main** dans la classe **App**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-175">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="6e25f-176">Ce code crée les deux instances **EventHubClient** et **PartitionReceiver** et vous permet de fermer l’application lorsque vous avez terminé le traitement des messages :</span><span class="sxs-lookup"><span data-stu-id="6e25f-176">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
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
    > <span data-ttu-id="6e25f-177">Ce code repose sur l’hypothèse selon laquelle vous avez créé votre IoT Hub dans le niveau F1 (gratuit).</span><span class="sxs-lookup"><span data-stu-id="6e25f-177">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="6e25f-178">Un IoT Hub gratuit comporte deux partitions nommées « 0 » et « 1 ».</span><span class="sxs-lookup"><span data-stu-id="6e25f-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="6e25f-179">Enregistrez et fermez le fichier App.java.</span><span class="sxs-lookup"><span data-stu-id="6e25f-179">Save and close the App.java file.</span></span>

12. <span data-ttu-id="6e25f-180">Pour générer l’application **read-d2c-messages** à l’aide de Maven, exécutez la commande suivante à l’invite de commandes dans le dossier read-d2c-messages :</span><span class="sxs-lookup"><span data-stu-id="6e25f-180">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="6e25f-181">Créer une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="6e25f-181">Create a device app</span></span>
<span data-ttu-id="6e25f-182">Dans cette section, vous allez créer une application console Java qui simule un appareil envoyant des messages des appareils vers le cloud à un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="6e25f-183">Dans le dossier iot-java-get-started que vous avez créé à la section *Création d’une identité d’appareil*, créez un projet Maven appelé **simulated-device** en entrant la commande suivante à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="6e25f-183">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="6e25f-184">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="6e25f-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="6e25f-185">À l’invite de commandes, accédez au dossier simulated-device.</span><span class="sxs-lookup"><span data-stu-id="6e25f-185">At your command prompt, navigate to the simulated-device folder.</span></span>

3. <span data-ttu-id="6e25f-186">Dans un éditeur de texte, ouvrez le fichier pom.xml dans le dossier simulated-device et ajoutez les dépendances suivantes au nœud **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="6e25f-186">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="6e25f-187">Cette dépendance vous permet d’utiliser le package iothub-java-client dans votre application pour communiquer avec votre IoT Hub et pour sérialiser les objets Java dans JSON :</span><span class="sxs-lookup"><span data-stu-id="6e25f-187">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>

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
    > <span data-ttu-id="6e25f-188">Vous pouvez rechercher la dernière version de **iot-device-client** avec la [recherche Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="6e25f-188">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="6e25f-189">Enregistrez et fermez le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="6e25f-189">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="6e25f-190">À l’aide d’un éditeur de texte, ouvrez le fichier simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="6e25f-190">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="6e25f-191">Ajoutez les instructions **import** suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="6e25f-191">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="6e25f-192">Ajoutez les variables de niveau classe suivantes à la classe **App** .</span><span class="sxs-lookup"><span data-stu-id="6e25f-192">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="6e25f-193">Remplacez la chaîne **{youriothubname}** par le nom de votre IoT Hub, et **{yourdevicekey}** par la valeur clé d’appareil que vous avez générée dans la section *Création d’une identité d’appareil* :</span><span class="sxs-lookup"><span data-stu-id="6e25f-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="6e25f-194">Cet exemple d’application utilise la variable **protocol** lorsqu’il instancie un objet **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-194">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="6e25f-195">Vous pouvez utiliser le protocole MQTT, AMQP ou HTTP pour communiquer avec le IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-195">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>

8. <span data-ttu-id="6e25f-196">Ajoutez la classe imbriquée **TelemetryDataPoint** suivante dans la classe **App** pour spécifier les données de télémétrie envoyées par votre appareil à votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="6e25f-196">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>

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
9. <span data-ttu-id="6e25f-197">Ajoutez la classe imbriquée **EventCallback** suivante dans la classe **App** pour afficher l’état d’accusé de réception que l’IoT Hub renvoie lorsqu’il traite un message provenant de l’application d’appareil.</span><span class="sxs-lookup"><span data-stu-id="6e25f-197">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the device app.</span></span> <span data-ttu-id="6e25f-198">Cette méthode avertit également le thread principal de l’application lorsque le message a été traité :</span><span class="sxs-lookup"><span data-stu-id="6e25f-198">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="6e25f-199">Ajoutez la classe imbriquée **MessageSender** suivante dans la classe **App**.</span><span class="sxs-lookup"><span data-stu-id="6e25f-199">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="6e25f-200">La méthode **run** de cette classe génère un échantillon de données de télémétrie à envoyer à votre IoT Hub et attend un accusé de réception avant d’envoyer le message suivant :</span><span class="sxs-lookup"><span data-stu-id="6e25f-200">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>

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

    <span data-ttu-id="6e25f-201">Cette méthode envoie un nouveau message Appareil vers cloud une seconde après que l’IoT Hub a accusé réception du message précédent.</span><span class="sxs-lookup"><span data-stu-id="6e25f-201">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="6e25f-202">Ce message contient un objet JSON sérialisé avec l’ID de l’appareil et des nombres générés de manière aléatoire pour simuler un thermomètre et un capteur d’humidité.</span><span class="sxs-lookup"><span data-stu-id="6e25f-202">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="6e25f-203">Remplacez la méthode **main** par le code suivant qui crée un thread pour envoyer des messages des appareils vers le cloud à votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="6e25f-203">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="6e25f-204">Enregistrez et fermez le fichier App.java.</span><span class="sxs-lookup"><span data-stu-id="6e25f-204">Save and close the App.java file.</span></span>

13. <span data-ttu-id="6e25f-205">Pour générer l’application **simulated-device** à l’aide de Maven, exécutez la commande suivante à l’invite de commandes dans le dossier simulated-device :</span><span class="sxs-lookup"><span data-stu-id="6e25f-205">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="6e25f-206">Pour simplifier les choses, ce didacticiel n’implémente aucune stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="6e25f-206">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6e25f-207">Dans le code de production, vous devez mettre en œuvre des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article MSDN [Gestion des erreurs temporaires][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="6e25f-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="6e25f-208">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="6e25f-208">Run the apps</span></span>

<span data-ttu-id="6e25f-209">Vous êtes maintenant prêt à exécuter les applications.</span><span class="sxs-lookup"><span data-stu-id="6e25f-209">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="6e25f-210">À l’invite de commandes du dossier read-d2c dossier, exécutez la commande suivante pour commencer à analyser la première partition de votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="6e25f-210">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Application Java du service IoT Hub pour surveiller les messages appareil-à-cloud][7]

2. <span data-ttu-id="6e25f-212">À l’invite de commande dans le dossier simulated-device, exécutez la commande suivante pour commencer à envoyer les données de télémétrie à votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="6e25f-212">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Application Java de l’appareil IoT Hub pour envoyer les messages appareil-à-cloud][8]

3. <span data-ttu-id="6e25f-214">La vignette **Utilisation** du [portail Azure][lnk-portal] indique le nombre de messages envoyés au IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="6e25f-214">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Vignette Utilisation du portail Azure indiquant le nombre de messages envoyés à IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="6e25f-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e25f-216">Next steps</span></span>
<span data-ttu-id="6e25f-217">Dans ce didacticiel, vous avez configuré un nouveau IoT Hub dans le portail Azure, puis créé une identité d’appareil dans le registre des identités de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-217">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="6e25f-218">Vous avez utilisé cette identité d’appareil pour permettre à l’application d’appareil d’envoyer des messages appareil-à-cloud à l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-218">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="6e25f-219">Vous avez également créé une application qui affiche les messages reçus par l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e25f-219">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="6e25f-220">Pour continuer la prise en main de IoT Hub et explorer les autres scénarios IoT, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="6e25f-220">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="6e25f-221">[Connexion de votre appareil][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="6e25f-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="6e25f-222">[Prise en main de la gestion d’appareils][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="6e25f-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="6e25f-223">[Explore Azure IoT Edge architecture on Linux][lnk-iot-edge] (Découvrir l’architecture Azure IoT Edge sur Linux)</span><span class="sxs-lookup"><span data-stu-id="6e25f-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="6e25f-224">Pour découvrir comment étendre votre solution IoT et traiter les messages appareil-à-cloud à grande échelle, consultez le didacticiel [Traitement des messages appareil-à-cloud][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="6e25f-224">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
