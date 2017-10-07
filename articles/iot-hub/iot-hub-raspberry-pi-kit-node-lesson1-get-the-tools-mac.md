---
title: "Se connecter framboises Pi (nœud) tooAzure IoT - leçon 1 : obtenir les outils (macOS) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application de Pi sur macOS."
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
ms.openlocfilehash: 382b066cb7ece7ffdeb22b162b725727b22e5fac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="10e8e-104">Obtenir les outils de hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="10e8e-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10e8e-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="10e8e-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="10e8e-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="10e8e-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="10e8e-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="10e8e-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="10e8e-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="10e8e-108">What you will do</span></span>
<span data-ttu-id="10e8e-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour votre framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="10e8e-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="10e8e-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="10e8e-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="10e8e-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="10e8e-111">What you will learn</span></span>
<span data-ttu-id="10e8e-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="10e8e-112">In this article, you will learn:</span></span>

* <span data-ttu-id="10e8e-113">Comment tooinstall Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="10e8e-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="10e8e-114">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="10e8e-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="10e8e-115">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="10e8e-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="10e8e-116">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="10e8e-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="10e8e-117">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="10e8e-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="10e8e-118">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="10e8e-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="10e8e-119">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="10e8e-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="10e8e-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="10e8e-120">What you need</span></span>
<span data-ttu-id="10e8e-121">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="10e8e-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="10e8e-122">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="10e8e-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="10e8e-123">Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="10e8e-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="10e8e-124">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="10e8e-124">Install Git and Node.js</span></span>
<span data-ttu-id="10e8e-125">tooinstall Git et Node.js, utilisez hello [Homebrew](http://brew.sh) utilitaire de gestion du package en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="10e8e-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="10e8e-126">Installer Homebrew.</span><span class="sxs-lookup"><span data-stu-id="10e8e-126">Install Homebrew.</span></span> <span data-ttu-id="10e8e-127">Si vous avez déjà installé Homebrew, accédez à toostep 2.</span><span class="sxs-lookup"><span data-stu-id="10e8e-127">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="10e8e-128">Appuyez sur `Cmd + Space` et entrez `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="10e8e-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="10e8e-129">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="10e8e-129">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="10e8e-130">Installer Git et Node.js en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="10e8e-130">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="10e8e-131">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="10e8e-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="10e8e-132">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooPi d’application exemple hello.</span><span class="sxs-lookup"><span data-stu-id="10e8e-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="10e8e-133">Hello d’utilisation [périphérique-détection-cli](https://github.com/Azure/device-discovery-cli) tooretrieve les informations de réseau sur vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="10e8e-133">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="10e8e-134">Installer `gulp` et `device-discovery-cli` en exécutant hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="10e8e-134">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="10e8e-135">Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur macOS, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-node-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="10e8e-135">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-node-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="10e8e-136">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="10e8e-136">Install Visual Studio Code</span></span>
<span data-ttu-id="10e8e-137">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="10e8e-137">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="10e8e-138">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="10e8e-138">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="10e8e-139">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="10e8e-139">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="10e8e-140">Résumé</span><span class="sxs-lookup"><span data-stu-id="10e8e-140">Summary</span></span>
<span data-ttu-id="10e8e-141">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="10e8e-141">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="10e8e-142">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Pi.</span><span class="sxs-lookup"><span data-stu-id="10e8e-142">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10e8e-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10e8e-143">Next steps</span></span>
[<span data-ttu-id="10e8e-144">Créer et déployer l’application d’exemple hello blink</span><span class="sxs-lookup"><span data-stu-id="10e8e-144">Create and deploy hello blink sample application</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-deploy-blink-app.md)

