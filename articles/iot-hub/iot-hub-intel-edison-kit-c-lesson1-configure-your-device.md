---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 1 : configurer l’appareil | Documents Microsoft"
description: "Configurez Intel Edison pour une première utilisation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configuré, connectez-vous arduino toopc, le programme d’installation arduino, arduino carte"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Configurer votre Intel Edison
## <a name="what-you-will-do"></a>Procédure à suivre
Configurer Intel Edison pour la première utilisation en assemblant tableau hello, en cours de l’installation de configuration outil tooyour bureau du système d’exploitation tooflash microprogramme Edison ensemble et son mot de passe connectez-la tooWi Wi-Fi. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment tooassemble Edison board et mettez-le sous tension.
* Comment les microprogrammes tooflash Edison, mot de passe et vous y connecter Wi-Fi.

## <a name="what-you-need"></a>Ce dont vous avez besoin
toocomplete cette opération, vous devez hello pièces suivantes à partir de votre Intel Edison Starter Kit :

* Module Intel® Edison
* Carte d’extension Arduino
* Les barres d’espacement ni vis inclus dans le package hello, y compris des deux vis toofasten hello toohello expansion carte et quatre ensembles de vis et des séparateurs en plastique.
* Un câble USB d’un de tooType Micro B
* Une alimentation en courant continu (CC). La puissance nominale de l’alimentation doit être :
  - 7-15 V CC
  - Au moins 1 500 mA
  - code confidentiel de Hello center/interne doit être pôle positif de hello d’alimentation hello

  ![Éléments de votre Starter Kit](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Vous aurez également besoin des éléments suivants :

* Un ordinateur exécutant Windows, Mac ou Linux.
* Une connexion sans fil pour tooconnect Edison à.
* Un outil de configuration toodownload de connexion Internet.

## <a name="assemble-your-board"></a>Assembler votre carte

Cette section contient les étapes tooattach votre carte Intel® Edison tooyour d’extension.

1. Placez le module Intel® Edison hello hiérarchique de hello blanc dans votre tableau d’extension, de trous hello sur le module de hello avec vis hello sur la carte d’extension de hello s’aligne.

2. Appuyez sur le module hello juste en dessous des mots hello `What will you make?` jusqu'à ce que vous pensez qu’un composant logiciel enfichable.

   ![assemblage de carte 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Utilisez hello deux fruits hex (inclus dans le package de hello) toosecure hello toohello expansion carte.

   ![assemblage de carte 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Insérer une vis de l’une des quatre trous de coin hello sur la carte d’extension de hello. Torsion et renforcer un des séparateurs de plastique hello blanc sur vis de hello.

   ![assemblage de carte 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Répétez cette opération pour hello autres séparateurs trois angle.

   ![assemblage de carte 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Votre carte est maintenant assemblée.

   ![carte assemblée](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Mise sous tension d’Edison

1. Branchez alimentation hello.

   ![Branchement du bloc d'alimentation](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Une DEL verte (étiquetée DS1 sur hello Arduino * de carte d’extension) doit s’allumer et restent allumée.

3. Patientez une minute pour toofinish de tableau hello le démarrage.

   > [!NOTE]
   > Si vous ne disposez pas d’une alimentation de contrôleur de domaine, vous pouvez toujours de carte hello l’alimentation via un port USB. Consultez la section `Connect Edison tooyour computer` pour plus d’informations. Cette procédure de mise sous tension de votre carte peut entraîner un comportement imprévisible de la carte, en particulier si vous utilisez un réseau Wi-Fi ou des moteurs d’entraînement.

## <a name="connect-edison-tooyour-computer"></a>Connectez Edison tooyour ordinateur

1. Basculer vers le bas microrupteur hello vers hello deux micro ports USB, afin que Edison est en mode de périphérique. Veuillez vous reporter [ici](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) pour connaître les différences entre le mode appareil et le mode hôte.

   ![Basculer vers le bas microrupteur de hello](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Branchez les câbles USB micro hello le port USB supérieur micro hello.

   ![Port micro USB du haut](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Plug hello l’autre extrémité du câble USB à votre ordinateur.

   ![USB de l’ordinateur](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

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

Félicitations ! Vous avez réussi à configurer Edison.

## <a name="summary"></a>Résumé
Dans cet article, vous avez appris comment tooassemble hello du tableau de Edison, flash son microprogramme, le mot de passe le programme d’installation et le connecter tooWi Wi-Fi en utilisant l’outil de configuration. Notez que hello que voyant ne s’allume encore. la tâche suivante Hello est tooinstall hello outils et nécessaires logiciel en vue d’un exemple d’application en cours d’exécution sur Edison.

## <a name="next-steps"></a>Étapes suivantes
[Obtenir les outils de hello][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md