---
title: "Répliquer des machines virtuelles Hyper-V sur un site VMM secondaire avec Azure Site Recovery | Microsoft Docs"
description: "Présente la réplication des machines virtuelles Hyper-V sur un site VMM secondaire via le portail Azure."
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
ms.openlocfilehash: b422dd2cf23426de2f154a553b38509082536309
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a><span data-ttu-id="1059d-103">Répliquer des machines virtuelles Hyper-V dans des clouds VMM vers un site VMM secondaire</span><span class="sxs-lookup"><span data-stu-id="1059d-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1059d-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1059d-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="1059d-105">Portail classique</span><span class="sxs-lookup"><span data-stu-id="1059d-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="1059d-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1059d-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="1059d-107">Cet article fournit une vue d’ensemble des étapes nécessaires pour répliquer vers un emplacement VMM secondaire des machines virtuelles Hyper-V locales gérées dans les clouds System Center Virtual Machine Manager (VMM) à l’aide d’[Azure Site Recovery](site-recovery-overview.md) sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1059d-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="1059d-108">Après avoir lu cet article, publiez des commentaires au bas de ce dernier ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1059d-108">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="1059d-109">Étape 1 : Examen de l’architecture du scénario</span><span class="sxs-lookup"><span data-stu-id="1059d-109">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="1059d-110">Avant de commencer le déploiement, vérifiez l’architecture du scénario et prenez connaissance de tous les composants que vous devez déployer.</span><span class="sxs-lookup"><span data-stu-id="1059d-110">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="1059d-111">Aller à [Étape 1 : Examen de l’architecture](vmm-to-vmm-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-111">Go to [Step 1: Review the architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="1059d-112">Étape 2 : Vérifier les conditions préalables et les limitations</span><span class="sxs-lookup"><span data-stu-id="1059d-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="1059d-113">Vérifiez que vous comprenez les conditions préalables et les limitations du déploiement.</span><span class="sxs-lookup"><span data-stu-id="1059d-113">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="1059d-114">**Conditions préalables Azure** : vous avez besoin d’un abonnement Microsoft Azure et d’un coffre Azure Recovery Services pour orchestrer et gérer la réplication.</span><span class="sxs-lookup"><span data-stu-id="1059d-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, to orchestrate and manage replication.</span></span>
<span data-ttu-id="1059d-115">**Serveurs VMM et hôtes Hyper-V locaux** : assurez-vous que les serveurs VMM et les hôtes Hyper-V sont conformes et préparés pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1059d-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="1059d-116">Aller à [Étape 2 : Vérifier les conditions préalables et les limitations](vmm-to-vmm-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-116">Go to [Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="1059d-117">Étape 3 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="1059d-117">Step 3: Plan networking</span></span>

<span data-ttu-id="1059d-118">Vous devez planifier votre mise en réseau pour vous assurer que vous pouvez configurer le mappage entre les réseaux de machines virtuelles VMM lorsque vous déployez le scénario.</span><span class="sxs-lookup"><span data-stu-id="1059d-118">You need to do some network planning to ensure that you can configure network mapping between VMM VM networks when you deploy the scenario.</span></span>

<span data-ttu-id="1059d-119">Aller à [Étape 3 : Planifier la mise en réseau](vmm-to-vmm-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-119">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="1059d-120">Étape 4 : Préparer VMM et Hyper-V</span><span class="sxs-lookup"><span data-stu-id="1059d-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="1059d-121">Préparez les serveurs VMM et les hôtes Hyper-V pour le déploiement Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1059d-121">Prepare the VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="1059d-122">Aller à [Étape 4 : Préparer les serveurs locaux](vmm-to-vmm-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-122">Go to [Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="1059d-123">Étape 5 : Configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="1059d-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="1059d-124">Configurez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="1059d-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="1059d-125">Le coffre comporte les paramètres de configuration et orchestre la réplication.</span><span class="sxs-lookup"><span data-stu-id="1059d-125">The vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="1059d-126">[Étape 5 : Configurer un coffre](vmm-to-vmm-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="1059d-127">Étape 6 : Configurer les paramètres de la source et de la cible</span><span class="sxs-lookup"><span data-stu-id="1059d-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="1059d-128">Configurez les emplacements VMM de réplication source et cible.</span><span class="sxs-lookup"><span data-stu-id="1059d-128">Set up the source and target replication VMM locations.</span></span> <span data-ttu-id="1059d-129">Ajoutez les serveurs VMM au coffre et téléchargez les fichiers d’installation pour les composants de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1059d-129">Add the VMM servers to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="1059d-130">Exécutez le fournisseur Azure Site Recovery sur le serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="1059d-130">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="1059d-131">La configuration installe le fournisseur sur le serveur VMM et enregistre ce dernier dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="1059d-131">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="1059d-132">Vous installez l’agent Microsoft Recovery Services sur chaque hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1059d-132">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="1059d-133">Aller à [Étape 6 : Configurer les paramètres de la source et de la cible](vmm-to-vmm-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-133">Go to [Step 6: Set up the source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="1059d-134">Étape 7 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="1059d-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="1059d-135">Mappez les réseaux de machines virtuelles VMM dans les emplacements source et cible.</span><span class="sxs-lookup"><span data-stu-id="1059d-135">Map VMM VM networks in the source and target locations.</span></span> <span data-ttu-id="1059d-136">Après le basculement, les machines virtuelles sont créées dans le réseau cible mappé au réseau de machines virtuelles source dans lequel se trouve la machine virtuelle Hyper-V source.</span><span class="sxs-lookup"><span data-stu-id="1059d-136">After failover, VMs are created in the target network that maps to the source VM network in which the source Hyper-V VM is located.</span></span>

<span data-ttu-id="1059d-137">Aller à [Étape 7 : Configuration du mappage réseau](vmm-to-vmm-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-137">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="1059d-138">Étape 8 : Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="1059d-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="1059d-139">Spécifiez comment les machines virtuelles seront répliquées entre les emplacements VMM.</span><span class="sxs-lookup"><span data-stu-id="1059d-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="1059d-140">Aller à [Étape 8 : configurer une stratégie de réplication](vmm-to-vmm-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-140">Go to [Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="1059d-141">Étape 9 : Activer la réplication des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1059d-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="1059d-142">Sélectionnez les machines virtuelles à répliquer.</span><span class="sxs-lookup"><span data-stu-id="1059d-142">Select the VMs you want to replicate.</span></span> <span data-ttu-id="1059d-143">L’activation de la réplication d’une machine virtuelle déclenche la réplication initiale vers le site secondaire, suivie de la réplication delta en cours.</span><span class="sxs-lookup"><span data-stu-id="1059d-143">Enabling a VM for replication triggers the initial replication to the secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="1059d-144">Aller à [Étape 9 : Activer la réplication](vmm-to-vmm-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-144">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="1059d-145">Étape 10 : Exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="1059d-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="1059d-146">Exécutez un test de basculement afin de vérifier que tout fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="1059d-146">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="1059d-147">Aller à [Étape 10 : Exécuter un test de basculement](vmm-to-vmm-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="1059d-147">Go to [Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
