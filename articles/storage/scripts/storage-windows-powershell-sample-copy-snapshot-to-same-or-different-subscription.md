---
title: "Exemple de script Azure PowerShell : Copier (déplacer) la capture instantanée d’un disque géré vers un abonnement identique ou différent | Microsoft Docs"
description: "Exemple de script Azure PowerShell : Copier (déplacer) la capture instantanée d’un disque géré vers un abonnement identique ou différent"
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
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="4c338-103">Copier une capture instantanée de disque géré dans un abonnement identique ou différent avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c338-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="4c338-104">Ce script crée la copie d’une capture instantanée dans le même abonnement ou un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c338-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="4c338-105">Utilisez ce script pour déplacer une capture instantanée vers un autre abonnement dans une optique de rétention des données.</span><span class="sxs-lookup"><span data-stu-id="4c338-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="4c338-106">Le stockage de captures instantanées dans un autre abonnement vous protège contre la suppression accidentelle de captures instantanées dans votre abonnement principal.</span><span class="sxs-lookup"><span data-stu-id="4c338-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4c338-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="4c338-107">Sample script</span></span>

<span data-ttu-id="4c338-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copier une capture instantanée")]</span><span class="sxs-lookup"><span data-stu-id="4c338-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="4c338-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="4c338-109">Script explanation</span></span>

<span data-ttu-id="4c338-110">Ce script utilise les commandes suivantes pour créer une capture instantanée dans l’abonnement cible à l’aide de l’ID de la capture instantanée source.</span><span class="sxs-lookup"><span data-stu-id="4c338-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="4c338-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="4c338-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4c338-112">Commande</span><span class="sxs-lookup"><span data-stu-id="4c338-112">Command</span></span> | <span data-ttu-id="4c338-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="4c338-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4c338-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="4c338-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="4c338-115">Crée une configuration de capture instantanée, utilisée pour la création de captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="4c338-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="4c338-116">Elle inclut l’ID de ressource de la capture instantanée parente et un emplacement identique à l’emplacement de la capture instantanée parente.</span><span class="sxs-lookup"><span data-stu-id="4c338-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="4c338-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="4c338-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="4c338-118">Crée une capture instantanée à partir de la configuration de capture instantanée, du nom de capture instantanée et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="4c338-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4c338-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c338-119">Next steps</span></span>

[<span data-ttu-id="4c338-120">Créer une machine virtuelle à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="4c338-120">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4c338-121">Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c338-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4c338-122">Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c338-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>