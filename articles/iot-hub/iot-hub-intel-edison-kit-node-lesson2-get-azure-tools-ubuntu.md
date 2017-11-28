---
title: "Se connecter tooAzure Intel Edison (nœud) IoT - leçon 2 : Windows Azure tools (Ubuntu) | Documents Microsoft"
description: "Sur Ubuntu, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ca2996b779a4d3cde833c5f2824d19ec46241bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="82155-104">Obtenir les outils Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="82155-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="82155-105">[Windows 7 et versions ultérieures][windows]</span><span class="sxs-lookup"><span data-stu-id="82155-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="82155-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="82155-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="82155-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="82155-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="82155-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="82155-108">What you will do</span></span>
<span data-ttu-id="82155-109">Installez hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="82155-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="82155-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="82155-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="82155-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="82155-111">What you will learn</span></span>
<span data-ttu-id="82155-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="82155-112">In this article, you will learn:</span></span>
* <span data-ttu-id="82155-113">Comment tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82155-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="82155-114">Comment tooadd un sous-groupe IoT Hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82155-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="82155-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="82155-115">What you need</span></span>
* <span data-ttu-id="82155-116">Un ordinateur Ubuntu connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="82155-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="82155-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="82155-117">An active Azure subscription.</span></span> <span data-ttu-id="82155-118">Si vous ne possédez pas de compte, vous pouvez créer un [compte d’évaluation gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="82155-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="82155-119">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="82155-119">Install hello Azure CLI</span></span>
<span data-ttu-id="82155-120">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure, ce qui vous toowork directement à partir de votre tooprovision de ligne de commande et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="82155-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="82155-121">tooinstall hello dernière CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="82155-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="82155-122">Exécutez hello suivant les commandes dans une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="82155-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="82155-123">Il peut prendre cinq minutes tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82155-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="82155-124">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="82155-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="82155-125">Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="82155-125">You should see hello following output if hello installation is successful.</span></span>

![Sortie qui indique la réussite](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="82155-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="82155-127">Summary</span></span>
<span data-ttu-id="82155-128">Vous avez installé hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82155-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="82155-129">La tâche suivante est toocreate votre Azure IoT hub et l’identité de l’appareil à l’aide hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82155-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82155-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82155-130">Next steps</span></span>
<span data-ttu-id="82155-131">[Créer votre IoT Hub et inscrire Intel Edison][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="82155-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
