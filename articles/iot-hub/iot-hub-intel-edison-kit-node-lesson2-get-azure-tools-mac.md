---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 2 : Outils Azure (macOS) | Microsoft Docs"
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
ms.openlocfilehash: 16705d54e90ee1482822986ca8c581a192e8702f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="5e094-104">Obtenir les outils Azure (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="5e094-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5e094-105">[Windows 7 et versions ultérieures][windows]</span><span class="sxs-lookup"><span data-stu-id="5e094-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="5e094-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="5e094-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="5e094-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="5e094-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5e094-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="5e094-108">What you will do</span></span>
<span data-ttu-id="5e094-109">Installez l’interface de ligne de commande Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="5e094-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="5e094-110">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5e094-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e094-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="5e094-111">What you will learn</span></span>
<span data-ttu-id="5e094-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5e094-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5e094-113">Comment installer Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5e094-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="5e094-114">Comment ajouter un sous-groupe IoT de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="5e094-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e094-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="5e094-115">What you need</span></span>
* <span data-ttu-id="5e094-116">Un Mac avec une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="5e094-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="5e094-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="5e094-117">An active Azure subscription.</span></span> <span data-ttu-id="5e094-118">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="5e094-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="5e094-119">Installer python</span><span class="sxs-lookup"><span data-stu-id="5e094-119">Install Python</span></span>
<span data-ttu-id="5e094-120">Bien que Mac OS soit fourni avec Python 2.7, il est recommandé d’installer Python via Homebrew.</span><span class="sxs-lookup"><span data-stu-id="5e094-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="5e094-121">Voir [Installation de Python sur Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="5e094-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="5e094-122">Installez Python et pip en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e094-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="5e094-123">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5e094-123">Install the Azure CLI</span></span>
<span data-ttu-id="5e094-124">L’interface de ligne de commande Azure offre une expérience de ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="5e094-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="5e094-125">Vous travaillez directement à partir de votre ligne de commande pour approvisionner et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="5e094-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="5e094-126">Pour installer la dernière version d’Azure CLI, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e094-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5e094-127">Exécutez les commandes suivantes dans une fenêtre de Terminal.</span><span class="sxs-lookup"><span data-stu-id="5e094-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="5e094-128">L’installation de l’interface de ligne de commande Azure peut prendre cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="5e094-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="5e094-129">Vérifiez l’installation en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e094-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="5e094-130">Si l’installation a réussi, vous devez voir la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="5e094-130">You should see the following output if the installation is successful.</span></span>

![Sortie indiquant la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="5e094-132">Résumé</span><span class="sxs-lookup"><span data-stu-id="5e094-132">Summary</span></span>
<span data-ttu-id="5e094-133">Vous avez installé l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="5e094-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="5e094-134">La tâche suivante consiste à créer votre Azure IoT Hub et votre identité d’appareil à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="5e094-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e094-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e094-135">Next steps</span></span>
<span data-ttu-id="5e094-136">[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="5e094-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
