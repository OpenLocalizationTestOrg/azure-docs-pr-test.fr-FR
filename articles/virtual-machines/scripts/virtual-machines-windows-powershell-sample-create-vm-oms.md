---
title: aaaAzure exemple de Script PowerShell - OMS | Documents Microsoft
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
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="4c544-103">Création d’une machine virtuelle surveillée par Operations Management Suite avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c544-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="4c544-104">Ce script crée une Machine virtuelle Azure installe l’agent Operations Management Suite (OMS) de hello et inscrit système hello avec un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="4c544-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="4c544-105">Une fois le script de hello a exécuté, hello virtuels seront visibles dans la console OMS hello.</span><span class="sxs-lookup"><span data-stu-id="4c544-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="4c544-106">En outre, vous devez tooupdate hello OMS espace de travail espace de travail et ID de clé.</span><span class="sxs-lookup"><span data-stu-id="4c544-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4c544-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="4c544-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4c544-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="4c544-108">Clean up deployment</span></span> 

<span data-ttu-id="4c544-109">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="4c544-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4c544-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="4c544-110">Script explanation</span></span>

<span data-ttu-id="4c544-111">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="4c544-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="4c544-112">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="4c544-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4c544-113">Commande</span><span class="sxs-lookup"><span data-stu-id="4c544-113">Command</span></span> | <span data-ttu-id="4c544-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="4c544-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4c544-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4c544-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4c544-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="4c544-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4c544-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4c544-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4c544-118">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-118">Creates a subnet configuration.</span></span> <span data-ttu-id="4c544-119">Cette configuration est utilisée avec le processus de création du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="4c544-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="4c544-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4c544-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="4c544-121">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4c544-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="4c544-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4c544-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4c544-123">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="4c544-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4c544-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4c544-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="4c544-125">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="4c544-126">Cette configuration est utilisé toocreate une règle de groupe de sécurité réseau lors de la création de hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="4c544-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="4c544-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="4c544-128">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="4c544-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4c544-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4c544-130">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-130">Gets subnet information.</span></span> <span data-ttu-id="4c544-131">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="4c544-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4c544-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4c544-133">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="4c544-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="4c544-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4c544-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4c544-135">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4c544-135">Creates a VM configuration.</span></span> <span data-ttu-id="4c544-136">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="4c544-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4c544-137">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4c544-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4c544-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4c544-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4c544-139">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4c544-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="4c544-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="4c544-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="4c544-141">Ajouter un ordinateur virtuel de machine virtuelle extension toohello.</span><span class="sxs-lookup"><span data-stu-id="4c544-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="4c544-142">Dans ce cas, hello extension de l’agent Operations Management Suite est utilisé tooinstall hello OMS agent et inscrire hello machine virtuelle dans un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="4c544-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="4c544-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4c544-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4c544-144">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="4c544-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4c544-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c544-145">Next steps</span></span>

<span data-ttu-id="4c544-146">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c544-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4c544-147">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c544-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
