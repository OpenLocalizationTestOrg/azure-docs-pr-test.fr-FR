---
title: "mappage d’aaaNetwork entre deux régions Azure dans Azure Site Recovery | Documents Microsoft"
description: "Azure Site Recovery coordonne la réplication hello, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. En savoir plus sur tooAzure de basculement ou un centre de données secondaire."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="4b55c-104">Mappage réseau entre deux régions Azure</span><span class="sxs-lookup"><span data-stu-id="4b55c-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="4b55c-105">Cet article décrit comment toomap Azure des réseaux virtuels de deux régions Azure entre eux.</span><span class="sxs-lookup"><span data-stu-id="4b55c-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="4b55c-106">Le mappage réseau garantit que lorsque l’ordinateur virtuel répliqué est créé dans la cible de hello région Azure, il est créé sur hello réseau virtuel réseau mappé toovirtual de machine virtuelle de hello source.</span><span class="sxs-lookup"><span data-stu-id="4b55c-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4b55c-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4b55c-107">Prerequisites</span></span>
<span data-ttu-id="4b55c-108">Avant de mapper des réseaux, vérifiez que vous avez créé des [réseaux virtuels Azure](../virtual-network/virtual-networks-overview.md) dans les régions Azure source et cible.</span><span class="sxs-lookup"><span data-stu-id="4b55c-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="4b55c-109">Mapper des réseaux</span><span class="sxs-lookup"><span data-stu-id="4b55c-109">Map networks</span></span>

<span data-ttu-id="4b55c-110">toomap un réseau virtuel Azure dans une région Azure tooanother réseau virtuel une autre région, accédez tooSite Infrastructure de récupération -> mappage de réseau (pour les Machines virtuelles Azure) et créer un mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="4b55c-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="4b55c-112">Exemple ci-dessous ma machine virtuelle est en cours d’exécution dans la région Asie et est en cours hello répliquée tooSoutheast Asie.</span><span class="sxs-lookup"><span data-stu-id="4b55c-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="4b55c-113">Sélectionnez le réseau source et cible de hello et puis cliquez sur OK toocreate un mappage réseau à partir de l’Asie orientale tooSoutheast en Asie.</span><span class="sxs-lookup"><span data-stu-id="4b55c-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="4b55c-115">Hello même chose toocreate un mappage réseau à partir de l’Asie du Sud-est tooEast en Asie.</span><span class="sxs-lookup"><span data-stu-id="4b55c-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="4b55c-117">Mappage réseau lors de l’activation de la réplication</span><span class="sxs-lookup"><span data-stu-id="4b55c-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="4b55c-118">Si le mappage réseau n’est pas effectué lorsque vous répliquez une machine virtuelle pour hello première heure formulaire une région Azure tooanother, vous pouvez choisir réseau cible dans le cadre de hello même processus.</span><span class="sxs-lookup"><span data-stu-id="4b55c-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="4b55c-119">Récupération de site crée des mappages de réseau à partir de la région de tootarget la région source et de région de toosource région cible en fonction de cette sélection.</span><span class="sxs-lookup"><span data-stu-id="4b55c-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="4b55c-121">Par défaut, Site Recovery crée un réseau dans la région cible hello qui est identique toohello source réseau et en ajoutant «-asr » en tant que suffixe toohello nom de réseau de source de hello.</span><span class="sxs-lookup"><span data-stu-id="4b55c-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="4b55c-122">Vous pouvez choisir un réseau déjà créé en cliquant sur Personnaliser.</span><span class="sxs-lookup"><span data-stu-id="4b55c-122">You can choose an already created network by clicking Customize.</span></span>

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="4b55c-124">Si le mappage réseau hello est déjà fait, vous ne pouvez pas modifier le réseau virtuel de hello cible lors de l’activation de la réplication.</span><span class="sxs-lookup"><span data-stu-id="4b55c-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="4b55c-125">toochange, modifiez le mappage réseau existant.</span><span class="sxs-lookup"><span data-stu-id="4b55c-125">toochange it, modify existing network mapping.</span></span>  

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="4b55c-128">Si vous modifiez un mappage de réseau à partir de la région-1 tooregion-2, assurez-vous que vous modifiez le mappage réseau hello de région-2 tooregion-1 ainsi.</span><span class="sxs-lookup"><span data-stu-id="4b55c-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="4b55c-129">Sélection de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="4b55c-129">Subnet selection</span></span>
<span data-ttu-id="4b55c-130">Sous-réseau de la machine virtuelle cible hello est sélectionné en fonction de nom hello du sous-réseau de hello d’ordinateur virtuel de hello source.</span><span class="sxs-lookup"><span data-stu-id="4b55c-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="4b55c-131">S’il existe un sous-réseau de hello même nom que celui de l’ordinateur virtuel à source de hello disponible dans le réseau cible de hello, qui est choisi pour la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="4b55c-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="4b55c-132">S’il n’existe aucun sous-réseau ne porte hello même nom dans le réseau cible de hello, puis par ordre alphabétique premier sous-réseau est choisi comme hello sous-réseau cible.</span><span class="sxs-lookup"><span data-stu-id="4b55c-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="4b55c-133">Vous pouvez modifier ce sous-réseau en accédant tooCompute et les paramètres réseau de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="4b55c-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Modifier le sous-réseau](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="4b55c-135">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="4b55c-135">IP address</span></span>

<span data-ttu-id="4b55c-136">Adresse IP pour chaque interface de réseau hello de la machine virtuelle cible hello est choisi comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b55c-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="4b55c-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="4b55c-137">DHCP</span></span>
<span data-ttu-id="4b55c-138">Si l’interface de réseau hello de machine virtuelle de hello source utilise le protocole DHCP, interface de réseau de la machine virtuelle cible hello est également définie en tant que DHCP.</span><span class="sxs-lookup"><span data-stu-id="4b55c-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="4b55c-139">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="4b55c-139">Static IP</span></span>
<span data-ttu-id="4b55c-140">Si l’interface de réseau hello de machine virtuelle de hello source utilise des adresses IP statiques, interface de réseau de la machine virtuelle cible hello est également défini toouse adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="4b55c-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="4b55c-141">L’adresse IP statique est choisie comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b55c-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="4b55c-142">Même espace d’adressage</span><span class="sxs-lookup"><span data-stu-id="4b55c-142">Same address space</span></span>

<span data-ttu-id="4b55c-143">Si sous-réseau de hello source et de sous-réseau cible de hello ont hello même espace d’adressage, puis IP cible est identique à l’IP hello d’interface de réseau hello de machine virtuelle de hello source.</span><span class="sxs-lookup"><span data-stu-id="4b55c-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="4b55c-144">Si la même adresse IP n’est pas disponible, une adresse IP disponible est définie en tant qu’adresse IP cible de hello.</span><span class="sxs-lookup"><span data-stu-id="4b55c-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="4b55c-145">Espace d’adressage différent</span><span class="sxs-lookup"><span data-stu-id="4b55c-145">Different address space</span></span>

<span data-ttu-id="4b55c-146">Si le sous-réseau de source de hello et sous-réseau cible de hello ont l’espace d’adressage différent, adresse IP cible est définie comme une adresse IP disponible dans le sous-réseau de cible hello.</span><span class="sxs-lookup"><span data-stu-id="4b55c-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="4b55c-147">Vous pouvez modifier l’adresse IP cible de hello sur chaque interface réseau en accédant tooCompute et les paramètres réseau de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="4b55c-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b55c-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b55c-148">Next steps</span></span>

- <span data-ttu-id="4b55c-149">En savoir plus sur la [mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="4b55c-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
