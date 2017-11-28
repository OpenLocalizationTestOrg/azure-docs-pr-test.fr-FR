---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 2 : Obtenir des outils (macOS) | Microsoft Docs"
description: "Installer les outils sur votre ordinateur Mac, créez un IoT hub et inscrire votre appareil dans le hub IoT de hello."
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
ms.openlocfilehash: 44bce452690e18e6c803df564fdafcdda7f41c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="34b55-104">Obtenir les outils de hello (MacOS)</span><span class="sxs-lookup"><span data-stu-id="34b55-104">Get hello tools (MacOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="34b55-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="34b55-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="34b55-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="34b55-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="34b55-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="34b55-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="34b55-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="34b55-108">What you will do</span></span>

- <span data-ttu-id="34b55-109">Installation de Git, Node.js, Gulp et Python.</span><span class="sxs-lookup"><span data-stu-id="34b55-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="34b55-110">Installez hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="34b55-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="34b55-111">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="34b55-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="34b55-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="34b55-112">What you will learn</span></span>

<span data-ttu-id="34b55-113">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="34b55-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="34b55-114">Comment tooinstall [Git](https://git-scm.com/) et [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="34b55-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="34b55-115">Git est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="34b55-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="34b55-116">exemple d’application Hello pour cette leçon est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="34b55-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="34b55-117">Node.js est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="34b55-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="34b55-118">Comment toouse [NPM](https://www.npmjs.com/) tooinstall des outils de développement Node.js.</span><span class="sxs-lookup"><span data-stu-id="34b55-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="34b55-119">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="34b55-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="34b55-120">NPM est un des gestionnaires de package hello pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="34b55-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="34b55-121">Comment tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="34b55-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="34b55-122">Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="34b55-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="34b55-123">Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.</span><span class="sxs-lookup"><span data-stu-id="34b55-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="34b55-124">Comment tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="34b55-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="34b55-125">Python est un langage de programmation interprété et dynamique, à usage général et fréquemment utilisé.</span><span class="sxs-lookup"><span data-stu-id="34b55-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="34b55-126">Comment tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="34b55-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="34b55-127">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="34b55-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="34b55-128">Travailler directement depuis une tooprovision de ligne de commande et de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="34b55-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="34b55-129">Comment toouse hello CLI d’Azure toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="34b55-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="34b55-130">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="34b55-130">What you need</span></span>

- <span data-ttu-id="34b55-131">Un toodownload de connexion Internet hello outils et logiciels.</span><span class="sxs-lookup"><span data-stu-id="34b55-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="34b55-132">Un ordinateur Mac exécutant OS X Yosemite (10.10) ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="34b55-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="34b55-133">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="34b55-133">Install Git and Node.js</span></span>

<span data-ttu-id="34b55-134">tooinstall Git et Node.js, utilisez l’utilitaire de gestion de package Homebrew hello en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="34b55-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="34b55-135">[Téléchargez](http://brew.sh/) et installez Homebrew.</span><span class="sxs-lookup"><span data-stu-id="34b55-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="34b55-136">Si vous avez déjà installé Homebrew, accédez à toostep 2.</span><span class="sxs-lookup"><span data-stu-id="34b55-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="34b55-137">Appuyez sur `Cmd + Space` et entrez `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="34b55-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="34b55-138">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34b55-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="34b55-139">Installer Git et Node.js en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34b55-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="34b55-140">Installer des outils de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="34b55-140">Install Node.js development tools</span></span>

<span data-ttu-id="34b55-141">Vous utilisez [fichier gulp.js](http://gulpjs.com/) tooautomate déploiement et l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="34b55-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="34b55-142">gulp de tooinstall, exécutez hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="34b55-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="34b55-143">Si vous rencontrez des problèmes avec l’installation de hello, consultez hello [guide de dépannage](iot-hub-gateway-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="34b55-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="34b55-144">Nœud, NPM et Gulp sont développés dans Node.js des scripts d’automatisation toorun requis.</span><span class="sxs-lookup"><span data-stu-id="34b55-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="34b55-145">Installation de Python</span><span class="sxs-lookup"><span data-stu-id="34b55-145">Install Python</span></span>

<span data-ttu-id="34b55-146">Bien que macOS X soit fourni avec Python 2.7, il est recommandé d’installer Python via Homebrew.</span><span class="sxs-lookup"><span data-stu-id="34b55-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="34b55-147">Consultez [Installation de Python sur macOS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="34b55-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="34b55-148">Installer Python et pip en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34b55-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="34b55-149">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="34b55-149">Install hello Azure CLI</span></span>

<span data-ttu-id="34b55-150">tooinstall hello CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="34b55-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="34b55-151">Exécutez hello suivant les commandes dans un terminal hello :</span><span class="sxs-lookup"><span data-stu-id="34b55-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="34b55-152">installation de Hello peut prendre 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="34b55-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="34b55-153">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="34b55-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="34b55-154">Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="34b55-154">You should see hello following output if hello installation is successful.</span></span>

   ![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="34b55-156">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="34b55-156">Install Visual Studio Code</span></span>

<span data-ttu-id="34b55-157">Vous utilisez Visual Studio Code ultérieurement dans les fichiers de configuration de didacticiel tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="34b55-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="34b55-158">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="34b55-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="34b55-159">Résumé</span><span class="sxs-lookup"><span data-stu-id="34b55-159">Summary</span></span>

<span data-ttu-id="34b55-160">Vous avez installé tous les outils de hello requis et des logiciels sur votre ordinateur Mac.</span><span class="sxs-lookup"><span data-stu-id="34b55-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="34b55-161">La tâche suivante est toouse hello CLI d’Azure toocreate un IoT hub et inscrire votre appareil dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="34b55-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34b55-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34b55-162">Next steps</span></span>
[<span data-ttu-id="34b55-163">Créer un IoT Hub et inscrire l’appareil</span><span class="sxs-lookup"><span data-stu-id="34b55-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
