---
title: "Exemple de script Azure CLI - Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="a585e-103">Créer une machine virtuelle utilisant un disque de système d’exploitation géré existant avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="a585e-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="a585e-104">Ce script crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a585e-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="a585e-105">Utilisez ce script dans des scénarios précédent :</span><span class="sxs-lookup"><span data-stu-id="a585e-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="a585e-106">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été copié d’un disque géré dans un autre abonnement</span><span class="sxs-lookup"><span data-stu-id="a585e-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="a585e-107">Créer une machine virtuelle à partir d’un disque géré existant qui a été créé à partir d’un fichier de disque dur virtuel spécialisé</span><span class="sxs-lookup"><span data-stu-id="a585e-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="a585e-108">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été créé à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="a585e-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a585e-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a585e-109">Sample script</span></span>

<span data-ttu-id="a585e-110">[!code-azurecli-interactive[ain](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Créer une machine virtuelle à partir d’un disque géré")]</span><span class="sxs-lookup"><span data-stu-id="a585e-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a585e-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a585e-111">Clean up deployment</span></span> 

<span data-ttu-id="a585e-112">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="a585e-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a585e-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a585e-113">Script explanation</span></span>

<span data-ttu-id="a585e-114">Ce script utilise les commandes suivantes pour obtenir des propriétés de disque géré, attacher un disque géré à une nouvelle machine virtuelle et créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a585e-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="a585e-115">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="a585e-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a585e-116">Commande</span><span class="sxs-lookup"><span data-stu-id="a585e-116">Command</span></span> | <span data-ttu-id="a585e-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="a585e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a585e-118">az disk show</span><span class="sxs-lookup"><span data-stu-id="a585e-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="a585e-119">Obtient des propriétés de disque géré à l’aide d’un nom de disque et d’un nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a585e-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="a585e-120">La propriété Id est utilisée pour attacher un disque géré à une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a585e-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="a585e-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="a585e-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a585e-122">Crée une machine virtuelle à l’aide d’un disque de système d’exploitation géré</span><span class="sxs-lookup"><span data-stu-id="a585e-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="a585e-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a585e-123">Next steps</span></span>

<span data-ttu-id="a585e-124">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a585e-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a585e-125">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a585e-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
