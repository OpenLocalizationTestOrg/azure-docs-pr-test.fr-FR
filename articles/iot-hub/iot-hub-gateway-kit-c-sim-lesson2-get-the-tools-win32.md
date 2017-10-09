---
title: "Appareil simulé et passerelle Azure IoT - Leçon 2 : Obtenir des outils (Windows) | Microsoft Docs"
description: "Installer les outils de hello et les logiciels de hello sur votre ordinateur hôte exécutant Windows, créez un IoT hub et inscrire votre appareil dans le hub IoT de hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, service cloud iot, logiciel internet des objets, azure cli, installer git sur windows, exécuter gulp, installer node js windows, installer npm sur windows, installer python sur windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7ca3c9f11eb232f853fc8fd921b0a49ae37d0184
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="0e503-104">Obtenir les outils de hello (Windows 7 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="0e503-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e503-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="0e503-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="0e503-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="0e503-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="0e503-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="0e503-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="0e503-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="0e503-108">What you will do</span></span>

- <span data-ttu-id="0e503-109">Installation de Git, Node.js, Gulp et Python.</span><span class="sxs-lookup"><span data-stu-id="0e503-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="0e503-110">Installez hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="0e503-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="0e503-111">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0e503-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0e503-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="0e503-112">What you will learn</span></span>

<span data-ttu-id="0e503-113">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="0e503-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="0e503-114">Comment tooinstall [Git](https://git-scm.com/) et [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="0e503-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="0e503-115">Git est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="0e503-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="0e503-116">exemple d’application Hello pour cette leçon est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="0e503-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="0e503-117">Node.js est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="0e503-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="0e503-118">Comment toouse [NPM](https://www.npmjs.com/) tooinstall des outils de développement Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e503-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="0e503-119">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="0e503-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="0e503-120">NPM est un des gestionnaires de package hello pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="0e503-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="0e503-121">Comment tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0e503-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="0e503-122">Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="0e503-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="0e503-123">Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.</span><span class="sxs-lookup"><span data-stu-id="0e503-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="0e503-124">Comment tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="0e503-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="0e503-125">Python est un langage de programmation interprété et dynamique, à usage général et fréquemment utilisé.</span><span class="sxs-lookup"><span data-stu-id="0e503-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="0e503-126">Comment tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0e503-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="0e503-127">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="0e503-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="0e503-128">Travailler directement depuis une tooprovision de ligne de commande et de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="0e503-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="0e503-129">Comment toouse hello CLI d’Azure toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0e503-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0e503-130">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="0e503-130">What you need</span></span>

- <span data-ttu-id="0e503-131">Un toodownload de connexion Internet hello outils et logiciels.</span><span class="sxs-lookup"><span data-stu-id="0e503-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="0e503-132">Un ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="0e503-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="0e503-133">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="0e503-133">Install Git and Node.js</span></span>

<span data-ttu-id="0e503-134">Cliquez sur Suivant toodownload de liens de hello et installer Git et LTS Node.js pour Windows.</span><span class="sxs-lookup"><span data-stu-id="0e503-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="0e503-135">Téléchargement de Git pour Windows</span><span class="sxs-lookup"><span data-stu-id="0e503-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="0e503-136">Téléchargement de Node.js LTS pour Windows</span><span class="sxs-lookup"><span data-stu-id="0e503-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="0e503-137">Installer des outils de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="0e503-137">Install Node.js development tools</span></span>

<span data-ttu-id="0e503-138">Vous utilisez [fichier gulp.js](http://gulpjs.com/) tooautomate déploiement et l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="0e503-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="0e503-139">Appuyez sur `Windows + R`, type `cmd` et appuyez sur `Enter` tooopen une fenêtre d’invite de commandes, puis en exécution hello suivant commande :</span><span class="sxs-lookup"><span data-stu-id="0e503-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="0e503-140">Si vous rencontrez des problèmes avec l’installation de hello, consultez hello [guide de dépannage](iot-hub-gateway-kit-c-sim-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="0e503-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="0e503-141">Nœud, NPM et Gulp sont développés dans Node.js des scripts d’automatisation toorun requis.</span><span class="sxs-lookup"><span data-stu-id="0e503-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="0e503-142">Installation de Python</span><span class="sxs-lookup"><span data-stu-id="0e503-142">Install Python</span></span>

<span data-ttu-id="0e503-143">Vous pouvez choisir entre Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="0e503-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="0e503-144">Dans ce didacticiel, nous utilisons Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="0e503-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="0e503-145">Si vous avez déjà installé les python, accédez à toohello la prochaine section.</span><span class="sxs-lookup"><span data-stu-id="0e503-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="0e503-146">Obtenir Python pour Windows</span><span class="sxs-lookup"><span data-stu-id="0e503-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="0e503-147">Vous devez également le chemin d’accès de hello tooadd de dossiers hello où Python.exe et pip.exe sont installés toohello système `PATH` variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="0e503-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="0e503-148">Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="0e503-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="0e503-149">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="0e503-149">Install hello Azure CLI</span></span>

<span data-ttu-id="0e503-150">tooinstall hello CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0e503-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0e503-151">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0e503-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="0e503-152">Installez hello CLI d’Azure en exécutant hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="0e503-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="0e503-153">installation de Hello peut prendre 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="0e503-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="0e503-154">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e503-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="0e503-155">Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="0e503-155">You should see hello following output if hello installation is successful.</span></span>

   ![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="0e503-157">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0e503-157">Install Visual Studio Code</span></span>

<span data-ttu-id="0e503-158">Vous utilisez Visual Studio Code ultérieurement dans les fichiers de configuration de didacticiel tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="0e503-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="0e503-159">[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0e503-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="0e503-160">Résumé</span><span class="sxs-lookup"><span data-stu-id="0e503-160">Summary</span></span>

<span data-ttu-id="0e503-161">Vous avez installé tous les outils de hello requis et les logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="0e503-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="0e503-162">La tâche suivante est toouse hello CLI d’Azure toocreate un IoT hub et inscrire votre appareil dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0e503-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e503-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e503-163">Next steps</span></span>
[<span data-ttu-id="0e503-164">Créer un hub IoT et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="0e503-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
