---
title: "Déployer des machines virtuelles Linux dans un réseau existant avec l’interface Azure CLI 1.0 | Microsoft Docs"
description: "Procédure de déploiement d’une machine virtuelle Linux dans un réseau virtuel existant à l’aide de l’interface Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="709db-103">Procédure de déploiement d’une machine virtuelle Linux dans un réseau virtuel Azure existant à l’aide de l’interface Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="709db-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="709db-104">Cet article vous montre comment utiliser l’interface Azure CLI 1.0 pour déployer une machine virtuelle dans un réseau virtuel existant (VNet).</span><span class="sxs-lookup"><span data-stu-id="709db-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="709db-105">Les conditions requises sont :</span><span class="sxs-lookup"><span data-stu-id="709db-105">The requirements are:</span></span>

- [<span data-ttu-id="709db-106">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="709db-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="709db-107">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="709db-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="709db-108">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="709db-108">CLI versions to complete the task</span></span>
<span data-ttu-id="709db-109">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="709db-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="709db-110">[Azure CLI 1.0](#quick-commands) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="709db-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="709db-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="709db-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="709db-112">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="709db-112">Quick Commands</span></span>

<span data-ttu-id="709db-113">Si vous avez besoin d’accomplir rapidement cette tâche, la section suivante décrit les commandes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="709db-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="709db-114">Pour obtenir plus d’informations et davantage de contexte pour chaque étape, lisez la suite de ce document, [à partir de cette section](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="709db-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="709db-115">Configuration requise : groupe de ressources, réseau virtuel, groupe de sécurité réseau avec SSH entrant, sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="709db-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="709db-116">Remplacez les exemples par vos propres paramètres.</span><span class="sxs-lookup"><span data-stu-id="709db-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="709db-117">Déployer la machine virtuelle dans l’infrastructure de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="709db-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="709db-118">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="709db-118">Detailed walkthrough</span></span>

<span data-ttu-id="709db-119">Les ressources Azure telles que les réseaux virtuels et les groupes de sécurité réseau doivent être des ressources statiques et durables qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="709db-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="709db-120">Une fois un réseau virtuel déployé, il peut être réutilisé par de nouveaux redéploiements, sans impact négatif sur l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="709db-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="709db-121">Voyez les réseaux virtuels comme étant des commutateurs réseau physiques traditionnels.</span><span class="sxs-lookup"><span data-stu-id="709db-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="709db-122">Vous n’avez pas besoin de configurer un nouveau commutateur matériel avec chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="709db-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="709db-123">Avec un réseau virtuel correctement configuré, vous pouvez continuer à déployer de nouveaux serveurs dans ce réseau virtuel encore et encore avec peu de modifications requises, voire aucune, tout au long de la durée de vie du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="709db-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="709db-124">Créer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="709db-124">Create the resource group</span></span>

<span data-ttu-id="709db-125">Tout d’abord, créez un groupe de ressources pour organiser tous les éléments créés dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="709db-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="709db-126">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="709db-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="709db-127">Créez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="709db-127">Create the VNet</span></span>

<span data-ttu-id="709db-128">La première étape consiste à créer un réseau virtuel dans lequel lancer les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="709db-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="709db-129">Le réseau virtuel contient un sous-réseau pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="709db-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="709db-130">Pour plus d’informations sur les réseaux virtuels Azure, consultez la section [Créer un réseau virtuel à l’aide de l’interface de ligne de commande Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="709db-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="709db-131">Créer le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="709db-131">Create the network security group</span></span>

<span data-ttu-id="709db-132">Le sous-réseau se trouvant derrière un groupe de sécurité réseau existant, vous devez développer le groupe de sécurité en premier.</span><span class="sxs-lookup"><span data-stu-id="709db-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="709db-133">Les groupes de sécurité réseau Azure s’apparentent à un pare-feu au niveau de la couche réseau.</span><span class="sxs-lookup"><span data-stu-id="709db-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="709db-134">Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [Guide de création des groupes de sécurité réseau dans l’interface de ligne de commande Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="709db-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="709db-135">Ajouter une règle d’autorisation SSH entrante</span><span class="sxs-lookup"><span data-stu-id="709db-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="709db-136">La machine virtuelle a besoin d’un accès à partir d’Internet. Une règle autorisant le trafic entrant sur le port 22 à être acheminé à travers le réseau jusqu’au port 22 de la machine virtuelle est donc nécessaire.</span><span class="sxs-lookup"><span data-stu-id="709db-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="709db-137">Ajouter un sous-réseau au réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="709db-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="709db-138">Les machines virtuelles d’un réseau virtuel doivent se trouver dans un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="709db-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="709db-139">Chaque réseau virtuel peut présenter plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="709db-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="709db-140">Créez le sous-réseau et associez-le au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="709db-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="709db-141">Le sous-réseau est désormais ajouté au sein du réseau virtuel et associé au groupe de sécurité réseau et à la règle dédiée.</span><span class="sxs-lookup"><span data-stu-id="709db-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="709db-142">Ajouter une carte réseau virtuelle au réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="709db-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="709db-143">Les cartes réseau virtuelles (VNic) sont importantes, car vous pouvez les réutiliser en les connectant sur différentes machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="709db-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="709db-144">Cette approche conserve la carte réseau virtuelle comme une ressource statique, tandis que les machines virtuelles peuvent être temporaires.</span><span class="sxs-lookup"><span data-stu-id="709db-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="709db-145">Créez une carte réseau virtuelle et associez-la au sous-réseau créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="709db-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="709db-146">Déployer la machine virtuelle dans le réseau virtuel et le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="709db-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="709db-147">Vous disposez désormais d’un réseau virtuel et d’un sous-réseau au sein de celui-ci, ainsi que d’un groupe de sécurité réseau qui protège le sous-réseau en bloquant l’ensemble du trafic entrant, à l’exception du port 22 pour SSH.</span><span class="sxs-lookup"><span data-stu-id="709db-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="709db-148">La machine virtuelle peut désormais être déployée au sein de cette infrastructure réseau existante.</span><span class="sxs-lookup"><span data-stu-id="709db-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="709db-149">À l’aide de l’interface CLI Azure, et de la commande `azure vm create`, la machine virtuelle Linux est déployée dans le groupe de ressources Azure, le réseau virtuel, le sous-réseau et la carte réseau virtuelle Azure existants.</span><span class="sxs-lookup"><span data-stu-id="709db-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="709db-150">Pour plus d’informations sur l’utilisation de l’interface CLI pour déployer une machine virtuelle complète, consultez la section [Création d’un environnement Linux complet à l’aide de l’interface CLI Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="709db-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="709db-151">En utilisant les indicateurs CLI pour appeler les ressources existantes, vous indiquez à Azure de déployer la machine virtuelle au sein du réseau existant.</span><span class="sxs-lookup"><span data-stu-id="709db-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="709db-152">Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="709db-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="709db-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="709db-153">Next steps</span></span>

* [<span data-ttu-id="709db-154">Déploiement et gestion de machines virtuelles à l’aide des modèles Azure Resource Manager et de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="709db-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="709db-155">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="709db-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="709db-156">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="709db-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
