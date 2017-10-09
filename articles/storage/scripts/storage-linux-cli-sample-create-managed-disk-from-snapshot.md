---
title: "aaaAzure exemple de Script CLI - créer un disque géré à partir d’un instantané | Documents Microsoft"
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
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="e40d9-103">Créer un disque managé à partir d’une capture instantanée avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e40d9-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="e40d9-104">Ce script crée un disque managé à partir d’une capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="e40d9-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="e40d9-105">Utiliser toorestore une machine virtuelle à partir de clichés instantanés des disques du système d’exploitation et des données.</span><span class="sxs-lookup"><span data-stu-id="e40d9-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="e40d9-106">Créez des disques managés de système d’exploitation et de données à partir des captures instantanées respectives, puis créez une machine virtuelle en joignant les disques managés.</span><span class="sxs-lookup"><span data-stu-id="e40d9-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="e40d9-107">Vous pouvez également restaurer les disques de données d’une machine virtuelle existante en joignant les disques de données créés à partir de captures instantanées.</span><span class="sxs-lookup"><span data-stu-id="e40d9-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e40d9-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e40d9-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e40d9-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e40d9-109">Script explanation</span></span>

<span data-ttu-id="e40d9-110">Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un instantané.</span><span class="sxs-lookup"><span data-stu-id="e40d9-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="e40d9-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e40d9-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e40d9-112">Commande</span><span class="sxs-lookup"><span data-stu-id="e40d9-112">Command</span></span> | <span data-ttu-id="e40d9-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="e40d9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e40d9-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="e40d9-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="e40d9-115">Obtient toutes les propriétés hello d’un instantané à l’aide du nom de hello et les propriétés du groupe de ressources de l’instantané d’hello.</span><span class="sxs-lookup"><span data-stu-id="e40d9-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="e40d9-116">Propriété ID est utilisé toocreate managé.</span><span class="sxs-lookup"><span data-stu-id="e40d9-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="e40d9-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="e40d9-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="e40d9-118">Crée un disque managé à l’aide de l’identifiant d’une capture instantanée managée.</span><span class="sxs-lookup"><span data-stu-id="e40d9-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e40d9-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e40d9-119">Next steps</span></span>

[<span data-ttu-id="e40d9-120">Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="e40d9-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e40d9-121">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e40d9-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e40d9-122">Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e40d9-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
