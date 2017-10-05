---
title: "Connecter Intel Edison (C) à Azure IoT - Leçon 1 : Obtenir des outils (Ubuntu) | Microsoft Docs"
description: "Téléchargez et installez les outils et logiciels nécessaires pour le premier exemple d’application pour Edison sur Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "outils de développement arduino, développement iot, logiciel iot, logiciel internet des objets, installer git sur ubuntu, installer node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 4c7b8e04-b892-459b-8b03-85bcaff2465c
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: e929a1cb38f1bacca833e86878c13f20e02885ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="ffe58-104">Obtenir les outils (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="ffe58-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="ffe58-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="ffe58-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="ffe58-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ffe58-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ffe58-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ffe58-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ffe58-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="ffe58-108">What you will do</span></span>
<span data-ttu-id="ffe58-109">Téléchargez les outils de développement et le logiciel pour le premier exemple d’application pour Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="ffe58-109">Download the development tools and the software for the first sample application for your Intel Edison.</span></span> <span data-ttu-id="ffe58-110">Si vous rencontrez des problèmes, recherchez des solutions sur la [page de résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ffe58-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="ffe58-111">Le langage de programmation de la logique principale est C. Cependant, les outils Node.js sont utilisés dans cette leçon pour créer et déployer des exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="ffe58-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ffe58-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="ffe58-112">What you will learn</span></span>
<span data-ttu-id="ffe58-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ffe58-113">In this article, you will learn:</span></span>

* <span data-ttu-id="ffe58-114">Comment installer Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="ffe58-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="ffe58-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="ffe58-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="ffe58-116">L’exemple d’application de cet article est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="ffe58-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="ffe58-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="ffe58-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="ffe58-118">Comment utiliser NPM pour installer des outils de développement Node.js supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ffe58-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="ffe58-119">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="ffe58-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="ffe58-120">[NPM](https://www.npmjs.com) est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffe58-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ffe58-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="ffe58-121">What you need</span></span>
<span data-ttu-id="ffe58-122">Pour effectuer cette opération, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ffe58-122">To complete this operation, you will need:</span></span>
* <span data-ttu-id="ffe58-123">Une connexion Internet pour télécharger les outils de développement et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="ffe58-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="ffe58-124">Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ffe58-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="ffe58-125">Installation de Git, Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="ffe58-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="ffe58-126">Utilisez le raccourci clavier `Ctrl + Alt + T` pour ouvrir une fenêtre de terminal, puis exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ffe58-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="ffe58-127">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ffe58-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="ffe58-128">Utilisez [gulp.js](http://gulpjs.com) pour automatiser le déploiement de l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="ffe58-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Edison.</span></span>

<span data-ttu-id="ffe58-129">Installez `gulp` en exécutant la commande suivante dans le terminal :</span><span class="sxs-lookup"><span data-stu-id="ffe58-129">Install `gulp` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="ffe58-130">Si vous rencontrez des problèmes pour installer Node.js et ces outils de développement supplémentaires sur Ubuntu, consultez le [guide de dépannage][troubleshooting] pour trouver des solutions aux problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="ffe58-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="ffe58-131">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ffe58-131">Install Visual Studio Code</span></span>
<span data-ttu-id="ffe58-132">[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ffe58-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="ffe58-133">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="ffe58-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="ffe58-134">Vous utiliserez cet éditeur ultérieurement dans ce didacticiel pour modifier l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="ffe58-134">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="ffe58-135">Résumé</span><span class="sxs-lookup"><span data-stu-id="ffe58-135">Summary</span></span>
<span data-ttu-id="ffe58-136">Vous avez installé les outils de développement et le logiciel nécessaire pour le premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="ffe58-136">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="ffe58-137">La tâche suivante consiste à créer, déployer et exécuter l’exemple d’application sur Edison.</span><span class="sxs-lookup"><span data-stu-id="ffe58-137">The next task is to create, deploy, and run the sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffe58-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ffe58-138">Next steps</span></span>
<span data-ttu-id="ffe58-139">[Création et déploiement de l’exemple d’application de clignotement][create-and-deploy-the-blink-application]</span><span class="sxs-lookup"><span data-stu-id="ffe58-139">[Create and deploy the blink sample application][create-and-deploy-the-blink-application]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-and-deploy-the-blink-application]: iot-hub-intel-edison-kit-c-lesson1-deploy-blink-app.md
[windows]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-mac.md
