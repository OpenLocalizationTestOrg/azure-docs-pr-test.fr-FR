---
title: "aaaHow tooload équilibrer les ordinateurs virtuels Linux dans Azure | Documents Microsoft"
description: "Découvrez comment toouse hello Azure charge équilibrage toocreate une application hautement disponible et sécurisée entre trois machines virtuelles de Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="bb085-103">Comment tooload équilibrer les ordinateurs virtuels Linux dans Azure toocreate une application hautement disponible</span><span class="sxs-lookup"><span data-stu-id="bb085-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="bb085-104">L’équilibrage de charge offre un niveau plus élevé de disponibilité en répartissant les demandes entrantes sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bb085-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="bb085-105">Dans ce didacticiel, vous découvrez hello différents composants d’équilibrage de charge Azure hello de distribuer le trafic et fournissant une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="bb085-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="bb085-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb085-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb085-107">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="bb085-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="bb085-108">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="bb085-109">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="bb085-110">Utiliser le nuage-init toocreate une application Node.js de base</span><span class="sxs-lookup"><span data-stu-id="bb085-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="bb085-111">Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa</span><span class="sxs-lookup"><span data-stu-id="bb085-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="bb085-112">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="bb085-112">View a load balancer in action</span></span>
> * <span data-ttu-id="bb085-113">Ajouter et supprimer des machines virtuelles d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bb085-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bb085-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bb085-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="bb085-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bb085-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb085-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="bb085-117">Vue d’ensemble de l’équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="bb085-117">Azure load balancer overview</span></span>
<span data-ttu-id="bb085-118">Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines.</span><span class="sxs-lookup"><span data-stu-id="bb085-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="bb085-119">Une sonde d’intégrité d’équilibrage de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="bb085-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="bb085-120">Vous définissez une configuration IP frontale qui contient une ou plusieurs adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="bb085-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="bb085-121">Cette configuration IP frontale permet à votre toobe d’applications et d’équilibrage de charge accessible sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="bb085-122">Machines virtuelles se connecter tooa équilibrage de charge à l’aide de leur carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="bb085-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="bb085-123">toohello du trafic toodistribute machines virtuelles, un pool d’adresses de serveur principal contient des adresses IP de hello d’équilibrage de charge hello virtuelle (NIC) connectées toohello.</span><span class="sxs-lookup"><span data-stu-id="bb085-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="bb085-124">flux de hello toocontrol du trafic, vous définissez des règles d’équilibrage de charge pour les ports et protocoles qui mappent des machines virtuelles de tooyour spécifiques.</span><span class="sxs-lookup"><span data-stu-id="bb085-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="bb085-125">Si vous avez suivi les didacticiel précédent hello trop[créer un ensemble d’échelle de machine virtuelle](tutorial-create-vmss.md), un équilibreur de charge a été créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="bb085-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="bb085-126">Tous ces composants ont été configurées dans le cadre de l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="bb085-127">Créer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="bb085-127">Create Azure load balancer</span></span>
<span data-ttu-id="bb085-128">Cette section décrit en détail comment vous pouvez créer et configurer chaque composant d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="bb085-129">Pour pouvoir créer votre équilibreur de charge, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bb085-130">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupLoadBalancer* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="bb085-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="bb085-131">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="bb085-131">Create a public IP address</span></span>
<span data-ttu-id="bb085-132">tooaccess votre application sur hello Internet, vous avez besoin d’une adresse IP publique pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="bb085-133">Créez une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="bb085-134">Hello exemple suivant crée une adresse IP publique nommée *myPublicIP* Bonjour *myResourceGroupLoadBalancer* groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="bb085-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="bb085-135">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-135">Create a load balancer</span></span>
<span data-ttu-id="bb085-136">Créez un équilibrage de charge avec la commande [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="bb085-137">Hello exemple suivant crée un équilibreur de charge nommé *myLoadBalancer* et assigne hello *myPublicIP* configuration IP frontale de l’adresse toohello :</span><span class="sxs-lookup"><span data-stu-id="bb085-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="bb085-138">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="bb085-138">Create a health probe</span></span>
<span data-ttu-id="bb085-139">tooallow hello équilibrage toomonitor hello l’état de charge de votre application, vous utilisez une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="bb085-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="bb085-140">Sonde d’intégrité Hello dynamiquement ajoute ou supprime des machines virtuelles à partir de la rotation d’équilibrage de charge hello en fonction de leurs contrôles toohealth de réponse.</span><span class="sxs-lookup"><span data-stu-id="bb085-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="bb085-141">Par défaut, un ordinateur virtuel est supprimé de la distribution d’équilibrage de charge hello après deux défaillances consécutives à des intervalles de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="bb085-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="bb085-142">Vous créez une sonde d’intégrité selon un protocole ou une page de vérification d’intégrité spécifique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bb085-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="bb085-143">Bonjour à l’exemple suivant crée une sonde TCP.</span><span class="sxs-lookup"><span data-stu-id="bb085-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="bb085-144">Vous pouvez également créer des sondes HTTP personnalisées pour des contrôles d’intégrité plus affinés.</span><span class="sxs-lookup"><span data-stu-id="bb085-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="bb085-145">Lorsque vous utilisez une sonde HTTP personnalisée, vous devez créer page vérifier l’intégrité hello, tel que *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="bb085-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="bb085-146">Sonde de Hello doit retourner un **HTTP 200 OK** réponse pour hello charge équilibrage tookeep hello hôte en rotation.</span><span class="sxs-lookup"><span data-stu-id="bb085-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="bb085-147">toocreate une sonde d’intégrité TCP, vous utilisez [sonde d’équilibrage de charge réseau az créer](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="bb085-148">Hello exemple suivant crée une sonde d’intégrité nommée *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="bb085-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="bb085-149">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-149">Create a load balancer rule</span></span>
<span data-ttu-id="bb085-150">Une règle d’équilibreur de charge est utilisé toodefine comment le trafic est distribué toohello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bb085-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="bb085-151">Vous définissez la configuration IP frontale de hello pour le trafic entrant de hello et hello principal pool tooreceive hello du trafic IP, ainsi que les sources requis hello et port de destination.</span><span class="sxs-lookup"><span data-stu-id="bb085-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="bb085-152">toomake que seuls les ordinateurs virtuels sains recevoir du trafic, vous définissez également toouse de sonde d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="bb085-153">Utilisez [az network lb rule create](/cli/azure/network/lb/rule#create) pour créer une règle d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="bb085-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="bb085-154">Hello exemple suivant crée une règle nommée *myLoadBalancerRule*, utilise hello *myHealthProbe* sonde d’intégrité et équilibre le trafic sur le port *80*:</span><span class="sxs-lookup"><span data-stu-id="bb085-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="bb085-155">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bb085-155">Configure virtual network</span></span>
<span data-ttu-id="bb085-156">Avant de déployer des machines virtuelles et tester votre programme d’équilibrage, créer hello prenant en charge des ressources du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="bb085-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="bb085-157">Pour plus d’informations sur les réseaux virtuels, consultez hello [gérer les réseaux virtuels Azure](tutorial-virtual-network.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bb085-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="bb085-158">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="bb085-158">Create network resources</span></span>
<span data-ttu-id="bb085-159">Créez un réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="bb085-160">Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec un sous-réseau nommé *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="bb085-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="bb085-161">tooadd un groupe de sécurité réseau, vous utilisez [az réseau nsg créer](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="bb085-162">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="bb085-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="bb085-163">Créez une règle de groupe de sécurité réseau avec la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="bb085-164">Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="bb085-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="bb085-165">Les cartes d’interface réseau virtuelles sont créées avec la commande [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="bb085-166">Hello exemple suivant crée trois cartes réseau virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bb085-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="bb085-167">(Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes).</span><span class="sxs-lookup"><span data-stu-id="bb085-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="bb085-168">Vous pouvez créer des cartes réseau virtuelles supplémentaires et des machines virtuelles à tout moment et ajoutez-les à équilibrage de charge toohello :</span><span class="sxs-lookup"><span data-stu-id="bb085-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="bb085-169">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bb085-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="bb085-170">Créer une configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="bb085-170">Create cloud-init config</span></span>
<span data-ttu-id="bb085-171">Dans un didacticiel précédent sur [comment toocustomize une machine virtuelle de Linux au premier démarrage](tutorial-automate-vm-deployment.md), vous avez appris comment personnalisation tooautomate avec init-cloud.</span><span class="sxs-lookup"><span data-stu-id="bb085-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="bb085-172">Vous pouvez utiliser hello même tooinstall fichier de configuration cloud-init NGINX et exécuter une application Node.js de « Hello World » simple.</span><span class="sxs-lookup"><span data-stu-id="bb085-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="bb085-173">Dans votre environnement actuel, créez un fichier nommé *cloud-init.txt* et coller hello de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="bb085-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="bb085-174">Par exemple, créer le fichier de hello Bonjour Cloud Shell pas sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="bb085-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="bb085-175">Entrez `sensible-editor cloud-init.txt` toocreate hello fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="bb085-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="bb085-176">Assurez-vous que ce fichier d’ensemble cloud-init hello est copié correctement, en particulier hello première ligne :</span><span class="sxs-lookup"><span data-stu-id="bb085-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="bb085-177">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bb085-177">Create virtual machines</span></span>
<span data-ttu-id="bb085-178">tooimprove hello haute disponibilité de votre application, placez vos machines virtuelles dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="bb085-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="bb085-179">Pour plus d’informations sur les groupes à haute disponibilité, consultez hello précédente [comment les ordinateurs virtuels hautement disponibles toocreate](tutorial-availability-sets.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bb085-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="bb085-180">Créez un groupe à haute disponibilité avec la commande [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="bb085-181">Hello exemple suivant crée un groupe à haute disponibilité nommée *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="bb085-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="bb085-182">Vous pouvez désormais créer VMs hello avec [az vm créer](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bb085-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bb085-183">Hello exemple suivant crée trois machines virtuelles et génère des clés SSH s’ils n’existent pas déjà :</span><span class="sxs-lookup"><span data-stu-id="bb085-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="bb085-184">Il existe des tâches en arrière-plan qui continuer toorun après que hello CLI d’Azure vous renvoie toohello invite.</span><span class="sxs-lookup"><span data-stu-id="bb085-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="bb085-185">Hello `--no-wait` paramètre n’attend pas pour tous les hello toocomplete de tâches.</span><span class="sxs-lookup"><span data-stu-id="bb085-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="bb085-186">Il peut être une ou deux minutes avant que vous pouvez accéder à application hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="bb085-187">Hello sonde d’intégrité d’équilibrage de charge détecte automatiquement lors de l’application hello est en cours d’exécution sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb085-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="bb085-188">Une fois que l’application hello est en cours d’exécution, règle d’équilibrage de charge hello démarre le trafic de toodistribute.</span><span class="sxs-lookup"><span data-stu-id="bb085-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="bb085-189">Tester l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-189">Test load balancer</span></span>
<span data-ttu-id="bb085-190">Obtenir hello une adresse IP publique de votre équilibreur de charge avec [az réseau public-ip afficher](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="bb085-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="bb085-191">exemple Hello obtient adresse IP hello *myPublicIP* créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="bb085-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="bb085-192">Vous pouvez entrer ensuite des adresse IP publique de hello dans tooa navigateur.</span><span class="sxs-lookup"><span data-stu-id="bb085-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="bb085-193">N’oubliez pas, il prend quelques minutes hello hello machines virtuelles toobe prêt avant le démarrage d’équilibrage de charge hello toodistribute trafic toothem.</span><span class="sxs-lookup"><span data-stu-id="bb085-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="bb085-194">application Hello est affichée, notamment le nom d’hôte hello Hello VM cet équilibrage de charge hello distributed tooas trafic Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bb085-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Exécution de l’application Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="bb085-196">équilibrage de charge toosee hello répartir le trafic entre tous les trois machines virtuelles exécutant votre application, vous pouvez forcer l’actualisation votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="bb085-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="bb085-197">Ajouter et supprimer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bb085-197">Add and remove VMs</span></span>
<span data-ttu-id="bb085-198">Vous devrez peut-être maintenance tooperform sur hello machines virtuelles exécutant votre application, telles que l’installation des mises à jour du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bb085-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="bb085-199">toodeal avec une augmentation du trafic tooyour application, vous devrez peut-être tooadd des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bb085-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="bb085-200">Cette section vous montre comment tooremove ou ajouter une machine virtuelle à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="bb085-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="bb085-201">Supprimer une machine virtuelle à partir de l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="bb085-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="bb085-202">Vous pouvez supprimer une machine virtuelle à partir du pool d’adresses principales hello avec [az carte réseau ip-config-pool d’adresses réseau supprimer](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="bb085-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="bb085-203">Hello suivant supprime de l’exemple hello carte réseau virtuelle pour **myVM2** de *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="bb085-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="bb085-204">équilibrage de charge toosee hello répartir le trafic entre hello deux autres machines virtuelles exécutant votre application vous pouvez forcer l’actualisation votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="bb085-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="bb085-205">Vous pouvez désormais effectuer la maintenance sur hello machine virtuelle, tels que l’installation des mises à jour du système d’exploitation ou d’effectuer un redémarrage de l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="bb085-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="bb085-206">Ajouter un équilibrage de charge de toohello de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bb085-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="bb085-207">Après avoir effectué la maintenance de la machine virtuelle, ou si vous devez tooexpand capacité, vous pouvez ajouter un pool d’adresses principales toohello machine virtuelle avec [az carte réseau ip-config-pool d’adresses réseau ajouter](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="bb085-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="bb085-208">exemple Hello ajoute hello carte réseau virtuelle pour **myVM2** trop*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="bb085-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="bb085-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb085-209">Next steps</span></span>
<span data-ttu-id="bb085-210">Dans ce didacticiel, vous créé un équilibreur de charge et attaché tooit de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bb085-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="bb085-211">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bb085-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb085-212">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="bb085-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="bb085-213">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="bb085-214">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="bb085-215">Utiliser le nuage-init toocreate une application Node.js de base</span><span class="sxs-lookup"><span data-stu-id="bb085-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="bb085-216">Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa</span><span class="sxs-lookup"><span data-stu-id="bb085-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="bb085-217">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="bb085-217">View a load balancer in action</span></span>
> * <span data-ttu-id="bb085-218">Ajouter et supprimer des machines virtuelles d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="bb085-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="bb085-219">Avance toolearn de didacticiel suivant toohello plus d’informations sur les composants de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="bb085-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb085-220">Gérer les machines virtuelles et les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="bb085-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
