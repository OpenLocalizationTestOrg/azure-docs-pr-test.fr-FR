---
title: "Se connecter Arduino tooAzure IoT - leçon 1 : obtenir les outils (Ubuntu) | Documents Microsoft"
description: "Téléchargez et installez les outils nécessaires hello et des logiciels pour hello premier exemple d’application pour le Wi-Fi M0 Adafruit contour sur Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "outils de développement arduino, développement iot, logiciel iot, logiciel internet des objets, installer git sur ubuntu, installer node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 7572f191-420d-41f0-923b-7ea86c0bfa73
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 586f89025d2fa11a31cb782e3789d306ade018a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="e9b8b-104">Obtenir les outils de hello (16.04 Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e9b8b-104">Get hello tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="e9b8b-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="e9b8b-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="e9b8b-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="e9b8b-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="e9b8b-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="e9b8b-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e9b8b-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="e9b8b-108">What you will do</span></span>

<span data-ttu-id="e9b8b-109">Télécharger les outils de développement hello et logiciel hello pour hello premier exemple d’application de la carte Adafruit estompe M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-109">Download hello development tools and hello software for hello first sample application for your Adafruit Feather M0 WiFi Arduino board.</span></span> 

<span data-ttu-id="e9b8b-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e9b8b-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

> [!NOTE]
> <span data-ttu-id="e9b8b-111">Bien que hello langage de la logique principale de hello de programmation est Arduino, Node.js tools sont utilisés dans hello leçons toobuild et déploiement les exemples d’applications.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-111">Although hello programming language of hello main logic is Arduino, Node.js tools are used in hello lessons toobuild and deploy sample applications.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e9b8b-112">Contenu</span><span class="sxs-lookup"><span data-stu-id="e9b8b-112">What you will learn</span></span>
<span data-ttu-id="e9b8b-113">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e9b8b-113">In this article, you will learn:</span></span>

* <span data-ttu-id="e9b8b-114">Comment tooinstall Git et Node.js</span><span class="sxs-lookup"><span data-stu-id="e9b8b-114">How tooinstall Git and Node.js</span></span>
  * <span data-ttu-id="e9b8b-115">[Git](https://git-scm.com) est un système de contrôle de versions distribué open source très populaire.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-115">[Git](https://git-scm.com) is an open source distributed version control system.</span></span> <span data-ttu-id="e9b8b-116">exemple d’application Hello pour cet article est stockée sur Git.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-116">hello sample application for this article is stored on Git.</span></span>
  * <span data-ttu-id="e9b8b-117">[Node.js](https://nodejs.org/en/) est un runtime JavaScript avec un écosystème de packages riche.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-117">[Node.js](https://nodejs.org/en/) is a JavaScript runtime with a rich package ecosystem.</span></span>
* <span data-ttu-id="e9b8b-118">Comment toouse NPM tooinstall Node.js développement des outils supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-118">How toouse NPM tooinstall additional Node.js development tools.</span></span>
  * <span data-ttu-id="e9b8b-119">la version minimale requise Hello de Node.js est 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  * <span data-ttu-id="e9b8b-120">[NPM](https://www.npmjs.com) est un des hello gestionnaires de packages pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-120">[NPM](https://www.npmjs.com) is one of hello package managers for Node.js.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9b8b-121">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="e9b8b-121">What you need</span></span>
<span data-ttu-id="e9b8b-122">toocomplete cette opération, vous devez :</span><span class="sxs-lookup"><span data-stu-id="e9b8b-122">toocomplete this operation, you will need:</span></span>
* <span data-ttu-id="e9b8b-123">Un toodownload de connexion Internet hello des outils de développement et hello logiciel.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-123">An Internet connection toodownload hello development tools and hello software.</span></span>
* <span data-ttu-id="e9b8b-124">Un ordinateur exécutant Ubuntu 16.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-124">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-nodejs-and-npm"></a><span data-ttu-id="e9b8b-125">Installation de Git, Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="e9b8b-125">Install Git, Node.js, and NPM</span></span>
<span data-ttu-id="e9b8b-126">Utiliser le raccourci clavier hello `Ctrl + Alt + T` tooopen un Bonjour Terminal Server et d’exécution suivant des commandes :</span><span class="sxs-lookup"><span data-stu-id="e9b8b-126">Use hello keyboard shortcut `Ctrl + Alt + T` tooopen a terminal and run hello following commands:</span></span>

```bash
sudo apt-get update
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install git
```

## <a name="install-additional-nodejs-development-tools"></a><span data-ttu-id="e9b8b-127">Installation des outils de développement Node.js supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e9b8b-127">Install additional Node.js development tools</span></span>
<span data-ttu-id="e9b8b-128">Utilisez [fichier gulp.js](http://gulpjs.com) déploiement de hello tooautomate de hello exemple application tooyour Arduino carte.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-128">Use [gulp.js](http://gulpjs.com) tooautomate hello deployment of hello sample application tooyour Arduino board.</span></span>

<span data-ttu-id="e9b8b-129">Installer `gulp`, `device-discovery-cli` en exécutant hello commande dans un terminal hello suivante :</span><span class="sxs-lookup"><span data-stu-id="e9b8b-129">Install `gulp`, `device-discovery-cli` by running hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp device-discovery-cli
```

<span data-ttu-id="e9b8b-130">Si vous rencontrez des problèmes d’installation de Node.js et ces outils de développement supplémentaires sur Ubuntu, consultez hello [guide de dépannage] [ troubleshooting] des problèmes de toocommon solutions.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-130">If you experience issues installing Node.js and these additional development tools on Ubuntu, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

## <a name="install-visual-studio-code"></a><span data-ttu-id="e9b8b-131">Installation de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e9b8b-131">Install Visual Studio Code</span></span>
<span data-ttu-id="e9b8b-132">[Téléchargez](https://code.visualstudio.com/docs/setup/linux) et installez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-132">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span> <span data-ttu-id="e9b8b-133">Visual Studio Code est un éditeur de code source simple mais puissant pour Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-133">Visual Studio Code is a lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="e9b8b-134">Vous utilisez cet éditeur ultérieurement dans le code d’exemple hello tooedit didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-134">You use this editor later in hello tutorial tooedit hello sample code.</span></span>

## <a name="summary"></a><span data-ttu-id="e9b8b-135">Résumé</span><span class="sxs-lookup"><span data-stu-id="e9b8b-135">Summary</span></span>
<span data-ttu-id="e9b8b-136">Vous avez installé les outils de développement hello requis et les logiciels pour hello premier exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-136">You've installed hello required development tools and software for hello first sample application.</span></span> <span data-ttu-id="e9b8b-137">la tâche suivante Hello est toocreate, déployer et exécuter l’exemple d’application hello dans votre tableau de Arduino.</span><span class="sxs-lookup"><span data-stu-id="e9b8b-137">hello next task is toocreate, deploy, and run hello sample application on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9b8b-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9b8b-138">Next steps</span></span>
<span data-ttu-id="e9b8b-139">[Créer et déployer l’application d’exemple hello blink][create-and-deploy-the-blink-sample-application]</span><span class="sxs-lookup"><span data-stu-id="e9b8b-139">[Create and deploy hello blink sample application][create-and-deploy-the-blink-sample-application]</span></span>

<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-mac.md
[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[create-and-deploy-the-blink-sample-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md