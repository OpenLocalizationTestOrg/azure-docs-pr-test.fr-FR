---
title: "Appareil simulé et passerelle Azure IoT - Leçon 2 : Obtenir des outils (Ubuntu) | Microsoft Docs"
description: "Installer les outils de hello et les logiciels de hello sur votre ordinateur hôte exécutant Ubuntu, créez un IoT hub et inscrire votre appareil dans le hub IoT de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, service cloud iot, logiciel internet des objets, azure cli, installer git sur ubuntu, exécuter gulp, installer node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a>Obtenir les outils de hello (16.04 Ubuntu)
> [!div class="op_single_selector"]
> * [Windows 7 ou version ultérieure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a>Procédure à suivre

- Installation de Git, Node.js, Gulp et Python.
- Installez hello Azure interface de ligne de commande (CLI d’Azure). 

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).
## <a name="what-you-will-learn"></a>Contenu

Dans cette leçon, vous allez apprendre :

- Comment tooinstall Git et Node.js.
  - Git est un système de contrôle de versions distribué open source très populaire. exemple d’application Hello pour cette leçon est stocké sur Git.
  - Node.js est un runtime JavaScript avec un écosystème de packages riche.
- Comment les outils de développement toouse NPM tooinstall Node.js.
  - la version minimale requise Hello de Node.js est 4.5 LTS.
  - NPM est un des gestionnaires de package hello pour Node.js.
- Comment tooinstall Visual Studio Code.
  - Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS. Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.
- Comment tooinstall hello CLI d’Azure
  - Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure. Travailler directement depuis une tooprovision de ligne de commande et de gérer les ressources.
- Comment toouse hello CLI d’Azure toocreate un IoT hub.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Un toodownload de connexion Internet hello outils et logiciels.
- Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.

## <a name="install-git-and-nodejs"></a>Installation de Git et Node.js

tooinstall Git et Node.js, procédez comme suit :

1. Appuyez sur `Ctrl + Alt + T` tooopen un terminal.
2. Exécutez hello suivant de commandes :

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a>Installer des outils de développement Node.js

Vous utilisez [fichier gulp.js](http://gulpjs.com/) tooautomate déploiement et l’exécution de scripts.

gulp de tooinstall, exécutez hello commande dans un terminal hello suivante :

```bash
sudo npm install -g gulp
```

Si vous rencontrez des problèmes avec l’installation de hello, consultez hello [guide de dépannage](iot-hub-gateway-kit-c-sim-troubleshooting.md) pour les problèmes de toocommon solutions.

> [!Note]
> Nœud, NPM et Gulp sont développés dans Node.js des scripts d’automatisation toorun requis.

## <a name="install-hello-azure-cli"></a>Installer hello CLI d’Azure

tooinstall hello CLI d’Azure, procédez comme suit :

1. Exécutez hello suivant les commandes dans un terminal hello :

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   installation de Hello peut prendre 5 minutes.

2. Hello Vérifiez-la en exécutant hello de commande suivante :

   ```bash
   az iot -h
   ```
Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.
![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)

### <a name="install-visual-studio-code"></a>Installation de Visual Studio Code

Vous utilisez Visual Studio Code ultérieurement dans les fichiers de configuration de didacticiel tooedit hello.

[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.

## <a name="summary"></a>Résumé

Vous avez installé tous les outils de hello requis et les logiciels sur votre ordinateur hôte. La tâche suivante est toouse hello CLI d’Azure toocreate un IoT hub et inscrire votre appareil dans votre hub IoT.

## <a name="next-steps"></a>Étapes suivantes
[Créer un hub IoT et enregistrer votre appareil](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
