---
title: "Exemple de script Azure PowerShell - Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation | Documents Microsoft"
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
ms.openlocfilehash: ec532811e94647c8a04b9faf9474f6749969f83e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="877bd-103">Créer une machine virtuelle en utilisant un disque de système d’exploitation géré existant avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="877bd-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="877bd-104">Ce script crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="877bd-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="877bd-105">Utilisez ce script dans des scénarios précédent :</span><span class="sxs-lookup"><span data-stu-id="877bd-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="877bd-106">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été copié d’un disque géré dans un autre abonnement</span><span class="sxs-lookup"><span data-stu-id="877bd-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="877bd-107">Créer une machine virtuelle à partir d’un disque géré existant qui a été créé à partir d’un fichier de disque dur virtuel spécialisé</span><span class="sxs-lookup"><span data-stu-id="877bd-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="877bd-108">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été créé à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="877bd-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="877bd-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="877bd-109">Sample script</span></span>

<span data-ttu-id="877bd-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Créer une machine virtuelle à partir d’une capture instantanée")]</span><span class="sxs-lookup"><span data-stu-id="877bd-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="877bd-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="877bd-111">Clean up deployment</span></span> 

<span data-ttu-id="877bd-112">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="877bd-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="877bd-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="877bd-113">Script explanation</span></span>

<span data-ttu-id="877bd-114">Ce script utilise les commandes suivantes pour obtenir des propriétés de disque géré, attacher un disque géré à une nouvelle machine virtuelle et créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="877bd-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="877bd-115">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="877bd-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="877bd-116">Commande</span><span class="sxs-lookup"><span data-stu-id="877bd-116">Command</span></span> | <span data-ttu-id="877bd-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="877bd-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="877bd-118">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="877bd-118">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="877bd-119">Obtient l’objet disque sur la base du nom et du groupe de ressources d’un disque.</span><span class="sxs-lookup"><span data-stu-id="877bd-119">Gets disk object based on the name and the resource group of a disk.</span></span> <span data-ttu-id="877bd-120">La propriété Id de l’objet disque retourné est utilisée pour attacher le disque à une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="877bd-120">Id property of the returned disk object is used to attach the disk to a new VM</span></span> |
| [<span data-ttu-id="877bd-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="877bd-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="877bd-122">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="877bd-122">Creates a VM configuration.</span></span> <span data-ttu-id="877bd-123">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="877bd-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="877bd-124">La configuration est utilisée lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="877bd-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="877bd-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="877bd-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="877bd-126">Attache un disque géré en utilisant la propriété Id du disque en tant que disque de système d’exploitation pour une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="877bd-126">Attaches a managed disk using the Id property of the disk as OS disk to a new virtual machine</span></span> |
| [<span data-ttu-id="877bd-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="877bd-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="877bd-128">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="877bd-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="877bd-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="877bd-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="877bd-130">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="877bd-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="877bd-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="877bd-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="877bd-132">Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="877bd-132">Create a virtual machine.</span></span> |
|[<span data-ttu-id="877bd-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="877bd-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="877bd-134">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="877bd-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="877bd-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="877bd-135">Next steps</span></span>

<span data-ttu-id="877bd-136">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="877bd-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="877bd-137">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="877bd-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>