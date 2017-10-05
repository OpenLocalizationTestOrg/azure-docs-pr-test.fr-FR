---
title: "ESP8266 vers cloud - Connecter la carte Feather HUZZAH ESP8266 à Azure IoT Hub | Microsoft Docs"
description: "Ce didacticiel explique comment configurer la carte Adafruit Feather HUZZAH ESP8266 et la connecter à Azure IoT Hub pour envoyer des données à la plateforme cloud Azure."
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
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a>Connecter l’Adafruit Feather HUZZAH ESP8266 à Azure IoT Hub dans le cloud

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Connexion entre un capteur DHT22, une carte Feather HUZZAH ESP8266 et IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Procédure


En premier lieu, vous connecterez l’Adafruit Feather HUZZAH ESP8266 à un IoT Hub créé à cette fin. Ensuite, vous exécutez un exemple d’application sur l’ESP8266 pour collecter des données de température et d’humidité provenant d’un capteur DHT22. Enfin, vous enverrez les données du capteur à votre IoT Hub.

> [!NOTE]
> Si vous utilisez une autre carte ESP8266, vous pouvez également suivre ces étapes pour la connecter à votre IoT Hub. Selon la carte ESP8266 que vous utilisez, il se peut que vous deviez reconfigurer le paramètre `LED_PIN`. Par exemple, si vous utilisez l’ESP8266 d’AI-Thinker, vous devrez peut-être remplacer la valeur `0` de ce paramètre par `2`. Vous n’avez pas encore de kit ? Obtenez-le depuis le [site web Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Contenu

* Création d’un IoT Hub et enregistrement d’un appareil pour la carte Feather HUZZAH ESP8266
* Connexion du Feather HUZZAH ESP8266 au capteur et à votre ordinateur
* Collecte des données du capteur en exécutant un exemple d’application sur la carte Feather HUZZAH ESP8266
* Envoi des données du capteur à votre IoT Hub

## <a name="what-you-need"></a>Ce dont vous avez besoin

![Composants requis pour le didacticiel](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

Pour cette opération, vous aurez besoin des composants suivants de votre Kit de démarrage Feather HUZZAH ESP8266 :

* La carte Feather HUZZAH ESP8266
* Un câble Micro USB Micro B vers USB Type A

Vous aurez également besoin des éléments suivants pour votre environnement de développement :

* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Un Mac ou un PC exécutant Windows ou Ubuntu.
* Un réseau sans fil auquel connecter la carte Feather HUZZAH ESP8266.
* Une connexion Internet pour télécharger l’outil de configuration.
* [Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 ou ultérieure. Les versions antérieures ne fonctionneront pas avec la bibliothèque AzureIoT.

Les éléments suivants sont facultatifs si vous n’avez pas de capteur. Vous avez également la possibilité d’utiliser des données de capteur simulées.

* Un capteur de température et d’humidité Adafruit DHT22
* Une platine d’expérimentation
* Des câbles de liaison M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a>Connecter la carte Feather HUZZAH ESP8266 au capteur et à votre ordinateur
Dans cette section, vous connectez les capteurs à votre tableau. Puis vous connectez votre appareil à votre ordinateur pour une utilisation ultérieure.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a>Connecter un capteur de température et d’humidité DHT22 à la carte Feather HUZZAH ESP8266

Utilisez la platine d’expérimentation et les câbles de liaison pour effectuer la connexion comme suit. Si vous n’avez pas de capteur, ignorez cette section. Vous pourrez utiliser des données de capteur simulées à la place.

![Schéma des connexions](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Pour les broches du capteur, utilisez le câblage suivant :


| Début (capteur)           | Fin (carte)           | Couleur du câble   |
| -----------------------  | ---------------------- | ------------: |
| VDD (broche 31F)            | 3V (broche 58H)           | Câble rouge     |
| DATA (broche 32F)           | GPIO 2 (broche 46A)       | Câble bleu    |
| GND (broche 34F)            | GND (broche 56I)          | Câble noir   |

Pour plus d’informations, consultez [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) (Configuration du capteur Adafruit DHT22) et [Adafruit Feather HUZZAH ESP8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts) (Disposition des broches de l’Adafruit Feather HUZZAH ESP8266).



Votre carte Feather HUZZAH ESP8266 devrait à présent être connectée à un capteur opérationnel.

![Connexion du capteur DHT22 à la carte Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a>Connexion de la carte Feather HUZZAH ESP8266 à votre ordinateur

Comme présenté ensuite, à l’aide du câble Micro USB vers USB Type A, connectez la carte Feather HUZZAH ESP8266 à votre ordinateur.

![Connexion de la carte Feather Huzzah à votre ordinateur](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Ajouter des autorisations de port série (Ubuntu uniquement)


Si vous utilisez Ubuntu, assurez-vous que vous disposez des autorisations nécessaires pour utiliser le port USB de la carte Feather HUZZAH ESP8266. Pour ajouter des autorisations de port série, procédez comme suit :


1. Dans un terminal, exécutez les commandes suivantes :

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Vous obtenez l’une des sorties suivantes :

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   Dans la sortie, `uucp` ou `dialout` correspond au nom du propriétaire du groupe du port USB.

1. Ajoutez l’utilisateur au groupe en exécutant la commande suivante :

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>` est le nom du propriétaire du groupe que vous avez obtenu à l’étape précédente. `<username>` est le nom de votre utilisateur Ubuntu.

1. Déconnectez-vous d’Ubuntu, puis reconnectez-vous pour que la modification prenne effet.

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a>Collecter les données du capteur et les envoyer à votre IoT Hub

Dans cette section, vous allez déployer et exécuter un exemple d’application sur la carte Feather HUZZAH ESP8266. L’exemple d’application fait clignoter la LED de la carte Feather HUZZAH ESP8266 et envoie les données de température et d’humidité collectées à partir du capteur DHT22 à votre IoT Hub.

### <a name="get-the-sample-application-from-github"></a>Obtenir l’exemple d’application à partir de GitHub

L’exemple d’application est hébergé sur GitHub. Clonez l’exemple de référentiel contenant l’exemple d’application à partir de GitHub. Pour cloner l’exemple de référentiel, procédez comme suit :

1. Ouvrez une invite de commandes ou une fenêtre de terminal.
1. Accédez au dossier à utiliser pour le stockage de l’exemple d’application.
1. Exécutez la commande suivante :

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Installez le package pour la carte Feather HUZZAH ESP8266 dans l’IDE Arduino :

1. Ouvrez le dossier où l’exemple d’application est stocké.
1. Ouvrez le fichier app.ino dans le dossier app de l’IDE Arduino.

   ![Ouverture de l’exemple d’application dans l’IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. Dans l’IDE Arduino, cliquez sur **Fichier** > **Préférences**.
1. Dans la boîte de dialogue **Préférences**, cliquez sur l’icône en regard de la zone **URL de gestionnaire de cartes supplémentaires**.
1. Dans la fenêtre contextuelle, entrez l’URL suivante, puis cliquez sur **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Pointage vers l’URL d’un package dans l’IDE Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. Dans la boîte de dialogue **Préférences**, cliquez sur **OK**.
1. Cliquez sur **Outils** > **Type de carte** > **Gestionnaire de carte**, puis recherchez « esp8266 ».

   Le gestionnaire de cartes indique que ESP8266 est installé avec une version 2.2.0 ou ultérieure.

   ![Le package ESP8266 est installé](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Cliquez sur **Outils** > **Type de carte** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Installer les bibliothèques nécessaires

1. Dans l’IDE Arduino, cliquez sur **Croquis** > **Inclure une bibliothèque** > **Gérer les bibliothèques**.
1. Recherchez les noms de bibliothèque suivants un par un. Pour chacune des bibliothèques trouvées, cliquez sur **Installer**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Vous n’avez pas de capteur DHT22 ?

L’exemple d’application permet de simuler des données de température et d’humidité si vous n’avez pas de capteur DHT22. Pour configurer l’utilisation de données simulées par l’exemple d’application, procédez comme suit :

1. Ouvrez le fichier `config.h` dans le dossier `app`.
1. Recherchez la ligne de code suivante et remplacez la valeur `false` par `true` :
   ```c
   define SIMULATED_DATA true
   ```
   ![Configuration de l’exemple d’application pour utiliser des données simulées](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Enregistrez le fichier avec `Control-s`.

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a>Déployer l’exemple d’application sur la carte Feather HUZZAH ESP8266

1. Dans l’IDE Arduino, cliquez sur **outil** > **Port**, puis cliquez sur le port série pour la carte Feather HUZZAH ESP8266.
1. Cliquez sur **Croquis** > **Téléverser** pour générer et déployer l’exemple d’application sur la carte Feather HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Entrer vos informations d’identification

Une fois le chargement terminé, suivez cette procédure pour entrer vos informations d’identification :

1. Dans l’IDE Arduino, cliquez sur **Outils** > **Moniteur série**.
1. Dans la fenêtre Moniteur série, vous pouvez remarquer la présence de deux listes déroulantes dans le coin inférieur droit.
1. Pour la liste déroulante de gauche, sélectionnez **Pas de fin de ligne**.
1. Pour la liste déroulante de droite, sélectionnez **115200 baud**.
1. Dans la zone de saisie située en haut de la fenêtre Moniteur série, entrez les informations suivantes si elles vous sont demandées, puis cliquez sur **Envoyer**.
   * SSID Wi-Fi
   * Mot de passe Wi-Fi
   * Chaîne de connexion de l’appareil

> [!Note]
> Les informations d’identification sont stockées dans la mémoire EEPROM de la carte Feather HUZZAH ESP8266. Si vous cliquez sur le bouton de réinitialisation de la carte Feather HUZZAH ESP8266, l’exemple d’application vous demande si vous souhaitez effacer ces informations. Entrez `Y` pour effacer les informations. Vous êtes invité à fournir les informations une deuxième fois.

### <a name="verify-the-sample-application-is-running-successfully"></a>Vérifier que l’exemple d’application s’exécute correctement

Si vous voyez la sortie suivante dans la fenêtre Moniteur série et la LED clignoter sur la carte Feather HUZZAH ESP8266, l’exemple d’application s’exécute correctement.

![Sortie finale dans Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Étapes suivantes

Vous avez correctement connecté une carte Feather HUZZAH ESP8266 à votre IoT Hub et envoyé les données de capteur collectées à votre IoT Hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

