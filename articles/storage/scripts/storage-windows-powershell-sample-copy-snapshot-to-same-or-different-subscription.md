---
title: "aaaAzure exemple de Script PowerShell - instantané copie (déplacer) d’un disque géré toosame ou un autre abonnement | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - instantané copie (déplacer) d’un disque géré toosame ou un autre abonnement"
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
ms.openlocfilehash: 7a3565356f13cb93759dec7ef9d0357e04c3410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="c02b8-103">Copier une capture instantanée de disque géré dans un abonnement identique ou différent avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="c02b8-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="c02b8-104">Ce script crée une copie d’un instantané Bonjour même abonnement même ou différents.</span><span class="sxs-lookup"><span data-stu-id="c02b8-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="c02b8-105">Utilisez cette toomove script un abonnement de toodifferent instantané pour la rétention des données.</span><span class="sxs-lookup"><span data-stu-id="c02b8-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="c02b8-106">Le stockage de captures instantanées dans un autre abonnement vous protège contre la suppression accidentelle de captures instantanées dans votre abonnement principal.</span><span class="sxs-lookup"><span data-stu-id="c02b8-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c02b8-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c02b8-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="c02b8-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c02b8-108">Script explanation</span></span>

<span data-ttu-id="c02b8-109">Ce script utilise suivante commandes toocreate un instantané à l’aide d’abonnement cible hello hello Id d’instantané de source de hello.</span><span class="sxs-lookup"><span data-stu-id="c02b8-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="c02b8-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c02b8-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c02b8-111">Commande</span><span class="sxs-lookup"><span data-stu-id="c02b8-111">Command</span></span> | <span data-ttu-id="c02b8-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="c02b8-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c02b8-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="c02b8-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="c02b8-114">Crée une configuration de capture instantanée, utilisée pour la création de captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="c02b8-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="c02b8-115">Il inclut hello Id de ressource de capture instantanée de hello parent et l’emplacement qui est identique à l’instantané de hello parent.</span><span class="sxs-lookup"><span data-stu-id="c02b8-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="c02b8-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="c02b8-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="c02b8-117">Crée une capture instantanée à partir de la configuration de capture instantanée, du nom de capture instantanée et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="c02b8-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c02b8-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c02b8-118">Next steps</span></span>

[<span data-ttu-id="c02b8-119">Créer une machine virtuelle à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="c02b8-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="c02b8-120">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c02b8-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c02b8-121">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c02b8-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
