---
title: "tooreplicate de ressources Azure aaaPrepare local tooAzure les ordinateurs virtuels VMware à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit ce que vous avez besoin en place dans Azure avant de commencer la réplication tooAzure d’ordinateurs virtuels VMware local à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a><span data-ttu-id="94b3e-103">Étape 5 : Préparer les ressources Azure pour VMWare réplication tooAzure</span><span class="sxs-lookup"><span data-stu-id="94b3e-103">Step 5: Prepare Azure resources for VMWare replication tooAzure</span></span>


<span data-ttu-id="94b3e-104">Utilisez les instructions de hello dans cette tooprepare article Azure ressources afin que vous pouvez répliquer tooAzure d’ordinateurs locaux à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="94b3e-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises machines tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="94b3e-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="94b3e-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="94b3e-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="94b3e-106">Before you start</span></span>

<span data-ttu-id="94b3e-107">Vérifiez que vous avez lu hello [conditions préalables](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="94b3e-107">Make sure you've read hello [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="94b3e-108">Configurer un compte Azure</span><span class="sxs-lookup"><span data-stu-id="94b3e-108">Set up an Azure account</span></span>

- <span data-ttu-id="94b3e-109">Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="94b3e-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="94b3e-110">Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94b3e-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="94b3e-111">Vérifiez les régions hello pris en charge pour la récupération de Site, sous géographique disponibilité dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="94b3e-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="94b3e-112">En savoir plus sur [Site Recovery tarification](site-recovery-faq.md#pricing)et obtenir hello [tarification](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="94b3e-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="94b3e-113">Configurer un réseau Azure</span><span class="sxs-lookup"><span data-stu-id="94b3e-113">Set up an Azure network</span></span>

- <span data-ttu-id="94b3e-114">Configurez un réseau Azure</span><span class="sxs-lookup"><span data-stu-id="94b3e-114">Set up an Azure network.</span></span> <span data-ttu-id="94b3e-115">Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="94b3e-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="94b3e-116">Récupération de site Bonjour portail Azure peut utiliser des réseaux définis dans [le Gestionnaire de ressources](../resource-manager-deployment-model.md), ou en mode classique.</span><span class="sxs-lookup"><span data-stu-id="94b3e-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="94b3e-117">réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre</span><span class="sxs-lookup"><span data-stu-id="94b3e-117">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="94b3e-118">Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="94b3e-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="94b3e-119">Découvrez la [connectivité de la machine virtuelle Azure](site-recovery-network-design.md) après le basculement.</span><span class="sxs-lookup"><span data-stu-id="94b3e-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="94b3e-120">Configurer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="94b3e-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="94b3e-121">Récupération de site réplique le stockage de tooAzure d’ordinateurs locaux.</span><span class="sxs-lookup"><span data-stu-id="94b3e-121">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="94b3e-122">Machines virtuelles Azure sont créés à partir du stockage de hello après que le basculement se produit.</span><span class="sxs-lookup"><span data-stu-id="94b3e-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="94b3e-123">Configurer un [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) pour les données répliquées.</span><span class="sxs-lookup"><span data-stu-id="94b3e-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="94b3e-124">Récupération de site Bonjour portail Azure peut utiliser des comptes de stockage configurés dans le Gestionnaire de ressources, ou en mode classique.</span><span class="sxs-lookup"><span data-stu-id="94b3e-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="94b3e-125">compte de stockage Hello peut être standard ou [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="94b3e-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="94b3e-126">Si vous configurez un compte premium, vous aurez également besoin d’un compte standard supplémentaire pour les données de journal.</span><span class="sxs-lookup"><span data-stu-id="94b3e-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94b3e-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94b3e-127">Next steps</span></span>

<span data-ttu-id="94b3e-128">Accédez trop[étape 6 : VMware de préparer les ressources](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="94b3e-128">Go too[Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
