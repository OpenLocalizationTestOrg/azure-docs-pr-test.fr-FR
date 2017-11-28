---
title: "tooAzure d’ordinateurs virtuels Hyper-V aaaReplicate avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment la réplication tooorchestrate, le basculement et récupération de local Hyper-V VM tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="bcc6a-103">Répliquer tooAzure d’ordinateurs virtuels (sans VMM) Hyper-V</span><span class="sxs-lookup"><span data-stu-id="bcc6a-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcc6a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="bcc6a-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="bcc6a-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="bcc6a-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="bcc6a-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcc6a-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="bcc6a-107">Cet article fournit une vue d’ensemble de hello étapes requises tooreplicate local Hyper-V virtual machines tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="bcc6a-108">Dans ce déploiement, les machines virtuelles Hyper-V ne sont pas gérées par System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="bcc6a-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="bcc6a-109">Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bcc6a-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="bcc6a-110">Étape 1 : vérifier l’architecture et les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="bcc6a-111">Avant de commencer le déploiement, consultez architecture du scénario hello et assurez-vous que vous comprenez tous les composants hello vous devez toodeploy</span><span class="sxs-lookup"><span data-stu-id="bcc6a-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="bcc6a-112">Accédez trop[étape 1 : examen de l’architecture de hello](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="bcc6a-113">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="bcc6a-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="bcc6a-114">Vérifiez que vous disposez des prérequis de hello en place pour chaque composant de déploiement :</span><span class="sxs-lookup"><span data-stu-id="bcc6a-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="bcc6a-115">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="bcc6a-116">**Conditions préalables pour les machines virtuelles Hyper-V locales** : assurez-vous que les hôtes Hyper-V sont préparés pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="bcc6a-117">**Répliquer les machines virtuelles**: machines virtuelles que vous souhaitez tooreplicate devez toocomply aux exigences d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="bcc6a-118">Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="bcc6a-119">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="bcc6a-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="bcc6a-120">Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="bcc6a-121">Il existe deux de toohelp disponibles des outils pour cela.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="bcc6a-122">Accédez tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-122">Go tooStep 2.</span></span> <span data-ttu-id="bcc6a-123">Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="bcc6a-124">Accédez trop[étape 3 : planifier la capacité](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="bcc6a-125">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="bcc6a-125">Step 4: Plan networking</span></span>

<span data-ttu-id="bcc6a-126">Vous devez toodo certains planification tooensure que les machines virtuelles Azure sont toonetworks connectés après que le basculement se produit, et que qu’ils ont hello droite des adresses IP d’un réseau.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="bcc6a-127">Accédez trop[étape 4 : planifier la mise en réseau](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="bcc6a-128">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="bcc6a-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="bcc6a-129">Configurez les réseaux et le stockage Azure avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="bcc6a-130">Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="bcc6a-131">Accédez trop[étape 5 : préparer le Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="bcc6a-132">Étape 6 : préparer Hyper-V</span><span class="sxs-lookup"><span data-stu-id="bcc6a-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="bcc6a-133">Assurez-vous que les serveurs Hyper-V remplissent les exigences liées au déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="bcc6a-134">Accédez trop[étape 6 : préparation de Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="bcc6a-135">Étape 7 : configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="bcc6a-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="bcc6a-136">Vous devez tooset d’un tooorchestrate du coffre Recovery Services et gérez la réplication.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="bcc6a-137">Lorsque vous configurez le coffre de hello, vous spécifiez ce que vous voulez tooreplicate, et où vous souhaitez que tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="bcc6a-138">Accédez trop[étape 7 : créer un coffre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="bcc6a-139">Étape 8 : configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="bcc6a-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="bcc6a-140">Configurer la source de hello et la cible qui est utilisée pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="bcc6a-141">Configuration des paramètres de la source comprend l’ajout d’Hyper-V héberge tooa Hyper-V site, l’installation hello fournisseur Site Recovery et l’agent Recovery Services sur chaque ordinateur hôte Hyper-V et l’enregistrement de site de hello Bonjour de coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="bcc6a-142">Accédez trop[étape 8 : configurer hello source et cible](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="bcc6a-143">Étape 9 : configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="bcc6a-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="bcc6a-144">Vous définissez des paramètres de réplication de stratégie toospecify pour les ordinateurs virtuels Hyper-V dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="bcc6a-145">Accédez trop[étape 9 : configurer une stratégie de réplication](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="bcc6a-146">Étape 10 : Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="bcc6a-146">Step 10: Enable replication</span></span>

<span data-ttu-id="bcc6a-147">Après avoir configuré une stratégie de réplication en place, après l’activation, la réplication initiale de hello machine virtuelle se produit.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="bcc6a-148">Accédez trop[étape 10 : activer la réplication](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="bcc6a-149">Étape 11 : Exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="bcc6a-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="bcc6a-150">Une fois la réplication initiale se termine, et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="bcc6a-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="bcc6a-151">Accédez trop[étape 11 : exécuter un test de basculement](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="bcc6a-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
