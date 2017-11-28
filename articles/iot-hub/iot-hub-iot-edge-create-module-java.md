---
title: "Créer un module Azure IoT Edge avec Java | Microsoft Docs"
description: "Ce didacticiel explique comment écrire un module de convertisseur de données BLE en utilisant les derniers packages Maven Azure IoT Edge."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: 0c430272225d79737baec2be15ed7c93991cdeac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="6a279-103">Créer un module Azure IoT Edge avec Java</span><span class="sxs-lookup"><span data-stu-id="6a279-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="6a279-104">Ce didacticiel explique comment vous pouvez créer un module pour Azure IoT Edge en Java.</span><span class="sxs-lookup"><span data-stu-id="6a279-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="6a279-105">Dans ce didacticiel, nous aborderons la configuration de l’environnement et expliquerons comment écrire un module de convertisseur de données [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) en utilisant les derniers packages Maven Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="6a279-105">In this tutorial, we will walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a279-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6a279-106">Prerequisites</span></span>

<span data-ttu-id="6a279-107">Dans cette section, vous allez configurer votre environnement pour le développement du module IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="6a279-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="6a279-108">Cela s’applique aux systèmes d’exploitation *Windows 64 bits* et *Linux 64 bits (Ubuntu/Debian 8)*.</span><span class="sxs-lookup"><span data-stu-id="6a279-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="6a279-109">Les logiciels suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="6a279-109">The following software is required:</span></span>

