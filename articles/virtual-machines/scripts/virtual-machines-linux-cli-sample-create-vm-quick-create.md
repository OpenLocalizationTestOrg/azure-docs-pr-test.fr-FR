---
title: "aaaAzure exemple de Script CLI - création rapide un VM Linux | Documents Microsoft"
description: "Exemple de script Azure CLI - Création rapide d’une machine virtuelle Linux"
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
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="a9f55-103">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a9f55-103">Create a virtual machine</span></span>

<span data-ttu-id="a9f55-104">Ce script crée une machine virtuelle Azure avec un système d’exploitation Ubuntu et les ressources réseau associées.</span><span class="sxs-lookup"><span data-stu-id="a9f55-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="a9f55-105">Après avoir exécuté le script de hello, vous pouvez accéder hello virtual machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="a9f55-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a9f55-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a9f55-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a9f55-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a9f55-107">Clean up deployment</span></span> 

<span data-ttu-id="a9f55-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="a9f55-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a9f55-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a9f55-109">Script explanation</span></span>

<span data-ttu-id="a9f55-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="a9f55-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a9f55-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="a9f55-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a9f55-112">Commande</span><span class="sxs-lookup"><span data-stu-id="a9f55-112">Command</span></span> | <span data-ttu-id="a9f55-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="a9f55-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a9f55-114">az group create</span><span class="sxs-lookup"><span data-stu-id="a9f55-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a9f55-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a9f55-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a9f55-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="a9f55-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a9f55-117">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a9f55-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="a9f55-118">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="a9f55-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="a9f55-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="a9f55-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a9f55-120">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="a9f55-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a9f55-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9f55-121">Next steps</span></span>

<span data-ttu-id="a9f55-122">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a9f55-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a9f55-123">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9f55-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
