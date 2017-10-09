---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 2 : Windows Azure tools (Windows) | Documents Microsoft"
description: "Installer Python et hello Azure interface de ligne de commande (CLI d’Azure) sur Windows 7 et versions ultérieures."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 60631b54-6d2e-4e8a-88bf-7c2f8e7e1f29
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0a2e941119f9106add708591d52f32eb9ed08451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="ee3a9-104">Obtenir les outils Azure (Windows 7 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="ee3a9-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ee3a9-105">[Windows 7 et versions ultérieures][windows]</span><span class="sxs-lookup"><span data-stu-id="ee3a9-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="ee3a9-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="ee3a9-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="ee3a9-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="ee3a9-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ee3a9-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="ee3a9-108">What you will do</span></span>
<span data-ttu-id="ee3a9-109">Installer Python et hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="ee3a9-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="ee3a9-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="ee3a9-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ee3a9-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="ee3a9-111">What you will learn</span></span>
<span data-ttu-id="ee3a9-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ee3a9-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ee3a9-113">Comment tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-113">How tooinstall Python.</span></span>
* <span data-ttu-id="ee3a9-114">Comment tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ee3a9-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="ee3a9-115">What you need</span></span>
* <span data-ttu-id="ee3a9-116">Un ordinateur Windows connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="ee3a9-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-117">An active Azure subscription.</span></span> <span data-ttu-id="ee3a9-118">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="ee3a9-119">Installation de Python</span><span class="sxs-lookup"><span data-stu-id="ee3a9-119">Install Python</span></span>
<span data-ttu-id="ee3a9-120">[Installez Python](https://www.python.org/downloads/) sur votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="ee3a9-121">Vous pouvez installer Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="ee3a9-122">Ce didacticiel est basé sur Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="ee3a9-123">Si vous avez déjà installé les Python, atteindre la section suivante de toohello et installer hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="ee3a9-124">Vous devez également le chemin d’accès de hello tooadd de dossiers hello où python.exe et pip.exe sont installés toohello système `PATH` variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="ee3a9-125">Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="ee3a9-126">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="ee3a9-126">Install hello Azure CLI</span></span>
<span data-ttu-id="ee3a9-127">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="ee3a9-128">Travailler directement depuis votre tooprovision de ligne de commande et de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="ee3a9-129">tooinstall hello CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee3a9-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="ee3a9-130">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="ee3a9-131">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="ee3a9-131">Run hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="ee3a9-132">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ee3a9-132">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

<span data-ttu-id="ee3a9-133">Vous consultez suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-133">You see hello following output if hello installation is successful.</span></span>

![Sortie qui indique la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="ee3a9-135">Résumé</span><span class="sxs-lookup"><span data-stu-id="ee3a9-135">Summary</span></span>
<span data-ttu-id="ee3a9-136">Vous avez installé hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="ee3a9-137">Votre prochaine tâche toocreate votre identité de Azure IoT hub et appareil à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3a9-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee3a9-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee3a9-138">Next steps</span></span>
<span data-ttu-id="ee3a9-139">[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="ee3a9-139">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
