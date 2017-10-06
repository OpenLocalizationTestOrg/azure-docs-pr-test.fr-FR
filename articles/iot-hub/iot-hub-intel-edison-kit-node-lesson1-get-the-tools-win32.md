---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 1 : obtenir les outils (Windows) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application pour Edison sur Windows 7 et versions ultérieures."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "outils de développement arduino, développement iot, logiciel iot, logiciel internet des objets, installer git sous windows, installer node js sous windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a>Obtenir les outils de hello (Windows 7 ou version ultérieure)
> [!div class="op_single_selector"]
> * [Windows 7 ou version ultérieure][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Procédure à suivre
Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour Intel Edison. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment tooinstall Git et Node.js.
  * [Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire. exemple d’application Hello pour cet article est stockée sur Git.
  * [Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.
* Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.
  * Hello version minimale requise de Node.js est 4.5 LTS.
  * [NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.

## <a name="what-you-need"></a>Ce dont vous avez besoin

toocomplete cette opération, vous devez :

* Un toodownload de connexion Internet hello des outils de développement et hello logiciel.
* Un ordinateur fonctionnant sous Windows.

## <a name="install-git-and-nodejs"></a>Installation de Git et Node.js

Cliquez sur les liens ci-dessous toodownload hello et installer Git et LTS Node.js pour Windows.

* [Téléchargement de Git pour Windows](https://git-scm.com/download/win/)
* [Téléchargement de Node.js LTS pour Windows](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a>Installation des outils de développement Node.js supplémentaires

Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooEdison d’application exemple hello.

Lancez une invite de commandes en tant qu’administrateur. Installer `gulp` en exécutant hello de commande suivante :

```cmd
npm install -g gulp
```

Si vous rencontrez des problèmes d’installation de Node.js et ces autres outils de développement de Node.js sur votre ordinateur, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.

## <a name="install-visual-studio-code"></a>Installation de Visual Studio Code

[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code. Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS. Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.

## <a name="summary"></a>Résumé

Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application. la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Edison.

## <a name="next-steps"></a>Étapes suivantes

[Créer et déployer des applications de clignotement hello][create-and-deploy-the-blink-application]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