* <span data-ttu-id="6a279-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="6a279-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="6a279-111">[JDK **x64**](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="6a279-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="6a279-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="6a279-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="6a279-113">Ouvrez une fenêtre de terminal de ligne de commande et clonez le référentiel suivant :</span><span class="sxs-lookup"><span data-stu-id="6a279-113">Open a command-line terminal window and clone the following repository:</span></span>

1. <span data-ttu-id="6a279-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="6a279-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="6a279-115">Architecture globale</span><span class="sxs-lookup"><span data-stu-id="6a279-115">Overall architecture</span></span>

<span data-ttu-id="6a279-116">La plateforme Azure IoT Edge adopte fortement [l’architecture de Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="6a279-116">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="6a279-117">Cela signifie que l’ensemble de l’architecture Azure IoT Edge est un système qui traite une entrée et produit une sortie, et que chaque module individuel est également un minuscule sous-système d’entrée-de sortie.</span><span class="sxs-lookup"><span data-stu-id="6a279-117">Which means that the entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="6a279-118">Dans ce didacticiel, nous allons présenter les deux modules suivants :</span><span class="sxs-lookup"><span data-stu-id="6a279-118">In this tutorial, we will introduce the following two modules:</span></span>

1. <span data-ttu-id="6a279-119">Un module qui reçoit un signal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulé et qui le convertit en message au format [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="6a279-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="6a279-120">Un module qui imprime le message [JSON](https://en.wikipedia.org/wiki/JSON) reçu.</span><span class="sxs-lookup"><span data-stu-id="6a279-120">A module which prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="6a279-121">L’image suivante affiche le flux de données de bout en bout classique pour ce projet :</span><span class="sxs-lookup"><span data-stu-id="6a279-121">The following image displays the typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="6a279-122">![Flux de données entre les trois modules](media/iot-hub-iot-edge-create-module/dataflow.png "Entrée : module BLE simulé ; processeur : module de convertisseur ; sortie : module d’imprimante")</span><span class="sxs-lookup"><span data-stu-id="6a279-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="6a279-123">Présentation du code</span><span class="sxs-lookup"><span data-stu-id="6a279-123">Understanding the code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="6a279-124">Structure du projet Maven</span><span class="sxs-lookup"><span data-stu-id="6a279-124">Maven project structure</span></span>

<span data-ttu-id="6a279-125">Comme les packages Azure IoT Edge reposent sur Maven, nous avons besoin de créer une structure de projet Maven classique, qui contient un fichier `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="6a279-125">Since Azure IoT Edge packages are based on Maven, we need to create a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="6a279-126">Le POM hérite du package `com.microsoft.azure.gateway.gateway-module-base`, qui déclare toutes les dépendances requises par un projet de module incluant les fichiers binaires du runtime, le chemin du fichier config et le comportement d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a279-126">The POM inherits from the `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of the dependencies needed by a module project which includes the runtime binaries, the gateway configuration file path, and the execution behavior.</span></span> <span data-ttu-id="6a279-127">Cela nous permet de gagner beaucoup de temps et élimine la nécessité d’écrire et de réécrire des centaines de lignes de code indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="6a279-127">This saves us lots of time and eliminate the need to write and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="6a279-128">Nous devons mettre à jour le fichier pom.xml en déclarant les dépendances/plug-ins requis et le nom du fichier config à utiliser par notre module, comme indiqué dans l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="6a279-128">We need to update the pom.xml file by declaring the required dependencies/plugins and the name of the configuration file to be used by our module as shown in the following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set the filename of the Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="6a279-129">Compréhension élémentaire d’un module Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="6a279-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="6a279-130">Vous pouvez traiter un module Azure IoT Edge comme un processeur de données dont la tâche consiste à : recevoir une entrée, la traiter et générer une sortie.</span><span class="sxs-lookup"><span data-stu-id="6a279-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="6a279-131">L’entrée peut être des données issues du matériel (comme un détecteur de mouvement), un message provenant d’autres modules ou toute autre chose (par exemple, un nombre aléatoire généré régulièrement par un minuteur).</span><span class="sxs-lookup"><span data-stu-id="6a279-131">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="6a279-132">La sortie est similaire à l’entrée, elle peut déclencher le comportement du matériel (comme le clignotement d’une LED), un message à d’autres modules ou toute autre chose (par exemple, une impression vers la console).</span><span class="sxs-lookup"><span data-stu-id="6a279-132">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="6a279-133">Les modules communiquent entre eux à l’aide de la classe `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="6a279-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="6a279-134">Le **contenu** d’un `Message` est un tableau d’octets qui est capable de représenter n’importe quel type de données de votre choix.</span><span class="sxs-lookup"><span data-stu-id="6a279-134">The **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="6a279-135">Les **propriétés** sont également disponibles dans le `Message` et sont simplement un mappage de chaîne à chaîne.</span><span class="sxs-lookup"><span data-stu-id="6a279-135">**Properties** are also available in the `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="6a279-136">Vous pouvez imaginer les **propriétés** comme étant les en-têtes d’une demande HTTP ou les métadonnées d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="6a279-136">You may think of **Properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="6a279-137">Pour développer un module Azure IoT Edge en Java, vous devez créer une classe de module qui hérite de `com.microsoft.azure.gateway.core.GatewayModule` et implémenter les méthodes abstraites `receive()` et `destroy()` requises.</span><span class="sxs-lookup"><span data-stu-id="6a279-137">In order to develop an Azure IoT Edge module in Java, you need to create a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement the required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="6a279-138">À ce stade, vous pouvez également choisir d’implémenter les méthodes `start()` ou `create()` facultatives.</span><span class="sxs-lookup"><span data-stu-id="6a279-138">At this point, you may also choose to implement the optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="6a279-139">L’extrait de code suivant vous montre comment prendre en main la création d’un module Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="6a279-139">The following code snippet shows you how to get started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let the GatewayModule do the dirty work of initialization. It's also
       a good time to parse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire the resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time to release all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic to process the input message. This method is required. */
    // ...
    /* Use publish() method to do the output. You are
       allowed to publish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="6a279-140">Module de convertisseur</span><span class="sxs-lookup"><span data-stu-id="6a279-140">Converter module</span></span>

| <span data-ttu-id="6a279-141">Entrée</span><span class="sxs-lookup"><span data-stu-id="6a279-141">Input</span></span>                    | <span data-ttu-id="6a279-142">Processeur</span><span class="sxs-lookup"><span data-stu-id="6a279-142">Processor</span></span>                              | <span data-ttu-id="6a279-143">Sortie</span><span class="sxs-lookup"><span data-stu-id="6a279-143">Output</span></span>                 | <span data-ttu-id="6a279-144">Fichier source</span><span class="sxs-lookup"><span data-stu-id="6a279-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="6a279-145">Message de données de température</span><span class="sxs-lookup"><span data-stu-id="6a279-145">Temperature data message</span></span> | <span data-ttu-id="6a279-146">Analyser et construire un nouveau message JSON</span><span class="sxs-lookup"><span data-stu-id="6a279-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="6a279-147">Structurer le message JSON</span><span class="sxs-lookup"><span data-stu-id="6a279-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="6a279-148">Ce module est un module Azure IoT Edge classique.</span><span class="sxs-lookup"><span data-stu-id="6a279-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="6a279-149">Il accepte des messages de température provenant d’autres modules (un module de matériel, ou dans notre cas, notre module BLE simulé), puis normalise le message de température dans un message JSON structuré (y compris l’ajout de l’ID de message, la définition de la propriété indiquant si nous devons déclencher l’alerte de température, etc.).</span><span class="sxs-lookup"><span data-stu-id="6a279-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="6a279-150">Module d’imprimante</span><span class="sxs-lookup"><span data-stu-id="6a279-150">Printer module</span></span>

| <span data-ttu-id="6a279-151">Entrée</span><span class="sxs-lookup"><span data-stu-id="6a279-151">Input</span></span>                          | <span data-ttu-id="6a279-152">Processeur</span><span class="sxs-lookup"><span data-stu-id="6a279-152">Processor</span></span> | <span data-ttu-id="6a279-153">Sortie</span><span class="sxs-lookup"><span data-stu-id="6a279-153">Output</span></span>                     | <span data-ttu-id="6a279-154">Fichier source</span><span class="sxs-lookup"><span data-stu-id="6a279-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="6a279-155">Tous les messages provenant d’autres modules</span><span class="sxs-lookup"><span data-stu-id="6a279-155">Any message from other modules</span></span> | <span data-ttu-id="6a279-156">N/A</span><span class="sxs-lookup"><span data-stu-id="6a279-156">N/A</span></span>       | <span data-ttu-id="6a279-157">Enregistrer le message sur la console</span><span class="sxs-lookup"><span data-stu-id="6a279-157">Log the message to console</span></span> | `PrinterModule.java` |

<span data-ttu-id="6a279-158">Il s’agit d’un module simple et explicite qui génère les messages reçus dans la fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="6a279-158">This is a simple, self-explanatory, module which outputs the received messages to the terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="6a279-159">Configuration d’Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="6a279-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="6a279-160">La dernière étape avant d’exécuter les modules consiste à configurer Azure IoT Edge et à établir les connexions entre les modules.</span><span class="sxs-lookup"><span data-stu-id="6a279-160">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="6a279-161">Tout d’abord, nous devons déclarer notre chargeur Java (étant donné qu’Azure IoT Edge prend en charge des chargeurs de différents langages) qui peut, par la suite, être référencé par son `name` dans les sections.</span><span class="sxs-lookup"><span data-stu-id="6a279-161">First we need to declare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="6a279-162">Une fois que nous avons déclaré nos chargeurs, nous devrons également déclarer nos modules.</span><span class="sxs-lookup"><span data-stu-id="6a279-162">Once we have declared our loaders, we will also need to declare our modules as well.</span></span> <span data-ttu-id="6a279-163">À l’instar de la déclaration des chargeurs, les modules peuvent aussi être référencés par leur attribut `name`.</span><span class="sxs-lookup"><span data-stu-id="6a279-163">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="6a279-164">Lors de la déclaration d’un module, nous devons spécifier le chargeur qu’il doit utiliser (qui doit être celui que nous avons défini avant) et le point d’entrée (qui doit être le nom de la classe normalisé de notre module) pour chaque module.</span><span class="sxs-lookup"><span data-stu-id="6a279-164">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="6a279-165">Le module `simulated_device` est un module natif qui est inclus dans le package de runtime principal Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="6a279-165">The `simulated_device` module is a native module which is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="6a279-166">Vous devez toujours inclure l’élément `args` dans le fichier JSON même si sa valeur est `null`.</span><span class="sxs-lookup"><span data-stu-id="6a279-166">You should always include `args` in the JSON file even if it is `null`.</span></span>

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="6a279-167">À la fin de la configuration, nous établissons les connexions.</span><span class="sxs-lookup"><span data-stu-id="6a279-167">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="6a279-168">Chaque connexion est exprimée par `source` et `sink`.</span><span class="sxs-lookup"><span data-stu-id="6a279-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="6a279-169">Ces valeurs doivent faire référence à un module prédéfini.</span><span class="sxs-lookup"><span data-stu-id="6a279-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="6a279-170">Le message de sortie du module `source` sera transféré à l’entrée du module `sink`.</span><span class="sxs-lookup"><span data-stu-id="6a279-170">The output message of `source` module will be forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="6a279-171">Exécution des modules</span><span class="sxs-lookup"><span data-stu-id="6a279-171">Running the modules</span></span>

<span data-ttu-id="6a279-172">Utilisez `mvn package` pour générer tous les éléments dans le dossier `target/`.</span><span class="sxs-lookup"><span data-stu-id="6a279-172">Use `mvn package` to build everything into the `target/` folder.</span></span> <span data-ttu-id="6a279-173">`mvn clean package` est également recommandé pour créer un build propre.</span><span class="sxs-lookup"><span data-stu-id="6a279-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="6a279-174">Utilisez `mvn exec:exec` pour exécuter Azure IoT Edge, et vous pourrez observer que les données de température et toutes les propriétés sont imprimées vers la console à une fréquence fixe.</span><span class="sxs-lookup"><span data-stu-id="6a279-174">Use `mvn exec:exec` to run the Azure IoT Edge and you should observe that the temperature data and all the properties are printed to the console at a fixed rate.</span></span>

<span data-ttu-id="6a279-175">Si vous souhaitez arrêter l’application, appuyez sur la touche `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="6a279-175">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a279-176">Il est déconseillé d’utiliser Ctrl + C pour arrêter l’application de passerelle IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="6a279-176">It is not recommended to use Ctrl + C to terminate the IoT Edge gateway application.</span></span> <span data-ttu-id="6a279-177">Cela peut entraîner l’arrêt anormal du processus.</span><span class="sxs-lookup"><span data-stu-id="6a279-177">As this may cause the process to terminate abnormally.</span></span>

