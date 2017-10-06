---
title: "aaaHow est la réplication entre le travail de régions Azure dans Azure Site Recovery machine virtuelle Azure ?  | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication des machines virtuelles Azure entre des régions Azure à l’aide du service d’Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="57e02-104">Comment la réplication de machine virtuelle Azure fonctionne-t-elle dans Site Recovery ?</span><span class="sxs-lookup"><span data-stu-id="57e02-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="57e02-105">Cet article décrit les composants hello et les processus impliqués dans la réplication et la récupération des machines virtuelles (VM) à partir d’une région tooanother à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="57e02-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="57e02-106">Réplication de machine virtuelle Azure avec hello service Site Recovery est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="57e02-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="57e02-107">Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="57e02-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="57e02-108">Composants architecturaux</span><span class="sxs-lookup"><span data-stu-id="57e02-108">Architectural components</span></span>

<span data-ttu-id="57e02-109">Hello suivant schéma fournit une vue d’ensemble d’un environnement de machine virtuelle Azure dans une région spécifique (dans cet exemple, hello emplacement de l’est des États-Unis).</span><span class="sxs-lookup"><span data-stu-id="57e02-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="57e02-110">Dans un environnement de machine virtuelle Azure :</span><span class="sxs-lookup"><span data-stu-id="57e02-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="57e02-111">Les applications peuvent s’exécuter sur des machines équipées de disques réparties sur plusieurs comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="57e02-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="57e02-112">Hello machines virtuelles peut être inclus dans un ou plusieurs sous-réseaux dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="57e02-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![environnement client](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="57e02-114">En savoir plus sur les conditions préalables au déploiement de hello et les besoins en hello [matrice de prise en charge](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="57e02-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="57e02-115">Processus de réplication</span><span class="sxs-lookup"><span data-stu-id="57e02-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="57e02-116">Étape 1</span><span class="sxs-lookup"><span data-stu-id="57e02-116">Step 1</span></span>

<span data-ttu-id="57e02-117">Lorsque vous activez la réplication de machine virtuelle Azure Bonjour portail Azure, hello les ressources affichées Bonjour suivant de schéma et table sont automatiquement créées dans la région cible hello.</span><span class="sxs-lookup"><span data-stu-id="57e02-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="57e02-118">Par défaut, les ressources sont créées en fonction des paramètres de la région source.</span><span class="sxs-lookup"><span data-stu-id="57e02-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="57e02-119">Vous pouvez personnaliser les paramètres de cible de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="57e02-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="57e02-120">[En savoir plus](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="57e02-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Activer le processus de réplication, étape 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="57e02-122">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="57e02-122">**Resource**</span></span> | <span data-ttu-id="57e02-123">**Détails**</span><span class="sxs-lookup"><span data-stu-id="57e02-123">**Details**</span></span>
--- | ---
<span data-ttu-id="57e02-124">**Groupe de ressources cible**</span><span class="sxs-lookup"><span data-stu-id="57e02-124">**Target resource group**</span></span> | <span data-ttu-id="57e02-125">Bonjour toowhich de groupe de ressources appartiennent des machines virtuelles répliquées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="57e02-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="57e02-126">**Réseau virtuel cible**</span><span class="sxs-lookup"><span data-stu-id="57e02-126">**Target virtual network**</span></span> | <span data-ttu-id="57e02-127">Hello du réseau virtuel dans lequel les machines virtuelles répliquées sont situés après le basculement.</span><span class="sxs-lookup"><span data-stu-id="57e02-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="57e02-128">Un mappage réseau est créé entre les réseaux virtuels source et cible, et inversement.</span><span class="sxs-lookup"><span data-stu-id="57e02-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="57e02-129">**Comptes Stockage de cache**</span><span class="sxs-lookup"><span data-stu-id="57e02-129">**Cache storage accounts**</span></span> | <span data-ttu-id="57e02-130">Avant que les modifications sur la source de que machines virtuelles sont répliquées toohello compte de stockage cible, elles sont suivies et envoyés le compte de stockage de cache toohello dans l’emplacement cible de hello.</span><span class="sxs-lookup"><span data-stu-id="57e02-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="57e02-131">Cela garantit un impact minimal sur les applications de production en cours d’exécution sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="57e02-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="57e02-132">**Comptes de stockage cibles**</span><span class="sxs-lookup"><span data-stu-id="57e02-132">**Target storage accounts**</span></span>  | <span data-ttu-id="57e02-133">Comptes de stockage de données de hello cibles emplacement toowhich hello est répliquée.</span><span class="sxs-lookup"><span data-stu-id="57e02-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="57e02-134">**Groupes à haute disponibilité cibles**</span><span class="sxs-lookup"><span data-stu-id="57e02-134">**Target availability sets**</span></span>  | <span data-ttu-id="57e02-135">Groupes à haute disponibilité dans le hello répliquée les machines virtuelles sont situés après le basculement.</span><span class="sxs-lookup"><span data-stu-id="57e02-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="57e02-136">Étape 2</span><span class="sxs-lookup"><span data-stu-id="57e02-136">Step 2</span></span>

<span data-ttu-id="57e02-137">Comme la réplication est activée, hello extension service mobilité de la récupération de Site est automatiquement installé sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57e02-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="57e02-138">suivant de Hello se produit :</span><span class="sxs-lookup"><span data-stu-id="57e02-138">hello following occurs:</span></span>

1. <span data-ttu-id="57e02-139">Hello machine virtuelle est enregistré dans la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="57e02-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="57e02-140">La réplication continue est configurée pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57e02-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="57e02-141">Données écrit sur la machine virtuelle de hello disques sont en permanence transférés du compte de stockage de cache toohello dans l’emplacement source de hello.</span><span class="sxs-lookup"><span data-stu-id="57e02-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Activer le processus de réplication, étape 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="57e02-143">Récupération de site n’a jamais besoin connectivité entrante toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57e02-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="57e02-144">Hello machine virtuelle doit uniquement connectivité sortante tooSite récupération service URL/adresses IP Office 365 authentification URL/adresses IP et adresses de compte de stockage du cache.</span><span class="sxs-lookup"><span data-stu-id="57e02-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="57e02-145">Pour plus d’informations, consultez hello [des conseils de mise en réseau pour la réplication des machines virtuelles](site-recovery-azure-to-azure-networking-guidance.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="57e02-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="57e02-146">Processus de réplication continue</span><span class="sxs-lookup"><span data-stu-id="57e02-146">Continuous replication process</span></span>

<span data-ttu-id="57e02-147">Une fois que l’utilisation de la réplication continue, disque écritures sont immédiatement transférées compte de stockage de cache toohello.</span><span class="sxs-lookup"><span data-stu-id="57e02-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="57e02-148">Récupération de site traite les données de hello et l’envoie toohello compte de stockage cible.</span><span class="sxs-lookup"><span data-stu-id="57e02-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="57e02-149">Une fois le traitement des données de hello, points de récupération sont générées dans le compte de stockage cible hello quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="57e02-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="57e02-150">Processus de basculement</span><span class="sxs-lookup"><span data-stu-id="57e02-150">Failover process</span></span>

<span data-ttu-id="57e02-151">Lorsque vous démarrez un basculement, hello qu'ordinateurs virtuels sont créés dans le groupe de ressources cible hello, réseau virtuel cible, sous-réseau cible et hello ciblent à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="57e02-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="57e02-152">Lors d’un basculement, vous pouvez utiliser n’importe quel point de récupération.</span><span class="sxs-lookup"><span data-stu-id="57e02-152">During a failover, you can use any recovery point.</span></span>

![Processus de basculement](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="57e02-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57e02-154">Next steps</span></span>

- <span data-ttu-id="57e02-155">En savoir plus sur la [mise en réseau](site-recovery-azure-to-azure-networking-guidance.md) pour la réplication de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="57e02-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="57e02-156">Suivez une procédure pas à pas trop[répliquer les machines virtuelles Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="57e02-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
