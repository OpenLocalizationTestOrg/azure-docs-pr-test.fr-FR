---
title: "Exemple de script Azure PowerShell : Créer un disque géré à partir d’une capture instantanée | Microsoft Docs"
description: "Exemple de script Azure PowerShell : Créer un disque géré à partir d’une capture instantanée"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: b475516694d120b7ea05d0892b6789710eec171e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="ab49d-103">Créer un disque géré à partir d’une capture instantanée avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab49d-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="ab49d-104">Ce script crée un disque géré à partir d’une capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="ab49d-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="ab49d-105">Utilisez-le pour restaurer une machine virtuelle à partir de captures instantanées de disques de système d’exploitation et de données.</span><span class="sxs-lookup"><span data-stu-id="ab49d-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="ab49d-106">Créez des disques managés de système d’exploitation et de données à partir des captures instantanées respectives, puis créez une machine virtuelle en joignant les disques managés.</span><span class="sxs-lookup"><span data-stu-id="ab49d-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="ab49d-107">Vous pouvez également restaurer les disques de données d’une machine virtuelle existante en joignant les disques de données créés à partir de captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="ab49d-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ab49d-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ab49d-108">Sample script</span></span>

<span data-ttu-id="ab49d-109">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Créer un disque managé à partir d’une capture instantanée")]</span><span class="sxs-lookup"><span data-stu-id="ab49d-109">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="ab49d-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ab49d-110">Script explanation</span></span>

<span data-ttu-id="ab49d-111">Ce script a recours aux commandes suivantes pour créer un disque managé à partir d’une capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="ab49d-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="ab49d-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="ab49d-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ab49d-113">Commande</span><span class="sxs-lookup"><span data-stu-id="ab49d-113">Command</span></span> | <span data-ttu-id="ab49d-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="ab49d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab49d-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="ab49d-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="ab49d-116">Obtient les propriétés de capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="ab49d-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="ab49d-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="ab49d-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="ab49d-118">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="ab49d-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="ab49d-119">Il inclut l’ID de ressource de la capture instantanée parente, un emplacement identique à l’emplacement de la capture instantanée parente, et le type de stockage.</span><span class="sxs-lookup"><span data-stu-id="ab49d-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="ab49d-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="ab49d-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="ab49d-121">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="ab49d-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ab49d-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab49d-122">Next steps</span></span>

[<span data-ttu-id="ab49d-123">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="ab49d-123">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="ab49d-124">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ab49d-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ab49d-125">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab49d-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>