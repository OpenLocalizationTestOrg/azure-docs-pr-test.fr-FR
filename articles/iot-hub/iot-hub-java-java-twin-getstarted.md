---
title: "Bien démarrer avec les jumeaux d’appareils Azure IoT Hub (Java) | Microsoft Docs"
description: "Guide d’utilisation des jumeaux d’appareils Azure IoT Hub pour ajouter des balises, puis utiliser une requête IoT Hub. Vous utilisez Azure IoT device SDK pour Java afin d’implémenter l’application pour appareils et Azure IoT service SDK afin d’implémenter une application de service qui ajoute les balises et exécute la requête IoT Hub."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 583cfcb9442c7be0a41aa1bc0f743bf8cf863665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="dab06-104">Bien démarrer avec les jumeaux d’appareils (Java)</span><span class="sxs-lookup"><span data-stu-id="dab06-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="dab06-105">Dans ce tutoriel, vous allez créer deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="dab06-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="dab06-106">**add-tags-query**, application principale Java qui ajoute des balises et interroge les jumeaux d’appareils.</span><span class="sxs-lookup"><span data-stu-id="dab06-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="dab06-107">**simulated-device**, application Java pour appareils qui se connecte à votre hub IoT et signale sa connectivité à l’aide d’une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="dab06-107">**simulated-device**, a Java device app that that connects to your IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="dab06-108">L’article [Kits Azure IoT SDK](iot-hub-devguide-sdks.md) fournit des informations sur les kits Azure IoT SDK que l’on peut utiliser pour générer des applications pour appareils et des applications principales.</span><span class="sxs-lookup"><span data-stu-id="dab06-108">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

<span data-ttu-id="dab06-109">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dab06-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="dab06-110">La version la plus récente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="dab06-110">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="dab06-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="dab06-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="dab06-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="dab06-112">An active Azure account.</span></span> <span data-ttu-id="dab06-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)</span><span class="sxs-lookup"><span data-stu-id="dab06-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="dab06-114">Si vous préférez créer l’identité de l’appareil par programmation, lisez la section correspondante dans l’article [Connecter un appareil à un hub IoT en Java](iot-hub-java-java-getstarted.md#create-a-device-identity).</span><span class="sxs-lookup"><span data-stu-id="dab06-114">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="dab06-115">Créer l’application de service</span><span class="sxs-lookup"><span data-stu-id="dab06-115">Create the service app</span></span>

