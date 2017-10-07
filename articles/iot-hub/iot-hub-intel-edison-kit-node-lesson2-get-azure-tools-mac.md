---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 2 : Windows Azure tools (macOS) | Documents Microsoft"
description: "Sur Mac OS, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 8a2a8031-b1a6-4219-b17d-2825550c35e1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e33b3c9ee8f06f1c6175457f98a0600dd945cf1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obtenir les outils Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 et versions ultérieures][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Procédure à suivre
Installez hello Azure interface de ligne de commande (CLI d’Azure). Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].

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

![Sortie qui indique la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Résumé
Vous avez installé hello CLI d’Azure. La tâche suivante est toocreate votre identité Azure IoT hub et appareil à l’aide de hello CLI d’Azure.

## <a name="next-steps"></a>Étapes suivantes
[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
