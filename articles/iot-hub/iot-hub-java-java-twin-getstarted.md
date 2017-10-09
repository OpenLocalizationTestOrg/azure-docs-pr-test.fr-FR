---
title: "aaaGet main jumeaux d’appareil Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub appareil jumeaux tooadd balises, puis utilisez une requête IoT Hub. Vous utilisez du SDK de périphérique Azure IoT hello pour périphériques d’application Java tooimplement hello et hello Azure IoT service SDK pour Java tooimplement une application de service qui ajoute des balises de hello et s’exécute hello requête de IoT Hub."
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
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="2d7d1-104">Bien démarrer avec les jumeaux d’appareils (Java)</span><span class="sxs-lookup"><span data-stu-id="2d7d1-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="2d7d1-105">Dans ce tutoriel, vous allez créer deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="2d7d1-106">**add-tags-query**, application principale Java qui ajoute des balises et interroge les jumeaux d’appareils.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="2d7d1-107">**APPAREIL simulé**, une périphérique d’application Java que qui connecte tooyour IoT hub et les rapports de son état de connectivité à l’aide d’une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="2d7d1-108">article de Hello [kits de développement logiciel Azure IoT](iot-hub-devguide-sdks.md) fournit des informations sur hello kits de développement logiciel Azure IoT que vous pouvez utiliser toobuild applications de périphérique et back-end.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="2d7d1-109">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="2d7d1-110">Hello dernières [8 de Kit de développement Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="2d7d1-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="2d7d1-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="2d7d1-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="2d7d1-112">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-112">An active Azure account.</span></span> <span data-ttu-id="2d7d1-113">(Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes seulement.)</span><span class="sxs-lookup"><span data-stu-id="2d7d1-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="2d7d1-114">Si vous préférez identité d’appareil toocreate hello par programmation, lire la section correspondante de hello Bonjour [connectez votre concentrateur de IoT tooyour périphérique à l’aide de Java](iot-hub-java-java-getstarted.md#create-a-device-identity) l’article.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="2d7d1-115">Créer l’application de service hello</span><span class="sxs-lookup"><span data-stu-id="2d7d1-115">Create hello service app</span></span>

<span data-ttu-id="2d7d1-116">Dans cette section, vous créez une application Java qui ajoute des métadonnées de l’emplacement associé à un double d’appareil toohello balise dans IoT Hub **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="2d7d1-117">application Hello interroge d’abord IoT hub pour les périphériques situés dans hello des États-Unis, puis pour les appareils qui indiquent une connexion réseau cellulaire.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="2d7d1-118">Sur votre ordinateur de développement, créez un dossier vide nommé `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="2d7d1-119">Bonjour `iot-java-twin-getstarted` dossier, créez un projet Maven appelé **ajouter de requête de balises** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="2d7d1-120">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2d7d1-121">À l’invite de commandes, accédez à toohello `add-tags-query` dossier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="2d7d1-122">À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `add-tags-query` dossier et ajoutez hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="2d7d1-123">Cette dépendance vous permet de toouse hello **iot-service-client** package dans toocommunicate de votre application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2d7d1-124">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2d7d1-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2d7d1-125">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2d7d1-126">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2d7d1-127">Enregistrez et fermez hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2d7d1-128">À l’aide d’un éditeur de texte, ouvrez hello `add-tags-query\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2d7d1-129">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="2d7d1-130">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2d7d1-131">Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="2d7d1-132">Hello de mise à jour **principal** suivant de méthode signature tooinclude hello `throws` clause :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="2d7d1-133">Ajouter hello suivant code toohello **principal** hello toocreate de méthode **DeviceTwin** et **DeviceTwinDevice** objets.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="2d7d1-134">Hello **DeviceTwin** objet gère la communication de hello avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="2d7d1-135">Hello **DeviceTwinDevice** objet représente le double de périphérique hello avec ses propriétés et les balises :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="2d7d1-136">Ajoutez hello suivant `try/catch` bloquer toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="2d7d1-137">tooupdate hello **région** et **plant** balises double de périphérique en double de votre appareil, ajouter hello suivant code Bonjour `try` bloc :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="2d7d1-138">jumeaux de périphérique tooquery hello dans IoT hub, ajouter hello suivant code toohello `try` bloc après le code hello ajoutée à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="2d7d1-139">code de Hello exécute deux requêtes.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-139">hello code runs two queries.</span></span> <span data-ttu-id="2d7d1-140">Chaque requête retourne un maximum de 100 appareils :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="2d7d1-141">Enregistrez et fermez hello `add-tags-query\src\main\java\com\mycompany\app\App.java` fichier</span><span class="sxs-lookup"><span data-stu-id="2d7d1-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="2d7d1-142">Build hello **ajouter de requête de balises** application et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="2d7d1-143">À l’invite de commandes, accédez à toohello `add-tags-query` dossier et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="2d7d1-144">Créer une application d’appareil</span><span class="sxs-lookup"><span data-stu-id="2d7d1-144">Create a device app</span></span>

<span data-ttu-id="2d7d1-145">Dans cette section, vous créer une application de console Java qui définit une valeur de propriété signalé est envoyée tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="2d7d1-146">Bonjour `iot-java-twin-getstarted` dossier, créez un projet Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="2d7d1-147">Il s’agit d’une commande unique et longue :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="2d7d1-148">À l’invite de commandes, accédez à toohello `simulated-device` dossier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="2d7d1-149">À l’aide d’un éditeur de texte, ouvrez hello `pom.xml` fichier Bonjour `simulated-device` dossier et ajoutez hello suivant dépendances toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="2d7d1-150">Cette dépendance vous permet de toouse hello **client de périphérique iot** package dans toocommunicate de votre application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="2d7d1-151">Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="2d7d1-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="2d7d1-152">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="2d7d1-153">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="2d7d1-154">Enregistrez et fermez hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="2d7d1-155">À l’aide d’un éditeur de texte, ouvrez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2d7d1-156">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="2d7d1-157">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="2d7d1-158">En remplaçant `{youriothubname}` avec votre nom de hub IoT, et `{yourdevicekey}` avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="2d7d1-159">Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="2d7d1-160">Actuellement, toouse appareil double fonctionnalités vous devez utiliser le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="2d7d1-161">Ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="2d7d1-162">Créer un toocommunicate de client de périphérique avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="2d7d1-163">Créer un **périphérique** toostore hello appareil deux propriétés de l’objet.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-163">Create a **Device** object toostore hello device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="2d7d1-164">Ajouter hello suivant code toohello **principal** méthode toocreate un **connectivityType** a signalé de propriété et l’envoyer tooIoT Hub :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
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

1. <span data-ttu-id="2d7d1-165">Ajouter hello suivant fin toohello de code Hello **principal** (méthode).</span><span class="sxs-lookup"><span data-stu-id="2d7d1-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="2d7d1-166">En attente de hello **entrée** clé permet au statut de hello IoT Hub tooreport d’opérations de double hello appareil :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="2d7d1-167">Enregistrez et fermez hello `simulated-device\src\main\java\com\mycompany\app\App.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="2d7d1-168">Build hello **appareil simulé** application et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="2d7d1-169">À l’invite de commandes, accédez à toohello `simulated-device` dossier et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="2d7d1-170">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="2d7d1-170">Run hello apps</span></span>

<span data-ttu-id="2d7d1-171">Vous êtes maintenant prêt toorun les applications de console hello.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="2d7d1-172">À l’invite de commande Bonjour `add-tags-query` dossier, exécutez hello suivant commande toorun hello **ajouter de requête de balises** application de service :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service application tooupdate baliser les valeurs et exécuter des requêtes de l’appareil](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="2d7d1-174">Vous pouvez voir hello **plant** et **région** balises ajoutées double de périphérique toohello.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="2d7d1-175">Hello première requête retourne votre appareil, mais hello deuxième pas.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="2d7d1-176">À l’invite de commande Bonjour `simulated-device` dossier, exécutez hello suivant commande tooadd hello **connectivityType** signalés double de propriété toohello appareil :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![client de périphérique Hello ajoute hello ** connectivityType ** signalé de propriété](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="2d7d1-178">À l’invite de commande Bonjour `add-tags-query` dossier, exécutez hello suivant commande toorun hello **ajouter de requête de balises** service application une deuxième fois :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service application tooupdate baliser les valeurs et exécuter des requêtes de l’appareil](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="2d7d1-180">Maintenant que votre appareil a envoyé hello **connectivityType** propriété tooIoT concentrateur, seconde hello retourne votre appareil.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d7d1-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d7d1-181">Next steps</span></span>

<span data-ttu-id="2d7d1-182">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="2d7d1-183">Vous ajouté des métadonnées de l’appareil sous forme de balises à partir d’une application back-end et a écrit un appareil application tooreport appareil connectivité des informations en double du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="2d7d1-184">Vous avez également appris comment tooquery hello informations double de l’appareil à l’aide du langage de requête de type SQL IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="2d7d1-185">Hello utilisation suivant comment les ressources toolearn à :</span><span class="sxs-lookup"><span data-stu-id="2d7d1-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="2d7d1-186">Envoyer la télémétrie des appareils avec hello [prise en main IoT Hub](iot-hub-java-java-getstarted.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="2d7d1-187">Contrôler les périphériques de manière interactive (telles que l’activation sur un ventilateur à partir d’une application contrôlée par l’utilisateur) avec hello [utiliser les méthodes directes](iot-hub-java-java-direct-methods.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d7d1-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
