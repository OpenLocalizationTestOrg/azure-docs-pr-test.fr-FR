---
title: "aaaAzure exemple de Script PowerShell - créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="63cff-103">Créer une machine virtuelle en utilisant un disque de système d’exploitation géré existant avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="63cff-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="63cff-104">Ce script crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="63cff-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="63cff-105">Utilisez ce script dans des scénarios précédent :</span><span class="sxs-lookup"><span data-stu-id="63cff-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="63cff-106">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été copié d’un disque géré dans un autre abonnement</span><span class="sxs-lookup"><span data-stu-id="63cff-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="63cff-107">Créer une machine virtuelle à partir d’un disque géré existant qui a été créé à partir d’un fichier de disque dur virtuel spécialisé</span><span class="sxs-lookup"><span data-stu-id="63cff-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="63cff-108">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été créé à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="63cff-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="63cff-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="63cff-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="63cff-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="63cff-110">Clean up deployment</span></span> 

<span data-ttu-id="63cff-111">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="63cff-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="63cff-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="63cff-112">Script explanation</span></span>

<span data-ttu-id="63cff-113">Ce script utilise hello commandes tooget géré disque propriétés suivantes, attacher un disque géré de tooa nouvelle machine virtuelle et créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="63cff-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="63cff-114">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="63cff-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="63cff-115">Commande</span><span class="sxs-lookup"><span data-stu-id="63cff-115">Command</span></span> | <span data-ttu-id="63cff-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="63cff-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="63cff-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="63cff-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="63cff-118">Obtient l’objet de disque basé sur le nom de hello et le groupe de ressources hello d’un disque.</span><span class="sxs-lookup"><span data-stu-id="63cff-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="63cff-119">Propriété d’ID de hello retourné objet de disque est utilisé tooattach hello disque tooa nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="63cff-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="63cff-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="63cff-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="63cff-121">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="63cff-121">Creates a VM configuration.</span></span> <span data-ttu-id="63cff-122">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="63cff-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="63cff-123">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="63cff-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="63cff-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="63cff-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="63cff-125">Attache un disque géré à l’aide de la propriété d’Id hello du disque de hello en tant que système d’exploitation disque tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="63cff-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="63cff-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="63cff-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="63cff-127">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="63cff-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="63cff-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="63cff-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="63cff-129">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="63cff-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="63cff-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="63cff-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="63cff-131">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="63cff-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="63cff-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="63cff-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="63cff-133">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="63cff-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="63cff-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63cff-134">Next steps</span></span>

<span data-ttu-id="63cff-135">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63cff-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="63cff-136">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63cff-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
