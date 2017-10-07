---
title: "M0 toocloud : connexion Wi-Fi de contour M0 tooAzure IoT Hub | Documents Microsoft"
description: "Découvrez comment tooset configurer et connecter Adafruit estompe M0 WiFi tooAzure plateforme de cloud computing Azure IoT Hub toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Connexion Wi-Fi de Adafruit estompe M0 tooAzure IoT Hub dans le cloud de hello
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur BME280, une carte Feather M0 WiFi et IoT Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

Dans ce didacticiel, commencer par découvrir hello les bases de l’utilisation de votre tableau Arduino. Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>Procédure

Connexion Wi-Fi de Adafruit estompe M0 tooan IoT hub que vous créez. Puis, vous exécutez un exemple d’application sur Wi-Fi M0 toocollect hello température et humidité les données à partir d’un BME280. Enfin, vous envoyez le hub IoT tooyour hello capteur données.


## <a name="what-you-learn"></a>Contenu

* Comment toocreate un IoT hub et inscrire un appareil pour le Wi-Fi de contour M0
* Comment tooconnect estompe M0 WiFi avec capteur de hello et votre ordinateur
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur le contour M0 WiFi
* Comment toosend hello tooyour IoT hub capteur données

## <a name="what-you-need"></a>Ce dont vous avez besoin

