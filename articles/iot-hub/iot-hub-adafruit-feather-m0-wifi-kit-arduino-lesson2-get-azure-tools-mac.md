---
title: "Se connecter Arduino tooAzure IoT - leçon 2 : Windows Azure tools (macOS) | Documents Microsoft"
description: "Sur Mac OS, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0ec4131e54af5475cd0b4240480c3fda497e14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obtenir les outils Azure (macOS 10.10)

> [!div class="op_single_selector"]
> * [Windows 7 ou version ultérieure][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Procédure à suivre

Installez hello Azure interface de ligne de commande (CLI d’Azure). Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) pour votre carte mère Adafruit estompe M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment tooinstall CLI d’Azure.
* Comment tooadd un sous-groupe IoT Hello CLI d’Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Un Mac avec une connexion Internet.
* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.

## <a name="install-python"></a>Installation de Python
Bien que macOS fourni avec Python 2.7 prédéfinies hello, nous vous recommandons d’installer Python via Homebrew. Voir [Installation de Python sur Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Installer Python et pip en exécutant hello de commande suivante :

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Installer hello CLI d’Azure
Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure. Travailler directement depuis votre tooprovision de ligne de commande et de gérer les ressources.

tooinstall hello dernière CLI d’Azure, procédez comme suit :

1. Exécutez hello suivant les commandes dans une fenêtre de terminal. Il peut prendre cinq minutes tooinstall hello CLI d’Azure.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Hello Vérifiez-la en exécutant hello de commande suivante :

   ```bash
   az iot -h
   ```

Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.

![Sortie qui indique la réussite][output]

## <a name="summary"></a>Résumé
Vous avez installé hello CLI d’Azure. La tâche suivante est toocreate votre identité Azure IoT hub et appareil à l’aide de hello CLI d’Azure.

## <a name="next-steps"></a>Étapes suivantes
[Créer votre IoT Hub et inscrire votre carte Arduino][create-your-iot-hub-and-register-your-arduino-board]


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md