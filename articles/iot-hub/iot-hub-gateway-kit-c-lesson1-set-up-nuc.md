---
title: "Appareil SensorTag et passerelle Azure Io - Leçon 1 : Configurer l’Intel NUC | Microsoft Docs"
description: Configurer Intel NUC toowork comme passerelle entre un capteur et les informations de capteur toocollect Azure IoT Hub IoT et envoyez-le tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: passerelle iot, intel nuc, ordinateur nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurer l’Intel NUC comme passerelle IoT
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>Procédure à suivre

- Configurez l’Intel NUC comme passerelle IoT.
- Installez le package de Azure IoT Edge de hello sur hello NUC d’Intel.
- Exécuter un exemple d’application « Bonjour_monde » sur hello fonctionnalité de passerelle Intel NUC tooverify hello.

  > Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Dans cette leçon, vous allez apprendre :

- Comment tooconnect Intel NUC avec les périphériques.
- Comment tooinstall et mise à jour des packages hello requis sur l’utilisation de Intel NUC hello actives Gestionnaire de Package.
- Comment toorun hello » Bonjour_monde » exemple de fonctionnalité de passerelle d’application tooverify hello.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Un Intel NUC Kit DE3815TYKE avec hello Intel IoT passerelle logiciel Suite (district de vent Linux * 7.0.0.13) préinstallé. [Cliquez ici toopurchase Grove IoT Commercial passerelle Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Un câble Ethernet.
- Un clavier.
- Un câble VGA ou HDMI.
- Un écran équipé d’un port VGA ou HDMI.
- Facultatif : [SensorTag Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Un kit de passerelle](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Se connecter Intel NUC avec les périphériques de hello

image Hello ci-dessous est un exemple de NUC Intel qui est connecté avec des périphériques différents :

1. Tooa connecté clavier.
2. Connecté tooa moniteur avec un câble VGA ou un câble HDMI.
3. Tooa connecté réseau via un câble Ethernet câblé.
4. Alimentation tooa connecté avec un câble d’alimentation.

![Intel NUC connecté tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Connecter le système d’Intel NUC toohello à partir de l’ordinateur hôte via Secure Shell (SSH)

Vous devez un clavier et une adresse IP de moniteur tooget hello de votre appareil NUC d’Intel. Si vous connaissez déjà hello IP adresse, vous pouvez ignorer le transfert toostep 3 de cette section.

1. Activez hello Intel NUC en appuyant sur le bouton d’alimentation hello et puis connectez-vous.

   nom d’utilisateur par défaut Hello et un mot de passe sont tous deux `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Adresse IP hello hello Intel NUC d’obtenir en exécutant hello `ifconfig` commande sur l’appareil de Intel NUC hello.

   Voici un exemple de sortie de la commande hello.

   ![Sortie de la commande ifconfig indiquant l’adresse IP de l’Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Dans cet exemple, hello valeur suit `inet addr:` est l’adresse IP hello dont vous avez besoin lorsque vous connecter toohello Intel NUC à partir d’un ordinateur hôte.

3. Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooIntel NUC.

    - [PuTTY](http://www.putty.org/) pour Windows.
    - client Hello intégré SSH sur Ubuntu ou macOS.

   Il est plus efficace et plus productif toooperate un NUC Intel à partir d’un ordinateur hôte. Vous aurez besoin hello adresse IP de NUC Intel tooit de tooconnect des nom et mot de passe utilisateur via un client SSH. Voici un exemple qui fait appel à un client SSH sur Mac OS.
   ![Client SSH exécuté sur macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Installer le package de Azure IoT bord hello

Azure IoT bord Hello contient hello des binaires précompilés de IoT Edge et ses dépendances. Ces fichiers binaires sont Azure IoT Edge, hello Azure IoT SDK et les outils correspondants hello. Hello package contient également une « Bonjour_monde » exemple d’application est une fonctionnalité de passerelle hello toovalidate utilisé. IoT bord fait partie de noyaux de hello de passerelle de hello. 

Suivez ces packages de hello tooinstall étapes.

1. Ajoutez hello référentiel de IoT Cloud en exécutant hello suivant les commandes dans une fenêtre de terminal :

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Entrez 'y', lorsque vous invite too'Include ce canal ? »
   
   Si vous recevez un `import read failed(-1)` erreur, hello utilisation suivant le problème de hello tooresolve de commandes :
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Hello `rpm` commande importations hello clé du TPM. Hello `smart channel` commande ajoute tr/min hello toohello actives Gestionnaire de Package de canal. Avant d’exécuter hello `smart update` de commande, vous pouvez voir une sortie comme ci-dessous.

   ![Sortie des commandes rpm et canal intelligent](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Exécuter la commande de mise à jour actives hello :

   ```bash
   smart update
   ```

3. Installer le package de passerelle de Azure IoT de hello en exécutant hello de commande suivante :

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`est le nom hello du package de hello. Hello `smart install` commande est utilisée tooinstall hello du package.

    > Suivante d’exécution hello commande si vous voyez cette erreur : « clé publique non disponible »

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Redémarrez hello Intel NUC si vous voyez cette erreur : « aucun package ne fournit util-linux-dev »

   Après installation du package hello, Intel NUC est toofunction prêt en tant que passerelle.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Exécuter hello Azure IoT bord « Bonjour_monde » exemple d’application

Hello suivant l’exemple d’application crée une passerelle d’un `hello_world.json` de fichier et utilise les composants fondamentaux de hello de Azure IoT bord architecture toolog un fichier de tooa message hello world (log.txt) toutes les 5 secondes.

Vous pouvez exécuter l’exemple hello Hello World en exécutant hello suivant les commandes :

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Permettent l’application hello Hello World s’exécuter pendant quelques minutes, puis appuyez sur toostop de clé entrée hello il.
![Sortie de l’application](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Vous pouvez ignorer les erreurs « invalid argument handle(NULL) » (Descripteur d’argument non valide (NULL)) qui s’affichent après que vous avez appuyé sur Entrée.

Vous pouvez vérifier cette passerelle hello a été effectuée correctement en ouvrant le fichier log.txt hello qui est désormais dans votre dossier Bonjour_monde ![log.txt vue d’annuaire](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Ouvrez log.txt à l’aide de hello de commande suivante :

```bash
vim log.txt
```

Vous verrez ensuite contenu hello de log.txt, qui sera une sortie au format JSON de messages de journalisation hello qui ont été écrits de toutes les 5 secondes par le module de Hello World hello passerelle.
![Vue du répertoire de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Résumé

Félicitations ! Vous avez terminé la configuration d’Intel NUC comme passerelle. Maintenant, vous êtes prêt toomove sur toohello prochaine leçon tooset votre ordinateur hôte, créez un Azure IoT Hub et inscrire votre appareil logique Azure IoT Hub.

## <a name="next-steps"></a>Étapes suivantes
[Utilisez un tooconnect de passerelle un tooAzure appareil IoT Hub IoT](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

