---
title: "Connect Raspberry PI (C) tooAzure IoT - dépanner | Documents Microsoft"
description: "Résolution des problèmes de page pour une expérience hello framboises Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problèmes iot, problèmes liés à l’internet des objets"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Résolution des problèmes
## <a name="hardware-issues"></a>Problèmes matériels
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>application Hello s’exécute correctement mais hello LED clignote pas
Ce problème est toujours une connectivité de circuits toohardware connexes. Utilisez hello étapes tooidentify problèmes suivants :

1. Vérifiez que vous avez choisi hello correct **GPIO** sur votre carte mère. Hello deux ports doivent être **GPIO GND (code confidentiel 6)** et **GPIO 04 (code confidentiel 7)**.
2. Vérifiez que la polarité hello de votre DEL est correcte. branche de plus de temps Hello doit indiquer hello **positif**, code confidentiel d’anode.
3. Hello d’utilisation **3,3 v épingler** et **code confidentiel de terre** sur framboises Pi 3. Traiter Pi comme hello alimentation électrique. Vérifiez que hello DEL fonctionne correctement.

![Spécification de la LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Autres problèmes matériels
Pour plus d’informations sur la résolution des problèmes courants sur framboises Pi 3, consultez hello [page officielle de dépannage](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problèmes de package Node.js
### <a name="no-response-during-gulp-tasks"></a>Aucune réponse lors des tâches gulp
Si vous rencontrez des problèmes dans gulp tâches en cours d’exécution, vous pouvez ajouter hello `--verbose` option pour le débogage. Essayez de tooterminate actuel gulp tâches à l’aide de Ctrl + C et puis exécutez hello commande dans les messages de débogage de toosee fenêtre console suivante. Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problèmes de détection d’appareil
Pour vous aider à résoudre les problèmes courants avec hello `devdisco` de commande, vérifiez hello [Lisez-moi](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>problèmes liés à npm
Essayez de votre package npm tooupdate à l’aide de hello de commande suivante :

```bash
npm install -g npm
```

Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Débogage à distance
### <a name="run-hello-sample-application-in-debug-mode"></a>Exécuter l’exemple d’application hello en mode débogage
```bash
gulp run --debug
```

Lorsque le moteur de débogage hello est prêt, vous devez voir ```Debugger listening on port 5858``` dans la sortie de console hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configurez le périphérique distant de Visual Studio Code tooconnect toohello
1. Ouvrez hello **déboguer** Panneau de configuration sur le côté gauche de hello.
2. Cliquez sur hello verte **démarrer le débogage** bouton (F5). Visual Studio Code ouvre un fichier launch.json.
3. Mettre à jour les fichiers de launch.json hello avec hello suivant le contenu. Remplacez `[device hostname or IP address]` avec hello périphérique réel IP adresse ou nom d’hôte.

> [!NOTE]
> toolearn en savoir plus sur hello débogage Visual Studio, consultez trop[débogage dans Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


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

![Configuration du débogage à distance](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Attacher toohello des applications à distance
Cliquez sur hello verte **démarrer le débogage** toostart de débogage de bouton (F5).

Lecture [JavaScript dans Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn plus à propos du débogueur de hello.

![Débogage interactif à distance](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problèmes d’interface de ligne de commande Azure
Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire. les solutions tooseek, vous pouvez utiliser hello [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.

Pour vous aider à résoudre les problèmes courants, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problèmes d’installation de Python
### <a name="legacy-installation-issues-macos"></a>Problèmes d’installation héritée (macOS)
Lors de l’installation de pip, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**. Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée. Certains packages pip d’une installation précédente ont été créées par la racine, ce qui provoque l’erreur d’autorisation hello. solution de Hello est tooremove ces packages installés par la racine. Utilisez hello suivant les étapes toocomplete cette tâche :

1. Accédez à : /usr/local/lib/python2.7/site-packages
2. Affichez la liste des packages créés par root : `ls -l | grep root`
3. Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`
4. Réinstallez Python.

## <a name="azure-iot-hub-issues"></a>Problèmes liés à Azure IoT Hub
Si vous avez déployé votre concentrateur Azure IoT avec CLI d’Azure et que vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, essayez de hello suite d’outils.

### <a name="device-explorer"></a>Explorateur d’appareils
Hello [Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure. Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](iot-hub-devguide.md):


* *Gestion des identités* tooprovision et gérer les appareils inscrits avec votre IoT hub.
* *Réception d’appareil-à-cloud* afin de surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision.
* *Envoyer le cloud-à-appareil* afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.

Configurer votre chaîne de connexion de hub IoT dans cette toouse outil toutes ses fonctionnalités.

### <a name="iothub-explorer"></a>iothub-explorer
[Explorateur d’iothub](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage pour les appareils. Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des messages cloud-à-appareil.

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
[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com) est une application autonome de Microsoft que vous pouvez utiliser toowork avec des données de stockage Azure sur Windows, Mac OS et Linux. À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello. Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.

