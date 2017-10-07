---
title: "tooAzure d’ordinateurs virtuels VMware aaaReplicate avec Azure Site Recovery | Documents Microsoft"
description: "Fournit une vue d’ensemble des étapes de hello pour répliquer les charges de travail en cours d’exécution sur les ordinateurs virtuels VMware tooAzure"
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
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="8b4ab-103">Répliquer tooAzure les ordinateurs virtuels VMware avec Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8b4ab-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="8b4ab-104">Cet article fournit une vue d’ensemble de hello étapes tooreplicate requis local VMware virtual machines tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Processus de déploiement](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="8b4ab-106">**Figure 1 : Résumé du processus de déploiement**</span><span class="sxs-lookup"><span data-stu-id="8b4ab-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="8b4ab-107">Étape 1 : vérifier l’architecture et les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="8b4ab-108">Avant de commencer le déploiement, consultez architecture du scénario hello et assurez-vous que vous comprenez tous les composants hello vous devez toodeploy</span><span class="sxs-lookup"><span data-stu-id="8b4ab-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="8b4ab-109">Accédez trop[étape 1 : examen de l’architecture de hello](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="8b4ab-110">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8b4ab-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="8b4ab-111">Vérifiez que vous disposez des prérequis de hello en place pour chaque composant de déploiement :</span><span class="sxs-lookup"><span data-stu-id="8b4ab-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="8b4ab-112">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="8b4ab-113">**Composants Site Recovery locaux** : vous avez besoin d’une machine exécutant les composants Site Recovery locaux.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="8b4ab-114">**Conditions préalables de VMware local**: vous devez tooset des comptes afin que la récupération de Site peut accéder aux serveurs VMware et les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="8b4ab-115">**Répliquer les machines virtuelles**: machines virtuelles vous toocomply besoin de tooreplicate aux exigences d’Azure et souhaitez composant du service mobilité hello installé.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="8b4ab-116">Accédez trop[étape 2 : passez en revue les conditions préalables et restrictions](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="8b4ab-117">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="8b4ab-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="8b4ab-118">Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="8b4ab-119">Il existe deux de toohelp disponibles des outils pour cela.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="8b4ab-120">Accédez tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-120">Go tooStep 2.</span></span> <span data-ttu-id="8b4ab-121">Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="8b4ab-122">Accédez trop[étape 3 : planifier la capacité](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="8b4ab-123">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="8b4ab-123">Step 4: Plan networking</span></span>

<span data-ttu-id="8b4ab-124">Vous devez toodo certains planification tooensure que les machines virtuelles Azure sont toonetworks connectés après que le basculement se produit, et que qu’ils ont hello droite des adresses IP d’un réseau.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="8b4ab-125">Accédez trop[étape 4 : planifier la mise en réseau](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="8b4ab-126">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="8b4ab-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="8b4ab-127">Configurez les réseaux et le stockage Azure avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="8b4ab-128">Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="8b4ab-129">Accédez trop[étape 5 : préparer le Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="8b4ab-130">Étape 6 : préparer VMware</span><span class="sxs-lookup"><span data-stu-id="8b4ab-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="8b4ab-131">Vous devez tooset des comptes de la récupération de Site utilisera pour :</span><span class="sxs-lookup"><span data-stu-id="8b4ab-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="8b4ab-132">Tooautomatically de serveurs de virtualisation de VMware accès détecter les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="8b4ab-133">Accéder au service de mobilité des machines virtuelles tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="8b4ab-134">Chaque ordinateur virtuel que vous souhaitez tooreplicate agent doit être hello mobilité service installé avant que vous pouvez activer la réplication.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="8b4ab-135">Accédez trop[étape 6 : préparation de VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="8b4ab-136">Étape 7 : configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="8b4ab-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="8b4ab-137">Vous devez tooset d’un tooorchestrate du coffre Recovery Services et gérez la réplication.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="8b4ab-138">Lorsque vous configurez le coffre de hello, vous spécifiez ce que vous voulez tooreplicate, et où vous souhaitez que tooreplicate à.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="8b4ab-139">Accédez trop[étape 7 : configurer un coffre](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="8b4ab-140">Étape 8 : configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="8b4ab-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="8b4ab-141">Configurer la source de hello et la cible qui est utilisée pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="8b4ab-142">Configuration des paramètres de la source inclut exécutant le programme d’installation unifiée tooinstall composants de Site Recovery hello locaux.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="8b4ab-143">Accédez trop[étape 8 : configurer hello source et cible](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="8b4ab-144">Étape 9 : configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="8b4ab-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="8b4ab-145">Vous définissez des paramètres de réplication toospecify de stratégie pour les ordinateurs virtuels VMware dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="8b4ab-146">Accédez trop[étape 9 : configurer une stratégie de réplication](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="8b4ab-147">Étape 10 : Installer le service de mobilité hello</span><span class="sxs-lookup"><span data-stu-id="8b4ab-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="8b4ab-148">Hello service mobilité doit être installé sur chaque machine virtuelle, vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="8b4ab-149">Il existe quelques façons tooset, configuration du service d’installation push ou pull hello.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="8b4ab-150">Accédez trop[étape 10 : installer le service de mobilité hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="8b4ab-151">Étape 11 : activer la réplication</span><span class="sxs-lookup"><span data-stu-id="8b4ab-151">Step 11: Enable replication</span></span>

<span data-ttu-id="8b4ab-152">Vous pouvez activer la réplication après que hello service mobilité est en cours d’exécution sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="8b4ab-153">Après l’activation, la réplication initiale de hello machine virtuelle se produit.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="8b4ab-154">Accédez trop[étape 11 : activer la réplication](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="8b4ab-155">Étape 12 : exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="8b4ab-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="8b4ab-156">Une fois la réplication initiale se termine, et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="8b4ab-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="8b4ab-157">Accédez trop[étape 12 : exécuter un test de basculement](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8b4ab-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
