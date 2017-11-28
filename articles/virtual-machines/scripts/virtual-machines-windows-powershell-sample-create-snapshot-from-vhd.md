---
title: "aaaAzure exemple de Script PowerShell - créer un instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques dans peu de temps | Documents Microsoft"
description: "Script Azure PowerShell exemple : création d’un instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques dans peu de temps"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="17782-103">Créer un instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques dans peu de temps avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="17782-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="17782-104">Ce script crée une capture instantanée à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou un abonnement différent.</span><span class="sxs-lookup"><span data-stu-id="17782-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="17782-105">Ce script de tooimport un instantané de tooa de disque dur virtuel (pas généralisé/préparée avec Sysprep) spécialisé et d’utiliser hello instantané toocreate plusieurs disques gérés identiques dans peu de temps.</span><span class="sxs-lookup"><span data-stu-id="17782-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="17782-106">Utilisez-le également pour tooimport un instantané de tooa de disque dur virtuel de données et utilisez hello instantané toocreate plusieurs disques gérés dans peu de temps.</span><span class="sxs-lookup"><span data-stu-id="17782-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="17782-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="17782-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="17782-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="17782-108">Script explanation</span></span>

<span data-ttu-id="17782-109">Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un disque dur virtuel dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="17782-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="17782-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="17782-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="17782-111">Commande</span><span class="sxs-lookup"><span data-stu-id="17782-111">Command</span></span> | <span data-ttu-id="17782-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="17782-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="17782-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="17782-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="17782-114">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="17782-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="17782-115">Il inclut le type de stockage, l’emplacement, Id de ressource de compte de stockage hello stockage de disque dur virtuel parent de hello et URI VHD du disque dur virtuel parent de hello.</span><span class="sxs-lookup"><span data-stu-id="17782-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="17782-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="17782-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="17782-117">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="17782-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="17782-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17782-118">Next steps</span></span>

[<span data-ttu-id="17782-119">Créer un disque géré à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="17782-119">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="17782-120">Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="17782-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="17782-121">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="17782-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="17782-122">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="17782-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
