---
title: "aaaAzure exemple de Script PowerShell - créer un disque géré à partir d’un instantané | Documents Microsoft"
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="b9b0e-103">Créer un disque géré à partir d’une capture instantanée avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9b0e-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="b9b0e-104">Ce script crée un disque managé à partir d’une capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="b9b0e-105">Utiliser toorestore une machine virtuelle à partir de clichés instantanés des disques du système d’exploitation et des données.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="b9b0e-106">Créez des disques managés de système d’exploitation et de données à partir des captures instantanées respectives, puis créez une machine virtuelle en joignant les disques managés.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="b9b0e-107">Vous pouvez également restaurer les disques de données d’une machine virtuelle existante en joignant les disques de données créés à partir de captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b9b0e-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b9b0e-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="b9b0e-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b9b0e-109">Script explanation</span></span>

<span data-ttu-id="b9b0e-110">Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un instantané.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="b9b0e-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b9b0e-112">Commande</span><span class="sxs-lookup"><span data-stu-id="b9b0e-112">Command</span></span> | <span data-ttu-id="b9b0e-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="b9b0e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b9b0e-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="b9b0e-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="b9b0e-115">Obtient les propriétés de capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="b9b0e-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="b9b0e-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="b9b0e-117">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="b9b0e-118">Il inclut des Id d’instantané de parent hello, emplacement qui est identique à l’emplacement de hello du type de stockage des instantanés et hello parent de la ressource hello.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="b9b0e-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="b9b0e-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="b9b0e-120">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="b9b0e-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b9b0e-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9b0e-121">Next steps</span></span>

[<span data-ttu-id="b9b0e-122">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="b9b0e-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="b9b0e-123">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b9b0e-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b9b0e-124">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9b0e-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
