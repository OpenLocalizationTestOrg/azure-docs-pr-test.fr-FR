---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 1 : déploiement d’une application | Documents Microsoft"
description: "Cloner l’application d’exemple C hello à partir de GitHub et exécutez gulp toodeploy cette tooyour application du tableau de Edison d’Intel. Cet exemple d’application clignote hello LED connecté toohello tableau toutes les deux secondes."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: projets de led arduino, clignotement de led arduino, code de clignotement de led arduino, programme de clignotement arduino, exemple de clignotement arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Créer et déployer des applications de clignotement hello
## <a name="what-you-will-do"></a>Procédure à suivre
Cloner l’application d’exemple C hello à partir de GitHub et utiliser l’exemple hello gulp outil toodeploy hello application tooIntel Edison. exemple d’application Hello clignote hello LED connecté toohello tableau toutes les deux secondes. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
* Comment toodeploy et exécution hello exemple d’application sur Edison.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir correctement terminé hello opérations suivantes :

* [Configuration de votre appareil][configure-your-device]
* [Obtenir les outils de hello][get-the-tools]

## <a name="open-hello-sample-application"></a>Exemple d’application hello ouvert
tooopen hello exemple d’application, procédez comme suit :

1. Clonez le dépôt d’exemples hello à partir de GitHub en exécutant hello de commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Structure du référentiel][repo-structure]

fichier Hello Bonjour `app` sous-dossier est le fichier de source de la clé de hello qui contient hello code toocontrol hello DEL.

### <a name="install-application-dependencies"></a>Installation des dépendances de l’application
Installer les bibliothèques hello et autres modules que vous avez besoin pour l’application d’exemple hello en exécutant hello commande suivante :

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Configurer la connexion du périphérique hello
tooconfigure hello connexion du périphérique, procédez comme suit :

1. Générer le fichier de configuration de périphérique de hello en exécutant hello de commande suivante :

   ```bash
   gulp init
   ```

   fichier de configuration Hello `config-edison.json` contient des informations d’identification de l’utilisateur hello vous utilisez toolog dans tooEdison. fuite de hello tooavoid des informations d’identification de l’utilisateur, le fichier de configuration de hello est généré dans le sous-dossier de hello `.iot-hub-getting-started` du dossier de base hello sur votre ordinateur.

2. Ouvrez le fichier de configuration de périphérique de hello dans le Code de Visual Studio en exécutant hello de commande suivante :

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Remplacez l’espace réservé de hello `[device hostname or IP address]` et `[device password]` avec l’adresse IP de hello et un mot de passe que vous avez marqués vers le bas dans la leçon précédente.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

Félicitations ! Vous venez de créer hello premier exemple d’application pour Edison.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello

### <a name="deploy-and-run-hello-sample-app"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello en exécutant hello de commande suivante :

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Vérifiez que hello application fonctionne
exemple d’application Hello se termine automatiquement après que hello LED clignote pour 20 fois. Si vous ne voyez pas hello LED clignote, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.

![LED clignotante][led-blinking]

## <a name="summary"></a>Résumé
Vous avez installé des hello requis outils toowork avec Edison et déployé un Bonjour de tooblink exemple application tooEdison DEL. Vous pouvez désormais créer, déployer et exécuter un autre exemple d’application qui se connecte Edison tooAzure toosend d’IoT Hub et recevoir des messages.

## <a name="next-steps"></a>Étapes suivantes
[Obtenir des outils Azure hello][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
