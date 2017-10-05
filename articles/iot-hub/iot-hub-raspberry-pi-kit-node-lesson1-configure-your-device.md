---
title: "Connecter Raspberry Pi (Node) à Azure IoT - Leçon 1 : Configurer l’appareil | Microsoft Docs"
description: Configure Raspberry Pi 3 for first-time use and install the Raspbian OS, a free operating system that is optimized for the Raspberry Pi hardware.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "installer raspbian, téléchargement de raspbian, installation de raspbian, configuration de raspbian, raspberry pi installer raspbian, raspberry pi installer le système d’exploitation, raspberry pi installer la carte sd, connexion de raspberry pi, connexion à raspberry pi, connectivité de raspberry pi"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b848c48157a2310f0eb1d6398f8b9aaa4395d47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a>Configurer votre appareil
## <a name="what-you-will-do"></a>Procédure à suivre
Configurez Pi pour une première utilisation et installez le système d’exploitation Raspbian. Raspbian est un système d’exploitation gratuit optimisé pour le matériel Raspberry Pi. Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Installation de Raspbian sur Pi.
* Mise sous tension de Pi à l’aide d’un câble USB.
* Connexion de Pi au réseau à l’aide d’un câble Ethernet ou d’un réseau sans fil.
* Ajout d’une LED sur la platine d’expérimentation et connexion à Pi.

## <a name="what-you-will-need"></a>Éléments requis
Pour cette opération, vous aurez besoin des composants suivants de votre Starter Kit Raspberry Pi 3 :

* Carte Raspberry Pi 3
* Carte microSD de 16 Go
* Alimentation 5V 2A avec le câble micro USB de 6 pieds (~183 cm)
* Platine d’expérimentation
* Câbles de connexion
* Résistance de 560 Ohm
* LED de 10 mm diffuse
* Câble Ethernet

![Éléments de votre Starter Kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Vous aurez également besoin des éléments suivants :

* Une connexion câblée ou sans fil pour la connexion de Pi.
* Un adaptateur USB-SD ou une carte mini-SD pour graver l’image du système d’exploitation sur la carte microSD.
* Un ordinateur exécutant Windows, Mac ou Linux. L’ordinateur est utilisé pour installer Raspbian sur la carte microSD.
* Une connexion Internet pour télécharger les outils et le logiciel nécessaires.

## <a name="install-raspbian-on-the-microsd-card"></a>Installation de Raspbian sur la carte microSD
Préparez la carte microSD pour l’installation de l’image Raspbian.

1. Téléchargez Raspbian.
   1. [Téléchargez](https://www.raspberrypi.org/downloads/raspbian/) le fichier .zip pour Raspbian Jessie avec Pixel.
   2. Extrayez l’image Raspbian dans un dossier sur votre ordinateur.
2. Installez Raspbian sur la carte microSD.
   1. [Téléchargez](https://www.etcher.io) et installez l’utilitaire de graveur de carte SD Etcher.
   2. Exécutez Etcher et sélectionnez l’image Raspbian extraite à l’étape 1.
   3. Sélectionnez le lecteur de carte microSD.
      Remarque : Etcher a peut-être déjà sélectionné le lecteur approprié.
   4. Cliquez sur **Flash** pour installer Raspbian sur la carte microSD.
   5. Retirez la carte microSD de votre ordinateur une fois l’installation terminée.
      Vous pouvez retirer directement la carte microSD en toute sécurité, car Etcher éjecte ou démonte automatiquement la carte microSD une fois le processus terminé.
   6. Insérez la carte microSD dans Pi.

![Insertion de la carte SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Mise sous tension de Pi
Mettez Pi sous tension à l’aide du câble micro USB et de l’alimentation.

![Mise sous tension](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Il est important d’utiliser l’alimentation fournie dans le kit qui dispose d’une puissance d’au moins 2A pour vous assurer que votre Raspberry dispose d’une puissance suffisante pour fonctionner correctement.

## <a name="enable-ssh"></a>Activation de SSH
En date de la version de novembre 2016, Raspbian a le serveur SSH désactivé par défaut. Vous devez l’activer manuellement. Vous pouvez faire référence aux [instructions officielles](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou connecter un écran et accéder à **Préférences-> Configuration de Raspberry Pi** pour activer SSH.

## <a name="connect-raspberry-pi-3-to-the-network"></a>Connexion de Raspberry Pi 3 au réseau
Vous pouvez connecter Pi à un réseau câblé ou à un réseau sans fil. Assurez-vous que Pi est connecté au même réseau que votre ordinateur. Par exemple, vous pouvez connecter Pi au même commutateur que celui utilisé par votre ordinateur.

### <a name="connect-to-a-wired-network"></a>Connexion à un réseau câblé
Utilisez le câble Ethernet pour connecter Pi à votre réseau câblé. Si la connexion est établie, les deux LED sur Pi s’allument.

![Connexion à l’aide d’un câble Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a>Connexion à un réseau sans fil
Suivez les [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) de Raspberry Pi Foundation pour connecter Pi à votre réseau sans fil. Ces instructions nécessitent tout d’abord de connecter un moniteur et un clavier à Pi.

## <a name="connect-the-led-to-pi"></a>Connexion de la LED à Pi
Pour effectuer cette tâche, utilisez la [platine d’expérimentation](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), les câbles de connexion, la LED et la résistance. Connectez-les aux ports [d’entrée/sortie à usage général](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) de Pi.

![Platine d’expérimentation, LED et résistance](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Connectez la broche la plus courte de la LED à **GPIO GND (broche 6)**.
2. Connectez la broche la plus longue de la LED à une broche de la résistance.
3. Connectez l’autre broche de la résistance à **GPIO 4 (broche 7)**.

Notez que la polarité de la LED est importante. Ce paramètre de polarité est communément appelé Faible actif.

![Brochage](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Félicitations ! Vous avez réussi à configurer Pi.

## <a name="summary"></a>Résumé
Dans cet article, vous avez appris à configurer Pi en installant Raspbian, en connectant Pi à un réseau et en connectant une LED à Pi. Notez que la LED n’est pas encore allumée. La tâche suivante consiste à installer les outils et le logiciel nécessaires en vue d’exécuter un exemple d’application sur Pi.

![Le matériel est prêt.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Étapes suivantes
[Obtention des outils](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

