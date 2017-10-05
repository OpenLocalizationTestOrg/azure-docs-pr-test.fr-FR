---
title: "Répliquer des machines virtuelles Hyper-V vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Explique comment orchestrer la réplication, le basculement et la récupération des machines virtuelles Hyper-V locales dans Azure"
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
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="6253f-103">Répliquer des machines virtuelles Hyper-V (sans VMM) vers Azure</span><span class="sxs-lookup"><span data-stu-id="6253f-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6253f-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6253f-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="6253f-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="6253f-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="6253f-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6253f-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="6253f-107">Cet article offre une vue d’ensemble des étapes à suivre pour répliquer des machines virtuelles Hyper-V locales vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6253f-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="6253f-108">Dans ce déploiement, les machines virtuelles Hyper-V ne sont pas gérées par System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="6253f-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="6253f-109">Après avoir lu cet article, envoyez vos commentaires en bas ou posez vos questions techniques sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6253f-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="6253f-110">Étape 1 : vérifier l’architecture et les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="6253f-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="6253f-111">Avant de commencer le déploiement, vérifiez l’architecture du scénario et prenez connaissance de tous les composants que vous devez déployer.</span><span class="sxs-lookup"><span data-stu-id="6253f-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="6253f-112">Accédez à [Étape 1 : examen de l’architecture](hyper-v-site-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="6253f-113">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="6253f-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="6253f-114">Assurez-vous que les conditions préalables sont remplies pour chaque composant du déploiement :</span><span class="sxs-lookup"><span data-stu-id="6253f-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="6253f-115">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, de réseaux Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="6253f-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="6253f-116">**Conditions préalables pour les machines virtuelles Hyper-V locales** : assurez-vous que les hôtes Hyper-V sont préparés pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6253f-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="6253f-117">**Machines virtuelles répliquées** : les machines virtuelles à répliquer doivent se conformer aux conditions requises pour Azure.</span><span class="sxs-lookup"><span data-stu-id="6253f-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="6253f-118">Accédez à [Étape 2 : vérifier les conditions préalables et les limitations](hyper-v-site-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="6253f-119">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="6253f-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="6253f-120">Si vous effectuez un déploiement complet, vous devez déterminer les ressources de réplication dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="6253f-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="6253f-121">Pour ce faire, vous disposez de plusieurs outils.</span><span class="sxs-lookup"><span data-stu-id="6253f-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="6253f-122">Accédez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="6253f-122">Go to Step 2.</span></span> <span data-ttu-id="6253f-123">Si vous souhaitez réaliser une configuration rapide pour tester l’environnement, vous pouvez passer cette étape.</span><span class="sxs-lookup"><span data-stu-id="6253f-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="6253f-124">Accédez à [Étape 3 : planifier la capacité](hyper-v-site-walkthrough-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="6253f-125">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="6253f-125">Step 4: Plan networking</span></span>

<span data-ttu-id="6253f-126">Vous devez établir un plan du réseau pour vous assurer que les machines virtuelles Azure sont connectées aux réseaux après le basculement et qu’elles disposent des bonnes adresses IP.</span><span class="sxs-lookup"><span data-stu-id="6253f-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="6253f-127">Aller à [Étape 4 : Planifier la mise en réseau](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="6253f-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="6253f-128">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="6253f-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="6253f-129">Configurez les réseaux et le stockage Azure avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="6253f-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="6253f-130">Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="6253f-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="6253f-131">Accédez à [Étape 5 : préparer Azure](hyper-v-site-walkthrough-prepare-azure.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="6253f-132">Étape 6 : préparer Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6253f-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="6253f-133">Assurez-vous que les serveurs Hyper-V remplissent les exigences liées au déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6253f-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="6253f-134">Accédez à [Étape 6 : préparer Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="6253f-135">Étape 7 : configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="6253f-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="6253f-136">Vous devez configurer un coffre Recovery Services pour orchestrer et gérer la réplication.</span><span class="sxs-lookup"><span data-stu-id="6253f-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="6253f-137">Lors de la configuration du coffre, vous spécifiez les éléments à répliquer et leur destination de réplication.</span><span class="sxs-lookup"><span data-stu-id="6253f-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="6253f-138">Accédez à [Étape 7 : créer un coffre](hyper-v-site-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="6253f-139">Étape 8 : configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="6253f-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="6253f-140">Configurez la source et la cible utilisées pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="6253f-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="6253f-141">La configuration des paramètres de source comprend l’ajout d’hôtes Hyper-V à un site Hyper-V, l’installation du fournisseur Site Recovery et de l’agent Recovery Services sur chaque hôte Hyper-V, et l’inscription du site dans le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="6253f-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="6253f-142">Accédez à [Étape 8 : configurer la source et la cible](hyper-v-site-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="6253f-143">Étape 9 : configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="6253f-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="6253f-144">Vous devez configurer une stratégie afin de spécifier les paramètres de réplication des machines virtuelles Hyper-V dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="6253f-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="6253f-145">Accédez à [Étape 9 : configurer une stratégie de réplication](hyper-v-site-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="6253f-146">Étape 10 : activer la réplication</span><span class="sxs-lookup"><span data-stu-id="6253f-146">Step 10: Enable replication</span></span>

<span data-ttu-id="6253f-147">Une fois que vous avez une stratégie de réplication en place, la réplication initiale de la machine virtuelle se produira après l’activation.</span><span class="sxs-lookup"><span data-stu-id="6253f-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="6253f-148">Accédez à [Étape 10 : activer la réplication](hyper-v-site-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="6253f-149">Étape 11 : exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="6253f-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="6253f-150">Lorsque la réplication initiale est terminée et la réplication delta est en cours d’exécution, vous pouvez exécuter un test de basculement pour vous assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="6253f-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="6253f-151">Accédez à [Étape 11 : exécuter un test de basculement](hyper-v-site-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="6253f-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
