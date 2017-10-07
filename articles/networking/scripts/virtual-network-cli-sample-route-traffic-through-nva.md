---
title: "exemple de script CLI aaaAzure - acheminer le trafic via un matériel de réseau virtuel | Documents Microsoft"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="909cc-103">Acheminer le trafic via une appliance virtuelle réseau</span><span class="sxs-lookup"><span data-stu-id="909cc-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="909cc-104">Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="909cc-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="909cc-105">Il crée également un ordinateur virtuel IP le trafic tooroute activé entre deux sous-réseaux de hello.</span><span class="sxs-lookup"><span data-stu-id="909cc-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="909cc-106">Après avoir exécuté le script de hello, vous pouvez déployer un logiciel réseau, telle qu’une application de pare-feu, toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="909cc-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="909cc-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="909cc-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="909cc-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="909cc-108">Clean up deployment</span></span> 

<span data-ttu-id="909cc-109">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="909cc-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="909cc-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="909cc-110">Script explanation</span></span>

<span data-ttu-id="909cc-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="909cc-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="909cc-112">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="909cc-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="909cc-113">Commande</span><span class="sxs-lookup"><span data-stu-id="909cc-113">Command</span></span> | <span data-ttu-id="909cc-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="909cc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="909cc-115">az group create</span><span class="sxs-lookup"><span data-stu-id="909cc-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="909cc-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="909cc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="909cc-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="909cc-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="909cc-118">Crée un réseau virtuel et un sous-réseau frontal Azure.</span><span class="sxs-lookup"><span data-stu-id="909cc-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="909cc-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="909cc-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="909cc-120">Crée des sous-réseaux principaux et DMZ.</span><span class="sxs-lookup"><span data-stu-id="909cc-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="909cc-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="909cc-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="909cc-122">Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="909cc-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="909cc-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="909cc-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="909cc-124">Crée une interface réseau virtuelle et active le transfert IP pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="909cc-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="909cc-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="909cc-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="909cc-126">Crée un groupe de sécurité réseau (NSG).</span><span class="sxs-lookup"><span data-stu-id="909cc-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="909cc-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="909cc-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="909cc-128">Crée des règles de groupe de sécurité réseau qui autorise les ports HTTP et HTTPS entrant toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="909cc-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="909cc-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="909cc-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="909cc-130">Associe hello des groupes de sécurité réseau et toosubnets des tables de routage.</span><span class="sxs-lookup"><span data-stu-id="909cc-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="909cc-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="909cc-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="909cc-132">Crée une table de routage pour tous les itinéraires.</span><span class="sxs-lookup"><span data-stu-id="909cc-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="909cc-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="909cc-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="909cc-134">Crée des itinéraires tooroute un trafic entre les sous-réseaux et hello Internet via hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="909cc-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="909cc-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="909cc-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="909cc-136">Crée une machine virtuelle et attache hello NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="909cc-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="909cc-137">Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="909cc-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="909cc-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="909cc-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="909cc-139">Supprime un groupe de ressources, ainsi que toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="909cc-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="909cc-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="909cc-140">Next steps</span></span>

<span data-ttu-id="909cc-141">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="909cc-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="909cc-142">Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="909cc-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
