---
title: "Créer un module Azure IoT Edge avec Node.js | Microsoft Docs"
description: "Ce didacticiel explique comment écrire un module de convertisseur de données BLE en utilisant les derniers packages NPM Azure IoT Edge et le générateur Yeoman."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="2dd89-103">Créer un module Azure IoT Edge avec Node.js</span><span class="sxs-lookup"><span data-stu-id="2dd89-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="2dd89-104">Ce didacticiel explique comment créer un module pour Azure IoT Edge en JS.</span><span class="sxs-lookup"><span data-stu-id="2dd89-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="2dd89-105">Dans ce didacticiel, nous aborderons la configuration de l’environnement et expliquerons comment écrire un module de convertisseur de données [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) en utilisant les derniers packages NPM Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="2dd89-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dd89-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2dd89-106">Prerequisites</span></span>

<span data-ttu-id="2dd89-107">Dans cette section, vous configurez votre environnement pour le développement du module IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="2dd89-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="2dd89-108">Cela s’applique aux systèmes d’exploitation *Windows 64 bits* et *Linux 64 bits (Ubuntu 14+)*.</span><span class="sxs-lookup"><span data-stu-id="2dd89-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="2dd89-109">Les logiciels suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="2dd89-109">The following software is required:</span></span>
* <span data-ttu-id="2dd89-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2dd89-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="2dd89-111">[LTS Node](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="2dd89-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="2dd89-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="2dd89-113">Architecture</span><span class="sxs-lookup"><span data-stu-id="2dd89-113">Architecture</span></span>

