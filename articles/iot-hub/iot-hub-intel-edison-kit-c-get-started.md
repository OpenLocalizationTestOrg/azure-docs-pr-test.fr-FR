---
title: aaaIntel Edison toocloud (C) - se connecter le Edison Intel tooAzure IoT Hub | Documents Microsoft
description: "Découvrez comment toosetup et connectez-vous Intel Edison tooAzure IoT Hub pour la plateforme de cloud computing Azure Intel Edison toosend données toohello dans ce didacticiel."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot intel edison, intel hub iot d’edison, intel edison envoyer des données toocloud, intel edison toocloud"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a>Se connecter Intel Edison tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Dans ce didacticiel, commencer par découvrir hello des bases de l’utilisation de Edison d’Intel. Vous apprendrez ensuite comment tooseamlessly connecter votre cloud toohello de périphériques à l’aide de [Azure IoT Hub](iot-hub-what-is-iot-hub.md).

Vous n’avez pas encore de kit ? Démarrer [ici](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>Procédure

* Configurez Intel Edison et les modules Grove.
* Créez un hub IoT.
* Inscrivez un appareil pour Edison dans votre IoT Hub.
* Exécuter un exemple d’application sur le concentrateur de Edison toosend capteur données tooyour IoT.

Connectez Intel Edison tooan IoT concentrateur que vous créez. Puis vous exécutez un exemple d’application sur Edison toocollect température et humidité les données à partir d’un capteur de température Grove. Enfin, vous envoyez le hub IoT tooyour hello capteur données.

## <a name="what-you-learn"></a>Contenu

* Comment toocreate un Azure IoT hub et obtenir votre nouvelle chaîne de connexion de périphérique.
* Comment tooconnect Edison avec un capteur de température Grove.
* Comment les données de capteur toocollect par un exemple d’application en cours d’exécution sur Edison.
* Comment le hub IoT tooyour toosend capteur données.

## <a name="what-you-need"></a>Ce dont vous avez besoin

![Ce dont vous avez besoin](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* Hello Conseil d’Intel Edison
* Carte d’extension Arduino
* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte d’évaluation Azure gratuit](https://azure.microsoft.com/free/) en quelques minutes.
* Un Mac ou un PC exécutant Windows ou Linux.
* Une connexion Internet.
* Un câble USB d’un de tooType Micro B
* Une alimentation en courant continu (CC). La puissance nominale de l’alimentation doit être :
  - 7-15 V CC
  - Au moins 1 500 mA
  - code confidentiel de Hello center/interne doit être pôle positif de hello d’alimentation hello

Hello éléments suivants est facultatif :

* Grove Base Shield V2
* Capteur de température Grove
* Câble Grove
* Les barres d’espacement ni vis inclus dans le package hello, y compris des deux vis toofasten hello toohello expansion carte et quatre ensembles de vis et des séparateurs en plastique.

> [!NOTE] 
Ces éléments sont facultatifs, car la prise en charge des exemples de code hello simulée des données de capteur.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Configuration d’Intel Edison

### <a name="assemble-your-board"></a>Assembler votre carte

Cette section contient les étapes tooattach votre carte Intel® Edison tooyour d’extension.

1. Placez le module Intel® Edison hello hiérarchique de hello blanc dans votre tableau d’extension, de trous hello sur le module de hello avec vis hello sur la carte d’extension de hello s’aligne.

2. Appuyez sur le module hello juste en dessous des mots hello `What will you make?` jusqu'à ce que vous pensez qu’un composant logiciel enfichable.

   ![assemblage de carte 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. Utilisez hello deux fruits hex (inclus dans le package de hello) toosecure hello toohello expansion carte.

   ![assemblage de carte 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. Insérer une vis de l’une des quatre trous de coin hello sur la carte d’extension de hello. Torsion et renforcer un des séparateurs de plastique hello blanc sur vis de hello.

   ![assemblage de carte 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. Répétez cette opération pour hello autres séparateurs trois angle.

   ![assemblage de carte 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

Votre carte est maintenant assemblée.

   ![carte assemblée](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Se connecter hello Grove Base bouclier et capteur de température hello

1. Placez hello Grove Base bouclier sur tooyour carte. Assurez-vous que toutes les broches sont bien insérées dans votre carte.
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. Capteur de température utilisez Grove câble tooconnect Grove sur hello Grove Base bouclier **A0** port.

   ![Se connecter tootemperature capteur](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Connexion d’Edison et du capteur](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

Votre capteur est maintenant prêt.

### <a name="power-up-edison"></a>Mise sous tension d’Edison

1. Branchez alimentation hello.

   ![Branchement du bloc d'alimentation](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. Une DEL verte (étiquetée DS1 sur hello Arduino * de carte d’extension) doit s’allumer et restent allumée.

3. Patientez une minute pour toofinish de tableau hello le démarrage.

   > [!NOTE]
   > Si vous ne disposez pas d’une alimentation de contrôleur de domaine, vous pouvez toujours de carte hello l’alimentation via un port USB. Consultez la section `Connect Edison tooyour computer` pour plus d’informations. Cette procédure de mise sous tension de votre carte peut entraîner un comportement imprévisible de la carte, en particulier si vous utilisez un réseau Wi-Fi ou des moteurs d’entraînement.

### <a name="connect-edison-tooyour-computer"></a>Connectez Edison tooyour ordinateur

1. Basculer vers le bas microrupteur hello vers hello deux micro ports USB, afin que Edison est en mode de périphérique. Veuillez vous reporter [ici](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) pour connaître les différences entre le mode appareil et le mode hôte.

   ![Basculer vers le bas microrupteur de hello](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. Branchez les câbles USB micro hello le port USB supérieur micro hello.

   ![Port micro USB du haut](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. Plug hello l’autre extrémité du câble USB à votre ordinateur.

   ![USB de l’ordinateur](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. Vous saurez que votre carte est entièrement initialisée lorsque l’ordinateur monte un nouveau lecteur (comme lorsque vous insérez une carte SD dans votre ordinateur).

## <a name="download-and-run-hello-configuration-tool"></a>Téléchargez et exécutez l’outil de configuration hello
Obtenir hello dernier outil de configuration à partir de [ce lien](https://software.intel.com/en-us/iot/hardware/edison/downloads) répertoriés sous hello `Installers` titre. Exécutez l’outil de hello et suivez sa à l’écran des instructions, en cliquant sur Suivant si nécessaire

### <a name="flash-firmware"></a>Flashage du microprogramme
1. Sur hello `Set up options` , cliquez sur `Flash Firmware`.
2. Sélectionnez tooflash d’image hello sur votre carte mère en effectuant l’une des manières suivantes les hello :
   - toodownload et flash votre carte mère avec hello dernière image de microprogramme auprès d’Intel, sélectionnez `Download hello latest image version xxxx`.
   - sélectionner de votre tableau avec une image que vous avez déjà enregistré sur votre ordinateur, tooflash `Select hello local image`. Parcourir tooand hello sélectionnez image de carte de tooyour tooflash.
3. outil de configuration Hello va tenter de tooflash votre carte mère. processus clignotant Hello peut prendre jusqu'à too10 minutes.

### <a name="set-password"></a>Définition du mot de passe
1. Sur hello `Set up options` , cliquez sur `Enable Security`.
2. Vous pouvez attribuer un nom personnalisé à votre carte Intel® Edison. Cette étape est facultative.
3. Tapez un mot de passe pour votre carte, puis cliquez sur `Set password`.
4. Démarquer hello un mot de passe qui sera utilisé ultérieurement.

### <a name="connect-wi-fi"></a>Connexion Wi-Fi
1. Sur hello `Set up options` , cliquez sur `Connect Wi-Fi`. Attente d’une minute tooone sous la forme d’analyses de votre ordinateur pour les réseaux Wi-Fi disponibles.
2. À partir de hello `Detected Networks` liste déroulante, sélectionnez votre réseau.
3. À partir de hello `Security` liste déroulante, le type de sécurité du réseau : sélectionnez hello.
4. Indiquez vos identifiant et mot de passe, puis cliquez sur `Configure Wi-Fi`.
5. Démarquer hello adresse IP, qui est utilisée ultérieurement.

> [!NOTE]
> Assurez-vous que Edison est connecté toohello même réseau que votre ordinateur. Votre ordinateur connecte tooyour Edison en utilisant l’adresse IP de hello.

   ![Se connecter tootemperature capteur](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

Félicitations ! Vous avez réussi à configurer Edison.

## <a name="run-a-sample-application-on-intel-edison"></a>Exécution d’un exemple d’application sur Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Préparer hello SDK de périphérique Azure IoT

1. Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooyour Edison d’Intel. adresse IP de Hello est à partir de l’outil de configuration hello et mot de passe hello hello que vous avez définie dans cet outil.
    - [PuTTY](http://www.putty.org/) pour Windows.
    - client SSH intégré de Hello sur Ubuntu ou macOS (exécutez `ssh root@"hello IP address"`).

2. Clone hello exemple client tooyour périphérique d’application. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. Puis accédez hello de toorun du dossier de dépôt toohello suivant toobuild de commande Azure IoT SDK

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a>Configurer l’application d’exemple hello

1. Ouvrez le fichier de configuration de hello en hello suivant les commandes en cours d’exécution :

   ```bash
   nano config.h
   ```

   ![Fichier de configuration](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   Deux éléments de type macros peuvent être configurés dans ce fichier. Bonjour tout d’abord un est `INTERVAL`, qui définit l’intervalle de temps hello entre les deux messages toocloud d’envoi. Hello deuxième `SIMULATED_DATA`, qui est une valeur booléenne pour toouse indique si les données de capteur simulé ou non.

   Si vous **n’avez pas capteur de hello**, affectez la valeur hello `SIMULATED_DATA` valeur trop`1` toomake hello exemple d’application, créer et utiliser des données de capteur simulé.

2. Enregistrez et quittez en appuyant sur Ctrl-O > Entrée > Ctrl-X.

### <a name="build-and-run-hello-sample-application"></a>Générer et exécuter l’exemple d’application hello

1. Générer l’exemple d’application hello en exécutant hello de commande suivante :

   ```bash
   cmake . && make
   ```
   ![Sortie de la génération](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. Exécuter l’exemple d’application hello en exécutant hello de commande suivante :

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Assurez-vous que vous copier-coller chaîne de connexion de périphérique hello dans des guillemets simples de hello.

Vous devez voir qu’affiche hello messages hello et les données de capteur envoyés tooyour IoT hub de sortie suivant de hello.

![Sortie - données de capteur envoyés à partir d’Intel Edison tooyour IoT hub](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a>Étapes suivantes

Vous avez exécuté un exemple de données de capteur application toocollect et envoyez tooyour IoT hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
