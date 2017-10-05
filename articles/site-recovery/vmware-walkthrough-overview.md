---
title: "Répliquer des machines virtuelles VMware sur Azure à l’aide de Azure Site Recovery | Microsoft Docs"
description: "Fournit une vue d’ensemble des étapes à suivre pour répliquer des charges de travail exécutées sur des machines virtuelles VMware sur Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: db6f5f95929503e82a529dba26b56af1edb0767f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-vms-to-azure-with-site-recovery"></a><span data-ttu-id="8bb0b-103">Répliquer des machines virtuelles VMware sur Azure à l’aide de Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8bb0b-103">Replicate VMware VMs to Azure with Site Recovery</span></span>

<span data-ttu-id="8bb0b-104">Cet article fournit une vue d’ensemble des étapes à suivre pour répliquer des machines virtuelles VMware locales sur Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-104">This article provides an overview of the steps required to replicate on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


![Processus de déploiement](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="8bb0b-106">**Figure 1 : Résumé du processus de déploiement**</span><span class="sxs-lookup"><span data-stu-id="8bb0b-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="8bb0b-107">Étape 1 : vérifier l’architecture et les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="8bb0b-108">Avant de commencer le déploiement, vérifiez l’architecture du scénario et prenez connaissance de tous les composants que vous devez déployer.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-108">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="8bb0b-109">Accédez à [Étape 1 : examen de l’architecture](vmware-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="8bb0b-109">Go to [Step 1: Review the architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="8bb0b-110">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8bb0b-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="8bb0b-111">Assurez-vous que les conditions préalables sont remplies pour chaque composant du déploiement :</span><span class="sxs-lookup"><span data-stu-id="8bb0b-111">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="8bb0b-112">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="8bb0b-113">**Composants Site Recovery locaux** : vous avez besoin d’une machine exécutant les composants Site Recovery locaux.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="8bb0b-114">**Conditions préalables de VMware locales** : vous devez configurer les comptes afin que Site Recovery puisse accéder aux serveurs VMware et aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-114">**On-premises VMware prerequisites**: You need to set up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="8bb0b-115">**Machines virtuelles répliquées** : Les machines virtuelles que vous souhaitez répliquer doivent se conformer aux exigences d’Azure, et les composants du service Mobilité doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-115">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements, and have the Mobility service component installed.</span></span>

<span data-ttu-id="8bb0b-116">Aller à [Étape 2 : vérifier les conditions préalables et les limitations](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-116">Go to [Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="8bb0b-117">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="8bb0b-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="8bb0b-118">Si vous effectuez un déploiement complet, vous devez déterminer les ressources de réplication dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-118">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="8bb0b-119">Pour ce faire, vous disposez de plusieurs outils.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-119">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="8bb0b-120">Accédez à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-120">Go to Step 2.</span></span> <span data-ttu-id="8bb0b-121">Si vous souhaitez réaliser une configuration rapide pour tester l’environnement, vous pouvez passer cette étape.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-121">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="8bb0b-122">Accédez à [Étape 3 : planifier la capacité](vmware-walkthrough-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="8bb0b-122">Go to [Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="8bb0b-123">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="8bb0b-123">Step 4: Plan networking</span></span>

<span data-ttu-id="8bb0b-124">Vous devez établir un plan du réseau pour vous assurer que les machines virtuelles Azure sont connectées aux réseaux après le basculement et qu’elles disposent des bonnes adresses IP.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-124">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="8bb0b-125">Aller à [Étape 4 : Planifier la mise en réseau](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-125">Go to [Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="8bb0b-126">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="8bb0b-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="8bb0b-127">Configurez les réseaux et le stockage Azure avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="8bb0b-128">Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="8bb0b-129">Aller à [Étape 5 : Préparer Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-129">Go to [Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="8bb0b-130">Étape 6 : préparer VMware</span><span class="sxs-lookup"><span data-stu-id="8bb0b-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="8bb0b-131">Vous devez configurer des comptes que Site Recovery utilisera pour :</span><span class="sxs-lookup"><span data-stu-id="8bb0b-131">You need to set up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="8bb0b-132">Accéder aux serveurs de virtualisation VMware pour détecter automatiquement les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-132">Access VMware virtualization servers to automatically detect VMs.</span></span>
- <span data-ttu-id="8bb0b-133">Accéder aux machines virtuelles pour installer le service Mobilité.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-133">Access VMs to install the Mobility service.</span></span> <span data-ttu-id="8bb0b-134">Vous devez installer l’agent du service Mobilité sur chaque machine virtuelle que vous souhaitez répliquer pour activer la réplication.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-134">Each VM you want to replicate must have the Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="8bb0b-135">Aller à [Étape 6 : préparer VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-135">Go to [Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="8bb0b-136">Étape 7 : configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="8bb0b-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="8bb0b-137">Vous devez configurer un coffre Recovery Services pour orchestrer et gérer la réplication.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-137">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="8bb0b-138">Lorsque vous configurez le coffre, vous spécifiez ce que vous voulez répliquer, et où vous souhaitez le répliquer.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-138">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="8bb0b-139">Aller à [Étape 7 : Configurer un coffre](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-139">Go to [Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="8bb0b-140">Étape 8 : configurer les paramètres source et cible</span><span class="sxs-lookup"><span data-stu-id="8bb0b-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="8bb0b-141">Configurez la source et la cible utilisées pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-141">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="8bb0b-142">Pour configurer les paramètres source, vous devez exécuter une installation unifiée afin d’installer les composants Site Recovery locaux.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-142">Setting up source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="8bb0b-143">Aller à [Étape 8 : configurer la source et la cible](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-143">Go to [Step 8: Set up the source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="8bb0b-144">Étape 9 : configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="8bb0b-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="8bb0b-145">Vous devez configurer une stratégie afin de spécifier les paramètres de réplication des machines virtuelles VMware dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-145">You set up a policy to specify replication settings for VMware VMs in the vault.</span></span>

<span data-ttu-id="8bb0b-146">Aller à [Étape 9 : configurer une stratégie de réplication](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-146">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="8bb0b-147">Étape 10 : installer le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="8bb0b-147">Step 10: Install the Mobility service</span></span>

<span data-ttu-id="8bb0b-148">Le service Mobility doit être installé sur chaque machine que vous souhaitez répliquer.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-148">The Mobility service must be installed on each VM you want to replicate.</span></span> <span data-ttu-id="8bb0b-149">Il existe plusieurs méthodes de configuration du service à l’aide d’une installation push ou pull.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-149">There are a few ways to set up the service with push or pull installation.</span></span>

<span data-ttu-id="8bb0b-150">Aller à [Étape 10 : installer le service Mobilité](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-150">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="8bb0b-151">Étape 11 : activer la réplication</span><span class="sxs-lookup"><span data-stu-id="8bb0b-151">Step 11: Enable replication</span></span>

<span data-ttu-id="8bb0b-152">Vous pouvez activer la réplication une fois que le service Mobilité est en cours d’exécution sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-152">After the Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="8bb0b-153">La réplication initiale de la machine virtuelle se produira après l’activation.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-153">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="8bb0b-154">Aller à [Étape 11 : activer la réplication](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-154">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="8bb0b-155">Étape 12 : exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="8bb0b-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="8bb0b-156">Lorsque la réplication initiale est terminée et la réplication delta est en cours d’exécution, vous pouvez exécuter un test de basculement pour vous assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="8bb0b-156">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="8bb0b-157">Aller à [Étape 12 : exécuter un test de basculement](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8bb0b-157">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
