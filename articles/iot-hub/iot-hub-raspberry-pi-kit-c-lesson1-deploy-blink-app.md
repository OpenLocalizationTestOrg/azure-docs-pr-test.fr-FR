---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : déploiement d’une application | Documents Microsoft"
description: "Cloner l’application d’exemple C hello à partir de GitHub et gulp toodeploy ce tableau de tooyour framboises Pi 3 d’application. Cet exemple d’application clignote hello LED connecté toohello tableau toutes les deux secondes."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: raspberry pi led clignotante, led clignotante avec raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Créer et déployer des applications de clignotement hello
## <a name="what-you-will-do"></a>Procédure à suivre
Cloner hello exemple C d’application à partir de GitHub et utiliser l’exemple hello gulp outil toodeploy hello application tooRaspberry Pi 3. exemple d’application Hello clignote hello LED connecté toohello tableau toutes les deux secondes. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment toouse hello `device-discover-cli` tooretrieve outil mise en réseau des informations sur Pi.
* Comment toodeploy et exécution hello exemple d’application sur Pi.
* Comment toodeploy et débogage des applications en cours d’exécution à distance sur Pi.

## <a name="what-you-need"></a>Ce dont vous avez besoin
Vous devez avoir correctement terminé hello opérations suivantes :

* [Configuration de votre appareil](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [Obtenir les outils de hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a>Obtenir hello IP adresse et nom d’hôte de Pi
Ouvrez une invite de commandes dans Windows ou d’un terminal dans macOS ou Ubuntu, puis exécutez hello de commande suivante :

```bash
devdisco list --eth
```

Vous devez voir une sortie similaire toohello suivantes :

![Découverte de l’appareil](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

Prenez note de hello `IP address` et `hostname` de Pi. Ces informations vous seront nécessaires plus loin dans cet article.

> [!NOTE]
> Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur. Par exemple, si votre ordinateur est connecté tooa les réseau sans fil pendant que Pi est connecté tooa réseau câblé, vous verrez ne peut-être pas hello IP adresse dans la sortie de devdisco hello.

## <a name="open-hello-sample-application"></a>Exemple d’application hello ouvert
tooopen hello exemple d’application, procédez comme suit :

1. Clonez le dépôt d’exemples hello à partir de GitHub en exécutant hello de commande suivante :
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. Ouvrir l’exemple d’application hello dans Visual Studio Code par hello suivant les commandes en cours d’exécution :
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Structure du référentiel](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

Hello `main.c` fichier Bonjour `app` sous-dossier est le fichier de source de la clé de hello qui contient hello code toocontrol hello DEL.

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
   
   fichier de configuration Hello `config-raspberrypi.json` contient des informations d’identification de l’utilisateur hello vous utilisez toolog dans tooPi. fuite de hello tooavoid des informations d’identification de l’utilisateur, le fichier de configuration de hello est généré dans le sous-dossier de hello `.iot-hub-getting-started` du dossier de base hello sur votre ordinateur.

2. Ouvrez le fichier de configuration de périphérique de hello dans le Code de Visual Studio en exécutant hello de commande suivante :
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. Remplacez l’espace réservé de hello `[device hostname or IP address]` avec l’adresse IP de hello ou nom d’hôte hello que vous avez obtenu précédemment dans « Obtention hello IP adresse et nom d’hôte de Pi. »
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> Vous pouvez utiliser la clé SSH au lieu de nom d’utilisateur et mot de passe lors de la connexion tooRaspberry Pi. Dans commande toodo cela avoir toogenerate hello clé à l’aide **ssh-keygen** et **pi ssh-copy-id @\<adresse du périphérique\>**.
>
> Sous Windows, ces commandes sont disponibles dans **Git Bash**.
>
> Sur Mac OS, vous devez toorun **brew installer ssh-copy-id**.
>
> Après avoir téléchargé avec succès les toohello de clé hello framboises Pi, remplacez **device_password** avec **device_key_path** propriété dans **raspberrypi.json de configuration**.
>
> Les lignes mises à jour doivent se présenter comme suit :
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

Félicitations ! Vous venez de créer hello premier exemple d’application de Pi.

## <a name="deploy-and-run-hello-sample-application"></a>Déployer et exécuter l’exemple d’application hello
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a>Installer hello Azure IoT Hub SDK sur Pi
Installer hello Azure IoT Hub SDK sur Pi en exécutant hello de commande suivante :

```bash
gulp install-tools
```

Cette tâche peut prendre quelques hello de toocomplete minutes première fois que vous l’exécutez.

### <a name="deploy-and-run-hello-sample-app"></a>Déployer et exécuter l’exemple d’application hello
Déployer et exécuter l’exemple d’application hello en exécutant hello de commande suivante :

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Vérifiez que hello application fonctionne
exemple d’application Hello se termine automatiquement après que hello LED clignote pour 20 fois. Si vous ne voyez pas hello LED clignote, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.
![LED clignotante](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)

## <a name="summary"></a>Résumé
Vous avez installé des hello requis outils toowork avec Pi et déployé un Bonjour de tooblink exemple application tooPi DEL. Vous pouvez désormais créer, déployer et exécuter un autre exemple d’application qui se connecte Pi tooAzure toosend d’IoT Hub et recevoir des messages.

## <a name="next-steps"></a>Étapes suivantes
[Obtenir les outils Azure](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

