---
title: "aaaAzure instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans autre région - exemple de Script PowerShell | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans la même région différente"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="daca1-103">Exportation ou copier des instantanés gérés en tant que compte de stockage de disque dur virtuel tooa dans autre région avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="daca1-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="daca1-104">Ce script exporte un compte de stockage géré instantané tooa dans autre région.</span><span class="sxs-lookup"><span data-stu-id="daca1-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="daca1-105">Il génère d’abord hello URI SAS d’instantané de hello et utilise ensuite toocopy il compte de stockage tooa dans autre région.</span><span class="sxs-lookup"><span data-stu-id="daca1-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="daca1-106">Utilisez cette sauvegarde toomaintain de script de vos disques gérés dans autre région pour la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="daca1-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="daca1-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="daca1-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="daca1-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="daca1-108">Script explanation</span></span>

<span data-ttu-id="daca1-109">Ce script utilise suivante commandes toogenerate URI SAS pour un Bonjour de capture instantanée ni copie managé d’instantané tooa compte de stockage à l’aide de l’URI SAS.</span><span class="sxs-lookup"><span data-stu-id="daca1-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="daca1-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="daca1-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="daca1-111">Commande</span><span class="sxs-lookup"><span data-stu-id="daca1-111">Command</span></span> | <span data-ttu-id="daca1-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="daca1-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="daca1-113">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="daca1-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="daca1-114">Génère l’URI SAS pour un instantané est utilisé toocopy il compte de stockage tooa.</span><span class="sxs-lookup"><span data-stu-id="daca1-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="daca1-115">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="daca1-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="daca1-116">Crée un contexte de compte de stockage à l’aide de la clé et le nom du compte hello.</span><span class="sxs-lookup"><span data-stu-id="daca1-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="daca1-117">Ce contexte peut être tooperform utilisé les opérations de lecture/écriture sur le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="daca1-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="daca1-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="daca1-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="daca1-119">Copies hello disque dur virtuel sous-jacent d’un compte de stockage tooa instantané</span><span class="sxs-lookup"><span data-stu-id="daca1-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="daca1-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daca1-120">Next steps</span></span>

[<span data-ttu-id="daca1-121">Créer un disque managé à partir d’un VHD</span><span class="sxs-lookup"><span data-stu-id="daca1-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="daca1-122">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="daca1-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="daca1-123">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="daca1-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="daca1-124">Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="daca1-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
