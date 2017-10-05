---
title: "Présentation de l’architecture utilisée pour la réplication Hyper-V sur un site secondaire avec Azure Site Recovery | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble de l’architecture utilisée pour la réplication de machines virtuelles Hyper-V locales sur un site System Center VMM secondaire avec Azure Site Recovery."
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
ms.openlocfilehash: b78cd0d5a5395873afaddc8856004775f447e8ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="68fe1-103">Étape 1 : présentation de l’architecture utilisée pour la réplication Hyper-V sur un site secondaire</span><span class="sxs-lookup"><span data-stu-id="68fe1-103">Step 1: Review the architecture for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="68fe1-104">Cet article décrit les composants et les processus impliqués dans la réplication des machines virtuelles Hyper-V locales dans des clouds System Center Virtual Machine Manager (VMM) sur un site VMM secondaire à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68fe1-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM site using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="68fe1-105">Publiez des commentaires au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="68fe1-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="68fe1-106">Composants architecturaux</span><span class="sxs-lookup"><span data-stu-id="68fe1-106">Architectural components</span></span>

<span data-ttu-id="68fe1-107">Voici ce dont vous avez besoin pour la réplication des machines virtuelles Hyper-V sur un site VMM secondaire.</span><span class="sxs-lookup"><span data-stu-id="68fe1-107">Here's what you need for replicating Hyper-V VMs to a secondary VMM site.</span></span>

<span data-ttu-id="68fe1-108">**Composant**</span><span class="sxs-lookup"><span data-stu-id="68fe1-108">**Component**</span></span> | <span data-ttu-id="68fe1-109">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="68fe1-109">**Location**</span></span> | <span data-ttu-id="68fe1-110">**Détails**</span><span class="sxs-lookup"><span data-stu-id="68fe1-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="68fe1-111">**Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="68fe1-111">**Azure**</span></span> | <span data-ttu-id="68fe1-112">Abonnement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="68fe1-112">Subscription in Azure.</span></span> | <span data-ttu-id="68fe1-113">Vous créez un coffre Recovery Services dans l’abonnement Azure pour orchestrer et gérer la réplication entre les emplacements VMM.</span><span class="sxs-lookup"><span data-stu-id="68fe1-113">You create a Recovery Services vault in the Azure subscription, to orchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="68fe1-114">**Serveur VMM**</span><span class="sxs-lookup"><span data-stu-id="68fe1-114">**VMM server**</span></span> | <span data-ttu-id="68fe1-115">Vous avez besoin d’un emplacement VMM principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="68fe1-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="68fe1-116">Nous recommandons l’utilisation d’un serveur VMM dans le site principal et un autre dans le site secondaire</span><span class="sxs-lookup"><span data-stu-id="68fe1-116">We recommend a VMM server in the primary site, and one in the secondary site</span></span> 
<span data-ttu-id="68fe1-117">**Serveur Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="68fe1-117">**Hyper-V server**</span></span> |  <span data-ttu-id="68fe1-118">Un ou plusieurs serveurs hôtes Hyper-V dans les clouds VMM principaux et secondaires.</span><span class="sxs-lookup"><span data-stu-id="68fe1-118">One or more Hyper-V host servers in the primary and secondary VMM clouds.</span></span> | <span data-ttu-id="68fe1-119">Les données sont répliquées entre les serveurs hôtes Hyper-V principal et secondaire via une liaison LAN ou VPN, en utilisant Kerberos ou une authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="68fe1-119">Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="68fe1-120">**Machines virtuelles Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="68fe1-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="68fe1-121">Sur le serveur hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="68fe1-121">On Hyper-V host server.</span></span> | <span data-ttu-id="68fe1-122">Le serveur hôte source doit avoir au moins une machine virtuelle que vous souhaitez répliquer.</span><span class="sxs-lookup"><span data-stu-id="68fe1-122">The source host server should have at least one VM that you want to replicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="68fe1-123">Processus de réplication</span><span class="sxs-lookup"><span data-stu-id="68fe1-123">Replication process</span></span>

