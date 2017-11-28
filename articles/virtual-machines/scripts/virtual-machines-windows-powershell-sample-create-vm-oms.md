---
title: Exemple de script PowerShell - OMS | Microsoft Docs
description: "Exemple de script Azure PowerShell - OMS"
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="2297c-103">Création d’une machine virtuelle surveillée par Operations Management Suite avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="2297c-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="2297c-104">Ce script crée une machine virtuelle Azure, installe l’agent Operations Management Suite (OMS) et inscrit le système avec un espace de nom OMS.</span><span class="sxs-lookup"><span data-stu-id="2297c-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="2297c-105">Une fois le script exécuté, la machine virtuelle est visible dans la console OMS.</span><span class="sxs-lookup"><span data-stu-id="2297c-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="2297c-106">Enfin, vous devez mettre à jour l’ID de l’espace de travail OMS et la clé d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="2297c-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2297c-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="2297c-107">Sample script</span></span>

<span data-ttu-id="2297c-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Créer une machine virtuelle OMS")]</span><span class="sxs-lookup"><span data-stu-id="2297c-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2297c-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="2297c-109">Clean up deployment</span></span> 

<span data-ttu-id="2297c-110">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="2297c-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2297c-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="2297c-111">Script explanation</span></span>

<span data-ttu-id="2297c-112">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="2297c-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="2297c-113">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="2297c-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2297c-114">Commande</span><span class="sxs-lookup"><span data-stu-id="2297c-114">Command</span></span> | <span data-ttu-id="2297c-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="2297c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2297c-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2297c-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2297c-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="2297c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2297c-118">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2297c-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="2297c-119">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-119">Creates a subnet configuration.</span></span> <span data-ttu-id="2297c-120">Cette configuration est utilisée avec le processus de création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2297c-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="2297c-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="2297c-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="2297c-122">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2297c-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="2297c-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="2297c-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="2297c-124">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="2297c-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="2297c-125">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="2297c-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="2297c-126">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="2297c-127">Cette configuration est utilisée pour créer une règle de groupe de sécurité réseau lors de la création d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="2297c-128">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="2297c-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="2297c-129">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="2297c-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="2297c-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="2297c-131">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-131">Gets subnet information.</span></span> <span data-ttu-id="2297c-132">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="2297c-133">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2297c-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="2297c-134">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="2297c-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="2297c-135">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="2297c-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="2297c-136">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2297c-136">Creates a VM configuration.</span></span> <span data-ttu-id="2297c-137">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="2297c-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="2297c-138">La configuration est utilisée lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2297c-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="2297c-139">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2297c-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="2297c-140">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2297c-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="2297c-141">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="2297c-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="2297c-142">Ajoutez une extension de machine virtuelle à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2297c-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="2297c-143">Dans ce cas, l’extension de l’agent Operations Management Suite est utilisée pour installer l’agent OMS et inscrire la machine virtuelle dans un espace de nom OMS.</span><span class="sxs-lookup"><span data-stu-id="2297c-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="2297c-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2297c-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2297c-145">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="2297c-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2297c-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2297c-146">Next steps</span></span>

<span data-ttu-id="2297c-147">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2297c-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2297c-148">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2297c-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
