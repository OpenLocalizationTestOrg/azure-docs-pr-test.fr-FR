---
title: "aaaReplicate un déploiement à plusieurs niveaux Citrix XenDesktop et XenApp à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooprotect et récupérez de Citrix XenDesktop et XenApp les déploiements à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="5b1e4-103">Répliquer un déploiement Citrix XenApp et XenDesktop multiniveau à l’aide d’Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5b1e4-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="5b1e4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5b1e4-104">Overview</span></span>

<span data-ttu-id="5b1e4-105">Citrix XenDesktop est une solution de virtualisation de bureau qui fournit des ordinateurs de bureau et des applications sous la forme d’un utilisateur de tooany à la demande de service, n’importe où.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="5b1e4-106">Avec une technologie de remise FlexCast XenDesktop peut rapidement et en toute sécurité fournir des applications et bureaux toousers.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="5b1e4-107">Aujourd’hui, Citrix XenApp ne fournit aucune fonctionnalité de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="5b1e4-108">Une solution de récupération d’urgence, devraient permettre la modélisation des plans de récupération autour hello au-dessus des architectures d’applications complexes et également avoir hello capacité tooadd personnalisé étapes toohandle mappages d’application entre les différents niveaux assurant ainsi une par simple clic que capture la solution dans l’événement hello d’un sinistre début tooa diminuer RTO.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="5b1e4-109">Ce document fournit des instructions pas à pas pour la création d’une solution de récupération d’urgence pour vos déploiements locaux de Citrix XenApp sur les plateformes Hyper-V et VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="5b1e4-110">Ce document décrit également comment tooperform un test de basculement (extraction de récupération d’urgence) et tooAzure basculement non planifié à l’aide de plans de récupération, les configurations de hello pris en charge et les composants requis.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5b1e4-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5b1e4-111">Prerequisites</span></span>

