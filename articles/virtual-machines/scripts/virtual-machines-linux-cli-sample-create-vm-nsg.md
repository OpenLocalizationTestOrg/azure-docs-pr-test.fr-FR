---
title: "aaaAzure exemple de Script CLI - créer deux machines virtuelles avec un groupe de sécurité réseau interne et externe | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer deux machines virtuelles avec un groupe de sécurité réseau interne et un groupe de sécurité réseau externe"
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="319a9-103">Sécuriser le trafic réseau entre les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="319a9-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="319a9-104">Ce script crée deux machines virtuelles et sécurise tooboth de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="319a9-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="319a9-105">Un ordinateur virtuel est accessible sur hello internet et a un groupe de sécurité réseau (NSG) configuré tooallow trafic sur le port 22 et le port 80.</span><span class="sxs-lookup"><span data-stu-id="319a9-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="319a9-106">machine virtuelle de la deuxième Hello n’est pas accessible sur internet de hello, et a une tooonly de groupe de sécurité réseau configuré autoriser le trafic à partir de la première machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="319a9-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="319a9-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="319a9-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="319a9-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="319a9-108">Clean up deployment</span></span> 

<span data-ttu-id="319a9-109">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="319a9-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="319a9-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="319a9-110">Script explanation</span></span>

<span data-ttu-id="319a9-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="319a9-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="319a9-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="319a9-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="319a9-113">Commande</span><span class="sxs-lookup"><span data-stu-id="319a9-113">Command</span></span> | <span data-ttu-id="319a9-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="319a9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="319a9-115">az group create</span><span class="sxs-lookup"><span data-stu-id="319a9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="319a9-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="319a9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="319a9-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="319a9-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="319a9-118">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="319a9-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="319a9-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="319a9-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="319a9-120">Crée un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="319a9-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="319a9-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="319a9-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="319a9-122">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="319a9-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="319a9-123">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="319a9-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="319a9-124">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="319a9-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="319a9-125">Renvoie les informations relatives à une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="319a9-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="319a9-126">Dans cet exemple, le nom de la règle hello est stocké dans une variable pour une utilisation ultérieure dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="319a9-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="319a9-127">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="319a9-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="319a9-128">Met à jour une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="319a9-128">Updates an NSG rule.</span></span> <span data-ttu-id="319a9-129">Dans cet exemple, la règle de principaux de hello est toopass mis à jour par le trafic uniquement à partir de sous-réseau frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="319a9-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="319a9-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="319a9-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="319a9-131">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="319a9-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="319a9-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="319a9-132">Next steps</span></span>

<span data-ttu-id="319a9-133">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="319a9-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="319a9-134">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="319a9-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
