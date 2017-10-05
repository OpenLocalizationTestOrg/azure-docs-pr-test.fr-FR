---
title: "Exemple de script Azure CLI - Filtrer le trafic réseau de machine virtuelle | Microsoft Docs"
description: "Exemple de script Azure CLI - Filtrer le trafic réseau de machine virtuelle entrant et sortant"
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="adb6c-103">Filtrer le trafic réseau de machine virtuelle entrant et sortant</span><span class="sxs-lookup"><span data-stu-id="adb6c-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="adb6c-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="adb6c-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="adb6c-105">Le trafic réseau entrant vers le sous-réseau frontal est limité à HTTP, HTTPS et SSH, tandis que le trafic sortant vers Internet à partir du sous-réseau principal n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="adb6c-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="adb6c-106">Après avoir exécuté le script, vous disposerez d’une machine virtuelle avec deux cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="adb6c-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="adb6c-107">Chacune est connectée à un sous-réseau différent.</span><span class="sxs-lookup"><span data-stu-id="adb6c-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="adb6c-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="adb6c-108">Sample script</span></span>


<span data-ttu-id="adb6c-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filtrer le trafic réseau de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="adb6c-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="adb6c-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="adb6c-110">Clean up deployment</span></span> 

<span data-ttu-id="adb6c-111">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="adb6c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="adb6c-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="adb6c-112">Script explanation</span></span>

<span data-ttu-id="adb6c-113">Ce script utilise les commandes suivantes pour créer un groupe de ressources, un réseau virtuel et les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="adb6c-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="adb6c-114">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="adb6c-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="adb6c-115">Commande</span><span class="sxs-lookup"><span data-stu-id="adb6c-115">Command</span></span> | <span data-ttu-id="adb6c-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="adb6c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="adb6c-117">az group create</span><span class="sxs-lookup"><span data-stu-id="adb6c-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="adb6c-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="adb6c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="adb6c-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="adb6c-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="adb6c-120">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="adb6c-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="adb6c-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="adb6c-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="adb6c-122">Crée un sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="adb6c-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="adb6c-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="adb6c-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="adb6c-124">Associe les groupes de sécurité réseau à des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="adb6c-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="adb6c-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="adb6c-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="adb6c-126">Crée une adresse IP publique pour accéder à la machine virtuelle à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="adb6c-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="adb6c-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="adb6c-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="adb6c-128">Crée des interfaces réseau virtuelles et les attache aux sous-réseaux frontaux et principaux du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="adb6c-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="adb6c-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="adb6c-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="adb6c-130">Crée des groupes de sécurité réseau (NSG) associés aux sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="adb6c-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="adb6c-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="adb6c-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="adb6c-132">Crée des règles NSG qui autorisent ou bloquent des ports spécifiques sur des sous-réseaux donnés.</span><span class="sxs-lookup"><span data-stu-id="adb6c-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="adb6c-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="adb6c-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="adb6c-134">Crée des machines virtuelles et associe une carte d’interface réseau à chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="adb6c-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="adb6c-135">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="adb6c-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="adb6c-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="adb6c-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="adb6c-137">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="adb6c-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="adb6c-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="adb6c-138">Next steps</span></span>

<span data-ttu-id="adb6c-139">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="adb6c-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="adb6c-140">Vous pouvez trouver des exemples supplémentaires de scripts CLI de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="adb6c-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>