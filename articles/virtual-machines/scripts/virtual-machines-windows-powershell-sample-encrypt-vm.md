---
title: aaaAzure exemple de Script PowerShell - chiffrer une machine virtuelle Windows | Documents Microsoft
description: "Exemple de script Azure PowerShell - Chiffrement d’une machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="06832-103">Chiffrement d’une machine virtuelle Windows avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="06832-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="06832-104">Ce script crée une solution Key Vault sécurisée, des clés de chiffrement, un principal de service Azure Active Directory et une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="06832-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="06832-105">Hello machine virtuelle est ensuite chiffrée à l’aide de la clé de chiffrement hello coffre de clés et les informations d’identification du principal de service.</span><span class="sxs-lookup"><span data-stu-id="06832-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="06832-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="06832-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="06832-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="06832-107">Clean up deployment</span></span> 

<span data-ttu-id="06832-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="06832-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="06832-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="06832-109">Script explanation</span></span>

<span data-ttu-id="06832-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="06832-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="06832-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="06832-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="06832-112">Commande</span><span class="sxs-lookup"><span data-stu-id="06832-112">Command</span></span> | <span data-ttu-id="06832-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="06832-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06832-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06832-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="06832-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="06832-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06832-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="06832-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="06832-117">Crée une coffre de clés Azure toostore sécuriser les données telles que des clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="06832-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="06832-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="06832-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="06832-119">Crée une clé de chiffrement dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="06832-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="06832-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="06832-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="06832-121">Crée un service Azure Active Directory toosecurely principal authentifier et contrôler les clés d’accès tooencryption.</span><span class="sxs-lookup"><span data-stu-id="06832-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="06832-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="06832-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="06832-123">Définit des autorisations sur hello coffre de clés toogrant hello service principal tooencryption clés d’accès.</span><span class="sxs-lookup"><span data-stu-id="06832-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="06832-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06832-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06832-125">Crée une configuration de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-125">Creates a subnet configuration.</span></span> <span data-ttu-id="06832-126">Cette configuration est utilisée avec le processus de création du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="06832-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="06832-127">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="06832-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="06832-128">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="06832-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="06832-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="06832-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="06832-130">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="06832-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="06832-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="06832-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="06832-132">Crée une configuration de règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="06832-133">Cette configuration est utilisé toocreate une règle de groupe de sécurité réseau lors de la création de hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="06832-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="06832-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="06832-135">Crée un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="06832-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06832-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06832-137">Obtient les informations du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-137">Gets subnet information.</span></span> <span data-ttu-id="06832-138">Ces informations sont utilisées lors de la création d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="06832-139">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="06832-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="06832-140">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="06832-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="06832-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="06832-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="06832-142">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="06832-142">Creates a VM configuration.</span></span> <span data-ttu-id="06832-143">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="06832-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="06832-144">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="06832-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="06832-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="06832-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="06832-146">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="06832-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="06832-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="06832-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="06832-148">Obtient les informations requises sur le coffre de clés de hello</span><span class="sxs-lookup"><span data-stu-id="06832-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="06832-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="06832-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="06832-150">Active le chiffrement sur une machine virtuelle à l’aide des informations d’identification de hello service principal et la clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="06832-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="06832-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="06832-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="06832-152">Montre l’état hello Hello processus de chiffrement de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="06832-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="06832-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06832-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="06832-154">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="06832-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06832-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06832-155">Next steps</span></span>

<span data-ttu-id="06832-156">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06832-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="06832-157">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06832-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
