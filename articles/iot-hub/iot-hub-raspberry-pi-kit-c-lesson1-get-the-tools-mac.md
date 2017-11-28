---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 1 : Obtenir des outils (macOS) | Microsoft Docs"
description: "Téléchargez et installez les outils et logiciels nécessaires pour le premier exemple d’application pour Pi sur macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, logiciel internet des objets, installer git sur mac, exécuter gulp, installer node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fc6bd2c8-a847-4bf5-818f-6f7f9a6835ee
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 64db77040ef3482f213bd622320fdb5df243fa93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="bd5f0-104">Obtenir les outils (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="bd5f0-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd5f0-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="bd5f0-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="bd5f0-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="bd5f0-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="bd5f0-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="bd5f0-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="bd5f0-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="bd5f0-108">What you will do</span></span>
<span data-ttu-id="bd5f0-109">Téléchargez les outils de développement et le logiciel pour le premier exemple d’application pour votre Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="bd5f0-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f0-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bd5f0-111">Le langage de programmation de la logique principale est C. Cependant, les outils Node.js sont utilisés dans cette leçon pour découvrir des appareils et créer et déployer des exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bd5f0-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="bd5f0-112">What you will learn</span></span>
<span data-ttu-id="bd5f0-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bd5f0-113">In this article, you will learn:</span></span>

* <span data-ttu-id="bd5f0-114">Installation de Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-114">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="bd5f0-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="bd5f0-116">L’exemple d’application de cet article est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="bd5f0-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="bd5f0-118">Comment utiliser NPM pour installer des outils de développement Node.js supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="bd5f0-119">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="bd5f0-120">[NPM](https://www.npmjs.com) est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bd5f0-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="bd5f0-121">What you need</span></span>
<span data-ttu-id="bd5f0-122">Pour effectuer cette opération, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bd5f0-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="bd5f0-123">Une connexion Internet pour télécharger les outils de développement et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="bd5f0-124">Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="bd5f0-125">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="bd5f0-125">Install Git and Node.js</span></span>
<span data-ttu-id="bd5f0-126">Pour installer Git et Node.js, servez-vous de l’utilitaire de gestion de package [Homebrew](http://brew.sh) en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="bd5f0-126">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="bd5f0-127">Installer Homebrew.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-127">Install Homebrew.</span></span> <span data-ttu-id="bd5f0-128">Si vous avez déjà installé Homebrew, passez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-128">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="bd5f0-129">Appuyez sur `Cmd + Space` puis entrez `Terminal` pour ouvrir une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-129">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="bd5f0-130">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bd5f0-130">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="bd5f0-131">Installez de Git et Node.js en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bd5f0-131">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="bd5f0-132">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bd5f0-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="bd5f0-133">Utilisez [gulp.js](http://gulpjs.com) pour automatiser le déploiement de l’exemple d’application sur votre Pi.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-133">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Pi.</span></span> <span data-ttu-id="bd5f0-134">Utilisez [device-discovery-cli](https://github.com/Azure/device-discovery-cli) (interface de ligne de commande de découverte d’appareils) pour récupérer les informations réseau concernant vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-134">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="bd5f0-135">Installez `gulp` et `device-discovery-cli` en exécutant la commande suivante dans la fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="bd5f0-135">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="bd5f0-136">Si vous rencontrez des problèmes pour installer Node.js et ces outils de développement supplémentaires sur macOS, pour trouver des solutions aux problèmes courants, voir le [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f0-136">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="bd5f0-137">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bd5f0-137">Install Visual Studio Code</span></span>
<span data-ttu-id="bd5f0-138">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="bd5f0-139">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="bd5f0-140">Vous utiliserez cet éditeur ultérieurement dans ce didacticiel pour modifier l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-140">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="bd5f0-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="bd5f0-141">Summary</span></span>
<span data-ttu-id="bd5f0-142">Vous avez installé les outils de développement et le logiciel nécessaire pour le premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-142">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="bd5f0-143">La tâche suivante consiste à créer, déployer et exécuter l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="bd5f0-143">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd5f0-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd5f0-144">Next steps</span></span>
[<span data-ttu-id="bd5f0-145">Créer et déployer l’application blink</span><span class="sxs-lookup"><span data-stu-id="bd5f0-145">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

