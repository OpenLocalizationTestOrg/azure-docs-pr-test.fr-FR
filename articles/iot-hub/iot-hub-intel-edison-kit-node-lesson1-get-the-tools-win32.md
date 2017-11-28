---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 1 : obtenir les outils (Windows) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application pour Edison sur Windows 7 et versions ultérieures."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "outils de développement arduino, développement iot, logiciel iot, logiciel internet des objets, installer git sous windows, installer node js sous windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 4164b5a1-5a42-4d8a-9ff6-441e79fcc936
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 933cc585d1b8b0236d76452f5c449ae9f2f3987b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="e523f-104">Obtenir les outils de hello (Windows 7 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="e523f-104">Get hello tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e523f-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="e523f-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="e523f-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="e523f-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="e523f-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="e523f-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e523f-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="e523f-108">What you will do</span></span>
<span data-ttu-id="e523f-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="e523f-109">Download hello development tools and hello software for hello first sample application for Intel Edison.</span></span> <span data-ttu-id="e523f-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e523f-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e523f-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="e523f-111">What you will learn</span></span>
<span data-ttu-id="e523f-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e523f-112">In this article, you will learn:</span></span>

* <span data-ttu-id="e523f-113">Comment tooinstall Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="e523f-113">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="e523f-114">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="e523f-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e523f-115">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="e523f-115">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e523f-116">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="e523f-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e523f-117">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e523f-117">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="e523f-118">Hello version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e523f-118">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e523f-119">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="e523f-119">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e523f-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="e523f-120">What you need</span></span>

<span data-ttu-id="e523f-121">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="e523f-121">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="e523f-122">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="e523f-122">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="e523f-123">Un ordinateur fonctionnant sous Windows.</span><span class="sxs-lookup"><span data-stu-id="e523f-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e523f-124">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="e523f-124">Install Git and Node.js</span></span>

<span data-ttu-id="e523f-125">Cliquez sur les liens ci-dessous toodownload hello et installer Git et LTS Node.js pour Windows.</span><span class="sxs-lookup"><span data-stu-id="e523f-125">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="e523f-126">Téléchargement de Git pour Windows</span><span class="sxs-lookup"><span data-stu-id="e523f-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="e523f-127">Téléchargement de Node.js LTS pour Windows</span><span class="sxs-lookup"><span data-stu-id="e523f-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e523f-128">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e523f-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="e523f-129">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooEdison d’application exemple hello.</span><span class="sxs-lookup"><span data-stu-id="e523f-129">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooEdison.</span></span>

<span data-ttu-id="e523f-130">Lancez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e523f-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="e523f-131">Installer `gulp` en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e523f-131">Install `gulp` by running hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="e523f-132">Si vous rencontrez des problèmes d’installation de Node.js et ces autres outils de développement de Node.js sur votre ordinateur, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="e523f-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e523f-133">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e523f-133">Install Visual Studio Code</span></span>

<span data-ttu-id="e523f-134">[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e523f-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="e523f-135">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e523f-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e523f-136">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="e523f-136">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e523f-137">Résumé</span><span class="sxs-lookup"><span data-stu-id="e523f-137">Summary</span></span>

<span data-ttu-id="e523f-138">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="e523f-138">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="e523f-139">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Edison.</span><span class="sxs-lookup"><span data-stu-id="e523f-139">hello next task is toocreate, deploy, and run hello sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e523f-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e523f-140">Next steps</span></span>

<span data-ttu-id="e523f-141">[Créer et déployer des applications de clignotement hello][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="e523f-141">[Create and deploy hello blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
