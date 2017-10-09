---
title: "aaaAzure exemple de Script PowerShell - copie (déplacer) géré toosame de disques ou d’un autre abonnement | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - toosame de disques géré de copie (déplacer) ou autre abonnement"
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
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="919eb-103">Copie géré des disques hello même abonnement ou autre avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="919eb-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="919eb-104">Ce script crée une copie d’un disque géré existant Bonjour même abonnement ou autre.</span><span class="sxs-lookup"><span data-stu-id="919eb-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="919eb-105">Hello nouveau disque est créé dans hello même région que le parent de hello gérés disque.</span><span class="sxs-lookup"><span data-stu-id="919eb-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="919eb-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="919eb-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="919eb-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="919eb-107">Script explanation</span></span>

<span data-ttu-id="919eb-108">Ce script utilise suivante commandes toocreate un nouveau disque géré à l’aide d’abonnement cible hello hello Id de source de hello gérés disque.</span><span class="sxs-lookup"><span data-stu-id="919eb-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="919eb-109">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="919eb-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="919eb-110">Commande</span><span class="sxs-lookup"><span data-stu-id="919eb-110">Command</span></span> | <span data-ttu-id="919eb-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="919eb-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="919eb-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="919eb-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="919eb-113">Crée une configuration de disque qui est utilisée pour la création du disque.</span><span class="sxs-lookup"><span data-stu-id="919eb-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="919eb-114">Il inclut hello Id de ressource de disque parent de hello et l’emplacement qui est identique à l’emplacement de hello du disque parent.</span><span class="sxs-lookup"><span data-stu-id="919eb-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="919eb-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="919eb-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="919eb-116">Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="919eb-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="919eb-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="919eb-117">Next steps</span></span>

[<span data-ttu-id="919eb-118">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="919eb-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="919eb-119">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="919eb-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="919eb-120">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="919eb-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
