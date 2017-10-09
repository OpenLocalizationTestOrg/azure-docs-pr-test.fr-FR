---
title: aaaESP8266 toocloud - se connecter de contour HUZZAH ESP8266 tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous Adafruit estompe HUZZAH ESP8266 tooAzure IoT Hub pour qu’il plateforme de cloud computing Azure toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Se connecter Adafruit estompe HUZZAH ESP8266 tooAzure IoT Hub dans le cloud de hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur DHT22, une carte Feather HUZZAH ESP8266 et IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Procédure


Se connecter Adafruit estompe HUZZAH ESP8266 tooan IoT hub que vous créez. Puis, vous exécutez un exemple d’application sur ESP8266 toocollect hello température et humidité les données à partir d’un capteur DHT22. Enfin, vous envoyez le hub IoT tooyour hello capteur données.

> [!NOTE]
> Si vous utilisez des autres cartes ESP8266, vous pouvez toujours suivre ces étapes tooconnect il tooyour IoT hub. Selon la carte hello ESP8266 vous utilisez, vous devrez peut-être tooreconfigure hello `LED_PIN`. Par exemple, si vous utilisez ESP8266 de AI-Thinker, vous pouvez modifier à partir `0` trop`2`. Vous n’avez pas encore de kit ? Obtenir à partir de hello [site Web Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Contenu

* Comment toocreate un IoT hub et inscrire un appareil pour estompe HUZZAH ESP8266
* Comment tooconnect estompe HUZZAH ESP8266 avec capteur de hello et votre ordinateur
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur le contour HUZZAH ESP8266
* Comment toosend hello tooyour IoT hub capteur données

## <a name="what-you-need"></a>Ce dont vous avez besoin

![Parties nécessaires pour hello didacticiel.](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete cette opération, vous devez hello pièces suivantes à partir de votre contour HUZZAH ESP8266 Starter Kit :

* Hello estompe HUZZAH ESP8266 carte
* Un câble USB d’un de tooType Micro USB

Vous devez également hello suivant choses pour votre environnement de développement :

* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Un Mac ou un PC exécutant Windows ou Ubuntu.
* Réseau sans fil pour tooconnect estompe HUZZAH ESP8266 à.
* Outil de configuration Internet connexion toodownload hello.
* [Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure. Les versions antérieures ne fonctionnent pas avec la bibliothèque de AzureIoT hello.

Hello éléments suivants sont facultatifs au cas où vous n’avez pas un capteur. Vous avez également option hello d’utilisation des données de capteur simulé.

* Un capteur de température et d’humidité Adafruit DHT22
* Une platine d’expérimentation
* Des câbles de liaison M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Se connecter estompe HUZZAH ESP8266 avec capteur de hello et votre ordinateur
Dans cette section, vous vous connectez tooyour du tableau capteurs de hello. Puis vous connectez votre ordinateur tooyour de périphérique pour une utilisation ultérieure.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Se connecter à un DHT22 température et humidité capteur tooFeather HUZZAH ESP8266

Utilisez hello breadboard et cavaliers fils toomake hello connexion comme suit. Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.

![Schéma des connexions](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Pour les codes confidentiels de capteur, utilisez hello suivant câblage :


| Début (capteur)           | Fin (carte)           | Couleur du câble   |
| -----------------------  | ---------------------- | ------------: |
| VDD (broche 31F)            | 3V (broche 58H)           | Câble rouge     |
| DATA (broche 32F)           | GPIO 2 (broche 46A)       | Câble bleu    |
| GND (broche 34F)            | GND (broche 56I)          | Câble noir   |

Pour plus d’informations, consultez [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) (Configuration du capteur Adafruit DHT22) et [Adafruit Feather HUZZAH ESP8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts) (Disposition des broches de l’Adafruit Feather HUZZAH ESP8266).



Votre carte Feather HUZZAH ESP8266 devrait à présent être connectée à un capteur opérationnel.

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Estompe HUZZAH ESP8266 tooyour ordinateur connecté

Comme le montre l’illustration suivante, utilisez l’ordinateur de tooyour estompe HUZZAH ESP8266 USB d’un câble tooconnect hello Micro USB tooType.

![Estompe Huzzah tooyour ordinateur connecté](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Ajouter des autorisations de port série (Ubuntu uniquement)


Si vous utilisez Ubuntu, assurez-vous que vous avez hello autorisations toooperate sur hello USB port de contour HUZZAH ESP8266. autorisations de port série tooadd, procédez comme suit :


1. Exécutez hello suivant de commandes à partir d’un terminal :

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Vous obtenez hello suivant sorties :

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Dans la sortie de hello, notez que `uucp` ou `dialout` est le nom du propriétaire de groupe de hello port USB hello.

1. Ajouter groupe toohello hello en exécutant hello de commande suivante :

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`est le nom de propriétaire de groupe de hello que vous avez obtenu à l’étape précédente de hello. `<username>` est le nom de votre utilisateur Ubuntu.

1. Déconnectez-vous d’Ubuntu et puis reconnectez-vous pour hello modification tooappear.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Collecter des données de capteur et les envoyer tooyour IoT hub

Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather HUZZAH ESP8266. exemple d’application Hello clignote hello LED sur estompe HUZZAH ESP8266 et envoie la température de hello et les données de l’humidité collectés hello DHT22 capteur tooyour IoT hub.

### <a name="get-hello-sample-application-from-github"></a>Obtenir un exemple d’application hello à partir de GitHub

exemple d’application Hello est hébergé sur GitHub. Clonez le dépôt d’exemples hello qui contient l’exemple d’application hello à partir de GitHub. dépôt d’exemples tooclone hello, procédez comme suit :

1. Ouvrez une invite de commandes ou une fenêtre de terminal.
1. Accédez tooa dossier dans lequel toobe d’application exemple hello stockée.
1. Exécutez hello de commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Installer le package de hello pour estompe HUZZAH ESP8266 Bonjour Arduino IDE :

1. Ouvrez le dossier hello où l’application d’exemple hello est stockée.
1. Ouvrez le fichier de app.ino de hello dans le dossier de l’application hello Bonjour Arduino IDE.

   ![Ouvrez l’application d’exemple hello dans Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. Bonjour Arduino IDE, cliquez sur **fichier** > **préférences**.
1. Bonjour **préférences** boîte de dialogue, cliquez sur toohello de hello icône suivant **URL du Gestionnaire de cartes supplémentaires** boîte.
1. Dans la fenêtre contextuelle de hello, entrez hello suivant l’URL, puis cliquez sur **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url du package point tooa dans Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. Bonjour **préférences** boîte de dialogue, cliquez sur **OK**.
1. Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».

   Le gestionnaire de cartes indique que ESP8266 est installé avec une version 2.2.0 ou ultérieure.

   ![Hello esp8266 package est installé](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Cliquez sur **Outils** > **Type de carte** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Installer les bibliothèques nécessaires

1. Bonjour Arduino IDE, cliquez sur **multiensembles** > **inclure une bibliothèque** > **gérer les bibliothèques**.
1. Rechercher le nom de bibliothèque un par un. Pour chacune des bibliothèques trouvées, cliquez sur **Installer**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Vous n’avez pas de capteur DHT22 ?

exemple d’application Hello permettre simuler des données de la température et humidité au cas où vous n’avez pas un capteur DHT22 réel. tooset des données toouse simulée l’application exemple hello, procédez comme suit :

1. Ouvrez hello `config.h` fichier Bonjour `app` dossier.
1. Recherchez hello ligne de code suivante et remplacez valeur hello `false` trop`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurer hello exemples application toouse simulée de données](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Enregistrez le fichier hello avec `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Déployer hello exemple application tooFeather HUZZAH ESP8266

1. Bonjour Arduino IDE, cliquez sur **outil** > **Port**, puis cliquez sur les ports série hello pour estompe HUZZAH ESP8266.
1. Cliquez sur **multiensembles** > **télécharger** toobuild et déployer hello exemple application tooFeather HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Entrer vos informations d’identification

Après avoir hello téléchargement se termine correctement, suivez ces étapes tooenter vos informations d’identification :

1. Bonjour Arduino IDE, cliquez sur **outils** > **moniteur série**.
1. Dans la fenêtre de l’analyseur série hello, notez hello deux listes déroulantes, dans le coin inférieur droit de hello.
1. Sélectionnez **aucun guillemet de fin de ligne** pour la liste déroulante gauche hello.
1. Sélectionnez **115 200 bauds** pour la liste déroulante droite hello.
1. Dans la zone d’entrée de hello situé en haut de hello de fenêtre du moniteur série hello, entrez hello informations suivantes si vous êtes invité à tooprovide, puis cliquez sur **envoyer**.
   * SSID Wi-Fi
   * Mot de passe Wi-Fi
   * Chaîne de connexion de l’appareil

> [!Note]
> informations d’identification de Hello sont stockées dans hello EEPROM de contour HUZZAH ESP8266. Si vous cliquez sur le bouton de réinitialisation hello sur hello estompe HUZZAH ESP8266 tableau, exemple d’application hello vous demande si vous souhaitez que les informations de hello tooerase. Entrez `Y` les informations de hello toohave effacées. Vous demande des informations de hello tooprovide une deuxième fois.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Vérifiez l’application d’exemple hello s’exécute correctement

Si vous voyez suivant de hello de sortie à partir de la fenêtre de l’analyseur série hello et hello clignote LED sur estompe HUZZAH ESP8266, exemple d’application hello s’exécute correctement.

![Sortie finale dans l’IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Étapes suivantes

Vous avez connecté un contour HUZZAH ESP8266 tooyour IoT hub et envoyé hello capturée capteur données tooyour IoT hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

