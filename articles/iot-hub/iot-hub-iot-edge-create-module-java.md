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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Créer un module Azure IoT Edge avec Java

Ce didacticiel explique comment vous pouvez créer un module pour Azure IoT Edge en Java.

Dans ce didacticiel, nous allons découvrir la configuration de l’environnement et comment toowrite un [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) module de convertisseur de données à l’aide de packages de Azure IoT bord Maven hello plus récente.

## <a name="prerequisites"></a>Composants requis

Dans cette section, vous allez configurer votre environnement pour le développement du module IoT Edge. Il s’applique tooboth *Windows 64 bits* et *64 bits Linux (8 Ubuntu/Debian)* systèmes d’exploitation.

Hello suivant logicielle est requise :

* [Client Git](https://git-scm.com/downloads).
* [JDK **x64**](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Ouvrez un en ligne de commande terminal fenêtre et clone hello suivant du référentiel :

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Architecture globale

plateforme de Azure IoT bord Hello adopte fortement hello [architecture de Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Ce qui signifie que cette architecture d’Azure IoT bord entier hello est un système qui traite l’entrée et produit une sortie ; et que chaque module individuel est également un sous-système d’e / s minuscule. Dans ce didacticiel, nous allons présenter hello suivant deux modules :

1. Un module qui reçoit un signal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulé et qui le convertit en message au format [JSON](https://en.wikipedia.org/wiki/JSON).
2. Un module qui imprime hello reçu [JSON](https://en.wikipedia.org/wiki/JSON) message.

Hello image suivante affiche hello les classique au bout de flux de données pour ce projet :

![Flux de données entre les trois modules](media/iot-hub-iot-edge-create-module/dataflow.png "Entrée : module BLE simulé ; processeur : module de convertisseur ; sortie : module d’imprimante")

## <a name="understanding-hello-code"></a>Description du code hello

### <a name="maven-project-structure"></a>Structure du projet Maven

Étant donné que les packages Azure IoT Edge sont basées sur Maven, nous devons toocreate une structure de projet Maven classique, qui contient un `pom.xml` fichier.

Hello POM hérite hello `com.microsoft.azure.gateway.gateway-module-base` package, qui déclare toutes les dépendances hello requises par un projet de module qui inclut les fichiers binaires du runtime hello, chemin de fichier de configuration de passerelle hello et le comportement de l’exécution de hello. Cela nous évite beaucoup de temps et éliminer hello besoin toowrite et réécrire des centaines de lignes de code indéfiniment.

Nous devons tooupdate le fichier pom.xml en déclarant hello requis dépendances/plug-ins et nom hello de toobe de fichier de configuration hello utilisé par notre module, comme illustré dans hello suivant extrait de code.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Compréhension élémentaire d’un module Azure IoT Edge

Vous pouvez traiter un module Azure IoT Edge comme un processeur de données dont la tâche consiste à : recevoir une entrée, la traiter et générer une sortie.

Hello entrée peut-être des données à partir du matériel (comme un détecteur de mouvement), un message à partir d’autres modules ou toute autre (par exemple, un nombre aléatoire généré régulièrement par un minuteur).

sortie de Hello est similaire toohello entrée, il risque de déclencher matériel comportement (hello clignote LED), un module de tooother message ou rien (comme l’impression toohello console).

Les modules communiquent entre eux à l’aide de la classe `com.microsoft.azure.gateway.messaging.Message`. Hello **contenu** d’un `Message` est un tableau d’octets qui est capable de représenter n’importe quel type de données de votre choix. **Propriétés** sont également disponibles dans hello `Message` et sont simplement un mappage de chaîne en chaîne. Vous pouvez vous représenter **propriétés** en tant qu’en-têtes hello dans une requête HTTP, ou métadonnées hello d’un fichier.

Dans l’ordre toodevelop un module Azure IoT Edge dans Java, vous devez toocreate une nouvelle classe de module qui hérite de `com.microsoft.azure.gateway.core.GatewayModule` et implémenter les méthodes abstraites hello requis `receive()` et `destroy()`. À ce stade, vous pouvez également choisir hello tooimplement facultatif `start()` ou `create()` également les méthodes. Hello suivant extrait de code montre comment tooget démarrer la création d’un module Azure IoT Edge.

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

### <a name="converter-module"></a>Module de convertisseur

| Entrée                    | Processeur                              | Sortie                 | Fichier source            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Message de données de température | Analyser et construire un nouveau message JSON | Structurer le message JSON | `ConverterModule.java` |

Ce module est un module Azure IoT Edge classique. Il accepte des messages de température d’autres modules (un module de matériel, ou dans ce cas, notre module BLE simulé) ; puis normalise hello température message tooa structuré JSON message (y compris l’ajout des ID de message hello, définition de propriété hello de si nous devons alerte de température hello tootrigger et ainsi de suite).

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

### <a name="printer-module"></a>Module d’imprimante

| Entrée                          | Processeur | Sortie                     | Fichier source          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Tous les messages provenant d’autres modules | N/A       | Ouvrez une session hello message tooconsole | `PrinterModule.java` |

Il s’agit d’un module de simple et explicite, qui génère la fenêtre de terminal toohello messages hello reçu.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Configuration d’Azure IoT Edge

étape finale de Hello avant d’exécuter les modules hello est tooconfigure hello Azure IoT Edge et tooestablish hello connexions entre des modules.

Nous devons abord toodeclare notre chargeur Java (depuis Azure IoT Edge prend en charge les chargeurs de langues différentes), qui peut être référencé par son `name` dans les sections hello par la suite.

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

Une fois que nous avons déclaré notre chargeurs, nous devez également toodeclare nos modules également. Les chargeurs de hello toodeclaring similaires, ils peuvent également être référencés par leurs `name` attribut. Lorsque vous déclarez un module, nous devons toospecify hello du chargeur doit être utilisé (qui doit être hello une nous avons défini avant) et hello point d’entrée (doit être le nom de classe normalisé hello de notre module) pour chaque module. Hello `simulated_device` module est un module natif qui est inclus dans le package de runtime hello Azure IoT bord core. Vous devez toujours inclure `args` Bonjour, même s’il s’agit du fichier JSON `null`.

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

Extrémité hello de configuration de hello, nous établir des connexions de hello. Chaque connexion est exprimée par `source` et `sink`. Ces valeurs doivent faire référence à un module prédéfini. message de sortie de type Hello `source` module sera transféré entrée toohello `sink` module.

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

## <a name="running-hello-modules"></a>Modules hello en cours d’exécution

Utilisez `mvn package` toobuild tout en hello `target/` dossier. `mvn clean package` est également recommandé pour créer un build propre.

Utilisez `mvn exec:exec` toorun hello Azure IoT Edge et vous devez observer que les données de température hello et toutes les propriétés de hello sont console toohello imprimé à un taux fixe.

Si vous souhaitez tooterminate hello application, appuyez sur `<Enter>` clé.

> [!IMPORTANT]
> Il est déconseillé de toouse Ctrl + C tooterminate hello IoT bord application passerelle. Car cela pourrait provoquer hello processus tooterminate anormalement.

