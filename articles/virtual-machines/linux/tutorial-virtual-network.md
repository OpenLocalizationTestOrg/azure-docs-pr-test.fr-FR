---
title: "aaaAzure réseaux virtuels et des ordinateurs virtuels Linux | Documents Microsoft"
description: "Didacticiel - gérer les réseaux virtuels Azure et les ordinateurs virtuels Linux par hello CLI d’Azure"
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
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="84516-103">Gérer les réseaux virtuels Azure et les ordinateurs virtuels Linux par hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="84516-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="84516-104">Les machines virtuelles Azure utilisent la gestion réseau Azure pour la communication réseau interne et externe.</span><span class="sxs-lookup"><span data-stu-id="84516-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="84516-105">Ce didacticiel vous guide dans le déploiement de deux machines virtuelles et la configuration de la gestion réseau Azure pour celles-ci.</span><span class="sxs-lookup"><span data-stu-id="84516-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="84516-106">exemples de Hello dans ce didacticiel partent du principe que les machines virtuelles de hello sont héberge une application web avec une base de données principale, toutefois, une application n’est pas déployée dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="84516-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="84516-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="84516-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84516-108">Déployer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="84516-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="84516-109">Créer un sous-réseau dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="84516-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="84516-110">Joindre des ordinateurs virtuels tooa sous-réseau</span><span class="sxs-lookup"><span data-stu-id="84516-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="84516-111">Gérer les adresses IP publiques des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="84516-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="84516-112">Sécuriser le trafic internet entrant</span><span class="sxs-lookup"><span data-stu-id="84516-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="84516-113">Sécuriser le trafic tooVM de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="84516-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="84516-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="84516-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="84516-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="84516-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="84516-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84516-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="84516-117">Vue d’ensemble de la mise en réseau de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="84516-117">VM networking overview</span></span>

<span data-ttu-id="84516-118">Réseaux virtuels Azure activer des connexions réseau sécurisées entre les machines virtuelles, hello internet et autres services Azure comme base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="84516-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="84516-119">Les réseaux virtuels sont divisés en segments logiques, appelés sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="84516-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="84516-120">Sous-réseaux sont utilisés les flux de réseau toocontrol et comme une limite de sécurité.</span><span class="sxs-lookup"><span data-stu-id="84516-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="84516-121">Lorsque vous déployez une machine virtuelle, il inclut généralement une interface de réseau virtuel, ce qui est attaché tooa sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="84516-122">Déployer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="84516-122">Deploy virtual network</span></span>

<span data-ttu-id="84516-123">Pour ce didacticiel, un seul réseau virtuel est créé avec deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="84516-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="84516-124">Un sous-réseau frontal pour l’hébergement d’une application web et un sous-réseau principal pour l’hébergement d’un serveur de base de données.</span><span class="sxs-lookup"><span data-stu-id="84516-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="84516-125">Avant de pouvoir créer un réseau virtuel, créez un groupe de ressources avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="84516-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="84516-126">Hello exemple suivant crée un groupe de ressources nommé *myRGNetwork* dans l’emplacement d’eastus hello.</span><span class="sxs-lookup"><span data-stu-id="84516-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="84516-127">Création d’un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="84516-127">Create virtual network</span></span>

<span data-ttu-id="84516-128">Nous hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create) commande toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="84516-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="84516-129">Dans cet exemple, le réseau de hello est nommé *mvVnet* et dispose d’un préfixe d’adresse *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="84516-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="84516-130">Un sous-réseau est également créé avec le nom *mySubnetFrontEnd* et le préfixe d’adresse *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="84516-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="84516-131">Plus loin dans ce didacticiel, une machine virtuelle frontale est connecté toothis sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="84516-132">Créer un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="84516-132">Create subnet</span></span>

