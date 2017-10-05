---
title: "Équilibrage de la charge des machines virtuelles Linux dans Azure | Microsoft Docs"
description: "Découvrez comment utiliser l’équilibreur de charge Azure pour créer une application hautement disponible et sécurisée entre trois machines virtuelles Linux"
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
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="3c463-103">Équilibrage de la charge des machines virtuelles Linux dans Azure pour créer une application hautement disponible</span><span class="sxs-lookup"><span data-stu-id="3c463-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="3c463-104">L’équilibrage de charge offre un niveau plus élevé de disponibilité en répartissant les demandes entrantes sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3c463-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="3c463-105">Dans ce didacticiel, vous allez découvrir les différents composants de l’équilibreur de charge Azure qui répartissent le trafic et fournissent une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="3c463-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="3c463-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3c463-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c463-107">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="3c463-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="3c463-108">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="3c463-109">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="3c463-110">Utiliser cloud-init pour créer une application Node.js de base</span><span class="sxs-lookup"><span data-stu-id="3c463-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="3c463-111">Créer des machines virtuelles et les attacher à un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="3c463-112">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="3c463-112">View a load balancer in action</span></span>
> * <span data-ttu-id="3c463-113">Ajouter et supprimer des machines virtuelles d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3c463-114">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3c463-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3c463-115">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3c463-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="3c463-116">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3c463-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="3c463-117">Vue d’ensemble de l’équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="3c463-117">Azure load balancer overview</span></span>
<span data-ttu-id="3c463-118">Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines.</span><span class="sxs-lookup"><span data-stu-id="3c463-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="3c463-119">Une sonde d’intégrité d’équilibreur de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic que vers une machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="3c463-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="3c463-120">Vous définissez une configuration IP frontale qui contient une ou plusieurs adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="3c463-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="3c463-121">Cette configuration IP frontale permet d’accéder à votre équilibreur de charge et à vos applications via Internet.</span><span class="sxs-lookup"><span data-stu-id="3c463-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="3c463-122">Les machines virtuelles se connectent à un équilibreur de charge à l’aide de leur carte d’interface réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="3c463-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="3c463-123">Pour distribuer le trafic vers les machines virtuelles, un pool d’adresses principal contient les adresses IP des cartes d’interface réseau virtuelles connectées à l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="3c463-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="3c463-124">Pour contrôler le flux de trafic, vous définissez les règles d’équilibrage de charge pour les ports et les protocoles spécifiques qui correspondent à vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3c463-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="3c463-125">Si vous avez suivi le didacticiel précédent pour [créer un groupe de machines virtuelles identiques](tutorial-create-vmss.md), un équilibreur de charge a été créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="3c463-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="3c463-126">Tous ces composants ont été configurés pour vous en relation avec le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="3c463-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="3c463-127">Créer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="3c463-127">Create Azure load balancer</span></span>
<span data-ttu-id="3c463-128">Cette section explique en détail comment vous pouvez créer et configurer chaque composant de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="3c463-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="3c463-129">Pour pouvoir créer votre équilibreur de charge, vous devez créer un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3c463-130">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupLoadBalancer* dans l’emplacement *westus*:</span><span class="sxs-lookup"><span data-stu-id="3c463-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="3c463-131">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="3c463-131">Create a public IP address</span></span>
<span data-ttu-id="3c463-132">Pour accéder à votre application sur Internet, vous avez besoin d’une adresse IP publique pour l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="3c463-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="3c463-133">Créez une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="3c463-134">L’exemple suivant crée une adresse IP publique nommée *myPublicIP* dans le groupe de ressources *myResourceGroupLoadBalancer* :</span><span class="sxs-lookup"><span data-stu-id="3c463-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="3c463-135">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-135">Create a load balancer</span></span>
<span data-ttu-id="3c463-136">Créez un équilibrage de charge avec la commande [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="3c463-137">L’exemple suivant crée un équilibreur de charge nommé *myLoadBalancer* et affecte l’adresse *myPublicIP* à la configuration IP frontale :</span><span class="sxs-lookup"><span data-stu-id="3c463-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="3c463-138">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="3c463-138">Create a health probe</span></span>
<span data-ttu-id="3c463-139">Pour permettre à l’équilibrage de charge de surveiller l’état de votre application, vous utilisez une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="3c463-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="3c463-140">La sonde d’intégrité ajoute ou supprime dynamiquement des machines virtuelles de la rotation d’équilibrage de charge en fonction de leur réponse aux vérifications d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="3c463-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="3c463-141">Par défaut, une machine virtuelle est supprimée de la distribution d’équilibrage de charge après deux échecs consécutifs à des intervalles de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="3c463-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="3c463-142">Vous créez une sonde d’intégrité selon un protocole ou une page de vérification d’intégrité spécifique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3c463-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="3c463-143">L’exemple suivant permet de créer une sonde TCP.</span><span class="sxs-lookup"><span data-stu-id="3c463-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="3c463-144">Vous pouvez également créer des sondes HTTP personnalisées pour des contrôles d’intégrité plus affinés.</span><span class="sxs-lookup"><span data-stu-id="3c463-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="3c463-145">Lorsque vous utilisez une sonde HTTP personnalisée, vous devez créer la page de contrôle d’intégrité, par exemple *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="3c463-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="3c463-146">La sonde doit retourner une réponse **HTTP 200 OK** pour l’équilibreur de charge pour assurer la rotation de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="3c463-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="3c463-147">Pour créer une sonde d’intégrité TCP, utilisez la commande [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="3c463-148">L’exemple suivant permet de créer une sonde d’intégrité nommée *myHealthProbe* :</span><span class="sxs-lookup"><span data-stu-id="3c463-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="3c463-149">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-149">Create a load balancer rule</span></span>
<span data-ttu-id="3c463-150">Une règle d’équilibrage de charge est utilisée pour définir la distribution du trafic vers les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3c463-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="3c463-151">Vous définissez la configuration IP frontale pour le trafic entrant et le pool d’adresses IP principal pour recevoir le trafic, ainsi que le port source et le port de destination requis.</span><span class="sxs-lookup"><span data-stu-id="3c463-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="3c463-152">Pour veiller à ce que seules les machines virtuelles saines reçoivent le trafic, vous devez également définir la sonde d’intégrité à utiliser.</span><span class="sxs-lookup"><span data-stu-id="3c463-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="3c463-153">Utilisez [az network lb rule create](/cli/azure/network/lb/rule#create) pour créer une règle d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="3c463-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="3c463-154">L’exemple suivant crée une règle nommée *myLoadBalancerRule*, utilise la sonde d’intégrité *myHealthProbe* et équilibre le trafic sur le port *80* :</span><span class="sxs-lookup"><span data-stu-id="3c463-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="3c463-155">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="3c463-155">Configure virtual network</span></span>
<span data-ttu-id="3c463-156">Avant de déployer des machines virtuelles et de pouvoir tester votre équilibreur, créez les ressources de réseau virtuel de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="3c463-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="3c463-157">Pour plus d’informations sur les réseaux virtuels, consultez le didacticiel [Manage Azure Virtual Networks (Gérer les réseaux virtuels Azure)](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="3c463-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="3c463-158">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="3c463-158">Create network resources</span></span>
<span data-ttu-id="3c463-159">Créez un réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="3c463-160">L’exemple suivant crée un réseau virtuel nommé *myVnet* avec un sous-réseau nommé *mySubnet* :</span><span class="sxs-lookup"><span data-stu-id="3c463-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="3c463-161">Pour ajouter un groupe de sécurité réseau, utilisez la commande [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="3c463-162">L’exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="3c463-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="3c463-163">Créez une règle de groupe de sécurité réseau avec la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="3c463-164">L’exemple suivant crée une règle de groupe de sécurité réseau nommée *myNetworkSecurityGroupRule* :</span><span class="sxs-lookup"><span data-stu-id="3c463-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="3c463-165">Les cartes d’interface réseau virtuelles sont créées avec la commande [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3c463-166">L’exemple suivant crée trois cartes réseau virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3c463-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="3c463-167">(Une carte d’interface réseau virtuelle pour chaque machine virtuelle que vous créez pour votre application dans les étapes suivantes).</span><span class="sxs-lookup"><span data-stu-id="3c463-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="3c463-168">Vous pouvez créer des machines virtuelles et des cartes d’interface réseau virtuelles supplémentaires à tout moment et les ajouter à l’équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="3c463-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="3c463-169">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3c463-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="3c463-170">Créer une configuration cloud-init</span><span class="sxs-lookup"><span data-stu-id="3c463-170">Create cloud-init config</span></span>
<span data-ttu-id="3c463-171">Dans le didacticiel précédent [How to customize a Linux virtual machine on first boot (Personnalisation d’une machine virtuelle Linux au premier démarrage)](tutorial-automate-vm-deployment.md), vous avez appris à automatiser la personnalisation des machines virtuelles avec cloud-init.</span><span class="sxs-lookup"><span data-stu-id="3c463-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="3c463-172">Vous pouvez utiliser le même fichier de configuration cloud-init pour installer NGINX et exécuter une simple application Node.js « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="3c463-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="3c463-173">Dans l’interpréteur de commandes actuel, créez un fichier nommé *cloud-init.txt* et collez la configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="3c463-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="3c463-174">Par exemple, créez le fichier dans l’interpréteur de commandes Cloud et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="3c463-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="3c463-175">Entrez `sensible-editor cloud-init.txt` pour créer le fichier et afficher la liste des éditeurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="3c463-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="3c463-176">Vérifiez que l’intégralité du fichier cloud-init est copiée, en particulier la première ligne :</span><span class="sxs-lookup"><span data-stu-id="3c463-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="3c463-177">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3c463-177">Create virtual machines</span></span>
<span data-ttu-id="3c463-178">Pour améliorer la haute disponibilité de votre application, placez vos machines virtuelles dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="3c463-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="3c463-179">Pour plus d’informations sur les groupes à haute disponibilité, consultez le didacticiel précédent [How to create highly available virtual machines (Création de machines virtuelles hautement disponibles)](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="3c463-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="3c463-180">Créez un groupe à haute disponibilité avec la commande [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="3c463-181">L’exemple suivant permet de créer un groupe à haute disponibilité nommé *myAvailabilitySet* :</span><span class="sxs-lookup"><span data-stu-id="3c463-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="3c463-182">À présent, créez les machines virtuelles avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3c463-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="3c463-183">L’exemple suivant crée trois machines virtuelles et génère des clés SSH si elles n’existent pas déjà :</span><span class="sxs-lookup"><span data-stu-id="3c463-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="3c463-184">Certaines tâches en arrière-plan continuent à s’exécuter une fois que l’interface CLI Azure vous renvoie à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="3c463-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="3c463-185">Le paramètre `--no-wait` n’attend pas que toutes les tâches se terminent.</span><span class="sxs-lookup"><span data-stu-id="3c463-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="3c463-186">Un délai de quelques minutes peut être nécessaire avant que vous puissiez accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="3c463-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="3c463-187">La sonde d’intégrité de l’équilibrage de charge détecte automatiquement lorsque l’application est en cours d’exécution sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c463-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="3c463-188">Une fois que l’application est en cours d’exécution, la règle d’équilibrage de charge commence à distribuer le trafic.</span><span class="sxs-lookup"><span data-stu-id="3c463-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="3c463-189">Tester l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-189">Test load balancer</span></span>
<span data-ttu-id="3c463-190">Obtenez l’adresse IP publique de votre équilibrage de charge avec [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="3c463-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="3c463-191">L’exemple suivant obtient l’adresse IP pour *myPublicIP* créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="3c463-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="3c463-192">Vous pouvez alors entrer l’adresse IP publique dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="3c463-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="3c463-193">N’oubliez pas - patientez quelques minutes avant que les machines virtuelles soient prêtes et que l’équilibreur de charge commence à diriger du trafic vers ces dernières.</span><span class="sxs-lookup"><span data-stu-id="3c463-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="3c463-194">L’application s’affiche, avec notamment le nom d’hôte de la machine virtuelle sur laquelle l’équilibreur de charge a distribué le trafic comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3c463-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Exécution de l’application Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="3c463-196">Pour visualiser la distribution de trafic par l’équilibreur de charge sur les trois machines virtuelles exécutant votre application, vous pouvez forcer l’actualisation de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="3c463-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="3c463-197">Ajouter et supprimer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3c463-197">Add and remove VMs</span></span>
<span data-ttu-id="3c463-198">Vous devrez peut-être effectuer la maintenance sur la machine virtuelle exécutant votre application, avec par exemple l’installation des mises à jour du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="3c463-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="3c463-199">Pour faire face à une augmentation du trafic vers votre application, vous devrez peut-être ajouter des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3c463-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="3c463-200">Cette section vous indique comment supprimer ou ajouter une machine virtuelle pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="3c463-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="3c463-201">Supprimer une machine virtuelle de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="3c463-202">Vous pouvez supprimer une machine virtuelle à partir du pool d’adresses principal avec la commande [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="3c463-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="3c463-203">L’exemple suivant supprime la carte réseau virtuelle pour **myVM2** de *myLoadBalancer* :</span><span class="sxs-lookup"><span data-stu-id="3c463-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="3c463-204">Pour visualiser la distribution de trafic par l’équilibreur de charge sur les deux machines virtuelles restantes exécutant votre application, vous pouvez forcer l’actualisation de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="3c463-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="3c463-205">Vous pouvez maintenant effectuer la maintenance sur la machine virtuelle, avec par exemple l’installation des mises à jour du système d’exploitation ou le redémarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c463-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="3c463-206">Ajouter une machine virtuelle à l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="3c463-207">Après avoir effectué les opérations de maintenance de la machine virtuelle, ou si vous devez développer la capacité, vous pouvez ajouter une machine virtuelle au pool d’adresses principal avec la commande [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="3c463-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="3c463-208">L’exemple suivant ajoute la carte réseau virtuelle pour **myVM2** à *myLoadBalancer* :</span><span class="sxs-lookup"><span data-stu-id="3c463-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="3c463-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c463-209">Next steps</span></span>
<span data-ttu-id="3c463-210">Ce didacticiel vous a montré comment créer un équilibrage de charge et y attacher des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3c463-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="3c463-211">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3c463-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c463-212">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="3c463-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="3c463-213">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="3c463-214">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="3c463-215">Utiliser cloud-init pour créer une application Node.js de base</span><span class="sxs-lookup"><span data-stu-id="3c463-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="3c463-216">Créer des machines virtuelles et les attacher à un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="3c463-217">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="3c463-217">View a load balancer in action</span></span>
> * <span data-ttu-id="3c463-218">Ajouter et supprimer des machines virtuelles d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="3c463-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="3c463-219">Passez au didacticiel suivant pour en savoir plus sur les composants de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="3c463-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c463-220">Gérer les machines virtuelles et les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="3c463-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
