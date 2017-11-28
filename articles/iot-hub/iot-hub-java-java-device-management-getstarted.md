---
title: "aaaGet a démarré avec la gestion des appareils Azure IoT Hub (Java) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub device management tooinitiate un appareil distant redémarrer. Vous utilisez du SDK de périphérique Azure IoT hello pour Java tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour Java tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="cad2c-104">Prise en main de la gestion d’appareils (Java)</span><span class="sxs-lookup"><span data-stu-id="cad2c-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="cad2c-105">Ce didacticiel vous explique les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="cad2c-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="cad2c-106">Utilisez hello toocreate portail Azure un IoT Hub et créer une identité d’appareil dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cad2c-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="cad2c-107">Créer une application d’appareil simulé qui implémente un périphérique de hello tooreboot méthode directe.</span><span class="sxs-lookup"><span data-stu-id="cad2c-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="cad2c-108">Méthodes directes sont appelés à partir du cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="cad2c-109">Créer une application qui appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello via votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cad2c-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="cad2c-110">Cette application, les analyses hello propriétés signalées de hello appareil toosee lorsque l’opération de redémarrage hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="cad2c-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="cad2c-111">À la fin de hello de ce didacticiel, vous avez deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="cad2c-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="cad2c-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="cad2c-112">**simulated-device**.</span></span> <span data-ttu-id="cad2c-113">Cette application :</span><span class="sxs-lookup"><span data-stu-id="cad2c-113">This app:</span></span>

* <span data-ttu-id="cad2c-114">Se connecte à tooyour IoT hub avec l’identité de l’appareil hello créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="cad2c-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="cad2c-115">reçoit un appel de méthode directe de redémarrage ;</span><span class="sxs-lookup"><span data-stu-id="cad2c-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="cad2c-116">simule un redémarrage physique ;</span><span class="sxs-lookup"><span data-stu-id="cad2c-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="cad2c-117">Indique le temps hello du dernier redémarrage de hello via une propriété signalée.</span><span class="sxs-lookup"><span data-stu-id="cad2c-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="cad2c-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="cad2c-118">**trigger-reboot**.</span></span> <span data-ttu-id="cad2c-119">Cette application :</span><span class="sxs-lookup"><span data-stu-id="cad2c-119">This app:</span></span>

