---
title: "Exemple de script Azure CLI - Copier (déplacer) des disques managés vers un abonnement identique ou différent | Microsoft Docs"
description: "Exemple de script Azure CLI - Copier (déplacer) des disques managés vers un abonnement identique ou différent"
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
ms.openlocfilehash: 784ad81db2c83da14665fa926425928f12a15c27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="18591-103">Copier des disques managés vers un abonnement identique ou différent avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="18591-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="18591-104">Ce script copie le disque managé vers un abonnement identique ou différent, mais dans la même région.</span><span class="sxs-lookup"><span data-stu-id="18591-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="18591-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="18591-105">Sample script</span></span>

<span data-ttu-id="18591-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copier un disque managé")]</span><span class="sxs-lookup"><span data-stu-id="18591-106">[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="18591-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="18591-107">Script explanation</span></span>

<span data-ttu-id="18591-108">Ce script utilise les commandes suivantes pour créer un disque géré dans l’abonnement cible à l’aide de l’ID du disque source géré.</span><span class="sxs-lookup"><span data-stu-id="18591-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="18591-109">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="18591-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="18591-110">Commande</span><span class="sxs-lookup"><span data-stu-id="18591-110">Command</span></span> | <span data-ttu-id="18591-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="18591-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="18591-112">az disk show</span><span class="sxs-lookup"><span data-stu-id="18591-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="18591-113">Obtient toutes les propriétés d’un disque managé en utilisant les propriétés de nom et de groupe de ressources du disque managé.</span><span class="sxs-lookup"><span data-stu-id="18591-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="18591-114">La propriété de l’identifiant est utilisée pour copier le disque managé vers un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="18591-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="18591-115">az disk create</span><span class="sxs-lookup"><span data-stu-id="18591-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="18591-116">Copie un disque managé en créant un disque managé dans un autre abonnement à l’aide de l’identifiant et du nom du disque managé parent.</span><span class="sxs-lookup"><span data-stu-id="18591-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="18591-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18591-117">Next steps</span></span>

[<span data-ttu-id="18591-118">Créer une machine virtuelle à partir d’un disque managé</span><span class="sxs-lookup"><span data-stu-id="18591-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="18591-119">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="18591-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="18591-120">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18591-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
