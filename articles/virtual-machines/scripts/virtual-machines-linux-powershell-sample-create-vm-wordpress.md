---
title: Exemple de script PowerShell - WordPress | Microsoft Docs
description: "Exemple de script Azure PowerShell - WordPress"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 778a6d5cfc63f80aa66654d682fedb178cfd67a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="8edbc-103">Créer une machine virtuelle WordPress avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8edbc-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="8edbc-104">Ce script crée une machine virtuelle et utilise l’extension du script personnalisé de machine virtuelle Azure pour installer WordPress.</span><span class="sxs-lookup"><span data-stu-id="8edbc-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="8edbc-105">Une fois que vous avez exécuté le script, vous pouvez accéder au site de configuration de WordPress à l’adresse `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="8edbc-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8edbc-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="8edbc-106">Sample script</span></span>

<span data-ttu-id="8edbc-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Création d’une machine virtuelle WordPress")]</span><span class="sxs-lookup"><span data-stu-id="8edbc-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8edbc-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="8edbc-108">Clean up deployment</span></span> 

<span data-ttu-id="8edbc-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="8edbc-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8edbc-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="8edbc-110">Script explanation</span></span>

<span data-ttu-id="8edbc-111">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8edbc-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="8edbc-112">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="8edbc-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8edbc-113">Commande</span><span class="sxs-lookup"><span data-stu-id="8edbc-113">Command</span></span> | <span data-ttu-id="8edbc-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="8edbc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8edbc-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8edbc-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8edbc-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="8edbc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8edbc-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8edbc-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8edbc-118">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-118">Creates a subnet configuration.</span></span> <span data-ttu-id="8edbc-119">Cette configuration est utilisée avec le processus de création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8edbc-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="8edbc-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8edbc-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="8edbc-121">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8edbc-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="8edbc-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="8edbc-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="8edbc-123">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8edbc-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="8edbc-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8edbc-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="8edbc-125">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="8edbc-126">Cette configuration est utilisée pour créer une règle de groupe de sécurité réseau lors de la création d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="8edbc-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="8edbc-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="8edbc-128">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="8edbc-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8edbc-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8edbc-130">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-130">Gets subnet information.</span></span> <span data-ttu-id="8edbc-131">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="8edbc-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8edbc-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="8edbc-133">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="8edbc-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="8edbc-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="8edbc-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="8edbc-135">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8edbc-135">Creates a VM configuration.</span></span> <span data-ttu-id="8edbc-136">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="8edbc-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="8edbc-137">La configuration est utilisée lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8edbc-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="8edbc-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="8edbc-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="8edbc-139">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8edbc-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="8edbc-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="8edbc-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="8edbc-141">Ajoute une extension de script personnalisé à la machine virtuelle, qui appelle un script pour installer WordPress.</span><span class="sxs-lookup"><span data-stu-id="8edbc-141">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
|[<span data-ttu-id="8edbc-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8edbc-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8edbc-143">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="8edbc-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8edbc-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8edbc-144">Next steps</span></span>

<span data-ttu-id="8edbc-145">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8edbc-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8edbc-146">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8edbc-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
