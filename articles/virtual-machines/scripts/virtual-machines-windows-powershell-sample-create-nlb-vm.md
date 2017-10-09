---
title: "aaaAzure exemple de Script PowerShell - créer une machine virtuelle Windows NLB | Documents Microsoft"
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
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="d4a22-103">Équilibrer la charge du trafic entre des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="d4a22-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="d4a22-104">Cet exemple de script crée tous les éléments nécessaires toorun plusieurs machines virtuelles de Windows Server 2016 configurés dans une haute disponibilité et de charge équilibrée de configuration.</span><span class="sxs-lookup"><span data-stu-id="d4a22-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="d4a22-105">Après l’exécution du script hello, vous aurez trois machines virtuelles, tooan jointe à haute disponibilité Azure et accessible via un équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a22-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d4a22-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d4a22-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d4a22-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="d4a22-107">Clean up deployment</span></span> 

<span data-ttu-id="d4a22-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="d4a22-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d4a22-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d4a22-109">Script explanation</span></span>

<span data-ttu-id="d4a22-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="d4a22-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="d4a22-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="d4a22-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d4a22-112">Commande</span><span class="sxs-lookup"><span data-stu-id="d4a22-112">Command</span></span> | <span data-ttu-id="d4a22-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="d4a22-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4a22-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4a22-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d4a22-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d4a22-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4a22-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d4a22-117">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-117">Creates a subnet configuration.</span></span> <span data-ttu-id="d4a22-118">Cette configuration est utilisée avec le processus de création du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="d4a22-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="d4a22-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d4a22-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d4a22-120">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d4a22-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="d4a22-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d4a22-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d4a22-122">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d4a22-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="d4a22-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="d4a22-124">Crée une configuration IP frontale pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="d4a22-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d4a22-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="d4a22-126">Crée une configuration de pool d’adresses principales pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="d4a22-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d4a22-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="d4a22-128">Crée une configuration de sonde pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="d4a22-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d4a22-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="d4a22-130">Crée une configuration de règle pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="d4a22-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d4a22-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="d4a22-132">Crée une configuration de règle NAT entrante pour un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="d4a22-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="d4a22-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="d4a22-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="d4a22-134">Crée un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="d4a22-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="d4a22-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d4a22-136">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="d4a22-137">Cette configuration est utilisé toocreate une règle de groupe de sécurité réseau lors de la création de hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="d4a22-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d4a22-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d4a22-139">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="d4a22-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d4a22-141">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-141">Gets subnet information.</span></span> <span data-ttu-id="d4a22-142">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="d4a22-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d4a22-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d4a22-144">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="d4a22-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="d4a22-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d4a22-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d4a22-146">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4a22-146">Creates a VM configuration.</span></span> <span data-ttu-id="d4a22-147">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="d4a22-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d4a22-148">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4a22-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d4a22-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d4a22-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d4a22-150">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d4a22-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="d4a22-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4a22-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d4a22-152">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="d4a22-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4a22-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4a22-153">Next steps</span></span>

<span data-ttu-id="d4a22-154">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4a22-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d4a22-155">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4a22-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
