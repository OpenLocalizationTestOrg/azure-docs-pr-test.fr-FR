---
title: "aaaAzure exemple de Script CLI - copie (déplacer) géré toosame de disques ou d’un autre abonnement | Documents Microsoft"
description: "Exemple de Script CLI Azure - Copy (déplacer) gérés disques toosame ou autre abonnement"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="bc4bf-103">Copier les disques gérés toosame ou autre abonnement avec l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="bc4bf-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="bc4bf-104">Ce script copie un disque géré toosame ou un autre abonnement, mais dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="bc4bf-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bc4bf-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="bc4bf-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="bc4bf-106">Explication du script</span><span class="sxs-lookup"><span data-stu-id="bc4bf-106">Script explanation</span></span>

<span data-ttu-id="bc4bf-107">Ce script utilise suivante commandes toocreate un nouveau disque géré à l’aide d’abonnement cible hello hello Id de source de hello gérés disque.</span><span class="sxs-lookup"><span data-stu-id="bc4bf-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="bc4bf-108">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="bc4bf-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bc4bf-109">Commande</span><span class="sxs-lookup"><span data-stu-id="bc4bf-109">Command</span></span> | <span data-ttu-id="bc4bf-110">Remarques</span><span class="sxs-lookup"><span data-stu-id="bc4bf-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bc4bf-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="bc4bf-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="bc4bf-112">Obtient toutes les propriétés de hello d’un disque géré à l’aide des propriétés du groupe hello nom et les ressources de disque géré de hello.</span><span class="sxs-lookup"><span data-stu-id="bc4bf-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="bc4bf-113">Propriété ID est utilisé toocopy hello géré disque toodifferent abonnement.</span><span class="sxs-lookup"><span data-stu-id="bc4bf-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="bc4bf-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="bc4bf-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="bc4bf-115">Copie d’un disque géré en créant un nouveau disque géré dans un autre abonnement à l’aide d’Id et nom du parent de hello gérés disque.</span><span class="sxs-lookup"><span data-stu-id="bc4bf-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="bc4bf-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc4bf-116">Next steps</span></span>

[<span data-ttu-id="bc4bf-117">Créer une machine virtuelle à partir d’un disque géré</span><span class="sxs-lookup"><span data-stu-id="bc4bf-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="bc4bf-118">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bc4bf-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bc4bf-119">Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bc4bf-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
