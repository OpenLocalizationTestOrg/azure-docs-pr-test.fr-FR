---
title: "aaaAzure exemple de Script CLI - créer un VM Linux | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux"
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
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="62667-103">Créer une machine virtuelle entièrement configurée</span><span class="sxs-lookup"><span data-stu-id="62667-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="62667-104">Ce script crée une machine virtuelle Azure avec un système d’exploitation Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="62667-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="62667-105">Après avoir exécuté le script de hello, vous pouvez accéder hello virtual machine via SSH.</span><span class="sxs-lookup"><span data-stu-id="62667-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="62667-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="62667-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="62667-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="62667-107">Clean up deployment</span></span> 

<span data-ttu-id="62667-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="62667-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="62667-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="62667-109">Script explanation</span></span>

<span data-ttu-id="62667-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="62667-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="62667-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="62667-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="62667-112">Commande</span><span class="sxs-lookup"><span data-stu-id="62667-112">Command</span></span> | <span data-ttu-id="62667-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="62667-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62667-114">az group create</span><span class="sxs-lookup"><span data-stu-id="62667-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62667-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="62667-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62667-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="62667-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="62667-117">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="62667-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="62667-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="62667-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="62667-119">Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé.</span><span class="sxs-lookup"><span data-stu-id="62667-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="62667-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="62667-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="62667-121">Crée un groupe de sécurité réseau (NSG), qui est une limite de sécurité entre l’ordinateur virtuel pour internet et hello hello.</span><span class="sxs-lookup"><span data-stu-id="62667-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="62667-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="62667-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="62667-123">Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="62667-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="62667-124">Dans cet exemple, le port 22 est ouvert pour le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="62667-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="62667-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="62667-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="62667-126">Crée une carte réseau virtuelle et attache les réseaux virtuels toohello, du sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="62667-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="62667-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="62667-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="62667-128">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="62667-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="62667-129">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="62667-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="62667-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="62667-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="62667-131">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="62667-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62667-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62667-132">Next steps</span></span>

<span data-ttu-id="62667-133">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62667-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62667-134">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62667-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