1. <span data-ttu-id="68fe1-124">Vous configurez le compte Azure, créez un coffre Recovery Services et spécifiez ce que vous souhaitez répliquer.</span><span class="sxs-lookup"><span data-stu-id="68fe1-124">You set up the Azure account, create a Recovery Services vault, and specify what you want to replicate.</span></span>
2. <span data-ttu-id="68fe1-125">Vous configurez les paramètres de réplication source et cible, notamment l’installation du fournisseur Azure Site Recovery sur les serveurs VMM et l’agent Microsoft Azure Recovery Services sur chaque hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="68fe1-125">You configure the source and target replication settings, which includes installing the Azure Site Recovery Provider on VMM servers, and the Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="68fe1-126">Vous créez une stratégie de réplication pour le cloud VMM source.</span><span class="sxs-lookup"><span data-stu-id="68fe1-126">You create a replication policy for the source VMM cloud.</span></span> <span data-ttu-id="68fe1-127">La stratégie est appliquée à toutes les machines virtuelles situées sur des hôtes dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="68fe1-127">The policy is applied to all VMs located on hosts in the cloud.</span></span>
4. <span data-ttu-id="68fe1-128">Vous activez la réplication pour chaque VMM, et la réplication initiale d’une machine virtuelle a lieu conformément aux paramètres que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="68fe1-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with the settings you choose.</span></span>
5. <span data-ttu-id="68fe1-129">À l’issue de la réplication initiale, la réplication des modifications delta commence.</span><span class="sxs-lookup"><span data-stu-id="68fe1-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="68fe1-130">Les modifications qui font l’objet d’un suivi sont conservées dans un fichier .hrl.</span><span class="sxs-lookup"><span data-stu-id="68fe1-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Local vers local](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="68fe1-132">Processus de basculement et de restauration automatique</span><span class="sxs-lookup"><span data-stu-id="68fe1-132">Failover and failback process</span></span>

1. <span data-ttu-id="68fe1-133">Vous pouvez effectuer un [basculement](site-recovery-failover.md) planifié ou non planifié entre des sites locaux.</span><span class="sxs-lookup"><span data-stu-id="68fe1-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="68fe1-134">Si vous exécutez un basculement planifié, les machines virtuelles sources sont arrêtées pour éviter toute perte de données.</span><span class="sxs-lookup"><span data-stu-id="68fe1-134">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="68fe1-135">Vous pouvez basculer vers une seule machine ou créer des [plans de récupération](site-recovery-create-recovery-plans.md) pour orchestrer le basculement de plusieurs machines.</span><span class="sxs-lookup"><span data-stu-id="68fe1-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="68fe1-136">Si vous effectuez un basculement non planifié vers un site secondaire, une fois l’opération terminée, les machines de l’emplacement secondaire ne sont pas protégées ou réplicables.</span><span class="sxs-lookup"><span data-stu-id="68fe1-136">If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="68fe1-137">Si vous avez lancé un basculement planifié, une fois l’opération terminée, les machines de l’emplacement secondaire sont protégées.</span><span class="sxs-lookup"><span data-stu-id="68fe1-137">If you ran a planned failover, after the failover, machines in the secondary location are protected.</span></span>
5. <span data-ttu-id="68fe1-138">Ensuite, validez le basculement pour accéder à la charge de travail à partir de la machine virtuelle répliquée.</span><span class="sxs-lookup"><span data-stu-id="68fe1-138">Then, you commit the failover to start accessing the workload from the replica VM.</span></span>
6. <span data-ttu-id="68fe1-139">Lorsque votre site principal est à nouveau disponible, vous déclenchez la réplication inverse depuis le site secondaire vers le site principal.</span><span class="sxs-lookup"><span data-stu-id="68fe1-139">When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary.</span></span> <span data-ttu-id="68fe1-140">La réplication inverse affecte aux machines virtuelles l’état protégé, mais l’emplacement actif est toujours le centre de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="68fe1-140">Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.</span></span>
7. <span data-ttu-id="68fe1-141">Pour placer le site principal à l’emplacement actif, lancez un basculement planifié depuis le site secondaire vers le site principal, puis une autre réplication inverse.</span><span class="sxs-lookup"><span data-stu-id="68fe1-141">To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="68fe1-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68fe1-142">Next steps</span></span>

<span data-ttu-id="68fe1-143">Allez à [Step 2: Review the prerequisites and limitations for Hyper-V VM replication to a secondary VMM site](vmm-to-vmm-walkthrough-prerequisites.md) (Étape 2 : vérifier les conditions préalables et les limitations pour la réplication de machine virtuelle Hyper-V sur un site VMM secondaire).</span><span class="sxs-lookup"><span data-stu-id="68fe1-143">Go to [Step 2: Review the prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
