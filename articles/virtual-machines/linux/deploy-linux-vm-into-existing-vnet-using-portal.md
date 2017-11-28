---
title: "aaaDeploy les machines virtuelles Linux sur un réseau existant avec le portail Azure | Documents Microsoft"
description: "Déployer un VM Linux dans un réseau virtuel Azure existant à l’aide du portail de hello."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="47e37-103">Comment toodeploy une machine virtuelle de Linux dans un réseau virtuel Azure existant avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="47e37-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="47e37-104">Cet article vous explique comment toodeploy un ordinateur virtuel (VM) dans un réseau virtuel (VNet).</span><span class="sxs-lookup"><span data-stu-id="47e37-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="47e37-105">Les ressources Azure telles que les réseaux virtuels et les groupes de sécurité réseau doivent être des ressources statiques et durables qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="47e37-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="47e37-106">Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par redéploiements constantes sans n’importe quelle infrastructure de toohello répercussions négatives.</span><span class="sxs-lookup"><span data-stu-id="47e37-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="47e37-107">Vous réfléchissez à un réseau virtuel comme étant une traditionnelle commutateur de réseau de matériel – vous n’avez pas tooconfigure basculer d’un nouveau matériel à chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="47e37-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="47e37-108">Avec un réseau virtuel configuré correctement, vous pouvez poursuivre toodeploy nouveaux serveurs dans ce réseau virtuel apportant peu, le cas échéant, de modifications nécessaires pendant toute la durée hello Hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="47e37-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="47e37-109">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="47e37-109">Create hello resource group</span></span>

<span data-ttu-id="47e37-110">Commencez par créer un tooorganize de groupe de ressources tout ce que vous créez dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="47e37-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="47e37-111">Pour plus d’informations sur les groupes de ressources Azure, consultez la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="47e37-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="47e37-113">Créer hello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="47e37-113">Create hello VNet</span></span>

<span data-ttu-id="47e37-114">Ensuite, générez un Bonjour toolaunch de réseau virtuel pour les machines virtuelles dans.</span><span class="sxs-lookup"><span data-stu-id="47e37-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="47e37-115">Hello réseau virtuel contient un sous-réseau et est associé au groupe de sécurité réseau hello à ce sous-réseau dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="47e37-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="47e37-117">Ajouter un sous-réseau toohello de carte réseau virtuelle</span><span class="sxs-lookup"><span data-stu-id="47e37-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="47e37-118">Les cartes réseau virtuelles (cartes réseau) sont importantes que vous pouvez vous connecter les machines virtuelles de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="47e37-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="47e37-119">Cette approche conserve hello VNic comme une ressource statique hello machines virtuelles peut être temporaire.</span><span class="sxs-lookup"><span data-stu-id="47e37-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="47e37-120">Créer une carte réseau virtuelle et l’associer à sous-réseau hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="47e37-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="47e37-122">Créer un groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="47e37-122">Create hello network security group</span></span>

<span data-ttu-id="47e37-123">Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello.</span><span class="sxs-lookup"><span data-stu-id="47e37-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="47e37-124">Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="47e37-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="47e37-126">Ajouter une règle d’autorisation SSH entrante</span><span class="sxs-lookup"><span data-stu-id="47e37-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="47e37-127">Hello machine virtuelle a besoin d’accéder à partir de hello internet, pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="47e37-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="47e37-129">Associer hello NSG sous-réseau de hello</span><span class="sxs-lookup"><span data-stu-id="47e37-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="47e37-130">Avec hello réseau virtuel et un sous-réseau hello créé, associez un groupe de sécurité réseau hello sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="47e37-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="47e37-131">Les groupes de sécurité réseau peuvent être associés à un sous-réseau entier ou à une carte réseau virtuelle individuelle.</span><span class="sxs-lookup"><span data-stu-id="47e37-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="47e37-132">Avec le pare-feu hello filtrage du trafic au niveau du sous-réseau hello, toutes les cartes réseau et hello machines virtuelles au sein du sous-réseau de hello sont protégés par le groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="47e37-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="47e37-133">Hello autre approche est hello groupe de sécurité réseau sont associées à une seule carte réseau virtuelle et la protection qu’une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="47e37-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="47e37-135">Déployer hello VM dans hello réseau virtuel et le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="47e37-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="47e37-136">À l’aide de hello portail Azure, hello Linux VM est déployé toohello existante du groupe de ressources Azure, du réseau virtuel, sous-réseau et une carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="47e37-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="47e37-138">À l’aide des ressources existantes hello toochoose portail, vous indiquez à toodeploy Azure hello machine virtuelle à l’intérieur du réseau existant de hello.</span><span class="sxs-lookup"><span data-stu-id="47e37-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="47e37-139">Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="47e37-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="47e37-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47e37-140">Next steps</span></span>

* [<span data-ttu-id="47e37-141">Utilisez un toocreate de modèle Azure Resource Manager un déploiement spécifique</span><span class="sxs-lookup"><span data-stu-id="47e37-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="47e37-142">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="47e37-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="47e37-143">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="47e37-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
