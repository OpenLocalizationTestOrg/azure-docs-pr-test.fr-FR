---
title: "Connecter Raspberry Pi (Node) à Azure IoT - Leçon 2 : Obtenir des outils (Ubuntu) | Microsoft Docs"
description: "Sur Ubuntu, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot cloud service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2f98923a-5274-4220-87d4-77ac8beb4d0f
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3933ccea992c62da1dd402f651d5b5b4ad43713d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="17380-104">Obtenir les outils Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="17380-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="17380-105">Windows 7 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="17380-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="17380-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="17380-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="17380-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="17380-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="17380-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="17380-108">What you will do</span></span>
<span data-ttu-id="17380-109">Installez l’interface de ligne de commande Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="17380-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="17380-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="17380-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="17380-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="17380-111">What you will learn</span></span>
<span data-ttu-id="17380-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="17380-112">In this article, you will learn:</span></span>
* <span data-ttu-id="17380-113">Installation de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="17380-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="17380-114">Ajout d’un sous-groupe IoT de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="17380-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="17380-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="17380-115">What you need</span></span>
* <span data-ttu-id="17380-116">Un ordinateur Ubuntu connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="17380-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="17380-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="17380-117">An active Azure subscription.</span></span> <span data-ttu-id="17380-118">Si vous ne possédez pas de compte, vous pouvez créer un [compte d’évaluation gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="17380-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="17380-119">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="17380-119">Install the Azure CLI</span></span>
<span data-ttu-id="17380-120">L’interface de ligne de commande Azure fournit une expérience de ligne de commande multiplateforme pour Azure, permettant de travailler directement à partir de la ligne de commande pour configurer et gérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="17380-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command-line to provision and manage resources.</span></span>

<span data-ttu-id="17380-121">Pour installer la dernière version d’Azure CLI, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="17380-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="17380-122">Exécutez les commandes suivantes dans une fenêtre de Terminal.</span><span class="sxs-lookup"><span data-stu-id="17380-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="17380-123">L’installation de l’interface de ligne de commande Azure peut prendre cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="17380-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="17380-124">Vérifiez l’installation en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="17380-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="17380-125">Si l’installation a réussi, vous devez voir la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="17380-125">You should see the following output if the installation is successful.</span></span>

![Sortie indiquant la réussite](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="17380-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="17380-127">Summary</span></span>
<span data-ttu-id="17380-128">Vous avez installé l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="17380-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="17380-129">La tâche suivante consiste à créer votre Azure IoT Hub et votre identité d’appareil à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="17380-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17380-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17380-130">Next steps</span></span>
[<span data-ttu-id="17380-131">Créer votre IoT Hub et inscrire Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="17380-131">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

