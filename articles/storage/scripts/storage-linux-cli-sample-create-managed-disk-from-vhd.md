---
title: "Exemple de script avec l’interface de ligne de commande Azure CLI - Créer un disque managé à partir d’un fichier de VHD dans un compte de stockage dans le même abonnement | Microsoft Docs"
description: "Exemple de script avec l’interface de ligne de commande Azure CLI - Créer un disque managé à partir d’un fichier de VHD dans un compte de stockage dans le même abonnement"
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
ms.openlocfilehash: 5022ca23ac2c2e515a9b80d44b1221f3c05fecb1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="af9d1-103">Créer un disque managé à partir d’un fichier de VHD dans un compte de stockage dans le même abonnement avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="af9d1-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="af9d1-104">Ce script crée un disque managé à partir d’un fichier de VHD dans un compte de stockage dans le même abonnement.</span><span class="sxs-lookup"><span data-stu-id="af9d1-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="af9d1-105">Utilisez ce script pour importer un VHD spécialisé (non généralisé/préparé avec Sysprep) vers un disque de système d’exploitation managé pour créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af9d1-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="af9d1-106">Ou bien, utilisez-le pour importer un VHD de données vers un disque de données managées.</span><span class="sxs-lookup"><span data-stu-id="af9d1-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="af9d1-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="af9d1-107">Sample script</span></span>

<span data-ttu-id="af9d1-108">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Créer un disque managé à partir d’un VHD")]</span><span class="sxs-lookup"><span data-stu-id="af9d1-108">[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="af9d1-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="af9d1-109">Script explanation</span></span>

<span data-ttu-id="af9d1-110">Ce script a recours aux commandes suivantes pour créer un disque managé à partir d’un VHD.</span><span class="sxs-lookup"><span data-stu-id="af9d1-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="af9d1-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="af9d1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="af9d1-112">Commande</span><span class="sxs-lookup"><span data-stu-id="af9d1-112">Command</span></span> | <span data-ttu-id="af9d1-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="af9d1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="af9d1-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="af9d1-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="af9d1-115">Crée un disque managé en utilisant l’URI d’un VHD dans un compte de stockage dans le même abonnement</span><span class="sxs-lookup"><span data-stu-id="af9d1-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="af9d1-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af9d1-116">Next steps</span></span>

[<span data-ttu-id="af9d1-117">Créer une machine virtuelle en joignant un disque managé en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="af9d1-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="af9d1-118">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af9d1-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="af9d1-119">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle et de disques managés dans la [documentation relative aux machines virtuelles Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af9d1-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
