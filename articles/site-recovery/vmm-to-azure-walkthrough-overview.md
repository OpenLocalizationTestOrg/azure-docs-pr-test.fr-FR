---
title: aaaReplicate des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure avec Azure Site Recovery | Documents Microsoft
description: "Fournit une vue d’ensemble pour répliquer des ordinateurs virtuels Hyper-V dans VMM tooAzure de nuages à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="499e5-103">Répliquer les machines virtuelles Hyper-V dans VMM tooAzure de nuages à l’aide de la récupération de Site Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="499e5-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="499e5-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="499e5-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="499e5-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="499e5-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="499e5-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="499e5-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="499e5-107">PowerShell Classic</span><span class="sxs-lookup"><span data-stu-id="499e5-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="499e5-108">Cet article fournit une vue d’ensemble de tooreplicate requis des étapes de hello local Hyper-V virtual machines virtuelles gérées dans System Center Virtual Machine Manager (VMM) clouds tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service dans Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="499e5-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="499e5-109">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="499e5-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="499e5-110">Étape 1 : Passez en revue l’architecture du scénario de hello</span><span class="sxs-lookup"><span data-stu-id="499e5-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="499e5-111">Avant de commencer le déploiement, examen de l’architecture du scénario hello et assurez-vous que vous comprenez tous les composants de hello, vous devez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="499e5-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="499e5-112">Accédez trop[étape 1 : examen de l’architecture de hello](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="499e5-113">Étape 2 : Vérifier les conditions préalables et les limitations</span><span class="sxs-lookup"><span data-stu-id="499e5-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="499e5-114">Assurez-vous que vous comprenez les limitations et les conditions préalables au déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="499e5-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="499e5-115">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="499e5-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="499e5-116">**Serveurs VMM et hôtes Hyper-V locaux** : assurez-vous que les serveurs VMM et les hôtes Hyper-V sont conformes et préparés pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="499e5-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="499e5-117">**Répliquer les machines virtuelles**: Vérifiez que vous voulez tooreplicate de machines virtuelles sont conformes aux exigences d’Azure.</span><span class="sxs-lookup"><span data-stu-id="499e5-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="499e5-118">Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="499e5-119">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="499e5-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="499e5-120">Si vous effectuez un déploiement complet, vous devez toofigure à quelles ressources de réplication que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="499e5-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="499e5-121">Il existe deux de toohelp disponibles des outils pour cela.</span><span class="sxs-lookup"><span data-stu-id="499e5-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="499e5-122">Si vous effectuez une rapide configurer tootest hello environnement, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="499e5-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="499e5-123">Accédez trop[étape 3 : planifier la capacité](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="499e5-124">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="499e5-124">Step 4: Plan networking</span></span>

<span data-ttu-id="499e5-125">Vous devez toodo certains tooensure que vous pouvez configurer le mappage réseau lorsque vous déployez le scénario de hello, de planification d’un réseau que les machines virtuelles Azure sera tooAzure connecté les réseaux virtuels après le basculement se produit et qu’ils sont attribués IP approprié répondant.</span><span class="sxs-lookup"><span data-stu-id="499e5-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="499e5-126">Accédez trop[étape 4 : planifier la mise en réseau](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="499e5-127">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="499e5-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="499e5-128">Configurez un compte Azure, des réseaux et du stockage.</span><span class="sxs-lookup"><span data-stu-id="499e5-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="499e5-129">Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="499e5-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="499e5-130">Accédez trop[étape 5 : préparer le Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="499e5-131">Étape 6 : Préparer VMM et Hyper-V</span><span class="sxs-lookup"><span data-stu-id="499e5-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="499e5-132">Préparer les serveurs VMM hello local et les hôtes Hyper-V pour le déploiement de la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="499e5-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="499e5-133">Accédez trop[étape 6 : préparer les serveurs locaux](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="499e5-134">Étape 7 : configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="499e5-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="499e5-135">Configurez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="499e5-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="499e5-136">coffre de Hello contient les paramètres de configuration et orchestre la réplication.</span><span class="sxs-lookup"><span data-stu-id="499e5-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="499e5-137">Étape 7 : Configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="499e5-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="499e5-138">Étape 8 : configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="499e5-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="499e5-139">Configurez les emplacements de hello source et cible de réplication.</span><span class="sxs-lookup"><span data-stu-id="499e5-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="499e5-140">Ajouter hello VMM serveur toohello dans l’archivage et télécharger des fichiers d’installation hello pour les composants de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="499e5-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="499e5-141">Exécutez le programme d’installation du fournisseur Azure Site Recovery sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="499e5-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="499e5-142">Le programme d’installation installe hello fournisseur sur le serveur VMM de hello et les enregistre sur le serveur hello dans le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="499e5-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="499e5-143">Vous installez hello Microsoft Recovery Services agent sur chaque hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="499e5-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="499e5-144">Accédez trop[étape 8 : configurer les paramètres source et cible](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="499e5-145">Étape 9 : Configurer le mappage réseau</span><span class="sxs-lookup"><span data-stu-id="499e5-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="499e5-146">Mappage des locaux des réseaux virtuels VMM VM réseaux tooAzure.</span><span class="sxs-lookup"><span data-stu-id="499e5-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="499e5-147">Après le basculement, les machines virtuelles Azure sont créés dans hello réseau Azure mappé toohello réseau d’ordinateurs virtuels en local dans le hello Hyper-V source se trouve.</span><span class="sxs-lookup"><span data-stu-id="499e5-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="499e5-148">Accédez trop[étape 9 : configurer le mappage réseau](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="499e5-149">Étape 10 : Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="499e5-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="499e5-150">Spécifiez comment les machines virtuelles de local sera répliquée tooAzure.</span><span class="sxs-lookup"><span data-stu-id="499e5-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="499e5-151">Accédez trop[étape 10 : définir une stratégie de réplication](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="499e5-152">Étape 11 : Activer la réplication des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="499e5-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="499e5-153">Sélectionnez hello machines virtuelles tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="499e5-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="499e5-154">Activation d’une machine virtuelle pour la réplication déclencheurs hello la réplication initiale tooAzure, suivie de la réplication delta en cours.</span><span class="sxs-lookup"><span data-stu-id="499e5-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="499e5-155">Accédez trop[étape 11 : activer la réplication](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="499e5-156">Étape 12 : exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="499e5-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="499e5-157">Exécutez un toomake de basculement de test que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="499e5-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="499e5-158">Accédez trop[étape 12 : exécuter un test de basculement](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="499e5-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


