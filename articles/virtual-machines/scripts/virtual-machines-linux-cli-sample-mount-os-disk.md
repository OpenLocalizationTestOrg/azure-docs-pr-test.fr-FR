---
title: "Exemple de Script CLI - disque de système d’exploitation de montage d’aaaAzure | Documents Microsoft"
description: "Exemple de script Azure CLI - Monter un disque de système d’exploitation"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="557cf-103">Résoudre les problèmes liés au disque du système d’exploitation de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="557cf-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="557cf-104">Ce script monte le disque du système d’exploitation hello d’un ordinateur virtuel a échoué ou problématique comme données disque tooa deuxième machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="557cf-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="557cf-105">Cette procédure peut s’avérer utile lors de la résolution de problèmes de disque ou la récupération de données.</span><span class="sxs-lookup"><span data-stu-id="557cf-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="557cf-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="557cf-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="557cf-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="557cf-107">Script explanation</span></span>

<span data-ttu-id="557cf-108">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="557cf-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="557cf-109">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="557cf-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="557cf-110">Commande</span><span class="sxs-lookup"><span data-stu-id="557cf-110">Command</span></span> | <span data-ttu-id="557cf-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="557cf-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="557cf-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="557cf-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="557cf-113">Renvoie la liste des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="557cf-113">Return a list of virtual machines.</span></span> <span data-ttu-id="557cf-114">Dans ce cas, l’option de requête hello est disque de système d’exploitation de machine virtuelle de hello tooreturn utilisé.</span><span class="sxs-lookup"><span data-stu-id="557cf-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="557cf-115">Cette valeur est ensuite ajoutée tooa nom de la variable « uri ».</span><span class="sxs-lookup"><span data-stu-id="557cf-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="557cf-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="557cf-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="557cf-117">Supprime une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="557cf-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="557cf-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="557cf-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="557cf-119">Crée une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="557cf-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="557cf-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="557cf-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="557cf-121">Joint un ordinateur virtuel de tooa disque.</span><span class="sxs-lookup"><span data-stu-id="557cf-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="557cf-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="557cf-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="557cf-123">Retourne hello des adresses IP d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="557cf-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="557cf-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="557cf-124">Next steps</span></span>

<span data-ttu-id="557cf-125">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="557cf-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="557cf-126">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="557cf-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
