---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 2 : Obtenir des outils (Windows) | Microsoft Docs"
description: "Installez les outils et les logiciels sur votre ordinateur hôte exécutant Windows, créez un hub IoT et inscrivez votre appareil dans l’IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, service cloud iot, logiciel internet des objets, azure cli, installer git sur windows, exécuter gulp, installer node js windows, installer npm sur windows, installer python sur windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0d8ba03df63d0b8657a9e275fc636e806c66b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="a0ec1-104">Obtenir les outils (Windows 7 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="a0ec1-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0ec1-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="a0ec1-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="a0ec1-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a0ec1-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="a0ec1-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a0ec1-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="a0ec1-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="a0ec1-108">What you will do</span></span>

- <span data-ttu-id="a0ec1-109">Installation de Git, Node.js, Gulp et Python.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="a0ec1-110">Installez l’interface de ligne de commande Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="a0ec1-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="a0ec1-111">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a0ec1-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0ec1-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="a0ec1-112">What you will learn</span></span>

<span data-ttu-id="a0ec1-113">Dans cette leçon, vous allez apprendre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a0ec1-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="a0ec1-114">Installation de [Git](https://git-scm.com/) et [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="a0ec1-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="a0ec1-115">Git est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="a0ec1-116">L’exemple d’application de cette leçon est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="a0ec1-117">Node.js est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="a0ec1-118">Utilisation de [NPM](https://www.npmjs.com/) pour installer des outils de développement Node.js.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="a0ec1-119">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="a0ec1-120">NPM est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="a0ec1-121">Installation de Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="a0ec1-122">Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a0ec1-123">Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="a0ec1-124">Comment installer Python.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-124">How to install Python.</span></span>
  - <span data-ttu-id="a0ec1-125">Python est un langage de programmation interprété et dynamique, à usage général et fréquemment utilisé.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="a0ec1-126">Installation de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="a0ec1-127">L’interface de ligne de commande Azure offre une expérience de ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="a0ec1-128">Vous travaillez directement à partir d’une ligne de commande pour approvisionner et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="a0ec1-129">Utilisation de l’interface de ligne de commande Azure pour créer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0ec1-130">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="a0ec1-130">What you need</span></span>

- <span data-ttu-id="a0ec1-131">Une connexion Internet pour télécharger les outils et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="a0ec1-132">Un ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="a0ec1-133">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="a0ec1-133">Install Git and Node.js</span></span>

<span data-ttu-id="a0ec1-134">Cliquez sur les liens ci-dessous pour télécharger et installer Git et Node.js LTS pour Windows.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="a0ec1-135">Téléchargement de Git pour Windows</span><span class="sxs-lookup"><span data-stu-id="a0ec1-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="a0ec1-136">Téléchargement de Node.js LTS pour Windows</span><span class="sxs-lookup"><span data-stu-id="a0ec1-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="a0ec1-137">Installer des outils de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="a0ec1-137">Install Node.js development tools</span></span>

<span data-ttu-id="a0ec1-138">Vous utilisez [gulp.js](http://gulpjs.com/) pour automatiser le déploiement et l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="a0ec1-139">Appuyez sur `Windows + R`, saisissez `cmd` et appuyez sur `Enter` pour ouvrir une fenêtre d’invite de commandes, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0ec1-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="a0ec1-140">Si vous rencontrez des problèmes lors de l’installation, consultez le [guide de dépannage](iot-hub-gateway-kit-c-troubleshooting.md) des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="a0ec1-141">Node, NPM et Gulp sont requis pour exécuter des scripts d’automatisation développés dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="a0ec1-142">Installer python</span><span class="sxs-lookup"><span data-stu-id="a0ec1-142">Install Python</span></span>

<span data-ttu-id="a0ec1-143">Vous pouvez choisir entre Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="a0ec1-144">Dans ce didacticiel, nous utilisons Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="a0ec1-145">Si vous avez déjà installé Python, passez à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="a0ec1-146">Obtenir Python pour Windows</span><span class="sxs-lookup"><span data-stu-id="a0ec1-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="a0ec1-147">Vous devez également ajouter le chemin d’accès des dossiers où Python.exe et pip.exe sont installés à la variable d’environnement `PATH` du système.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="a0ec1-148">Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="a0ec1-149">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a0ec1-149">Install the Azure CLI</span></span>

<span data-ttu-id="a0ec1-150">Pour installer l’interface de ligne de commande Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0ec1-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a0ec1-151">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="a0ec1-152">Installez l’interface de ligne de commande Azure en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a0ec1-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="a0ec1-153">L’installation peut prendre 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="a0ec1-154">Vérifiez l’installation en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a0ec1-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="a0ec1-155">Si l’installation a réussi, vous devez voir la sortie suivante.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-155">You should see the following output if the installation is successful.</span></span>

   ![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="a0ec1-157">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a0ec1-157">Install Visual Studio Code</span></span>

<span data-ttu-id="a0ec1-158">Visual Studio Code, plus loin dans ce didacticiel, vous permet de modifier les fichiers de configuration.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="a0ec1-159">[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="a0ec1-160">Résumé</span><span class="sxs-lookup"><span data-stu-id="a0ec1-160">Summary</span></span>

<span data-ttu-id="a0ec1-161">Vous avez installé tous les outils et logiciels nécessaires sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="a0ec1-162">La tâche suivante consiste à utiliser l’interface de ligne de commande Azure pour créer un IoT Hub et inscrire votre appareil dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a0ec1-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0ec1-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0ec1-163">Next steps</span></span>
[<span data-ttu-id="a0ec1-164">Créer un hub IoT et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="a0ec1-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
