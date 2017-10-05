---
title: "Réseaux virtuels Azure et machines virtuelles Linux | Microsoft Docs"
description: "Didacticiel : Gérer des réseaux virtuels Azure et des machines virtuelles Linux avec Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2366905b8160675f77cbc41ba97540af70be8c01
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="72328-103">Gérer des réseaux virtuels Azure et des machines virtuelles Linux avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="72328-103">Manage Azure Virtual Networks and Linux Virtual Machines with the Azure CLI</span></span>

<span data-ttu-id="72328-104">Les machines virtuelles Azure utilisent la gestion réseau Azure pour la communication réseau interne et externe.</span><span class="sxs-lookup"><span data-stu-id="72328-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="72328-105">Ce didacticiel vous guide dans le déploiement de deux machines virtuelles et la configuration de la gestion réseau Azure pour celles-ci.</span><span class="sxs-lookup"><span data-stu-id="72328-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="72328-106">Les exemples de ce didacticiel supposent que les machines virtuelles hébergent une application web avec un back-end de base de données. Le didacticiel ne comprend cependant pas le déploiement d’une application.</span><span class="sxs-lookup"><span data-stu-id="72328-106">The examples in this tutorial assume that the VMs are hosting a web application with a database back-end, however an application is not deployed in the tutorial.</span></span> <span data-ttu-id="72328-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="72328-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72328-108">Déployer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="72328-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="72328-109">Créer un sous-réseau dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="72328-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="72328-110">Attacher des machines virtuelles à un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="72328-110">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="72328-111">Gérer les adresses IP publiques des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="72328-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="72328-112">Sécuriser le trafic internet entrant</span><span class="sxs-lookup"><span data-stu-id="72328-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="72328-113">Sécuriser le trafic entre machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="72328-113">Secure VM to VM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="72328-114">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter l’interface de ligne de commande Azure version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="72328-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="72328-115">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="72328-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="72328-116">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72328-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="72328-117">Vue d’ensemble de la mise en réseau de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="72328-117">VM networking overview</span></span>

<span data-ttu-id="72328-118">Les réseaux virtuels Azure permettent des connexions réseau sécurisées entre des machines virtuelles, Internet et d’autres services Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="72328-118">Azure virtual networks enable secure network connections between virtual machines, the internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="72328-119">Les réseaux virtuels sont divisés en segments logiques, appelés sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="72328-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="72328-120">Les sous-réseaux sont utilisés pour contrôler le flux du réseau et comme une limite de sécurité.</span><span class="sxs-lookup"><span data-stu-id="72328-120">Subnets are used to control network flow, and as a security boundary.</span></span> <span data-ttu-id="72328-121">Quand vous déployez une machine virtuelle, elle inclut généralement une interface de réseau virtuel, qui est attachée à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-121">When deploying a VM, it generally includes a virtual network interface, which is attached to a subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="72328-122">Déployer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="72328-122">Deploy virtual network</span></span>

<span data-ttu-id="72328-123">Pour ce didacticiel, un seul réseau virtuel est créé avec deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="72328-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="72328-124">Un sous-réseau frontal pour l’hébergement d’une application web et un sous-réseau principal pour l’hébergement d’un serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="72328-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="72328-125">Avant de pouvoir créer un réseau virtuel, créez un groupe de ressources avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="72328-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="72328-126">L’exemple suivant crée un groupe de ressources nommé *myRGNetwork* à l’emplacement eastus.</span><span class="sxs-lookup"><span data-stu-id="72328-126">The following example creates a resource group named *myRGNetwork* in the eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="72328-127">Création d’un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="72328-127">Create virtual network</span></span>

