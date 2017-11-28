---
title: "Exemple de Script CLI - instantané copie (déplacer) d’un disque géré toosame ou un autre abonnement avec l’interface CLI d’aaaAzure | Documents Microsoft"
description: "Exemple de Script CLI Azure - instantané copie (déplacer) d’un disque géré toosame ou un autre abonnement avec l’interface CLI"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="a0d7c-103">Copier la capture instantanée d’un disque géré toosame ou un autre abonnement avec l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="a0d7c-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="a0d7c-104">Ce script copie un instantané d’un disque géré toosame ou un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="a0d7c-105">Utilisez cette toomove script un abonnement aux instantanés toodifferent Bonjour même région que l’instantané de hello parent.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a0d7c-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a0d7c-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="a0d7c-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a0d7c-107">Script explanation</span></span>

<span data-ttu-id="a0d7c-108">Ce script utilise suivante commandes toocreate un instantané à l’aide d’abonnement cible hello hello Id d’instantané de source de hello.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="a0d7c-109">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a0d7c-110">Commande</span><span class="sxs-lookup"><span data-stu-id="a0d7c-110">Command</span></span> | <span data-ttu-id="a0d7c-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="a0d7c-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a0d7c-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="a0d7c-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="a0d7c-113">Obtient toutes les propriétés hello d’un instantané à l’aide du nom de hello et les propriétés du groupe de ressources de l’instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="a0d7c-114">Propriété ID est utilisé toocopy hello instantané toodifferent abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="a0d7c-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="a0d7c-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="a0d7c-116">Copie d’un instantané en créant un instantané à l’aide de l’autre abonnement hello Id et nom du hello instantané parent.</span><span class="sxs-lookup"><span data-stu-id="a0d7c-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="a0d7c-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0d7c-117">Next steps</span></span>

[<span data-ttu-id="a0d7c-118">Créer une machine virtuelle à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="a0d7c-118">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a0d7c-119">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0d7c-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a0d7c-120">Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0d7c-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