<span data-ttu-id="84516-133">Un nouveau sous-réseau est ajouté toohello de réseau virtuel à l’aide de hello [créer de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#create) commande.</span><span class="sxs-lookup"><span data-stu-id="84516-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="84516-134">Dans cet exemple, le sous-réseau de hello est nommé *mySubnetBackEnd* et dispose d’un préfixe d’adresse *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="84516-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="84516-135">Ce sous-réseau est utilisé avec tous les services principaux.</span><span class="sxs-lookup"><span data-stu-id="84516-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="84516-136">À ce stade, un réseau a été créé et segmenté en deux sous-réseaux, un pour les services frontaux et un autre pour les services principaux.</span><span class="sxs-lookup"><span data-stu-id="84516-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="84516-137">Dans la section suivante de hello, les ordinateurs virtuels sont créés et toothese sous-réseaux connectés.</span><span class="sxs-lookup"><span data-stu-id="84516-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="84516-138">Présentation des adresses IP publiques</span><span class="sxs-lookup"><span data-stu-id="84516-138">Understand public IP address</span></span>

<span data-ttu-id="84516-139">Une adresse IP publique permet de ressources Azure toobe accessible sur internet de hello.</span><span class="sxs-lookup"><span data-stu-id="84516-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="84516-140">Dans cette section du didacticiel de hello, une machine virtuelle est créée toodemonstrate comment les adresses toowork avec l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="84516-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="84516-141">Méthode d’allocation</span><span class="sxs-lookup"><span data-stu-id="84516-141">Allocation method</span></span>

<span data-ttu-id="84516-142">Une adresse IP publique peut être allouée comme adresse dynamique ou statique.</span><span class="sxs-lookup"><span data-stu-id="84516-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="84516-143">Par défaut, une adresse IP publique est allouée dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="84516-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="84516-144">Les adresses IP dynamiques sont libérées quand une machine virtuelle est désallouée.</span><span class="sxs-lookup"><span data-stu-id="84516-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="84516-145">Ce comportement provoque hello IP adresse toochange pendant toute opération qui inclut une désallocation de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="84516-146">méthode d’allocation de Hello peut être définie toostatic, ce qui garantit que les adresses IP de hello restent affectés tooa machine virtuelle, même pendant un état libéré.</span><span class="sxs-lookup"><span data-stu-id="84516-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="84516-147">Lorsque vous utilisez une adresse IP allouée de manière statique, hello adresse IP ne peut pas être spécifié.</span><span class="sxs-lookup"><span data-stu-id="84516-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="84516-148">Au lieu de cela, elle est allouée à partir d’un pool d’adresses disponibles.</span><span class="sxs-lookup"><span data-stu-id="84516-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="84516-149">Allocation dynamique</span><span class="sxs-lookup"><span data-stu-id="84516-149">Dynamic allocation</span></span>

<span data-ttu-id="84516-150">Lors de la création d’une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) hello par défaut public d’allocation méthode d’adresse IP est dynamique de la commande.</span><span class="sxs-lookup"><span data-stu-id="84516-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="84516-151">Bonjour l’exemple suivant, un ordinateur virtuel est créé avec une adresse IP dynamique.</span><span class="sxs-lookup"><span data-stu-id="84516-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

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

### <a name="static-allocation"></a><span data-ttu-id="84516-152">Allocation statique</span><span class="sxs-lookup"><span data-stu-id="84516-152">Static allocation</span></span>

