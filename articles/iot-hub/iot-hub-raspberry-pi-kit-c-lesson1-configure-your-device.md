---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : configurer l’appareil | Documents Microsoft"
description: "Configurer framboises Pi 3 pour la première utilisation et installer hello Raspbian du système d’exploitation, un système d’exploitation libre qui est optimisé pour hello matériel de framboises Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspbian de l’installation, téléchargement de raspbian, comment tooinstall raspbian, raspbian raspberry, le programme d’installation pi installation raspbian, raspberry pi installation du système d’exploitation, raspberry pi sd carte install, raspberry pi vous connecter, se connecter connectivité de pi pi, raspberry tooraspberry"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configurer votre appareil
## <a name="what-you-will-do"></a>Procédure à suivre
Configurer Pi pour la première utilisation et installer le système d’exploitation de Raspbian hello. Raspbian est un système d’exploitation libre qui est optimisé pour hello matériel de framboises Pi. Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :

* Comment tooinstall Raspbian sur Pi.
* Comment toopower des Pi à l’aide d’un câble USB.
* Comment tooconnect Pi toohello réseau à l’aide d’un réseau sans fil ou un câble Ethernet.
* Comment tooadd un toohello LED breadboard et connectez-la tooPi.

## <a name="what-you-need"></a>Ce dont vous avez besoin
toocomplete cette opération, vous devez hello pièces suivantes à partir de votre framboises Pi 3 Starter Kit :

* Hello framboises Pi 3 tableau
* carte microSD de 16 Go de Hello
* Hello 5-volt 2-amp alimentation avec un câble USB micro de hello 6-pied
* breadboard de Hello
* Câbles de connexion
* Résistance de 560 Ohm
* LED de 10 mm diffuse
* Hello câble Ethernet

![Éléments de votre Starter Kit](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

Vous aurez également besoin des éléments suivants :

* Une connexion câblée ou sans fil pour tooconnect Pi à.
* Un USB-SD adaptateur ou mini-SD tooburn hello du système d’exploitation image de la carte sur une carte microSD de hello.
* Un ordinateur exécutant Windows, Mac ou Linux. l’ordinateur Hello est utilisé tooinstall Raspbian sur une carte microSD de hello.
* Un toodownload de connexion Internet hello outils nécessaires et logiciels.

## <a name="install-raspbian-on-hello-microsd-card"></a>Installer Raspbian sur une carte MicroSD de hello
Préparer la carte microSD de hello pour l’installation de l’image de Raspbian hello.

1. Téléchargez Raspbian.
   1. [Télécharger](https://www.raspberrypi.org/downloads/raspbian/) fichier .zip hello Raspbian Jessie par Pixel.
   2. Extraire le dossier de tooa hello Raspbian image sur votre ordinateur.
2. Installez Raspbian toohello microSD carte.
   1. [Télécharger](https://www.etcher.io) et installer l’utilitaire de graveur carte hello Etcher SD.
   2. Exécutez Etcher et sélectionnez l’image Raspbian hello que vous avez extrait à l’étape 1.
   3. Sélectionnez le lecteur de carte microSD hello.
      Notez que Etcher peut avoir déjà sélectionné lecteur hello.
   4. Cliquez sur **Flash** tooinstall Raspbian toohello microSD carte.
   5. Retirez hello microSD votre ordinateur lorsque l’installation est terminée.
      Carte microSD de hello tooremove safe est directement car Etcher éjecte automatiquement ou démonte carte microSD de hello à l’achèvement.
   6. Insérer carte microSD de hello dans votre Pi.

![Insérez la carte de hello SD](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Mise sous tension de Pi
Pi sous tension à l’aide de câble USB micro de hello et alimentation hello.

![Mise sous tension](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Il s’agit d’alimentation toouse important hello kit hello est au moins de toomake 2 a que votre framboises comporte suffisamment toowork power correctement.

## <a name="enable-ssh"></a>Activation de SSH
À compter de la version de novembre 2016 de hello, Raspbian de serveur SSH de hello désactivé par défaut. Vous devez tooenable il manuellement. Vous pouvez faire référence toohello [instructions officielles](https://www.raspberrypi.org/documentation/remote-access/ssh/) ou connecter un moniteur et accédez trop**Préférences -> Configuration de Pi framboises** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Connecter framboises Pi 3 toohello réseau
Vous pouvez vous connecter tooa Pi câblé réseau tooa réseau ou sans fil. Assurez-vous que Pi est connecté toohello même réseau que votre ordinateur. Par exemple, vous pouvez vous connecter toohello Pi à que même commutateur que votre ordinateur est connecté.

### <a name="connect-tooa-wired-network"></a>Se connecter tooa de réseau câblé
Utilisez tooconnect de câble Ethernet hello tooyour Pi réseau câblé. Hello deux voyants Pi sous tension si hello connexion est établie.

![Connexion à l’aide d’un câble Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Connexion réseau sans fil de tooa
Suivez hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) à partir du réseau sans fil tooyour du Pi tooconnect hello framboises Pi Foundation. Les instructions suivantes requièrent que vous toofirst connecter un moniteur et un tooPi de clavier.

## <a name="connect-hello-led-toopi"></a>Se connecter hello DEL tooPi
toocomplete de cette tâche, utilisez hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello fils de connecteur, hello DEL et hello résistance. Connectez-les toohello [à usage général d’entrée/sortie](https://www.raspberrypi.org/documentation/usage/gpio/) ports (GPIO) de Pi.

![Platine d’expérimentation, LED et résistance](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Vous connecter trop de tronçon de hello plus courte de hello DEL**GPIO GND (code confidentiel 6)**.
2. Se connecter tronçon de plus de temps hello Hello tronçon de tooone LED de résistance de hello.
3. Se connecter hello autres tronçon de résistance de hello trop**GPIO 4 (code confidentiel 7)**.

Notez que la polarité hello DEL est importante. Ce paramètre de polarité est communément appelé Faible actif.

![Brochage](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

Félicitations ! Vous avez réussi à configurer Pi.

## <a name="summary"></a>Résumé
Dans cet article, vous avez appris comment tooconfigure Pi en installant Raspbian, connexion au réseau tooa Pi et de la connexion à un tooPi LED. Notez que hello que voyant ne s’allume encore. la tâche suivante Hello est tooinstall hello outils et nécessaires logiciel en vue d’un exemple d’application en cours d’exécution sur Pi.

![Le matériel est prêt.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Étapes suivantes
[Obtenir les outils de hello](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

