---
title: "aaaAzure exemple de Script CLI - équilibre la charge de plusieurs sites Web avec hello CLI d’Azure | Documents Microsoft"
description: "Exemple de Script CLI Azure - équilibre la charge de plusieurs sites Web toohello même machine virtuelle"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="22849-103">Équilibrer la charge de plusieurs sites web</span><span class="sxs-lookup"><span data-stu-id="22849-103">Load balance multiple websites</span></span>

<span data-ttu-id="22849-104">Cet exemple de script crée un réseau virtuel avec deux machines virtuelles qui sont membres d’un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="22849-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="22849-105">Un équilibreur de charge dirige le trafic pour les deux machines virtuelles de toohello deux des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="22849-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="22849-106">Après l’exécution du script hello, vous pouvez déployer toohello logiciel de serveur web machines virtuelles et héberger plusieurs sites web, chacune avec sa propre adresse IP.</span><span class="sxs-lookup"><span data-stu-id="22849-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="22849-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="22849-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="22849-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="22849-108">Clean up deployment</span></span> 

<span data-ttu-id="22849-109">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="22849-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="22849-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="22849-110">Script explanation</span></span>

<span data-ttu-id="22849-111">Ce script utilise hello suivant les commandes toocreate un groupe de ressources du réseau virtuel, équilibreur de charge et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="22849-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="22849-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="22849-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="22849-113">Commande</span><span class="sxs-lookup"><span data-stu-id="22849-113">Command</span></span> | <span data-ttu-id="22849-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="22849-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="22849-115">az group create</span><span class="sxs-lookup"><span data-stu-id="22849-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="22849-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="22849-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="22849-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="22849-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="22849-118">Crée un réseau virtuel et un sous-réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="22849-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="22849-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="22849-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="22849-120">Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé.</span><span class="sxs-lookup"><span data-stu-id="22849-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="22849-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="22849-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="22849-122">Crée un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="22849-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="22849-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="22849-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="22849-124">Crée une sonde d’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="22849-124">Creates a load balancer probe.</span></span> <span data-ttu-id="22849-125">Une sonde d’équilibrage de charge est utilisé toomonitor chaque machine virtuelle dans le jeu d’équilibrage de charge de hello.</span><span class="sxs-lookup"><span data-stu-id="22849-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="22849-126">Si toutes les machines virtuelles devient inaccessible, le trafic n’est pas routé toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="22849-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="22849-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="22849-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="22849-128">Crée une règle d’équilibeur de charge.</span><span class="sxs-lookup"><span data-stu-id="22849-128">Creates a load balancer rule.</span></span> <span data-ttu-id="22849-129">Dans cet exemple, une règle est créée pour le port 80.</span><span class="sxs-lookup"><span data-stu-id="22849-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="22849-130">Comme le trafic HTTP arrive au niveau de l’équilibrage de charge hello, il est routé tooport 80 une des machines virtuelles de hello dans le jeu d’équilibrage de charge de hello.</span><span class="sxs-lookup"><span data-stu-id="22849-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="22849-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="22849-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="22849-132">Créer une adresse IP de serveur frontal pour hello équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="22849-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="22849-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="22849-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="22849-134">Crée un pool d’adresses principal.</span><span class="sxs-lookup"><span data-stu-id="22849-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="22849-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="22849-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="22849-136">Crée une carte réseau virtuelle et l’attache toohello des réseaux virtuels et le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="22849-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="22849-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="22849-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="22849-138">Crée un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="22849-138">Creates an availability set.</span></span> <span data-ttu-id="22849-139">Haute disponibilité garantit la disponibilité des applications en répartissant les machines virtuelles de hello sur ressources physiques telles qu’en cas de défaillance, ensemble hello n’est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="22849-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="22849-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="22849-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="22849-141">Crée une configuration IP.</span><span class="sxs-lookup"><span data-stu-id="22849-141">Creates an IP confiuration.</span></span> <span data-ttu-id="22849-142">Vous devez avoir hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic fonctionnalité est activée pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="22849-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="22849-143">Qu’une seule configuration peut être désignée comme configuration IP principale de hello par carte réseau, à l’aide de hello--Vérifiez principal indicateur.</span><span class="sxs-lookup"><span data-stu-id="22849-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="22849-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="22849-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="22849-145">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="22849-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="22849-146">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="22849-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="22849-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="22849-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="22849-148">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="22849-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22849-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="22849-149">Next steps</span></span>

<span data-ttu-id="22849-150">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22849-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="22849-151">Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22849-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