<span data-ttu-id="dab06-116">Dans cette section, vous créez une application Java qui ajoute des métadonnées d’emplacement sous forme de balise au jumeau d’appareil associé à **myDeviceId** dans IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dab06-116">In this section, you create a Java app that adds location metadata as a tag to the device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="dab06-117">L’application interroge IoT Hub pour lister d’abord les appareils situés aux États-Unis, puis les appareils qui signalent une connexion réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="dab06-117">The app first queries IoT hub for devices located in the US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="dab06-118">Sur votre ordinateur de développement, créez un dossier vide nommé `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="dab06-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="dab06-119">Dans le dossier `iot-java-twin-getstarted`, créez un projet Maven nommé **add-tags-query** en lançant la commande ci-dessous dans votre invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="dab06-119">In the `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using the following command at your command prompt.</span></span> <span data-ttu-id="dab06-120">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="dab06-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="dab06-121">Dans votre invite de commandes, accédez au dossier `add-tags-query`.</span><span class="sxs-lookup"><span data-stu-id="dab06-121">At your command prompt, navigate to the `add-tags-query` folder.</span></span>

1. <span data-ttu-id="dab06-122">Dans un éditeur de texte, ouvrez le fichier `pom.xml` dans le dossier `add-tags-query` et ajoutez la dépendance suivante au nœud **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="dab06-122">Using a text editor, open the `pom.xml` file in the `add-tags-query` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="dab06-123">Cette dépendance vous permet d’utiliser le package **iot-service-client** dans votre application pour communiquer avec votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="dab06-123">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="dab06-124">Vous pouvez rechercher la dernière version de **iot-service-client** avec la [recherche Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="dab06-124">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="dab06-125">Ajoutez le nœud **build** suivant après le nœud **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="dab06-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="dab06-126">Cette configuration ordonne à Maven d’utiliser Java 1.8 pour générer l’application :</span><span class="sxs-lookup"><span data-stu-id="dab06-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="dab06-127">Enregistrez et fermez le fichier `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="dab06-127">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="dab06-128">Ouvrez le fichier `add-tags-query\src\main\java\com\mycompany\app\App.java` dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="dab06-128">Using a text editor, open the `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="dab06-129">Ajoutez les instructions **import** suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="dab06-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="dab06-130">Ajoutez les variables de niveau classe suivantes à la classe **App** .</span><span class="sxs-lookup"><span data-stu-id="dab06-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="dab06-131">Remplacez `{youriothubconnectionstring}` par la chaîne de connexion de votre hub IoT, que vous avez notée dans la section *Créer un hub IoT* :</span><span class="sxs-lookup"><span data-stu-id="dab06-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="dab06-132">Mettez à jour la signature de la méthode **main** pour qu’elle inclue la clause `throws` suivante :</span><span class="sxs-lookup"><span data-stu-id="dab06-132">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="dab06-133">Ajoutez le code suivant à la méthode **main** pour créer les objets **DeviceTwin** et **DeviceTwinDevice**.</span><span class="sxs-lookup"><span data-stu-id="dab06-133">Add the following code to the **main** method to create the **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="dab06-134">L’objet **DeviceTwin** gère la communication avec votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="dab06-134">The **DeviceTwin** object handles the communication with your IoT hub.</span></span> <span data-ttu-id="dab06-135">L’objet **DeviceTwinDevice** représente le jumeau de l’appareil avec ses propriétés et ses balises :</span><span class="sxs-lookup"><span data-stu-id="dab06-135">The **DeviceTwinDevice** object represents the device twin with its properties and tags:</span></span>

    ```java
    // Get the DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="dab06-136">Ajoutez le bloc `try/catch` suivant à la méthode **main** :</span><span class="sxs-lookup"><span data-stu-id="dab06-136">Add the following `try/catch` block to the **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="dab06-137">Pour mettre à jour les balises **region** et **plant** du jumeau de l’appareil, ajoutez le code suivant dans le bloc `try` :</span><span class="sxs-lookup"><span data-stu-id="dab06-137">To update the **region** and **plant** device twin tags in your device twin, add the following code in the `try` block:</span></span>

    ```java
    // Get the device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from the existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create the tags and attach them to the DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update the device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve the device twin with the tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="dab06-138">Pour interroger les jumeaux d’appareils dans IoT Hub, ajoutez le code suivant au bloc `try` après le code que vous avez ajouté à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="dab06-138">To query the device twins in IoT hub, add the following code to the `try` block after the code you added in the previous step.</span></span> <span data-ttu-id="dab06-139">Le code exécute deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="dab06-139">The code runs two queries.</span></span> <span data-ttu-id="dab06-140">Chaque requête retourne un maximum de 100 appareils :</span><span class="sxs-lookup"><span data-stu-id="dab06-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query the device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct the query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run the query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct the query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run the query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="dab06-141">Enregistrez et fermez le fichier `add-tags-query\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="dab06-141">Save and close the `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="dab06-142">Générez l’application **add-tags-query** et corrigez les erreurs éventuelles.</span><span class="sxs-lookup"><span data-stu-id="dab06-142">Build the **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="dab06-143">Dans votre invite de commandes, accédez au dossier `add-tags-query` et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dab06-143">At your command prompt, navigate to the `add-tags-query` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="dab06-144">Créer une application pour appareils</span><span class="sxs-lookup"><span data-stu-id="dab06-144">Create a device app</span></span>

<span data-ttu-id="dab06-145">Dans cette section, vous allez créer une application console Java qui définit une valeur de propriété signalée à envoyer à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dab06-145">In this section, you create a Java console app that sets a reported property value that is sent to IoT Hub.</span></span>

1. <span data-ttu-id="dab06-146">Dans le dossier `iot-java-twin-getstarted`, créez un projet Maven nommé **simulated-device** en lançant la commande suivante dans votre invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="dab06-146">In the `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="dab06-147">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="dab06-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="dab06-148">Dans votre invite de commandes, accédez au dossier `simulated-device`.</span><span class="sxs-lookup"><span data-stu-id="dab06-148">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="dab06-149">Dans un éditeur de texte, ouvrez le fichier `pom.xml` dans le dossier `simulated-device` et ajoutez les dépendances suivantes au nœud **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="dab06-149">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="dab06-150">Cette dépendance vous permet d’utiliser le package **iot-device-client** dans votre application pour communiquer avec votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="dab06-150">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="dab06-151">Vous pouvez rechercher la dernière version de **iot-device-client** avec la [recherche Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="dab06-151">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="dab06-152">Ajoutez le nœud **build** suivant après le nœud **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="dab06-152">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="dab06-153">Cette configuration ordonne à Maven d’utiliser Java 1.8 pour générer l’application :</span><span class="sxs-lookup"><span data-stu-id="dab06-153">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="dab06-154">Enregistrez et fermez le fichier `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="dab06-154">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="dab06-155">Ouvrez le fichier `simulated-device\src\main\java\com\mycompany\app\App.java` dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="dab06-155">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="dab06-156">Ajoutez les instructions **import** suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="dab06-156">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="dab06-157">Ajoutez les variables de niveau classe suivantes à la classe **App** .</span><span class="sxs-lookup"><span data-stu-id="dab06-157">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="dab06-158">Remplacez `{youriothubname}` par le nom de votre IoT Hub, et `{yourdevicekey}` par la valeur de clé de l’appareil que vous avez générée dans la section *Créer une identité d’appareil* :</span><span class="sxs-lookup"><span data-stu-id="dab06-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="dab06-159">Cet exemple d’application utilise la variable **protocol** lorsqu’il instancie un objet **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="dab06-159">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="dab06-160">Actuellement, pour utiliser les fonctionnalités des jumeaux d’appareils, vous devez utiliser le protocole MQTT.</span><span class="sxs-lookup"><span data-stu-id="dab06-160">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="dab06-161">Ajoutez le code suivant à la méthode **main** pour :</span><span class="sxs-lookup"><span data-stu-id="dab06-161">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="dab06-162">créer un client d’appareil afin de communiquer avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dab06-162">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="dab06-163">créer un objet **Device** afin de stocker les propriétés du jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="dab06-163">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object to store the device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed to " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="dab06-164">Ajoutez le code suivant à la méthode **main** pour créer une propriété signalée **connectivityType** et l’envoyer à IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="dab06-164">Add the following code to the **main** method to create a **connectivityType** reported property and send it to IoT Hub:</span></span>

    ```java
    try {
      // Open the DeviceClient and start the device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it to your IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="dab06-165">Ajoutez le code suivant à la fin de la méthode **main**.</span><span class="sxs-lookup"><span data-stu-id="dab06-165">Add the following code to the end of the **main** method.</span></span> <span data-ttu-id="dab06-166">Le fait d’attendre la touche **Entrée** laisse le temps à IoT Hub de signaler l’état des opérations du jumeau d’appareil :</span><span class="sxs-lookup"><span data-stu-id="dab06-166">Waiting for the **Enter** key allows time for IoT Hub to report the status of the device twin operations:</span></span>

    ```java
    System.out.println("Press any key to exit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="dab06-167">Enregistrez et fermez le fichier `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="dab06-167">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="dab06-168">Générez l’application **simulated-device** et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="dab06-168">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="dab06-169">Dans votre invite de commandes, accédez au dossier `simulated-device` et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dab06-169">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="dab06-170">Exécuter les applications</span><span class="sxs-lookup"><span data-stu-id="dab06-170">Run the apps</span></span>

<span data-ttu-id="dab06-171">Vous êtes maintenant prêt à exécuter les applications de console.</span><span class="sxs-lookup"><span data-stu-id="dab06-171">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="dab06-172">Dans une invite de commande, exécutez la commande suivante dans le dossier `add-tags-query` pour exécuter l’application de service **add-tags-query** :</span><span class="sxs-lookup"><span data-stu-id="dab06-172">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Application de service Java IoT Hub pour mettre à jour la valeur des balises et exécuter les requêtes des appareils](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="dab06-174">Vous pouvez constater que les balises **plant** et **region** sont ajoutées au jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="dab06-174">You can see the **plant** and **region** tags added to the device twin.</span></span> <span data-ttu-id="dab06-175">La première requête retourne votre appareil, la seconde non.</span><span class="sxs-lookup"><span data-stu-id="dab06-175">The first query returns your device, but the second does not.</span></span>

1. <span data-ttu-id="dab06-176">Dans une invite de commandes, exécutez la commande suivante dans le dossier `simulated-device` pour ajouter la propriété signalée **connectivityType** au jumeau d’appareil :</span><span class="sxs-lookup"><span data-stu-id="dab06-176">At a command prompt in the `simulated-device` folder, run the following command to add the **connectivityType** reported property to the device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Le client d’appareil ajoute la propriété signalée **connectivityType**](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="dab06-178">Dans une invite de commandes, exécutez la commande suivante dans le dossier `add-tags-query` pour exécuter de nouveau l’application de service **add-tags-query** :</span><span class="sxs-lookup"><span data-stu-id="dab06-178">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Application de service Java IoT Hub pour mettre à jour la valeur des balises et exécuter les requêtes des appareils](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="dab06-180">Maintenant que votre appareil a envoyé la propriété **connectivityType** à IoT Hub, la deuxième requête retourne votre appareil.</span><span class="sxs-lookup"><span data-stu-id="dab06-180">Now your device has sent the **connectivityType** property to IoT Hub, the second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dab06-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dab06-181">Next steps</span></span>

<span data-ttu-id="dab06-182">Dans ce didacticiel, vous avez configuré un nouveau IoT Hub dans le portail Azure, puis créé une identité d’appareil dans le registre des identités de l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dab06-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="dab06-183">Vous avez ajouté des métadonnées d’appareils sous forme de balises à partir d’une application principale et écrit une application pour appareils afin d’envoyer des informations sur la connectivité des appareils dans le jumeau d’appareil.</span><span class="sxs-lookup"><span data-stu-id="dab06-183">You added device metadata as tags from a back-end app, and wrote a device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="dab06-184">Vous avez également appris à interroger les informations du jumeau d’appareil avec le langage de requête IoT Hub de type SQL.</span><span class="sxs-lookup"><span data-stu-id="dab06-184">You also learned how to query the device twin information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="dab06-185">Utilisez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="dab06-185">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="dab06-186">Envoyez des données de télémétrie à partir d’appareils en suivant le didacticiel [Bien démarrer avec IoT Hub](iot-hub-java-java-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="dab06-186">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="dab06-187">Contrôlez les appareils de façon interactive (par exemple pour mettre en marche un ventilateur à partir d’une application contrôlée par l’utilisateur) en suivant le didacticiel [Utiliser des méthodes directes](iot-hub-java-java-direct-methods.md).</span><span class="sxs-lookup"><span data-stu-id="dab06-187">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
