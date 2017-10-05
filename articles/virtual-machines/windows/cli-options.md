---
title: "Utilisation de l’interface de ligne de commande Azure sur Windows | Microsoft Docs"
description: "Utilisation de l’interface de ligne de commande Azure sur Windows"
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
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="aeb77-103">Utilisation de l’interface de ligne de commande Azure sur Windows</span><span class="sxs-lookup"><span data-stu-id="aeb77-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="aeb77-104">L’interface de ligne de commande Azure (CLI) fournit un environnement de script et de ligne de commande pour la création et la gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb77-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="aeb77-105">Azure CLI est disponible pour les systèmes d’exploitation Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="aeb77-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="aeb77-106">Dans ces systèmes d’exploitation, les commandes CLI sont identiques, mais la syntaxe de script peut varier.</span><span class="sxs-lookup"><span data-stu-id="aeb77-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="aeb77-107">Ce document détaille la façon dont l’interface de ligne de commande Azure peut être installée et exécutée sur Windows, ainsi que sa syntaxe.</span><span class="sxs-lookup"><span data-stu-id="aeb77-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="aeb77-108">Pour en savoir plus sur Azure CLI, voir la [documentation Azure CLI]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aeb77-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="aeb77-109">Sous-système Windows pour Linux</span><span class="sxs-lookup"><span data-stu-id="aeb77-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="aeb77-110">Le sous-système Windows pour Linux fournit un environnement Linux Ubuntu sur la Mise à jour anniversaire Microsoft Windows 10 et les éditions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="aeb77-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="aeb77-111">Une fois activé, le sous-système Windows pour Linux offre une expérience Bash native qui permet de créer et d’exécuter des scripts Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aeb77-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="aeb77-112">Étant donné que le sous-système Windows pour Linux offre une expérience Bash native, les scripts Azure CLI peuvent être partagés par Mac OS, Linux et Windows sans nécessiter de modification.</span><span class="sxs-lookup"><span data-stu-id="aeb77-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="aeb77-113">Pour utiliser l’interface de ligne de commande Azure dans le sous-système Windows pour Linux, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="aeb77-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="aeb77-114">Task</span><span class="sxs-lookup"><span data-stu-id="aeb77-114">Task</span></span> | <span data-ttu-id="aeb77-115">Instructions</span><span class="sxs-lookup"><span data-stu-id="aeb77-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="aeb77-116">Activer le sous-système Windows pour Linux</span><span class="sxs-lookup"><span data-stu-id="aeb77-116">Enable WSL</span></span> | [<span data-ttu-id="aeb77-117">Documentation d’installation du sous-système Windows pour Linux</span><span class="sxs-lookup"><span data-stu-id="aeb77-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="aeb77-118">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aeb77-118">Install the Azure CLI</span></span> |[<span data-ttu-id="aeb77-119">Installer l’interface de ligne de commande sur le sous-système Windows pour Linux/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="aeb77-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="aeb77-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aeb77-120">PowerShell</span></span>

<span data-ttu-id="aeb77-121">L’interface de ligne de commande Azure peut être exécutée en mode natif dans Windows.</span><span class="sxs-lookup"><span data-stu-id="aeb77-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="aeb77-122">Dans cette configuration, le package Azure CLI est installé sur le système d’exploitation Windows, et les commandes peuvent être exécutées à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aeb77-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="aeb77-123">Dans cette configuration, les scripts et les commandes CLI Azure peuvent être exécutés sur n’importe quelle version prise en charge de Windows. Cependant, une syntaxe de script spécifique à la plateforme est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="aeb77-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="aeb77-124">C’est pourquoi les scripts ne peuvent pas toujours être partagés par Mac OS, Linux et Windows sans nécessiter de modification.</span><span class="sxs-lookup"><span data-stu-id="aeb77-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="aeb77-125">Pour utiliser l’interface de ligne de commande Azure sur Windows, installez le package en suivant les instructions d’[installation de l’interface de ligne de commande sur Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="aeb77-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="aeb77-126">Image Docker</span><span class="sxs-lookup"><span data-stu-id="aeb77-126">Docker Image</span></span>

<span data-ttu-id="aeb77-127">Lorsque vous utilisez Docker pour Windows, vous pouvez démarrer une image Docker incluant l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb77-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="aeb77-128">Cette image est basée sur Linux et inclut une expérience Bash native.</span><span class="sxs-lookup"><span data-stu-id="aeb77-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="aeb77-129">Lorsque vous utilisez Docker pour Windows et l’image de l’interface de ligne de commande Azure, les scripts peuvent être partagés par Windows, Linux et Mac OS.</span><span class="sxs-lookup"><span data-stu-id="aeb77-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="aeb77-130">Pour utiliser l’interface de ligne de commande Azure sur Docker pour Windows, assurez-vous que Docker pour Windows est en cours d’exécution, puis exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="aeb77-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="aeb77-131">Une fois cette opération terminée, une session Bash préchargée avec les outils Azure CLI démarre.</span><span class="sxs-lookup"><span data-stu-id="aeb77-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb77-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aeb77-132">Next Steps</span></span>

[<span data-ttu-id="aeb77-133">Exemple de commande pour les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="aeb77-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="aeb77-134">Exemples de commande pour Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="aeb77-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="aeb77-135">Exemples de commande pour Azure SQL</span><span class="sxs-lookup"><span data-stu-id="aeb77-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
