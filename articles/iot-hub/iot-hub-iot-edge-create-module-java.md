---
title: aaaCreate un Module de bord Azure IoT avec Java | Documents Microsoft
description: "Ce didacticiel montre comment un ver données convertisseur module à l’aide de toowrite hello derniers packages Azure IoT bord Maven."
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
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="4466d-103">Créer un module Azure IoT Edge avec Java</span><span class="sxs-lookup"><span data-stu-id="4466d-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="4466d-104">Ce didacticiel explique comment vous pouvez créer un module pour Azure IoT Edge en Java.</span><span class="sxs-lookup"><span data-stu-id="4466d-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="4466d-105">Dans ce didacticiel, nous allons découvrir la configuration de l’environnement et comment toowrite un [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) module de convertisseur de données à l’aide de packages de Azure IoT bord Maven hello plus récente.</span><span class="sxs-lookup"><span data-stu-id="4466d-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4466d-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4466d-106">Prerequisites</span></span>

<span data-ttu-id="4466d-107">Dans cette section, vous allez configurer votre environnement pour le développement du module IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4466d-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="4466d-108">Il s’applique tooboth *Windows 64 bits* et *64 bits Linux (8 Ubuntu/Debian)* systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="4466d-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="4466d-109">Hello suivant logicielle est requise :</span><span class="sxs-lookup"><span data-stu-id="4466d-109">hello following software is required:</span></span>

