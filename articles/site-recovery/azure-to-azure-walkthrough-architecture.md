---
title: "architecture de hello aaaReview pour la réplication de machines virtuelles Azure entre les régions Azure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication des machines virtuelles Azure entre les régions Azure à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="71940-103">Étape 1 : Passez en revue l’architecture hello pour la réplication de machine virtuelle Azure entre les régions Azure</span><span class="sxs-lookup"><span data-stu-id="71940-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="71940-104">Après avoir examiné hello [étapes](azure-to-azure-walkthrough-overview.md) pour ce déploiement, lisez cette composants de l’article toounderstand hello et les processus utilisés lors de la réplication et la récupération des machines virtuelles (VM) à partir d’une région Azure tooanother, à l’aide de [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71940-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="71940-105">Lorsque vous avez terminé l’article de hello, doit avoir une bonne compréhension du fonctionne de la région de tooanother de réplication de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="71940-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="71940-106">Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="71940-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="71940-107">Réplication de machine virtuelle Azure avec hello service Site Recovery est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="71940-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="71940-108">Composants architecturaux</span><span class="sxs-lookup"><span data-stu-id="71940-108">Architectural components</span></span>

<span data-ttu-id="71940-109">Hello suivant schéma fournit une vue d’ensemble d’un environnement de machine virtuelle Azure dans une région spécifique (dans cet exemple, hello emplacement de l’est des États-Unis).</span><span class="sxs-lookup"><span data-stu-id="71940-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="71940-110">Dans un environnement de machine virtuelle Azure :</span><span class="sxs-lookup"><span data-stu-id="71940-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="71940-111">Les applications peuvent s’exécuter sur des machines équipées de disques réparties sur plusieurs comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="71940-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="71940-112">Hello machines virtuelles peut être inclus dans un ou plusieurs sous-réseaux dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="71940-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![environnement client](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="71940-114">Processus de réplication</span><span class="sxs-lookup"><span data-stu-id="71940-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="71940-115">Étape 1</span><span class="sxs-lookup"><span data-stu-id="71940-115">Step 1</span></span>

<span data-ttu-id="71940-116">Lorsque vous activez la réplication de machine virtuelle Azure Bonjour portail Azure, hello les ressources affichées Bonjour suivant de schéma et table sont automatiquement créées dans la région cible hello.</span><span class="sxs-lookup"><span data-stu-id="71940-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="71940-117">Par défaut, les ressources sont créées en fonction des paramètres de la région source.</span><span class="sxs-lookup"><span data-stu-id="71940-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="71940-118">Vous pouvez personnaliser les paramètres de cible de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="71940-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="71940-119">[En savoir plus](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="71940-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Activer le processus de réplication, étape 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="71940-121">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="71940-121">**Resource**</span></span> | <span data-ttu-id="71940-122">**Détails**</span><span class="sxs-lookup"><span data-stu-id="71940-122">**Details**</span></span>
--- | ---
<span data-ttu-id="71940-123">**Groupe de ressources cible**</span><span class="sxs-lookup"><span data-stu-id="71940-123">**Target resource group**</span></span> | <span data-ttu-id="71940-124">Bonjour toowhich de groupe de ressources appartiennent des machines virtuelles répliquées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="71940-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="71940-125">**Réseau virtuel cible**</span><span class="sxs-lookup"><span data-stu-id="71940-125">**Target virtual network**</span></span> | <span data-ttu-id="71940-126">Hello du réseau virtuel dans lequel les machines virtuelles répliquées sont situés après le basculement.</span><span class="sxs-lookup"><span data-stu-id="71940-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="71940-127">Un mappage réseau est créé entre les réseaux virtuels source et cible, et inversement.</span><span class="sxs-lookup"><span data-stu-id="71940-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="71940-128">**Comptes Stockage de cache**</span><span class="sxs-lookup"><span data-stu-id="71940-128">**Cache storage accounts**</span></span> | <span data-ttu-id="71940-129">Avant que les modifications sur la source de que machines virtuelles sont répliquées toohello compte de stockage cible, elles sont suivies et envoyés le compte de stockage de cache toohello dans l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="71940-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="71940-130">Cela garantit un impact minimal sur les applications de production en cours d’exécution sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="71940-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="71940-131">**Comptes de stockage cibles**</span><span class="sxs-lookup"><span data-stu-id="71940-131">**Target storage accounts**</span></span>  | <span data-ttu-id="71940-132">Comptes de stockage de données de hello cibles emplacement toowhich hello est répliquée.</span><span class="sxs-lookup"><span data-stu-id="71940-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="71940-133">**Groupes à haute disponibilité cibles**</span><span class="sxs-lookup"><span data-stu-id="71940-133">**Target availability sets**</span></span>  | <span data-ttu-id="71940-134">Groupes à haute disponibilité dans le hello répliquée les machines virtuelles sont situés après le basculement.</span><span class="sxs-lookup"><span data-stu-id="71940-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="71940-135">Étape 2</span><span class="sxs-lookup"><span data-stu-id="71940-135">Step 2</span></span>

<span data-ttu-id="71940-136">Comme la réplication est activée, hello extension service mobilité de la récupération de Site est automatiquement installé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71940-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="71940-137">suivant de Hello se produit :</span><span class="sxs-lookup"><span data-stu-id="71940-137">hello following occurs:</span></span>

1. <span data-ttu-id="71940-138">Hello machine virtuelle est enregistré dans la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="71940-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="71940-139">La réplication continue est configurée pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71940-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="71940-140">Données écrit sur la machine virtuelle de hello disques sont en permanence transférés du compte de stockage de cache toohello dans l’emplacement source de hello.</span><span class="sxs-lookup"><span data-stu-id="71940-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Activer le processus de réplication, étape 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="71940-142">Notez que Site Recovery n’a jamais besoin entrant connectivité toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71940-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="71940-143">Uniquement sortant service de connectivité tooSite récupération les adresses URL/IP, les adresses URL/IP authentification Office 365 et adresses de compte de stockage du cache est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="71940-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="71940-144">Processus de réplication continue</span><span class="sxs-lookup"><span data-stu-id="71940-144">Continuous replication process</span></span>

<span data-ttu-id="71940-145">Une fois que l’utilisation de la réplication continue, disque écritures sont immédiatement transférées compte de stockage de cache toohello.</span><span class="sxs-lookup"><span data-stu-id="71940-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="71940-146">Récupération de site traite les données de hello et l’envoie toohello compte de stockage cible.</span><span class="sxs-lookup"><span data-stu-id="71940-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="71940-147">Une fois le traitement des données de hello, points de récupération sont générées dans le compte de stockage cible hello quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="71940-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="71940-148">Processus de basculement</span><span class="sxs-lookup"><span data-stu-id="71940-148">Failover process</span></span>

<span data-ttu-id="71940-149">Lorsque vous démarrez un basculement, hello qu'ordinateurs virtuels sont créés dans le groupe de ressources cible hello, réseau virtuel cible, sous-réseau cible et hello ciblent à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="71940-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="71940-150">Lors d’un basculement, vous pouvez utiliser n’importe quel point de récupération.</span><span class="sxs-lookup"><span data-stu-id="71940-150">During a failover, you can use any recovery point.</span></span>

![Processus de basculement](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="71940-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71940-152">Next steps</span></span>

<span data-ttu-id="71940-153">Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="71940-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
