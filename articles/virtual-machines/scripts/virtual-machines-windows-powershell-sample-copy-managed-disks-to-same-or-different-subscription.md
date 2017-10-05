---
title: "Exemple de script Azure PowerShell : Copier (déplacer) des disques gérés vers un abonnement identique ou différent | Microsoft Docs"
description: "Exemple de script Azure PowerShell : Copier (déplacer) des disques gérés vers un abonnement identique ou différent"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 75beb35dc19fa530d9b2c19aed6040f74afafbc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-in-the-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="87cc0-103">Copier des disques gérés dans un abonnement unique ou différent avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="87cc0-103">Copy managed disks in the same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="87cc0-104">Ce script crée la copie d’un disque géré existant dans le même abonnement ou un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="87cc0-104">This script creates a copy of an existing managed disk in the same subscription or different subscription.</span></span> <span data-ttu-id="87cc0-105">Le disque est créé dans la même région que le disque géré parent.</span><span class="sxs-lookup"><span data-stu-id="87cc0-105">The new disk is created in the same region as the parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="87cc0-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="87cc0-106">Sample script</span></span>

<span data-ttu-id="87cc0-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copier un disque managé")]</span><span class="sxs-lookup"><span data-stu-id="87cc0-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="87cc0-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="87cc0-108">Script explanation</span></span>

<span data-ttu-id="87cc0-109">Ce script utilise les commandes suivantes pour créer un disque géré dans l’abonnement cible à l’aide de l’ID du disque source géré.</span><span class="sxs-lookup"><span data-stu-id="87cc0-109">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="87cc0-110">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="87cc0-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="87cc0-111">Commande</span><span class="sxs-lookup"><span data-stu-id="87cc0-111">Command</span></span> | <span data-ttu-id="87cc0-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="87cc0-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="87cc0-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="87cc0-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="87cc0-114">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="87cc0-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="87cc0-115">Elle inclut l’ID de ressource du disque parent et un emplacement identique à l’emplacement du disque parent.</span><span class="sxs-lookup"><span data-stu-id="87cc0-115">It includes the resource Id of the parent disk and location that is same as the location of parent disk.</span></span>  |
| [<span data-ttu-id="87cc0-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="87cc0-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="87cc0-117">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="87cc0-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="87cc0-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87cc0-118">Next steps</span></span>

[<span data-ttu-id="87cc0-119">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="87cc0-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="87cc0-120">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87cc0-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="87cc0-121">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87cc0-121">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>