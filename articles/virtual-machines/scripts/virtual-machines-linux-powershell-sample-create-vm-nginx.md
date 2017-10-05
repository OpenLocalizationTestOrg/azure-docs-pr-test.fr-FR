---
title: Exemple de script PowerShell - NGINX | Microsoft Docs
description: "Exemple de script Azure PowerShell - NGINX"
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
ms.openlocfilehash: e4b2a02d6019d7610fc1dce95d94efa764c6f04c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-nginx-vm-with-powershell"></a><span data-ttu-id="3bc55-103">Créer une machine virtuelle NGINX avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bc55-103">Create an NGINX VM with PowerShell</span></span>

<span data-ttu-id="3bc55-104">Ce script crée une machine virtuelle Azure, puis utilise l’extension du script personnalisé de machine virtuelle Azure pour installer NGINX.</span><span class="sxs-lookup"><span data-stu-id="3bc55-104">This script creates an Azure Virtual Machine and then uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="3bc55-105">Une fois que vous avez exécuté le script, vous pouvez accéder à un site web de démonstration sur l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3bc55-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3bc55-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3bc55-106">Sample script</span></span>

<span data-ttu-id="3bc55-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.ps1 "Créer une machine virtuelle NGINX")]</span><span class="sxs-lookup"><span data-stu-id="3bc55-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.ps1 "Create VM NGINX")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3bc55-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="3bc55-108">Clean up deployment</span></span> 

<span data-ttu-id="3bc55-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="3bc55-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3bc55-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="3bc55-110">Script explanation</span></span>

<span data-ttu-id="3bc55-111">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3bc55-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="3bc55-112">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="3bc55-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3bc55-113">Commande</span><span class="sxs-lookup"><span data-stu-id="3bc55-113">Command</span></span> | <span data-ttu-id="3bc55-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="3bc55-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3bc55-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3bc55-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3bc55-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="3bc55-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3bc55-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3bc55-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3bc55-118">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-118">Creates a subnet configuration.</span></span> <span data-ttu-id="3bc55-119">Cette configuration est utilisée avec le processus de création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3bc55-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="3bc55-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3bc55-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="3bc55-121">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3bc55-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="3bc55-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="3bc55-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="3bc55-123">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="3bc55-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="3bc55-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="3bc55-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="3bc55-125">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="3bc55-126">Cette configuration est utilisée pour créer une règle de groupe de sécurité réseau lors de la création d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="3bc55-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="3bc55-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="3bc55-128">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="3bc55-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3bc55-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3bc55-130">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-130">Gets subnet information.</span></span> <span data-ttu-id="3bc55-131">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="3bc55-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="3bc55-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="3bc55-133">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="3bc55-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="3bc55-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="3bc55-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="3bc55-135">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3bc55-135">Creates a VM configuration.</span></span> <span data-ttu-id="3bc55-136">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="3bc55-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="3bc55-137">La configuration est utilisée lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3bc55-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="3bc55-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="3bc55-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="3bc55-139">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3bc55-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="3bc55-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="3bc55-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="3bc55-141">Ajoutez une extension de machine virtuelle à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3bc55-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="3bc55-142">Dans cet exemple, l’extension de script personnalisé sert à installer NGINX.</span><span class="sxs-lookup"><span data-stu-id="3bc55-142">In this sample, the custom script extension is used to install NGINX.</span></span> |
|[<span data-ttu-id="3bc55-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3bc55-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3bc55-144">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="3bc55-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3bc55-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bc55-145">Next steps</span></span>

<span data-ttu-id="3bc55-146">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3bc55-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3bc55-147">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3bc55-147">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
