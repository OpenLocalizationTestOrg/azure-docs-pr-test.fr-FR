---
title: "aaaReplicate machines virtuelles Azure entre les régions Azure | Des documents Microsoft"
description: "Résume hello étapes requises tooreplicate machines virtuelles Azure entre des régions Azure avec le service d’Azure Site Recovery hello Bonjour portail Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="07d89-103">Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="07d89-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="07d89-104">Cet article fournit une vue d’ensemble de tooreplicate requis des étapes de hello machines virtuelles Azure (VM) dans une région Azure tooAzure machines virtuelles dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="07d89-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="07d89-105">La réplication de machines virtuelles Azure est actuellement disponible en préversion.</span><span class="sxs-lookup"><span data-stu-id="07d89-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="07d89-106">Ajouter des commentaires et questions bas hello de cet article ou sur hello [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="07d89-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="07d89-107">Étape 1 : examen de l’architecture</span><span class="sxs-lookup"><span data-stu-id="07d89-107">Step 1: Review architecture</span></span>

<span data-ttu-id="07d89-108">Avant de commencer le déploiement, passez en revue l’architecture du scénario hello et composants hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="07d89-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="07d89-109">Accédez trop[étape 1 : examen de l’architecture de hello](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="07d89-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="07d89-110">Étape 2 : Vérifier les conditions préalables</span><span class="sxs-lookup"><span data-stu-id="07d89-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="07d89-111">Vérifiez que vous avez hello Azure conditions préalables dans des lieux, y compris un abonnement, les réseaux virtuels, les comptes de stockage et les exigences de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="07d89-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="07d89-112">Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="07d89-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="07d89-113">Étape 3 : Planifier la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="07d89-113">Step 3: Plan networking</span></span>

<span data-ttu-id="07d89-114">Vérifiez que la connectivité sortante est configurée sur des machines virtuelles de Azure vous voulez tooreplicate et que les connexions du site sont configurées.</span><span class="sxs-lookup"><span data-stu-id="07d89-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="07d89-115">Accédez trop[étape 4 : planifier la mise en réseau](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="07d89-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="07d89-116">Étape 4 : créer un coffre</span><span class="sxs-lookup"><span data-stu-id="07d89-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="07d89-117">Vous devez tooset d’un tooorchestrate du coffre Recovery Services et gérez la réplication et spécifiez la région de la source hello.</span><span class="sxs-lookup"><span data-stu-id="07d89-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="07d89-118">Accédez trop[étape 4 : créer un coffre](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="07d89-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="07d89-119">Étape 5 : activer la réplication</span><span class="sxs-lookup"><span data-stu-id="07d89-119">Step 5: Enable replication</span></span>


<span data-ttu-id="07d89-120">tooenable la réplication, vous configurez les paramètres de l’emplacement cible, définir une stratégie de réplication et sélectionnez hello machines virtuelles d’Azure que vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="07d89-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="07d89-121">Après l’activation, la réplication initiale de hello machine virtuelle se produit.</span><span class="sxs-lookup"><span data-stu-id="07d89-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="07d89-122">Accédez trop[étape 5 : activer la réplication](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="07d89-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="07d89-123">Étape 6 : exécuter un test de basculement</span><span class="sxs-lookup"><span data-stu-id="07d89-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="07d89-124">Une fois la réplication initiale se termine, et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="07d89-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="07d89-125">Accédez trop[étape 6 : exécuter un test de basculement](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="07d89-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


