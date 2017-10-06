---
title: "Connect Intel Edison (C) tooAzure IoT - leçon 2 : Windows Azure tools (Ubuntu) | Documents Microsoft"
description: "Sur Ubuntu, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 2463cb8e-5758-4d72-af98-62520d41f2f7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a7691c13d43aa6dfff24adf2b470728d5266713e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Obtenir les outils Azure (Ubuntu 16.04)
> [!div class="op_single_selector"]
> * [Windows 7 et versions ultérieures][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Procédure à suivre
Installez hello Azure interface de ligne de commande (CLI d’Azure). Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment tooinstall hello CLI d’Azure.
* Comment tooadd un sous-groupe IoT Hello CLI d’Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Un ordinateur Ubuntu connecté à Internet.
* Un abonnement Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte d’évaluation gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.

## <a name="install-hello-azure-cli"></a>Installer hello CLI d’Azure
Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure, ce qui vous toowork directement à partir de votre tooprovision de ligne de commande et gérer les ressources.

tooinstall hello dernière CLI d’Azure, procédez comme suit :

1. Exécutez hello suivant les commandes dans une fenêtre de terminal. Il peut prendre cinq minutes tooinstall hello CLI d’Azure.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Hello Vérifiez-la en exécutant hello de commande suivante :

   ```bash
   az iot -h
   ```

Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.

![Sortie qui indique la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a>Résumé
Vous avez installé hello CLI d’Azure. La tâche suivante est toocreate votre Azure IoT hub et l’identité de l’appareil à l’aide hello CLI d’Azure.

## <a name="next-steps"></a>Étapes suivantes
[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
