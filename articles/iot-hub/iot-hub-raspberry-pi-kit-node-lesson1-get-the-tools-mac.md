---
title: "Connecter Raspberry Pi (Node) à Azure IoT - Leçon 1 : Obtenir des outils (macOS) | Microsoft Docs"
description: "Téléchargez et installez les outils et logiciels nécessaires pour le premier exemple d’application pour Pi sur macOS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "développement iot, logiciel iot, logiciel internet des objets, installer python mac, installer git sur mac, exécuter gulp, installer node js mac"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 2ea6d211-c0e8-4ade-ac69-d1c2261d78c4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6c2338baa8e88bab4c4be64568220f53178943cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-macos-1010"></a><span data-ttu-id="cc66a-104">Obtenir les outils (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="cc66a-104">Get the tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc66a-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="cc66a-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="cc66a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="cc66a-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="cc66a-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="cc66a-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="cc66a-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="cc66a-108">What you will do</span></span>
<span data-ttu-id="cc66a-109">Téléchargez les outils de développement et le logiciel pour le premier exemple d’application pour votre Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="cc66a-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="cc66a-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cc66a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cc66a-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="cc66a-111">What you will learn</span></span>
<span data-ttu-id="cc66a-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc66a-112">In this article, you will learn:</span></span>

* <span data-ttu-id="cc66a-113">Installation de Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc66a-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="cc66a-114">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="cc66a-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="cc66a-115">L’exemple d’application de cet article est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="cc66a-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="cc66a-116">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="cc66a-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="cc66a-117">Comment utiliser NPM pour installer des outils de développement Node.js supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="cc66a-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="cc66a-118">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="cc66a-118">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="cc66a-119">[NPM](https://www.npmjs.com) est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc66a-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cc66a-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="cc66a-120">What you need</span></span>
<span data-ttu-id="cc66a-121">Pour effectuer cette opération, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc66a-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="cc66a-122">Une connexion Internet pour télécharger les outils de développement et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="cc66a-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="cc66a-123">Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cc66a-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="cc66a-124">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="cc66a-124">Install Git and Node.js</span></span>
<span data-ttu-id="cc66a-125">Pour installer Git et Node.js, servez-vous de l’utilitaire de gestion de package [Homebrew](http://brew.sh) en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc66a-125">To install Git and Node.js, use the [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="cc66a-126">Installer Homebrew.</span><span class="sxs-lookup"><span data-stu-id="cc66a-126">Install Homebrew.</span></span> <span data-ttu-id="cc66a-127">Si vous avez déjà installé Homebrew, passez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="cc66a-127">If you've already installed Homebrew, go to step 2.</span></span>
   
   1. <span data-ttu-id="cc66a-128">Appuyez sur `Cmd + Space` puis entrez `Terminal` pour ouvrir une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="cc66a-128">Press `Cmd + Space` and enter `Terminal` to open a terminal.</span></span>
   2. <span data-ttu-id="cc66a-129">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cc66a-129">Run the following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="cc66a-130">Installez de Git et Node.js en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cc66a-130">Install Git and Node.js by running the following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="cc66a-131">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cc66a-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="cc66a-132">Utilisez [gulp.js](http://gulpjs.com) pour automatiser le déploiement de l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="cc66a-132">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="cc66a-133">Utilisez [device-discovery-cli](https://github.com/Azure/device-discovery-cli) (interface de ligne de commande de découverte d’appareils) pour récupérer les informations réseau concernant vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="cc66a-133">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="cc66a-134">Installez `gulp` et `device-discovery-cli` en exécutant la commande suivante dans la fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="cc66a-134">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="cc66a-135">Si vous rencontrez des problèmes pour installer Node.js et ces outils de développement supplémentaires sur macOS, pour trouver des solutions aux problèmes courants, voir le [guide de dépannage](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cc66a-135">If you experience issues installing Node.js and these additional development tools on macOS, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="cc66a-136">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="cc66a-136">Install Visual Studio Code</span></span>
<span data-ttu-id="cc66a-137">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cc66a-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="cc66a-138">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="cc66a-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="cc66a-139">Vous utiliserez cet éditeur ultérieurement dans ce didacticiel pour modifier l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="cc66a-139">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="cc66a-140">Résumé</span><span class="sxs-lookup"><span data-stu-id="cc66a-140">Summary</span></span>
<span data-ttu-id="cc66a-141">Vous avez installé les outils de développement et le logiciel nécessaire pour le premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="cc66a-141">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="cc66a-142">La tâche suivante consiste à créer, déployer et exécuter l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="cc66a-142">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc66a-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc66a-143">Next steps</span></span>
[<span data-ttu-id="cc66a-144">Création et déploiement de l’exemple d’application de clignotement</span><span class="sxs-lookup"><span data-stu-id="cc66a-144">Create and deploy the blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

