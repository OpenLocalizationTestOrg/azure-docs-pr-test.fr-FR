---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 4 : Résolution des problèmes | Microsoft Docs"
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
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Résolution de problèmes
## <a name="hardware-issues"></a>Problèmes matériels
Pour plus d’informations sur la résolution de problèmes courants sur Intel Edison, consultez la [page de dépannage officielle](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problèmes de package Node.js
### <a name="no-response-during-gulp-tasks"></a>Aucune réponse lors des tâches gulp
Si vous rencontrez des problèmes d’exécution des tâches gulp, vous pouvez ajouter l’option `--verbose` pour le débogage. Essayez d’arrêter les tâches gulp en cours en appuyant sur `Ctrl + C`, puis exécutez la commande suivante dans la fenêtre de la console pour afficher les messages de débogage. Des messages d’erreur détaillés peuvent s’afficher dans la sortie de la console. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>Problèmes liés à NPM
Essayez de mettre à jour votre package NPM avec la commande suivante :

```bash
npm install -g npm
```

Si le problème persiste, entrez vos commentaires à la fin de cet article ou créez un problème GitHub dans notre [exemple de référentiel][sample-repository].

## <a name="remote-debugging"></a>Débogage à distance

### <a name="run-the-sample-application-in-debug-mode"></a>Exécuter l’application en mode débogage

```bash
gulp run --debug
```

Lorsque le moteur de débogage est prêt, ```Debugger listening on port 5858``` devrait apparaître dans la sortie de la console.

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a>Configurer Visual Studio Code pour la connexion à l’appareil distant

Ouvrez le panneau **Déboguer** dans la partie gauche.

Cliquez sur le bouton vert **Démarrer le débogage** (F5). Visual Studio Code ouvre un fichier **launch.json** que vous devez mettre à jour.

Mettez à jour le fichier **launch.json** avec le contenu suivant, puis remplacez `[device hostname or IP address]` par l’adresse IP ou le nom d'hôte réel de l'appareil.  

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

### <a name="attach-to-the-remote-application"></a>Attacher à l’application distante

Cliquez sur le bouton vert **Démarrer le débogage** (F5) pour commencer à déboguer.

Pour en savoir plus sur le débogueur, vous pouvez lire [JavaScript dans VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) (JavaScript dans Visual Studio Code).

![Débogage interactif à distance](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problèmes liés à l'interface de ligne de commande Azure
L’interface de ligne de commande Azure est une version d’évaluation. Pour rechercher des solutions, voir le [Guide d’installation de la version d’évaluation](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md). Essayez de mettre à niveau Azure-cli à la version la plus récente lorsque les commandes ne fonctionnent pas comme prévu.

Si vous rencontrez des bogues avec l’outil, documentez un [problème](https://github.com/Azure/azure-cli/issues) dans la section **Issues** du dépôt GitHub.

Pour obtenir de l’aide sur la résolution de problèmes courants, voir la rubrique [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Si l’erreur « Impossible de trouver une version conforme à la configuration requise » s’affiche, exécutez la commande suivante pour mettre à niveau pip vers la dernière version.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problèmes d’installation de Python
### <a name="legacy-installation-issues-macos"></a>Problèmes d’installation héritée (macOS)
Lors de l’installation de **pip**, une erreur d’autorisation est levée s’il existe des packages antérieurs qui sont installés avec des autorisations **su**. Cette situation se produit parce qu’une installation précédente de Python utilisant brew (macOS) n’est pas complètement désinstallée. Certains packages **pip** d’une installation précédente ont été créés par root, ce qui génère l’erreur d’autorisation. La solution consiste à supprimer les packages installés par root. Pour effectuer cette tâche, procédez comme suit :

1. Accédez à : /usr/local/lib/python2.7/site-packages
2. Affichez la liste des packages créés par root : `ls -l | grep root`.
3. Désinstallez les packages identifiés à l’étape 2 : `sudo rm -rf {package name}`
4. Réinstallez Python.

## <a name="azure-iot-hub-issues"></a>Problèmes liés à Azure IoT Hub
Si vous avez correctement configuré votre Azure IoT Hub avec `azure-cli`, et avez besoin d’un outil pour gérer les appareils se connectant à votre IoT Hub, essayez les outils suivants :

### <a name="device-explorer"></a>Explorateur d’appareils
L’[Explorateur d’appareils](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) s’exécute sur votre ordinateur Windows local et se connecte à votre IoT Hub dans Azure. Il communique avec les [points de terminaison IoT Hub](iot-hub-devguide.md) suivants :

- _Device identity management_ (Gestion d’identité d’appareil) pour configurer et gérer les appareils inscrits auprès de votre IoT Hub.
- _Receive device-to-cloud_ (Réception appareil-à-cloud) pour pouvoir surveiller les messages envoyés par votre appareil à votre IoT Hub.
- _Send cloud-to-device_ (Envoi cloud-à-appareil) pour pouvoir envoyer des messages à vos appareils à partir de votre IoT Hub.

Configurez votre `IoT hub connection string` dans cet outil pour utiliser toutes ses fonctionnalités.

### <a name="iot-hub-explorer"></a>IoT Hub Explorer
[IoT Hub Explorer](https://github.com/Azure/iothub-explorer) est un exemple d’outil d’interface de ligne de commande multiplateforme destiné à la gestion d’appareils clients. Cet outil permet de gérer les appareils dans le registre des identités, de surveiller les messages appareil-à-cloud et d’envoyer des commandes cloud-à-appareil.

Pour installer la dernière version (préliminaire) de l’outil iothub-explorer, dans votre environnement de ligne de commande, exécutez la commande suivante :

```bash
npm install -g iothub-explorer@latest
```

Pour obtenir une aide supplémentaire sur toutes les commandes d’iothub-explorer et leurs paramètres, vous pouvez utiliser la commande suivante :

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Portail Azure
Une expérience complète de l’interface de ligne de commande vous permet de créer et de gérer toutes vos ressources Azure. Vous pouvez également être amené à utiliser le [portail Azure](../azure-portal-overview.md) pour configurer, gérer et déboguer vos ressources Azure.

## <a name="azure-storage-issues"></a>Problèmes liés au stockage Azure
[L’Explorateur de stockage Microsoft Azure (en version préliminaire)](http://storageexplorer.com) est une application autonome de Microsoft qui vous permet d’utiliser des données du [Stockage Azure](https://azure.microsoft.com/en-us/services/storage/) sur Windows, macOS et Linux. Cet outil vous permet de vous connecter à votre table et d’en consulter les données. Vous pouvez l’utiliser cet outil pour résoudre des problèmes liés au Stockage Azure.

## <a name="next-steps"></a>Étapes suivantes
Cette page inclut uniquement les problèmes les plus courants du kit Intel Edison. Vous pouvez également laisser des commentaires en bas pour signaler des problèmes nécessitant un dépannage.

Revenez à [Prise en main d’Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started