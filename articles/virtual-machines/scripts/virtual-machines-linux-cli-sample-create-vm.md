---
title: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux | Microsoft Docs"
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
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="d1732-103">Créer une machine virtuelle entièrement configurée</span><span class="sxs-lookup"><span data-stu-id="d1732-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="d1732-104">Ce script crée une machine virtuelle Azure avec un système d’exploitation Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d1732-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="d1732-105">Une fois que vous avez exécuté le script, vous pouvez accéder à la machine virtuelle via SSH.</span><span class="sxs-lookup"><span data-stu-id="d1732-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d1732-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d1732-106">Sample script</span></span>

<span data-ttu-id="d1732-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Création rapide de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="d1732-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d1732-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="d1732-108">Clean up deployment</span></span> 

<span data-ttu-id="d1732-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d1732-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d1732-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d1732-110">Script explanation</span></span>

<span data-ttu-id="d1732-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d1732-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d1732-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d1732-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d1732-113">Commande</span><span class="sxs-lookup"><span data-stu-id="d1732-113">Command</span></span> | <span data-ttu-id="d1732-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="d1732-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1732-115">az group create</span><span class="sxs-lookup"><span data-stu-id="d1732-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d1732-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d1732-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1732-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d1732-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="d1732-118">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="d1732-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="d1732-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="d1732-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="d1732-120">Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé.</span><span class="sxs-lookup"><span data-stu-id="d1732-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="d1732-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="d1732-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="d1732-122">Crée un groupe de sécurité réseau qui représente une frontière de sécurité entre Internet et la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d1732-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="d1732-123">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="d1732-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="d1732-124">Crée une règle de groupe de sécurité réseau permettant d’autoriser le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d1732-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="d1732-125">Dans cet exemple, le port 22 est ouvert pour le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="d1732-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="d1732-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="d1732-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="d1732-127">Crée une carte réseau virtuelle et l’associe au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d1732-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="d1732-128">az vm create</span><span class="sxs-lookup"><span data-stu-id="d1732-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d1732-129">Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d1732-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="d1732-130">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="d1732-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d1732-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="d1732-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d1732-132">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="d1732-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d1732-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1732-133">Next steps</span></span>

<span data-ttu-id="d1732-134">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1732-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d1732-135">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1732-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
