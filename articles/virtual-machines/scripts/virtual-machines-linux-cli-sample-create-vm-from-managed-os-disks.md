---
title: "aaaAzure exemple de Script CLI - créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation | Documents Microsoft"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="88162-103">Créer une machine virtuelle utilisant un disque de système d’exploitation géré existant avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="88162-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="88162-104">Ce script crée une machine virtuelle en attachant un disque géré existant en tant que disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="88162-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="88162-105">Utilisez ce script dans des scénarios précédent :</span><span class="sxs-lookup"><span data-stu-id="88162-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="88162-106">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été copié d’un disque géré dans un autre abonnement</span><span class="sxs-lookup"><span data-stu-id="88162-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="88162-107">Créer une machine virtuelle à partir d’un disque géré existant qui a été créé à partir d’un fichier de disque dur virtuel spécialisé</span><span class="sxs-lookup"><span data-stu-id="88162-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="88162-108">Créer une machine virtuelle à partir d’un disque de système d’exploitation géré existant qui a été créé à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="88162-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="88162-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="88162-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="88162-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="88162-110">Clean up deployment</span></span> 

<span data-ttu-id="88162-111">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="88162-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="88162-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="88162-112">Script explanation</span></span>

<span data-ttu-id="88162-113">Ce script utilise hello commandes tooget géré disque propriétés suivantes, attacher un disque géré de tooa nouvelle machine virtuelle et créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="88162-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="88162-114">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="88162-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="88162-115">Commande</span><span class="sxs-lookup"><span data-stu-id="88162-115">Command</span></span> | <span data-ttu-id="88162-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="88162-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="88162-117">az disk show</span><span class="sxs-lookup"><span data-stu-id="88162-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="88162-118">Obtient des propriétés de disque géré à l’aide d’un nom de disque et d’un nom de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="88162-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="88162-119">Propriété ID est utilisé tooattach un tooa disque géré nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="88162-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="88162-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="88162-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="88162-121">Crée une machine virtuelle à l’aide d’un disque de système d’exploitation géré</span><span class="sxs-lookup"><span data-stu-id="88162-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="88162-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88162-122">Next steps</span></span>

<span data-ttu-id="88162-123">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88162-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="88162-124">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88162-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
