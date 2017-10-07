---
title: aaaESP8266 toocloud - se connecter Sparkfun ESP8266 chose Dev tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous de plateforme de cloud computing Azure toosend données toohello Sparkfun ESP8266 chose Dev tooAzure IoT Hub pour qu’il dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Se connecter Sparkfun ESP8266 chose Dev tooAzure IoT Hub dans le cloud de hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![connexion entre un capteur DHT22, Thing Dev et IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Procédure à suivre

Se connecter Sparkfun ESP8266 chose Dev tooan IoT hub, que vous allez créer. Puis exécutez un exemple d’application sur les données de température et humidité toocollect ESP8266 à partir d’un capteur DHT22. Enfin, envoyez le hub IoT tooyour hello capteur données.

> [!NOTE]
> Si vous utilisez des autres cartes ESP8266, vous pouvez toujours suivre ces étapes tooconnect il tooyour IoT hub. Selon la carte hello ESP8266 que vous utilisez, vous devrez peut-être tooreconfigure hello `LED_PIN`. Par exemple, si vous utilisez ESP8266 de AI-Thinker, vous pouvez le changer à partir de `0` trop`2`. Vous n’avez pas encore de kit ? Cliquez [ici](http://azure.com/iotstarterkits).

## <a name="what-you-will-learn"></a>Contenu

* Comment toocreate un IoT hub et inscrire un appareil d’espace réservé de chose pour
* Comment tooconnect chose Dev avec capteur de hello et votre ordinateur.
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur l’élément réservé
* Comment toosend hello tooyour IoT hub capteur données.

## <a name="what-you-will-need"></a>Éléments requis

![Parties nécessaires pour hello didacticiel.](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete cette opération, vous devez hello pièces suivantes à partir de votre Starter Kit de développement de chose :

* Hello Sparkfun ESP8266 chose Dev tableau.
* Un Micro USB tooType un câble.

Éléments de hello suivants sont également nécessaires pour votre environnement de développement :

* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Un Mac ou un PC exécutant Windows ou Ubuntu.
* Réseau sans fil pour tooconnect Sparkfun ESP8266 chose Dev à.
* Outil de configuration Internet connexion toodownload hello.
* [Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (ou ultérieure), les versions antérieures ne fonctionnent pas avec la bibliothèque de AzureIoT hello.

Hello éléments suivants sont facultatifs au cas où vous n’avez pas un capteur. Vous avez également option hello d’utilisation des données de capteur simulé.

* Un capteur de température et d’humidité Adafruit DHT22.
* Une platine d’expérimentation.
* Des câbles de liaison M/M.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Se connecter ESP8266 chose Dev avec capteur de hello et votre ordinateur

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Se connecter à un capteur de température et humidité DHT22 tooESP8266 chose Dev

Utilisez hello breadboard et cavaliers fils toomake hello connexion comme suit. Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.

![Schéma des connexions](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Pour les codes confidentiels de capteur, nous allons utiliser hello suivant câblage :

| Début (capteur)           | Fin (carte)           | Couleur du câble   |
| -----------------------  | ---------------------- | ------------: |
| VDD (broche 27F)            | 3V (broche 8A)           | Câble rouge     |
| DATA (broche 28F)           | GPIO 2 (broche 9A)       | Câble blanc    |
| GND (broche 30F)            | GND (broche 7J)          | Câble noir   |


- Pour en savoir plus, consultez les [détails de la configuration du capteur DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) et les [spécifications relatives à la carte Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711).

Votre carte Sparkfun ESP8266 Thing Dev devrait à présent être connectée à un capteur opérationnel.

![connecter un capteur dht22 à la carte ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Se connecter Sparkfun ESP8266 chose Dev tooyour ordinateur

Utilisez hello Micro USB tooType USB d’un câble tooconnect Sparkfun ESP8266 chose tooyour ordinateur Dev comme suit.

![estompe huzzah tooyour ordinateur connecté](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Ajouter des autorisations de port série (Ubuntu uniquement)

Si vous utilisez Ubuntu, assurez-vous qu’utilisateur normal a hello autorisations toooperate sur hello USB port de Sparkfun ESP8266 chose dev. autorisations de port série tooadd pour un utilisateur normal, procédez comme suit :

1. Exécutez hello suivant de commandes à partir d’un terminal :

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Vous obtenez hello suivant sorties :

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Dans la sortie de hello, notez `uucp` ou `dialout` qui est hello propriétaire du nom du groupe de hello port USB.

1. Ajouter groupe toohello hello en exécutant hello de commande suivante :

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`est le nom de propriétaire de groupe de hello que vous avez obtenu à l’étape précédente de hello. `<username>` est le nom de votre utilisateur Ubuntu.

1. Fermez la session Ubuntu, qu’elle contient à nouveau pour modifier un effet de tootake hello.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Collecter des données de capteur et les envoyer tooyour IoT hub

Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Sparkfun ESP8266 Thing Dev. exemple d’application Hello clignote hello LED sur Sparkfun ESP8266 chose Dev et envoie la température de hello et les données de l’humidité collectés hello DHT22 capteur tooyour IoT hub.

### <a name="get-hello-sample-application-from-github"></a>Obtenir un exemple d’application hello à partir de GitHub

exemple d’application Hello est hébergé sur GitHub. Clonez le dépôt d’exemples hello qui contient l’exemple d’application hello à partir de GitHub. dépôt d’exemples tooclone hello, procédez comme suit :

1. Ouvrez une invite de commandes ou une fenêtre de terminal.
1. Accédez tooa dossier dans lequel toobe d’application exemple hello stockée.
1. Exécutez hello de commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Installer le package de hello pour le développement de chose Sparkfun ESP8266 dans Arduino IDE :

1. Ouvrez le dossier hello où l’application d’exemple hello est stockée.
1. Ouvrez le fichier de app.ino de hello dans le dossier de l’application hello dans Arduino IDE.

   ![Ouvrez l’application d’exemple hello dans arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. Bonjour Arduino IDE, cliquez sur **fichier** > **préférences**.
1. Bonjour **préférences** boîte de dialogue, cliquez sur toohello de hello icône suivant **URL du Gestionnaire de cartes supplémentaires** zone de texte.
1. Dans la fenêtre contextuelle de hello, entrez hello suivant l’URL, puis cliquez sur **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url du package point tooa dans arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. Bonjour **préférences** boîte de dialogue, cliquez sur **OK**.
1. Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».
   La version 2.2.0 ou ultérieure du package ESP8266 doit être installée.

   ![Hello esp8266 package est installé](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Cliquez sur **Outils** > **Carte** > **Sparkfun ESP8266 Thing Dev**.

### <a name="install-necessary-libraries"></a>Installer les bibliothèques nécessaires

1. Bonjour Arduino IDE, cliquez sur **multiensembles** > **inclure une bibliothèque** > **gérer les bibliothèques**.
1. Rechercher le nom de bibliothèque un par un. Pour chaque bibliothèque hello vous trouvez, cliquez sur **installer**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Vous n’avez pas de capteur DHT22 ?

exemple d’application Hello permettre simuler des données de la température et humidité au cas où vous n’avez pas un capteur DHT22 réel. données de toouse simulée d’application d’exemple hello tooenable, procédez comme suit :

1. Ouvrez hello `config.h` fichier Bonjour `app` dossier.
1. Recherchez hello ligne de code suivante et remplacez valeur hello `false` trop`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurer hello exemples application toouse simulée de données](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Enregistrez avec `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Déployer hello exemple application tooSparkfun ESP8266 chose Dev

1. Bonjour Arduino IDE, cliquez sur **outil** > **Port**, puis cliquez sur les ports série hello pour Sparkfun ESP8266 chose réservé
1. Cliquez sur **multiensembles** > **télécharger** toobuild et déployer hello exemple application tooSparkfun ESP8266 chose réservé

> [!Note]
> Si vous utilisez macOS, vous obtiendrez probablement hello suivant des messages lors du téléchargement. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Ouvrez la fenêtre ternimal et terminer ci-dessous actions toosolve ce problème.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Entrer vos informations d’identification

Une fois le téléchargement de hello se termine correctement, suivez hello étapes tooenter vos informations d’identification :

1. Bonjour Arduino IDE, cliquez sur **outils** > **moniteur série**.
1. Dans la fenêtre de l’analyseur série hello, notez hello deux listes déroulantes, sur hello coin inférieur droit.
1. Sélectionnez **aucun guillemet de fin de ligne** pour la liste déroulante gauche hello.
1. Sélectionnez **115 200 bauds** pour la liste déroulante droite hello.
1. Dans la zone d’entrée de hello situé en haut de hello de fenêtre du moniteur série hello, entrez hello informations suivantes si vous êtes invité à tooprovide, puis cliquez sur **envoyer**.
   * SSID Wi-Fi
   * Mot de passe Wi-Fi
   * Chaîne de connexion de l’appareil

> [!Note]
> informations d’identification de Hello sont stockées dans hello EEPROM de Sparkfun ESP8266 chose dev. Si vous cliquez sur le bouton de réinitialisation hello sur hello Sparkfun ESP8266 chose Dev tableau, exemple d’application hello vous demande si vous souhaitez que les informations de hello tooerase. Entrez `Y` toohave hello informations est effacée et vous êtes invité à nouveau les informations de hello tooprovide.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Vérifiez l’application d’exemple hello s’exécute correctement

Si vous voyez suivant de hello de sortie à partir de la fenêtre de l’analyseur série hello et hello clignote LED sur le développement de chose Sparkfun ESP8266, exemple d’application hello s’exécute correctement.

![Sortie finale dans l’IDE Arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Étapes suivantes

Vous avez connecté un Sparkfun ESP8266 chose Dev tooyour IoT hub et envoyé hello capturée capteur données tooyour IoT hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
