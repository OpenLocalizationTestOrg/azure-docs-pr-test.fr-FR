---
title: "aaaAzure exemple de Script CLI - créer une machine virtuelle Windows Server | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Windows Server"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="bdea6-103">Créer une machine virtuelle avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="bdea6-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="bdea6-104">Ce script crée une machine virtuelle Azure exécutant Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bdea6-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="bdea6-105">Après avoir exécuté le script de hello, vous pouvez accéder hello virtual machine via une connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="bdea6-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bdea6-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="bdea6-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bdea6-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="bdea6-107">Clean up deployment</span></span> 

<span data-ttu-id="bdea6-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="bdea6-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="bdea6-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="bdea6-109">Script explanation</span></span>

<span data-ttu-id="bdea6-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="bdea6-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="bdea6-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="bdea6-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bdea6-112">Commande</span><span class="sxs-lookup"><span data-stu-id="bdea6-112">Command</span></span> | <span data-ttu-id="bdea6-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="bdea6-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bdea6-114">az group create</span><span class="sxs-lookup"><span data-stu-id="bdea6-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bdea6-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="bdea6-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bdea6-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="bdea6-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="bdea6-117">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="bdea6-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="bdea6-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="bdea6-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="bdea6-119">Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé.</span><span class="sxs-lookup"><span data-stu-id="bdea6-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="bdea6-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="bdea6-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="bdea6-121">Crée un groupe de sécurité réseau (NSG), qui est une limite de sécurité entre l’ordinateur virtuel pour internet et hello hello.</span><span class="sxs-lookup"><span data-stu-id="bdea6-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="bdea6-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="bdea6-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="bdea6-123">Crée une carte réseau virtuelle et attache les réseaux virtuels toohello, du sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="bdea6-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="bdea6-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="bdea6-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="bdea6-125">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="bdea6-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="bdea6-126">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="bdea6-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="bdea6-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="bdea6-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="bdea6-128">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="bdea6-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bdea6-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bdea6-129">Next steps</span></span>

<span data-ttu-id="bdea6-130">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bdea6-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bdea6-131">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de Windows Azure VM](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bdea6-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