<span data-ttu-id="72328-128">Utilisez la commande [az network vnet create](/cli/azure/network/vnet#create) pour créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="72328-128">Us the [az network vnet create](/cli/azure/network/vnet#create) command to create a virtual network.</span></span> <span data-ttu-id="72328-129">Dans cet exemple, le réseau est nommé *mvVnet* et le préfixe d’adresse *10.0.0.0/16* lui est affecté.</span><span class="sxs-lookup"><span data-stu-id="72328-129">In this example, the network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="72328-130">Un sous-réseau est également créé avec le nom *mySubnetFrontEnd* et le préfixe d’adresse *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="72328-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="72328-131">Plus loin dans ce didacticiel, une machine virtuelle frontale est connectée à ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-131">Later in this tutorial a front-end VM is connected to this subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="72328-132">Créer un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="72328-132">Create subnet</span></span>

<span data-ttu-id="72328-133">Un nouveau sous-réseau est ajouté au réseau virtuel à l’aide de la commande [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="72328-133">A new subnet is added to the virtual network using the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="72328-134">Dans cet exemple, le réseau est nommé *mySubnetBackEnd* et le préfixe d’adresse *10.0.2.0/24* lui est affecté.</span><span class="sxs-lookup"><span data-stu-id="72328-134">In this example, the subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="72328-135">Ce sous-réseau est utilisé avec tous les services principaux.</span><span class="sxs-lookup"><span data-stu-id="72328-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="72328-136">À ce stade, un réseau a été créé et segmenté en deux sous-réseaux, un pour les services frontaux et un autre pour les services principaux.</span><span class="sxs-lookup"><span data-stu-id="72328-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="72328-137">Dans la section suivante, des machines virtuelles sont créées et connectées à ces sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="72328-137">In the next section, virtual machines are created and connected to these subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="72328-138">Présentation des adresses IP publiques</span><span class="sxs-lookup"><span data-stu-id="72328-138">Understand public IP address</span></span>

<span data-ttu-id="72328-139">Une adresse IP publique permet aux ressources Azure d’être accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="72328-139">A public IP address allows Azure resources to be accessible on the internet.</span></span> <span data-ttu-id="72328-140">Dans cette section du didacticiel, une machine virtuelle est créée pour montrer l’utilisation des adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="72328-140">In this section of the tutorial, a VM is created to demonstrate how to work with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="72328-141">Méthode d’allocation</span><span class="sxs-lookup"><span data-stu-id="72328-141">Allocation method</span></span>

<span data-ttu-id="72328-142">Une adresse IP publique peut être allouée comme adresse dynamique ou statique.</span><span class="sxs-lookup"><span data-stu-id="72328-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="72328-143">Par défaut, une adresse IP publique est allouée dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="72328-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="72328-144">Les adresses IP dynamiques sont libérées quand une machine virtuelle est désallouée.</span><span class="sxs-lookup"><span data-stu-id="72328-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="72328-145">Ce comportement fait que l’adresse IP change lors de toute opération qui inclut une désallocation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-145">This behavior causes the IP address to change during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="72328-146">La méthode d’allocation peut être définie comme étant statique, ce qui garantit que l’adresse IP reste affectée à une machine virtuelle, même pendant qu’elle est désallouée.</span><span class="sxs-lookup"><span data-stu-id="72328-146">The allocation method can be set to static, which ensures that the IP address remain assigned to a VM, even during a deallocated state.</span></span> <span data-ttu-id="72328-147">Quand vous utilisez une adresse IP allouée de manière statique, vous ne pouvez pas spécifier l’adresse IP elle-même.</span><span class="sxs-lookup"><span data-stu-id="72328-147">When using a statically allocated IP address, the IP address itself cannot be specified.</span></span> <span data-ttu-id="72328-148">Au lieu de cela, elle est allouée à partir d’un pool d’adresses disponibles.</span><span class="sxs-lookup"><span data-stu-id="72328-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="72328-149">Allocation dynamique</span><span class="sxs-lookup"><span data-stu-id="72328-149">Dynamic allocation</span></span>

<span data-ttu-id="72328-150">Quand vous créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create), la méthode d’allocation des adresse IP publiques par défaut est dynamique.</span><span class="sxs-lookup"><span data-stu-id="72328-150">When creating a VM with the [az vm create](/cli/azure/vm#create) command, the default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="72328-151">Dans l’exemple suivant, une machine virtuelle est créée avec une adresse IP dynamique.</span><span class="sxs-lookup"><span data-stu-id="72328-151">In the following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="72328-152">Allocation statique</span><span class="sxs-lookup"><span data-stu-id="72328-152">Static allocation</span></span>

<span data-ttu-id="72328-153">Lors de la création d’une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create), incluez l’argument `--public-ip-address-allocation static` pour affecter une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="72328-153">When creating a virtual machine using the [az vm create](/cli/azure/vm#create) command, include the `--public-ip-address-allocation static` argument to assign a static public IP address.</span></span> <span data-ttu-id="72328-154">Cette opération n’est pas montrée dans ce didacticiel, mais dans la section suivante, une adresse IP dynamique est changée en adresse statique.</span><span class="sxs-lookup"><span data-stu-id="72328-154">This operation is not demonstrated in this tutorial, however in the next section a dynamically allocated IP address is changed to a statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="72328-155">Changer la méthode d’allocation</span><span class="sxs-lookup"><span data-stu-id="72328-155">Change allocation method</span></span>

<span data-ttu-id="72328-156">La méthode d’allocation d’adresse IP peut être changée avec la commande [az network public-ip update](/cli/azure/network/public-ip#update).</span><span class="sxs-lookup"><span data-stu-id="72328-156">The IP address allocation method can be changed using the [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="72328-157">Dans cet exemple, la méthode de l’allocation de l’adresse IP de la machine virtuelle frontale est changée en statique.</span><span class="sxs-lookup"><span data-stu-id="72328-157">In this example, the IP address allocation method of the front-end VM is changed to static.</span></span>

<span data-ttu-id="72328-158">Désallouez d’abord la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-158">First, deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="72328-159">Utilisez la commande [az network public-ip update](/cli/azure/network/public-ip#update) pour mettre à jour la méthode d’allocation.</span><span class="sxs-lookup"><span data-stu-id="72328-159">Use the [az network public-ip update](/cli/azure/network/public-ip#update) command to update the allocation method.</span></span> <span data-ttu-id="72328-160">Dans ce cas, la `--allocation-method` est définie sur *statique*.</span><span class="sxs-lookup"><span data-stu-id="72328-160">In this case, the `--allocation-method` is being set to *static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="72328-161">Démarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-161">Start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="72328-162">Pas d’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="72328-162">No public IP address</span></span>

<span data-ttu-id="72328-163">Souvent, une machine virtuelle ne doit pas être accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="72328-163">Often, a VM does not need to be accessible over the internet.</span></span> <span data-ttu-id="72328-164">Pour créer une machine virtuelle sans adresse IP publique, utilisez l’argument `--public-ip-address ""` avec une paire de guillemets doubles vide.</span><span class="sxs-lookup"><span data-stu-id="72328-164">To create a VM without a public IP address, use the `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="72328-165">Cette configuration est montrée plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="72328-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="72328-166">sécurisent le trafic réseau</span><span class="sxs-lookup"><span data-stu-id="72328-166">Secure network traffic</span></span>

<span data-ttu-id="72328-167">Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou rejettent le trafic réseau vers les ressources connectées aux réseaux virtuels Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="72328-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to Azure Virtual Networks (VNet).</span></span> <span data-ttu-id="72328-168">Les groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des interfaces réseau individuelles.</span><span class="sxs-lookup"><span data-stu-id="72328-168">NSGs can be associated to subnets or individual network interfaces.</span></span> <span data-ttu-id="72328-169">Quand un groupe de sécurité réseau est associé à une interface réseau, il s’applique seulement à la machine virtuelle associée.</span><span class="sxs-lookup"><span data-stu-id="72328-169">When an NSG is associated with a network interface, it applies only the associated VM.</span></span> <span data-ttu-id="72328-170">Lorsqu’un NSG est associé à un sous-réseau, les règles s’appliquent à toutes les ressources connectées au sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-170">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="72328-171">Règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="72328-171">Network security group rules</span></span>

<span data-ttu-id="72328-172">Les règles de groupe de sécurité réseau définissent les ports réseau sur lesquels le trafic est autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="72328-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="72328-173">Les règles peuvent comprendre des plages d’adresses IP sources et de destination, de façon à ce que le trafic soit contrôlé entre des systèmes ou des sous-réseaux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="72328-173">The rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="72328-174">Les règles de groupe de sécurité réseau ont également une priorité (entre 1 et 4 096).</span><span class="sxs-lookup"><span data-stu-id="72328-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="72328-175">Les règles sont évaluées dans l’ordre des priorités.</span><span class="sxs-lookup"><span data-stu-id="72328-175">Rules are evaluated in the order of priority.</span></span> <span data-ttu-id="72328-176">Une règle avec une priorité de 100 est évaluée avant une règle avec une priorité de 200.</span><span class="sxs-lookup"><span data-stu-id="72328-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="72328-177">Tous les groupes de ressources réseau contiennent un ensemble de règles par défaut.</span><span class="sxs-lookup"><span data-stu-id="72328-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="72328-178">Les règles par défaut ne peuvent pas être supprimées, mais comme la priorité la plus basse leur est attribuée, elles peuvent être remplacées par les règles que vous créez.</span><span class="sxs-lookup"><span data-stu-id="72328-178">The default rules cannot be deleted, but because they are assigned the lowest priority, they can be overridden by the rules that you create.</span></span>

- <span data-ttu-id="72328-179">**Réseau virtuel** : le trafic en provenance et à destination d’un réseau virtuel est autorisé à la fois dans les directions entrante et sortante.</span><span class="sxs-lookup"><span data-stu-id="72328-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="72328-180">**Internet** : le trafic sortant est autorisé, mais le trafic entrant est bloqué.</span><span class="sxs-lookup"><span data-stu-id="72328-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="72328-181">**Équilibreur de charge** : autoriser l’équilibreur de charge d’Azure à tester l’intégrité de vos machines virtuelles et des instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="72328-181">**Load balancer** - Allow Azure’s load balancer to probe the health of your VMs and role instances.</span></span> <span data-ttu-id="72328-182">Si vous n’utilisez pas un groupe à charge équilibrée, vous pouvez remplacer cette règle.</span><span class="sxs-lookup"><span data-stu-id="72328-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="72328-183">Créer des groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="72328-183">Create network security groups</span></span>

<span data-ttu-id="72328-184">Un groupe de sécurité réseau peut être créé en même temps qu’une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="72328-184">A network security group can be created at the same time as a VM using the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="72328-185">Dans ce cas, le groupe de sécurité réseau est associé à l’interface réseau des machines virtuelles et une règle de groupe de sécurité réseau est créée automatiquement pour autoriser le trafic sur le port *22* depuis n’importe quelle source.</span><span class="sxs-lookup"><span data-stu-id="72328-185">When doing so, the NSG is associated with the VMs network interface and an NSG rule is auto created to allow traffic on port *22* from any source.</span></span> <span data-ttu-id="72328-186">Plus tôt dans ce didacticiel, le groupe de sécurité réseau frontal a été créé automatiquement avec la machine virtuelle frontale.</span><span class="sxs-lookup"><span data-stu-id="72328-186">Earlier in this tutorial, the front-end NSG was auto-created with the front-end VM.</span></span> <span data-ttu-id="72328-187">Une règle de groupe de sécurité réseau a également été créée automatiquement pour le port 22.</span><span class="sxs-lookup"><span data-stu-id="72328-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="72328-188">Dans certains cas, il peut être utile de créer au préalable un groupe de sécurité réseau, par exemple quand des règles SSH par défaut ne doivent pas être créées ou quand le groupe de sécurité réseau doit être attaché à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-188">In some cases, it may be helpful to pre-create an NSG, such as when default SSH rules should not be created, or when the NSG should be attached to a subnet.</span></span> 

<span data-ttu-id="72328-189">Utilisez la commande [az network nsg create](/cli/azure/network/nsg#create) pour créer un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-189">Use the [az network nsg create](/cli/azure/network/nsg#create) command to create a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="72328-190">Au lieu que le groupe de sécurité réseau soit associé à une interface réseau, il est associé à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-190">Instead of associating the NSG to a network interface, it is associated with a subnet.</span></span> <span data-ttu-id="72328-191">Dans cette configuration, toute machine virtuelle qui est attachée au sous-réseau hérite des règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-191">In this configuration, any VM that is attached to the subnet inherits the NSG rules.</span></span>

<span data-ttu-id="72328-192">Mettez à jour le sous-réseau existant nommé *mySubnetBackEnd* avec le nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-192">Update the existing subnet named *mySubnetBackEnd* with the new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="72328-193">Créez maintenant une machine virtuelle attachée à *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="72328-193">Now create a virtual machine, which is attached to the *mySubnetBackEnd*.</span></span> <span data-ttu-id="72328-194">Notez que l’argument `--nsg` a comme valeur une paire de guillemets doubles vide.</span><span class="sxs-lookup"><span data-stu-id="72328-194">Notice that the `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="72328-195">Vous n’avez pas besoin de créer un groupe de sécurité réseau avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-195">An NSG does not need to be created with the VM.</span></span> <span data-ttu-id="72328-196">La machine virtuelle est attachée au sous-réseau principal, qui est protégé par le groupe de sécurité réseau principal créé au préalable.</span><span class="sxs-lookup"><span data-stu-id="72328-196">The VM is attached to the back-end subnet, which is protected with the pre-created back-end NSG.</span></span> <span data-ttu-id="72328-197">Ce groupe de sécurité réseau s’applique à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-197">This NSG applies to the VM.</span></span> <span data-ttu-id="72328-198">Notez aussi que l’argument `--public-ip-address` a comme valeur une paire de guillemets doubles vide.</span><span class="sxs-lookup"><span data-stu-id="72328-198">Also, notice here that the `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="72328-199">Cette configuration crée une machine virtuelle sans adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="72328-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="72328-200">Sécuriser le trafic entrant</span><span class="sxs-lookup"><span data-stu-id="72328-200">Secure incoming traffic</span></span>

<span data-ttu-id="72328-201">Quand la machine virtuelle frontale a été créée, une règle de groupe de sécurité réseau a été créée pour autoriser le trafic entrant sur le port 22.</span><span class="sxs-lookup"><span data-stu-id="72328-201">When the front-end VM was created, an NSG rule was created to allow incoming traffic on port 22.</span></span> <span data-ttu-id="72328-202">Cette règle autorise les connexions SSH à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-202">This rule allows SSH connections to the VM.</span></span> <span data-ttu-id="72328-203">Pour cet exemple, le trafic doit également être autorisé sur le port *80*.</span><span class="sxs-lookup"><span data-stu-id="72328-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="72328-204">Cette configuration rend accessible une application web sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72328-204">This configuration allows a web application to be accessed on the VM.</span></span>

<span data-ttu-id="72328-205">Utilisez la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create) pour créer une règle pour le port *80*.</span><span class="sxs-lookup"><span data-stu-id="72328-205">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="72328-206">La machine virtuelle frontale est maintenant accessible seulement sur le port *22* et sur le port *80*.</span><span class="sxs-lookup"><span data-stu-id="72328-206">The front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="72328-207">Tout le trafic entrant est bloqué au niveau du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-207">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="72328-208">Il peut être utile de visualiser les configurations des règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-208">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="72328-209">Vous pouvez obtenir la configuration des règles de groupe de sécurité réseau avec la commande [az network rule list](/cli/azure/network/nsg/rule#list).</span><span class="sxs-lookup"><span data-stu-id="72328-209">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="72328-210">Output:</span><span class="sxs-lookup"><span data-stu-id="72328-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-to-vm-traffic"></a><span data-ttu-id="72328-211">Sécuriser le trafic entre machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="72328-211">Secure VM to VM traffic</span></span>

<span data-ttu-id="72328-212">Les règles de groupe de sécurité réseau peuvent également s’appliquer entre les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="72328-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="72328-213">Pour cet exemple, la machine virtuelle frontale doit communiquer avec la machine virtuelle principale sur les ports *22* et *3306*.</span><span class="sxs-lookup"><span data-stu-id="72328-213">For this example, the front-end VM needs to communicate with the back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="72328-214">Cette configuration autorise les connexions SSH à partir de la machine virtuelle frontale et permet aussi à une application sur la machine virtuelle frontale de communiquer avec une base de données MySQL principale.</span><span class="sxs-lookup"><span data-stu-id="72328-214">This configuration allows SSH connections from the front-end VM, and also allow an application on the front-end VM to communicate with a back-end MySQL database.</span></span> <span data-ttu-id="72328-215">Tout autre trafic doit être bloqué entre la machine virtuelle frontale et la machine virtuelle principale.</span><span class="sxs-lookup"><span data-stu-id="72328-215">All other traffic should be blocked between the front-end and back-end virtual machines.</span></span>

<span data-ttu-id="72328-216">Utilisez la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create) pour créer une règle pour le port 22.</span><span class="sxs-lookup"><span data-stu-id="72328-216">Use the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command to create a rule for port 22.</span></span> <span data-ttu-id="72328-217">Notez que l’argument `--source-address-prefix` spécifie la valeur *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="72328-217">Notice that the `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="72328-218">Cette configuration garantit que seul le trafic provenant du sous-réseau frontal est autorisé à travers le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-218">This configuration ensures that only traffic from the front-end subnet is allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="72328-219">Ajoutez maintenant une règle pour le trafic MySQL sur le port 3306.</span><span class="sxs-lookup"><span data-stu-id="72328-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="72328-220">Enfin, comme les groupes de sécurité réseau ont une règle par défaut qui autorise tout le trafic entre les machines virtuelles d’un même réseau virtuel, vous pouvez créer une règle pour que les groupes de sécurité réseau principaux bloquent tout le trafic.</span><span class="sxs-lookup"><span data-stu-id="72328-220">Finally, because NSGs have a default rule allowing all traffic between VMs in the same VNet, a rule can be created for the back-end NSGs to block all traffic.</span></span> <span data-ttu-id="72328-221">Notez ici que `--priority` a la valeur *300*, qui est inférieure à la règle du groupe de sécurité réseau et à la règle MySQL.</span><span class="sxs-lookup"><span data-stu-id="72328-221">Notice here that the `--priority` is given a value of *300*, which is lower that both the NSG and MySQL rules.</span></span> <span data-ttu-id="72328-222">Cette configuration garantit que le trafic SSH et MySQL est toujours autorisé à travers le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-222">This configuration ensures that SSH and MySQL traffic is still allowed through the NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="72328-223">La machine virtuelle principale est maintenant accessible seulement sur le port *22* et sur le port *3306* à partir du sous réseau frontal.</span><span class="sxs-lookup"><span data-stu-id="72328-223">The back-end VM is now only accessible on port *22* and port *3306* from the front-end subnet.</span></span> <span data-ttu-id="72328-224">Tout le trafic entrant est bloqué au niveau du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-224">All other incoming traffic is blocked at the network security group.</span></span> <span data-ttu-id="72328-225">Il peut être utile de visualiser les configurations des règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="72328-225">It may be helpful to visualize the NSG rule configurations.</span></span> <span data-ttu-id="72328-226">Vous pouvez obtenir la configuration des règles de groupe de sécurité réseau avec la commande [az network rule list](/cli/azure/network/nsg/rule#list).</span><span class="sxs-lookup"><span data-stu-id="72328-226">Return the NSG rule configuration with the [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="72328-227">Output:</span><span class="sxs-lookup"><span data-stu-id="72328-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="72328-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72328-228">Next steps</span></span>

<span data-ttu-id="72328-229">Dans ce tutoriel, vous avez créé et sécurisé des réseaux Azure concernant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="72328-229">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> <span data-ttu-id="72328-230">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="72328-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72328-231">Déployer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="72328-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="72328-232">Créer un sous-réseau dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="72328-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="72328-233">Attacher des machines virtuelles à un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="72328-233">Attach virtual machines to a subnet</span></span>
> * <span data-ttu-id="72328-234">Gérer les adresses IP publiques des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="72328-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="72328-235">Sécuriser le trafic internet entrant</span><span class="sxs-lookup"><span data-stu-id="72328-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="72328-236">Sécuriser le trafic entre machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="72328-236">Secure VM to VM traffic</span></span>

<span data-ttu-id="72328-237">Passez au didacticiel suivant pour découvrir comment sécuriser les données sur des machines virtuelles avec Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="72328-237">Advance to the next tutorial to learn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="72328-238">Sauvegarder des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="72328-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
