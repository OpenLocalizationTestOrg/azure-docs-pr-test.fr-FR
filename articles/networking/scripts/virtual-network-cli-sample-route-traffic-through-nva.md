---
title: "Exemple de script Azure CLI - Acheminer le trafic via une appliance virtuelle réseau | Microsoft Docs"
description: "Exemple de script Azure CLI - Acheminer le trafic via une appliance virtuelle réseau de pare-feu."
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
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="d24c6-103">Acheminer le trafic via une appliance virtuelle réseau</span><span class="sxs-lookup"><span data-stu-id="d24c6-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="d24c6-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="d24c6-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d24c6-105">Il crée également une machine virtuelle sur laquelle le transfert IP est activé pour acheminer le trafic entre les deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="d24c6-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="d24c6-106">Après avoir exécuté le script, vous pouvez déployer un logiciel réseau, telle qu’une application de pare-feu, sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d24c6-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="d24c6-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d24c6-107">Sample script</span></span>


<span data-ttu-id="d24c6-108">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Acheminer le trafic via une appliance virtuelle réseau")]</span><span class="sxs-lookup"><span data-stu-id="d24c6-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d24c6-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="d24c6-109">Clean up deployment</span></span> 

<span data-ttu-id="d24c6-110">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d24c6-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d24c6-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d24c6-111">Script explanation</span></span>

<span data-ttu-id="d24c6-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, un réseau virtuel et les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d24c6-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d24c6-113">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d24c6-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d24c6-114">Commande</span><span class="sxs-lookup"><span data-stu-id="d24c6-114">Command</span></span> | <span data-ttu-id="d24c6-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="d24c6-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d24c6-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d24c6-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d24c6-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d24c6-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d24c6-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d24c6-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="d24c6-119">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="d24c6-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d24c6-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="d24c6-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d24c6-121">Crée des sous-réseaux principaux et DMZ.</span><span class="sxs-lookup"><span data-stu-id="d24c6-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="d24c6-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="d24c6-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="d24c6-123">Crée une adresse IP publique pour accéder à la machine virtuelle à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="d24c6-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="d24c6-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="d24c6-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="d24c6-125">Crée une interface réseau virtuelle et active le transfert IP pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d24c6-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="d24c6-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="d24c6-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="d24c6-127">Crée un groupe de sécurité réseau (NSG).</span><span class="sxs-lookup"><span data-stu-id="d24c6-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="d24c6-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="d24c6-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="d24c6-129">Crée des règles NSG qui autorisent des ports HTTP et HTTPS entrants sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d24c6-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="d24c6-130">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="d24c6-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="d24c6-131">Associe les NSG et les tables de routage aux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="d24c6-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="d24c6-132">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="d24c6-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="d24c6-133">Crée une table de routage pour tous les itinéraires.</span><span class="sxs-lookup"><span data-stu-id="d24c6-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="d24c6-134">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="d24c6-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="d24c6-135">Créer des itinéraires pour acheminer le trafic entre les sous-réseaux et Internet via la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d24c6-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="d24c6-136">az vm create</span><span class="sxs-lookup"><span data-stu-id="d24c6-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="d24c6-137">Crée une machine virtuelle et lui associe la carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="d24c6-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="d24c6-138">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="d24c6-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="d24c6-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="d24c6-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d24c6-140">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="d24c6-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d24c6-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d24c6-141">Next steps</span></span>

<span data-ttu-id="d24c6-142">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d24c6-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="d24c6-143">Vous pouvez trouver des exemples supplémentaires de scripts CLI de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d24c6-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>