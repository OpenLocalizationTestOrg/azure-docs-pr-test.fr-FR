---
title: "aaaDifferent manières toocreate un ordinateur virtuel Windows Azure | Documents Microsoft"
description: "Répertorie les différentes façons de hello toocreate machine virtuelle Windows avec le Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="8cd33-103">Différentes façons toocreate une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="8cd33-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="8cd33-104">Azure offre toocreate de différentes façons d’un ordinateur virtuel, car les machines virtuelles sont adaptés à différents utilisateurs et à des fins.</span><span class="sxs-lookup"><span data-stu-id="8cd33-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="8cd33-105">Cela signifie que vous devez toomake certains choix sur l’ordinateur virtuel de hello et comment toocreate il.</span><span class="sxs-lookup"><span data-stu-id="8cd33-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="8cd33-106">Cet article vous fournit un résumé de ces choix et des liens tooinstructions.</span><span class="sxs-lookup"><span data-stu-id="8cd33-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="8cd33-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8cd33-107">Azure portal</span></span>
<span data-ttu-id="8cd33-108">À l’aide de hello portail Azure d’est une tootry facilement à une machine virtuelle, en particulier si vous démarrez avec Azure.</span><span class="sxs-lookup"><span data-stu-id="8cd33-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="8cd33-109">Créer une machine virtuelle exécutant Windows à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="8cd33-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="8cd33-110">Modèle</span><span class="sxs-lookup"><span data-stu-id="8cd33-110">Template</span></span>
<span data-ttu-id="8cd33-111">Les machines virtuelles requièrent une combinaison de ressources (par exemple un groupe à haute disponibilité et des comptes de stockage).</span><span class="sxs-lookup"><span data-stu-id="8cd33-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="8cd33-112">Plutôt que le déploiement et la gestion de chaque ressource séparément, vous pouvez créer un modèle Azure Resource Manager qui déploie et configure toutes les ressources hello dans une opération unique et coordonnée.</span><span class="sxs-lookup"><span data-stu-id="8cd33-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="8cd33-113">Création d’une machine virtuelle Windows avec un modèle du Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="8cd33-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="8cd33-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd33-114">Azure PowerShell</span></span>
<span data-ttu-id="8cd33-115">Si vous préférez travailler dans une invite de commandes, vous pouvez utiliser Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8cd33-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="8cd33-116">Créer une machine virtuelle Windows à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cd33-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="8cd33-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cd33-117">Visual Studio</span></span>
<span data-ttu-id="8cd33-118">Utilisez Visual Studio toobuild, gérer et déployer des machines virtuelles avec hello Windows Azure Tools pour Visual Studio et hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="8cd33-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="8cd33-119">Azure Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cd33-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