* <span data-ttu-id="4466d-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="4466d-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="4466d-111">[JDK **x64**](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="4466d-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="4466d-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="4466d-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="4466d-113">Ouvrez un en ligne de commande terminal fenêtre et clone hello suivant du référentiel :</span><span class="sxs-lookup"><span data-stu-id="4466d-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="4466d-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="4466d-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="4466d-115">Architecture globale</span><span class="sxs-lookup"><span data-stu-id="4466d-115">Overall architecture</span></span>

<span data-ttu-id="4466d-116">plateforme de Azure IoT bord Hello adopte fortement hello [architecture de Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="4466d-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="4466d-117">Ce qui signifie que cette architecture d’Azure IoT bord entier hello est un système qui traite l’entrée et produit une sortie ; et que chaque module individuel est également un sous-système d’e / s minuscule.</span><span class="sxs-lookup"><span data-stu-id="4466d-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="4466d-118">Dans ce didacticiel, nous allons présenter hello suivant deux modules :</span><span class="sxs-lookup"><span data-stu-id="4466d-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="4466d-119">Un module qui reçoit un signal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulé et qui le convertit en message au format [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="4466d-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="4466d-120">Un module qui imprime hello reçu [JSON](https://en.wikipedia.org/wiki/JSON) message.</span><span class="sxs-lookup"><span data-stu-id="4466d-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="4466d-121">Hello image suivante affiche hello les classique au bout de flux de données pour ce projet :</span><span class="sxs-lookup"><span data-stu-id="4466d-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="4466d-122">![Flux de données entre les trois modules](media/iot-hub-iot-edge-create-module/dataflow.png "Entrée : module BLE simulé ; processeur : module de convertisseur ; sortie : module d’imprimante")</span><span class="sxs-lookup"><span data-stu-id="4466d-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="4466d-123">Description du code hello</span><span class="sxs-lookup"><span data-stu-id="4466d-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="4466d-124">Structure du projet Maven</span><span class="sxs-lookup"><span data-stu-id="4466d-124">Maven project structure</span></span>

<span data-ttu-id="4466d-125">Étant donné que les packages Azure IoT Edge sont basées sur Maven, nous devons toocreate une structure de projet Maven classique, qui contient un `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="4466d-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="4466d-126">Hello POM hérite hello `com.microsoft.azure.gateway.gateway-module-base` package, qui déclare toutes les dépendances hello requises par un projet de module qui inclut les fichiers binaires du runtime hello, chemin de fichier de configuration de passerelle hello et le comportement de l’exécution de hello.</span><span class="sxs-lookup"><span data-stu-id="4466d-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="4466d-127">Cela nous évite beaucoup de temps et éliminer hello besoin toowrite et réécrire des centaines de lignes de code indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="4466d-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="4466d-128">Nous devons tooupdate le fichier pom.xml en déclarant hello requis dépendances/plug-ins et nom hello de toobe de fichier de configuration hello utilisé par notre module, comme illustré dans hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="4466d-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

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

  <!-- Set hello filename of hello Azure IoT Edge configuration located
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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="4466d-129">Compréhension élémentaire d’un module Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4466d-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="4466d-130">Vous pouvez traiter un module Azure IoT Edge comme un processeur de données dont la tâche consiste à : recevoir une entrée, la traiter et générer une sortie.</span><span class="sxs-lookup"><span data-stu-id="4466d-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="4466d-131">Hello entrée peut-être des données à partir du matériel (comme un détecteur de mouvement), un message à partir d’autres modules ou toute autre (par exemple, un nombre aléatoire généré régulièrement par un minuteur).</span><span class="sxs-lookup"><span data-stu-id="4466d-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="4466d-132">sortie de Hello est similaire toohello entrée, il risque de déclencher matériel comportement (hello clignote LED), un module de tooother message ou rien (comme l’impression toohello console).</span><span class="sxs-lookup"><span data-stu-id="4466d-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="4466d-133">Les modules communiquent entre eux à l’aide de la classe `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="4466d-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="4466d-134">Hello **contenu** d’un `Message` est un tableau d’octets qui est capable de représenter n’importe quel type de données de votre choix.</span><span class="sxs-lookup"><span data-stu-id="4466d-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="4466d-135">**Propriétés** sont également disponibles dans hello `Message` et sont simplement un mappage de chaîne en chaîne.</span><span class="sxs-lookup"><span data-stu-id="4466d-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="4466d-136">Vous pouvez vous représenter **propriétés** en tant qu’en-têtes hello dans une requête HTTP, ou métadonnées hello d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="4466d-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="4466d-137">Dans l’ordre toodevelop un module Azure IoT Edge dans Java, vous devez toocreate une nouvelle classe de module qui hérite de `com.microsoft.azure.gateway.core.GatewayModule` et implémenter les méthodes abstraites hello requis `receive()` et `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="4466d-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="4466d-138">À ce stade, vous pouvez également choisir hello tooimplement facultatif `start()` ou `create()` également les méthodes.</span><span class="sxs-lookup"><span data-stu-id="4466d-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="4466d-139">Hello suivant extrait de code montre comment tooget démarrer la création d’un module Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4466d-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="4466d-140">Module de convertisseur</span><span class="sxs-lookup"><span data-stu-id="4466d-140">Converter module</span></span>

| <span data-ttu-id="4466d-141">Entrée</span><span class="sxs-lookup"><span data-stu-id="4466d-141">Input</span></span>                    | <span data-ttu-id="4466d-142">Processeur</span><span class="sxs-lookup"><span data-stu-id="4466d-142">Processor</span></span>                              | <span data-ttu-id="4466d-143">Sortie</span><span class="sxs-lookup"><span data-stu-id="4466d-143">Output</span></span>                 | <span data-ttu-id="4466d-144">Fichier source</span><span class="sxs-lookup"><span data-stu-id="4466d-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="4466d-145">Message de données de température</span><span class="sxs-lookup"><span data-stu-id="4466d-145">Temperature data message</span></span> | <span data-ttu-id="4466d-146">Analyser et construire un nouveau message JSON</span><span class="sxs-lookup"><span data-stu-id="4466d-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="4466d-147">Structurer le message JSON</span><span class="sxs-lookup"><span data-stu-id="4466d-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="4466d-148">Ce module est un module Azure IoT Edge classique.</span><span class="sxs-lookup"><span data-stu-id="4466d-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="4466d-149">Il accepte des messages de température d’autres modules (un module de matériel, ou dans ce cas, notre module BLE simulé) ; puis normalise hello température message tooa structuré JSON message (y compris l’ajout des ID de message hello, définition de propriété hello de si nous devons alerte de température hello tootrigger et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="4466d-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="4466d-150">Module d’imprimante</span><span class="sxs-lookup"><span data-stu-id="4466d-150">Printer module</span></span>

| <span data-ttu-id="4466d-151">Entrée</span><span class="sxs-lookup"><span data-stu-id="4466d-151">Input</span></span>                          | <span data-ttu-id="4466d-152">Processeur</span><span class="sxs-lookup"><span data-stu-id="4466d-152">Processor</span></span> | <span data-ttu-id="4466d-153">Sortie</span><span class="sxs-lookup"><span data-stu-id="4466d-153">Output</span></span>                     | <span data-ttu-id="4466d-154">Fichier source</span><span class="sxs-lookup"><span data-stu-id="4466d-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="4466d-155">Tous les messages provenant d’autres modules</span><span class="sxs-lookup"><span data-stu-id="4466d-155">Any message from other modules</span></span> | <span data-ttu-id="4466d-156">N/A</span><span class="sxs-lookup"><span data-stu-id="4466d-156">N/A</span></span>       | <span data-ttu-id="4466d-157">Ouvrez une session hello message tooconsole</span><span class="sxs-lookup"><span data-stu-id="4466d-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="4466d-158">Il s’agit d’un module de simple et explicite, qui génère la fenêtre de terminal toohello messages hello reçu.</span><span class="sxs-lookup"><span data-stu-id="4466d-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="4466d-159">Configuration d’Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4466d-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="4466d-160">étape finale de Hello avant d’exécuter les modules hello est tooconfigure hello Azure IoT Edge et tooestablish hello connexions entre des modules.</span><span class="sxs-lookup"><span data-stu-id="4466d-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="4466d-161">Nous devons abord toodeclare notre chargeur Java (depuis Azure IoT Edge prend en charge les chargeurs de langues différentes), qui peut être référencé par son `name` dans les sections hello par la suite.</span><span class="sxs-lookup"><span data-stu-id="4466d-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

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

<span data-ttu-id="4466d-162">Une fois que nous avons déclaré notre chargeurs, nous devez également toodeclare nos modules également.</span><span class="sxs-lookup"><span data-stu-id="4466d-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="4466d-163">Les chargeurs de hello toodeclaring similaires, ils peuvent également être référencés par leurs `name` attribut.</span><span class="sxs-lookup"><span data-stu-id="4466d-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="4466d-164">Lorsque vous déclarez un module, nous devons toospecify hello du chargeur doit être utilisé (qui doit être hello une nous avons défini avant) et hello point d’entrée (doit être le nom de classe normalisé hello de notre module) pour chaque module.</span><span class="sxs-lookup"><span data-stu-id="4466d-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="4466d-165">Hello `simulated_device` module est un module natif qui est inclus dans le package de runtime hello Azure IoT bord core.</span><span class="sxs-lookup"><span data-stu-id="4466d-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="4466d-166">Vous devez toujours inclure `args` Bonjour, même s’il s’agit du fichier JSON `null`.</span><span class="sxs-lookup"><span data-stu-id="4466d-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="4466d-167">Extrémité hello de configuration de hello, nous établir des connexions de hello.</span><span class="sxs-lookup"><span data-stu-id="4466d-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="4466d-168">Chaque connexion est exprimée par `source` et `sink`.</span><span class="sxs-lookup"><span data-stu-id="4466d-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="4466d-169">Ces valeurs doivent faire référence à un module prédéfini.</span><span class="sxs-lookup"><span data-stu-id="4466d-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="4466d-170">message de sortie de type Hello `source` module sera transféré entrée toohello `sink` module.</span><span class="sxs-lookup"><span data-stu-id="4466d-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="4466d-171">Modules hello en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="4466d-171">Running hello modules</span></span>

<span data-ttu-id="4466d-172">Utilisez `mvn package` toobuild tout en hello `target/` dossier.</span><span class="sxs-lookup"><span data-stu-id="4466d-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="4466d-173">`mvn clean package` est également recommandé pour créer un build propre.</span><span class="sxs-lookup"><span data-stu-id="4466d-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="4466d-174">Utilisez `mvn exec:exec` toorun hello Azure IoT Edge et vous devez observer que les données de température hello et toutes les propriétés de hello sont console toohello imprimé à un taux fixe.</span><span class="sxs-lookup"><span data-stu-id="4466d-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="4466d-175">Si vous souhaitez tooterminate hello application, appuyez sur `<Enter>` clé.</span><span class="sxs-lookup"><span data-stu-id="4466d-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4466d-176">Il est déconseillé de toouse Ctrl + C tooterminate hello IoT bord application passerelle.</span><span class="sxs-lookup"><span data-stu-id="4466d-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="4466d-177">Car cela pourrait provoquer hello processus tooterminate anormalement.</span><span class="sxs-lookup"><span data-stu-id="4466d-177">As this may cause hello process tooterminate abnormally.</span></span>

