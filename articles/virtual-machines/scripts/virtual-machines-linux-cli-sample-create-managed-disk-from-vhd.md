---
title: "aaaAzure exemple de Script CLI - créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement | Documents Microsoft"
description: "Le Script CLI Azure exemple : création d’un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement"
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="907da-103">Créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement avec l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="907da-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="907da-104">Ce script crée un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="907da-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="907da-105">Utilisez cette tooimport script un spécialisé toocreate (pas généralisé/préparée avec Sysprep) disque dur virtuel toomanaged du système d’exploitation disque un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="907da-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="907da-106">Ou bien, utilisez-la tooimport un disque de données toomanaged données disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="907da-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="907da-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="907da-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="907da-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="907da-108">Script explanation</span></span>

<span data-ttu-id="907da-109">Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="907da-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="907da-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="907da-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="907da-111">Commande</span><span class="sxs-lookup"><span data-stu-id="907da-111">Command</span></span> | <span data-ttu-id="907da-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="907da-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="907da-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="907da-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="907da-114">Crée un disque géré à l’aide de l’URI d’un disque dur virtuel dans un compte de stockage hello même abonnement</span><span class="sxs-lookup"><span data-stu-id="907da-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="907da-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="907da-115">Next steps</span></span>

[<span data-ttu-id="907da-116">Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="907da-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="907da-117">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="907da-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="907da-118">Machine virtuelle supplémentaire et des exemples de scripts CLI de disques gérés sont accessibles dans hello [documentation de la machine virtuelle de Azure Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="907da-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
