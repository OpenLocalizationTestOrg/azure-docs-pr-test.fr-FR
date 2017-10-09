---
title: aaaReplicate physique local tooAzure serveurs avec Azure Site Recovery | Documents Microsoft
description: "Fournit une vue d’ensemble des étapes de hello pour répliquer les charges de travail en cours d’exécution sur tooAzure de serveurs physiques locaux Windows/Linux avec hello service Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="542d4-103">Répliquer tooAzure serveurs physiques avec Site Recovery</span><span class="sxs-lookup"><span data-stu-id="542d4-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="542d4-104">Cet article fournit une vue d’ensemble de hello étapes requises tooreplicate local Windows/Linux serveurs physiques tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="542d4-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="542d4-105">Étape 1 : vérifier l’architecture et les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="542d4-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="542d4-106">Avant de commencer le déploiement, consultez architecture du scénario hello et assurez-vous que vous comprenez tous les composants hello vous devez tooset le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="542d4-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="542d4-107">Accédez trop[étape 1 : examen de l’architecture de hello](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="542d4-108">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="542d4-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="542d4-109">Vérifiez que vous disposez des prérequis de hello en place pour chaque composant de déploiement :</span><span class="sxs-lookup"><span data-stu-id="542d4-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="542d4-110">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="542d4-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="542d4-111">**Composants Site Recovery locaux** : vous avez besoin d’une machine exécutant les composants Site Recovery locaux.</span><span class="sxs-lookup"><span data-stu-id="542d4-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="542d4-112">**Machines répliquées**: serveurs tooreplicate doivent toocomply avec locaux et les conditions requises pour Azure.</span><span class="sxs-lookup"><span data-stu-id="542d4-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="542d4-113">Accédez trop[étape 2 : passez en revue les conditions préalables et restrictions](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="542d4-114">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="542d4-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="542d4-115">Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="542d4-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="542d4-116">Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="542d4-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="542d4-117">Accédez trop[étape 3 : planifier la capacité](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="542d4-118">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="542d4-118">Step 4: Plan networking</span></span>

<span data-ttu-id="542d4-119">Vous devez toodo certains planification tooensure que les machines virtuelles Azure sont toonetworks connectés après que le basculement se produit, et que qu’ils ont hello droite des adresses IP d’un réseau.</span><span class="sxs-lookup"><span data-stu-id="542d4-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="542d4-120">Accédez trop[étape 4 : planifier la mise en réseau](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="542d4-121">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="542d4-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="542d4-122">Configurez les réseaux et le stockage Azure avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="542d4-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="542d4-123">Accédez trop[étape 5 : préparer le Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="542d4-124">Étape 6 : Configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="542d4-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="542d4-125">Vous configurez un tooorchestrate du coffre Recovery Services et gérez la réplication.</span><span class="sxs-lookup"><span data-stu-id="542d4-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="542d4-126">Lorsque vous configurez le coffre de hello, vous spécifiez ce que vous voulez tooreplicate, et où vous souhaitez que tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="542d4-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="542d4-127">Accédez trop[étape 6 : configurer un coffre](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="542d4-128">Étape 7 : Configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="542d4-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="542d4-129">Configurer les paramètres de source de hello et cibles de site (Azure).</span><span class="sxs-lookup"><span data-stu-id="542d4-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="542d4-130">Paramètres de la source inclut exécutant le programme d’installation unifiée tooinstall composants de Site Recovery hello locaux.</span><span class="sxs-lookup"><span data-stu-id="542d4-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="542d4-131">Accédez trop[étape 7 : configurer hello source et cible](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="542d4-132">Étape 8 : Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="542d4-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="542d4-133">Vous configurez une stratégie toospecify physiques doivent répliquer les serveurs.</span><span class="sxs-lookup"><span data-stu-id="542d4-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="542d4-134">Accédez trop[étape 8 : définir une stratégie de réplication](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="542d4-135">Étape 9 : Installer le service de mobilité hello</span><span class="sxs-lookup"><span data-stu-id="542d4-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="542d4-136">Hello service mobilité doit être installé sur chaque serveur, vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="542d4-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="542d4-137">Il existe quelques façons tooset, configuration du service hello, avec l’installation push ou pull.</span><span class="sxs-lookup"><span data-stu-id="542d4-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="542d4-138">Accédez trop[étape 9 : installer le service de mobilité hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="542d4-139">Étape 10 : Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="542d4-139">Step 10: Enable replication</span></span>

<span data-ttu-id="542d4-140">Une fois hello service mobilité est en cours d’exécution sur un serveur, vous pouvez activer la réplication.</span><span class="sxs-lookup"><span data-stu-id="542d4-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="542d4-141">Après l’activation, la réplication initiale de hello machine virtuelle se produit.</span><span class="sxs-lookup"><span data-stu-id="542d4-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="542d4-142">Accédez trop[étape 10 : activer la réplication](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="542d4-143">Étape 11 : Exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="542d4-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="542d4-144">Une fois la réplication initiale est terminée et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="542d4-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="542d4-145">Accédez trop[étape 11 : exécuter un test de basculement](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="542d4-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

