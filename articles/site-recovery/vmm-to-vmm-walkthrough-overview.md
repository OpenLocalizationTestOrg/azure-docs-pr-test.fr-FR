---
title: aaaReplicate des ordinateurs virtuels Hyper-V tooa secondaire deux sites VMM avec Azure Site Recovery | Documents Microsoft
description: "Fournit une vue d’ensemble pour la réplication de site VMM secondaire tooa ordinateurs virtuels Hyper-V à l’aide de hello portail Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="792ee-103">Réplication d’ordinateurs virtuels Hyper-V dans le site VMM secondaire VMM clouds tooa</span><span class="sxs-lookup"><span data-stu-id="792ee-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="792ee-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="792ee-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="792ee-105">Portail classique</span><span class="sxs-lookup"><span data-stu-id="792ee-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="792ee-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="792ee-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="792ee-107">Cet article fournit une vue d’ensemble de hello étapes requises tooreplicate local Hyper-V virtual machines virtuelles gérées dans des clouds System Center Virtual Machine Manager (VMM), emplacement de VMM secondaire tooa, à l’aide de [Azure Site Recovery](site-recovery-overview.md)Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="792ee-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="792ee-108">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="792ee-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="792ee-109">Étape 1 : Passez en revue l’architecture du scénario de hello</span><span class="sxs-lookup"><span data-stu-id="792ee-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="792ee-110">Avant de commencer le déploiement, examen de l’architecture du scénario hello et assurez-vous que vous comprenez tous les composants de hello, vous devez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="792ee-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="792ee-111">Accédez trop[étape 1 : examen de l’architecture de hello](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="792ee-112">Étape 2 : Vérifier les conditions préalables et les limitations</span><span class="sxs-lookup"><span data-stu-id="792ee-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="792ee-113">Assurez-vous que vous comprenez les limitations et les conditions préalables au déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="792ee-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="792ee-114">**Conditions préalables Azure**: vous avez besoin d’un abonnement Microsoft Azure et Azure Recovery Services coffre, tooorchestrate et gérer la réplication.</span><span class="sxs-lookup"><span data-stu-id="792ee-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="792ee-115">**Serveurs VMM et hôtes Hyper-V locaux** : assurez-vous que les serveurs VMM et les hôtes Hyper-V sont conformes et préparés pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="792ee-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="792ee-116">Accédez trop[étape 2 : vérifier les conditions préalables et limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="792ee-117">Étape 3 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="792ee-117">Step 3: Plan networking</span></span>

<span data-ttu-id="792ee-118">Vous devez toodo certains tooensure que vous pouvez configurer le mappage réseau entre les réseaux de VM de VMM lorsque vous déployez le scénario de hello de planification d’un réseau.</span><span class="sxs-lookup"><span data-stu-id="792ee-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="792ee-119">Accédez trop[étape 3 : planifier la mise en réseau](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="792ee-120">Étape 4 : Préparer VMM et Hyper-V</span><span class="sxs-lookup"><span data-stu-id="792ee-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="792ee-121">Préparer les serveurs VMM hello et hôtes Hyper-V pour le déploiement de la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="792ee-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="792ee-122">Accédez trop[étape 4 : préparer les serveurs locaux](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="792ee-123">Étape 5 : Configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="792ee-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="792ee-124">Configurez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="792ee-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="792ee-125">coffre de Hello contient les paramètres de configuration et orchestre la réplication.</span><span class="sxs-lookup"><span data-stu-id="792ee-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="792ee-126">[Étape 5 : Configurer un coffre](vmm-to-vmm-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="792ee-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="792ee-127">Étape 6 : Configurer les paramètres de la source et de la cible</span><span class="sxs-lookup"><span data-stu-id="792ee-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="792ee-128">Configurez les emplacements de VMM réplication source et cible des hello.</span><span class="sxs-lookup"><span data-stu-id="792ee-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="792ee-129">Ajouter hello VMM serveurs toohello coffre-fort et télécharger les fichiers d’installation hello pour les composants de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="792ee-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="792ee-130">Exécutez le programme d’installation du fournisseur Azure Site Recovery sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="792ee-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="792ee-131">Le programme d’installation installe hello fournisseur sur le serveur VMM de hello et les enregistre sur le serveur hello dans le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="792ee-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="792ee-132">Vous installez hello Microsoft Recovery Services agent sur chaque hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="792ee-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="792ee-133">Accédez trop[étape 6 : configurer les paramètres source et cible hello](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="792ee-134">Étape 7 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="792ee-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="792ee-135">Mappez les réseaux VMM VM dans les emplacements source et cible hello.</span><span class="sxs-lookup"><span data-stu-id="792ee-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="792ee-136">Après le basculement, les machines virtuelles sont créées dans le réseau cible de hello ce réseau d’ordinateurs virtuels maps toohello source dans le hello source d’ordinateur virtuel Hyper-V se trouve.</span><span class="sxs-lookup"><span data-stu-id="792ee-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="792ee-137">Accédez trop[étape 7 : configurer le mappage réseau](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="792ee-138">Étape 8 : Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="792ee-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="792ee-139">Spécifiez comment les machines virtuelles seront répliquées entre les emplacements VMM.</span><span class="sxs-lookup"><span data-stu-id="792ee-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="792ee-140">Accédez trop[étape 8 : définir une stratégie de réplication](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="792ee-141">Étape 9 : Activer la réplication des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="792ee-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="792ee-142">Sélectionnez hello machines virtuelles tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="792ee-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="792ee-143">Activation d’une machine virtuelle pour le site secondaire toohello de la réplication initiale hello réplication déclencheurs, suivie de la réplication delta en cours.</span><span class="sxs-lookup"><span data-stu-id="792ee-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="792ee-144">Accédez trop[étape 9 : activer la réplication](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="792ee-145">Étape 10 : Exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="792ee-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="792ee-146">Exécutez un toomake de basculement de test que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="792ee-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="792ee-147">Accédez trop[étape 10 : exécuter un test de basculement](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="792ee-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
