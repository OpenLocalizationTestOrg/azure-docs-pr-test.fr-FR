---
title: "Répliquer des serveurs physiques locaux vers Azure avec Azure Site Recovery | Microsoft Docs"
description: "Fournit une vue d’ensemble des étapes pour la réplication des charges de travail exécutées sur des serveurs physiques locaux Windows/Linux vers Azure avec le service Azure Site Recovery."
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
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="496bb-103">Répliquer des serveurs physiques vers Azure avec Site Recovery</span><span class="sxs-lookup"><span data-stu-id="496bb-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="496bb-104">Cet article fournit une vue d’ensemble des étapes à suivre pour répliquer des serveurs physiques locaux Windows/Linux vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="496bb-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="496bb-105">Étape 1 : Vérifier l’architecture et les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="496bb-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="496bb-106">Avant de commencer le déploiement, vérifiez l’architecture du scénario et prenez connaissance de tous les composants nécessaires pour procéder au déploiement.</span><span class="sxs-lookup"><span data-stu-id="496bb-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="496bb-107">Aller à [Étape 1 : Examen de l’architecture](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="496bb-108">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="496bb-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="496bb-109">Assurez-vous que les conditions préalables sont remplies pour chaque composant du déploiement :</span><span class="sxs-lookup"><span data-stu-id="496bb-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="496bb-110">**Conditions préalables Azure** : vous avez besoin d’un compte Microsoft Azure, d’un réseau Azure et de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="496bb-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="496bb-111">**Composants Site Recovery locaux** : vous avez besoin d’une machine exécutant les composants Site Recovery locaux.</span><span class="sxs-lookup"><span data-stu-id="496bb-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="496bb-112">**Machines répliquées** : les serveurs à répliquer doivent remplir les conditions requises pour l’environnement local et Azure.</span><span class="sxs-lookup"><span data-stu-id="496bb-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="496bb-113">Aller à [Étape 2 : Vérifier les conditions préalables et les limitations](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="496bb-114">Étape 3 : planifier la capacité</span><span class="sxs-lookup"><span data-stu-id="496bb-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="496bb-115">Si vous effectuez un déploiement complet, vous devez déterminer les ressources de réplication dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="496bb-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="496bb-116">Si vous souhaitez réaliser une configuration rapide pour tester l’environnement, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="496bb-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="496bb-117">Aller à [Étape 3 : Planifier la capacité](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="496bb-118">Étape 4 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="496bb-118">Step 4: Plan networking</span></span>

<span data-ttu-id="496bb-119">Vous devez établir un plan du réseau pour vous assurer que les machines virtuelles Azure sont connectées aux réseaux après le basculement et qu’elles disposent des bonnes adresses IP.</span><span class="sxs-lookup"><span data-stu-id="496bb-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="496bb-120">Aller à [Étape 4 : Planifier la mise en réseau](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="496bb-121">Étape 5 : Préparer les ressources Azure</span><span class="sxs-lookup"><span data-stu-id="496bb-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="496bb-122">Configurez les réseaux et le stockage Azure avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="496bb-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="496bb-123">Aller à [Étape 5 : Préparer Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="496bb-124">Étape 6 : Configurer un coffre</span><span class="sxs-lookup"><span data-stu-id="496bb-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="496bb-125">Vous devez configurer un coffre Recovery Services pour orchestrer et gérer la réplication.</span><span class="sxs-lookup"><span data-stu-id="496bb-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="496bb-126">Lors de la configuration du coffre, vous spécifiez les éléments à répliquer et leur destination de réplication.</span><span class="sxs-lookup"><span data-stu-id="496bb-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="496bb-127">Aller à [Étape 6 : Configurer un coffre](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="496bb-128">Étape 7 : Configurer les paramètres de source et de cible</span><span class="sxs-lookup"><span data-stu-id="496bb-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="496bb-129">Configurez les paramètres des sites source et cible (Azure).</span><span class="sxs-lookup"><span data-stu-id="496bb-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="496bb-130">Pour les paramètres source, vous devez exécuter une installation unifiée afin d’installer les composants Site Recovery locaux.</span><span class="sxs-lookup"><span data-stu-id="496bb-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="496bb-131">Aller à [Étape 7 : Configurer la source et la cible](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="496bb-132">Étape 8 : Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="496bb-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="496bb-133">Vous configurez une stratégie pour spécifier les modalités de réplication des serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="496bb-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="496bb-134">Aller à [Étape 8 : Configurer une stratégie de réplication](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="496bb-135">Étape 9 : Installer le service Mobilité</span><span class="sxs-lookup"><span data-stu-id="496bb-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="496bb-136">Le service Mobilité doit être installé sur chaque serveur que vous souhaitez répliquer.</span><span class="sxs-lookup"><span data-stu-id="496bb-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="496bb-137">Il existe plusieurs méthodes de configuration du service à l’aide d’une installation push ou pull.</span><span class="sxs-lookup"><span data-stu-id="496bb-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="496bb-138">Aller à [Étape 9 : Installer le service Mobilité](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="496bb-139">Étape 10 : Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="496bb-139">Step 10: Enable replication</span></span>

<span data-ttu-id="496bb-140">Vous pouvez activer la réplication une fois que le service Mobilité est en cours d’exécution sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="496bb-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="496bb-141">La réplication initiale de la machine virtuelle se produira après l’activation.</span><span class="sxs-lookup"><span data-stu-id="496bb-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="496bb-142">Aller à [Étape 10 : Activer la réplication](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="496bb-143">Étape 11 : Exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="496bb-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="496bb-144">Lorsque la réplication initiale est terminée et que la réplication delta est en cours d’exécution, vous pouvez exécuter un test de basculement pour vous assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="496bb-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="496bb-145">Aller à [Étape 11 : Exécuter un test de basculement](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="496bb-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