![Parties nécessaires pour hello didacticiel.](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete cette opération, vous devez hello pièces suivantes à partir de votre Starter Kit de contour M0 Wi-Fi :

* Hello estompe M0 WiFi tableau
* Un câble USB d’un de tooType Micro USB

Vous devez également hello suivant choses pour votre environnement de développement :

* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Un Mac ou un PC exécutant Windows ou Ubuntu.
* Un réseau sans fil pour tooconnect estompe M0 WiFi à.
* Un outil de configuration Internet connexion toodownload hello.
* [Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure. Les versions antérieures ne fonctionnent pas avec la bibliothèque de Azure IoT Hub hello.

Si vous n’avez pas un capteur, hello éléments suivants est facultatif. Vous avez également option hello d’utilisation des données de capteur simulée :

* Un capteur de température et d’humidité BME280
* Une platine d’expérimentation
* Des câbles de liaison M/M

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Connexion Wi-Fi de contour M0 avec capteur de hello et votre ordinateur
Dans cette section, vous vous connectez tooyour du tableau capteurs de hello. Puis vous connectez votre ordinateur tooyour de périphérique pour une utilisation ultérieure.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Se connecter à un DHT22 température et humidité capteur tooFeather Wi-Fi M0

Utilisez hello breadboard et cavaliers fils toomake hello la connexion. Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.

![Schéma des connexions](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Pour les codes confidentiels de capteur, utilisez hello suivant câblage :


| Début (capteur)           | Fin (carte)            | Couleur du câble   |
| -----------------------  | ---------------------- | ------------: |
| VDD (broche 27A)            | 3V (broche 3A)            | Câble rouge     |
| GND (broche 29A)            | GND (broche 6A)           | Câble noir   |
| SCK (broche 30A)            | SCK (broche 12A)          | Câble jaune  |
| SDO (broche 31A)            | MI (broche 14A)           | Câble blanc   |
| SDI (broche 32A)            | M0 (broche 13A)           | Câble bleu    |
| CS (broche 33A)             | GPIO 5 (broche 15J)       | Câble orange  |

Pour plus d’informations, consultez [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) (Atelier sur le capteur de température, de pression barométrique et d’humidité Adafruit BME280) et [Adafruit Feather M0 WiFi Pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts) (Brochages de la carte Adafruit Feather M0 WiFi).



Votre carte Feather M0 WiFi devrait à présent être connectée à un capteur opérationnel.

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Connexion Wi-Fi de contour M0 tooyour ordinateur

Utilisez hello Micro tooType USB d’un câble tooconnect estompe M0 WiFi tooyour ordinateur USB, comme indiqué :

![Estompe Huzzah tooyour ordinateur connecté](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Ajouter des autorisations de port série (Ubuntu uniquement)

Si vous utilisez Ubuntu, assurez-vous que vous avez hello autorisations toooperate sur hello USB port de contour M0 Wi-Fi. autorisations de port série tooadd, procédez comme suit :


1. À un terminal, exécutez hello suivant de commandes :

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Vous obtenez hello suivant sorties :

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Dans la sortie de hello, notez que `uucp` ou `dialout` est le nom du propriétaire de groupe de hello port USB hello.

2. tooadd hello toohello groupe d’utilisateurs, exécutez hello de commande suivante :

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   Dans l’étape précédente de hello, vous avez obtenu le nom du propriétaire du groupe hello `<group-owner-name>`. Votre nom d’utilisateur Ubuntu est `<username>`.

3. Pour hello modification tooappear, déconnectez-vous d’Ubuntu et puis reconnectez-vous.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Collecter des données de capteur et les envoyer tooyour IoT hub

Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather M0 WiFi. exemple d’application Hello rend hello blink LED sur estompe M0 WiFi. Il envoie ensuite la température de hello et données de l’humidité collectés hello BME280 capteur tooyour IoT hub.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Obtenir un exemple d’application hello à partir de GitHub et préparer hello Arduino IDE

exemple d’application Hello est hébergé sur GitHub. Clonez le dépôt d’exemples hello qui contient l’exemple d’application hello à partir de GitHub. dépôt d’exemples tooclone hello, procédez comme suit :

1. Ouvrez une invite de commandes ou une fenêtre de terminal.

2. Accédez tooa dossier dans lequel toobe d’application exemple hello stockée.
3. Exécutez hello de commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Installer hello pour le Wi-Fi de contour M0 Bonjour Arduino IDE

1. Ouvrez le dossier hello où l’application d’exemple hello est stockée.

2. Ouvrez le fichier de app.ino de hello dans le dossier de l’application hello Bonjour Arduino IDE.

   ![Ouvrez l’application d’exemple hello dans Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Cliquez sur **fichier** > **préférences** (Windows/Linux) ou **Arduino** > **préférences** (Mac) et la copie et Coller avec liaison ci-dessous hello en hello **URL du Gestionnaire de cartes supplémentaires** option Bonjour préférences Arduino IDE.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Cliquez sur **outils** > **tableau** > **Gestionnaire de cartes**, puis installez hello `Arduino SAMD Boards` version `1.6.2` ou version ultérieure. 

1. Ensuite, dans hello même fenêtre, installez `Adafruit SAMD Boards` définitions de fichier de carte tooadd hello du package.

   ![Hello esp8266 package est installé](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Cliquez sur **Outils** > **Carte** > **Adafruit M0 WiFi**.

5. Installez les pilotes (pour Windows uniquement). Lorsque vous branchez estompe M0 WiFi, vous devrez peut-être tooinstall un pilote. Cliquez sur [hello lien de téléchargement sur la page Web de hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) programme d’installation du pilote toodownload hello. Suivez hello étapes tooinstall hello pilotes.

### <a name="install-necessary-libraries"></a>Installer les bibliothèques nécessaires

1. Bonjour Arduino IDE, cliquez sur **multiensembles** > **inclure une bibliothèque** > **gérer les bibliothèques**.

2. Rechercher le nom de bibliothèque un par un. Pour chacune des bibliothèques trouvées, cliquez sur **Installer** :

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Installez manuellement `Adafruit_WINC1500`. Accédez trop[ce site Web](https://github.com/adafruit/Adafruit_WINC1500) et cliquez sur **Clone ou téléchargement** > **ZIP de téléchargement**. Dans votre IDE Arduino, passez trop**multiensembles** > **inclure une bibliothèque** > **ajouter .zip bibliothèque** et ajoutez le fichier zip de hello.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Utilisez l’exemple d’application hello si vous n’avez pas un capteur BME280 réel

Si vous n’avez pas un capteur BME280 réel, exemple d’application hello permettre simuler des données de la température et humidité. tooset des données toouse simulée l’application exemple hello, procédez comme suit :

1. Ouvrez hello `config.h` fichier Bonjour `app` dossier.

2. Recherchez hello ligne de code suivante et remplacez valeur hello `false` trop`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurer hello exemples application toouse simulée de données](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Enregistrez le fichier hello avec `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Déployer hello exemple application tooFeather Wi-Fi M0

1. Bonjour Arduino IDE, cliquez sur **outil** > **Port**, puis cliquez sur les ports série hello pour le Wi-Fi de contour M0.

2. Cliquez sur **multiensembles** > **télécharger** toobuild et déployer hello exemple application tooFeather Wi-Fi M0.

### <a name="enter-your-credentials"></a>Entrer vos informations d’identification

Après avoir hello téléchargement se termine correctement, suivez ces étapes tooenter vos informations d’identification :

1. Bonjour Arduino IDE, cliquez sur **outils** > **moniteur série**.

2. Dans hello bas à droite de fenêtre du moniteur série hello, sélectionnez **aucun guillemet de fin de ligne** dans la liste déroulante de hello sur hello gauche.
3. Sélectionnez **115 200 bauds** dans la liste déroulante hello hello droite.
4. Dans la zone d’entrée de hello haut hello, entrez hello informations suivantes si vous êtes invité tooprovide, puis cliquez sur **envoyer**:

   * SSID Wi-Fi
   * Mot de passe Wi-Fi
   * Chaîne de connexion de l’appareil

> [!Note]
> informations d’identification de Hello sont stockées dans hello EEPROM de contour M0 Wi-Fi. Si vous cliquez sur le bouton Réinitialiser hello hello estompe M0 WiFi tableau, exemple d’application hello vous demande si vous souhaitez que les informations de hello tooerase. Entrez `Y` plus d’informations tooerase hello. Vous devez indiquer les informations de hello tooprovide une deuxième fois.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Vérifiez que les application d’exemple hello s’exécute avec succès

Si vous voyez suivant de hello la sortie à partir de la fenêtre de l’analyseur série hello et hello clignote LED sur estompe M0 Wi-Fi, exemple d’application hello est exécuté avec succès :

![Sortie finale dans l’IDE Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Étapes suivantes

Vous avez connecté le Wi-Fi de contour M0 tooyour IoT hub et envoyé hello capturée capteur données tooyour IoT hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

