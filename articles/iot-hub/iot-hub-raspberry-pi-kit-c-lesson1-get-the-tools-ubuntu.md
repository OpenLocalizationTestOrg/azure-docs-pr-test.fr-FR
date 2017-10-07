---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 1 : obtenir les outils (Ubuntu) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application de Pi sur Ubuntu."
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
ms.openlocfilehash: 794928b5da63521cb0a72cb54256f2ad9724ec84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="088cc-104">Obtenir les outils de hello (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="088cc-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="088cc-105">Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="088cc-105">Windows 7 or later</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)
> * [<span data-ttu-id="088cc-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="088cc-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="088cc-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="088cc-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="088cc-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="088cc-108">What you will do</span></span>
<span data-ttu-id="088cc-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application pour votre framboises Pi 3.</span><span class="sxs-lookup"><span data-stu-id="088cc-109">Download hello development tools and hello software for hello first sample application for your Raspberry Pi 3.</span></span> <span data-ttu-id="088cc-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="088cc-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

> [!NOTE]
> <span data-ttu-id="088cc-111">Bien que hello langage de la logique principale de hello de programmation C, Node.js tools sont utilisées dans les appareils de leçons toodiscover hello, génèrent et déploiement des exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="088cc-111">Although hello programming language of hello main logic is C, Node.js tools are used in hello lessons toodiscover devices, and build and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="088cc-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="088cc-112">What you will learn</span></span>
<span data-ttu-id="088cc-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="088cc-113">In this article, you will learn:</span></span>

* <span data-ttu-id="088cc-114">Comment tooinstall Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="088cc-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="088cc-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="088cc-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="088cc-116">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="088cc-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="088cc-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="088cc-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="088cc-118">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="088cc-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="088cc-119">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="088cc-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="088cc-120">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="088cc-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="088cc-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="088cc-121">What you need</span></span>
<span data-ttu-id="088cc-122">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="088cc-122">toocomplete this operation, you will need:</span></span>

* <span data-ttu-id="088cc-123">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="088cc-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="088cc-124">Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="088cc-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="088cc-125">Installation de Git, Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="088cc-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="088cc-126">Utiliser le raccourci clavier hello `Ctrl + Alt + T` tooopen un Bonjour Terminal Server et d’exécution suivant des commandes :</span><span class="sxs-lookup"><span data-stu-id="088cc-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="088cc-127">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="088cc-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="088cc-128">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de tooPi d’application exemple hello.</span><span class="sxs-lookup"><span data-stu-id="088cc-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooPi.</span></span> <span data-ttu-id="088cc-129">Hello d’utilisation [périphérique-détection-cli](https://github.com/Azure/device-discovery-cli) tooretrieve les informations de réseau sur vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="088cc-129">Use hello [device-discovery-cli](https://github.com/Azure/device-discovery-cli) tooretrieve network information about your IoT devices.</span></span>

<span data-ttu-id="088cc-130">Installer `gulp` et `device-discovery-cli` en exécutant hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="088cc-130">Install `gulp` and `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g device-discovery-cli gulp
```

<span data-ttu-id="088cc-131">Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur Ubuntu, consultez hello [guide de dépannage](iot-hub-raspberry-pi-kit-c-troubleshooting.md) pour les problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="088cc-131">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="088cc-132">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="088cc-132">Install Visual Studio Code</span></span>
<span data-ttu-id="088cc-133">[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="088cc-133">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="088cc-134">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="088cc-134">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="088cc-135">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="088cc-135">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="088cc-136">Résumé</span><span class="sxs-lookup"><span data-stu-id="088cc-136">Summary</span></span>
<span data-ttu-id="088cc-137">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="088cc-137">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="088cc-138">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello sur Pi.</span><span class="sxs-lookup"><span data-stu-id="088cc-138">hello next task is toocreate, deploy, and run hello sample application on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="088cc-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="088cc-139">Next steps</span></span>
[<span data-ttu-id="088cc-140">Créer et déployer des applications de clignotement hello</span><span class="sxs-lookup"><span data-stu-id="088cc-140">Create and deploy hello blink application</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-deploy-blink-app.md)

