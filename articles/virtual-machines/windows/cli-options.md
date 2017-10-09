---
title: "aaaUsing hello CLI d’Azure sur Windows | Documents Microsoft"
description: "À l’aide de hello CLI d’Azure sur Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="69e69-103">À l’aide de hello CLI d’Azure sur Windows</span><span class="sxs-lookup"><span data-stu-id="69e69-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="69e69-104">Bonjour Azure Interface de ligne de commande (CLI) fournit une ligne de commande et l’environnement de script pour créer et gérer des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="69e69-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="69e69-105">Hello CLI d’Azure est disponible pour les systèmes d’exploitation Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="69e69-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="69e69-106">Dans ces systèmes d’exploitation, les commandes CLI hello sont identiques, mais la syntaxe de script spécifique de système d’exploitation peut être différentes.</span><span class="sxs-lookup"><span data-stu-id="69e69-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="69e69-107">Ce document détails hello manières hello CLI d’Azure peut être installé et exécuté sur Windows et les détails des considérations syntaxiques pour chaque.</span><span class="sxs-lookup"><span data-stu-id="69e69-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="69e69-108">Pour en savoir plus sur Azure CLI, voir la [documentation Azure CLI]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69e69-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="69e69-109">Sous-système Windows pour Linux</span><span class="sxs-lookup"><span data-stu-id="69e69-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="69e69-110">Hello le sous-système Windows pour Linux (WSL) fournit un environnement de Ubuntu Linux sur anniversaire Windows 10 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="69e69-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="69e69-111">Une fois activé, le sous-système Windows pour Linux offre une expérience Bash native qui permet de créer et d’exécuter des scripts Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="69e69-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="69e69-112">Étant donné que le sous-système Windows pour Linux offre une expérience Bash native, les scripts Azure CLI peuvent être partagés par Mac OS, Linux et Windows sans nécessiter de modification.</span><span class="sxs-lookup"><span data-stu-id="69e69-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="69e69-113">toouse hello CLI d’Azure dans WSL, effectuer des opérations suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="69e69-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="69e69-114">Task</span><span class="sxs-lookup"><span data-stu-id="69e69-114">Task</span></span> | <span data-ttu-id="69e69-115">Instructions</span><span class="sxs-lookup"><span data-stu-id="69e69-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="69e69-116">Activer le sous-système Windows pour Linux</span><span class="sxs-lookup"><span data-stu-id="69e69-116">Enable WSL</span></span> | [<span data-ttu-id="69e69-117">Documentation d’installation du sous-système Windows pour Linux</span><span class="sxs-lookup"><span data-stu-id="69e69-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="69e69-118">Installer hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="69e69-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="69e69-119">Installer hello CLI sur WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="69e69-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="69e69-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69e69-120">PowerShell</span></span>

<span data-ttu-id="69e69-121">Hello CLI d’Azure peut être exécuté en mode natif dans Windows.</span><span class="sxs-lookup"><span data-stu-id="69e69-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="69e69-122">Dans cette configuration, package de CLI d’Azure hello est installé sur le système d’exploitation de Windows hello et commandes peuvent être exécutées à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69e69-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="69e69-123">Dans cette configuration, les scripts et les commandes CLI Azure peuvent être exécutés sur n’importe quelle version prise en charge de Windows. Cependant, une syntaxe de script spécifique à la plateforme est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="69e69-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="69e69-124">C’est pourquoi les scripts ne peuvent pas toujours être partagés par Mac OS, Linux et Windows sans nécessiter de modification.</span><span class="sxs-lookup"><span data-stu-id="69e69-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="69e69-125">toouse hello CLI d’Azure sur Windows, installer le package hello à l’aide de ces instructions, [installation hello CLI sur Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="69e69-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="69e69-126">Image Docker</span><span class="sxs-lookup"><span data-stu-id="69e69-126">Docker Image</span></span>

<span data-ttu-id="69e69-127">Lors de l’utilisation de Docker pour Windows, une image Docker qui inclut hello CLI d’Azure peut démarrer.</span><span class="sxs-lookup"><span data-stu-id="69e69-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="69e69-128">Cette image est basée sur Linux et inclut une expérience Bash native.</span><span class="sxs-lookup"><span data-stu-id="69e69-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="69e69-129">Lors de l’utilisation de Docker pour Windows et image de CLI d’Azure hello, toobe scripts partagés entre macOS, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="69e69-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="69e69-130">toouse hello CLI d’Azure sur Docker pour Windows, assurez-vous que Docker pour Windows est en cours d’exécution et exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="69e69-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="69e69-131">Une fois terminé, une session démarre qui est un interpréteur de commandes préchargée avec des outils de CLI d’Azure hello.</span><span class="sxs-lookup"><span data-stu-id="69e69-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69e69-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69e69-132">Next Steps</span></span>

[<span data-ttu-id="69e69-133">Exemple de commande pour les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="69e69-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="69e69-134">Exemples de commande pour Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="69e69-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="69e69-135">Exemples de commande pour Azure SQL</span><span class="sxs-lookup"><span data-stu-id="69e69-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
