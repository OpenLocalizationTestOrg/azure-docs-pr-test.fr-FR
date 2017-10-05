---
title: "Connecter Intel Edison (Node) à Azure IoT - Leçon 1 : Obtenir des outils (Windows) | Microsoft Docs"
description: "Téléchargez et installez les outils et logiciels nécessaires pour le premier exemple d’application pour Edison sur Windows 7 et versions ultérieures."
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
ms.openlocfilehash: 35b7ae24f8616848eaa6affccb96630603b823b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-or-later"></a><span data-ttu-id="e6a0d-104">Obtenir les outils (Windows 7 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="e6a0d-104">Get the tools (Windows 7 or later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e6a0d-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="e6a0d-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="e6a0d-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="e6a0d-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="e6a0d-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="e6a0d-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e6a0d-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="e6a0d-108">What you will do</span></span>
<span data-ttu-id="e6a0d-109">Téléchargez les outils de développement et le logiciel pour le premier exemple d’application pour Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-109">Download the development tools and the software for the first sample application for Intel Edison.</span></span> <span data-ttu-id="e6a0d-110">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e6a0d-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e6a0d-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="e6a0d-111">What you will learn</span></span>
<span data-ttu-id="e6a0d-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e6a0d-112">In this article, you will learn:</span></span>

* <span data-ttu-id="e6a0d-113">Installation de Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-113">How to install Git and Node.js.</span></span>
  * <span data-ttu-id="e6a0d-114">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-114">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e6a0d-115">L’exemple d’application de cet article est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-115">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e6a0d-116">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-116">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e6a0d-117">Comment utiliser NPM pour installer des outils de développement Node.js supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-117">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="e6a0d-118">La version minimum requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-118">The minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e6a0d-119">[NPM](https://www.npmjs.com) est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-119">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e6a0d-120">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="e6a0d-120">What you need</span></span>

<span data-ttu-id="e6a0d-121">Pour effectuer cette opération, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e6a0d-121">To complete this operation, you will need:</span></span>

* <span data-ttu-id="e6a0d-122">Une connexion Internet pour télécharger les outils de développement et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-122">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="e6a0d-123">Un ordinateur fonctionnant sous Windows.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-123">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="e6a0d-124">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="e6a0d-124">Install Git and Node.js</span></span>

<span data-ttu-id="e6a0d-125">Cliquez sur les liens ci-dessous pour télécharger et installer Git et Node.js LTS pour Windows.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-125">Click the links below to download and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="e6a0d-126">Téléchargement de Git pour Windows</span><span class="sxs-lookup"><span data-stu-id="e6a0d-126">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="e6a0d-127">Téléchargement de Node.js LTS pour Windows</span><span class="sxs-lookup"><span data-stu-id="e6a0d-127">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e6a0d-128">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e6a0d-128">Install additional Node.js development tools</span></span>

<span data-ttu-id="e6a0d-129">Utilisez [gulp.js](http://gulpjs.com) pour automatiser le déploiement de l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-129">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="e6a0d-130">Lancez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-130">Start a command prompt as an administrator.</span></span> <span data-ttu-id="e6a0d-131">Installez `gulp` en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e6a0d-131">Install `gulp` by running the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="e6a0d-132">Si vous rencontrez des problèmes pour installer Node.js et ces outils de développement Node.js supplémentaires sur votre ordinateur, consultez le [guide de résolution des problèmes][troubleshooting] pour trouver une solution aux problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-132">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e6a0d-133">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e6a0d-133">Install Visual Studio Code</span></span>

<span data-ttu-id="e6a0d-134">[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-134">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="e6a0d-135">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-135">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e6a0d-136">Vous utiliserez cet éditeur ultérieurement dans ce didacticiel pour modifier l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-136">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e6a0d-137">Résumé</span><span class="sxs-lookup"><span data-stu-id="e6a0d-137">Summary</span></span>

<span data-ttu-id="e6a0d-138">Vous avez installé les outils de développement et le logiciel nécessaire pour le premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-138">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="e6a0d-139">La tâche suivante consiste à créer, déployer et exécuter l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="e6a0d-139">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6a0d-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6a0d-140">Next steps</span></span>

<span data-ttu-id="e6a0d-141">[Créer et déployer l’application Blink][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="e6a0d-141">[Create and deploy the blink application][create-and-deploy-the-blink-application]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-node-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-mac.md
