---
title: "Appareil simulé et passerelle Azure IoT - Leçon 2 : Obtenir des outils (Windows) | Microsoft Docs"
description: "Installer les outils de hello et les logiciels de hello sur votre ordinateur hôte exécutant Windows, créez un IoT hub et inscrire votre appareil dans le hub IoT de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, service cloud iot, logiciel internet des objets, azure cli, installer git sur windows, exécuter gulp, installer node js windows, installer npm sur windows, installer python sur windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a>Obtenir les outils de hello (Windows 7 et versions ultérieures)
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

- Comment tooinstall [Git](https://git-scm.com/) et [Node.js](https://nodejs.org/en/).
  - Git est un système de contrôle de versions distribué open source très populaire. exemple d’application Hello pour cette leçon est stocké sur Git.
  - Node.js est un runtime JavaScript avec un écosystème de packages riche.
- Comment toouse [NPM](https://www.npmjs.com/) tooinstall des outils de développement Node.js.
  - la version minimale requise Hello de Node.js est 4.5 LTS.
  - NPM est un des gestionnaires de package hello pour Node.js.
- Comment tooinstall Visual Studio Code.
  - Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS. Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.
- Comment tooinstall Python.
  - Python est un langage de programmation interprété et dynamique, à usage général et fréquemment utilisé.
- Comment tooinstall hello CLI d’Azure.
  - Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure. Travailler directement depuis une tooprovision de ligne de commande et de gérer les ressources.
- Comment toouse hello CLI d’Azure toocreate un IoT hub.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Un toodownload de connexion Internet hello outils et logiciels.
- Un ordinateur Windows.

## <a name="install-git-and-nodejs"></a>Installation de Git et Node.js

Cliquez sur Suivant toodownload de liens de hello et installer Git et LTS Node.js pour Windows.

- [Téléchargement de Git pour Windows](https://git-scm.com/download/win/)
- [Téléchargement de Node.js LTS pour Windows](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a>Installer des outils de développement Node.js

Vous utilisez [fichier gulp.js](http://gulpjs.com/) tooautomate déploiement et l’exécution de scripts.

Appuyez sur `Windows + R`, type `cmd` et appuyez sur `Enter` tooopen une fenêtre d’invite de commandes, puis en exécution hello suivant commande :

```cmd
npm install -g gulp
```

Si vous rencontrez des problèmes avec l’installation de hello, consultez hello [guide de dépannage](iot-hub-gateway-kit-c-sim-troubleshooting.md) pour les problèmes de toocommon solutions.

> [!Note]
> Nœud, NPM et Gulp sont développés dans Node.js des scripts d’automatisation toorun requis.

## <a name="install-python"></a>Installation de Python

Vous pouvez choisir entre Python 2.7, 3.4 ou 3.5. Dans ce didacticiel, nous utilisons Python 2.7. Si vous avez déjà installé les python, accédez à toohello la prochaine section.

[Obtenir Python pour Windows](https://www.python.org/downloads/)

Vous devez également le chemin d’accès de hello tooadd de dossiers hello où Python.exe et pip.exe sont installés toohello système `PATH` variable d’environnement. Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Installer hello CLI d’Azure

tooinstall hello CLI d’Azure, procédez comme suit :

1. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.

2. Installez hello CLI d’Azure en exécutant hello suivant de commandes :

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   installation de Hello peut prendre 5 minutes.

3. Hello Vérifiez-la en exécutant hello de commande suivante :

   ```cmd
   az iot -h
   ```

   Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.

   ![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a>Installation de Visual Studio Code

Vous utilisez Visual Studio Code ultérieurement dans les fichiers de configuration de didacticiel tooedit hello.

[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code.

## <a name="summary"></a>Résumé

Vous avez installé tous les outils de hello requis et les logiciels sur votre ordinateur hôte. La tâche suivante est toouse hello CLI d’Azure toocreate un IoT hub et inscrire votre appareil dans votre hub IoT.

## <a name="next-steps"></a>Étapes suivantes
[Créer un hub IoT et enregistrer votre appareil](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