<span data-ttu-id="84516-153">Lors de la création d’un ordinateur virtuel à l’aide de hello [az vm créer](/cli/azure/vm#create) command, inclure hello `--public-ip-address-allocation static` argument tooassign une adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="84516-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="84516-154">Cette opération n’est pas illustrée dans ce didacticiel, toutefois dans la section suivante de hello une adresse IP allouée dynamiquement est modifié tooa alloué statiquement adresse.</span><span class="sxs-lookup"><span data-stu-id="84516-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="84516-155">Changer la méthode d’allocation</span><span class="sxs-lookup"><span data-stu-id="84516-155">Change allocation method</span></span>

<span data-ttu-id="84516-156">la méthode de l’allocation d’adresses IP Hello peut être modifiée à l’aide de hello [mise à jour de az réseau public-ip](/cli/azure/network/public-ip#update) commande.</span><span class="sxs-lookup"><span data-stu-id="84516-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="84516-157">Dans cet exemple, hello méthode d’allocation d’adresse IP de hello frontal machine virtuelle est déplacée toostatic.</span><span class="sxs-lookup"><span data-stu-id="84516-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="84516-158">Tout d’abord, désallouer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="84516-159">Hello d’utilisation [mise à jour de az réseau public-ip](/cli/azure/network/public-ip#update) commande tooupdate hello d’allocation (méthode).</span><span class="sxs-lookup"><span data-stu-id="84516-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="84516-160">Dans ce cas, hello `--allocation-method` est défini trop*statique*.</span><span class="sxs-lookup"><span data-stu-id="84516-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="84516-161">Démarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="84516-162">Pas d’adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="84516-162">No public IP address</span></span>

<span data-ttu-id="84516-163">Souvent, une machine virtuelle n’a pas besoin toobe accessible sur internet de hello.</span><span class="sxs-lookup"><span data-stu-id="84516-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="84516-164">toocreate une machine virtuelle sans une adresse IP publique, utilisez hello `--public-ip-address ""` argument avec un ensemble vide de guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="84516-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="84516-165">Cette configuration est montrée plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="84516-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="84516-166">sécurisent le trafic réseau</span><span class="sxs-lookup"><span data-stu-id="84516-166">Secure network traffic</span></span>

<span data-ttu-id="84516-167">Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooresources de trafic réseau connecté tooAzure de réseaux virtuels (VNet).</span><span class="sxs-lookup"><span data-stu-id="84516-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="84516-168">Groupes de sécurité réseau peuvent être toosubnets associée ou interfaces réseau individuelles.</span><span class="sxs-lookup"><span data-stu-id="84516-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="84516-169">Lorsqu’un groupe de sécurité réseau est associé à une interface réseau, il s’applique uniquement hello associé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="84516-170">Lorsqu’un groupe de sécurité réseau est associé tooa sous-réseau, les règles de hello s’appliquent tooall ressources toohello connecté sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="84516-171">Règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="84516-171">Network security group rules</span></span>

<span data-ttu-id="84516-172">Les règles de groupe de sécurité réseau définissent les ports réseau sur lesquels le trafic est autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="84516-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="84516-173">règles de Hello peuvent inclure des plages d’adresses IP source et de destination afin que le trafic est contrôlé entre systèmes spécifiques ou des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="84516-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="84516-174">Les règles de groupe de sécurité réseau ont également une priorité (entre 1 et 4 096).</span><span class="sxs-lookup"><span data-stu-id="84516-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="84516-175">Les règles sont évaluées dans l’ordre de hello de priorité.</span><span class="sxs-lookup"><span data-stu-id="84516-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="84516-176">Une règle avec une priorité de 100 est évaluée avant une règle avec une priorité de 200.</span><span class="sxs-lookup"><span data-stu-id="84516-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="84516-177">Tous les groupes de ressources réseau contiennent un ensemble de règles par défaut.</span><span class="sxs-lookup"><span data-stu-id="84516-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="84516-178">les règles par défaut Hello ne peut pas être supprimés, mais comme ils sont affectés de priorité la plus faible de hello, elles peuvent être remplacées par les règles hello que vous créez.</span><span class="sxs-lookup"><span data-stu-id="84516-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="84516-179">**Réseau virtuel** : le trafic en provenance et à destination d’un réseau virtuel est autorisé à la fois dans les directions entrante et sortante.</span><span class="sxs-lookup"><span data-stu-id="84516-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="84516-180">**Internet** : le trafic sortant est autorisé, mais le trafic entrant est bloqué.</span><span class="sxs-lookup"><span data-stu-id="84516-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="84516-181">**L’équilibrage de charge** -charge équilibrage tooprobe hello l’intégrité autoriser Azure de vos machines virtuelles et les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="84516-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="84516-182">Si vous n’utilisez pas un groupe à charge équilibrée, vous pouvez remplacer cette règle.</span><span class="sxs-lookup"><span data-stu-id="84516-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="84516-183">Créer des groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="84516-183">Create network security groups</span></span>

<span data-ttu-id="84516-184">Un groupe de sécurité réseau permettre être créé à hello même temps comme un ordinateur virtuel à l’aide de hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="84516-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="84516-185">Lorsque vous procédez ainsi, hello NSG associée à interface réseau de machines virtuelles hello et une règle de groupe de sécurité réseau est créé automatiquement le trafic de tooallow sur le port *22* à partir de n’importe quelle source.</span><span class="sxs-lookup"><span data-stu-id="84516-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="84516-186">Plus haut dans ce didacticiel, hello NSG frontal a été créée automatiquement avec hello frontal machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="84516-187">Une règle de groupe de sécurité réseau a également été créée automatiquement pour le port 22.</span><span class="sxs-lookup"><span data-stu-id="84516-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="84516-188">Dans certains cas, il peut être utile toopre-créer un groupe de sécurité réseau, tels que lorsque les règles SSH par défaut ne doivent pas être créées, ou lorsque hello NSG doit être attaché tooa sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="84516-189">Hello d’utilisation [az réseau nsg créer](/cli/azure/network/nsg#create) commande toocreate un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="84516-190">Au lieu de l’association d’interface réseau de hello NSG tooa, il est associé à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="84516-191">Dans cette configuration, toutes les machines virtuelles qui sont attaché toohello sous-réseau hérite des règles du groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="84516-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="84516-192">Mise à jour hello de sous-réseau existant nommé *mySubnetBackEnd* avec hello du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="84516-193">Maintenant créer un ordinateur virtuel, qui est attaché toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="84516-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="84516-194">Notez que hello `--nsg` argument a une valeur de guillemets doubles vides.</span><span class="sxs-lookup"><span data-stu-id="84516-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="84516-195">Un groupe de sécurité réseau n’a pas besoin toobe créé par hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="84516-196">Hello machine virtuelle est sous-réseau principal toohello attachée, ce qui est protégé par hello principal groupe de sécurité réseau créé au préalable.</span><span class="sxs-lookup"><span data-stu-id="84516-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="84516-197">Ce groupe de sécurité réseau s’applique toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="84516-198">En outre, Notez ici que hello `--public-ip-address` argument a une valeur de guillemets doubles vides.</span><span class="sxs-lookup"><span data-stu-id="84516-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="84516-199">Cette configuration crée une machine virtuelle sans adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="84516-199">This configuration creates a VM without a public IP address.</span></span> 

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

### <a name="secure-incoming-traffic"></a><span data-ttu-id="84516-200">Sécuriser le trafic entrant</span><span class="sxs-lookup"><span data-stu-id="84516-200">Secure incoming traffic</span></span>

<span data-ttu-id="84516-201">Lorsque hello frontal machine virtuelle a été créée, une règle de groupe de sécurité réseau a été créée tooallow du trafic entrant sur le port 22.</span><span class="sxs-lookup"><span data-stu-id="84516-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="84516-202">Cette règle permet de toohello des connexions SSH machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="84516-203">Pour cet exemple, le trafic doit également être autorisé sur le port *80*.</span><span class="sxs-lookup"><span data-stu-id="84516-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="84516-204">Cette configuration autorise une toobe d’application web accédé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84516-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="84516-205">Hello d’utilisation [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) commande toocreate une règle pour le port *80*.</span><span class="sxs-lookup"><span data-stu-id="84516-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

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

<span data-ttu-id="84516-206">Hello frontal machine virtuelle est désormais uniquement accessible sur le port *22* et le port *80*.</span><span class="sxs-lookup"><span data-stu-id="84516-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="84516-207">Tout le trafic entrant est bloqué au niveau de groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="84516-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="84516-208">Il peut être utile de toovisualize configurations de la règle NSG hello.</span><span class="sxs-lookup"><span data-stu-id="84516-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="84516-209">Configuration de la règle NSG hello retour avec hello [liste de règles de réseau az](/cli/azure/network/nsg/rule#list) commande.</span><span class="sxs-lookup"><span data-stu-id="84516-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="84516-210">Output:</span><span class="sxs-lookup"><span data-stu-id="84516-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="84516-211">Sécuriser le trafic tooVM de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="84516-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="84516-212">Les règles de groupe de sécurité réseau peuvent également s’appliquer entre les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="84516-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="84516-213">Pour cet exemple, hello VM frontal doit toocommunicate avec hello VM principal sur le port *22* et *3306*.</span><span class="sxs-lookup"><span data-stu-id="84516-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="84516-214">Cette configuration permet des connexions SSH hello frontal machine virtuelle et également autoriser une application sur hello frontal toocommunicate de machine virtuelle avec une base de données MySQL back-end.</span><span class="sxs-lookup"><span data-stu-id="84516-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="84516-215">Tout autre trafic doit être bloqué entre hello frontaux et principaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="84516-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="84516-216">Hello d’utilisation [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) commande toocreate une règle pour le port 22.</span><span class="sxs-lookup"><span data-stu-id="84516-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="84516-217">Notez que hello `--source-address-prefix` argument spécifie une valeur de *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="84516-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="84516-218">Cette configuration garantit que seul le trafic de sous-réseau frontal de hello est autorisé via hello NSG.</span><span class="sxs-lookup"><span data-stu-id="84516-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

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

<span data-ttu-id="84516-219">Ajoutez maintenant une règle pour le trafic MySQL sur le port 3306.</span><span class="sxs-lookup"><span data-stu-id="84516-219">Now add a rule for MySQL traffic on port 3306.</span></span>

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

<span data-ttu-id="84516-220">Enfin, étant donné que les groupes de sécurité réseau ont une règle par défaut lui accordant tout le trafic entre les ordinateurs virtuels dans hello même réseau virtuel, une règle peut être créée pour hello principaux groupes de sécurité réseau tooblock tout le trafic.</span><span class="sxs-lookup"><span data-stu-id="84516-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="84516-221">Notez ici que hello `--priority` reçoit la valeur de *300*, qui est plus faible que les deux hello des règles de groupe de sécurité réseau et de MySQL.</span><span class="sxs-lookup"><span data-stu-id="84516-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="84516-222">Cette configuration garantit que le trafic SSH et MySQL est toujours autorisé via hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="84516-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

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

<span data-ttu-id="84516-223">Hello principal machine virtuelle est désormais uniquement accessible sur le port *22* et le port *3306* à partir du sous-réseau frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="84516-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="84516-224">Tout le trafic entrant est bloqué au niveau de groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="84516-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="84516-225">Il peut être utile de toovisualize configurations de la règle NSG hello.</span><span class="sxs-lookup"><span data-stu-id="84516-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="84516-226">Configuration de la règle NSG hello retour avec hello [liste de règles de réseau az](/cli/azure/network/nsg/rule#list) commande.</span><span class="sxs-lookup"><span data-stu-id="84516-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="84516-227">Output:</span><span class="sxs-lookup"><span data-stu-id="84516-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="84516-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84516-228">Next steps</span></span>

<span data-ttu-id="84516-229">Dans ce didacticiel, vous créé et sécurisé de réseaux Azure en tant que machines de toovirtual connexes.</span><span class="sxs-lookup"><span data-stu-id="84516-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="84516-230">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="84516-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84516-231">Déployer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="84516-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="84516-232">Créer un sous-réseau dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="84516-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="84516-233">Joindre des ordinateurs virtuels tooa sous-réseau</span><span class="sxs-lookup"><span data-stu-id="84516-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="84516-234">Gérer les adresses IP publiques des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="84516-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="84516-235">Sécuriser le trafic internet entrant</span><span class="sxs-lookup"><span data-stu-id="84516-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="84516-236">Sécuriser le trafic tooVM de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="84516-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="84516-237">Avance toohello toolearn de didacticiel suivant sur la sécurisation des données sur des machines virtuelles à l’aide de la sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="84516-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="84516-238">Sauvegarder des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="84516-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