* <span data-ttu-id="cad2c-120">Appelle une méthode directe dans l’application d’appareil simulé hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="cad2c-121">Affiche l’appel de méthode directe hello réponse toohello envoyé par appareil simulé de hello</span><span class="sxs-lookup"><span data-stu-id="cad2c-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="cad2c-122">Hello affiche mis à jour a signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="cad2c-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="cad2c-123">Pour plus d’informations sur les kits de développement logiciel de hello que vous pouvez utiliser toobuild applications toorun sur les périphériques et votre principal de la solution, consultez [kits de développement logiciel Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="cad2c-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="cad2c-124">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="cad2c-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="cad2c-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="cad2c-125">Java SE 8.</span></span> <br/> <span data-ttu-id="cad2c-126">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Java pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="cad2c-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cad2c-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="cad2c-127">Maven 3.</span></span>  <br/> <span data-ttu-id="cad2c-128">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall [Maven] [ lnk-maven] pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="cad2c-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="cad2c-129">[Node.js version 0.10.0 ou supérieure](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="cad2c-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="cad2c-130">Déclencher un arrêt à distance sur l’appareil hello à l’aide d’une méthode directe</span><span class="sxs-lookup"><span data-stu-id="cad2c-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="cad2c-131">Dans cette section, vous allez créer une application console Java qui :</span><span class="sxs-lookup"><span data-stu-id="cad2c-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="cad2c-132">Appelle la méthode directe de redémarrage hello dans l’application d’appareil simulé hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="cad2c-133">Affiche la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-133">Displays hello response.</span></span>
1. <span data-ttu-id="cad2c-134">Hello de sondages signalé propriétés envoyées à partir de toodetermine de périphérique hello lorsque hello redémarrage soit terminé.</span><span class="sxs-lookup"><span data-stu-id="cad2c-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="cad2c-135">Cette application console connecte tooyour IoT Hub méthode directe de tooinvoke hello et lecture hello signalé des propriétés.</span><span class="sxs-lookup"><span data-stu-id="cad2c-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="cad2c-136">Créez un dossier vide appelé dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="cad2c-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="cad2c-137">Dans le dossier d’exploration de données-get-started hello, créez un projet de Maven appelé **déclencheur-redémarrage** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="cad2c-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="cad2c-138">Hello Voici une commande unique longue :</span><span class="sxs-lookup"><span data-stu-id="cad2c-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="cad2c-139">À l’invite de commandes, accédez toohello déclencheur-redémarrage dossier.</span><span class="sxs-lookup"><span data-stu-id="cad2c-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="cad2c-140">À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier de redémarrage de déclencheur hello et ajouter hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="cad2c-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="cad2c-141">Cette dépendance permet de vous toouse hello iot-service-package client dans votre toocommunicate d’application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="cad2c-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="cad2c-142">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="cad2c-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="cad2c-143">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="cad2c-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="cad2c-144">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="cad2c-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="cad2c-145">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="cad2c-146">À l’aide d’un éditeur de texte, d’ouvrir le fichier de source de trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="cad2c-147">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="cad2c-147">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="cad2c-148">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="cad2c-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="cad2c-149">Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :</span><span class="sxs-lookup"><span data-stu-id="cad2c-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="cad2c-150">tooimplement un thread qui lit hello a signalé des propriétés à partir du double du périphérique hello toutes les 10 secondes, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="cad2c-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="cad2c-151">méthode directe de redémarrage hello tooinvoke sur l’appareil simulé de hello, ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="cad2c-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="cad2c-152">toostart hello thread toopoll hello propriétés signalées à partir de l’appareil simulé de hello, ajoutez des hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="cad2c-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="cad2c-153">tooenable vous toostop hello application Ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="cad2c-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="cad2c-154">Enregistrez et fermez le fichier de trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="cad2c-155">Build hello **déclencheur-redémarrage** applications principal et corriger les erreurs éventuelles.</span><span class="sxs-lookup"><span data-stu-id="cad2c-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="cad2c-156">Votre invite de commandes, accédez à toohello déclencheur-redémarrage dossier et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cad2c-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="cad2c-157">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="cad2c-157">Create a simulated device app</span></span>

<span data-ttu-id="cad2c-158">Dans cette section, vous créez une application console Java qui simule un appareil.</span><span class="sxs-lookup"><span data-stu-id="cad2c-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="cad2c-159">application Hello écoute les appels de méthode directe hello redémarrage à partir de votre hub IoT et répond immédiatement toothat appel.</span><span class="sxs-lookup"><span data-stu-id="cad2c-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="cad2c-160">Hello application puis se met en veille pendant un certain temps toosimulate le processus de redémarrage hello avant d’utiliser un Bonjour toonotify de propriété signalé **déclencheur-redémarrage** application principaux qui hello redémarrage est terminée.</span><span class="sxs-lookup"><span data-stu-id="cad2c-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="cad2c-161">Dans le dossier d’exploration de données-get-started hello, créez un projet de Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="cad2c-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="cad2c-162">Hello Voici une commande unique longue :</span><span class="sxs-lookup"><span data-stu-id="cad2c-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="cad2c-163">Votre invite de commandes, accédez à dossier d’appareil simulé toohello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="cad2c-164">À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier d’appareil simulé hello et ajouter hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="cad2c-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="cad2c-165">Cette dépendance permet de vous toouse hello iot-service-package client dans votre toocommunicate d’application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="cad2c-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="cad2c-166">Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="cad2c-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="cad2c-167">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="cad2c-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="cad2c-168">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="cad2c-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="cad2c-169">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="cad2c-170">À l’aide d’un éditeur de texte, d’ouvrir le fichier de source de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="cad2c-171">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="cad2c-171">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="cad2c-172">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="cad2c-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="cad2c-173">Remplacez `{yourdeviceconnectionstring}` avec chaîne de connexion de périphérique hello noté Bonjour *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="cad2c-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="cad2c-174">tooimplement un gestionnaire de rappel pour les événements d’état de méthode directe, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="cad2c-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="cad2c-175">tooimplement un gestionnaire de rappel pour les événements d’état de périphérique double, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="cad2c-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="cad2c-176">tooimplement un gestionnaire de rappel pour les événements de propriété, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="cad2c-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="cad2c-177">tooimplement un thread toosimulate hello redémarrage de l’appareil, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="cad2c-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="cad2c-178">thread de Hello se met en veille pendant cinq secondes et qu’il définit ensuite hello **lastReboot** a signalé de propriété :</span><span class="sxs-lookup"><span data-stu-id="cad2c-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="cad2c-179">méthode directe de tooimplement hello sur le périphérique de hello, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="cad2c-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="cad2c-180">Lorsque application simulé hello reçoit un appel toohello **redémarrer** méthode directe, il retourne un appelant de toohello d’accusé de réception et démarre un Bonjour tooprocess de thread redémarrez :</span><span class="sxs-lookup"><span data-stu-id="cad2c-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="cad2c-181">Modifier la signature hello Hello **principal** hello toothrow de méthode suivant des exceptions :</span><span class="sxs-lookup"><span data-stu-id="cad2c-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="cad2c-182">tooinstantiate un **DeviceClient**, ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="cad2c-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="cad2c-183">toostart l’écoute des appels de méthode directe, ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="cad2c-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="cad2c-184">tooshut vers le bas de simulateur d’appareil hello, ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="cad2c-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="cad2c-185">Enregistrez et fermez le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="cad2c-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="cad2c-186">Build hello **appareil simulé** applications principal et corriger les erreurs éventuelles.</span><span class="sxs-lookup"><span data-stu-id="cad2c-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="cad2c-187">Votre invite de commandes, accédez à dossier d’appareil simulé toohello et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cad2c-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="cad2c-188">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="cad2c-188">Run hello apps</span></span>

<span data-ttu-id="cad2c-189">Vous êtes maintenant prêt toorun hello applications.</span><span class="sxs-lookup"><span data-stu-id="cad2c-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="cad2c-190">À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande écoute les appels de méthode de redémarrage à partir de votre hub IoT :</span><span class="sxs-lookup"><span data-stu-id="cad2c-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulée toolisten d’application de périphérique pour les appels de méthode directe de redémarrage][1]

1. <span data-ttu-id="cad2c-192">À une invite de commandes dans le dossier de redémarrage de déclencheur hello, exécutez hello suivant de méthode de redémarrage de la commande toocall hello sur votre appareil simulé à partir de votre hub IoT :</span><span class="sxs-lookup"><span data-stu-id="cad2c-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hello de toocall application Java IoT Hub service redémarrer méthode directe][2]

1. <span data-ttu-id="cad2c-194">APPAREIL simulé de Hello répond appel de méthode directe toohello redémarrage :</span><span class="sxs-lookup"><span data-stu-id="cad2c-194">hello simulated device responds toohello reboot direct method call:</span></span>

    ![Application d’appareil simulé Java IoT Hub répond l’appel de méthode directe toohello][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22