---
title: "Mappage réseau entre deux régions Azure dans Azure Site Recovery | Microsoft Docs"
description: "Azure Site Recovery coordonne la réplication, le basculement et la récupération des machines virtuelles et des serveurs physiques. Informez-vous sur le basculement dans Microsoft Azure ou un centre de données secondaire."
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
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="66753-104">Mappage réseau entre deux régions Azure</span><span class="sxs-lookup"><span data-stu-id="66753-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="66753-105">Cet article explique comment mapper des réseaux virtuels Azure de deux régions Azure.</span><span class="sxs-lookup"><span data-stu-id="66753-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="66753-106">Le mappage réseau garantit que quand une machine virtuelle répliquée est créée dans la région Azure cible, elle est créée sur le réseau virtuel qui est mappé au réseau virtuel de la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="66753-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="66753-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="66753-107">Prerequisites</span></span>
<span data-ttu-id="66753-108">Avant de mapper des réseaux, vérifiez que vous avez créé des [réseaux virtuels Azure](../virtual-network/virtual-networks-overview.md) dans les régions Azure source et cible.</span><span class="sxs-lookup"><span data-stu-id="66753-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="66753-109">Mapper des réseaux</span><span class="sxs-lookup"><span data-stu-id="66753-109">Map networks</span></span>

<span data-ttu-id="66753-110">Pour mapper un réseau virtuel Azure dans une région Azure à un autre réseau virtuel dans une autre région, accédez à Infrastructure Site Recovery -> Mappage réseau (pour les machines virtuelles Azure) et créez un mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="66753-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="66753-112">Dans l’exemple ci-dessous, ma machine virtuelle s’exécute dans la région Asie de l’Est et est répliquée vers Asie du Sud-Est.</span><span class="sxs-lookup"><span data-stu-id="66753-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="66753-113">Sélectionnez les réseaux source et cible, puis cliquez sur OK pour créer un mappage réseau Asie de l’Est à Asie du Sud-Est.</span><span class="sxs-lookup"><span data-stu-id="66753-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="66753-115">Faites la même chose pour créer un mappage réseau Asie du Sud-Est à Asie de l’Est.</span><span class="sxs-lookup"><span data-stu-id="66753-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="66753-117">Mappage réseau lors de l’activation de la réplication</span><span class="sxs-lookup"><span data-stu-id="66753-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="66753-118">Si le mappage réseau n’est pas effectué quand vous répliquez une machine virtuelle pour la première fois d’une région Azure vers une autre, vous pouvez choisir le réseau cible dans le cadre du même processus.</span><span class="sxs-lookup"><span data-stu-id="66753-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="66753-119">Site Recovery crée des mappages réseau de la région source à la région cible et de la région cible à la région source, en fonction de cette sélection.</span><span class="sxs-lookup"><span data-stu-id="66753-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="66753-121">Par défaut, Site Recovery crée dans la région cible un réseau qui est identique au réseau source, en ajoutant « -asr » comme suffixe au nom du réseau source.</span><span class="sxs-lookup"><span data-stu-id="66753-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="66753-122">Vous pouvez choisir un réseau déjà créé en cliquant sur Personnaliser.</span><span class="sxs-lookup"><span data-stu-id="66753-122">You can choose an already created network by clicking Customize.</span></span>

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="66753-124">Si le mappage réseau est déjà fait, vous ne pouvez pas changer le réseau virtuel cible lors de l’activation de la réplication.</span><span class="sxs-lookup"><span data-stu-id="66753-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="66753-125">Pour le changer, modifiez le mappage réseau existant.</span><span class="sxs-lookup"><span data-stu-id="66753-125">To change it, modify existing network mapping.</span></span>  

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="66753-128">Si vous modifiez un mappage réseau de la région 1 à la région 2, n’oubliez pas de modifier aussi le mappage réseau de la région 2 à la région 1.</span><span class="sxs-lookup"><span data-stu-id="66753-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="66753-129">Sélection de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="66753-129">Subnet selection</span></span>
<span data-ttu-id="66753-130">Le sous-réseau de la machine virtuelle cible est sélectionné en fonction du nom du sous-réseau de la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="66753-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="66753-131">Si un sous-réseau portant le même nom que celui de la machine virtuelle source est disponible sur le réseau cible, il est choisi pour la machine virtuelle cible.</span><span class="sxs-lookup"><span data-stu-id="66753-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="66753-132">S’il n’y a aucun sous-réseau du même nom sur le réseau cible, le premier sous-réseau dans l’ordre alphabétique est choisi comme sous-réseau cible.</span><span class="sxs-lookup"><span data-stu-id="66753-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="66753-133">Vous pouvez modifier ce sous-réseau en accédant aux paramètres Calcul et réseau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66753-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Modifier le sous-réseau](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="66753-135">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="66753-135">IP address</span></span>

<span data-ttu-id="66753-136">L’adresse IP pour chaque interface réseau de la machine virtuelle cible est choisie comme suit :</span><span class="sxs-lookup"><span data-stu-id="66753-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="66753-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="66753-137">DHCP</span></span>
<span data-ttu-id="66753-138">Si l’interface réseau de la machine virtuelle source utilise le protocole DHCP, l’interface réseau de la machine virtuelle cible est également définie avec DHCP.</span><span class="sxs-lookup"><span data-stu-id="66753-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="66753-139">Adresse IP statique</span><span class="sxs-lookup"><span data-stu-id="66753-139">Static IP</span></span>
<span data-ttu-id="66753-140">Si l’interface réseau de la machine virtuelle source utilise une adresse IP statique, l’interface réseau de la machine virtuelle cible est également configurée pour utiliser une adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="66753-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="66753-141">L’adresse IP statique est choisie comme suit :</span><span class="sxs-lookup"><span data-stu-id="66753-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="66753-142">Même espace d’adressage</span><span class="sxs-lookup"><span data-stu-id="66753-142">Same address space</span></span>

<span data-ttu-id="66753-143">Si les sous-réseaux source et cible ont le même espace d’adressage, l’adresse IP cible est configurée comme identique à l’adresse IP de l’interface réseau de la machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="66753-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="66753-144">Si la même adresse IP n’est pas disponible, une autre adresse IP disponible est définie comme adresse IP cible.</span><span class="sxs-lookup"><span data-stu-id="66753-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="66753-145">Espace d’adressage différent</span><span class="sxs-lookup"><span data-stu-id="66753-145">Different address space</span></span>

<span data-ttu-id="66753-146">Si les sous-réseaux source et cible ont un espace d’adressage différent, l’adresse IP cible est configurée avec n’importe quelle adresse IP disponible sur le sous-réseau cible.</span><span class="sxs-lookup"><span data-stu-id="66753-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="66753-147">Vous pouvez modifier l’adresse IP cible sur chaque interface réseau en accédant aux paramètres Calcul et réseau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66753-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66753-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66753-148">Next steps</span></span>

- <span data-ttu-id="66753-149">En savoir plus sur la [mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="66753-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
