---
title: "Réplication de machines virtuelles Hyper-V dans les clouds VMM vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Fournit une vue d’ensemble de la réplication de machines virtuelles Hyper-V dans les clouds VMM vers Azure à l’aide du service Azure Site Recovery"
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
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="663ea-103">Répliquer vers Azure des machines virtuelles Hyper-V hébergées dans des clouds VMM à l’aide de Site Recovery sur le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="663ea-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="663ea-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="663ea-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="663ea-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="663ea-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="663ea-106">PowerShell Resource Manager</span><span class="sxs-lookup"><span data-stu-id="663ea-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="663ea-107">PowerShell Classic</span><span class="sxs-lookup"><span data-stu-id="663ea-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="663ea-108">Cet article fournit une vue d’ensemble des étapes nécessaires pour répliquer vers Azure des machines virtuelles Hyper-V locales gérées dans les clouds System Center Virtual Machine Manager (VMM) à l’aide du service [Azure Site Recovery](site-recovery-overview.md) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="663ea-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="663ea-109">Après avoir lu cet article, publiez des commentaires au bas de ce dernier ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="663ea-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="663ea-110">Étape 1 : Examen de l’architecture du scénario</span><span class="sxs-lookup"><span data-stu-id="663ea-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="663ea-111">Avant de commencer le déploiement, vérifiez l’architecture du scénario et prenez connaissance de tous les composants que vous devez déployer.</span><span class="sxs-lookup"><span data-stu-id="663ea-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="663ea-112">Aller à [Étape 1 : Examen de l’architecture](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="663ea-113">Étape 2 : Examen des prérequis et des limitations</span><span class="sxs-lookup"><span data-stu-id="663ea-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="663ea-114">Vérifiez que vous comprenez les prérequis et les limitations du déploiement.</span><span class="sxs-lookup"><span data-stu-id="663ea-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="663ea-115">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="663ea-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="663ea-116">**Serveurs VMM et hôtes Hyper-V locaux** : assurez-vous que les serveurs VMM et les hôtes Hyper-V sont conformes et préparés pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="663ea-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="663ea-117">**Machines virtuelles répliquées** : vérifiez que les machines virtuelles à répliquer sont conformes aux conditions requises pour Azure.</span><span class="sxs-lookup"><span data-stu-id="663ea-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="663ea-118">Aller à [Étape 2 : vérifier les conditions préalables et les limitations](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="663ea-119">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="663ea-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="663ea-120">Si vous effectuez un déploiement complet, vous devez déterminer les ressources de réplication dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="663ea-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="663ea-121">Pour ce faire, vous disposez de plusieurs outils.</span><span class="sxs-lookup"><span data-stu-id="663ea-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="663ea-122">Si vous souhaitez réaliser une configuration rapide pour tester l’environnement, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="663ea-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="663ea-123">Aller à [Étape 3 : Planifier la capacité](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="663ea-124">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="663ea-124">Step 4: Plan networking</span></span>

<span data-ttu-id="663ea-125">Vous devez effectuer une planification réseau pour vous assurer que vous pouvez configurer le mappage réseau lorsque vous déployez le scénario, que les machines virtuelles Azure seront connectées aux réseaux virtuels Azure après le basculement et que des adresses IP appropriées leur sont attribuées.</span><span class="sxs-lookup"><span data-stu-id="663ea-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="663ea-126">Aller à [Étape 4 : Planifier la mise en réseau](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="663ea-127">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="663ea-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="663ea-128">Configurez un compte Azure, des réseaux et du stockage.</span><span class="sxs-lookup"><span data-stu-id="663ea-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="663ea-129">Vous pouvez le faire pendant le déploiement, mais nous vous recommandons de vous en occuper avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="663ea-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="663ea-130">Aller à [Étape 5 : Préparer Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="663ea-131">Étape 6 : Préparer VMM et Hyper-V</span><span class="sxs-lookup"><span data-stu-id="663ea-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="663ea-132">Préparez les serveurs VMM et les hôtes Hyper-V locaux pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="663ea-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="663ea-133">Aller à [Étape 6 : Préparer les serveurs locaux](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="663ea-134">Étape 7 : configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="663ea-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="663ea-135">Configurez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="663ea-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="663ea-136">Le coffre comporte les paramètres de configuration et orchestre la réplication.</span><span class="sxs-lookup"><span data-stu-id="663ea-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="663ea-137">Étape 7 : Configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="663ea-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="663ea-138">Étape 8 : configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="663ea-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="663ea-139">Configurez les emplacements de réplication source et cible.</span><span class="sxs-lookup"><span data-stu-id="663ea-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="663ea-140">Ajoutez le serveur VMM au coffre et téléchargez les fichiers d’installation pour les composants de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="663ea-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="663ea-141">Exécutez le fournisseur Azure Site Recovery sur le serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="663ea-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="663ea-142">La configuration installe le fournisseur sur le serveur VMM et enregistre ce dernier dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="663ea-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="663ea-143">Vous installez l’agent Microsoft Recovery Services sur chaque hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="663ea-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="663ea-144">Aller à [Étape 8 : Configurer les paramètres de source et de cible](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="663ea-145">Étape 9 : Configurer le mappage réseau</span><span class="sxs-lookup"><span data-stu-id="663ea-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="663ea-146">Mappez des réseaux de machines virtuels VMM locaux à des réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="663ea-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="663ea-147">Après le basculement, les machines virtuelles Azure sont créées dans le réseau Azure mappé au réseau de machines virtuelles local dans lequel se trouve la source Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="663ea-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="663ea-148">Aller à [Étape 9 : Configurer le mappage réseau](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="663ea-149">Étape 10 : Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="663ea-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="663ea-150">Spécifiez le mode de réplication des machines virtuelles locales vers Azure.</span><span class="sxs-lookup"><span data-stu-id="663ea-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="663ea-151">Aller à [Étape 10 : Configurer une stratégie de réplication](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="663ea-152">Étape 11 : Activer la réplication des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="663ea-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="663ea-153">Sélectionnez les machines virtuelles à répliquer.</span><span class="sxs-lookup"><span data-stu-id="663ea-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="663ea-154">L’activation de la réplication d’une machine virtuelle déclenche la réplication initiale vers Azure, suivie de la réplication delta en cours.</span><span class="sxs-lookup"><span data-stu-id="663ea-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="663ea-155">Aller à [Étape 11 : activer la réplication](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="663ea-156">Étape 12 : exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="663ea-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="663ea-157">Exécutez un test de basculement afin de vérifier que tout fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="663ea-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="663ea-158">Aller à [Étape 12 : exécuter un test de basculement](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="663ea-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


