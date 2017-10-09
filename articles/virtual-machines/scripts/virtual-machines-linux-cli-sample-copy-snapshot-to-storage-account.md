---
title: "aaaAzure exemple de Script CLI - instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans autre région | Documents Microsoft"
description: "Exemple de Script CLI Azure - instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans l’abonnement identique ou différent"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="80973-103">Exportation ou copier des instantanés gérés en tant que compte de stockage de disque dur virtuel tooa dans autre région avec l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="80973-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="80973-104">Ce script exporte un compte de stockage géré instantané tooa dans autre région.</span><span class="sxs-lookup"><span data-stu-id="80973-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="80973-105">Il génère d’abord hello URI SAS d’instantané de hello et utilise ensuite toocopy il compte de stockage tooa dans autre région.</span><span class="sxs-lookup"><span data-stu-id="80973-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="80973-106">Utilisez cette sauvegarde toomaintain de script de vos disques gérés dans autre région pour la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="80973-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="80973-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="80973-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="80973-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="80973-108">Script explanation</span></span>

<span data-ttu-id="80973-109">Ce script utilise suivante commandes toogenerate URI SAS pour un Bonjour de capture instantanée ni copie managé d’instantané tooa compte de stockage à l’aide de l’URI SAS.</span><span class="sxs-lookup"><span data-stu-id="80973-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="80973-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="80973-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="80973-111">Commande</span><span class="sxs-lookup"><span data-stu-id="80973-111">Command</span></span> | <span data-ttu-id="80973-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="80973-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80973-113">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="80973-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="80973-114">Génère les associations de sécurité en lecture seule qui sont utilisé toocopy sous-jacent du compte de stockage de tooa de fichier de disque dur virtuel ou le télécharger tooon local</span><span class="sxs-lookup"><span data-stu-id="80973-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="80973-115">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="80973-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="80973-116">Copie un objet blob de façon asynchrone à partir d’un tooanother de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="80973-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80973-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80973-117">Next steps</span></span>

[<span data-ttu-id="80973-118">Créer un disque managé à partir d’un VHD</span><span class="sxs-lookup"><span data-stu-id="80973-118">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="80973-119">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="80973-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="80973-120">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80973-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="80973-121">Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80973-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
