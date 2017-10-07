---
title: "Se connecter Arduino tooAzure IoT - leçon 1 : obtenir les outils (macOS) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application pour le Wi-Fi M0 Adafruit contour sur macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "outils de développement arduino, développement iot, logiciel iot, logiciel internet des objets, installer git sur mac, installer node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 0262f3dd-0259-4eb0-962f-9fb534f8359e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5fd306fecd7259fb8f1e99d76282a1e464c4d4f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a>Obtenir les outils de hello (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 ou version ultérieure][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Procédure à suivre

Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application de la carte Adafruit estompe M0 Wi-Fi Arduino. 

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

> [!NOTE]
> Bien que hello langage de la logique principale de hello de programmation est Arduino, Node.js tools sont utilisés dans hello leçons toobuild et déploiement les exemples d’applications.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment tooinstall Git et Node.js.
  * [Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire. exemple d’application Hello pour cet article est stockée sur Git.
  * [Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.
* Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.
  * la version minimale requise Hello de Node.js est 4.5 LTS.
  * [NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.

## <a name="what-you-need"></a>Ce dont vous avez besoin
toocomplete cette opération, vous devez :
* Un toodownload de connexion Internet hello des outils de développement et hello logiciel.
* Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.

## <a name="install-git-and-nodejs"></a>Installation de Git et Node.js
tooinstall Git et Node.js, utilisez hello [Homebrew](http://brew.sh) utilitaire de gestion du package en procédant comme suit :

1. Installer Homebrew. Si vous avez déjà installé Homebrew, accédez à toostep 2.

   1. Appuyez sur `Cmd + Space` et entrez `Terminal` tooopen un terminal.
   2. Exécutez hello de commande suivante :

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. Installer Git et Node.js en exécutant hello de commande suivante :

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a>Installation des outils de développement Node.js supplémentaires
Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de hello exemple application tooyour Arduino carte.

Installer `gulp`, `device-discovery-cli` en exécutant hello commande dans un terminal hello suivante :

```bash
sudo npm install -g gulp device-discovery-cli
```

Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur macOS, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.

## <a name="install-visual-studio-code"></a>Installation de Visual Studio Code
[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code. Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS. Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.

## <a name="summary"></a>Résumé
Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application. la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello dans votre tableau de Arduino.

## <a name="next-steps"></a>Étapes suivantes
[Créer et déployer des applications de clignotement hello][create-and-deploy-the-blink-application]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md