---
title: "aaaPlan mise en réseau pour la réplication Hyper-V (sans System Center VMM) tooAzure avec Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit la planification d’un réseau requis lors de la réplication des ordinateurs virtuels Hyper-V (sans VMM) tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a><span data-ttu-id="6fd40-103">Étape 4 : Planifier la mise en réseau pour la réplication Hyper-V tooAzure</span><span class="sxs-lookup"><span data-stu-id="6fd40-103">Step 4: Plan networking for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="6fd40-104">Cet article résume les considérations de planification lors de la réplication locale tooAzure de machines virtuelles de Hyper-V (sans System Center VMM) à l’aide de hello de réseau [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="6fd40-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="6fd40-105">Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6fd40-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-tooreplica-vms-after-failover"></a><span data-ttu-id="6fd40-106">Connecter des machines virtuelles de tooreplica après le basculement</span><span class="sxs-lookup"><span data-stu-id="6fd40-106">Connecting tooreplica VMs after failover</span></span>

<span data-ttu-id="6fd40-107">Lorsque vous planifiez votre stratégie de basculement et de réplication, une des questions clés de hello est comment tooconnect toohello machine virtuelle Azure après le basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="6fd40-108">Il existe plusieurs options lors de la conception de votre stratégie réseau pour les machines virtuelles réplica Azure :</span><span class="sxs-lookup"><span data-stu-id="6fd40-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="6fd40-109">**Autre adresse IP**: vous pouvez sélectionner toouse une plage d’adresses IP différentes pour hello répliquées réseau d’ordinateurs virtuels de Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-109">**Different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="6fd40-110">Dans cette hello scénario VM Obtient une nouvelle adresse IP après un basculement, et une mise à jour DNS est requis.</span><span class="sxs-lookup"><span data-stu-id="6fd40-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="6fd40-111">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="6fd40-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="6fd40-112">**Même adresse IP**: vous souhaiterez peut-être toouse hello même plage d’adresses IP comme qui dans votre site local principal de réseau, pour hello réseau Azure après le basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-112">**Same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="6fd40-113">Hello conserver des adresses IP mêmes simplifie la récupération hello en réduisant les problèmes de réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-113">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="6fd40-114">Toutefois, lorsque vous effectuez une réplication tooAzure, vous devez les itinéraires tooupdate avec hello nouvel emplacement des adresses IP de hello après le basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-114">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="6fd40-115">Conserver les adresses IP</span><span class="sxs-lookup"><span data-stu-id="6fd40-115">Retain IP addresses</span></span>

<span data-ttu-id="6fd40-116">Récupération de site fournit la fonctionnalité hello tooretain fixée des adresses IP lors du basculement tooAzure, avec un basculement de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6fd40-116">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="6fd40-117">Avec le basculement de sous-réseau, un sous-réseau spécifique est présent sur le Site 1 ou sur le Site 2, mais jamais sur les deux sites simultanément.</span><span class="sxs-lookup"><span data-stu-id="6fd40-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="6fd40-118">Dans l’ordre toomaintain hello espace d’adressage IP dans les événements hello d’un basculement, vous organiser par programme des sous-réseaux de hello hello routeur infrastructure toomove à partir d’un site tooanother.</span><span class="sxs-lookup"><span data-stu-id="6fd40-118">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="6fd40-119">Pendant le basculement, déplacement de sous-réseaux hello avec hello associés à des ordinateurs virtuels protégés.</span><span class="sxs-lookup"><span data-stu-id="6fd40-119">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="6fd40-120">Hello principal inconvénient est que dans l’événement hello d’une défaillance, vous disposez de sous-réseau entier de toomove hello.</span><span class="sxs-lookup"><span data-stu-id="6fd40-120">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="6fd40-121">Exemple de basculement</span><span class="sxs-lookup"><span data-stu-id="6fd40-121">Failover example</span></span>

