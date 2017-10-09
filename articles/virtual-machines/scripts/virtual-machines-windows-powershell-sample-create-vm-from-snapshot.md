---
title: "aaaAzure exemple de Script PowerShell - créer une machine virtuelle à partir d’un instantané | Documents Microsoft"
description: "Exemples de script Azure PowerShell - Créer une machine virtuelle à partir d’une capture instantanée"
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
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="acf81-103">Créer une machine virtuelle à partir d’une capture instantanée avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="acf81-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="acf81-104">Ce script crée une machine virtuelle à partir d’une capture instantanée d’un disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="acf81-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="acf81-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="acf81-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="acf81-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="acf81-106">Clean up deployment</span></span> 

<span data-ttu-id="acf81-107">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="acf81-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="acf81-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="acf81-108">Script explanation</span></span>

<span data-ttu-id="acf81-109">Ce script utilise hello suivant les commandes tooget propriétés d’instantané, créer un disque géré à partir de l’instantané et créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="acf81-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="acf81-110">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="acf81-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="acf81-111">Commande</span><span class="sxs-lookup"><span data-stu-id="acf81-111">Command</span></span> | <span data-ttu-id="acf81-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="acf81-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="acf81-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="acf81-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="acf81-114">Obtient une capture instantanée à l’aide du nom de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="acf81-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="acf81-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="acf81-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="acf81-116">Crée une configuration de disque.</span><span class="sxs-lookup"><span data-stu-id="acf81-116">Creates a disk configuration.</span></span> <span data-ttu-id="acf81-117">Cette configuration est utilisée avec le processus de création du disque hello.</span><span class="sxs-lookup"><span data-stu-id="acf81-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="acf81-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="acf81-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="acf81-119">Crée un disque géré.</span><span class="sxs-lookup"><span data-stu-id="acf81-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="acf81-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="acf81-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="acf81-121">Crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="acf81-121">Creates a VM configuration.</span></span> <span data-ttu-id="acf81-122">Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="acf81-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="acf81-123">configuration de Hello est utilisée lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="acf81-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="acf81-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="acf81-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="acf81-125">Attache un disque géré de hello en tant qu’ordinateur virtuel de système d’exploitation disque toohello</span><span class="sxs-lookup"><span data-stu-id="acf81-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="acf81-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="acf81-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="acf81-127">Crée une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="acf81-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="acf81-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="acf81-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="acf81-129">Crée une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="acf81-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="acf81-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="acf81-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="acf81-131">Crée une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="acf81-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="acf81-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="acf81-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="acf81-133">Supprime un groupe de ressources et toutes les ressources contenues.</span><span class="sxs-lookup"><span data-stu-id="acf81-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="acf81-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="acf81-134">Next steps</span></span>

<span data-ttu-id="acf81-135">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="acf81-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="acf81-136">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="acf81-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
