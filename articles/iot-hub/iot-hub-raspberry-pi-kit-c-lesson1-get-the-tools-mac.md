---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : obtenir les outils (macOS) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application de Pi sur macOS."
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
ms.openlocfilehash: 68ee44945dd69edcdf61ab3da4c80379c0ef955d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos-1010"></a><span data-ttu-id="55ca5-104">Obtenir les outils de hello (macOS 10.10)</span><span class="sxs-lookup"><span data-stu-id="55ca5-104">Get hello tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55ca5-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="55ca5-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="55ca5-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="55ca5-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="55ca5-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="55ca5-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="55ca5-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="55ca5-108">What you will do</span></span>
<span data-ttu-id="55ca5-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour votre framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="55ca5-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="55ca5-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="55ca5-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="55ca5-111">Bien que hello langage de la logique principale de hello de programmation C, Node.js tools sont utilisées dans les appareils de leçons toodiscover hello, génèrent et déploiement des exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="55ca5-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="55ca5-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="55ca5-112">What you will learn</span></span>
<span data-ttu-id="55ca5-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="55ca5-113">In this article, you will learn:</span></span>

* <span data-ttu-id="55ca5-114">Comment tooinstall Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="55ca5-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="55ca5-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="55ca5-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="55ca5-116">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="55ca5-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="55ca5-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="55ca5-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="55ca5-118">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="55ca5-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="55ca5-119">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="55ca5-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="55ca5-120">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="55ca5-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="55ca5-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="55ca5-121">What you need</span></span>
<span data-ttu-id="55ca5-122">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="55ca5-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="55ca5-123">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="55ca5-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="55ca5-124">Un Mac exécutant macOS Yosemite (10.10) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="55ca5-124">A Mac that is running macOS Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="55ca5-125">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="55ca5-125">Install Git and Node.js</span></span>
<span data-ttu-id="55ca5-126">tooinstall Git et Node.js, utilisez hello [Homebrew](http://brew.sh) utilitaire de gestion du package en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="55ca5-126">tooinstall Git and Node.js, use hello [Homebrew](http://brew.sh) package management utility by following these steps:</span></span>

1. <span data-ttu-id="55ca5-127">Installer Homebrew.</span><span class="sxs-lookup"><span data-stu-id="55ca5-127">Install Homebrew.</span></span> <span data-ttu-id="55ca5-128">Si vous avez déjà installé Homebrew, accédez à toostep 2.</span><span class="sxs-lookup"><span data-stu-id="55ca5-128">If you've already installed Homebrew, go toostep 2.</span></span>
   
   1. <span data-ttu-id="55ca5-129">Appuyez sur `Cmd + Space` et entrez `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="55ca5-129">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="55ca5-130">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="55ca5-130">Run hello following command:</span></span>
      
      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
2. <span data-ttu-id="55ca5-131">Installer Git et Node.js en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="55ca5-131">Install Git and Node.js by running hello following command:</span></span>
   
   ```bash
   brew install node git
   ```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="55ca5-132">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="55ca5-132">Install additional Node.js development tools</span></span>
<span data-ttu-id="55ca5-133">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooyour d’application exemple hello Pi.</span><span class="sxs-lookup"><span data-stu-id="55ca5-133">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Pi.</span></span> <span data-ttu-id="55ca5-134">Hello d’utilisation [périphérique-détection-cli](https://github.com/Azure/device-discovery-cli) tooretrieve les informations de réseau sur vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="55ca5-134">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="55ca5-135">Installer `gulp` et `device-discovery-cli` en exécutant hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="55ca5-135">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="55ca5-136">Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur macOS, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="55ca5-136">If you experience issues installing Node.js and these additional development tools on macOS, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="55ca5-137">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="55ca5-137">Install Visual Studio Code</span></span>
<span data-ttu-id="55ca5-138">[Téléchargez](https://code.visualstudio.com/docs/setup/osx) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="55ca5-138">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span> <span data-ttu-id="55ca5-139">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="55ca5-139">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="55ca5-140">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="55ca5-140">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="55ca5-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="55ca5-141">Summary</span></span>
<span data-ttu-id="55ca5-142">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="55ca5-142">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="55ca5-143">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Pi.</span><span class="sxs-lookup"><span data-stu-id="55ca5-143">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55ca5-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="55ca5-144">Next steps</span></span>
[<span data-ttu-id="55ca5-145">Créer et déployer des applications de clignotement hello</span><span class="sxs-lookup"><span data-stu-id="55ca5-145">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

