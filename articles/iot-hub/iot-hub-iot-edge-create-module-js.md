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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Créer un module Azure IoT Edge avec Node.js

Ce didacticiel présente comment toocreate un module pour Azure IoT arête JS.

Dans ce didacticiel, nous suivons la configuration de l’environnement et comment toowrite un [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) module de convertisseur de données à l’aide de packages de Azure IoT bord NPM hello plus récente.

## <a name="prerequisites"></a>Composants requis

Dans cette section, vous configurez votre environnement pour le développement du module IoT Edge. Il s’applique tooboth *Windows 64 bits* et *64 bits Linux (Ubuntu + 14)* systèmes d’exploitation.

Hello suivant logicielle est requise :
* [Client Git](https://git-scm.com/downloads).
* [LTS Node](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Architecture

plateforme de Azure IoT bord Hello adopte fortement hello [architecture de Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Ce qui signifie que cette architecture d’Azure IoT bord entier hello est un système qui traite l’entrée et produit une sortie ; et que chaque module individuel est également un sous-système d’e / s minuscule. Dans ce didacticiel, nous introduisons hello suivant deux modules :

1. Un module qui reçoit un signal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulé et le convertit en message au format [JSON](https://en.wikipedia.org/wiki/JSON).
2. Un module qui imprime hello reçu [JSON](https://en.wikipedia.org/wiki/JSON) message.

Hello image suivante affiche hello fin classique tooend flux de données pour ce projet :

![Flux de données entre les trois modules](media/iot-hub-iot-edge-create-module/dataflow.png "Entrée : module BLE simulé ; processeur : module de convertisseur ; sortie : module d’imprimante")

## <a name="set-up-hello-environment"></a>Configuration d’environnement de hello
Ci-dessous nous vous indiquons comment tooquickly configurer environnement toostart toowrite votre premier module de convertisseur BLE avec JS.

### <a name="create-module-project"></a>Créer le projet de module
1. Ouvrez une fenêtre de ligne de commande et exécutez `yo az-iot-gw-module`.
2. Suivez les étapes de hello lors de l’initialisation hello écran toofinish hello de votre projet de module.

### <a name="project-structure"></a>Structure de projet
Un projet de module JS se compose de hello suivant des composants :

`modules`-hello personnalisé les fichiers de source de module JS. Remplacez la valeur par défaut hello `sensor.js` et `printer.js` avec vos propres fichiers de module.

`app.js`-instance de bord du fichier toostart hello hello entrée.

`gw.config.json`-hello configuration fichier toocustomize hello modules toobe chargé par le bord.

`package.json`-hello des informations de métadonnées pour un projet de module.

`README.md`-hello documentation de base pour le projet de module.


### <a name="package-file"></a>Fichier de package

Cela `package.json` déclare toutes les informations de métadonnées hello requises par un projet de module qui inclut les dépendances de nom, version, écriture, scripts, runtime et développement hello.

Comment suivant montre le code extrait tooconfigure pour le convertisseur de BLE exemple de projet.
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


### <a name="entry-file"></a>Fichier d’entrée
Hello `app.js` définit hello moyen tooinitialize hello bord instance. Ici nous ne devons toomake toute modification.

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

### <a name="interface-of-module"></a>Interface de module
Vous pouvez traiter un module Azure IoT Edge comme un processeur de données dont la tâche consiste à : recevoir une entrée, la traiter et générer une sortie.

Hello entrée peut-être des données à partir du matériel (comme un détecteur de mouvement), un message à partir d’autres modules ou toute autre (par exemple, un nombre aléatoire généré régulièrement par un minuteur).

sortie de Hello est similaire toohello entrée, il risque de déclencher matériel comportement (hello clignote LED), un module de tooother message ou rien (comme l’impression toohello console).

Les modules communiquent entre eux à l’aide de l’objet `message`. Hello **contenu** d’un `message` est un tableau d’octets qui est capable de représenter n’importe quel type de données de votre choix. **Propriétés** sont également disponibles dans hello `message` et sont simplement un mappage de chaîne en chaîne. Vous pouvez vous représenter **propriétés** en tant qu’en-têtes hello dans une requête HTTP, ou métadonnées hello d’un fichier.

Dans l’ordre toodevelop un module Azure IoT Edge dans JS, vous devez toocreate un nouvel objet du module qui implémente les méthodes hello requis `receive()`. À ce stade, vous pouvez également choisir hello tooimplement facultatif `create()` ou `start()`, ou `destroy()` également les méthodes. Hello suivant extrait de code montre que Hello à génération de modèles automatique de l’objet de module JS.

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

### <a name="converter-module"></a>Module de convertisseur
| Entrée                    | Processeur                              | Sortie                 | Fichier source            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Message de données de température | Analyser et construire un nouveau message JSON | Structurer le message JSON | `converter.js` |

Ce module est un module Azure IoT Edge classique. Il accepte des messages de température d’autres modules (un module de matériel, ou dans ce cas, notre module BLE simulé) ; puis normalise hello température message tooa structuré JSON message (y compris l’ajout des ID de message hello, définition de propriété hello de si nous devons alerte de température hello tootrigger et ainsi de suite).

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

### <a name="printer-module"></a>Module d’imprimante
| Entrée                          | Processeur | Sortie                     | Fichier source          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Tous les messages provenant d’autres modules | N/A       | Ouvrez une session hello message tooconsole | `printer.js` |

Ce module est simple et explicites, qui génère la fenêtre de terminal de toohello hello reçu les messages (propriété, le contenu).

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Configuration
étape finale de Hello avant d’exécuter les modules hello est tooconfigure hello Azure IoT Edge et tooestablish hello connexions entre des modules.

Tout d’abord, nous devons toodeclare notre `node` chargeur (depuis Azure IoT Edge prend en charge les chargeurs de langues différentes), qui peut être référencé par son `name` dans les sections hello par la suite.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Une fois que nous avons déclaré notre chargeurs, nous devons également toodeclare nos modules également. Les chargeurs de hello toodeclaring similaires, ils peuvent également être référencés par leurs `name` attribut. Lorsque vous déclarez un module, nous devons toospecify hello du chargeur doit être utilisé (qui doit être hello une nous avons défini avant) et hello point d’entrée (doit être le nom de classe normalisé hello de notre module) pour chaque module. Hello `simulated_device` module est un module natif qui est inclus dans le package de runtime hello Azure IoT bord core. Inclure `args` Bonjour, même s’il s’agit du fichier JSON `null`.

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

Extrémité hello de configuration de hello, nous établir des connexions de hello. Chaque connexion est exprimée par `source` et `sink`. Ces valeurs doivent faire référence à un module prédéfini. message de sortie de type Hello `source` module est transféré entrée toohello `sink` module.

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

## <a name="running-hello-modules"></a>Modules hello en cours d’exécution
1. `npm install`
2. `npm start`

Si vous souhaitez tooterminate hello application, appuyez sur `<Enter>` clé.

> [!IMPORTANT]
> Il est déconseillé de toouse Ctrl + C tooterminate hello IoT bord application. Comme cette façon peut provoquer hello processus tooterminate anormalement.
