---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 4 : dépannage | Documents Microsoft"
description: "Page Dépannage pour l’expérience Node.js Intel Edison"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "résolution des problèmes arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Résolution de problèmes
## <a name="hardware-issues"></a>Problèmes matériels
Pour plus d’informations sur la résolution des problèmes courants sur Intel Edison, consultez hello [page officielle de dépannage](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problèmes de package Node.js
### <a name="no-response-during-gulp-tasks"></a>Aucune réponse lors des tâches gulp
Si vous rencontrez des problèmes d’exécution des tâches de choses, vous pouvez ajouter hello `--verbose` option pour le débogage. Essayez tooterminate actuel gulp tâches à l’aide de `Ctrl + C`, puis en exécution hello suivant commande dans les messages de débogage de toosee fenêtre console. Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>problèmes liés à NPM
Essayez de votre package NPM tooupdate avec hello de commande suivante :

```bash
npm install -g npm
```

Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples][sample-repository].

## <a name="remote-debugging"></a>Débogage à distance

### <a name="run-hello-sample-application-in-debug-mode"></a>Exécuter l’exemple d’application hello en mode débogage

```bash
gulp run --debug
```

Une fois que le moteur de débogage hello est prêt, vous devez être en mesure de toosee ```Debugger listening on port 5858``` à partir de la sortie de console hello.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>Configurez le périphérique distant de VS Code tooconnect toohello

Ouvrez hello **déboguer** Panneau de configuration à partir de hello côté gauche.

Cliquez sur hello verte **démarrer le débogage** bouton (F5). VS Code ouvrirait un **launch.json** de fichiers, ce qui vous avez besoin de tooupdate.

Hello de mise à jour **launch.json** avec hello suivant le contenu du fichier, remplacez `[device hostname or IP address]` avec l’adresse IP de périphérique réel hello ou nom d’hôte.  

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Configuration du débogage à distance](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Attacher toohello des applications à distance

Cliquez sur hello verte **démarrer le débogage** (F5) bouton et profitez de débogage.

Vous pouvez lire [JavaScript dans Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn plus à propos du débogueur de hello.

![Débogage interactif à distance](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problèmes liés à l'interface de ligne de commande Azure
Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire. Recherchez la solution Bonjour [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions. Essayez tooupgrade cli d’Azure toolatest version lorsque les commandes ne fonctionnent pas comme prévu.

Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.

Pour résoudre les problèmes courants de l’aide, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).

Si vous répondez à « Impossible de trouver une version qui satisfait aux exigences de hello, » veuillez suivante d’exécution hello commande version de toolastest tooupgrade pip.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problèmes d’installation de Python
### <a name="legacy-installation-issues-macos"></a>Problèmes d’installation héritée (macOS)
Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**. Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée. Certains **pip** packages à partir d’une installation précédente ont été créés à la racine, ce qui provoque l’erreur d’autorisation hello. solution de Hello est tooremove ces packages installés par la racine. Utilisez hello suivant les étapes toocomplete cette tâche :

1. Accédez à : /usr/local/lib/python2.7/site-packages
2. Affichez la liste des packages créés par root : `ls -l | grep root`.
3. Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`
4. Réinstallez Python.

## <a name="azure-iot-hub-issues"></a>Problèmes liés à Azure IoT Hub
Si vous avez déployé votre concentrateur Azure IoT avec `azure-cli`, et vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, hello try suivant outils :

### <a name="device-explorer"></a>Explorateur d’appareils
[Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure. Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](iot-hub-devguide.md):

- _Gestion des identités_ tooprovision et gérer les appareils inscrits avec votre IoT hub.
- _Réception d’appareil-à-cloud_ afin de surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision.
- _Envoyer le cloud-à-appareil_ afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.

Configurer votre `IoT hub connection string` dans cette toouse outil toutes ses fonctionnalités.

### <a name="iot-hub-explorer"></a>IoT Hub Explorer
[IoT hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage appareils clients. Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des commandes de cloud sur l’appareil.

tooinstall hello la dernière version (version préliminaire) de hello iothub-Explorateur, exécutez hello commande dans votre environnement de ligne de commande suivante :

```bash
npm install -g iothub-explorer@latest
```

Vous pouvez utiliser hello tooget une aide supplémentaire sur l’ensemble hello iothub-Explorateur commandes et leurs paramètres de commande suivante :

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Portail Azure
Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure. Vous pouvez également vous toouse hello [portail Azure](../azure-portal-overview.md) toohelp configurer, gérer et déboguer vos ressources Azure.

## <a name="azure-storage-issues"></a>Problèmes liés au Stockage Azure
[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com) est une application autonome de Microsoft que vous pouvez utiliser toowork avec [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) données sur Windows, Mac OS et Linux. À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello. Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.

## <a name="next-steps"></a>Étapes suivantes
Cette page inclut uniquement les problèmes les plus courants hello du kit de Edison d’Intel. Vous pouvez également laisser les commentaires en bas problèmes tooreport pour résoudre le problème.

Revenir en arrière trop[prise en main Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started