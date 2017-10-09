---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : obtenir les outils (Windows) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application de Pi sous Windows 7 et versions ultérieures."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "développement iot, logiciel iot, logiciel internet des objets, installer git sur windows, installer node js sur windows, installer npm sur windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: bd765ddd-65b7-4241-a391-dc77cb3af1c0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 70ae6d15f9d6af116ff065a79a30d99afc67bffd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-or-later"></a><span data-ttu-id="f39a9-104">Obtenir les outils de hello (Windows 7 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="f39a9-104">Get hello tools (Windows 7 or later)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f39a9-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="f39a9-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="f39a9-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f39a9-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="f39a9-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="f39a9-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="f39a9-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="f39a9-108">What you will do</span></span>
<span data-ttu-id="f39a9-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="f39a9-109">Download hello development tools and hello software for hello first sample application for Raspberry Pi 3.</span></span> <span data-ttu-id="f39a9-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f39a9-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f39a9-111">Bien que hello langage de la logique principale de hello de programmation C, Node.js tools sont utilisées dans les appareils de leçons toodiscover hello, génèrent et déploiement des exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="f39a9-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f39a9-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="f39a9-112">What you will learn</span></span>
<span data-ttu-id="f39a9-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f39a9-113">In this article, you will learn:</span></span>

* <span data-ttu-id="f39a9-114">Comment tooinstall Git et Node.js.</span><span class="sxs-lookup"><span data-stu-id="f39a9-114">How tooinstall Git and Node.js.</span></span>
  * <span data-ttu-id="f39a9-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="f39a9-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="f39a9-116">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="f39a9-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="f39a9-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="f39a9-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="f39a9-118">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f39a9-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="f39a9-119">Hello version minimale requise de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="f39a9-119">hello minimum version requirement of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="f39a9-120">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="f39a9-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f39a9-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="f39a9-121">What you need</span></span>

<span data-ttu-id="f39a9-122">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f39a9-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="f39a9-123">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="f39a9-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="f39a9-124">Un ordinateur fonctionnant sous Windows.</span><span class="sxs-lookup"><span data-stu-id="f39a9-124">A computer that is running Windows.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="f39a9-125">Installation de Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="f39a9-125">Install Git and Node.js</span></span>

<span data-ttu-id="f39a9-126">Cliquez sur les liens ci-dessous toodownload hello et installer Git et LTS Node.js pour Windows.</span><span class="sxs-lookup"><span data-stu-id="f39a9-126">Click hello links below toodownload and install Git and Node.js LTS for Windows.</span></span>

* [<span data-ttu-id="f39a9-127">Téléchargement de Git pour Windows</span><span class="sxs-lookup"><span data-stu-id="f39a9-127">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
* [<span data-ttu-id="f39a9-128">Téléchargement de Node.js LTS pour Windows</span><span class="sxs-lookup"><span data-stu-id="f39a9-128">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="f39a9-129">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f39a9-129">Install additional Node.js development tools</span></span>

<span data-ttu-id="f39a9-130">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooPi d’application exemple hello.</span><span class="sxs-lookup"><span data-stu-id="f39a9-130">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="f39a9-131">Hello d’utilisation [périphérique-détection-cli](https://github.com/Azure/device-discovery-cli) tooretrieve les informations de réseau sur vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="f39a9-131">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="f39a9-132">Lancez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f39a9-132">Start a command prompt as an administrator.</span></span> <span data-ttu-id="f39a9-133">Installer `gulp` et `device-discovery-cli` en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f39a9-133">Install `gulp` and `device-discovery-cli` by running hello following command:</span></span>

```bash
npm install -g device-discovery-cli gulp
```

<span data-ttu-id="f39a9-134">Si vous rencontrez des problèmes d’installation de Node.js et ces autres outils de développement de Node.js sur votre ordinateur, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="f39a9-134">If you experience issues installing Node.js and these additional Node.js development tools on your computer, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="f39a9-135">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f39a9-135">Install Visual Studio Code</span></span>

<span data-ttu-id="f39a9-136">[Téléchargez](https://code.visualstudio.com/docs/setup/windows) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f39a9-136">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span> <span data-ttu-id="f39a9-137">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="f39a9-137">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="f39a9-138">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="f39a9-138">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="f39a9-139">Résumé</span><span class="sxs-lookup"><span data-stu-id="f39a9-139">Summary</span></span>

<span data-ttu-id="f39a9-140">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="f39a9-140">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="f39a9-141">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Pi.</span><span class="sxs-lookup"><span data-stu-id="f39a9-141">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f39a9-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f39a9-142">Next steps</span></span>

[<span data-ttu-id="f39a9-143">Créer et déployer des applications de clignotement hello</span><span class="sxs-lookup"><span data-stu-id="f39a9-143">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)
