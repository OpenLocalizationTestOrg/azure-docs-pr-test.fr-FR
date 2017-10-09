---
title: "aaaUse Azure IoT Hub direct de méthodes (Java) | Documents Microsoft"
description: "Comment toouse Azure IoT Hub direct de méthodes. Vous utilisez du SDK de périphérique Azure IoT hello pour Java tooimplement une application d’appareil simulé qui inclut une méthode directe et la hello Azure IoT service SDK pour Java tooimplement une application de service qui appelle la méthode directe hello."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="c6c74-104">Utilisation des méthodes directes (Java)</span><span class="sxs-lookup"><span data-stu-id="c6c74-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="c6c74-105">Dans ce tutoriel, vous allez créer deux applications de console Java :</span><span class="sxs-lookup"><span data-stu-id="c6c74-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="c6c74-106">**méthode directe Invoke**, une principal d’application Java qui appelle une méthode dans l’application d’appareil simulé hello et affiche la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="c6c74-107">**APPAREIL simulé**, une application Java qui simule un appareil de connexion tooyour IoT hub avec l’identité d’appareil hello vous créez.</span><span class="sxs-lookup"><span data-stu-id="c6c74-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="c6c74-108">Cette application répond toohello directement appelée à partir de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="c6c74-109">Pour plus d’informations sur les kits de développement logiciel de hello que vous pouvez utiliser toobuild applications toorun sur les périphériques et votre principal de la solution, consultez [kits de développement logiciel Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="c6c74-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="c6c74-110">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="c6c74-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c6c74-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="c6c74-111">Java SE 8.</span></span> <br/> <span data-ttu-id="c6c74-112">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall Java pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c6c74-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c6c74-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="c6c74-113">Maven 3.</span></span>  <br/> <span data-ttu-id="c6c74-114">[Préparer votre environnement de développement] [ lnk-dev-setup] décrit comment tooinstall [Maven] [ lnk-maven] pour ce didacticiel sur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c6c74-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c6c74-115">[Node.js version 0.10.0 ou supérieure](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="c6c74-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c6c74-116">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="c6c74-116">Create a simulated device app</span></span>

<span data-ttu-id="c6c74-117">Dans cette section, vous créez une application de console Java qui répond méthode tooa appelée par solution hello retour de fin.</span><span class="sxs-lookup"><span data-stu-id="c6c74-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="c6c74-118">Créez un dossier vide appelé iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="c6c74-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="c6c74-119">Dans le dossier de méthode iot-java-direct hello, créez un projet de Maven appelé **appareil simulé** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="c6c74-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="c6c74-120">Hello commande suivante est une commande unique longue :</span><span class="sxs-lookup"><span data-stu-id="c6c74-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c6c74-121">Votre invite de commandes, accédez à dossier d’appareil simulé toohello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="c6c74-122">À l’aide d’un éditeur de texte, ouvrir le fichier de pom.xml hello dans le dossier d’appareil simulé hello et ajouter hello suivant dépendances toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="c6c74-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="c6c74-123">Cette dépendance permet à vous toouse hello client de périphérique iot package dans toocommunicate de votre application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="c6c74-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c6c74-124">Vous pouvez vérifier pour la version la plus récente de hello **client de périphérique iot** à l’aide de [recherche de Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="c6c74-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="c6c74-125">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="c6c74-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c6c74-126">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="c6c74-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c6c74-127">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="c6c74-128">À l’aide d’un éditeur de texte, d’ouvrir le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c6c74-129">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="c6c74-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="c6c74-130">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="c6c74-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c6c74-131">En remplaçant `{youriothubname}` avec votre nom de hub IoT, et `{yourdevicekey}` avec la valeur de clé de périphérique hello générées dans hello *créer une identité d’appareil* section :</span><span class="sxs-lookup"><span data-stu-id="c6c74-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="c6c74-132">Cet exemple d’application utilise hello **protocole** variable lorsqu’il instancie une **DeviceClient** objet.</span><span class="sxs-lookup"><span data-stu-id="c6c74-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="c6c74-133">Actuellement, toouse directe des méthodes que vous devez utiliser le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="c6c74-134">tooreturn un IoT hub état code tooyour, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="c6c74-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c6c74-135">appels de méthode directe d’hello toohandle de hello solution serveur principal, ajoutez des éléments suivants de hello imbriqués classe toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="c6c74-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="c6c74-136">toocreate un **DeviceClient** et écouter les appels de méthode directe, ajoutez un **principal** méthode toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="c6c74-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="c6c74-137">Enregistrez et fermez le fichier de simulated-device\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="c6c74-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="c6c74-138">Build hello **appareil simulé** application et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="c6c74-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="c6c74-139">Votre invite de commandes, accédez à dossier d’appareil simulé toohello et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6c74-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="c6c74-140">Appeler une méthode directe sur un appareil</span><span class="sxs-lookup"><span data-stu-id="c6c74-140">Call a direct method on a device</span></span>

<span data-ttu-id="c6c74-141">Dans cette section, vous créez une application de console Java qui appelle une méthode directe, puis affiche les réponse hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="c6c74-142">Cette application console connecte tooyour méthode directe de IoT Hub tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="c6c74-143">Dans le dossier de méthode iot-java-direct hello, créez un projet de Maven appelé **méthode direct invoke** à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="c6c74-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="c6c74-144">Hello commande suivante est une commande unique longue :</span><span class="sxs-lookup"><span data-stu-id="c6c74-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c6c74-145">Votre invite de commandes, accédez à toohello invoke-direct-méthode dossier.</span><span class="sxs-lookup"><span data-stu-id="c6c74-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="c6c74-146">À l’aide d’un éditeur de texte, ouvrez le fichier de pom.xml de hello dans le dossier d’appel de méthode de direct hello et ajouter hello suivant dépendance toohello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="c6c74-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c6c74-147">Cette dépendance permet de vous toouse hello iot-service-package client dans votre toocommunicate d’application avec votre IoT hub :</span><span class="sxs-lookup"><span data-stu-id="c6c74-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c6c74-148">Vous pouvez vérifier pour la version la plus récente de hello **iot-service-client** à l’aide de [recherche de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="c6c74-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="c6c74-149">Ajoutez hello suivant **générer** nœud après hello **dépendances** nœud.</span><span class="sxs-lookup"><span data-stu-id="c6c74-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c6c74-150">Cette configuration indique d’application hello toobuild 1,8 Maven toouse Java :</span><span class="sxs-lookup"><span data-stu-id="c6c74-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c6c74-151">Enregistrez et fermez le fichier de pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="c6c74-152">À l’aide d’un éditeur de texte, d’ouvrir le fichier de invoke-direct-method\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c6c74-153">Ajoutez hello suivant **importer** fichier de toohello instructions :</span><span class="sxs-lookup"><span data-stu-id="c6c74-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="c6c74-154">Ajouter hello suivant des variables de niveau classe toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="c6c74-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c6c74-155">Remplacez `{youriothubconnectionstring}` avec votre chaîne de connexion de hub IoT noté dans hello *créez un IoT Hub* section :</span><span class="sxs-lookup"><span data-stu-id="c6c74-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="c6c74-156">méthode hello tooinvoke appareil simulé de hello, ajouter hello suivant code toohello **principal** méthode :</span><span class="sxs-lookup"><span data-stu-id="c6c74-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="c6c74-157">Enregistrez et fermez le fichier de invoke-direct-method\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="c6c74-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="c6c74-158">Build hello **méthode direct invoke** application et corrigez les erreurs.</span><span class="sxs-lookup"><span data-stu-id="c6c74-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="c6c74-159">Votre invite de commandes, accédez à dossier d’appel de méthode de direct toohello et exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6c74-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="c6c74-160">Exécuter des applications de hello</span><span class="sxs-lookup"><span data-stu-id="c6c74-160">Run hello apps</span></span>

<span data-ttu-id="c6c74-161">Vous êtes maintenant prêt toorun les applications de console hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="c6c74-162">À une invite de commandes dans le dossier d’appareil simulé hello, exécutez hello suivant toobegin commande écoute les appels de méthode à partir de votre hub IoT :</span><span class="sxs-lookup"><span data-stu-id="c6c74-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub simulée toolisten d’application de périphérique pour les appels de méthode directe][8]

1. <span data-ttu-id="c6c74-164">À une invite de commandes dans le dossier d’appel de méthode de direct hello, exécutez hello suivant de commande toocall une méthode sur votre appareil simulé à partir de votre hub IoT :</span><span class="sxs-lookup"><span data-stu-id="c6c74-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Java IoT Hub service application toocall une méthode directe][7]

1. <span data-ttu-id="c6c74-166">APPAREIL simulé de Hello répond l’appel de méthode directe toohello :</span><span class="sxs-lookup"><span data-stu-id="c6c74-166">hello simulated device responds toohello direct method call:</span></span>

    ![Application d’appareil simulé Java IoT Hub répond l’appel de méthode directe toohello][9]

## <a name="next-steps"></a><span data-ttu-id="c6c74-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6c74-168">Next steps</span></span>

<span data-ttu-id="c6c74-169">Dans ce didacticiel, vous configuré un IoT hub Bonjour portail Azure et ensuite créé une identité d’appareil dans le Registre des identités de hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c6c74-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="c6c74-170">Vous avez utilisé ce périphérique identité tooenable hello simulée appareil application tooreact toomethods appelée par le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="c6c74-171">Vous avez créé également une application qui appelle des méthodes sur l’appareil de hello et affiche la réponse hello périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="c6c74-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="c6c74-172">tooexplore autres scénarios IoT, consultez [planifier des travaux sur plusieurs appareils][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="c6c74-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="c6c74-173">toolearn tooextend votre méthode de planification et de solution IoT des appels sur plusieurs appareils, consultez hello [planification et les tâches de diffusion] [ lnk-tutorial-jobs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c6c74-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
