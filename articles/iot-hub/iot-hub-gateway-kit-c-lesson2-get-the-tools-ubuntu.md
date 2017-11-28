---
title: "Appareil SensorTag et passerelle Azure IoT - Leçon 2 : Obtenir des outils (Ubuntu) | Microsoft Docs"
description: "Installer les outils de hello et les logiciels de hello sur votre ordinateur hôte exécutant Ubuntu, créez un IoT hub et inscrire votre appareil dans le hub IoT de hello."
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
ms.openlocfilehash: c9edca91e791ef914b1920178b66eadd12ae0281
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="09d16-104">Obtenir les outils de hello (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="09d16-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09d16-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="09d16-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="09d16-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="09d16-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="09d16-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="09d16-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="09d16-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="09d16-108">What you will do</span></span>

- <span data-ttu-id="09d16-109">Installation de Git, Node.js, Gulp et Python.</span><span class="sxs-lookup"><span data-stu-id="09d16-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="09d16-110">Installez hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="09d16-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="09d16-111">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="09d16-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="09d16-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="09d16-112">What you will learn</span></span>

<span data-ttu-id="09d16-113">Dans cette leçon, vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="09d16-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="09d16-114">Comment tooinstall Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="09d16-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="09d16-115">Git est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="09d16-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="09d16-116">exemple d’application Hello pour cette leçon est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="09d16-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="09d16-117">Node.js est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="09d16-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="09d16-118">Comment les outils de développement toouse NPM tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="09d16-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="09d16-119">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="09d16-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="09d16-120">NPM est un des gestionnaires de package hello pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="09d16-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="09d16-121">Comment tooinstall Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="09d16-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="09d16-122">Visual Studio Code est un éditeur de code source multiplateforme simple mais puissant pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="09d16-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="09d16-123">Il offre une aide appréciable pour le débogage, le contrôle Git incorporé, la mise en surbrillance de syntaxe, la complétion de code intelligente, les extraits et la refactorisation de code.</span><span class="sxs-lookup"><span data-stu-id="09d16-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="09d16-124">Comment tooinstall hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="09d16-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="09d16-125">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="09d16-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="09d16-126">Travailler directement depuis une tooprovision de ligne de commande et de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="09d16-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="09d16-127">Comment toouse hello CLI d’Azure toocreate un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="09d16-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="09d16-128">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="09d16-128">What you need</span></span>

- <span data-ttu-id="09d16-129">Un toodownload de connexion Internet hello outils et logiciels.</span><span class="sxs-lookup"><span data-stu-id="09d16-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="09d16-130">Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="09d16-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="09d16-131">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="09d16-131">Install Git and Node.js</span></span>

<span data-ttu-id="09d16-132">tooinstall Git et Node.js, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="09d16-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="09d16-133">Appuyez sur `Ctrl + Alt + T` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="09d16-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="09d16-134">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="09d16-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="09d16-135">Installer des outils de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="09d16-135">Install Node.js development tools</span></span>

<span data-ttu-id="09d16-136">Vous utilisez [fichier gulp.js](http://gulpjs.com/) tooautomate déploiement et l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="09d16-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="09d16-137">gulp de tooinstall, exécutez hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="09d16-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="09d16-138">Si vous rencontrez des problèmes avec l’installation de hello, consultez hello [guide de dépannage](iot-hub-gateway-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="09d16-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="09d16-139">Nœud, NPM et Gulp sont développés dans Node.js des scripts d’automatisation toorun requis.</span><span class="sxs-lookup"><span data-stu-id="09d16-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="09d16-140">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="09d16-140">Install hello Azure CLI</span></span>

<span data-ttu-id="09d16-141">tooinstall hello CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="09d16-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="09d16-142">Exécutez hello suivant les commandes dans un terminal hello :</span><span class="sxs-lookup"><span data-stu-id="09d16-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="09d16-143">installation de Hello peut prendre 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="09d16-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="09d16-144">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="09d16-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="09d16-145">Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="09d16-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="09d16-146">![Vérifier l’installation de l’interface de ligne de commande Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="09d16-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="09d16-147">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="09d16-147">Install Visual Studio Code</span></span>

<span data-ttu-id="09d16-148">Vous utilisez Visual Studio Code ultérieurement dans les fichiers de configuration de didacticiel tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="09d16-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="09d16-149">[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="09d16-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="09d16-150">Résumé</span><span class="sxs-lookup"><span data-stu-id="09d16-150">Summary</span></span>

<span data-ttu-id="09d16-151">Vous avez installé tous les outils de hello requis et les logiciels sur votre ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="09d16-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="09d16-152">La tâche suivante est toouse hello CLI d’Azure toocreate un IoT hub et inscrire votre appareil dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="09d16-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09d16-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09d16-153">Next steps</span></span>
[<span data-ttu-id="09d16-154">Créer un hub IoT et enregistrer votre appareil</span><span class="sxs-lookup"><span data-stu-id="09d16-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
