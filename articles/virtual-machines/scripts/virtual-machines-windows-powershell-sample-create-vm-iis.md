---
title: aaaAzure exemple de Script PowerShell - IIS | Documents Microsoft
description: "Exemple de script Azure PowerShell - IIS"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 707563e3cce32e667c41ab9ec2392c8f12ef116c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="20edc-103">Créer une machine virtuelle IIS avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="20edc-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="20edc-104">Ce script crée une Machine virtuelle de Azure exécutant Windows Server 2016 et utilise ensuite tooinstall d’Extension de Script personnalisé Machine virtuelle Azure hello IIS.</span><span class="sxs-lookup"><span data-stu-id="20edc-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="20edc-105">Après avoir exécuté le script de hello, vous pouvez accéder hello IIS site Web par défaut hello adresse IP publique de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="20edc-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="20edc-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="20edc-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="20edc-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="20edc-107">Clean up deployment</span></span> 

<span data-ttu-id="20edc-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="20edc-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="20edc-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="20edc-109">Script explanation</span></span>

<span data-ttu-id="20edc-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="20edc-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="20edc-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="20edc-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="20edc-112">Commande</span><span class="sxs-lookup"><span data-stu-id="20edc-112">Command</span></span> | <span data-ttu-id="20edc-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="20edc-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20edc-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20edc-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="20edc-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="20edc-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20edc-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="20edc-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="20edc-117">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-117">Creates a subnet configuration.</span></span> <span data-ttu-id="20edc-118">Cette configuration est utilisée avec le processus de création du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="20edc-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="20edc-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="20edc-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="20edc-120">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="20edc-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="20edc-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="20edc-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="20edc-122">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="20edc-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="20edc-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="20edc-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="20edc-124">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="20edc-125">Cette configuration est utilisé toocreate une règle de groupe de sécurité réseau lors de la création de hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="20edc-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="20edc-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="20edc-127">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="20edc-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="20edc-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="20edc-129">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-129">Gets subnet information.</span></span> <span data-ttu-id="20edc-130">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="20edc-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="20edc-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="20edc-132">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="20edc-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="20edc-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="20edc-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="20edc-134">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="20edc-134">Creates a VM configuration.</span></span> <span data-ttu-id="20edc-135">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="20edc-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="20edc-136">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="20edc-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="20edc-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="20edc-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="20edc-138">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="20edc-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="20edc-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="20edc-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="20edc-140">Ajouter un ordinateur virtuel de machine virtuelle extension toohello.</span><span class="sxs-lookup"><span data-stu-id="20edc-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="20edc-141">Dans cet exemple, extension de script personnalisé hello est utilisé tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="20edc-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="20edc-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20edc-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="20edc-143">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="20edc-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20edc-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="20edc-144">Next steps</span></span>

<span data-ttu-id="20edc-145">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20edc-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="20edc-146">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20edc-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>