<span data-ttu-id="6fd40-122">Examinons un exemple de tooAzure de basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-122">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="6fd40-123">La banque Woodgrove, une société fictive, possède une infrastructure locale pour l’hébergement de ses applications métier.</span><span class="sxs-lookup"><span data-stu-id="6fd40-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="6fd40-124">Ses applications mobiles sont hébergées sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="6fd40-125">Connectivité entre machines virtuelles Woodgrove Bank serveurs locaux et Azure est fournie par une connexion (VPN) de site à site entre le réseau de périmètre local hello et hello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="6fd40-126">Cela signifie que VPN qui hello réseau virtuel de la société dans Azure s’affiche comme une extension de leur réseau local.</span><span class="sxs-lookup"><span data-stu-id="6fd40-126">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="6fd40-127">Woodgrove veut toouse Site Recovery tooreplicate localement les charges de travail tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-127">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="6fd40-128">Woodgrove a toodeal avec des applications et des configurations dépendent codé en dur des adresses IP et doivent tooretain des adresses IP pour leurs applications après basculement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-128">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="6fd40-129">Woodgrove a des adresses IP à partir de la plage 172.16.1.0/24, 172.16.2.0/24 tooits les ressources affectées s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="6fd40-130">Pour Woodgrove toobe en mesure de tooreplicate son tooAzure de machines virtuelles pendant en conservant hello IP adresses, ce qui est société hello doit toodo :</span><span class="sxs-lookup"><span data-stu-id="6fd40-130">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="6fd40-131">Créez un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-131">Create an Azure virtual network.</span></span> <span data-ttu-id="6fd40-132">Il doit être une extension de hello local réseau, afin que les applications peuvent basculer en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="6fd40-132">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="6fd40-133">Azure permet vous tooadd site-à-site connectivité VPN, en outre, les réseaux virtuels toohello toopoint-à-site connectivité créés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-133">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="6fd40-134">Lorsque vous configurez la connexion de site à site hello, Bonjour Azure réseau, vous pouvez acheminer un emplacement de site du trafic toohello (réseau local) uniquement si la plage d’adresses IP hello est différent de la plage d’adresses IP hello localement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-134">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="6fd40-135">Cela est dû au fait qu’Azure ne prend pas en charge les sous-réseaux étirés.</span><span class="sxs-lookup"><span data-stu-id="6fd40-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="6fd40-136">Par conséquent, si vous avez sous-réseau 192.168.1.0/24 locale, Impossible d’ajouter un 192.168.1.0/24 réseau local Bonjour réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="6fd40-137">Ceci est dû au fait que Azure ne sait pas qu’il en existe aucune machine virtuelle active dans le sous-réseau de hello, et ce sous-réseau hello est en cours de création pour la récupération d’urgence uniquement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-137">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="6fd40-138">toobe toocorrectly en mesure de router le trafic réseau en dehors d’un Azure hello des sous-réseaux dans le réseau de hello et réseau local hello ne doit pas entrer en conflit.</span><span class="sxs-lookup"><span data-stu-id="6fd40-138">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Avant le basculement de sous-réseau](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="6fd40-140">Avant le basculement</span><span class="sxs-lookup"><span data-stu-id="6fd40-140">Before failover</span></span>

1. <span data-ttu-id="6fd40-141">Créez un réseau supplémentaire (par exemple, un réseau de récupération).</span><span class="sxs-lookup"><span data-stu-id="6fd40-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="6fd40-142">Il s’agit hello réseau qui a échoué sur les ordinateurs virtuels sont créés.</span><span class="sxs-lookup"><span data-stu-id="6fd40-142">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="6fd40-143">tooensure qui hello d’adresse IP pour une machine virtuelle est conservée après un basculement, dans les propriétés de machine virtuelle hello > **configurer**, spécifiez hello même adresse IP que hello machine virtuelle a local, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6fd40-143">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="6fd40-144">Lorsque hello machine virtuelle est basculé, Azure Site Recovery attribuera hello fourni tooit d’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="6fd40-144">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Propriétés du réseau](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="6fd40-146">Une fois le basculement déclencheur est déclenché et machines virtuelles de hello sont créés dans Azure avec l’adresse IP de hello requis, vous pouvez vous connecter à l’aide du réseau toohello un [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="6fd40-146">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="6fd40-147">Cette action peut être scriptée.</span><span class="sxs-lookup"><span data-stu-id="6fd40-147">This action can be scripted.</span></span>
5. <span data-ttu-id="6fd40-148">Itinéraires doivent toobe modifiée en conséquence, tooreflect que 192.168.1.0/24 est passée tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6fd40-148">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![Après le basculement de sous-réseau](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="6fd40-150">Après le basculement</span><span class="sxs-lookup"><span data-stu-id="6fd40-150">After failover</span></span>

<span data-ttu-id="6fd40-151">Si vous ne possédez pas de réseau Azure comme illustré ci-dessus, vous pouvez créer une connexion VPN de site à site entre votre site principal et Azure après le basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="6fd40-152">Modifier les adresses IP</span><span class="sxs-lookup"><span data-stu-id="6fd40-152">Change IP addresses</span></span>

<span data-ttu-id="6fd40-153">Cela [billet de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explique comment tooset des hello Azure infrastructure réseau lorsque vous n’avez pas besoin de tooretain IP répond après le basculement.</span><span class="sxs-lookup"><span data-stu-id="6fd40-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="6fd40-154">Il commence par une description de l’application, ressemble à la tooset un réseau local et dans Azure et se termine avec des informations sur l’exécution des basculements.</span><span class="sxs-lookup"><span data-stu-id="6fd40-154">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6fd40-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fd40-155">Next steps</span></span>

<span data-ttu-id="6fd40-156">Accédez trop[étape 5 : préparer le Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6fd40-156">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>