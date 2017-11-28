---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 1 : Obtenir des outils (macOS) | Microsoft Docs"
description: "Téléchargez et installez les outils et logiciels nécessaires pour le premier exemple d’application pour Edison sur macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "outils de développement arduino, développement iot, logiciel iot, logiciel internet des objets, installer git sur mac, installer node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fb6742be-2825-4524-89f7-8ccb7e7f1de1
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a5e406f49379e9f2192ee93334ab1dcf9f3e53d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="0bc26-104">Obtenir les outils (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="0bc26-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0bc26-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="0bc26-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="0bc26-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="0bc26-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="0bc26-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="0bc26-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0bc26-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="0bc26-108">What you will do</span></span>
<span data-ttu-id="0bc26-109">Téléchargez les outils de développement et le logiciel pour le premier exemple d’application pour Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="0bc26-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="0bc26-110">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="0bc26-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0bc26-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="0bc26-111">What you will learn</span></span>
<span data-ttu-id="0bc26-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0bc26-112">In this article, you will learn:</span></span>

* <span data-ttu-id="0bc26-113">Installation de Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="0bc26-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="0bc26-114">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="0bc26-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="0bc26-115">L’exemple d’application de cet article est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="0bc26-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="0bc26-116">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="0bc26-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="0bc26-117">Comment utiliser NPM pour installer des outils de développement Node.js supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0bc26-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="0bc26-118">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="0bc26-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="0bc26-119">[NPM](https://www.npmjs.com) est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="0bc26-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0bc26-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="0bc26-120">What you need</span></span>
<span data-ttu-id="0bc26-121">Pour effectuer cette opération, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0bc26-121">To complete this operation, you will need:</span></span>
* <span data-ttu-id="0bc26-122">Une connexion Internet pour télécharger les outils de développement et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="0bc26-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="0bc26-123">Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0bc26-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="0bc26-124">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="0bc26-124">Install Git and Node.js</span></span>
<span data-ttu-id="0bc26-125">Pour installer Git et Node.js, servez-vous de l’utilitaire de gestion de package [Homebrew](http://brew.sh) en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="0bc26-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="0bc26-126">Installer Homebrew.</span><span class="sxs-lookup"><span data-stu-id="0bc26-126">Install Homebrew.</span></span> <span data-ttu-id="0bc26-127">Si vous avez déjà installé Homebrew, passez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="0bc26-127">If you've already installed Homebrew, go to step 2.</span></span>

   1. <span data-ttu-id="0bc26-128">Appuyez sur `Cmd + Space` puis entrez `Terminal` pour ouvrir une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="0bc26-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="0bc26-129">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0bc26-129">Run the following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="0bc26-130">Installez de Git et Node.js en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0bc26-130">Install Git and Node.js by running the following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="0bc26-131">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0bc26-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="0bc26-132">Utilisez [gulp.js](http://gulpjs.com) pour automatiser le déploiement de l’exemple d’application sur votre Edison.</span><span class="sxs-lookup"><span data-stu-id="0bc26-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to your Edison.</span></span>

<span data-ttu-id="0bc26-133">Installez `gulp` en exécutant la commande suivante dans le terminal :</span><span class="sxs-lookup"><span data-stu-id="0bc26-133">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="0bc26-134">Si vous rencontrez des problèmes pour installer Node.js et ces outils de développement supplémentaires sur macOS, consultez le [guide de dépannage][troubleshooting] pour trouver des solutions aux problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="0bc26-134">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="0bc26-135">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0bc26-135">Install Visual Studio Code</span></span>
<span data-ttu-id="0bc26-136">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0bc26-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="0bc26-137">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="0bc26-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="0bc26-138">Vous utiliserez cet éditeur ultérieurement dans ce didacticiel pour modifier l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="0bc26-138">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="0bc26-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="0bc26-139">Summary</span></span>
<span data-ttu-id="0bc26-140">Vous avez installé les outils de développement et le logiciel nécessaire pour le premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="0bc26-140">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="0bc26-141">La tâche suivante consiste à créer, déployer et exécuter l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="0bc26-141">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bc26-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bc26-142">Next steps</span></span>
<span data-ttu-id="0bc26-143">[Créer et déployer l’application Blink][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="0bc26-143">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
