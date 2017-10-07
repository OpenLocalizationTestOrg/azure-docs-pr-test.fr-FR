---
title: "Appareil SensorTag et passerelle Azure IoT - Résolution de problèmes | Microsoft Docs"
description: "Page de résolution des problèmes pour la passerelle Intel NUC"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problèmes iot, problèmes liés à l’internet des objets"
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Résolution des problèmes

## <a name="hardware-issues"></a>Problèmes matériels

### <a name="ti-sensortag-cannot-be-connected"></a>TI SensorTag ne peut pas être connecté

des problèmes de connectivité tootroubleshoot SensorTag utiliser hello [SensorTag application](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Problème avec Intel NUC

tootroubleshoot démarrage, consultez trop[résolution des problèmes de démarrage non sur Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

tootroubleshoot système d’exploitation, consultez trop[résolution des problèmes du système d’exploitation sur Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot autres, consultez trop[Blink de Codes et émettre un signal sonore pour Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Problèmes de package Node.js

### <a name="no-response-during-gulp-tasks"></a>Aucune réponse lors des tâches gulp

Si vous rencontrez des problèmes dans gulp tâches en cours d’exécution, vous pouvez ajouter hello `--verbose` option pour le débogage. Essayez tooterminate actuel gulp tâches à l’aide de `Ctrl + C`, puis en exécution hello suivant commande dans les messages de débogage de toosee fenêtre console. Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problèmes de détection d’appareil

Pour vous aider à résoudre les problèmes courants avec hello `discover-sensortag` de commande, vérifiez hello [page wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>problèmes liés à npm

Essayez tooupdate votre package npm en exécutant hello de commande suivante :

```bash
npm install -g npm
```

Si le problème de hello existe toujours, laisser vos commentaires à la fin de hello de cet article ou créer un problème de GitHub dans notre [dépôt d’exemples](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Débogage à distance
> Les instructions ci-dessous s’appliquent au débogage des scripts node.js utilisés dans ce didacticiel.
### <a name="run-hello-sample-application-in-debug-mode"></a>Exécuter l’exemple d’application hello en mode débogage

Exécuter l’exemple d’application hello en mode débogage en exécutant hello de commande suivante :

```bash
gulp run --debug
```

Lorsque le moteur de débogage hello est prêt, vous devez voir `Debugger listening on port 5858` dans la sortie de console hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configurez le périphérique distant de Visual Studio Code tooconnect toohello

1. Ouvrez hello **déboguer** Panneau de configuration sur le côté gauche de hello.
2. Cliquez sur hello verte **démarrer le débogage** bouton (F5). Visual Studio Code ouvre un fichier `launch.json`.
3. Hello de mise à jour `launch.json` fichier avec hello suivant le contenu. Remplacez `[device hostname or IP address]` avec hello périphérique réel IP adresse ou nom d’hôte.

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuration du débogage à distance](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Attacher toohello des applications à distance

Cliquez sur hello verte **démarrer le débogage** toostart de débogage de bouton (F5).

Lecture [JavaScript dans Visual Studio Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn plus à propos du débogueur de hello.

![Exemple de débogage BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Problèmes d’interface de ligne de commande Azure

Bonjour Azure interface de ligne de commande (CLI d’Azure) est une version préliminaire. les solutions tooseek, vous pouvez utiliser hello [Guide d’installation de version préliminaire](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Si vous rencontrez des bogues avec l’outil de hello, fichier un [problème](https://github.com/Azure/azure-cli/issues) Bonjour **problèmes** section du référentiel GitHub de hello.

Pour vous aider à résoudre les problèmes courants, consultez hello [Lisez-moi](https://github.com/Azure/azure-cli/blob/master/README.rst).

Si vous répondez à « Impossible de trouver une version qui satisfait aux exigences de hello, » veuillez suivante d’exécution hello commande version de toolastest tooupgrade pip.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problèmes d’installation de Python

### <a name="legacy-installation-issues-macos"></a>Problèmes d’installation héritée (macOS)

Lors de l’installation de pip, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**. Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée. Certains packages pip d’une installation précédente ont été créées par la racine, ce qui provoque l’erreur d’autorisation hello. solution de Hello est tooremove ces packages installés par la racine. Utilisez hello suivant les étapes toocomplete cette tâche :

1. Accédez trop`/usr/local/lib/python2.7/site-packages`
2. Affichez la liste des packages créés par root : `ls -l | grep root`
3. Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`
4. Réinstallez Python.

## <a name="azure-iot-hub-issues"></a>Problèmes liés à Azure IoT Hub

Si vous avez déployé votre concentrateur Azure IoT avec hello CLI d’Azure et que vous avez besoin d’un outil toomanage hello les appareils qui sont connectent tooyour IoT hub, essayez de hello suite d’outils.

### <a name="device-explorer"></a>Explorateur d’appareils

[Explorateur de périphérique](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) s’exécute sur votre ordinateur local de Windows et se connecte tooyour IoT hub dans Azure. Il communique avec les éléments suivants de hello [points de terminaison IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Tooprovision de gestion de périphérique identité et de gérer les appareils inscrits avec votre IoT hub.
- Vous pouvez surveiller les messages envoyés à partir de votre appareil tooyour IoT de supervision reçoivent appareil-à-cloud.
- Envoyer le cloud sur l’appareil afin de pouvoir envoyer des messages tooyour périphériques à partir de votre hub IoT.

Configurer votre chaîne de connexion de hub IoT dans cette toouse outil toutes ses fonctionnalités.

### <a name="iothub-explorer"></a>iothub-explorer

[Explorateur d’iothub](https://github.com/Azure/iothub-explorer) est un exemple d’outil CLI multiplateforme toomanage appareils clients. Vous pouvez utiliser des périphériques de hello hello outil toomanage dans le Registre des identités hello, surveiller les messages appareil-à-cloud et envoyer des commandes de cloud sur l’appareil.

tooinstall hello dernière (version préliminaire) version de hello iothub-explorer outil, exécutez hello de commande suivante :

```bash
npm install -g iothub-explorer@latest
```

tooget une aide supplémentaire sur tous les hello iothub-Explorateur commandes et leurs paramètres, exécutez hello de commande suivante :

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Hello portail Azure

Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure. Vous pouvez également vous toouse hello [portail Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp configurer, gérer et déboguer vos ressources Azure.

## <a name="azure-storage-issues"></a>Problèmes liés au Stockage Azure

[Explorateur de stockage Microsoft Azure (aperçu)](http://storageexplorer.com/) est une application autonome de Microsoft que vous pouvez utiliser toowork avec des données de stockage Azure sur Windows, Mac OS et Linux. À l’aide de cet outil, vous pouvez connecter tooyour table et voir les données hello. Vous pouvez utiliser cet outil tootroubleshoot vos problèmes de stockage Azure.
