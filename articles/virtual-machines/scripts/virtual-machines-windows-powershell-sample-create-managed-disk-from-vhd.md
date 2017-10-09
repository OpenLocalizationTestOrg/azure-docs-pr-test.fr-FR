---
title: "aaaAzure exemple de Script PowerShell - créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans l’abonnement identiques ou différent | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou dans un abonnement différent"
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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="4bee2-103">Créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou dans un abonnement différent avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bee2-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="4bee2-104">Ce script crée un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou un abonnement différent.</span><span class="sxs-lookup"><span data-stu-id="4bee2-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="4bee2-105">Utilisez cette tooimport script un spécialisé toocreate (pas généralisé/préparée avec Sysprep) disque dur virtuel toomanaged du système d’exploitation disque un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="4bee2-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="4bee2-106">Utilisez-le également pour tooimport un disque de données toomanaged données disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="4bee2-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="4bee2-107">Ne créez pas plusieurs disques gérés identiques à partir d’un fichier de disque dur virtuel dans un court laps de temps.</span><span class="sxs-lookup"><span data-stu-id="4bee2-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="4bee2-108">toocreate des disques gérés à partir d’un fichier de disque dur virtuel, instantané d’objet blob du fichier de disque dur virtuel hello est créé et il est utilisé toocreate géré disques.</span><span class="sxs-lookup"><span data-stu-id="4bee2-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="4bee2-109">Instantané d’objet seul blob peut être créé dans une minute qui provoque l’échec de la création de disque toothrottling échéance.</span><span class="sxs-lookup"><span data-stu-id="4bee2-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="4bee2-110">tooavoid cette limitation, créer un [instantané managé à partir du fichier de disque dur virtuel hello](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) , puis utilisez hello gérés instantané toocreate plusieurs disques gérés dans peu de temps.</span><span class="sxs-lookup"><span data-stu-id="4bee2-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4bee2-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="4bee2-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="4bee2-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="4bee2-112">Script explanation</span></span>

<span data-ttu-id="4bee2-113">Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un disque dur virtuel dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="4bee2-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="4bee2-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="4bee2-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4bee2-115">Commande</span><span class="sxs-lookup"><span data-stu-id="4bee2-115">Command</span></span> | <span data-ttu-id="4bee2-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="4bee2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4bee2-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="4bee2-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="4bee2-118">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="4bee2-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="4bee2-119">Il inclut le type de stockage, emplacement, Id de ressource de hello compte de stockage où le disque dur virtuel parent de hello est stocké, URI VHD du disque dur virtuel parent de hello.</span><span class="sxs-lookup"><span data-stu-id="4bee2-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="4bee2-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="4bee2-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="4bee2-121">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="4bee2-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4bee2-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4bee2-122">Next steps</span></span>

[<span data-ttu-id="4bee2-123">Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="4bee2-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4bee2-124">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bee2-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4bee2-125">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bee2-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
