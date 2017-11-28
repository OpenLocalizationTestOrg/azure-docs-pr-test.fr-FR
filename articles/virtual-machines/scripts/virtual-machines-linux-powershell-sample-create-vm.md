---
title: "aaaAzure exemple de Script PowerShell - créer un VM Linux | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Création d’une machine virtuelle Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8ee2ee42aa68ee135a859b7eaead25811cf54095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="4b43d-103">Création d’une machine virtuelle entièrement configurée avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b43d-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="4b43d-104">Ce script crée une machine virtuelle Azure avec un système d’exploitation Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="4b43d-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="4b43d-105">Après avoir exécuté le script de hello, vous pouvez accéder hello virtual machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="4b43d-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4b43d-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="4b43d-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4b43d-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="4b43d-107">Clean up deployment</span></span> 

<span data-ttu-id="4b43d-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="4b43d-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4b43d-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="4b43d-109">Script explanation</span></span>

<span data-ttu-id="4b43d-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="4b43d-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="4b43d-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="4b43d-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4b43d-112">Commande</span><span class="sxs-lookup"><span data-stu-id="4b43d-112">Command</span></span> | <span data-ttu-id="4b43d-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="4b43d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4b43d-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b43d-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4b43d-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="4b43d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4b43d-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4b43d-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4b43d-117">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-117">Creates a subnet configuration.</span></span> <span data-ttu-id="4b43d-118">Cette configuration est utilisée avec le processus de création du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="4b43d-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="4b43d-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4b43d-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="4b43d-120">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4b43d-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="4b43d-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4b43d-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4b43d-122">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="4b43d-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4b43d-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4b43d-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="4b43d-124">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="4b43d-125">Cette configuration est utilisé toocreate une règle de groupe de sécurité réseau lors de la création de hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="4b43d-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="4b43d-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="4b43d-127">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="4b43d-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4b43d-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4b43d-129">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-129">Gets subnet information.</span></span> <span data-ttu-id="4b43d-130">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="4b43d-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4b43d-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4b43d-132">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="4b43d-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="4b43d-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4b43d-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4b43d-134">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4b43d-134">Creates a VM configuration.</span></span> <span data-ttu-id="4b43d-135">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="4b43d-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4b43d-136">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4b43d-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4b43d-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4b43d-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4b43d-138">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4b43d-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="4b43d-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b43d-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4b43d-140">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="4b43d-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4b43d-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b43d-141">Next steps</span></span>

<span data-ttu-id="4b43d-142">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b43d-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4b43d-143">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de la machine virtuelle de Azure Linux](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b43d-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>