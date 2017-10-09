---
title: toocloud aaaRaspberry Pi (Node.js) - se connecter un Pi framboises tooAzure IoT Hub | Documents Microsoft
description: "Se connecter tooAzure framboises Pi IoT Hub pour framboises Pi toosend données toohello cloud Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoi données toocloud, raspberry pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Se connecter framboises Pi tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de Pi framboises qui Raspbian est en cours d’exécution. Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Pour obtenir des exemples de Windows 10 IoT Core, accédez à toohello [centre de développement Windows](http://www.windowsondevices.com/).

Vous n’avez pas encore de kit ? Essayez de hello [framboises Pi 3 émulateur](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Procédure

* Configurez Raspberry Pi.
* Créez un hub IoT.
* Inscrivez un appareil pour Pi dans votre IoT Hub.
* Exécuter un exemple d’application sur le concentrateur de Pi toosend capteur données tooyour IoT.

Connectez framboises Pi tooan IoT concentrateur que vous créez. Ensuite, vous exécutez un exemple d’application sur les données de température et humidité toocollect Pi à partir d’un capteur BME280. Enfin, vous envoyez le hub IoT tooyour hello capteur données.

## <a name="what-you-learn"></a>Contenu

* Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.
* Comment tooconnect Pi, avec un capteur BME280.
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Pi.
* Comment le hub IoT tooyour toosend capteur données.

## <a name="what-you-need"></a>Ce dont vous avez besoin

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Hello framboises Pi 2 ou 3 de Pi framboises du tableau.
* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Un moniteur, un clavier USB et la souris qui se connectent tooPi.
* Un Mac ou un PC exécutant Windows ou Linux.
* Une connexion Internet.
* Une carte microSD d’au moins 16 Go.
* Une USB-SD carte microSD carte tooburn hello système d’exploitation image ou sur une carte microSD de hello.
* Une puissance de 2-amp 5-v fournir avec un câble USB micro de hello 6-pied.

Hello éléments suivants est facultatif :

* Un capteur de température, de pression et d’humidité Adafruit BME280 assemblé.
* Une platine d’expérimentation.
* 6 câbles de liaison F/M.
* Une LED de 10 mm diffuse.

  > [!NOTE] 
  Ces éléments sont facultatifs, car la prise en charge des exemples de code hello simulée des données de capteur.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Configuration de Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Installer le système d’exploitation de Raspbian hello de Pi

Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.

1. Téléchargez Raspbian.
   1. [Télécharger Raspbian Jessie avec Pixel](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip de hello).
   1. Extraire le dossier de tooa hello Raspbian image sur votre ordinateur.
1. Installez Raspbian toohello microSD carte.
   1. [Téléchargez et installez l’utilitaire graveur de hello Etcher SD carte](https://etcher.io/).
   1. Exécutez Etcher et sélectionnez l’image Raspbian hello que vous avez extrait à l’étape 1.
   1. Sélectionnez le lecteur de carte microSD hello. Notez que Etcher peut avoir déjà sélectionné lecteur hello.
   1. Cliquez sur le disque mémoire Flash tooinstall Raspbian toohello microSD carte.
   1. Retirez hello microSD votre ordinateur lorsque l’installation est terminée. Carte microSD de hello tooremove safe est directement car Etcher éjecte automatiquement ou démonte carte microSD de hello à l’achèvement.
   1. Insérer carte microSD de hello Pi.

### <a name="enable-ssh-and-i2c"></a>Activer SSH et I2C

1. Connecter le moniteur de toohello Pi, clavier et souris, démarrer Pi, puis Raspbian à l’aide de `pi` en tant que nom d’utilisateur hello et `raspberry` comme mot de passe hello.
1. Cliquez sur hello icône Raspberry > **préférences** > **framboises Pi Configuration**.

   ![menu de préférences de Raspbian Hello](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Sur hello **Interfaces** onglet, définissez **I2C** et **SSH** trop**activer**, puis cliquez sur **OK**. Si vous n’ayez des capteurs physiques et souhaitez que les données de capteur toouse simulée, cette étape est facultative.

   ![Activer I2C et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH et I2C, vous trouverez plus de documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Se connecter hello capteur tooPi

Utilisez les fils de breadboard et cavaliers hello tooconnect une DEL et un tooPi BME280 comme suit. Si vous n’avez pas capteur de hello, ignorez cette section.

![Hello framboises Pi et capteur de connexion](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

capteur de Hello BME280 pouvez collecter des données de température et humidité. Et hello LED clignote s’il existe une communication entre l’appareil et hello cloud. 

Pour les codes confidentiels de capteur, utilisez hello suivant câblage :

| Début (capteur et LED)     | Fin (carte)            | Couleur du câble   |
| -----------------------  | ---------------------- | ------------: |
| VDD (broche 5G)             | ALIM 3,3 V (broche 1)       | Câble blanc   |
| GND (broche 7G)             | GND (broche 6)            | Câble marron   |
| SCK (broche 8G)             | I2C1 SDA (broche 3)       | Câble orange  |
| SDI (broche 10G)            | I2C1 SCL (broche 5)       | Câble rouge     |
| LED VDD (broche 18F)        | GPIO 24 (broche 18)       | Câble blanc   |
| LED GND (broche 17F)        | GND (broche 20)           | Câble noir   |

Cliquez sur tooview [framboises Pi 2 et 3 mappages de code confidentiel](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) de référence.

Une fois que vous avez connecté BME280 tooyour framboises Pi, elle doit être comme sous l’image.

![Pi et BME280 connectés](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Connecter Pi toohello réseau

Pi sous tension à l’aide de câble USB micro de hello et alimentation hello. Utilisez hello Ethernet câble tooconnect Pi tooyour câblé réseau ou suivez hello [instructions hello framboises Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) réseau sans fil de tooconnect Pi tooyour. Une fois votre Pi a été correctement connecté toohello réseau, vous devez tootake note de hello [adresse IP de votre Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Réseau de toowired connecté](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur. Par exemple, si votre ordinateur est connecté tooa les réseau sans fil pendant que Pi est connecté tooa réseau câblé, vous verrez ne peut-être pas hello IP adresse dans la sortie de devdisco hello.

## <a name="run-a-sample-application-on-pi"></a>Exécuter un exemple d’application sur Pi

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Cloner l’exemple d’application et installer les packages de composants requis hello

1. Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour framboises Pi.
    - [PuTTY](http://www.putty.org/) pour Windows. Vous avez besoin d’adresse IP hello votre tooconnect Pi via SSH.
    - client Hello intégré SSH sur Ubuntu ou macOS. Vous pouvez peut-être exécuter `ssh pi@<ip address of pi>` tooconnect Pi via SSH.

   > [!NOTE] 
   nom d’utilisateur par défaut de Hello est `pi` , et le mot de passe hello est `raspberry`.

1. Installation de Node.js et NPM tooyour Pi.
   
   Tout d’abord, vous devez vérifier votre version de Node.js avec hello commande suivante. 
   
   ```bash
   node -v
   ```

   Version de hello est inférieure à 4.x ou s’il n’existe aucune Node.js sur votre Pi, puis exécutez hello suivant tooinstall de commande ou de mettre à jour de Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Pour cloner l’exemple d’application hello en exécutant hello de commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Installez tous les packages en hello commande suivante. Cela inclut Azure IoT device SDK, la bibliothèque de capteur BME280 et la bibliothèque de câblage de Pi.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Il peut prendre plusieurs minutes toofinish cette denpening de processus d’installation sur votre connexion réseau.

### <a name="configure-hello-sample-application"></a>Configurer l’application d’exemple hello

1. Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   nano config.json
   ```

   ![Fichier de configuration](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Deux éléments peuvent être configurés dans ce fichier. Bonjour tout d’abord un est `interval`, qui définit l’intervalle de temps hello entre les deux messages toocloud d’envoi. Hello deuxième `simulatedData`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non.

   Si vous **n’avez pas capteur de hello**, affectez la valeur hello `simulatedData` valeur trop`true` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.

1. Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.

### <a name="run-hello-sample-application"></a>Exécutez l’exemple d’application hello

1. Exécuter l’exemple d’application hello en exécutant hello de commande suivante :

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello.


Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.

![Sortie - données de capteur envoyés à partir de framboises Pi tooyour IoT hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Étapes suivantes

Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]