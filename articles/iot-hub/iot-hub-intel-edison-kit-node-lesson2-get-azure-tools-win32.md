---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 2 : Outils Azure (Windows) | Microsoft Docs"
description: "Sur Windows 7 et versions ultérieures, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7257fe98fa1075456de620ca46b4e10c34e06574
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="06d18-104">Obtenir les outils Azure (Windows 7 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="06d18-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="06d18-105">[Windows 7 et versions ultérieures][windows]</span><span class="sxs-lookup"><span data-stu-id="06d18-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="06d18-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="06d18-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="06d18-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="06d18-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="06d18-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="06d18-108">What you will do</span></span>
<span data-ttu-id="06d18-109">Installez Python et l’interface de ligne de commande Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="06d18-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="06d18-110">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="06d18-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="06d18-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="06d18-111">What you will learn</span></span>
<span data-ttu-id="06d18-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="06d18-112">In this article, you will learn:</span></span>
* <span data-ttu-id="06d18-113">Comment installer Python.</span><span class="sxs-lookup"><span data-stu-id="06d18-113">How to install Python.</span></span>
* <span data-ttu-id="06d18-114">Installation de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="06d18-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="06d18-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="06d18-115">What you need</span></span>
* <span data-ttu-id="06d18-116">Un ordinateur Windows connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="06d18-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="06d18-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="06d18-117">An active Azure subscription.</span></span> <span data-ttu-id="06d18-118">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="06d18-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="06d18-119">Installation de Python</span><span class="sxs-lookup"><span data-stu-id="06d18-119">Install Python</span></span>
<span data-ttu-id="06d18-120">[Installez Python](https://www.python.org/downloads/) sur votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="06d18-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="06d18-121">Vous pouvez installer Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="06d18-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="06d18-122">Ce didacticiel est basé sur Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="06d18-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="06d18-123">Si vous avez déjà installé Python, accédez à la section suivante et installez l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="06d18-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="06d18-124">Vous devez également ajouter le chemin d’accès des dossiers où python.exe et pip.exe sont installés à la variable d’environnement `PATH` du système.</span><span class="sxs-lookup"><span data-stu-id="06d18-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="06d18-125">Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="06d18-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="06d18-126">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="06d18-126">Install the Azure CLI</span></span>
<span data-ttu-id="06d18-127">L’interface de ligne de commande Azure offre une expérience de ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="06d18-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="06d18-128">Vous travaillez directement à partir de votre ligne de commande pour configurer et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="06d18-128">You work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="06d18-129">Pour installer l’interface de ligne de commande Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="06d18-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="06d18-130">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="06d18-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="06d18-131">Exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="06d18-131">Run the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="06d18-132">Vérifiez l’installation en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="06d18-132">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="06d18-133">Si l’installation a réussi, vous voyez la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="06d18-133">You see the following output if the installation is successful.</span></span>

![Sortie qui indique la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="06d18-135">Résumé</span><span class="sxs-lookup"><span data-stu-id="06d18-135">Summary</span></span>
<span data-ttu-id="06d18-136">Vous avez installé l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="06d18-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="06d18-137">La tâche suivante consiste à créer votre Azure IoT Hub et votre identité d’appareil à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="06d18-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06d18-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06d18-138">Next steps</span></span>
<span data-ttu-id="06d18-139">[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="06d18-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md