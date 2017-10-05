---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 2 : Obtenir des outils (Ubuntu) | Microsoft Docs"
description: "Installez les outils et les logiciels sur votre ordinateur hôte exécutant Ubuntu, créez un IoT Hub et inscrivez votre appareil dans l’IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, service cloud iot, logiciel internet des objets, azure cli, installer git sur ubuntu, exécuter gulp, installer node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0bac1412-385b-4255-a33f-9d44c35feb3e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 234b60e1f8eaff52ce07f54d4d12de2421cc1a52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="7a34e-104">Obtenir les outils (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="7a34e-104">Get the tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a34e-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="7a34e-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="7a34e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7a34e-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="7a34e-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="7a34e-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="7a34e-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="7a34e-108">What you will do</span></span>

- <span data-ttu-id="7a34e-109">Installation de Git, Node.js, Gulp et Python.</span><span class="sxs-lookup"><span data-stu-id="7a34e-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="7a34e-110">Installez l’interface de ligne de commande Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="7a34e-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="7a34e-111">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7a34e-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="7a34e-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="7a34e-112">What you will learn</span></span>

<span data-ttu-id="7a34e-113">Dans cette leçon, vous allez apprendre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7a34e-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="7a34e-114">Installation de Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="7a34e-114">How to install Git and Node.js.</span></span>
  - <span data-ttu-id="7a34e-115">Git est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="7a34e-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="7a34e-116">L’exemple d’application de cette leçon est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="7a34e-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="7a34e-117">Node.js est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="7a34e-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="7a34e-118">Comment utiliser NPM pour installer des outils de développement Node.js.</span><span class="sxs-lookup"><span data-stu-id="7a34e-118">How to use NPM to install Node.js development tools.</span></span>
  - <span data-ttu-id="7a34e-119">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="7a34e-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="7a34e-120">NPM est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="7a34e-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="7a34e-121">Installation de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7a34e-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="7a34e-122">Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="7a34e-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="7a34e-123">Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.</span><span class="sxs-lookup"><span data-stu-id="7a34e-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="7a34e-124">Installation de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7a34e-124">How to install the Azure CLI</span></span>
  - <span data-ttu-id="7a34e-125">L’interface de ligne de commande Azure offre une expérience de ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="7a34e-125">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="7a34e-126">Vous travaillez directement à partir d’une ligne de commande pour approvisionner et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="7a34e-126">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="7a34e-127">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7a34e-127">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7a34e-128">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="7a34e-128">What you need</span></span>

- <span data-ttu-id="7a34e-129">Une connexion Internet pour télécharger les outils et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="7a34e-129">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="7a34e-130">Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7a34e-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="7a34e-131">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="7a34e-131">Install Git and Node.js</span></span>

<span data-ttu-id="7a34e-132">Pour installer Git et Node.js, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a34e-132">To install Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="7a34e-133">Appuyez sur `Ctrl + Alt + T` pour ouvrir un terminal.</span><span class="sxs-lookup"><span data-stu-id="7a34e-133">Press `Ctrl + Alt + T` to open a terminal.</span></span>
2. <span data-ttu-id="7a34e-134">Exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7a34e-134">Run the following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="7a34e-135">Installer des outils de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="7a34e-135">Install Node.js development tools</span></span>

<span data-ttu-id="7a34e-136">Vous utilisez [gulp.js](http://gulpjs.com/) pour automatiser le déploiement et l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="7a34e-136">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="7a34e-137">Pour installer gulp, exécutez la commande suivante dans le terminal :</span><span class="sxs-lookup"><span data-stu-id="7a34e-137">To install gulp, run the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="7a34e-138">Si vous rencontrez des problèmes lors de l’installation, consultez le [guide de dépannage](iot-hub-gateway-kit-c-troubleshooting.md) des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="7a34e-138">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="7a34e-139">Node, NPM et Gulp sont requis pour exécuter des scripts d’automatisation développés dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="7a34e-139">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="7a34e-140">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7a34e-140">Install the Azure CLI</span></span>

<span data-ttu-id="7a34e-141">Pour installer l’interface de ligne de commande Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a34e-141">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="7a34e-142">Exécutez les commandes suivantes dans le terminal :</span><span class="sxs-lookup"><span data-stu-id="7a34e-142">Run the following commands in the terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="7a34e-143">L’installation peut prendre 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="7a34e-143">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="7a34e-144">Vérifiez l’installation en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7a34e-144">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="7a34e-145">Si l’installation a réussi, vous devez voir la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="7a34e-145">You should see the following output if the installation is successful.</span></span>
<span data-ttu-id="7a34e-146">![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="7a34e-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="7a34e-147">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7a34e-147">Install Visual Studio Code</span></span>

<span data-ttu-id="7a34e-148">Visual Studio Code, plus loin dans ce didacticiel, vous permet de modifier les fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="7a34e-148">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="7a34e-149">[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7a34e-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="7a34e-150">Résumé</span><span class="sxs-lookup"><span data-stu-id="7a34e-150">Summary</span></span>

<span data-ttu-id="7a34e-151">Vous avez installé tous les outils et logiciels nécessaires sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="7a34e-151">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="7a34e-152">La tâche suivante consiste à utiliser l’interface de ligne de commande Azure pour créer un IoT Hub et inscrire votre appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7a34e-152">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a34e-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a34e-153">Next steps</span></span>
[<span data-ttu-id="7a34e-154">Créer un hub IoT et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="7a34e-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
