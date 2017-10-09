---
title: "Connect Raspberry PI (C) tooAzure IoT - leçon 2 : Windows Azure tools (Windows) | Documents Microsoft"
description: "Installer Python et hello Azure interface de ligne de commande (CLI d’Azure) sur Windows 7 et versions ultérieures."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: iot cloud service, azure cli
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="d040f-104">Obtenir les outils Azure (Windows 7 et versions ultérieures)</span><span class="sxs-lookup"><span data-stu-id="d040f-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d040f-105">Windows 7 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="d040f-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="d040f-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d040f-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="d040f-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="d040f-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="d040f-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="d040f-108">What you will do</span></span>
<span data-ttu-id="d040f-109">Installer Python et hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="d040f-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="d040f-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d040f-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d040f-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="d040f-111">What you will learn</span></span>
<span data-ttu-id="d040f-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d040f-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d040f-113">Comment tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="d040f-113">How tooinstall Python.</span></span>
* <span data-ttu-id="d040f-114">Comment tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d040f-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d040f-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="d040f-115">What you need</span></span>
* <span data-ttu-id="d040f-116">Un ordinateur Windows connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="d040f-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="d040f-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="d040f-117">An active Azure subscription.</span></span> <span data-ttu-id="d040f-118">Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte d’évaluation Azure gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d040f-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="d040f-119">Installation de Python</span><span class="sxs-lookup"><span data-stu-id="d040f-119">Install Python</span></span>
<span data-ttu-id="d040f-120">[Installez Python](https://www.python.org/downloads/) sur votre ordinateur Windows.</span><span class="sxs-lookup"><span data-stu-id="d040f-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="d040f-121">Vous pouvez installer Python 2.7, 3.4 ou 3.5.</span><span class="sxs-lookup"><span data-stu-id="d040f-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="d040f-122">Ce didacticiel est basé sur Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="d040f-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="d040f-123">Si vous avez déjà installé les Python, atteindre la section suivante de toohello et installer hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d040f-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="d040f-124">Vous devez également le chemin d’accès de hello tooadd de dossiers hello où python.exe et pip.exe sont installés toohello système `PATH` variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d040f-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="d040f-125">Par défaut, python.exe est installé dans `C:\Python27`, et pip.exe dans `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="d040f-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="d040f-126">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="d040f-126">Install hello Azure CLI</span></span>
<span data-ttu-id="d040f-127">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure.</span><span class="sxs-lookup"><span data-stu-id="d040f-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="d040f-128">Travailler directement depuis votre tooprovision de ligne de commande et de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="d040f-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="d040f-129">tooinstall hello CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d040f-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="d040f-130">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d040f-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="d040f-131">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d040f-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="d040f-132">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d040f-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="d040f-133">Vous consultez suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="d040f-133">You see hello following output if hello installation is successful.</span></span>

![Sortie qui indique la réussite](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="d040f-135">Résumé</span><span class="sxs-lookup"><span data-stu-id="d040f-135">Summary</span></span>
<span data-ttu-id="d040f-136">Vous avez installé hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d040f-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="d040f-137">Votre prochaine tâche toocreate votre identité de Azure IoT hub et appareil à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d040f-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d040f-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d040f-138">Next steps</span></span>
[<span data-ttu-id="d040f-139">Créer votre IoT Hub et inscrire Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d040f-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

