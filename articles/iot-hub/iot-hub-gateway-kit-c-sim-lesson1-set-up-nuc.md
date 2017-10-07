---
title: "Appareil simulé et passerelle Azure IoT - Leçon 1 : Configurer NUC | Microsoft Docs"
description: Configurer Intel NUC toowork comme passerelle entre un capteur et les informations de capteur toocollect Azure IoT Hub IoT et envoyez-le tooIoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: passerelle iot, intel nuc, ordinateur nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurer l’Intel NUC comme passerelle IoT

## <a name="what-you-will-do"></a>Procédure à suivre

- Configurez l’Intel NUC comme passerelle IoT.
- Installez le package de Azure IoT Edge de hello sur NUC d’Intel.
- Exécuter un exemple d’application « Bonjour_monde » sur la fonctionnalité de passerelle Intel NUC tooverify hello.
Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu

Dans cette leçon, vous allez apprendre :

- Comment tooconnect Intel NUC avec les périphériques.
- Comment tooinstall et mise à jour des packages hello requis sur l’utilisation de Intel NUC hello actives Gestionnaire de Package.
- Comment toorun hello » Bonjour_monde » exemple de fonctionnalité de passerelle d’application tooverify hello.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Un Intel NUC Kit DE3815TYKE avec hello Intel IoT passerelle logiciel Suite (district de vent Linux * 7.0.0.13) préinstallé.
- Un câble Ethernet.
- Un clavier.
- Un câble VGA ou HDMI.
- Un écran équipé d’un port VGA ou HDMI.

![Un kit de passerelle](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Se connecter Intel NUC avec les périphériques de hello

image Hello ci-dessous est un exemple de NUC Intel qui est connecté avec des périphériques différents :

1. Tooa connecté clavier.
2. Connecté analyse toohello par un câble VGA ou un câble HDMI.
3. Tooa connecté réseau câblé via un câble Ethernet.
4. Alimentation toohello connecté avec un câble d’alimentation.

![Intel NUC connecté tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Connecter le système d’Intel NUC toohello à partir de l’ordinateur hôte via Secure Shell (SSH)

Ici, vous devez clavier et écran tooget hello adresse IP de votre périphérique NUC. Si vous connaissez déjà hello IP adresse, vous pouvez ignorer toostep 3 de cette section.

1. Intel NUC sous tension en appuyant sur le bouton d’alimentation hello et de journal dans le système de hello.

   nom d’utilisateur par défaut Hello et un mot de passe sont tous deux `root`.

2. Obtenir l’adresse IP hello NUC en exécutant hello `ifconfig` commande. Cette étape est effectuée sur l’appareil NUC hello.

   Voici un exemple de sortie de la commande hello.

   ![sortie ifconfig indiquant l’IP NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Dans cet exemple, hello valeur suit `inet addr:` est l’adresse IP hello dont vous avez besoin lorsque vous planifiez tooconnect à distance à partir d’un tooIntel d’ordinateur hôte NUC.

3. Utilisez une des hello suivant clients SSH à partir de votre ordinateur hôte ordinateur tooconnect tooIntel NUC.

   - [PuTTY](http://www.putty.org/) pour Windows.
   - Hello dans build client SSH sur Ubuntu ou macOS.

   Il est plus efficace et plus productif toooperate sur Intel NUC à partir d’un ordinateur hôte. Vous avez besoin d’adresse IP de hello hello, nom d’utilisateur et mot de passe tooconnect hello NUC via un client SSH. Voici le client SSH de hello exemple utilisation sur macOS.
   ![Client SSH exécuté sur macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Installer le package de Azure IoT bord hello

Bonjour Azure IoT bord contient hello des binaires précompilés Hello SDK et ses dépendances. Ces fichiers binaires sont Azure IoT Edge, hello Azure IoT SDK et les outils correspondants hello. Hello contient également un exemple d’application « Bonjour_monde » qui est une fonctionnalité de passerelle hello toovalidate utilisé. IoT bord fait partie de noyaux de hello de passerelle de hello. tooinstall hello du package, procédez comme suit :

1. Ajoutez référentiel de cloud IoT hello en exécutant hello suivant les commandes dans une fenêtre de terminal :

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Hello `rpm` commande importations hello clé du TPM. Hello `smart channel` commande ajoute tr/min hello toohello actives Gestionnaire de Package de canal. Avant d’exécuter hello `smart update` commande, vous voyez une sortie similaire à ci-dessous.

   ![Sortie des commandes rpm et canal intelligent](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Installer hello en exécutant hello de commande suivante :

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`est le nom hello du package de hello. Hello `smart install` commande est utilisée tooinstall hello du package.

   Après installation du package hello, Intel NUC est toowork attendu en tant que passerelle.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Exécuter hello Azure IoT bord « Bonjour_monde » exemple d’application

Accédez trop`azureiotgatewaysdk/samples` et exécuter l’exemple d’application hello exemple « Bonjour_monde ». Cet exemple d’application crée une passerelle de hello `hello_world.json` de fichier et utilise les composants fondamentaux de hello de hello Azure IoT bord architecture toolog un fichier de tooa hello world message toutes les 5 secondes.

Vous pouvez exécuter hello exemple « Bonjour_monde » exemple d’application en exécutant hello de commande suivante :

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

exemple d’application Hello génère suivant hello de sortie si la fonctionnalité de passerelle hello fonctionne correctement :

![sortie d’application](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Résumé

Félicitations ! Vous avez terminé la configuration d’Intel NUC comme passerelle. Maintenant, vous êtes prêt toomove sur toohello prochaine leçon tooset votre ordinateur hôte, créez un Azure IoT hub et inscrire votre unité logique de Azure IoT hub.

## <a name="next-steps"></a>Étapes suivantes
[Préparer votre ordinateur hôte et Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
