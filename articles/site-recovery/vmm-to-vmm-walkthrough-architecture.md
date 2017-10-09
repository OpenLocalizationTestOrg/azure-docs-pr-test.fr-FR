---
title: "architecture de hello aaaReview pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de l’architecture de hello pour répliquer des ordinateurs virtuels Hyper-V tooa secondaire System Center VMM site local avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="99d1b-103">Étape 1 : Passez en revue l’architecture hello pour le site secondaire de tooa de réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="99d1b-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="99d1b-104">Cet article décrit les composants hello et processus impliqués lors de la réplication locale Hyper-V, machines virtuelles (VM) dans des clouds System Center Virtual Machine Manager (VMM), à l’aide de hello le site VMM secondaire tooa [Azure Site Recovery](site-recovery-overview.md)service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="99d1b-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="99d1b-105">Valider les commentaires en bas de hello de cet article ou Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="99d1b-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="99d1b-106">Composants architecturaux</span><span class="sxs-lookup"><span data-stu-id="99d1b-106">Architectural components</span></span>

<span data-ttu-id="99d1b-107">Voici ce que vous avez besoin pour la réplication de site VMM secondaire de machines virtuelles Hyper-V tooa.</span><span class="sxs-lookup"><span data-stu-id="99d1b-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="99d1b-108">**Composant**</span><span class="sxs-lookup"><span data-stu-id="99d1b-108">**Component**</span></span> | <span data-ttu-id="99d1b-109">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="99d1b-109">**Location**</span></span> | <span data-ttu-id="99d1b-110">**Détails**</span><span class="sxs-lookup"><span data-stu-id="99d1b-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="99d1b-111">**Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="99d1b-111">**Azure**</span></span> | <span data-ttu-id="99d1b-112">Abonnement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="99d1b-112">Subscription in Azure.</span></span> | <span data-ttu-id="99d1b-113">Vous créez un coffre Recovery Services Bonjour abonnement Azure, tooorchestrate et gérez la réplication entre les emplacements de VMM.</span><span class="sxs-lookup"><span data-stu-id="99d1b-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="99d1b-114">**Serveur VMM**</span><span class="sxs-lookup"><span data-stu-id="99d1b-114">**VMM server**</span></span> | <span data-ttu-id="99d1b-115">Vous avez besoin d’un emplacement VMM principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="99d1b-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="99d1b-116">Nous vous recommandons d’un serveur VMM dans le site principal de hello et un site secondaire de hello</span><span class="sxs-lookup"><span data-stu-id="99d1b-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="99d1b-117">**Serveur Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="99d1b-117">**Hyper-V server**</span></span> |  <span data-ttu-id="99d1b-118">Serveurs d’hôte Hyper-V un ou plusieurs dans des clouds VMM principaux et secondaires hello.</span><span class="sxs-lookup"><span data-stu-id="99d1b-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="99d1b-119">Données sont répliquées entre hello serveurs principaux et secondaires Hyper-V hôte via hello LAN ou VPN, à l’aide de l’authentification Kerberos ou le certificat.</span><span class="sxs-lookup"><span data-stu-id="99d1b-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="99d1b-120">**Machines virtuelles Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="99d1b-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="99d1b-121">Sur le serveur hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="99d1b-121">On Hyper-V host server.</span></span> | <span data-ttu-id="99d1b-122">serveur hôte de Hello source doit avoir au moins une machine virtuelle que vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="99d1b-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="99d1b-123">Processus de réplication</span><span class="sxs-lookup"><span data-stu-id="99d1b-123">Replication process</span></span>

1. <span data-ttu-id="99d1b-124">Vous définir hello compte Azure, créez un coffre Recovery Services et ce que vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="99d1b-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="99d1b-125">Vous configurez hello source et cible paramètres de réplication, notamment l’installation hello fournisseur Azure Site Recovery sur les serveurs VMM et l’agent de Microsoft Azure Recovery Services hello sur chaque ordinateur hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="99d1b-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="99d1b-126">Vous créez une stratégie de réplication pour la source de hello cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="99d1b-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="99d1b-127">stratégie de Hello est appliqué tooall machines virtuelles situées sur des ordinateurs hôtes dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="99d1b-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="99d1b-128">Activation de la réplication pour chaque VMM et la réplication initiale d’une machine virtuelle a lieu conformément aux paramètres que vous choisissez hello.</span><span class="sxs-lookup"><span data-stu-id="99d1b-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="99d1b-129">À l’issue de la réplication initiale, la réplication des modifications delta commence.</span><span class="sxs-lookup"><span data-stu-id="99d1b-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="99d1b-130">Les modifications qui font l’objet d’un suivi sont conservées dans un fichier .hrl.</span><span class="sxs-lookup"><span data-stu-id="99d1b-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Tooon-site local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="99d1b-132">Processus de basculement et de restauration automatique</span><span class="sxs-lookup"><span data-stu-id="99d1b-132">Failover and failback process</span></span>

1. <span data-ttu-id="99d1b-133">Vous pouvez effectuer un [basculement](site-recovery-failover.md) planifié ou non planifié entre des sites locaux.</span><span class="sxs-lookup"><span data-stu-id="99d1b-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="99d1b-134">Si vous exécutez un basculement planifié, alors que les machines virtuelles source sont arrêtés tooensure aucune perte de données.</span><span class="sxs-lookup"><span data-stu-id="99d1b-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="99d1b-135">Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md) basculement tooorchestrate de plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="99d1b-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="99d1b-136">Si vous effectuez un basculement non planifié tooa site secondaire une fois que les machines de basculement hello dans l’emplacement secondaire de hello ne sont pas activés pour la réplication ou de protection.</span><span class="sxs-lookup"><span data-stu-id="99d1b-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="99d1b-137">Si vous avez exécuté un basculement planifié, après le basculement de hello, dans l’emplacement secondaire de hello, les ordinateurs sont protégés.</span><span class="sxs-lookup"><span data-stu-id="99d1b-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="99d1b-138">Ensuite, vous validez hello basculement toostart accès hello la charge de travail à partir de l’ordinateur virtuel de réplication hello.</span><span class="sxs-lookup"><span data-stu-id="99d1b-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="99d1b-139">Lorsque votre site principal est à nouveau disponible, vous lancez tooreplicate la réplication inverse de hello toohello de site secondaire principal.</span><span class="sxs-lookup"><span data-stu-id="99d1b-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="99d1b-140">La réplication inverse place les ordinateurs virtuels de hello dans un état protégé, mais hello de centre de données secondaire est toujours un emplacement Directory hello.</span><span class="sxs-lookup"><span data-stu-id="99d1b-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="99d1b-141">site principal de hello toomake dans un emplacement Directory hello là encore, vous initiez un basculement planifié à partir de tooprimary secondaire, suivie de la réplication inverse un autre.</span><span class="sxs-lookup"><span data-stu-id="99d1b-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="99d1b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="99d1b-142">Next steps</span></span>

<span data-ttu-id="99d1b-143">Accédez trop[étape 2 : passez en revue les conditions préalables de hello et limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="99d1b-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
