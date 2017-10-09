---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 2 : Windows Azure tools (Windows) | Documents Microsoft"
description: "Installer Python et hello Azure interface de ligne de commande (CLI d’Azure) sur Windows 7 et versions ultérieures."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: iot cloud service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Obtenir les outils Azure (Windows 7 et versions ultérieures)
> [!div class="op_single_selector"]
> * [Windows 7 et versions ultérieures](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Procédure à suivre
Installer Python et hello Azure interface de ligne de commande (CLI d’Azure). Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Contenu
Cet article portera sur les éléments suivants :
* Comment tooinstall Python.
* Comment tooinstall hello CLI d’Azure.

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Un ordinateur Windows connecté à Internet.
* Un abonnement Azure actif. Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.

## <a name="install-python"></a>Installation de Python
[Installez Python](https://www.python.org/downloads/) sur votre ordinateur Windows. Vous pouvez installer Python 2.7, 3.4 ou 3.5. Ce didacticiel est basé sur Python 2.7. Si vous avez déjà installé les Python, atteindre la section suivante de toohello et installer hello CLI d’Azure.

Vous devez également le chemin d’accès de hello tooadd de dossiers hello où python.exe et pip.exe sont installés toohello système `PATH` variable d’environnement. Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Installer hello CLI d’Azure
Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure. Travailler directement depuis votre tooprovision de ligne de commande et de gérer les ressources.

tooinstall hello CLI d’Azure, procédez comme suit :

1. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.
2. Exécutez hello suivant de commandes :

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Hello Vérifiez-la en exécutant hello de commande suivante :

   ```bash
   az iot -h
   ```

Vous consultez suivant de hello de sortie si l’installation de hello a réussi.

![Sortie qui indique la réussite](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Résumé
Vous avez installé hello CLI d’Azure. Votre prochaine tâche toocreate votre identité de Azure IoT hub et appareil à l’aide de hello CLI d’Azure.

## <a name="next-steps"></a>Étapes suivantes
[Créer votre IoT Hub et inscrire Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

