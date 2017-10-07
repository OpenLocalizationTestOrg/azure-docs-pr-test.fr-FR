---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : obtenir les outils (Ubuntu) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application de Pi sur Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, logiciel internet des objets, installer git sur ubuntu, exécuter gulp, installer node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obtenir les outils de hello (16.04 Ubuntu)

> [!div class="op_single_selector"]
> * [Windows 7 ou version ultérieure](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Procédure à suivre
Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour votre framboises Pi 3. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

> [!NOTE]
> Bien que hello langage de la logique principale de hello de programmation C, Node.js tools sont utilisées dans les appareils de leçons toodiscover hello, génèrent et déploiement des exemples d’applications.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment tooinstall Git et Node.js
  * [Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire. exemple d’application Hello pour cet article est stockée sur Git.
  * [Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.
* Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.
  * la version minimale requise Hello de Node.js est 4.5 LTS.
  * [NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.

## <a name="what-you-need"></a>Ce dont vous avez besoin
toocomplete cette opération, vous devez :

* Un toodownload de connexion Internet hello des outils de développement et hello logiciel.
* Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.

## <a name="install-git-nodejs-and-npm"></a>Installation de Git, Node.js et NPM
Utiliser le raccourci clavier hello `Ctrl + Alt + T` tooopen un Bonjour Terminal Server et d’exécution suivant des commandes :

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a>Installation des outils de développement Node.js supplémentaires
Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooPi d’application exemple hello. Hello d’utilisation [périphérique-détection-cli](https://github.com/Azure/device-discovery-cli) tooretrieve les informations de réseau sur vos appareils IoT.

Installer `gulp` et `device-discovery-cli` en exécutant hello commande dans un terminal hello suivante :

```bash
sudo npm install -g device-discovery-cli gulp
```

Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur Ubuntu, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.

## <a name="install-visual-studio-code"></a>Installation de Visual Studio Code
[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code. Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS. Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.

## <a name="summary"></a>Résumé
Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application. la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Pi.

## <a name="next-steps"></a>Étapes suivantes
[Créer et déployer des applications de clignotement hello](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

