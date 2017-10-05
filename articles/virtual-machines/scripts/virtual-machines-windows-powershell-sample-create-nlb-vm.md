---
title: "Exemple de script Azure PowerShell - Création d’un équilibrage de charge réseau de machine virtuelle Windows | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Création d’un équilibrage de charge réseau de machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="5b6b9-103">Équilibrer la charge du trafic entre des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="5b6b9-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="5b6b9-104">Cet exemple de script crée tous les éléments nécessaires pour exécuter plusieurs machines virtuelles Windows Server 2016 configurées dans une configuration haute disponibilité avec équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="5b6b9-105">Une fois que vous avez exécuté le script, vous obtenez trois machines virtuelles jointes à un groupe à haute disponibilité Azure et accessibles par le biais d’Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5b6b9-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="5b6b9-106">Sample script</span></span>

<span data-ttu-id="5b6b9-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Créer un équilibrage de charge réseau de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="5b6b9-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5b6b9-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="5b6b9-108">Clean up deployment</span></span> 

<span data-ttu-id="5b6b9-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5b6b9-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="5b6b9-110">Script explanation</span></span>

<span data-ttu-id="5b6b9-111">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5b6b9-112">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5b6b9-113">Commande</span><span class="sxs-lookup"><span data-stu-id="5b6b9-113">Command</span></span> | <span data-ttu-id="5b6b9-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="5b6b9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b6b9-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5b6b9-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5b6b9-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5b6b9-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5b6b9-118">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-118">Creates a subnet configuration.</span></span> <span data-ttu-id="5b6b9-119">Cette configuration est utilisée avec le processus de création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="5b6b9-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5b6b9-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5b6b9-121">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5b6b9-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5b6b9-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5b6b9-123">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5b6b9-124">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="5b6b9-125">Crée une configuration IP frontale pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b6b9-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="5b6b9-127">Crée une configuration de pool d’adresses principales pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b6b9-128">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="5b6b9-129">Crée une configuration de sonde pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b6b9-130">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="5b6b9-131">Crée une configuration de règle pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b6b9-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="5b6b9-133">Crée une configuration de règle NAT entrante pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b6b9-134">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="5b6b9-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="5b6b9-135">Crée un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="5b6b9-136">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5b6b9-137">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5b6b9-138">Cette configuration est utilisée pour créer une règle de groupe de sécurité réseau lors de la création d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="5b6b9-139">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5b6b9-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5b6b9-140">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="5b6b9-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5b6b9-142">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-142">Gets subnet information.</span></span> <span data-ttu-id="5b6b9-143">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5b6b9-144">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5b6b9-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5b6b9-145">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="5b6b9-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5b6b9-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5b6b9-147">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-147">Creates a VM configuration.</span></span> <span data-ttu-id="5b6b9-148">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5b6b9-149">La configuration est utilisée lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5b6b9-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5b6b9-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5b6b9-151">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b6b9-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5b6b9-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5b6b9-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5b6b9-153">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="5b6b9-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5b6b9-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b6b9-154">Next steps</span></span>

<span data-ttu-id="5b6b9-155">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b6b9-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5b6b9-156">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b6b9-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
