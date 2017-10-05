---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 2 : Obtenir des outils (macOS) | Microsoft Docs"
description: "Installez les outils sur votre ordinateur Mac, créez un IoT Hub et inscrivez votre appareil dans l’IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, service cloud iot, logiciel internet des objets, azure cli, installer python mac, installer git sur mac, exécuter gulp, installer node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 94e538ef-9857-4023-9c3c-e92a0be7c395
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 07bc5f2cf6542273c334371b77520c674c5d2f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos"></a><span data-ttu-id="ea462-104">Obtenir les outils (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="ea462-104">Get the tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea462-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="ea462-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="ea462-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="ea462-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="ea462-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="ea462-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="ea462-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="ea462-108">What you will do</span></span>

- <span data-ttu-id="ea462-109">Installation de Git, Node.js, Gulp et Python.</span><span class="sxs-lookup"><span data-stu-id="ea462-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="ea462-110">Installez l’interface de ligne de commande Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="ea462-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="ea462-111">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ea462-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ea462-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="ea462-112">What you will learn</span></span>

<span data-ttu-id="ea462-113">Dans cette leçon, vous allez apprendre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ea462-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="ea462-114">Installation de [Git](https://git-scm.com/) et [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ea462-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="ea462-115">Git est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="ea462-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="ea462-116">L’exemple d’application de cette leçon est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="ea462-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="ea462-117">Node.js est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="ea462-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="ea462-118">Utilisation de [NPM](https://www.npmjs.com/) pour installer des outils de développement Node.js.</span><span class="sxs-lookup"><span data-stu-id="ea462-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="ea462-119">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="ea462-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="ea462-120">NPM est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="ea462-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="ea462-121">Installation de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ea462-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="ea462-122">Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="ea462-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="ea462-123">Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.</span><span class="sxs-lookup"><span data-stu-id="ea462-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="ea462-124">Comment installer Python.</span><span class="sxs-lookup"><span data-stu-id="ea462-124">How to install Python.</span></span>
  - <span data-ttu-id="ea462-125">Python est un langage de programmation interprété et dynamique, à usage général et fréquemment utilisé.</span><span class="sxs-lookup"><span data-stu-id="ea462-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="ea462-126">Installation de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="ea462-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="ea462-127">L’interface de ligne de commande Azure offre une expérience de ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ea462-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="ea462-128">Vous travaillez directement à partir d’une ligne de commande pour approvisionner et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="ea462-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="ea462-129">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ea462-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ea462-130">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="ea462-130">What you need</span></span>

- <span data-ttu-id="ea462-131">Une connexion Internet pour télécharger les outils et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="ea462-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="ea462-132">Un ordinateur Mac exécutant OS X Yosemite (10.10) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ea462-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="ea462-133">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="ea462-133">Install Git and Node.js</span></span>

<span data-ttu-id="ea462-134">Pour installer Git et Node.js, servez-vous de l’utilitaire de gestion de package Homebrew en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea462-134">To install Git and Node.js, use the Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="ea462-135">[Téléchargez](http://brew.sh/) et installez Homebrew.</span><span class="sxs-lookup"><span data-stu-id="ea462-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="ea462-136">Si vous avez déjà installé Homebrew, passez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="ea462-136">If you’ve already installed Homebrew, go to step 2.</span></span>
   1. <span data-ttu-id="ea462-137">Appuyez sur `Cmd + Space` puis entrez `Terminal` pour ouvrir une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="ea462-137">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="ea462-138">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea462-138">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="ea462-139">Installez de Git et Node.js en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea462-139">Install Git and Node.js by running the following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="ea462-140">Installer des outils de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="ea462-140">Install Node.js development tools</span></span>

<span data-ttu-id="ea462-141">Vous utilisez [gulp.js](http://gulpjs.com/) pour automatiser le déploiement et l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="ea462-141">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="ea462-142">Pour installer gulp, exécutez la commande suivante dans le terminal :</span><span class="sxs-lookup"><span data-stu-id="ea462-142">To install gulp, run the following command in the terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="ea462-143">Si vous rencontrez des problèmes lors de l’installation, consultez le [guide de dépannage](iot-hub-gateway-kit-c-troubleshooting.md) des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="ea462-143">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="ea462-144">Node, NPM et Gulp sont requis pour exécuter des scripts d’automatisation développés dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="ea462-144">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="ea462-145">Installer python</span><span class="sxs-lookup"><span data-stu-id="ea462-145">Install Python</span></span>

<span data-ttu-id="ea462-146">Bien que macOS X soit fourni avec Python 2.7, il est recommandé d’installer Python via Homebrew.</span><span class="sxs-lookup"><span data-stu-id="ea462-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="ea462-147">Consultez [Installation de Python sur macOS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="ea462-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="ea462-148">Installez Python et pip en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea462-148">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="ea462-149">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ea462-149">Install the Azure CLI</span></span>

<span data-ttu-id="ea462-150">Pour installer l’interface de ligne de commande Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea462-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="ea462-151">Exécutez les commandes suivantes dans le terminal :</span><span class="sxs-lookup"><span data-stu-id="ea462-151">Run the following commands in the terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="ea462-152">L’installation peut prendre 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="ea462-152">The installation might take 5 minutes.</span></span>

2. <span data-ttu-id="ea462-153">Vérifiez l’installation en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ea462-153">Verify the installation by running the following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="ea462-154">Si l’installation a réussi, vous devez voir la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="ea462-154">You should see the following output if the installation is successful.</span></span>

   ![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="ea462-156">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ea462-156">Install Visual Studio Code</span></span>

<span data-ttu-id="ea462-157">Visual Studio Code, plus loin dans ce didacticiel, vous permet de modifier les fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="ea462-157">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="ea462-158">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ea462-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="ea462-159">Résumé</span><span class="sxs-lookup"><span data-stu-id="ea462-159">Summary</span></span>

<span data-ttu-id="ea462-160">Vous avez installé tous les outils et logiciels nécessaires sur votre ordinateur Mac.</span><span class="sxs-lookup"><span data-stu-id="ea462-160">You’ve installed all the required tools and software on your Mac computer.</span></span> <span data-ttu-id="ea462-161">La tâche suivante consiste à utiliser l’interface de ligne de commande Azure pour créer un IoT Hub et inscrire votre appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ea462-161">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea462-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea462-162">Next steps</span></span>
[<span data-ttu-id="ea462-163">Créer un IoT Hub et inscrire l’appareil</span><span class="sxs-lookup"><span data-stu-id="ea462-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
