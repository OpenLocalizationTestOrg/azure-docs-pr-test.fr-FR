---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 1 : obtenir les outils (macOS) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application pour Edison sur macOS."
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
ms.openlocfilehash: f32c0ea3c69eb2f912171fd694ae883d2586c72e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="2d16b-104">Obtenir les outils de hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="2d16b-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2d16b-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="2d16b-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="2d16b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="2d16b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="2d16b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="2d16b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2d16b-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="2d16b-108">What you will do</span></span>
<span data-ttu-id="2d16b-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour votre Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="2d16b-109">Download hello development tools and hello software for hello first sample application for your Intel Edison.</span></span> <span data-ttu-id="2d16b-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2d16b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2d16b-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="2d16b-111">What you will learn</span></span>
<span data-ttu-id="2d16b-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2d16b-112">In this article, you will learn:</span></span>

* <span data-ttu-id="2d16b-113">Comment tooinstall Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="2d16b-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="2d16b-114">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="2d16b-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="2d16b-115">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="2d16b-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="2d16b-116">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="2d16b-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="2d16b-117">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="2d16b-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="2d16b-118">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="2d16b-118">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="2d16b-119">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="2d16b-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2d16b-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="2d16b-120">What you need</span></span>
<span data-ttu-id="2d16b-121">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="2d16b-121">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="2d16b-122">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="2d16b-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="2d16b-123">Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2d16b-123">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="2d16b-124">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="2d16b-124">Install Git and Node.js</span></span>
<span data-ttu-id="2d16b-125">tooinstall Git et Node.js, utilisez hello [Homebrew](http://brew.sh) utilitaire de gestion du package en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d16b-125">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="2d16b-126">Installer Homebrew.</span><span class="sxs-lookup"><span data-stu-id="2d16b-126">Install Homebrew.</span></span> <span data-ttu-id="2d16b-127">Si vous avez déjà installé Homebrew, accédez à toostep 2.</span><span class="sxs-lookup"><span data-stu-id="2d16b-127">If you've already installed Homebrew, go toostep 2.</span></span>

   1. <span data-ttu-id="2d16b-128">Appuyez sur `Cmd + Space` et entrez `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="2d16b-128">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="2d16b-129">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d16b-129">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="2d16b-130">Installer Git et Node.js en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d16b-130">Install Git and Node.js by running hello following command:</span></span>

   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="2d16b-131">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2d16b-131">Install additional Node.js development tools</span></span>
<span data-ttu-id="2d16b-132">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de hello exemple application tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="2d16b-132">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Edison.</span></span>

<span data-ttu-id="2d16b-133">Installer `gulp` en exécutant hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="2d16b-133">Install `gulp` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="2d16b-134">Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur macOS, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="2d16b-134">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="2d16b-135">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d16b-135">Install Visual Studio Code</span></span>
<span data-ttu-id="2d16b-136">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2d16b-136">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="2d16b-137">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="2d16b-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2d16b-138">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="2d16b-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="2d16b-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="2d16b-139">Summary</span></span>
<span data-ttu-id="2d16b-140">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="2d16b-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="2d16b-141">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Edison.</span><span class="sxs-lookup"><span data-stu-id="2d16b-141">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d16b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d16b-142">Next steps</span></span>
<span data-ttu-id="2d16b-143">[Créer et déployer des applications de clignotement hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="2d16b-143">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
