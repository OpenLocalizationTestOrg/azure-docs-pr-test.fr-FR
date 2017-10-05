---
title: "Exemple de script Azure PowerShell - Création d’une capture instantanée à partir d’un disque dur virtuel pour créer rapidement plusieurs disques gérés identiques | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Création d’une capture instantanée à partir d’un disque dur virtuel pour créer rapidement plusieurs disques gérés identiques"
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
ms.openlocfilehash: 02a69abd6c17ce765996379309e22afad82c4e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="5c1a0-103">Création d’une capture instantanée à partir d’un disque dur virtuel pour créer rapidement plusieurs disques gérés identiques avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c1a0-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="5c1a0-104">Ce script crée une capture instantanée à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou un abonnement différent.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="5c1a0-105">Utilisez ce script pour importer un disque dur virtuel spécialisé (non généralisé/préparé avec Sysprep) dans une capture instantanée, puis utilisez la capture instantanée pour créer rapidement plusieurs disques gérés identiques.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="5c1a0-106">Vous pouvez également vous en servir pour importer un disque dur virtuel de données dans une capture instantanée, puis utiliser la capture instantanée pour créer rapidement plusieurs disques gérés.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c1a0-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="5c1a0-107">Sample script</span></span>

<span data-ttu-id="5c1a0-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Créer une capture instantanée à partir d’un disque dur virtuel")]</span><span class="sxs-lookup"><span data-stu-id="5c1a0-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="5c1a0-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="5c1a0-109">Script explanation</span></span>

<span data-ttu-id="5c1a0-110">Ce script a recours aux commandes suivantes pour créer un disque géré à partir d’un disque dur virtuel dans un abonnement différent.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="5c1a0-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c1a0-112">Commande</span><span class="sxs-lookup"><span data-stu-id="5c1a0-112">Command</span></span> | <span data-ttu-id="5c1a0-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="5c1a0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c1a0-114">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="5c1a0-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="5c1a0-115">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="5c1a0-116">Il inclut le type de stockage, l’emplacement, l’ID de ressource du compte de stockage dans lequel le disque dur virtuel parent est stocké et l’URI du disque dur virtuel parent.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="5c1a0-117">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="5c1a0-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="5c1a0-118">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="5c1a0-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c1a0-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c1a0-119">Next steps</span></span>

[<span data-ttu-id="5c1a0-120">Créer un disque géré à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="5c1a0-120">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="5c1a0-121">Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="5c1a0-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5c1a0-122">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c1a0-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5c1a0-123">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c1a0-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>