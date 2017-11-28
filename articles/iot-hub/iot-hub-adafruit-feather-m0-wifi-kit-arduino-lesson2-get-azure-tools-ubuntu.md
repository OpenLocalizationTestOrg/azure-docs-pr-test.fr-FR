---
title: "Se connecter Arduino tooAzure IoT - leçon 2 : Windows Azure tools (Ubuntu) | Documents Microsoft"
description: "Sur Ubuntu, installez Python et l’interface de ligne de commande Azure (Azure CLI)."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: interface de ligne de commande azure, service cloud iot, cloud arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="3fcc6-104">Obtenir les outils Azure (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="3fcc6-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="3fcc6-105">[Windows 7 ou version ultérieure][windows]</span><span class="sxs-lookup"><span data-stu-id="3fcc6-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="3fcc6-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="3fcc6-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="3fcc6-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="3fcc6-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="3fcc6-108">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="3fcc6-108">What you will do</span></span>

<span data-ttu-id="3fcc6-109">Installez hello Azure interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="3fcc6-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="3fcc6-110">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) pour votre carte mère Adafruit estompe M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3fcc6-111">Contenu</span><span class="sxs-lookup"><span data-stu-id="3fcc6-111">What you will learn</span></span>
<span data-ttu-id="3fcc6-112">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3fcc6-112">In this article, you will learn:</span></span>
* <span data-ttu-id="3fcc6-113">Comment tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-113">How tooinstall hello Azure CLI.</span></span>
* <span data-ttu-id="3fcc6-114">Comment tooadd un sous-groupe IoT Hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3fcc6-115">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="3fcc6-115">What you need</span></span>
* <span data-ttu-id="3fcc6-116">Un ordinateur Ubuntu connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="3fcc6-117">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-117">An active Azure subscription.</span></span> <span data-ttu-id="3fcc6-118">Si vous ne possédez pas de compte, vous pouvez créer un [compte d’évaluation gratuit](http://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="3fcc6-119">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="3fcc6-119">Install hello Azure CLI</span></span>
<span data-ttu-id="3fcc6-120">Hello CLI d’Azure fournit une expérience en ligne de commande multiplateforme pour Azure, ce qui vous toowork directement à partir de votre tooprovision de ligne de commande et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-120">hello Azure CLI provides a multiplatform command-line experience for Azure, enabling you toowork directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="3fcc6-121">tooinstall hello dernière CLI d’Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3fcc6-121">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="3fcc6-122">Exécutez hello suivant les commandes dans une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-122">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="3fcc6-123">Il peut prendre cinq minutes tooinstall hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-123">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="3fcc6-124">Hello Vérifiez-la en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3fcc6-124">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="3fcc6-125">Vous devez voir suivant de hello de sortie si l’installation de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-125">You should see hello following output if hello installation is successful.</span></span>

![Sortie qui indique la réussite][output]

## <a name="summary"></a><span data-ttu-id="3fcc6-127">Résumé</span><span class="sxs-lookup"><span data-stu-id="3fcc6-127">Summary</span></span>
<span data-ttu-id="3fcc6-128">Vous avez installé hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-128">You've installed hello Azure CLI.</span></span> <span data-ttu-id="3fcc6-129">La tâche suivante est toocreate votre Azure IoT hub et l’identité de l’appareil à l’aide hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3fcc6-129">Your next task is toocreate your Azure IoT hub and device identity using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fcc6-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3fcc6-130">Next steps</span></span>
<span data-ttu-id="3fcc6-131">[Créer votre IoT Hub et inscrire votre carte Arduino][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="3fcc6-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md