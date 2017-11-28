---
title: "Exemples de script Azure CLI - Créer un disque managé à partir d’une capture instantanée | Microsoft Docs"
description: "Exemples de script Azure CLI - Créer un disque managé à partir d’une capture instantanée"
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
ms.openlocfilehash: 030fa06bc5819443dac5832172a93c2dca28d1ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="29f00-103">Créer un disque managé à partir d’une capture instantanée avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="29f00-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="29f00-104">Ce script crée un disque managé à partir d’une capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="29f00-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="29f00-105">Utilisez-le pour restaurer une machine virtuelle à partir de captures instantanées de disques de système d’exploitation et de données.</span><span class="sxs-lookup"><span data-stu-id="29f00-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="29f00-106">Créez des disques managés de système d’exploitation et de données à partir des captures instantanées respectives, puis créez une machine virtuelle en joignant les disques managés.</span><span class="sxs-lookup"><span data-stu-id="29f00-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="29f00-107">Vous pouvez également restaurer les disques de données d’une machine virtuelle existante en joignant les disques de données créés à partir de captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="29f00-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="29f00-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="29f00-108">Sample script</span></span>

<span data-ttu-id="29f00-109">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Créer un disque managé à partir d’une capture instantanée")]</span><span class="sxs-lookup"><span data-stu-id="29f00-109">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="29f00-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="29f00-110">Script explanation</span></span>

<span data-ttu-id="29f00-111">Ce script a recours aux commandes suivantes pour créer un disque managé à partir d’une capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="29f00-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="29f00-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="29f00-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="29f00-113">Commande</span><span class="sxs-lookup"><span data-stu-id="29f00-113">Command</span></span> | <span data-ttu-id="29f00-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="29f00-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="29f00-115">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="29f00-115">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="29f00-116">Obtient toutes les propriétés d’une capture instantanée en utilisant les propriétés de nom et de groupe de ressources de la capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="29f00-116">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="29f00-117">La propriété de l’identifiant est utilisée pour créer le disque managé.</span><span class="sxs-lookup"><span data-stu-id="29f00-117">Id property is used to create managed disk.</span></span>  |
| [<span data-ttu-id="29f00-118">az disk create</span><span class="sxs-lookup"><span data-stu-id="29f00-118">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="29f00-119">Crée un disque managé à l’aide de l’identifiant d’une capture instantanée managée.</span><span class="sxs-lookup"><span data-stu-id="29f00-119">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="29f00-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29f00-120">Next steps</span></span>

[<span data-ttu-id="29f00-121">Créer une machine virtuelle en joignant un disque managé en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="29f00-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="29f00-122">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29f00-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="29f00-123">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29f00-123">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>