---
title: aaaCreate un Module de bord Azure IoT avec Node.js | Documents Microsoft
description: "Ce didacticiel montre comment un ver données convertisseur module à l’aide de toowrite hello derniers packages Azure IoT bord NPM et Yeoman générateur."
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
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="0bf75-103">Créer un module Azure IoT Edge avec Node.js</span><span class="sxs-lookup"><span data-stu-id="0bf75-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="0bf75-104">Ce didacticiel présente comment toocreate un module pour Azure IoT arête JS.</span><span class="sxs-lookup"><span data-stu-id="0bf75-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="0bf75-105">Dans ce didacticiel, nous suivons la configuration de l’environnement et comment toowrite un [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) module de convertisseur de données à l’aide de packages de Azure IoT bord NPM hello plus récente.</span><span class="sxs-lookup"><span data-stu-id="0bf75-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bf75-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0bf75-106">Prerequisites</span></span>

<span data-ttu-id="0bf75-107">Dans cette section, vous configurez votre environnement pour le développement du module IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="0bf75-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="0bf75-108">Il s’applique tooboth *Windows 64 bits* et *64 bits Linux (Ubuntu + 14)* systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="0bf75-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="0bf75-109">Hello suivant logicielle est requise :</span><span class="sxs-lookup"><span data-stu-id="0bf75-109">hello following software is required:</span></span>
* <span data-ttu-id="0bf75-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="0bf75-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="0bf75-111">[LTS Node](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0bf75-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="0bf75-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="0bf75-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="0bf75-113">Architecture</span><span class="sxs-lookup"><span data-stu-id="0bf75-113">Architecture</span></span>

<span data-ttu-id="0bf75-114">plateforme de Azure IoT bord Hello adopte fortement hello [architecture de Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="0bf75-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="0bf75-115">Ce qui signifie que cette architecture d’Azure IoT bord entier hello est un système qui traite l’entrée et produit une sortie ; et que chaque module individuel est également un sous-système d’e / s minuscule.</span><span class="sxs-lookup"><span data-stu-id="0bf75-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="0bf75-116">Dans ce didacticiel, nous introduisons hello suivant deux modules :</span><span class="sxs-lookup"><span data-stu-id="0bf75-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="0bf75-117">Un module qui reçoit un signal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulé et le convertit en message au format [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="0bf75-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="0bf75-118">Un module qui imprime hello reçu [JSON](https://en.wikipedia.org/wiki/JSON) message.</span><span class="sxs-lookup"><span data-stu-id="0bf75-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="0bf75-119">Hello image suivante affiche hello fin classique tooend flux de données pour ce projet :</span><span class="sxs-lookup"><span data-stu-id="0bf75-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="0bf75-120">![Flux de données entre les trois modules](media/iot-hub-iot-edge-create-module/dataflow.png "Entrée : module BLE simulé ; processeur : module de convertisseur ; sortie : module d’imprimante")</span><span class="sxs-lookup"><span data-stu-id="0bf75-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="0bf75-121">Configuration d’environnement de hello</span><span class="sxs-lookup"><span data-stu-id="0bf75-121">Set up hello environment</span></span>
<span data-ttu-id="0bf75-122">Ci-dessous nous vous indiquons comment tooquickly configurer environnement toostart toowrite votre premier module de convertisseur BLE avec JS.</span><span class="sxs-lookup"><span data-stu-id="0bf75-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="0bf75-123">Créer le projet de module</span><span class="sxs-lookup"><span data-stu-id="0bf75-123">Create module project</span></span>
1. <span data-ttu-id="0bf75-124">Ouvrez une fenêtre de ligne de commande et exécutez `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="0bf75-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="0bf75-125">Suivez les étapes de hello lors de l’initialisation hello écran toofinish hello de votre projet de module.</span><span class="sxs-lookup"><span data-stu-id="0bf75-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="0bf75-126">Structure de projet</span><span class="sxs-lookup"><span data-stu-id="0bf75-126">Project structure</span></span>
<span data-ttu-id="0bf75-127">Un projet de module JS se compose de hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="0bf75-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="0bf75-128">`modules`-hello personnalisé les fichiers de source de module JS.</span><span class="sxs-lookup"><span data-stu-id="0bf75-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="0bf75-129">Remplacez la valeur par défaut hello `sensor.js` et `printer.js` avec vos propres fichiers de module.</span><span class="sxs-lookup"><span data-stu-id="0bf75-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="0bf75-130">`app.js`-instance de bord du fichier toostart hello hello entrée.</span><span class="sxs-lookup"><span data-stu-id="0bf75-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="0bf75-131">`gw.config.json`-hello configuration fichier toocustomize hello modules toobe chargé par le bord.</span><span class="sxs-lookup"><span data-stu-id="0bf75-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="0bf75-132">`package.json`-hello des informations de métadonnées pour un projet de module.</span><span class="sxs-lookup"><span data-stu-id="0bf75-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="0bf75-133">`README.md`-hello documentation de base pour le projet de module.</span><span class="sxs-lookup"><span data-stu-id="0bf75-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="0bf75-134">Fichier de package</span><span class="sxs-lookup"><span data-stu-id="0bf75-134">Package file</span></span>

<span data-ttu-id="0bf75-135">Cela `package.json` déclare toutes les informations de métadonnées hello requises par un projet de module qui inclut les dépendances de nom, version, écriture, scripts, runtime et développement hello.</span><span class="sxs-lookup"><span data-stu-id="0bf75-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="0bf75-136">Comment suivant montre le code extrait tooconfigure pour le convertisseur de BLE exemple de projet.</span><span class="sxs-lookup"><span data-stu-id="0bf75-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="0bf75-137">Fichier d’entrée</span><span class="sxs-lookup"><span data-stu-id="0bf75-137">Entry file</span></span>
<span data-ttu-id="0bf75-138">Hello `app.js` définit hello moyen tooinitialize hello bord instance.</span><span class="sxs-lookup"><span data-stu-id="0bf75-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="0bf75-139">Ici nous ne devons toomake toute modification.</span><span class="sxs-lookup"><span data-stu-id="0bf75-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="0bf75-140">Interface de module</span><span class="sxs-lookup"><span data-stu-id="0bf75-140">Interface of module</span></span>
<span data-ttu-id="0bf75-141">Vous pouvez traiter un module Azure IoT Edge comme un processeur de données dont la tâche consiste à : recevoir une entrée, la traiter et générer une sortie.</span><span class="sxs-lookup"><span data-stu-id="0bf75-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="0bf75-142">Hello entrée peut-être des données à partir du matériel (comme un détecteur de mouvement), un message à partir d’autres modules ou toute autre (par exemple, un nombre aléatoire généré régulièrement par un minuteur).</span><span class="sxs-lookup"><span data-stu-id="0bf75-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="0bf75-143">sortie de Hello est similaire toohello entrée, il risque de déclencher matériel comportement (hello clignote LED), un module de tooother message ou rien (comme l’impression toohello console).</span><span class="sxs-lookup"><span data-stu-id="0bf75-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="0bf75-144">Les modules communiquent entre eux à l’aide de l’objet `message`.</span><span class="sxs-lookup"><span data-stu-id="0bf75-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="0bf75-145">Hello **contenu** d’un `message` est un tableau d’octets qui est capable de représenter n’importe quel type de données de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0bf75-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="0bf75-146">**Propriétés** sont également disponibles dans hello `message` et sont simplement un mappage de chaîne en chaîne.</span><span class="sxs-lookup"><span data-stu-id="0bf75-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="0bf75-147">Vous pouvez vous représenter **propriétés** en tant qu’en-têtes hello dans une requête HTTP, ou métadonnées hello d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="0bf75-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="0bf75-148">Dans l’ordre toodevelop un module Azure IoT Edge dans JS, vous devez toocreate un nouvel objet du module qui implémente les méthodes hello requis `receive()`.</span><span class="sxs-lookup"><span data-stu-id="0bf75-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="0bf75-149">À ce stade, vous pouvez également choisir hello tooimplement facultatif `create()` ou `start()`, ou `destroy()` également les méthodes.</span><span class="sxs-lookup"><span data-stu-id="0bf75-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="0bf75-150">Hello suivant extrait de code montre que Hello à génération de modèles automatique de l’objet de module JS.</span><span class="sxs-lookup"><span data-stu-id="0bf75-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="0bf75-151">Module de convertisseur</span><span class="sxs-lookup"><span data-stu-id="0bf75-151">Converter module</span></span>
| <span data-ttu-id="0bf75-152">Entrée</span><span class="sxs-lookup"><span data-stu-id="0bf75-152">Input</span></span>                    | <span data-ttu-id="0bf75-153">Processeur</span><span class="sxs-lookup"><span data-stu-id="0bf75-153">Processor</span></span>                              | <span data-ttu-id="0bf75-154">Sortie</span><span class="sxs-lookup"><span data-stu-id="0bf75-154">Output</span></span>                 | <span data-ttu-id="0bf75-155">Fichier source</span><span class="sxs-lookup"><span data-stu-id="0bf75-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="0bf75-156">Message de données de température</span><span class="sxs-lookup"><span data-stu-id="0bf75-156">Temperature data message</span></span> | <span data-ttu-id="0bf75-157">Analyser et construire un nouveau message JSON</span><span class="sxs-lookup"><span data-stu-id="0bf75-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="0bf75-158">Structurer le message JSON</span><span class="sxs-lookup"><span data-stu-id="0bf75-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="0bf75-159">Ce module est un module Azure IoT Edge classique.</span><span class="sxs-lookup"><span data-stu-id="0bf75-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="0bf75-160">Il accepte des messages de température d’autres modules (un module de matériel, ou dans ce cas, notre module BLE simulé) ; puis normalise hello température message tooa structuré JSON message (y compris l’ajout des ID de message hello, définition de propriété hello de si nous devons alerte de température hello tootrigger et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="0bf75-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
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

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="0bf75-161">Module d’imprimante</span><span class="sxs-lookup"><span data-stu-id="0bf75-161">Printer module</span></span>
| <span data-ttu-id="0bf75-162">Entrée</span><span class="sxs-lookup"><span data-stu-id="0bf75-162">Input</span></span>                          | <span data-ttu-id="0bf75-163">Processeur</span><span class="sxs-lookup"><span data-stu-id="0bf75-163">Processor</span></span> | <span data-ttu-id="0bf75-164">Sortie</span><span class="sxs-lookup"><span data-stu-id="0bf75-164">Output</span></span>                     | <span data-ttu-id="0bf75-165">Fichier source</span><span class="sxs-lookup"><span data-stu-id="0bf75-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="0bf75-166">Tous les messages provenant d’autres modules</span><span class="sxs-lookup"><span data-stu-id="0bf75-166">Any message from other modules</span></span> | <span data-ttu-id="0bf75-167">N/A</span><span class="sxs-lookup"><span data-stu-id="0bf75-167">N/A</span></span>       | <span data-ttu-id="0bf75-168">Ouvrez une session hello message tooconsole</span><span class="sxs-lookup"><span data-stu-id="0bf75-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="0bf75-169">Ce module est simple et explicites, qui génère la fenêtre de terminal de toohello hello reçu les messages (propriété, le contenu).</span><span class="sxs-lookup"><span data-stu-id="0bf75-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="0bf75-170">Configuration</span><span class="sxs-lookup"><span data-stu-id="0bf75-170">Configuration</span></span>
<span data-ttu-id="0bf75-171">étape finale de Hello avant d’exécuter les modules hello est tooconfigure hello Azure IoT Edge et tooestablish hello connexions entre des modules.</span><span class="sxs-lookup"><span data-stu-id="0bf75-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="0bf75-172">Tout d’abord, nous devons toodeclare notre `node` chargeur (depuis Azure IoT Edge prend en charge les chargeurs de langues différentes), qui peut être référencé par son `name` dans les sections hello par la suite.</span><span class="sxs-lookup"><span data-stu-id="0bf75-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="0bf75-173">Une fois que nous avons déclaré notre chargeurs, nous devons également toodeclare nos modules également.</span><span class="sxs-lookup"><span data-stu-id="0bf75-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="0bf75-174">Les chargeurs de hello toodeclaring similaires, ils peuvent également être référencés par leurs `name` attribut.</span><span class="sxs-lookup"><span data-stu-id="0bf75-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="0bf75-175">Lorsque vous déclarez un module, nous devons toospecify hello du chargeur doit être utilisé (qui doit être hello une nous avons défini avant) et hello point d’entrée (doit être le nom de classe normalisé hello de notre module) pour chaque module.</span><span class="sxs-lookup"><span data-stu-id="0bf75-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="0bf75-176">Hello `simulated_device` module est un module natif qui est inclus dans le package de runtime hello Azure IoT bord core.</span><span class="sxs-lookup"><span data-stu-id="0bf75-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="0bf75-177">Inclure `args` Bonjour, même s’il s’agit du fichier JSON `null`.</span><span class="sxs-lookup"><span data-stu-id="0bf75-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="0bf75-178">Extrémité hello de configuration de hello, nous établir des connexions de hello.</span><span class="sxs-lookup"><span data-stu-id="0bf75-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="0bf75-179">Chaque connexion est exprimée par `source` et `sink`.</span><span class="sxs-lookup"><span data-stu-id="0bf75-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="0bf75-180">Ces valeurs doivent faire référence à un module prédéfini.</span><span class="sxs-lookup"><span data-stu-id="0bf75-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="0bf75-181">message de sortie de type Hello `source` module est transféré entrée toohello `sink` module.</span><span class="sxs-lookup"><span data-stu-id="0bf75-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="0bf75-182">Modules hello en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="0bf75-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="0bf75-183">Si vous souhaitez tooterminate hello application, appuyez sur `<Enter>` clé.</span><span class="sxs-lookup"><span data-stu-id="0bf75-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bf75-184">Il est déconseillé de toouse Ctrl + C tooterminate hello IoT bord application.</span><span class="sxs-lookup"><span data-stu-id="0bf75-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="0bf75-185">Comme cette façon peut provoquer hello processus tooterminate anormalement.</span><span class="sxs-lookup"><span data-stu-id="0bf75-185">As this way may cause hello process tooterminate abnormally.</span></span>
