---
title: "aaaDeploy les machines virtuelles Linux sur un réseau existant avec Azure CLI 1.0 | Documents Microsoft"
description: "Comment un VM Linux dans un réseau virtuel existant à l’aide de toodeploy hello Azure CLI 1.0"
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
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="e5e46-103">Comment toodeploy une machine virtuelle de Linux dans un réseau virtuel Azure existant avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e5e46-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="e5e46-104">Cet article vous montre comment toouse Azure CLI 1.0 toodeploy un ordinateur virtuel (VM) dans un réseau virtuel (VNet).</span><span class="sxs-lookup"><span data-stu-id="e5e46-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="e5e46-105">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="e5e46-105">hello requirements are:</span></span>

- [<span data-ttu-id="e5e46-106">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="e5e46-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="e5e46-107">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="e5e46-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e5e46-108">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="e5e46-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e5e46-109">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5e46-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e5e46-110">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="e5e46-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e5e46-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="e5e46-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e5e46-112">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="e5e46-112">Quick Commands</span></span>

<span data-ttu-id="e5e46-113">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires.</span><span class="sxs-lookup"><span data-stu-id="e5e46-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="e5e46-114">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e5e46-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="e5e46-115">Configuration requise : groupe de ressources, réseau virtuel, groupe de sécurité réseau avec SSH entrant, sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e5e46-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="e5e46-116">Remplacez les exemples par vos propres paramètres.</span><span class="sxs-lookup"><span data-stu-id="e5e46-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="e5e46-117">Déployer hello VM dans l’infrastructure de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="e5e46-117">Deploy hello VM into hello virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="e5e46-118">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="e5e46-118">Detailed walkthrough</span></span>

<span data-ttu-id="e5e46-119">Ressources Azure, comme hello des réseaux virtuels et des groupes de sécurité réseau doivent être statiques et de longue durée de vie ressources qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="e5e46-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="e5e46-120">Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives.</span><span class="sxs-lookup"><span data-stu-id="e5e46-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="e5e46-121">Voyez les réseaux virtuels comme étant des commutateurs réseau physiques traditionnels.</span><span class="sxs-lookup"><span data-stu-id="e5e46-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="e5e46-122">Vous ne devez pas tooconfigure basculer d’un nouveau matériel à chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="e5e46-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="e5e46-123">Avec un réseau virtuel configuré correctement, vous pouvez poursuivre toodeploy nouveaux serveurs dans ce réseau virtuel apportant peu, le cas échéant, de modifications nécessaires pendant toute la durée hello Hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e5e46-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="e5e46-124">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="e5e46-124">Create hello resource group</span></span>

<span data-ttu-id="e5e46-125">Commencez par créer un tooorganize de groupe de ressources tout ce que vous créez dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="e5e46-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="e5e46-126">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e5e46-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="e5e46-127">Créer hello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e5e46-127">Create hello VNet</span></span>

<span data-ttu-id="e5e46-128">première étape de Hello est toobuild un toolaunch de réseau virtuel hello des machines virtuelles dans.</span><span class="sxs-lookup"><span data-stu-id="e5e46-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="e5e46-129">Hello réseau virtuel contient un sous-réseau pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="e5e46-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="e5e46-130">Pour plus d’informations sur des réseaux virtuels Azure, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e5e46-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="e5e46-131">Créer un groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="e5e46-131">Create hello network security group</span></span>

<span data-ttu-id="e5e46-132">sous-réseau de Hello repose derrière un groupe de sécurité réseau existant ainsi générer le groupe de sécurité de réseau hello avant le sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="e5e46-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="e5e46-133">Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello.</span><span class="sxs-lookup"><span data-stu-id="e5e46-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="e5e46-134">Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [comment les groupes de sécurité de réseau toocreate Bonjour CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e5e46-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="e5e46-135">Ajouter une règle d’autorisation SSH entrante</span><span class="sxs-lookup"><span data-stu-id="e5e46-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="e5e46-136">Hello machine virtuelle a besoin d’accéder à partir de hello internet pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello machine virtuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e5e46-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="e5e46-137">Ajouter un sous-réseau de toohello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e5e46-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="e5e46-138">Machines virtuelles au sein de hello réseau virtuel doivent se trouver dans un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e5e46-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="e5e46-139">Chaque réseau virtuel peut présenter plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="e5e46-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="e5e46-140">Créer hello sous-réseau et l’associer à un groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="e5e46-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="e5e46-141">Hello sous-réseau est désormais ajouté à l’intérieur de hello réseau virtuel et associé à la règle et le groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="e5e46-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="e5e46-142">Ajouter un sous-réseau toohello de carte réseau virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5e46-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="e5e46-143">Les cartes réseau virtuelles (cartes réseau) sont importantes que vous puissiez les réutiliser en connectant les machines virtuelles de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="e5e46-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="e5e46-144">Cette approche conserve hello VNic comme une ressource statique hello machines virtuelles peut être temporaire.</span><span class="sxs-lookup"><span data-stu-id="e5e46-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="e5e46-145">Créer une carte réseau virtuelle et l’associer à sous-réseau hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="e5e46-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="e5e46-146">Déployer hello VM dans hello réseau virtuel et le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="e5e46-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="e5e46-147">Vous avez maintenant un réseau virtuel et un sous-réseau à l’intérieur de ce réseau virtuel et un groupe de sécurité réseau font Office de sous-réseau de hello tooprotect en bloque tout le trafic entrant, à l’exception de port 22 pour SSH.</span><span class="sxs-lookup"><span data-stu-id="e5e46-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="e5e46-148">Hello machine virtuelle peut désormais être déployé à l’intérieur de cette infrastructure réseau existante.</span><span class="sxs-lookup"><span data-stu-id="e5e46-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="e5e46-149">À l’aide de hello CLI d’Azure et hello `azure vm create` hello Linux VM est déployé toohello existante du groupe de ressources Azure, du réseau virtuel, sous-réseau et une carte réseau virtuelle de la commande.</span><span class="sxs-lookup"><span data-stu-id="e5e46-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="e5e46-150">Pour plus d’informations sur l’utilisation de hello CLI toodeploy une machine virtuelle complète, consultez [créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="e5e46-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="e5e46-151">À l’aide de hello CLI indicateurs toocall les ressources existantes, vous indiquez à Azure toodeploy hello machine virtuelle à l’intérieur du réseau existant de hello.</span><span class="sxs-lookup"><span data-stu-id="e5e46-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="e5e46-152">Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e46-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e5e46-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5e46-153">Next steps</span></span>

* [<span data-ttu-id="e5e46-154">Utilisez un toocreate de modèle Azure Resource Manager un déploiement spécifique</span><span class="sxs-lookup"><span data-stu-id="e5e46-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="e5e46-155">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="e5e46-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="e5e46-156">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="e5e46-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
