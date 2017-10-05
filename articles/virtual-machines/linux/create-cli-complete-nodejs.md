---
title: "Création d’un environnement Linux complet à l’aide de l’interface Azure CLI 1.0 | Microsoft Docs"
description: "Créez un stockage, une machine virtuelle Linux, un réseau virtuel et un sous-réseau, un équilibreur de charge, une carte d’interface réseau, une adresse IP publique et un groupe de sécurité réseau à partir de zéro à l’aide de l’interface de ligne de commande Azure 1.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="8f43b-103">Créer un environnement Linux complet à l’aide de l’interface Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8f43b-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="8f43b-104">Dans cet article, nous créons un réseau simple avec un équilibreur de charge et deux machines virtuelles à des fins de développement et de calcul simple.</span><span class="sxs-lookup"><span data-stu-id="8f43b-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="8f43b-105">Nous suivons ce processus, commande par commande, jusqu’à ce que vous disposiez de deux machines virtuelles Linux sécurisées opérationnelles, auxquelles vous pouvez vous connecter à partir de n’importe quel emplacement via Internet.</span><span class="sxs-lookup"><span data-stu-id="8f43b-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="8f43b-106">Vous pourrez ensuite créer des réseaux et des environnements plus complexes.</span><span class="sxs-lookup"><span data-stu-id="8f43b-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="8f43b-107">Vous allez découvrir la hiérarchie des dépendances et la puissance que vous offre le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8f43b-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="8f43b-108">Une fois que vous avez compris la façon dont le système est créé, vous pouvez le reconstruire beaucoup plus rapidement en utilisant des [modèles Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f43b-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8f43b-109">De même, après avoir compris la façon dont les différentes parties de votre environnement s’imbriquent, la création de modèles pour automatiser ces dernières se révèle plus simple.</span><span class="sxs-lookup"><span data-stu-id="8f43b-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="8f43b-110">L’environnement contient :</span><span class="sxs-lookup"><span data-stu-id="8f43b-110">The environment contains:</span></span>

* <span data-ttu-id="8f43b-111">Deux machines virtuelles dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8f43b-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="8f43b-112">Un équilibreur de charge avec une règle d’équilibrage de charge sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="8f43b-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="8f43b-113">Des règles de groupe de sécurité réseau (NSG) pour protéger votre machine virtuelle de tout trafic indésirable.</span><span class="sxs-lookup"><span data-stu-id="8f43b-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="8f43b-114">Pour créer cet environnement personnalisé, [l’interface de ligne de commande 1.0 Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) la plus récente doit être installée en mode Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="8f43b-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="8f43b-115">Vous avez également besoin d’un outil d’analyse JSON.</span><span class="sxs-lookup"><span data-stu-id="8f43b-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="8f43b-116">Cet exemple utilise [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="8f43b-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8f43b-117">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="8f43b-117">CLI versions to complete the task</span></span>
<span data-ttu-id="8f43b-118">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="8f43b-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="8f43b-119">[Azure CLI 1.0](#quick-commands) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="8f43b-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8f43b-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f43b-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="8f43b-121">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="8f43b-121">Quick commands</span></span>
<span data-ttu-id="8f43b-122">Si vous avez besoin d’accomplir rapidement cette tâche, la section suivante décrit les commandes de base qui vous permettront de charger une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8f43b-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="8f43b-123">Pour obtenir plus d’informations et davantage de contexte pour chaque étape, lisez la suite de ce document, à partir de [cette section](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8f43b-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="8f43b-124">Veillez à ce que [l’interface de ligne de commande 1.0 Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) soit connectée et utilise le mode Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="8f43b-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8f43b-125">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="8f43b-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8f43b-126">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="8f43b-127">Créez le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8f43b-127">Create the resource group.</span></span> <span data-ttu-id="8f43b-128">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` à l’emplacement `westeurope` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="8f43b-129">Vérifiez le groupe de ressources à l’aide de l’analyseur JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8f43b-130">Créez le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8f43b-130">Create the storage account.</span></span> <span data-ttu-id="8f43b-131">L’exemple suivant permet de créer un compte de stockage nommé `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="8f43b-132">(Le nom du compte de stockage doit être unique, fournissez donc votre propre nom unique.)</span><span class="sxs-lookup"><span data-stu-id="8f43b-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="8f43b-133">Vérifiez le compte de stockage à l’aide de l’analyseur JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="8f43b-134">Création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8f43b-134">Create the virtual network.</span></span> <span data-ttu-id="8f43b-135">L’exemple suivant crée un réseau virtuel nommé `myVnet` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="8f43b-136">Créez un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-136">Create a subnet.</span></span> <span data-ttu-id="8f43b-137">L’exemple suivant permet de créer un sous-réseau nommé `mySubnet` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="8f43b-138">Vérifiez le réseau virtuel et le sous-réseau à l’aide de l’analyseur JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="8f43b-139">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8f43b-139">Create a public IP.</span></span> <span data-ttu-id="8f43b-140">L’exemple suivant permet de créer une adresse IP publique nommée `myPublicIP` avec le nom DNS de `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="8f43b-141">(Le nom DNS doit être unique, fournissez donc votre propre nom unique.)</span><span class="sxs-lookup"><span data-stu-id="8f43b-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="8f43b-142">Créez l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-142">Create the load balancer.</span></span> <span data-ttu-id="8f43b-143">L’exemple suivant permet de créer un équilibrage de charge nommé `myLoadBalancer` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="8f43b-144">Créez un pool d’adresses IP frontal pour l’équilibrage de charge et associez-le à l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8f43b-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="8f43b-145">L’exemple suivant permet de créer un pool d’adresses IP frontal nommé `mySubnetPool` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="8f43b-146">Créez le pool d’adresses IP principal pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="8f43b-147">L’exemple suivant permet de créer un pool d’adresses IP principal nommé `myBackEndPool` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="8f43b-148">Créez les règles de traduction d’adresse réseau (NAT) de trafic entrant SSH pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="8f43b-149">L’exemple suivant permet de créer deux règles d’équilibrage de charge, `myLoadBalancerRuleSSH1` et `myLoadBalancerRuleSSH2` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="8f43b-150">Créez les règles NAT entrantes Web pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="8f43b-151">L’exemple suivant permet de créer une règle d’équilibrage de charge nommée `myLoadBalancerRuleWeb` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="8f43b-152">Créez la sonde d’intégrité d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-152">Create the load balancer health probe.</span></span> <span data-ttu-id="8f43b-153">L’exemple suivant permet de créer une sonde TCP nommée `myHealthProbe` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="8f43b-154">Vérifier l’équilibreur de charge, les pools d’adresses IP et les règles NAT à l’aide de l’analyseur JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="8f43b-155">Créez la première carte d’interface réseau (NIC).</span><span class="sxs-lookup"><span data-stu-id="8f43b-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="8f43b-156">Remplacez les sections `#####-###-###` par votre propre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8f43b-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="8f43b-157">Votre ID d’abonnement est indiqué dans la sortie de **jq** lorsque vous examinez les ressources créées.</span><span class="sxs-lookup"><span data-stu-id="8f43b-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="8f43b-158">Vous pouvez également afficher votre ID d’abonnement avec `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="8f43b-159">L’exemple suivant permet de créer une carte d’interface réseau nommée `myNic1` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="8f43b-160">Créez la deuxième carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-160">Create the second NIC.</span></span> <span data-ttu-id="8f43b-161">L’exemple suivant permet de créer une carte d’interface réseau nommée `myNic2` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="8f43b-162">Vérifiez les deux cartes d’interface réseau à l’aide de l’analyseur JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="8f43b-163">Créez le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-163">Create the network security group.</span></span> <span data-ttu-id="8f43b-164">L’exemple suivant permet de créer un groupe de sécurité réseau nommé `myNetworkSecurityGroup` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="8f43b-165">Ajoutez deux règles de trafic entrant pour le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="8f43b-166">L’exemple suivant permet de créer deux règles, `myNetworkSecurityGroupRuleSSH` et `myNetworkSecurityGroupRuleHTTP` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="8f43b-167">Vérifiez le groupe de sécurité réseau et les règles de trafic entrant à l’aide de l’analyseur JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="8f43b-168">Liez le groupe de sécurité réseau aux deux cartes réseau :</span><span class="sxs-lookup"><span data-stu-id="8f43b-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="8f43b-169">Créez le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8f43b-169">Create the availability set.</span></span> <span data-ttu-id="8f43b-170">L’exemple suivant permet de créer un groupe à haute disponibilité nommé `myAvailabilitySet` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="8f43b-171">Créez la première machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="8f43b-171">Create the first Linux VM.</span></span> <span data-ttu-id="8f43b-172">L’exemple suivant permet de créer une machine virtuelle nommée `myVM1` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-172">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="8f43b-173">Créez la deuxième machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="8f43b-173">Create the second Linux VM.</span></span> <span data-ttu-id="8f43b-174">L’exemple suivant permet de créer une machine virtuelle nommée `myVM2` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-174">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="8f43b-175">Utilisez l’analyseur JSON pour vérifier tout ce qui a été créé :</span><span class="sxs-lookup"><span data-stu-id="8f43b-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="8f43b-176">Exportez votre nouvel environnement dans un modèle pour recréer rapidement des instances nouvelles :</span><span class="sxs-lookup"><span data-stu-id="8f43b-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="8f43b-177">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="8f43b-177">Detailed walkthrough</span></span>
<span data-ttu-id="8f43b-178">Les étapes détaillées qui suivent expliquent ce que chaque commande fait lorsque vous générez votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8f43b-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="8f43b-179">Ces concepts sont utiles lorsque vous créez vos propres environnements personnalisés pour le développement ou la production.</span><span class="sxs-lookup"><span data-stu-id="8f43b-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="8f43b-180">Veillez à ce que [l’interface de ligne de commande 1.0 Azure](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) soit connectée et utilise le mode Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="8f43b-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8f43b-181">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="8f43b-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8f43b-182">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="8f43b-183">Créer des groupes de ressources et choisir les emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="8f43b-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="8f43b-184">Les groupes de ressources Azure sont des entités de déploiement logiques qui contiennent des informations de configuration et des métadonnées pour permettre la gestion logique des déploiements de ressources.</span><span class="sxs-lookup"><span data-stu-id="8f43b-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="8f43b-185">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` à l’emplacement `westeurope` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="8f43b-186">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="8f43b-187">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8f43b-187">Create a storage account</span></span>
<span data-ttu-id="8f43b-188">Vous avez besoin de comptes de stockage pour vos disques de machine virtuelle et pour tous les disques de données que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="8f43b-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="8f43b-189">Vous créez des comptes de stockage presque immédiatement après avoir créé des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="8f43b-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="8f43b-190">Ici, nous utilisons la commande `azure storage account create` pour transmettre l’emplacement du compte, le groupe de ressources qui le contrôle, ainsi que le type de support de stockage souhaité.</span><span class="sxs-lookup"><span data-stu-id="8f43b-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="8f43b-191">L’exemple qui suit permet de créer un compte de stockage nommé `mystorageaccount` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="8f43b-192">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="8f43b-193">Pour examiner notre groupe de ressources à l’aide de la commande `azure group show`, nous nous servons de l’outil [jq](https://stedolan.github.io/jq/) avec l’option de ligne de commande Azure `--json`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="8f43b-194">(Vous pouvez utiliser **jsawk** ou la bibliothèque de langue de votre choix pour analyser le fichier JSON.)</span><span class="sxs-lookup"><span data-stu-id="8f43b-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8f43b-195">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="8f43b-196">Pour examiner le compte de stockage à l’aide de l’interface de ligne de commande, vous devez d’abord définir les noms de comptes et les clés.</span><span class="sxs-lookup"><span data-stu-id="8f43b-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="8f43b-197">Remplacez le nom du compte de stockage dans l’exemple suivant par le nom de votre choix :</span><span class="sxs-lookup"><span data-stu-id="8f43b-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="8f43b-198">Vous pouvez alors visualiser facilement vos informations de stockage :</span><span class="sxs-lookup"><span data-stu-id="8f43b-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="8f43b-199">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="8f43b-200">Créer un réseau virtuel et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="8f43b-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="8f43b-201">Vous allez maintenant créer un réseau virtuel dans Azure et un sous-réseau dans lesquels vous pouvez créer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="8f43b-202">L’exemple suivant permet de créer un réseau virtuel nommé `myVnet` avec le préfixe d’adresse `192.168.0.0/16` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="8f43b-203">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="8f43b-204">Là encore, nous allons utiliser l’option --json de `azure group show` et de `jq` pour examiner la façon dont nous créons nos ressources.</span><span class="sxs-lookup"><span data-stu-id="8f43b-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="8f43b-205">Nous disposons maintenant d’une ressource `storageAccounts` et d’une ressource `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8f43b-206">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="8f43b-207">À présent, créons dans le réseau virtuel `myVnet` un sous-réseau dans lequel les machines virtuelles seront déployées.</span><span class="sxs-lookup"><span data-stu-id="8f43b-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="8f43b-208">Nous utilisons la commande `azure network vnet subnet create` ainsi que les ressources que nous avons déjà créées : le groupe de ressources `myResourceGroup` et le réseau virtuel `myVnet`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="8f43b-209">Dans l’exemple suivant, nous ajoutons le sous-réseau nommé `mySubnet` avec le préfixe d’adresse de sous-réseau `192.168.1.0/24` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="8f43b-210">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="8f43b-211">Étant donné que le sous-réseau figure logiquement à l’intérieur du réseau virtuel, nous recherchons les informations de sous-réseau avec une commande légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="8f43b-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="8f43b-212">Nous utilisons la commande `azure network vnet show`, mais nous continuons à examiner la sortie JSON à l’aide de `jq`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="8f43b-213">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="8f43b-214">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="8f43b-214">Create a public IP address</span></span>
<span data-ttu-id="8f43b-215">Créons à présent l’adresse IP publique (PIP) à attribuer à votre équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="8f43b-216">Elle permet de vous connecter à vos machines virtuelles depuis Internet à l’aide de la commande `azure network public-ip create` .</span><span class="sxs-lookup"><span data-stu-id="8f43b-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="8f43b-217">Étant donné que l’adresse par défaut est dynamique, nous créons une entrée DNS nommée dans le domaine **cloudapp.azure.com** à l’aide de l’option `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="8f43b-218">L’exemple suivant permet de créer une adresse IP publique nommée `myPublicIP` avec le nom DNS de `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="8f43b-219">Étant donné que le nom DNS doit être unique, choisissez un autre nom DNS qui n’est pas susceptible d’être déjà utilisé :</span><span class="sxs-lookup"><span data-stu-id="8f43b-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="8f43b-220">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="8f43b-221">L’adresse IP publique étant également une ressource de niveau supérieur, vous pouvez la visualiser avec `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8f43b-222">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="8f43b-223">Vous pouvez examiner d’autres détails de la ressource, dont le nom de domaine complet (FQDN) du sous-domaine, en utilisant la commande `azure network public-ip show` complète.</span><span class="sxs-lookup"><span data-stu-id="8f43b-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="8f43b-224">La ressource d’adresse IP publique a été allouée de façon logique, mais aucune adresse spécifique n’a encore été attribuée.</span><span class="sxs-lookup"><span data-stu-id="8f43b-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="8f43b-225">Pour obtenir une adresse IP, vous aurez besoin d’un équilibreur de charge que nous n’avons pas encore créé.</span><span class="sxs-lookup"><span data-stu-id="8f43b-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="8f43b-226">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="8f43b-227">Créer un équilibreur de charge et des pools d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="8f43b-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="8f43b-228">Lorsque vous créez un équilibreur de charge, celui-ci vous permet de répartir le trafic entre plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="8f43b-229">Cela assure également la redondance de votre application en exécutant plusieurs machines virtuelles qui répondent aux demandes des utilisateurs en cas de maintenance ou de lourdes charges.</span><span class="sxs-lookup"><span data-stu-id="8f43b-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="8f43b-230">L’exemple suivant permet de créer un équilibrage de charge nommé `myLoadBalancer` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="8f43b-231">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="8f43b-232">Notre équilibreur de charge est relativement vide. Nous allons donc créer des pools d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8f43b-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="8f43b-233">Nous souhaitons créer deux pools d’adresses IP pour notre équilibreur de charge : une pour le pool frontal et une pour le pool principal.</span><span class="sxs-lookup"><span data-stu-id="8f43b-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="8f43b-234">Le pool d’adresses IP frontal est visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="8f43b-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="8f43b-235">Il s’agit également de l’emplacement où nous attribuons le PIP que nous avons créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8f43b-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="8f43b-236">Nous utilisons ensuite le pool principal comme emplacement auquel connecter nos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="8f43b-237">Ainsi, le trafic peut transiter via l’équilibreur de charge vers les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="8f43b-238">Commençons tout d’abord par créer notre pool d’adresses IP frontal.</span><span class="sxs-lookup"><span data-stu-id="8f43b-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="8f43b-239">L’exemple suivant permet de créer un pool frontal nommé `myFrontEndPool` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="8f43b-240">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="8f43b-241">Notez comment nous avons utilisé le commutateur `--public-ip-name` pour transmettre le `myPublicIP` créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8f43b-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="8f43b-242">L’attribution de l’adresse IP publique à l’équilibreur de charge vous permet d’atteindre vos machines virtuelles via Internet.</span><span class="sxs-lookup"><span data-stu-id="8f43b-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="8f43b-243">Nous allons maintenant créer notre deuxième pool d’adresses IP pour le trafic principal.</span><span class="sxs-lookup"><span data-stu-id="8f43b-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="8f43b-244">L’exemple suivant permet de créer un pool principal nommé `myBackEndPool` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="8f43b-245">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="8f43b-246">Nous pouvons vérifier la façon dont notre équilibreur de charge apparaît avec `azure network lb show` et en examinant la sortie JSON :</span><span class="sxs-lookup"><span data-stu-id="8f43b-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="8f43b-247">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="8f43b-248">Créer des règles NAT d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="8f43b-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="8f43b-249">Pour que le trafic transite par notre équilibrage de charge, nous devons créer des règles de traduction d’adresse réseau (NAT) spécifiant les actions entrantes ou sortantes.</span><span class="sxs-lookup"><span data-stu-id="8f43b-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="8f43b-250">Vous pouvez spécifier le protocole utilisé, puis mapper les ports externes aux ports internes comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="8f43b-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="8f43b-251">Pour notre environnement, nous allons créer des règles autorisant SSH à accéder à nos machines virtuelles par le biais de notre équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="8f43b-252">Nous configurons les ports TCP 4222 et 4223 de manière à orienter le trafic vers le port TCP 22 sur nos machines virtuelles (que nous créerons plus tard).</span><span class="sxs-lookup"><span data-stu-id="8f43b-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="8f43b-253">L’exemple suivant crée une règle nommée `myLoadBalancerRuleSSH1` pour mapper le port TCP 4222 sur le port 22 :</span><span class="sxs-lookup"><span data-stu-id="8f43b-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="8f43b-254">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="8f43b-255">Répétez cette procédure pour votre deuxième règle NAT pour le protocole SSH.</span><span class="sxs-lookup"><span data-stu-id="8f43b-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="8f43b-256">L’exemple suivant crée une règle nommée `myLoadBalancerRuleSSH2` pour mapper le port TCP 4223 sur le port 22 :</span><span class="sxs-lookup"><span data-stu-id="8f43b-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="8f43b-257">Nous allons maintenant créer une règle NAT pour le port TCP 80 du trafic web , en liant la règle à nos pools d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8f43b-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="8f43b-258">Si nous lions l’adresse à un pool d’adresses IP au lieu de la lier à nos machines virtuelles individuellement, nous pouvons ajouter ou supprimer des machines virtuelles dans le pool d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8f43b-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="8f43b-259">L’équilibrage de charge ajuste alors automatiquement le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="8f43b-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="8f43b-260">L’exemple suivant crée une règle nommée `myLoadBalancerRuleWeb` pour mapper le port TCP 80 sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="8f43b-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="8f43b-261">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="8f43b-262">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="8f43b-262">Create a load balancer health probe</span></span>
<span data-ttu-id="8f43b-263">Une sonde d’intégrité contrôle régulièrement les machines virtuelles situées derrière notre équilibreur de charge pour s’assurer qu’elles fonctionnent correctement et répondent aux demandes, telles que définies.</span><span class="sxs-lookup"><span data-stu-id="8f43b-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="8f43b-264">Dans le cas contraire, elles sont supprimées du processus pour garantir que les utilisateurs ne sont pas orientés vers elles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="8f43b-265">Vous pouvez définir les contrôles personnalisés de la sonde d’intégrité, ainsi que des valeurs d’intervalle et de délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="8f43b-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="8f43b-266">Pour plus d'informations sur les sondes d’intégrité, consultez [Sondes d’équilibreur de charge](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f43b-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8f43b-267">L’exemple suivant permet de créer une sonde d’intégrité TCP nommée `myHealthProbe` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="8f43b-268">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="8f43b-269">Ici, nous avons spécifié un intervalle de 15 secondes pour nos contrôles d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="8f43b-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="8f43b-270">Nous pouvons manquer au maximum quatre sondes (une minute) avant que l’équilibreur de charge considère que l’hôte ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="8f43b-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="8f43b-271">Vérifier l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="8f43b-271">Verify the load balancer</span></span>
<span data-ttu-id="8f43b-272">Vérifiez maintenant que la configuration de l’équilibreur de charge est terminée.</span><span class="sxs-lookup"><span data-stu-id="8f43b-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="8f43b-273">Voici la procédure que vous avez suivie :</span><span class="sxs-lookup"><span data-stu-id="8f43b-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="8f43b-274">Vous avez créé un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-274">You created a load balancer.</span></span>
2. <span data-ttu-id="8f43b-275">Vous avez créé un pool d’adresses IP frontal et lui avez affecté une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8f43b-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="8f43b-276">Vous avez créé un pool d’adresses IP principal auquel les machines virtuelles peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="8f43b-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="8f43b-277">Vous avez créé des règles NAT qui autorisent le protocole SSH pour les machines virtuelles à des fins de gestion, ainsi qu’une règle autorisant le port TCP 80 de notre application web.</span><span class="sxs-lookup"><span data-stu-id="8f43b-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="8f43b-278">Vous avez ajouté une sonde d’intégrité pour contrôler périodiquement les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="8f43b-279">Cette sonde d’intégrité s’assure que des utilisateurs n’essaient d’accéder à une machine virtuelle qui ne fonctionne plus ou qui ne sert plus de contenu.</span><span class="sxs-lookup"><span data-stu-id="8f43b-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="8f43b-280">Regardons maintenant à quoi ressemble votre équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="8f43b-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="8f43b-281">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="8f43b-282">Créer une carte d’interface réseau (NIC) à utiliser avec la machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="8f43b-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="8f43b-283">La disponibilité des cartes d’interface réseau peut être déterminée par programme car vous pouvez définir des règles régissant leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="8f43b-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="8f43b-284">Vous pouvez également avoir plusieurs cartes.</span><span class="sxs-lookup"><span data-stu-id="8f43b-284">You can also have more than one.</span></span> <span data-ttu-id="8f43b-285">Dans la commande `azure network nic create` suivante, vous avez lié la carte d’interface réseau au pool d’adresses IP principal de charge, et l’avez associée à la règle NAT pour autoriser le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="8f43b-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="8f43b-286">Remplacez les sections `#####-###-###` par votre propre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8f43b-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="8f43b-287">Votre ID d’abonnement est indiqué dans la sortie de `jq` lorsque vous examinez les ressources créées.</span><span class="sxs-lookup"><span data-stu-id="8f43b-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="8f43b-288">Vous pouvez également afficher votre ID d’abonnement avec `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="8f43b-289">L’exemple suivant permet de créer une carte d’interface réseau nommée `myNic1` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="8f43b-290">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="8f43b-291">Vous pouvez visualiser les détails de la ressource en examinant directement cette dernière.</span><span class="sxs-lookup"><span data-stu-id="8f43b-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="8f43b-292">Vous examinez la ressource à l’aide de la commande `azure network nic show` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="8f43b-293">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="8f43b-294">Nous créons maintenant la deuxième carte réseau en la liant à nouveau à notre pool d’adresses IP principal.</span><span class="sxs-lookup"><span data-stu-id="8f43b-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="8f43b-295">Cette fois, la deuxième règle NAT autorise le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="8f43b-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="8f43b-296">L’exemple suivant permet de créer une carte d’interface réseau nommée `myNic2` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="8f43b-297">Créer un groupe de sécurité réseau et les règles associées</span><span class="sxs-lookup"><span data-stu-id="8f43b-297">Create a network security group and rules</span></span>
<span data-ttu-id="8f43b-298">Nous allons à présent créer un groupe de sécurité réseau et les règles de trafic entrant qui régissent l’accès à la carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="8f43b-299">Un groupe de sécurité réseau peut être appliqué à une carte d’interface réseau ou à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="8f43b-300">Vous définissez des règles pour contrôler le flux de trafic vers et à partir de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="8f43b-301">L’exemple suivant permet de créer un groupe de sécurité réseau nommé `myNetworkSecurityGroup` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="8f43b-302">Ajoutons la règle de trafic entrant pour le groupe de sécurité réseau afin d’autoriser les connexions entrantes sur le port 22 (pour prendre en charge le protocole SSH).</span><span class="sxs-lookup"><span data-stu-id="8f43b-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="8f43b-303">L’exemple suivant permet de créer une règle nommée `myNetworkSecurityGroupRuleSSH` pour autoriser le trafic TCP sur le port 22 :</span><span class="sxs-lookup"><span data-stu-id="8f43b-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="8f43b-304">À présent, nous ajoutons la règle de trafic entrant pour le groupe de sécurité réseau afin d’autoriser les connexions entrantes sur le port 80 (pour prendre en charge le trafic web).</span><span class="sxs-lookup"><span data-stu-id="8f43b-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="8f43b-305">L’exemple suivant permet de créer une règle nommée `myNetworkSecurityGroupRuleHTTP` pour autoriser le trafic TCP sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="8f43b-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="8f43b-306">La règle de trafic entrant est un filtre pour les connexions réseau entrantes.</span><span class="sxs-lookup"><span data-stu-id="8f43b-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="8f43b-307">Dans cet exemple, nous lions le NSG à la carte d’interface réseau (NIC) virtuelle des machines virtuelles, ce qui signifie que toute demande adressée au port 22 est transmise à la carte d’interface réseau sur notre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8f43b-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="8f43b-308">Cette règle de trafic entrant concerne une connexion réseau, et non à un point de terminaison, comme dans le cas de déploiements classiques.</span><span class="sxs-lookup"><span data-stu-id="8f43b-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="8f43b-309">Pour ouvrir un port, vous devez laisser la commande `--source-port-range` définie sur « \* » (valeur par défaut) afin d’accepter les demandes entrantes de **tous** les ports demandeurs.</span><span class="sxs-lookup"><span data-stu-id="8f43b-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="8f43b-310">Ces ports sont généralement dynamiques.</span><span class="sxs-lookup"><span data-stu-id="8f43b-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="8f43b-311">Liaison avec la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="8f43b-311">Bind to the NIC</span></span>
<span data-ttu-id="8f43b-312">Liez le groupe de sécurité réseau aux cartes d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="8f43b-313">Vous devez connecter les cartes d’interface réseau avec le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="8f43b-314">Exécutez les deux commandes, pour connecter les deux cartes d’interface réseau :</span><span class="sxs-lookup"><span data-stu-id="8f43b-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="8f43b-315">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="8f43b-315">Create an availability set</span></span>
<span data-ttu-id="8f43b-316">Les groupes à haute disponibilité aident à diffuser vos machines virtuelles sur des domaines d’erreur et des domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="8f43b-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="8f43b-317">Nous allons maintenant voir comment créer un groupe à haute disponibilité pour vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="8f43b-318">L’exemple suivant permet de créer un groupe à haute disponibilité nommé `myAvailabilitySet` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="8f43b-319">Les domaines d’erreur désignent un groupe de machines virtuelles partageant une source d’alimentation et un commutateur réseau communs.</span><span class="sxs-lookup"><span data-stu-id="8f43b-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="8f43b-320">Par défaut, les machines virtuelles configurées dans votre groupe à haute disponibilité sont réparties entre trois domaines de défaillance au maximum.</span><span class="sxs-lookup"><span data-stu-id="8f43b-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="8f43b-321">Ainsi, en cas de problème matériel dans l’un de ces domaines d’erreur, aucune machine virtuelle exécutant votre application n’est affectée.</span><span class="sxs-lookup"><span data-stu-id="8f43b-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="8f43b-322">Azure distribue automatiquement les machines virtuelles sur les domaines d’erreur lorsque vous les placez dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8f43b-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="8f43b-323">Les domaines de mise à niveau indiquent les groupes de machines virtuelles et les équipements physiques sous-jacents pouvant être redémarrés en même temps.</span><span class="sxs-lookup"><span data-stu-id="8f43b-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="8f43b-324">L’ordre de redémarrage des domaines de mise à jour peut ne pas être séquentiel au cours de la maintenance planifiée, mais les mises à niveau sont redémarrées une par une.</span><span class="sxs-lookup"><span data-stu-id="8f43b-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="8f43b-325">Cette fois encore, Azure distribue automatiquement vos machines virtuelles entre les domaines de mise à niveau lorsque vous les placez dans un site de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8f43b-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="8f43b-326">Vous pouvez obtenir des informations supplémentaires sur [la gestion de la disponibilité des machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f43b-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="8f43b-327">Créer les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="8f43b-327">Create the Linux VMs</span></span>
<span data-ttu-id="8f43b-328">Vous avez créé les ressources de stockage et de réseau pour prendre en charge des machines virtuelles accessibles par Internet.</span><span class="sxs-lookup"><span data-stu-id="8f43b-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="8f43b-329">Créons maintenant ces machines virtuelles et sécurisons-les avec une clé SSH sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8f43b-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="8f43b-330">Dans ce cas précis, nous allons créer une machine virtuelle Ubuntu basée sur la dernière version LTS.</span><span class="sxs-lookup"><span data-stu-id="8f43b-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="8f43b-331">Nous recherchons les informations de cette image en utilisant `azure vm image list`, comme décrit dans [Recherche d’images de machine virtuelle Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f43b-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8f43b-332">Nous avons sélectionné une image à l’aide de la commande `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="8f43b-333">Dans ce cas, nous utilisons `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="8f43b-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="8f43b-334">Pour le dernier champ, nous passons `latest` afin de toujours obtenir la build la plus récente.</span><span class="sxs-lookup"><span data-stu-id="8f43b-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="8f43b-335">(La chaîne que nous utilisons est `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="8f43b-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="8f43b-336">Cette étape est familière à toute personne ayant déjà créé une paire de clés publique et privée SSH RSA sur Linux ou Mac à l’aide de la commande **ssh-keygen -t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="8f43b-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="8f43b-337">Si vous ne disposez pas de toutes les paires de clés de certificat dans votre répertoire `~/.ssh` , vous pouvez les créer ainsi :</span><span class="sxs-lookup"><span data-stu-id="8f43b-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="8f43b-338">Automatiquement à l’aide de l’option `azure vm create --generate-ssh-keys` .</span><span class="sxs-lookup"><span data-stu-id="8f43b-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="8f43b-339">Manuellement en suivant [les instructions pour les créer vous-même](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f43b-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8f43b-340">Vous pouvez également utiliser la méthode `--admin-password` pour authentifier vos connexions SSH une fois la machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="8f43b-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="8f43b-341">Cette méthode est généralement moins sécurisée.</span><span class="sxs-lookup"><span data-stu-id="8f43b-341">This method is typically less secure.</span></span>

<span data-ttu-id="8f43b-342">Nous créons la machine virtuelle en regroupant toutes nos ressources et informations avec la commande `azure vm create` :</span><span class="sxs-lookup"><span data-stu-id="8f43b-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="8f43b-343">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="8f43b-344">Vous pouvez alors vous connecter immédiatement à votre machine virtuelle à l’aide de vos clés SSH par défaut.</span><span class="sxs-lookup"><span data-stu-id="8f43b-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="8f43b-345">Assurez-vous de spécifier le port approprié dans la mesure où nous transitions par l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="8f43b-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="8f43b-346">(Pour notre première machine virtuelle, nous configurons la règle NAT pour transférer le port 4222 vers votre machine virtuelle.)</span><span class="sxs-lookup"><span data-stu-id="8f43b-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="8f43b-347">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="8f43b-348">Vous allez maintenant créer votre deuxième machine virtuelle en procédant de la même manière :</span><span class="sxs-lookup"><span data-stu-id="8f43b-348">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="8f43b-349">Et vous pouvez à présent utiliser la commande `azure vm show myResourceGroup myVM1` pour examiner ce que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="8f43b-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="8f43b-350">À ce stade, vous exécutez vos machines virtuelles Ubuntu derrière un équilibreur de charge dans Azure auquel vous pouvez uniquement vous connecter avec votre paire de clés SSH (car les mots de passe sont désactivés).</span><span class="sxs-lookup"><span data-stu-id="8f43b-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="8f43b-351">Vous pouvez installer nginx ou httpd, déployer une application web et voir le flux de trafic transitant par l’équilibreur de charge vers toutes les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="8f43b-352">Output:</span><span class="sxs-lookup"><span data-stu-id="8f43b-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="8f43b-353">Exportation de l’environnement en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="8f43b-353">Export the environment as a template</span></span>
<span data-ttu-id="8f43b-354">Maintenant que vous avez créé cet environnement, que se passe-t-il si vous souhaitez créer un environnement de développement supplémentaire avec les mêmes paramètres ou un environnement de production correspondant ?</span><span class="sxs-lookup"><span data-stu-id="8f43b-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="8f43b-355">Resource Manager utilise des modèles JSON qui définissent tous les paramètres pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8f43b-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="8f43b-356">Vous créez des environnements entiers en faisant référence à ce modèle JSON.</span><span class="sxs-lookup"><span data-stu-id="8f43b-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="8f43b-357">Vous pouvez [créer manuellement des modèles JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exporter un environnement existant qui créera le modèle JSON pour vous :</span><span class="sxs-lookup"><span data-stu-id="8f43b-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="8f43b-358">Cette commande crée le fichier `myResourceGroup.json` dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="8f43b-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="8f43b-359">Lorsque vous créez un environnement à partir de ce modèle, vous êtes invité à fournir les noms de toutes les ressources, dont l’équilibreur de charge, les interfaces réseau ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="8f43b-360">Vous pouvez entrer ces éléments dans votre fichier de modèle en ajoutant le paramètre `-p` ou `--includeParameterDefaultValue` à la commande `azure group export` indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8f43b-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="8f43b-361">Modifiez votre modèle JSON pour spécifier les noms de ressources, ou [créez un fichier parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui spécifie les noms de ressources.</span><span class="sxs-lookup"><span data-stu-id="8f43b-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="8f43b-362">Pour créer un nouvel environnement à partir de votre modèle :</span><span class="sxs-lookup"><span data-stu-id="8f43b-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="8f43b-363">Vous pouvez lire la section contenant [plus de détails sur le déploiement à partir de modèles](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f43b-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8f43b-364">Découvrez notamment comment mettre à jour des environnements de manière incrémentielle, utiliser le fichier de paramètres et accéder aux modèles à partir d’un emplacement de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="8f43b-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f43b-365">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f43b-365">Next steps</span></span>
<span data-ttu-id="8f43b-366">Vous voici en mesure de commencer à utiliser plusieurs composants réseau et machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8f43b-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="8f43b-367">Vous pouvez utiliser cet exemple d’environnement pour générer votre application en utilisant les composants de base présentés ici.</span><span class="sxs-lookup"><span data-stu-id="8f43b-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
