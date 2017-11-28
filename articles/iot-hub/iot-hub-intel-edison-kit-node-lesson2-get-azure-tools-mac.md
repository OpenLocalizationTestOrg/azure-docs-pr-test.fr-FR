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
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="bf77b-104">Obtenir les outils Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="bf77b-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="bf77b-105">[Windows 7 et versions ultérieures][windows]</span><span class="sxs-lookup"><span data-stu-id="bf77b-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="bf77b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="bf77b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="bf77b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="bf77b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="bf77b-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="bf77b-108">What you will do</span></span>
<span data-ttu-id="bf77b-109">Installez hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="bf77b-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="bf77b-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="bf77b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bf77b-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="bf77b-111">What you will learn</span></span>
<span data-ttu-id="bf77b-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf77b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="bf77b-113">Comment tooinstall CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bf77b-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="bf77b-114">Comment tooadd un sous-groupe IoT Hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bf77b-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bf77b-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="bf77b-115">What you need</span></span>
* <span data-ttu-id="bf77b-116">Un Mac avec une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="bf77b-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="bf77b-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="bf77b-117">An active Azure subscription.</span></span> <span data-ttu-id="bf77b-118">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bf77b-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="bf77b-119">Installation de Python</span><span class="sxs-lookup"><span data-stu-id="bf77b-119">Install Python</span></span>
<span data-ttu-id="bf77b-120">Bien que macOS fourni avec Python 2.7 prédéfinies hello, nous vous recommandons d’installer Python via Homebrew.</span><span class="sxs-lookup"><span data-stu-id="bf77b-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="bf77b-121">Voir [Installation de Python sur Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="bf77b-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="bf77b-122">Installer Python et pip en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bf77b-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="bf77b-123">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="bf77b-123">Install hello Azure CLI</span></span>
<span data-ttu-id="bf77b-124">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="bf77b-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="bf77b-125">Travailler directement depuis votre tooprovision de ligne de commande et de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="bf77b-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="bf77b-126">tooinstall hello dernière CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf77b-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="bf77b-127">Exécutez hello suivant les commandes dans une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="bf77b-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="bf77b-128">Il peut prendre cinq minutes tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bf77b-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="bf77b-129">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bf77b-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="bf77b-130">Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="bf77b-130">You should see hello following output if hello installation is successful.</span></span>

![Sortie qui indique la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="bf77b-132">Résumé</span><span class="sxs-lookup"><span data-stu-id="bf77b-132">Summary</span></span>
<span data-ttu-id="bf77b-133">Vous avez installé hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bf77b-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="bf77b-134">La tâche suivante est toocreate votre identité Azure IoT hub et appareil à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bf77b-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf77b-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf77b-135">Next steps</span></span>
<span data-ttu-id="bf77b-136">[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="bf77b-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
