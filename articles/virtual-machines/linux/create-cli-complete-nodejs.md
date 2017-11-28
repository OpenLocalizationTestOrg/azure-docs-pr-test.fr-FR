---
title: aaaCreate un environnement Linux complet avec hello Azure CLI 1.0 | Documents Microsoft
description: "Créer des stockage, un VM Linux, un réseau virtuel et du sous-réseau, un équilibreur de charge, une carte réseau, une adresse IP publique et un groupe de sécurité réseau, tous les à partir de hello d’arrière-plan à l’aide de hello Azure CLI 1.0."
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
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="2cf21-103">Créer un environnement de Linux complète avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2cf21-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="2cf21-104">Dans cet article, nous créons un réseau simple avec un équilibreur de charge et deux machines virtuelles à des fins de développement et de calcul simple.</span><span class="sxs-lookup"><span data-stu-id="2cf21-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="2cf21-105">Nous Guide de processus de hello par commande, jusqu'à ce que vous avez deux, sécurisez toowhich les machines virtuelles Linux que vous pouvez vous connecter à partir de n’importe où sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="2cf21-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="2cf21-106">Ensuite, vous pouvez déplacer sur les environnements et les réseaux complexes toomore.</span><span class="sxs-lookup"><span data-stu-id="2cf21-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="2cf21-107">Le long de la façon de hello, vous allez découvrir la hiérarchie des dépendances hello que modèle de déploiement du Gestionnaire de ressources hello offre, et sur la quantité d’énergie il.</span><span class="sxs-lookup"><span data-stu-id="2cf21-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="2cf21-108">Une fois que vous voyez comment le système de hello est créée, vous pouvez reconstruire il beaucoup plus rapidement à l’aide de [modèles Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cf21-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2cf21-109">En outre, une fois que vous coordination des parties hello de votre environnement, la création de modèles tooautomate les devient plus facile.</span><span class="sxs-lookup"><span data-stu-id="2cf21-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="2cf21-110">environnement de Hello contient :</span><span class="sxs-lookup"><span data-stu-id="2cf21-110">hello environment contains:</span></span>

* <span data-ttu-id="2cf21-111">Deux machines virtuelles dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2cf21-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="2cf21-112">Un équilibreur de charge avec une règle d’équilibrage de charge sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="2cf21-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="2cf21-113">Les règles de groupe de sécurité réseau (NSG) tooprotect votre machine virtuelle à partir d’un trafic indésirable.</span><span class="sxs-lookup"><span data-stu-id="2cf21-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="2cf21-114">toocreate cet environnement personnalisé, vous devez hello dernières [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en mode de gestionnaire de ressources (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="2cf21-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="2cf21-115">Vous avez également besoin d’un outil d’analyse JSON.</span><span class="sxs-lookup"><span data-stu-id="2cf21-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="2cf21-116">Cet exemple utilise [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="2cf21-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2cf21-117">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="2cf21-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="2cf21-118">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2cf21-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="2cf21-119">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="2cf21-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2cf21-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="2cf21-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="2cf21-121">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="2cf21-121">Quick commands</span></span>
<span data-ttu-id="2cf21-122">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section tooupload des commandes de base un tooAzure de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2cf21-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="2cf21-123">Plus d’informations et le contexte de chaque étape se trouvent dans le reste de hello du document hello, en commençant [ici](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="2cf21-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="2cf21-124">Assurez-vous que vous avez [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) connecté et l’utilisation du mode de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="2cf21-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="2cf21-125">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2cf21-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2cf21-126">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="2cf21-127">Créer un groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-127">Create hello resource group.</span></span> <span data-ttu-id="2cf21-128">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement :</span><span class="sxs-lookup"><span data-stu-id="2cf21-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="2cf21-129">Vérifiez le groupe de ressources hello en utilisant l’analyseur JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="2cf21-130">Créer un compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-130">Create hello storage account.</span></span> <span data-ttu-id="2cf21-131">Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="2cf21-132">(nom de compte de stockage hello doit être unique, par conséquent, fournissez votre propre nom unique).</span><span class="sxs-lookup"><span data-stu-id="2cf21-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="2cf21-133">Vérifiez le compte de stockage hello en utilisant l’analyseur JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="2cf21-134">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-134">Create hello virtual network.</span></span> <span data-ttu-id="2cf21-135">Hello exemple suivant crée un réseau virtuel nommé `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="2cf21-136">Créez un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2cf21-136">Create a subnet.</span></span> <span data-ttu-id="2cf21-137">Hello exemple suivant crée un sous-réseau nommé `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="2cf21-138">Vérifiez que hello réseau et sous-réseau virtuels en utilisant l’analyseur JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="2cf21-139">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="2cf21-139">Create a public IP.</span></span> <span data-ttu-id="2cf21-140">Hello exemple suivant crée une adresse IP publique nommée `myPublicIP` portant le nom DNS de hello de `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="2cf21-141">(nom DNS de hello doit être unique, par conséquent, fournissez votre propre nom unique).</span><span class="sxs-lookup"><span data-stu-id="2cf21-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="2cf21-142">Créer un équilibreur de charge hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-142">Create hello load balancer.</span></span> <span data-ttu-id="2cf21-143">Hello exemple suivant crée un équilibreur de charge nommé `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="2cf21-144">Créer un pool IP frontal pour l’équilibrage de charge hello et associer l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="2cf21-145">Hello exemple suivant crée un pool IP frontal nommé `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="2cf21-146">Créer un pool d’IP hello principal pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="2cf21-147">Hello exemple suivant crée un pool d’IP principal nommé `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="2cf21-148">Permet de créer des règles de translation (NAT) d’adresse pour l’équilibrage de charge hello de réseau entrant de SSH.</span><span class="sxs-lookup"><span data-stu-id="2cf21-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="2cf21-149">Hello exemple suivant crée deux règles d’équilibrage de charge, `myLoadBalancerRuleSSH1` et `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="2cf21-150">Créer hello web règles NAT de trafic entrant pour hello l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="2cf21-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="2cf21-151">Hello exemple suivant crée une règle d’équilibreur de charge nommée `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="2cf21-152">Créez la sonde d’intégrité d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="2cf21-153">Hello exemple suivant crée une sonde TCP nommée `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="2cf21-154">Vérifiez hello équilibrage de charge, pools d’adresses IP et les règles NAT à l’aide d’analyseur JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="2cf21-155">Créer hello première carte d’interface réseau (NIC).</span><span class="sxs-lookup"><span data-stu-id="2cf21-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="2cf21-156">Remplacez hello `#####-###-###` sections avec votre propre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf21-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="2cf21-157">Votre abonnement ID est indiqué dans la sortie de hello de **jq** lorsque vous examinez les ressources hello vous créez.</span><span class="sxs-lookup"><span data-stu-id="2cf21-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="2cf21-158">Vous pouvez également afficher votre ID d’abonnement avec `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="2cf21-159">Hello exemple suivant crée une carte réseau nommée `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="2cf21-160">Créer hello seconde carte réseau.</span><span class="sxs-lookup"><span data-stu-id="2cf21-160">Create hello second NIC.</span></span> <span data-ttu-id="2cf21-161">Hello exemple suivant crée une carte réseau nommée `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="2cf21-162">Vérifiez que hello deux cartes d’interface réseau en utilisant l’analyseur JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="2cf21-163">Créer un groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-163">Create hello network security group.</span></span> <span data-ttu-id="2cf21-164">Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="2cf21-165">Ajoutez deux règles de trafic entrant pour le groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="2cf21-166">Hello exemple suivant crée deux règles, `myNetworkSecurityGroupRuleSSH` et `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="2cf21-167">Vérifiez le groupe de sécurité réseau hello et les règles de trafic entrant à l’aide d’analyseur JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="2cf21-168">Liaison de sécurité réseau hello toohello deux cartes d’interface réseau de groupe :</span><span class="sxs-lookup"><span data-stu-id="2cf21-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="2cf21-169">Créer un groupe à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-169">Create hello availability set.</span></span> <span data-ttu-id="2cf21-170">Hello exemple suivant crée un groupe à haute disponibilité nommée `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="2cf21-171">Créer hello première Linux VM.</span><span class="sxs-lookup"><span data-stu-id="2cf21-171">Create hello first Linux VM.</span></span> <span data-ttu-id="2cf21-172">Hello exemple suivant crée un ordinateur virtuel nommé `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-172">hello following example creates a VM named `myVM1`:</span></span>

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

<span data-ttu-id="2cf21-173">Créer hello deuxième Linux VM.</span><span class="sxs-lookup"><span data-stu-id="2cf21-173">Create hello second Linux VM.</span></span> <span data-ttu-id="2cf21-174">Hello exemple suivant crée un ordinateur virtuel nommé `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-174">hello following example creates a VM named `myVM2`:</span></span>

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

<span data-ttu-id="2cf21-175">Utilisez hello JSON analyseur tooverify que tout ce qui a été créé :</span><span class="sxs-lookup"><span data-stu-id="2cf21-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="2cf21-176">Exporter votre nouvel environnement tooa modèle tooquickly nouvelle création de nouvelles instances :</span><span class="sxs-lookup"><span data-stu-id="2cf21-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="2cf21-177">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="2cf21-177">Detailed walkthrough</span></span>
<span data-ttu-id="2cf21-178">Hello détaillées étapes qui suivent expliquent ce que chaque commande fait pendant la génération de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="2cf21-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="2cf21-179">Ces concepts sont utiles lorsque vous créez vos propres environnements personnalisés pour le développement ou la production.</span><span class="sxs-lookup"><span data-stu-id="2cf21-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="2cf21-180">Assurez-vous que vous avez [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) connecté et l’utilisation du mode de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="2cf21-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="2cf21-181">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2cf21-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2cf21-182">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="2cf21-183">Créer des groupes de ressources et choisir les emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="2cf21-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="2cf21-184">Groupes de ressources Azure sont des entités logiques de déploiement qui contiennent des informations et des métadonnées tooenable hello logique gestion de la configuration des déploiements de ressources.</span><span class="sxs-lookup"><span data-stu-id="2cf21-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="2cf21-185">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement :</span><span class="sxs-lookup"><span data-stu-id="2cf21-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="2cf21-186">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-186">Output:</span></span>

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

## <a name="create-a-storage-account"></a><span data-ttu-id="2cf21-187">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2cf21-187">Create a storage account</span></span>
<span data-ttu-id="2cf21-188">Vous avez besoin de comptes de stockage pour vos disques de machine virtuelle et les disques de données supplémentaires que vous souhaitez tooadd.</span><span class="sxs-lookup"><span data-stu-id="2cf21-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="2cf21-189">Vous créez des comptes de stockage presque immédiatement après avoir créé des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="2cf21-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="2cf21-190">Nous utilisons ici hello `azure storage account create` de commande, en passant emplacement hello du compte hello, groupe de ressources hello qui contrôle et le type hello de prise en charge de stockage souhaité.</span><span class="sxs-lookup"><span data-stu-id="2cf21-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="2cf21-191">Hello exemple suivant crée un compte de stockage nommé `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="2cf21-192">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="2cf21-193">tooexamine notre ressource de groupe à l’aide de hello `azure group show` de commande, nous allons utiliser hello [jq](https://stedolan.github.io/jq/) outil avec hello `--json` option de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf21-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="2cf21-194">(Vous pouvez utiliser **jsawk** ou n’importe quelle bibliothèque de langue que vous préférez tooparse hello JSON.)</span><span class="sxs-lookup"><span data-stu-id="2cf21-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="2cf21-195">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-195">Output:</span></span>

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

<span data-ttu-id="2cf21-196">le compte de stockage tooinvestigate hello à l’aide de hello CLI, vous devez tout d’abord clés et les noms de compte tooset hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="2cf21-197">Remplacez le nom hello hello du compte de stockage Bonjour avec un nom que vous choisissez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2cf21-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="2cf21-198">Vous pouvez alors visualiser facilement vos informations de stockage :</span><span class="sxs-lookup"><span data-stu-id="2cf21-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="2cf21-199">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="2cf21-200">Créer un réseau virtuel et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="2cf21-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="2cf21-201">Ensuite vous allez tooneed toocreate un réseau virtuel en cours d’exécution dans Azure et un sous-réseau dans lequel vous pouvez créer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="2cf21-202">Hello exemple suivant crée un réseau virtuel nommé `myVnet` avec hello `192.168.0.0/16` préfixe d’adresse :</span><span class="sxs-lookup"><span data-stu-id="2cf21-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="2cf21-203">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-203">Output:</span></span>

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

<span data-ttu-id="2cf21-204">Là encore, nous allons opter hello--json de `azure group show` et `jq` toosee comment nous mettons nos ressources.</span><span class="sxs-lookup"><span data-stu-id="2cf21-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="2cf21-205">Nous disposons maintenant d’une ressource `storageAccounts` et d’une ressource `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="2cf21-206">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-206">Output:</span></span>

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

<span data-ttu-id="2cf21-207">Maintenant nous allons créer un sous-réseau Bonjour `myVnet` réseau virtuel dans le hello machines virtuelles sont déployées.</span><span class="sxs-lookup"><span data-stu-id="2cf21-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="2cf21-208">Nous utilisons hello `azure network vnet subnet create` commande, ainsi que des ressources hello, nous avons déjà créé : hello `myResourceGroup` groupe de ressources et hello `myVnet` réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2cf21-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="2cf21-209">Bonjour l’exemple suivant, nous ajoutons sous-réseau hello nommé `mySubnet` avec un préfixe d’adresse de sous-réseau hello `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="2cf21-210">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="2cf21-211">Étant donné que le sous-réseau de hello est logiquement à l’intérieur du réseau virtuel de hello, nous allons pour plus d’informations de sous-réseau hello avec une commande légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="2cf21-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="2cf21-212">Nous utilisons la commande Hello est `azure network vnet show`, mais nous continuons la sortie JSON hello tooexamine à l’aide de `jq`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="2cf21-213">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-213">Output:</span></span>

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

## <a name="create-a-public-ip-address"></a><span data-ttu-id="2cf21-214">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="2cf21-214">Create a public IP address</span></span>
<span data-ttu-id="2cf21-215">Maintenant nous allons créer hello adresse IP publique (PIP) que nous affectons d’équilibrage de charge tooyour.</span><span class="sxs-lookup"><span data-stu-id="2cf21-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="2cf21-216">Il vous permet de tooconnect tooyour machines virtuelles à partir de hello Internet à l’aide de hello `azure network public-ip create` commande.</span><span class="sxs-lookup"><span data-stu-id="2cf21-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="2cf21-217">Étant donné que l’adresse par défaut de hello est dynamique, nous créons une entrée DNS nommée Bonjour **cloudapp.azure.com** domaine à l’aide de hello `--domain-name-label` option.</span><span class="sxs-lookup"><span data-stu-id="2cf21-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="2cf21-218">Hello exemple suivant crée une adresse IP publique nommée `myPublicIP` portant le nom DNS de hello de `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="2cf21-219">Étant donné que le nom DNS de hello doit être unique, vous fournissez votre propre nom DNS unique :</span><span class="sxs-lookup"><span data-stu-id="2cf21-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="2cf21-220">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
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

<span data-ttu-id="2cf21-221">Bonjour adresse IP publique est également une ressource de niveau supérieur, afin de voir avec `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="2cf21-222">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-222">Output:</span></span>

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

<span data-ttu-id="2cf21-223">Vous pouvez rechercher plus d’informations de ressources, notamment le nom de domaine complet (FQDN) hello du sous-domaine de hello, à l’aide de hello complète `azure network public-ip show` commande.</span><span class="sxs-lookup"><span data-stu-id="2cf21-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="2cf21-224">ressource d’adresse IP publique Hello a été allouée logiquement, mais une adresse spécifique n’a pas encore été assignée.</span><span class="sxs-lookup"><span data-stu-id="2cf21-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="2cf21-225">tooobtain une adresse IP, vous allez tooneed un équilibreur de charge, nous n’avons pas encore créé.</span><span class="sxs-lookup"><span data-stu-id="2cf21-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="2cf21-226">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-226">Output:</span></span>

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

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="2cf21-227">Créer un équilibreur de charge et des pools d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="2cf21-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="2cf21-228">Lorsque vous créez un équilibreur de charge, il vous permet de toodistribute du trafic entre plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="2cf21-229">Il fournit également l’application tooyour de redondance en exécutant plusieurs machines virtuelles qui répondent toouser des demandes dans l’événement hello de maintenance ou de lourdes charges.</span><span class="sxs-lookup"><span data-stu-id="2cf21-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="2cf21-230">Hello exemple suivant crée un équilibreur de charge nommé `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="2cf21-231">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="2cf21-232">Notre équilibreur de charge est relativement vide. Nous allons donc créer des pools d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="2cf21-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="2cf21-233">Nous souhaitons toocreate deux pools d’adresses IP pour notre programme d’équilibrage de charge, un serveur frontal hello et un pour le back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="2cf21-234">pool d’adresses IP frontal Hello est visible publiquement.</span><span class="sxs-lookup"><span data-stu-id="2cf21-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="2cf21-235">Il est également toowhich d’emplacement hello que nous affectons hello PIP que nous avons créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="2cf21-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="2cf21-236">Puis nous utiliser hello principal comme un emplacement pour notre tooconnect de machines virtuelles à.</span><span class="sxs-lookup"><span data-stu-id="2cf21-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="2cf21-237">De cette façon, hello circulent via toohello équilibrage de charge hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="2cf21-238">Commençons tout d’abord par créer notre pool d’adresses IP frontal.</span><span class="sxs-lookup"><span data-stu-id="2cf21-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="2cf21-239">Hello exemple suivant crée un pool frontal nommé `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="2cf21-240">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="2cf21-241">Notez comment nous avons utilisé hello `--public-ip-name` commutateur toopass Bonjour `myPublicIP` que nous avons créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="2cf21-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="2cf21-242">Affectation d’adresse IP publique hello équilibrage de charge adresse toohello vous permet de tooreach vos machines virtuelles entre hello Internet.</span><span class="sxs-lookup"><span data-stu-id="2cf21-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="2cf21-243">Nous allons maintenant créer notre deuxième pool d’adresses IP pour le trafic principal.</span><span class="sxs-lookup"><span data-stu-id="2cf21-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="2cf21-244">Hello exemple suivant crée un pool principal nommé `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="2cf21-245">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="2cf21-246">Nous pouvons voir faire de notre programme d’équilibrage de charge en consultant avec `azure network lb show` et en examinant la sortie JSON hello :</span><span class="sxs-lookup"><span data-stu-id="2cf21-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="2cf21-247">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-247">Output:</span></span>

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

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="2cf21-248">Créer des règles NAT d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="2cf21-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="2cf21-249">tout trafic tooget via notre programme d’équilibrage de charge, nous avons besoin de règles toocreate réseau adresse translation (NAT) qui spécifient les actions entrantes ou sortantes.</span><span class="sxs-lookup"><span data-stu-id="2cf21-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="2cf21-250">Vous pouvez spécifier hello protocole toouse, puis mapper les ports de toointernal des ports externes comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2cf21-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="2cf21-251">Pour notre environnement, nous allons créer des règles qui autorisent SSH via notre tooour d’équilibrage de charge machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="2cf21-252">Nous avons configuré le port TCP ports 4222 et 4223 toodirect tooTCP 22 sur nos machines virtuelles (ce qui nous créer ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="2cf21-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="2cf21-253">Hello exemple suivant crée une règle nommée `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22 :</span><span class="sxs-lookup"><span data-stu-id="2cf21-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="2cf21-254">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
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

<span data-ttu-id="2cf21-255">Répétez la procédure de hello pour votre deuxième règle NAT pour SSH.</span><span class="sxs-lookup"><span data-stu-id="2cf21-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="2cf21-256">Hello exemple suivant crée une règle nommée `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22 :</span><span class="sxs-lookup"><span data-stu-id="2cf21-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="2cf21-257">Nous allons également continuer et créer une règle NAT pour le port TCP 80 pour le trafic web, raccorder les règle hello tooour pools d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="2cf21-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="2cf21-258">Si nous raccorder hello règle tooan de pool IP, au lieu de raccorder hello règle tooour machines virtuelles individuellement, nous pouvons ajouter ou supprimer des machines virtuelles à partir du pool d’adresses IP hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="2cf21-259">équilibrage de charge Hello ajuste automatiquement le flux hello du trafic.</span><span class="sxs-lookup"><span data-stu-id="2cf21-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="2cf21-260">Hello exemple suivant crée une règle nommée `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80 :</span><span class="sxs-lookup"><span data-stu-id="2cf21-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="2cf21-261">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
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

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="2cf21-262">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="2cf21-262">Create a load balancer health probe</span></span>
<span data-ttu-id="2cf21-263">Un contrôle d’intégrité de sonde périodiquement les vérifications sur hello machines virtuelles qui se trouvent derrière notre toomake d’équilibrage de charge que leur date d’exploitation et de répondre toorequests tel que défini.</span><span class="sxs-lookup"><span data-stu-id="2cf21-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="2cf21-264">Si non, ils sont supprimés de tooensure opération que les utilisateurs ne sont pas en cours dirigé toothem.</span><span class="sxs-lookup"><span data-stu-id="2cf21-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="2cf21-265">Vous pouvez définir des contrôles personnalisés pour la sonde d’intégrité hello, ainsi que les intervalles et les valeurs de délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="2cf21-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="2cf21-266">Pour plus d'informations sur les sondes d’intégrité, consultez [Sondes d’équilibreur de charge](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cf21-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2cf21-267">Hello exemple suivant crée un TCP intégrité détectés nommée `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="2cf21-268">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="2cf21-269">Ici, nous avons spécifié un intervalle de 15 secondes pour nos contrôles d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="2cf21-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="2cf21-270">Nous pouvons ne pas conforme à un maximum de quatre sondes (une minute) avant de l’équilibrage de charge hello considère que cet hôte hello ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="2cf21-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="2cf21-271">Vérifiez l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="2cf21-271">Verify hello load balancer</span></span>
<span data-ttu-id="2cf21-272">Configuration d’équilibrage de charge de hello est maintenant terminée.</span><span class="sxs-lookup"><span data-stu-id="2cf21-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="2cf21-273">Voici les étapes hello que vous avez suivies :</span><span class="sxs-lookup"><span data-stu-id="2cf21-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="2cf21-274">Vous avez créé un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="2cf21-274">You created a load balancer.</span></span>
2. <span data-ttu-id="2cf21-275">Vous créé un pool IP frontal et affecté un tooit IP public.</span><span class="sxs-lookup"><span data-stu-id="2cf21-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="2cf21-276">Vous avez créé un pool d’adresses IP principal auquel les machines virtuelles peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="2cf21-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="2cf21-277">Vous avez créé des règles NAT qui autorisent les machines virtuelles toohello SSH pour la gestion, ainsi que d’une règle qui autorise le port TCP 80 pour notre application web.</span><span class="sxs-lookup"><span data-stu-id="2cf21-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="2cf21-278">Vous avez ajouté un Bonjour de vérification d’intégrité sonde tooperiodically machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="2cf21-279">Cette sonde d’intégrité permet de s’assurer que les utilisateurs n’essaient pas tooaccess une machine virtuelle qui n’est plus fonctionne ni héberger un contenu.</span><span class="sxs-lookup"><span data-stu-id="2cf21-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="2cf21-280">Regardons maintenant à quoi ressemble votre équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="2cf21-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="2cf21-281">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-281">Output:</span></span>

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

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="2cf21-282">Créer une carte réseau toouse avec hello Linux VM</span><span class="sxs-lookup"><span data-stu-id="2cf21-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="2cf21-283">Cartes réseau est disponibles par programme, car vous pouvez appliquer des règles tootheir utilisation.</span><span class="sxs-lookup"><span data-stu-id="2cf21-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="2cf21-284">Vous pouvez également avoir plusieurs cartes.</span><span class="sxs-lookup"><span data-stu-id="2cf21-284">You can also have more than one.</span></span> <span data-ttu-id="2cf21-285">Suivant de hello `azure network nic create` de commande, vous raccordez le pool d’adresses IP hello NIC toohello charge principal et l’associez à hello NAT règle toopermit SSH du trafic.</span><span class="sxs-lookup"><span data-stu-id="2cf21-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="2cf21-286">Remplacez hello `#####-###-###` sections avec votre propre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf21-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="2cf21-287">Votre abonnement ID est indiqué dans la sortie de hello de `jq` lorsque vous examinez les ressources hello vous créez.</span><span class="sxs-lookup"><span data-stu-id="2cf21-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="2cf21-288">Vous pouvez également afficher votre ID d’abonnement avec `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="2cf21-289">Hello exemple suivant crée une carte réseau nommée `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="2cf21-290">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
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

<span data-ttu-id="2cf21-291">Vous pouvez afficher les détails de hello en examinant les ressources hello directement.</span><span class="sxs-lookup"><span data-stu-id="2cf21-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="2cf21-292">Vous examinez les ressources hello à l’aide de hello `azure network nic show` commande :</span><span class="sxs-lookup"><span data-stu-id="2cf21-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="2cf21-293">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-293">Output:</span></span>

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

<span data-ttu-id="2cf21-294">Maintenant nous créons hello seconde carte réseau, raccorder à nouveau dans le pool d’adresses IP tooour back-end.</span><span class="sxs-lookup"><span data-stu-id="2cf21-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="2cf21-295">Cette règle NAT hello deuxième autorise le trafic SSH.</span><span class="sxs-lookup"><span data-stu-id="2cf21-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="2cf21-296">Hello exemple suivant crée une carte réseau nommée `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="2cf21-297">Créer un groupe de sécurité réseau et les règles associées</span><span class="sxs-lookup"><span data-stu-id="2cf21-297">Create a network security group and rules</span></span>
<span data-ttu-id="2cf21-298">Désormais nous créer un groupe de sécurité réseau, hello des règles de trafic entrant qui régissent l’accès toohello carte</span><span class="sxs-lookup"><span data-stu-id="2cf21-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="2cf21-299">Un groupe de sécurité réseau peut être appliqué tooa carte réseau ou sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2cf21-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="2cf21-300">Vous définissez un flux de hello toocontrol de règles de trafic vers et depuis vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="2cf21-301">Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="2cf21-302">Vous allez ajouter la règle de trafic entrant hello pour hello NSG tooallow connexions sur le port 22 (toosupport SSH) entrantes.</span><span class="sxs-lookup"><span data-stu-id="2cf21-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="2cf21-303">Hello exemple suivant crée une règle nommée `myNetworkSecurityGroupRuleSSH` tooallow TCP sur le port 22 :</span><span class="sxs-lookup"><span data-stu-id="2cf21-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="2cf21-304">Maintenant vous allez ajouter la règle de trafic entrant hello pour hello NSG tooallow connexions sur le port 80 (trafic web de toosupport) entrantes.</span><span class="sxs-lookup"><span data-stu-id="2cf21-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="2cf21-305">Hello exemple suivant crée une règle nommée `myNetworkSecurityGroupRuleHTTP` tooallow TCP sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="2cf21-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="2cf21-306">règle de trafic entrant Hello est un filtre pour les connexions réseau entrantes.</span><span class="sxs-lookup"><span data-stu-id="2cf21-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="2cf21-307">Dans cet exemple, nous lions hello NSG toohello machines virtuelles carte réseau virtuelle, ce qui signifie que n’importe quel tooport demande 22 est passée via toohello carte réseau sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2cf21-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="2cf21-308">Cette règle de trafic entrant concerne une connexion réseau, et non à un point de terminaison, comme dans le cas de déploiements classiques.</span><span class="sxs-lookup"><span data-stu-id="2cf21-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="2cf21-309">tooopen un port, vous devez laisser hello `--source-port-range` défini trop '\*' (valeur par défaut de hello) tooaccept les demandes d’entrantes **n’importe quel** port de demande.</span><span class="sxs-lookup"><span data-stu-id="2cf21-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="2cf21-310">Ces ports sont généralement dynamiques.</span><span class="sxs-lookup"><span data-stu-id="2cf21-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="2cf21-311">Lier toohello carte réseau</span><span class="sxs-lookup"><span data-stu-id="2cf21-311">Bind toohello NIC</span></span>
<span data-ttu-id="2cf21-312">Lier hello NSG toohello cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="2cf21-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="2cf21-313">Nous avons besoin de ses cartes réseau tooconnect à notre groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="2cf21-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="2cf21-314">Exécutez les deux commandes, toohook des deux de ses cartes réseau :</span><span class="sxs-lookup"><span data-stu-id="2cf21-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="2cf21-315">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="2cf21-315">Create an availability set</span></span>
<span data-ttu-id="2cf21-316">Les groupes à haute disponibilité aident à diffuser vos machines virtuelles sur des domaines d’erreur et des domaines de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="2cf21-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="2cf21-317">Nous allons maintenant voir comment créer un groupe à haute disponibilité pour vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="2cf21-318">Hello exemple suivant crée un groupe à haute disponibilité nommée `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="2cf21-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="2cf21-319">Les domaines d’erreur désignent un groupe de machines virtuelles partageant une source d’alimentation et un commutateur réseau communs.</span><span class="sxs-lookup"><span data-stu-id="2cf21-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="2cf21-320">Par défaut, hello virtuels qui sont configurés au sein de votre jeu de disponibilité sont séparées à travers des domaines d’erreur toothree.</span><span class="sxs-lookup"><span data-stu-id="2cf21-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="2cf21-321">Hello est qu’un problème matériel dans un de ces domaines d’erreur n’affecte pas de chaque machine virtuelle qui exécute votre application.</span><span class="sxs-lookup"><span data-stu-id="2cf21-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="2cf21-322">Azure distribue automatiquement les machines virtuelles entre les domaines d’erreur hello lorsque vous les placez dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2cf21-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="2cf21-323">Indiquent les domaines de mise à niveau des ordinateurs virtuels et le matériel physique sous-jacent qui peut être redémarré à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="2cf21-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="2cf21-324">commande Hello dans lequel les domaines de mise à niveau sont redémarrés peut ne pas être séquentiel pendant les maintenances, mais la mise à niveau qu’un seul est redémarré à la fois.</span><span class="sxs-lookup"><span data-stu-id="2cf21-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="2cf21-325">Cette fois encore, Azure distribue automatiquement vos machines virtuelles entre les domaines de mise à niveau lorsque vous les placez dans un site de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2cf21-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="2cf21-326">En savoir plus sur [gestion de la disponibilité de hello de machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cf21-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="2cf21-327">Créer des machines virtuelles Linux hello</span><span class="sxs-lookup"><span data-stu-id="2cf21-327">Create hello Linux VMs</span></span>
<span data-ttu-id="2cf21-328">Vous avez créé des ressources de stockage et réseau hello machines virtuelles de toosupport accessible via Internet.</span><span class="sxs-lookup"><span data-stu-id="2cf21-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="2cf21-329">Créons maintenant ces machines virtuelles et sécurisons-les avec une clé SSH sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2cf21-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="2cf21-330">Dans ce cas, nous allons toocreate une VM Ubuntu selon hello LTS plus récente.</span><span class="sxs-lookup"><span data-stu-id="2cf21-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="2cf21-331">Nous recherchons les informations de cette image en utilisant `azure vm image list`, comme décrit dans [Recherche d’images de machine virtuelle Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cf21-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2cf21-332">Nous avons sélectionné une image à l’aide de commande hello `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="2cf21-333">Dans ce cas, nous utilisons `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="2cf21-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="2cf21-334">Pour le dernier champ de hello, nous passons `latest` afin que dans les futures hello, nous obtenons toujours build la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="2cf21-335">(nous utilisons la chaîne hello est `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="2cf21-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="2cf21-336">Cette étape est familier tooanyone qui a déjà créé un ssh rsa publique et privée paire de clés sur Linux ou Mac à l’aide de **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="2cf21-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="2cf21-337">Si vous ne disposez pas de toutes les paires de clés de certificat dans votre répertoire `~/.ssh` , vous pouvez les créer ainsi :</span><span class="sxs-lookup"><span data-stu-id="2cf21-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="2cf21-338">Automatiquement, à l’aide de hello `azure vm create --generate-ssh-keys` option.</span><span class="sxs-lookup"><span data-stu-id="2cf21-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="2cf21-339">Manuellement, à l’aide [hello instructions toocreate les vous-même](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cf21-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2cf21-340">Vous pouvez également utiliser hello `--admin-password` méthode tooauthenticate vos connexions SSH après hello machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="2cf21-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="2cf21-341">Cette méthode est généralement moins sécurisée.</span><span class="sxs-lookup"><span data-stu-id="2cf21-341">This method is typically less secure.</span></span>

<span data-ttu-id="2cf21-342">Nous créons hello machine virtuelle en rassemblant tous nos ressources et informations avec hello `azure vm create` commande :</span><span class="sxs-lookup"><span data-stu-id="2cf21-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

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

<span data-ttu-id="2cf21-343">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="2cf21-344">Vous pouvez connecter tooyour VM immédiatement à l’aide de vos clés SSH par défaut.</span><span class="sxs-lookup"><span data-stu-id="2cf21-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="2cf21-345">Assurez-vous que vous spécifiez le port approprié de hello dans la mesure où nous transmettons via l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="2cf21-346">(Pour notre premier ordinateur virtuel, nous configurons hello NAT règle tooforward port 4222 tooour machine virtuelle.)</span><span class="sxs-lookup"><span data-stu-id="2cf21-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="2cf21-347">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="2cf21-348">Pour commencer, créez votre deuxième machine virtuelle Bonjour même manière :</span><span class="sxs-lookup"><span data-stu-id="2cf21-348">Go ahead and create your second VM in hello same manner:</span></span>

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

<span data-ttu-id="2cf21-349">Et vous pouvez maintenant utiliser hello `azure vm show myResourceGroup myVM1` commande tooexamine à ce que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="2cf21-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="2cf21-350">À ce stade, vous exécutez vos machines virtuelles Ubuntu derrière un équilibreur de charge dans Azure auquel vous pouvez uniquement vous connecter avec votre paire de clés SSH (car les mots de passe sont désactivés).</span><span class="sxs-lookup"><span data-stu-id="2cf21-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="2cf21-351">Vous pouvez installer nginx ou httpd, déployer une application web et voir hello trafic circule tooboth d’équilibrage de charge hello de machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="2cf21-352">Output:</span><span class="sxs-lookup"><span data-stu-id="2cf21-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
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


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="2cf21-353">Environnement de hello d’exportation en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="2cf21-353">Export hello environment as a template</span></span>
<span data-ttu-id="2cf21-354">Maintenant que vous avez créé à cet environnement, que se passe-t-il si vous souhaitez toocreate à un environnement de développement supplémentaire avec hello mêmes paramètres, ou un environnement de production qui lui correspond ?</span><span class="sxs-lookup"><span data-stu-id="2cf21-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="2cf21-355">Le Gestionnaire de ressources utilise des modèles JSON qui définissent tous les paramètres de hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="2cf21-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="2cf21-356">Vous créez des environnements entiers en faisant référence à ce modèle JSON.</span><span class="sxs-lookup"><span data-stu-id="2cf21-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="2cf21-357">Vous pouvez [créer manuellement des modèles JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exporter un modèle JSON environnement toocreate hello existant pour vous :</span><span class="sxs-lookup"><span data-stu-id="2cf21-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="2cf21-358">Cette commande crée hello `myResourceGroup.json` fichier dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="2cf21-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="2cf21-359">Lorsque vous créez un environnement à partir de ce modèle, vous êtes invité pour tous les noms de ressource hello, y compris les noms de hello pour l’équilibrage de charge hello, les interfaces réseau ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="2cf21-360">Vous pouvez remplir ces noms dans votre fichier de modèle en ajoutant hello `-p` ou `--includeParameterDefaultValue` paramètre toohello `azure group export` commande qui a été indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="2cf21-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="2cf21-361">Modifier les noms de ressources JSON modèle toospecify hello, ou [créer un fichier parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui spécifie les noms de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2cf21-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="2cf21-362">toocreate un environnement à partir de votre modèle :</span><span class="sxs-lookup"><span data-stu-id="2cf21-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="2cf21-363">Vous souhaiterez peut-être tooread [plus sur la façon toodeploy à partir de modèles](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cf21-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2cf21-364">Découvrez comment tooincrementally les environnements de mise à jour, utilisez le fichier de paramètres hello et accéder aux modèles à partir d’un emplacement de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="2cf21-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cf21-365">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2cf21-365">Next steps</span></span>
<span data-ttu-id="2cf21-366">Vous êtes maintenant prêt toobegin utilisation de plusieurs composants réseau et les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2cf21-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="2cf21-367">Vous pouvez utiliser cette toobuild d’environnement exemple votre application à l’aide de composants hello introduits ici.</span><span class="sxs-lookup"><span data-stu-id="2cf21-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