<span data-ttu-id="2dd89-114">La plateforme Azure IoT Edge adopte fortement [l’architecture de Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="2dd89-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="2dd89-115">Cela signifie que l’ensemble de l’architecture Azure IoT Edge est un système qui traite une entrée et produit une sortie, et que chaque module individuel est également un minuscule sous-système d’entrée-de sortie.</span><span class="sxs-lookup"><span data-stu-id="2dd89-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="2dd89-116">Dans ce didacticiel, nous présentons les deux modules suivants :</span><span class="sxs-lookup"><span data-stu-id="2dd89-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="2dd89-117">Un module qui reçoit un signal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulé et le convertit en message au format [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="2dd89-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="2dd89-118">Un module qui imprime le message [JSON](https://en.wikipedia.org/wiki/JSON) reçu.</span><span class="sxs-lookup"><span data-stu-id="2dd89-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="2dd89-119">L’image suivante affiche le flux de données de bout en bout classique pour ce projet :</span><span class="sxs-lookup"><span data-stu-id="2dd89-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="2dd89-120">![Flux de données entre les trois modules](media/iot-hub-iot-edge-create-module/dataflow.png "Entrée : module BLE simulé ; processeur : module de convertisseur ; sortie : module d’imprimante")</span><span class="sxs-lookup"><span data-stu-id="2dd89-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="2dd89-121">Configurer l’environnement</span><span class="sxs-lookup"><span data-stu-id="2dd89-121">Set up the environment</span></span>
<span data-ttu-id="2dd89-122">Nous vous montrons ci-après comment configurer rapidement l’environnement pour commencer à écrire votre premier module de convertisseur BLE avec JS.</span><span class="sxs-lookup"><span data-stu-id="2dd89-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="2dd89-123">Créer le projet de module</span><span class="sxs-lookup"><span data-stu-id="2dd89-123">Create module project</span></span>
1. <span data-ttu-id="2dd89-124">Ouvrez une fenêtre de ligne de commande et exécutez `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="2dd89-125">Suivez les étapes à l’écran pour terminer l’initialisation de votre projet de module.</span><span class="sxs-lookup"><span data-stu-id="2dd89-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="2dd89-126">Structure de projet</span><span class="sxs-lookup"><span data-stu-id="2dd89-126">Project structure</span></span>
<span data-ttu-id="2dd89-127">Un projet de module JS est constitué des composants suivants :</span><span class="sxs-lookup"><span data-stu-id="2dd89-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="2dd89-128">`modules` - Les fichiers source du module JS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2dd89-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="2dd89-129">Remplacez les valeurs par défaut `sensor.js` et `printer.js` par vos propres fichiers de module.</span><span class="sxs-lookup"><span data-stu-id="2dd89-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="2dd89-130">`app.js` - Le fichier d’entrée pour démarrer l’instance Edge.</span><span class="sxs-lookup"><span data-stu-id="2dd89-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="2dd89-131">`gw.config.json` - Le fichier config pour personnaliser les modules à charger par Edge.</span><span class="sxs-lookup"><span data-stu-id="2dd89-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="2dd89-132">`package.json` - Les informations de métadonnées pour le projet de module.</span><span class="sxs-lookup"><span data-stu-id="2dd89-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="2dd89-133">`README.md` - La documentation de base pour le projet de module.</span><span class="sxs-lookup"><span data-stu-id="2dd89-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="2dd89-134">Fichier de package</span><span class="sxs-lookup"><span data-stu-id="2dd89-134">Package file</span></span>

<span data-ttu-id="2dd89-135">Cet élément `package.json` déclare toutes les informations de métadonnées requises par un projet de module incluant le nom, la version, l’entrée, les scripts, le runtime et les dépendances de développement.</span><span class="sxs-lookup"><span data-stu-id="2dd89-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="2dd89-136">L’extrait de code suivant illustre la configuration de l’exemple de projet de convertisseur BLE.</span><span class="sxs-lookup"><span data-stu-id="2dd89-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a><span data-ttu-id="2dd89-137">Fichier d’entrée</span><span class="sxs-lookup"><span data-stu-id="2dd89-137">Entry file</span></span>
<span data-ttu-id="2dd89-138">L’élément `app.js` définit la façon dont l’instance Edge est initialisée.</span><span class="sxs-lookup"><span data-stu-id="2dd89-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="2dd89-139">Ici, nous n’avons pas besoin d’apporter de modifications.</span><span class="sxs-lookup"><span data-stu-id="2dd89-139">Here we don't need to make any change.</span></span>

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a><span data-ttu-id="2dd89-140">Interface de module</span><span class="sxs-lookup"><span data-stu-id="2dd89-140">Interface of module</span></span>
<span data-ttu-id="2dd89-141">Vous pouvez traiter un module Azure IoT Edge comme un processeur de données dont la tâche consiste à : recevoir une entrée, la traiter et générer une sortie.</span><span class="sxs-lookup"><span data-stu-id="2dd89-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="2dd89-142">L’entrée peut être des données issues du matériel (comme un détecteur de mouvement), un message provenant d’autres modules ou toute autre chose (par exemple, un nombre aléatoire généré régulièrement par un minuteur).</span><span class="sxs-lookup"><span data-stu-id="2dd89-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="2dd89-143">La sortie est similaire à l’entrée, elle peut déclencher le comportement du matériel (comme le clignotement d’une LED), un message à d’autres modules ou toute autre chose (par exemple, une impression vers la console).</span><span class="sxs-lookup"><span data-stu-id="2dd89-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="2dd89-144">Les modules communiquent entre eux à l’aide de l’objet `message`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="2dd89-145">Le **contenu** d’un `message` est un tableau d’octets qui est capable de représenter n’importe quel type de données de votre choix.</span><span class="sxs-lookup"><span data-stu-id="2dd89-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="2dd89-146">Les **propriétés** sont également disponibles dans le `message` et sont simplement un mappage de chaîne à chaîne.</span><span class="sxs-lookup"><span data-stu-id="2dd89-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="2dd89-147">Vous pouvez imaginer les **propriétés** comme étant les en-têtes d’une demande HTTP ou les métadonnées d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="2dd89-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="2dd89-148">Pour développer un module Azure IoT Edge en JS, vous devez créer un nouvel objet de module qui implémente les méthodes requises `receive()`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="2dd89-149">À ce stade, vous pouvez également choisir d’implémenter les méthodes `create()`, `start()` ou `destroy()` facultatives.</span><span class="sxs-lookup"><span data-stu-id="2dd89-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="2dd89-150">L’extrait de code suivant vous montre la structure de l’objet de module JS.</span><span class="sxs-lookup"><span data-stu-id="2dd89-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a><span data-ttu-id="2dd89-151">Module de convertisseur</span><span class="sxs-lookup"><span data-stu-id="2dd89-151">Converter module</span></span>
| <span data-ttu-id="2dd89-152">Entrée</span><span class="sxs-lookup"><span data-stu-id="2dd89-152">Input</span></span>                    | <span data-ttu-id="2dd89-153">Processeur</span><span class="sxs-lookup"><span data-stu-id="2dd89-153">Processor</span></span>                              | <span data-ttu-id="2dd89-154">Sortie</span><span class="sxs-lookup"><span data-stu-id="2dd89-154">Output</span></span>                 | <span data-ttu-id="2dd89-155">Fichier source</span><span class="sxs-lookup"><span data-stu-id="2dd89-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="2dd89-156">Message de données de température</span><span class="sxs-lookup"><span data-stu-id="2dd89-156">Temperature data message</span></span> | <span data-ttu-id="2dd89-157">Analyser et construire un nouveau message JSON</span><span class="sxs-lookup"><span data-stu-id="2dd89-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="2dd89-158">Structurer le message JSON</span><span class="sxs-lookup"><span data-stu-id="2dd89-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="2dd89-159">Ce module est un module Azure IoT Edge classique.</span><span class="sxs-lookup"><span data-stu-id="2dd89-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="2dd89-160">Il accepte des messages de température provenant d’autres modules (un module de matériel, ou dans notre cas, notre module BLE simulé), puis normalise le message de température dans un message JSON structuré (y compris l’ajout de l’ID de message, la définition de la propriété indiquant si nous devons déclencher l’alerte de température, etc.).</span><span class="sxs-lookup"><span data-stu-id="2dd89-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="2dd89-161">Module d’imprimante</span><span class="sxs-lookup"><span data-stu-id="2dd89-161">Printer module</span></span>
| <span data-ttu-id="2dd89-162">Entrée</span><span class="sxs-lookup"><span data-stu-id="2dd89-162">Input</span></span>                          | <span data-ttu-id="2dd89-163">Processeur</span><span class="sxs-lookup"><span data-stu-id="2dd89-163">Processor</span></span> | <span data-ttu-id="2dd89-164">Sortie</span><span class="sxs-lookup"><span data-stu-id="2dd89-164">Output</span></span>                     | <span data-ttu-id="2dd89-165">Fichier source</span><span class="sxs-lookup"><span data-stu-id="2dd89-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="2dd89-166">Tous les messages provenant d’autres modules</span><span class="sxs-lookup"><span data-stu-id="2dd89-166">Any message from other modules</span></span> | <span data-ttu-id="2dd89-167">N/A</span><span class="sxs-lookup"><span data-stu-id="2dd89-167">N/A</span></span>       | <span data-ttu-id="2dd89-168">Enregistrer le message sur la console</span><span class="sxs-lookup"><span data-stu-id="2dd89-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="2dd89-169">Ce module est simple, explicite et génère les messages reçus (propriété, contenu) dans la fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="2dd89-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="2dd89-170">Configuration</span><span class="sxs-lookup"><span data-stu-id="2dd89-170">Configuration</span></span>
<span data-ttu-id="2dd89-171">La dernière étape avant d’exécuter les modules consiste à configurer Azure IoT Edge et à établir les connexions entre les modules.</span><span class="sxs-lookup"><span data-stu-id="2dd89-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="2dd89-172">Tout d’abord, nous devons déclarer notre chargeur `node` (étant donné qu’Azure IoT Edge prend en charge des chargeurs de différents langages) qui peut, par la suite, être référencé par son `name` dans les sections.</span><span class="sxs-lookup"><span data-stu-id="2dd89-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="2dd89-173">Une fois que nous avons déclaré nos chargeurs, nous devons également déclarer nos modules.</span><span class="sxs-lookup"><span data-stu-id="2dd89-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="2dd89-174">À l’instar de la déclaration des chargeurs, les modules peuvent aussi être référencés par leur attribut `name`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="2dd89-175">Lors de la déclaration d’un module, nous devons spécifier le chargeur qu’il doit utiliser (qui doit être celui que nous avons défini avant) et le point d’entrée (qui doit être le nom de la classe normalisé de notre module) pour chaque module.</span><span class="sxs-lookup"><span data-stu-id="2dd89-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="2dd89-176">Le module `simulated_device` est un module natif qui est inclus dans le package de runtime principal Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="2dd89-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="2dd89-177">Ajoutez l’élément `args` dans le fichier JSON même si sa valeur est `null`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-177">Include `args` in the JSON file even if it is `null`.</span></span>

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
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="2dd89-178">À la fin de la configuration, nous établissons les connexions.</span><span class="sxs-lookup"><span data-stu-id="2dd89-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="2dd89-179">Chaque connexion est exprimée par `source` et `sink`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="2dd89-180">Ces valeurs doivent faire référence à un module prédéfini.</span><span class="sxs-lookup"><span data-stu-id="2dd89-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="2dd89-181">Le message de sortie du module `source` est transféré à l’entrée du module `sink`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="2dd89-182">Exécution des modules</span><span class="sxs-lookup"><span data-stu-id="2dd89-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="2dd89-183">Si vous souhaitez arrêter l’application, appuyez sur la touche `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="2dd89-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dd89-184">Il est déconseillé d’utiliser Ctrl + C pour arrêter l’application IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="2dd89-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="2dd89-185">Cela peut entraîner l’arrêt anormal du processus.</span><span class="sxs-lookup"><span data-stu-id="2dd89-185">As this way may cause the process to terminate abnormally.</span></span>
