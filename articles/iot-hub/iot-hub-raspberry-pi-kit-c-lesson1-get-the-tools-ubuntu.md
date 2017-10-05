---
title: "Connecter Raspberry Pi (C) à Azure IoT - Leçon 1 : Obtenir des outils (Ubuntu) | Microsoft Docs"
description: "Téléchargez et installez les outils et logiciels nécessaires pour le premier exemple d’application pour Pi sur Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, logiciel internet des objets, installer git sur ubuntu, exécuter gulp, installer node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 32cfea00-c254-4cef-8f6f-bbf807eca6b6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 28ebba82e90d91470518cd830c96e6da39d8b9b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-ubuntu-1604"></a><span data-ttu-id="a67cd-104">Obtenir les outils (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="a67cd-104">Get the tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a67cd-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="a67cd-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="a67cd-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="a67cd-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="a67cd-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="a67cd-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="a67cd-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="a67cd-108">What you will do</span></span>
<span data-ttu-id="a67cd-109">Téléchargez les outils de développement et le logiciel pour le premier exemple d’application pour votre Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="a67cd-109">Download the development tools and the software for the first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="a67cd-110">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a67cd-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a67cd-111">Le langage de programmation de la logique principale est C. Cependant, les outils Node.js sont utilisés dans cette leçon pour découvrir des appareils et créer et déployer des exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="a67cd-111">Although the programming language of the main logic is C, Node.js tools are used in the lessons to discover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a67cd-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="a67cd-112">What you will learn</span></span>
<span data-ttu-id="a67cd-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a67cd-113">In this article, you will learn:</span></span>

* <span data-ttu-id="a67cd-114">Comment installer Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="a67cd-114">How to install Git and Node.js</span></span>
  * <span data-ttu-id="a67cd-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="a67cd-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="a67cd-116">L’exemple d’application de cet article est stocké sur Git.</span><span class="sxs-lookup"><span data-stu-id="a67cd-116">The sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="a67cd-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="a67cd-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="a67cd-118">Comment utiliser NPM pour installer des outils de développement Node.js supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a67cd-118">How to use NPM to install additional Node.js development tools.</span></span>
  * <span data-ttu-id="a67cd-119">La version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="a67cd-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="a67cd-120">[NPM](https://www.npmjs.com) est l’un des gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="a67cd-120">[NPM](https://www.npmjs.com) is one of the package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a67cd-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="a67cd-121">What you need</span></span>
<span data-ttu-id="a67cd-122">Pour effectuer cette opération, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a67cd-122">To complete this operation, you will need:</span></span>

* <span data-ttu-id="a67cd-123">Une connexion Internet pour télécharger les outils de développement et le logiciel.</span><span class="sxs-lookup"><span data-stu-id="a67cd-123">An Internet connection to download the development tools and the software.</span></span>
* <span data-ttu-id="a67cd-124">Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a67cd-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="a67cd-125">Installation de Git, Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="a67cd-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="a67cd-126">Utilisez le raccourci clavier `Ctrl + Alt + T` pour ouvrir une fenêtre de terminal, puis exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a67cd-126">Use the keyboard shortcut `Ctrl + Alt + T` to open a terminal and run the following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="a67cd-127">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a67cd-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="a67cd-128">Utilisez [gulp.js](http://gulpjs.com) pour automatiser le déploiement de l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="a67cd-128">Use [gulp.js](http://gulpjs.com) to automate the deployment of the sample application to Pi.</span></span> <span data-ttu-id="a67cd-129">Utilisez [device-discovery-cli](https://github.com/Azure/device-discovery-cli) (interface de ligne de commande de découverte d’appareils) pour récupérer les informations réseau concernant vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="a67cd-129">Use the [device-discovery-cli](https://github.com/Azure/device-discovery-cli) to retrieve network information about your IoT devices.</span></span>

<span data-ttu-id="a67cd-130">Installez `gulp` et `device-discovery-cli` en exécutant la commande suivante dans la fenêtre de terminal :</span><span class="sxs-lookup"><span data-stu-id="a67cd-130">Install `gulp` and `device-discovery-cli` by running the following command in the terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="a67cd-131">Si vous rencontrez des problèmes pour installer Node.js et ces outils de développement supplémentaires sur Ubuntu, pour trouver des solutions aux problèmes courants, voir le [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a67cd-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="a67cd-132">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="a67cd-132">Install Visual Studio Code</span></span>
<span data-ttu-id="a67cd-133">[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a67cd-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="a67cd-134">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a67cd-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="a67cd-135">Vous utiliserez cet éditeur ultérieurement dans ce didacticiel pour modifier l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="a67cd-135">You use this editor later in the tutorial to edit the sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="a67cd-136">Résumé</span><span class="sxs-lookup"><span data-stu-id="a67cd-136">Summary</span></span>
<span data-ttu-id="a67cd-137">Vous avez installé les outils de développement et le logiciel nécessaire pour le premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="a67cd-137">You've installed the required development tools and software for the first sample application.</span></span> <span data-ttu-id="a67cd-138">La tâche suivante consiste à créer, déployer et exécuter l’exemple d’application sur Pi.</span><span class="sxs-lookup"><span data-stu-id="a67cd-138">The next task is to create, deploy, and run the sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a67cd-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a67cd-139">Next steps</span></span>
[<span data-ttu-id="a67cd-140">Créer et déployer l’application blink</span><span class="sxs-lookup"><span data-stu-id="a67cd-140">Create and deploy the blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

