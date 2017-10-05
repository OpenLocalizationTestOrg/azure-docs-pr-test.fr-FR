---
title: "Exemple de script Azure CLI - Copier (déplacer) la capture instantanée d’un disque managé vers un abonnement identique ou différent avec l’interface de ligne de commande | Microsoft Docs"
description: "Exemple de script Azure CLI - Copier (déplacer) la capture instantanée d’un disque managé vers un abonnement identique ou différent avec l’interface de ligne de commande"
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="2e691-103">Copier la capture instantanée d’un disque managé vers un abonnement identique ou différent avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="2e691-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="2e691-104">Ce script copie la capture instantanée d’un disque managé vers un abonnement identique ou différent.</span><span class="sxs-lookup"><span data-stu-id="2e691-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="2e691-105">Utilisez ce script pour déplacer une capture instantanée vers un abonnement différent dans la même région que la capture instantanée parente.</span><span class="sxs-lookup"><span data-stu-id="2e691-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2e691-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="2e691-106">Sample script</span></span>

<span data-ttu-id="2e691-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copier une capture instantanée")]</span><span class="sxs-lookup"><span data-stu-id="2e691-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="2e691-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="2e691-108">Script explanation</span></span>

<span data-ttu-id="2e691-109">Ce script utilise les commandes suivantes pour créer une capture instantanée dans l’abonnement cible à l’aide de l’ID de la capture instantanée source.</span><span class="sxs-lookup"><span data-stu-id="2e691-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="2e691-110">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="2e691-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2e691-111">Commande</span><span class="sxs-lookup"><span data-stu-id="2e691-111">Command</span></span> | <span data-ttu-id="2e691-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="2e691-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e691-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="2e691-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="2e691-114">Obtient toutes les propriétés d’une capture instantanée en utilisant les propriétés de nom et de groupe de ressources de la capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="2e691-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="2e691-115">La propriété de l’identifiant est utilisée pour copier la capture instantanée vers un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e691-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="2e691-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="2e691-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="2e691-117">Copie une capture instantanée en créant une capture instantanée dans un abonnement différent à l’aide de l’identifiant et du nom de la capture instantanée parente.</span><span class="sxs-lookup"><span data-stu-id="2e691-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="2e691-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e691-118">Next steps</span></span>

[<span data-ttu-id="2e691-119">Créer une machine virtuelle à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="2e691-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="2e691-120">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e691-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2e691-121">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e691-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