<span data-ttu-id="5b1e4-112">Avant de commencer, assurez-vous que vous comprenez les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="5b1e4-113">Réplication d’un tooAzure de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b1e4-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="5b1e4-114">Comment trop[concevoir un réseau de récupération](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="5b1e4-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="5b1e4-115">Effectuer un tooAzure de basculement de test</span><span class="sxs-lookup"><span data-stu-id="5b1e4-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="5b1e4-116">Effectuer un basculement tooAzure</span><span class="sxs-lookup"><span data-stu-id="5b1e4-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="5b1e4-117">Comment trop[répliquer un contrôleur de domaine](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="5b1e4-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="5b1e4-118">Comment trop[répliquer de SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="5b1e4-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="5b1e4-119">Modèles de déploiement</span><span class="sxs-lookup"><span data-stu-id="5b1e4-119">Deployment patterns</span></span>

<span data-ttu-id="5b1e4-120">Une batterie de serveurs Citrix XenApp et XenDesktop a généralement hello suivant le modèle de déploiement :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="5b1e4-121">**Modèle de déploiement**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-121">**Deployment pattern**</span></span>

<span data-ttu-id="5b1e4-122">Déploiement Citrix XenApp et XenDesktop avec serveur DNS Active Directory, serveur de base de données SQL, Citrix Delivery Controller, serveur StoreFront, XenApp Master (VDA) et serveur de licences Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="5b1e4-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Modèle de déploiement 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="5b1e4-124">Prise en charge de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5b1e4-124">Site Recovery support</span></span>

<span data-ttu-id="5b1e4-125">Pour les besoins de hello de cet article, Citrix des déploiements sur des machines virtuelles VMware gérées par vSphere 6.0 / System Center VMM 2012 R2 ont été utilisé toosetup de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="5b1e4-126">Source et cible</span><span class="sxs-lookup"><span data-stu-id="5b1e4-126">Source and target</span></span>

<span data-ttu-id="5b1e4-127">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-127">**Scenario**</span></span> | <span data-ttu-id="5b1e4-128">**site secondaire de tooa**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-128">**tooa secondary site**</span></span> | <span data-ttu-id="5b1e4-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="5b1e4-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-130">**Hyper-V**</span></span> | <span data-ttu-id="5b1e4-131">Non compris</span><span class="sxs-lookup"><span data-stu-id="5b1e4-131">Not in scope</span></span> | <span data-ttu-id="5b1e4-132">Oui</span><span class="sxs-lookup"><span data-stu-id="5b1e4-132">Yes</span></span>
<span data-ttu-id="5b1e4-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-133">**VMware**</span></span> | <span data-ttu-id="5b1e4-134">Non compris</span><span class="sxs-lookup"><span data-stu-id="5b1e4-134">Not in scope</span></span> | <span data-ttu-id="5b1e4-135">Oui</span><span class="sxs-lookup"><span data-stu-id="5b1e4-135">Yes</span></span>
<span data-ttu-id="5b1e4-136">**Serveur physique**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-136">**Physical server**</span></span> | <span data-ttu-id="5b1e4-137">Non compris</span><span class="sxs-lookup"><span data-stu-id="5b1e4-137">Not in scope</span></span> | <span data-ttu-id="5b1e4-138">Oui</span><span class="sxs-lookup"><span data-stu-id="5b1e4-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="5b1e4-139">Versions</span><span class="sxs-lookup"><span data-stu-id="5b1e4-139">Versions</span></span>
<span data-ttu-id="5b1e4-140">Les clients peuvent déployer des composants XenApp en tant que machines virtuelles s’exécutant sur Hyper-V ou VMware ou en tant que serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="5b1e4-141">Azure Site Recovery peut protéger les deux tooAzure déploiements physiques et virtuels.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="5b1e4-142">Étant donné que XenApp 7.7 ou version ultérieure est pris en charge dans Azure, seuls les déploiements avec ces versions peuvent être basculés tooAzure pour la migration ou de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="5b1e4-143">Tookeep choses à l’esprit</span><span class="sxs-lookup"><span data-stu-id="5b1e4-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="5b1e4-144">Protection et la récupération de site sur les déploiements à l’aide du système d’exploitation serveur machines toodeliver XenApp applications publiées et XenApp publié des postes de travail est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="5b1e4-145">Protection et récupération des déploiements sur site à l’aide du bureau du système d’exploitation de machines toodeliver Desktop VDI pour les bureaux virtuels du client, y compris Windows 10, n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="5b1e4-146">Il s’agit, car la récupération automatique du système ne prend pas en charge la récupération hello d’ordinateurs avec le bureau OS'es.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="5b1e4-147">De plus, certaines versions de postes de travail virtuels clients (par exemple</span><span class="sxs-lookup"><span data-stu-id="5b1e4-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="5b1e4-148">Windows 7) ne sont pas encore prises en charge pour la gestion des licences dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="5b1e4-149">[Apprenez-en plus](https://azure.microsoft.com/pricing/licensing-faq/) sur les licences pour les bureaux client/serveur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="5b1e4-150">Azure Site Recovery ne peut pas répliquer et protéger les clones MCS ou PVS locaux existants.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="5b1e4-151">Vous devez toorecreate ces clones Azure RM configuration à partir du contrôleur de remise.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="5b1e4-152">NetScaler ne peut pas être protégé à l’aide d’Azure Site Recovery, car NetScaler repose sur FreeBSD et Azure Site Recovery ne prend pas en charge la protection du système d’exploitation FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="5b1e4-153">Vous devez toodeploy et configurer un nouveau dispositif NetScaler de marché d’Azure après basculement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="5b1e4-154">Réplication des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="5b1e4-154">Replicating virtual machines</span></span>

<span data-ttu-id="5b1e4-155">Hello suivant des composants de hello Citrix XenApp déploiement devez toobe protégé tooenable réplication et la récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="5b1e4-156">Protection du serveur DNS Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b1e4-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="5b1e4-157">Protection du serveur de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5b1e4-157">Protection of SQL database server</span></span>
* <span data-ttu-id="5b1e4-158">Protection de Citrix Delivery Controller</span><span class="sxs-lookup"><span data-stu-id="5b1e4-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="5b1e4-159">Protection du serveur StoreFront</span><span class="sxs-lookup"><span data-stu-id="5b1e4-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="5b1e4-160">Protection de XenApp Master (VDA)</span><span class="sxs-lookup"><span data-stu-id="5b1e4-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="5b1e4-161">Protection du serveur de licences Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="5b1e4-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="5b1e4-162">**Réplication du serveur DNS Active Directory**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-162">**AD DNS server replication**</span></span>

<span data-ttu-id="5b1e4-163">Reportez-vous trop[protéger Active Directory et DNS avec Azure Site Recovery](site-recovery-active-directory.md) sur des conseils pour la réplication et la configuration d’un contrôleur de domaine dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="5b1e4-164">**Réplication du serveur de base de données SQL**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-164">**SQL database Server replication**</span></span>

<span data-ttu-id="5b1e4-165">Reportez-vous trop[protéger SQL Server avec la récupération d’urgence de SQL Server et Azure Site Recovery](site-recovery-sql.md) pour des conseils techniques détaillés sur hello recommandé d’options de protection de serveurs SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="5b1e4-166">Suivez [ce guide](site-recovery-vmware-to-azure.md) toostart réplication hello autres tooAzure de machines virtuelles de composant.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Protection des composants XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="5b1e4-168">**Paramètres Calcul et réseau**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="5b1e4-169">Une fois les ordinateurs hello sont protégés (état est affiché comme « Protégées » sous les éléments répliqués), hello calcul et les paramètres de réseau doivent toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="5b1e4-170">Dans le calcul et réseau > calcul des propriétés, vous pouvez spécifier la taille de nom et la cible de la machine virtuelle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="5b1e4-171">Modifiez toocomply de nom hello aux exigences d’Azure si vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="5b1e4-172">Vous pouvez également afficher et ajouter des informations sur le réseau cible de hello, du sous-réseau et adresse IP qui sera assigné toohello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="5b1e4-173">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-173">Note hello following:</span></span>

* <span data-ttu-id="5b1e4-174">Vous pouvez définir l’adresse IP de hello cible.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-174">You can set hello target IP address.</span></span> <span data-ttu-id="5b1e4-175">Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="5b1e4-176">Si vous définissez une adresse qui n’est pas disponible lors du basculement, hello basculement ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="5b1e4-177">Hello même adresse IP peut servir pour le test de basculement si l’adresse de hello est disponible dans le réseau de basculement de test hello.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="5b1e4-178">Pour le serveur DNS/Active Directory de hello, en conservant hello local adresse vous permet de que spécifier hello même adresse en tant que serveur DNS de hello pour le réseau virtuel Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="5b1e4-179">nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle de cible hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="5b1e4-180">Si le nombre de hello de cartes réseau sur l’ordinateur source de hello est inférieur ou égal toohello le nombre de cartes autorisé pour la taille de la machine cible hello, puis cible de hello aura hello même nombre de cartes en tant que source de hello.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="5b1e4-181">Si nombre hello de cartes pour l’ordinateur virtuel de hello source dépasse nombre hello autorisé pour la taille cible hello puis la taille maximale de la cible hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="5b1e4-182">Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello aura deux cartes.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="5b1e4-183">Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="5b1e4-184">Si l’ordinateur virtuel de hello possède plusieurs cartes réseau qu’ils seront connectent tous toohello même réseau.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="5b1e4-185">Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, puis hello premier celui illustré dans la liste de hello devient carte de réseau par défaut hello Bonjour machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="5b1e4-186">Création d’un plan de récupération</span><span class="sxs-lookup"><span data-stu-id="5b1e4-186">Creating a recovery plan</span></span>

<span data-ttu-id="5b1e4-187">Une fois la réplication est activée pour hello XenApp, composant machines virtuelles, étape suivante de hello est toocreate un plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="5b1e4-188">Un plan de récupération regroupe les machines virtuelles ayant les mêmes exigences de basculement et de récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="5b1e4-189">**Étapes toocreate un plan de récupération**</span><span class="sxs-lookup"><span data-stu-id="5b1e4-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="5b1e4-190">Ajoutez hello XenApp composant virtuels Bonjour un Plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="5b1e4-191">Cliquez sur Plans de récupération -> + Plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="5b1e4-192">Fournit un nom intuitif hello plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="5b1e4-193">Pour les machines virtuelles VMware : sélectionnez Serveur de processus VMware comme source, Microsoft Azure comme cible et Resource Manager comme modèle de déploiement, puis cliquez sur Sélectionner les éléments.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="5b1e4-194">Pour les ordinateurs virtuels Hyper-V : sélectionnez source en tant que serveur VMM, cible en tant que Microsoft Azure et le modèle de déploiement en tant que le Gestionnaire de ressources et cliquez sur Sélectionner des éléments, puis déploiement de XenApp hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="5b1e4-195">Ajout de groupes de machines virtuelles toofailover</span><span class="sxs-lookup"><span data-stu-id="5b1e4-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="5b1e4-196">Plans de récupération peuvent être personnalisé tooadd des groupes de basculement pour les actions de commande, des scripts ou manuel de démarrage spécifique.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="5b1e4-197">Hello, les groupes suivants doivent plan de récupération toobe toohello ajouté.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="5b1e4-198">Groupe de basculement 1 : DNS Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b1e4-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="5b1e4-199">Groupe de basculement 2 : Machines virtuelles SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b1e4-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="5b1e4-200">Groupe de basculement 3 : Machine virtuelle d’image maîtresse VDA</span><span class="sxs-lookup"><span data-stu-id="5b1e4-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="5b1e4-201">Groupe de basculement 4 : Delivery Controller et machines virtuelles de serveur StoreFront</span><span class="sxs-lookup"><span data-stu-id="5b1e4-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="5b1e4-202">Ajout de scripts de plan de récupération toohello</span><span class="sxs-lookup"><span data-stu-id="5b1e4-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="5b1e4-203">Vous pouvez exécuter des scripts avant ou après un groupe spécifique dans un plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="5b1e4-204">Vous pouvez aussi inclure et effectuer des actions manuelles pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="5b1e4-205">plan de récupération personnalisée Hello ressemble à hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="5b1e4-206">Groupe de basculement 1 : DNS Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b1e4-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="5b1e4-207">Groupe de basculement 2 : Machines virtuelles SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b1e4-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="5b1e4-208">Groupe de basculement 3 : Machine virtuelle d’image maîtresse VDA</span><span class="sxs-lookup"><span data-stu-id="5b1e4-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="5b1e4-209">Les étapes 4, 6 et 7 contenant des actions manuelles ou un script sont applicable tooonly un XenApp local > environnement avec des catalogues MCS/PVS.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="5b1e4-210">Action manuelle ou un script de groupe 3 : hello de VDA VM master arrêt Master VDA VM lorsque basculé tooAzure sera en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="5b1e4-211">toocreate nouveaux MCS catalogues à l’aide de l’hébergement de Azure ARM, le maître de hello VDA VM est requis toobe arrêté (de allouée) état.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="5b1e4-212">Hello arrêt machine virtuelle à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="5b1e4-213">Groupe de basculement 4 : Delivery Controller et machines virtuelles de serveur StoreFront</span><span class="sxs-lookup"><span data-stu-id="5b1e4-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="5b1e4-214">Action manuelle ou de script 1 de Groupe 3 :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="5b1e4-215">***Ajouter une connexion hôte Azure ARM***</span><span class="sxs-lookup"><span data-stu-id="5b1e4-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="5b1e4-216">Créer la connexion d’hôte Azure ARM dans tooprovision d’ordinateur de contrôleur de remise nouveaux catalogues MCS dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="5b1e4-217">Suivez les étapes de hello comme expliqué dans cet [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="5b1e4-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="5b1e4-218">Action manuelle ou de script 2 de Groupe 3 :</span><span class="sxs-lookup"><span data-stu-id="5b1e4-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="5b1e4-219">***Recréer les catalogues MCS dans Azure***</span><span class="sxs-lookup"><span data-stu-id="5b1e4-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="5b1e4-220">Hello existant MCS ou PVS clones sur le site principal de hello ne seront pas répliquée tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="5b1e4-221">Vous devez toorecreate ces clones à l’aide de hello répliquées VDA maître et ARM Azure de configuration à partir du contrôleur de remise. Suivez les étapes de hello comme expliqué dans cet [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogues dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![Plan de récupération pour les composants XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="5b1e4-223">Vous pouvez utiliser des scripts à [emplacement](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS avec hello basculé de nouvelles adresses IP de hello > ordinateurs virtuels ou tooattach un équilibrage de charge sur hello a échoué sur l’ordinateur virtuel, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="5b1e4-224">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="5b1e4-224">Doing a test failover</span></span>

<span data-ttu-id="5b1e4-225">Suivez [ce guide](site-recovery-test-failover-to-azure.md) toodo un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![Plan de récupération](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="5b1e4-227">Exécution d’un basculement</span><span class="sxs-lookup"><span data-stu-id="5b1e4-227">Doing a failover</span></span>

<span data-ttu-id="5b1e4-228">Suivez [ce guide](site-recovery-failover.md) lorsque vous effectuez un basculement.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1e4-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b1e4-229">Next steps</span></span>

<span data-ttu-id="5b1e4-230">Pour en savoir plus sur la réplication des déploiements Citrix XenApp et XenDesktop, consultez [ce livre blanc](https://aka.ms/citrix-xenapp-xendesktop-with-asr).</span><span class="sxs-lookup"><span data-stu-id="5b1e4-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="5b1e4-231">Examinez les conseils hello trop[répliquer des autres applications](site-recovery-workload.md) à l’aide de la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="5b1e4-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
