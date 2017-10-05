---
title: "Exemple de script Azure CLI - Création d’une machine virtuelle Windows Server | Microsoft Docs"
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
ms.openlocfilehash: 9690e743e498a55d7339b6f51861fac37c9b0f56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="6ea5b-103">Créer une machine virtuelle avec l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6ea5b-103">Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="6ea5b-104">Ce script crée une machine virtuelle Azure exécutant Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="6ea5b-105">Une fois que vous avez exécuté le script, vous pouvez accéder à la machine virtuelle au moyen d’une connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6ea5b-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6ea5b-106">Sample script</span></span>

<span data-ttu-id="6ea5b-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Création rapide de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="6ea5b-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6ea5b-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="6ea5b-108">Clean up deployment</span></span> 

<span data-ttu-id="6ea5b-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6ea5b-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6ea5b-110">Script explanation</span></span>

<span data-ttu-id="6ea5b-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6ea5b-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6ea5b-113">Commande</span><span class="sxs-lookup"><span data-stu-id="6ea5b-113">Command</span></span> | <span data-ttu-id="6ea5b-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="6ea5b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ea5b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6ea5b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6ea5b-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ea5b-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="6ea5b-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="6ea5b-118">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="6ea5b-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="6ea5b-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="6ea5b-120">Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="6ea5b-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="6ea5b-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="6ea5b-122">Crée un groupe de sécurité réseau qui représente une frontière de sécurité entre Internet et la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="6ea5b-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="6ea5b-123">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="6ea5b-124">Crée une carte réseau virtuelle et l’associe au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-124">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="6ea5b-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="6ea5b-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6ea5b-126">Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6ea5b-127">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6ea5b-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="6ea5b-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6ea5b-129">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="6ea5b-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ea5b-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ea5b-130">Next steps</span></span>

<span data-ttu-id="6ea5b-131">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ea5b-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6ea5b-132">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ea5b-132">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
