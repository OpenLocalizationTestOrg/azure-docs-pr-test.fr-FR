---
title: toocloud aaaRaspberry Pi (Python) - se connecter un Pi framboises tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous framboises Pi tooAzure IoT Hub pour la plateforme de cloud computing Azure framboises Pi toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot raspberry pi, raspberry pi iot hub, raspberry pi envoi données toocloud, raspberry pi toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a>Se connecter framboises Pi tooAzure IoT Hub (Python)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de Pi framboises qui Raspbian est en cours d’exécution. Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Pour obtenir des exemples de Windows 10 IoT Core, accédez à toohello [centre de développement Windows](http://www.windowsondevices.com/).

Vous n’avez pas encore de kit ? Essayez [le simulateur en ligne Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md). Ou achetez un nouveau kit [ici](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Procédure

* Créez un hub IoT.
* Inscrivez un appareil pour Pi dans votre IoT Hub.
* Configurez Raspberry Pi.
* Exécuter un exemple d’application sur le concentrateur de Pi toosend capteur données tooyour IoT.

Connectez framboises Pi tooan IoT concentrateur que vous créez. Ensuite, vous exécutez un exemple d’application sur les données de température et humidité toocollect Pi à partir d’un capteur BME280. Enfin, vous envoyez le hub IoT tooyour hello capteur données.

## <a name="what-you-learn"></a>Contenu

* Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.
* Comment tooconnect Pi, avec un capteur BME280.
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Pi.
* Comment le hub IoT tooyour toosend capteur données.

## <a name="what-you-need"></a>Ce dont vous avez besoin

![Ce dont vous avez besoin](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

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

## <a name="set-up-raspberry-pi"></a>Installer Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Installer le système d’exploitation de Raspbian hello de Pi

Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.

1. Téléchargez Raspbian.
   1. [Télécharger Raspbian Jessie avec le bureau](https://www.raspberrypi.org/downloads/raspbian/) (fichier .zip de hello).
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

   ![menu de préférences de Raspbian Hello](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Sur hello **Interfaces** onglet, définissez **I2C** et **SSH** trop**activer**, puis cliquez sur **OK**. Si vous n’ayez des capteurs physiques et souhaitez que les données de capteur toouse simulée, cette étape est facultative.

   ![Activer I2C et SSH sur Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH et I2C, vous trouverez plus de documents de référence sur [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) et [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Se connecter hello capteur tooPi

Utilisez les fils de breadboard et cavaliers hello tooconnect une DEL et un tooPi BME280 comme suit. Si vous n’avez capteur hello [ignorer cette section](#connect-pi-to-the-network).

![Hello framboises Pi et capteur de connexion](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

capteur de Hello BME280 pouvez collecter des données de température et humidité. Et hello LED clignote s’il existe une communication entre l’appareil et hello cloud. 

Pour les codes confidentiels de capteur, utilisez hello suivant câblage :

| Début (capteur et LED)     | Fin (carte)            | Couleur du câble   |
| -----------------------  | ---------------------- | ------------: |
| VDD (broche 5G)             | ALIM 3,3 V (broche 1)       | Câble blanc   |
| GND (broche 7G)             | GND (broche 6)            | Câble marron   |
| SDI (broche 10G)            | I2C1 SDA (broche 3)       | Câble rouge     |
| SCK (broche 8G)             | I2C1 SCL (broche 5)       | Câble orange  |
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

### <a name="install-hello-prerequisite-packages"></a>Installer les packages de composants requis hello

Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour framboises Pi.
   
   **Utilisateurs Windows**
   1. Téléchargez et installez [PuTTY](http://www.putty.org/) pour Windows. 
   1. Copier l’adresse IP de hello de votre section Pi dans hello hôte nom (ou adresse IP) et sélectionnez SSH en tant que type de connexion hello.
   
   
   **Utilisateurs Mac et Ubuntu**
   
   Utilisez hello intégré client SSH sur Ubuntu ou macOS. Vous devrez peut-être toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.
   > [!NOTE] 
   nom d’utilisateur par défaut de Hello est `pi` , et le mot de passe hello est `raspberry`.


### <a name="configure-hello-sample-application"></a>Configurer l’application d’exemple hello

1. Pour cloner l’exemple d’application hello en exécutant hello de commande suivante :

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   Ce fichier contient 5 macros configurables. Bonjour tout d’abord un est `MESSAGE_TIMESPAN`, qui définit l’intervalle de temps hello (en millisecondes) entre les deux messages toocloud d’envoi. Hello deuxième `SIMULATED_DATA`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non. `I2C_ADDRESS`est l’adresse hello I2C votre récepteur BME280 est connecté. `GPIO_PIN_ADDRESS`adresse GPIO hello n’est pour votre DEL. Hello dernière un est `BLINK_TIMESPAN`, qui défini hello timespan lorsque votre DEL est activée en millisecondes.

   Si vous **n’avez pas capteur de hello**, affectez la valeur hello `SIMULATED_DATA` valeur trop`True` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.

1. Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.

### <a name="build-and-run-hello-sample-application"></a>Générer et exécuter l’exemple d’application hello

1. Générer l’exemple d’application hello en exécutant hello commande suivante. Hello kits de développement Azure IoT pour Python étant wrappers par-dessus hello Kit de développement logiciel Azure IoT appareil C, vous devez les bibliothèques hello C toocompile si vous voulez ou devez des bibliothèques de Python hello toogenerate à partir de code source.

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   Vous pouvez également spécifier la version de hello en exécutant `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`. Si vous exécutez le script sans paramètre, le script de hello détectera automatiquement version hello de python installé (ordre de recherche 2.7 -> 3.4 -> 3.5). Assurez-vous de la cohérence de votre version de Python pendant la création et l’exécution. 
   
   > [!NOTE] 
   Sur la création de bibliothèque cliente de Python hello (iothub_client.so) sur les périphériques de Linux qui ont moins de 1 Go de RAM, vous pouvez voir générer bloqué 98 % lors de la génération iothub_client_python.cpp comme indiqué ci-dessous `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`. Si vous rencontrez ce problème, vérifiez la consommation de mémoire hello de l’utilisation de périphériques hello `free -m command` dans une autre fenêtre de Terminal Server pendant ce temps. Si vous manquez de mémoire lors de la compilation du fichier de iothub_client_python.cpp, que vous deviez tootemporarily augmenter hello swap espace tooget toosuccessfully de mémoire disponible plus générer la bibliothèque de kit de développement logiciel de périphérique hello Python côté client.
   
1. Exécuter l’exemple d’application hello en exécutant hello de commande suivante :

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello. Et si vous utilisez python de hello 3, vous pouvez ensuite utiliser hello commande `python3 app.py '<your Azure IoT hub device connection string>'`.


   Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.

   ![Sortie - données de capteur envoyés à partir de framboises Pi tooyour IoT hub](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a>Étapes suivantes

Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub. messages de type hello toosee que votre Pi framboises a envoyé tooyour IoT hub ou envoyer des messages tooyour framboises Pi dans une interface de ligne de commande, consultez hello [gérer cloud appareil avec iothub-didacticiel de messagerie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
