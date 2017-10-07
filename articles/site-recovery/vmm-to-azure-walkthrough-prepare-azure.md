---
title: "aaaPrepare ressources Azure tooreplicate des ordinateurs virtuels Hyper-V (avec System Center VMM) tooAzure à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Décrit ce que vous avez besoin en place dans Azure avant de pouvoir répliquer des ordinateurs virtuels Hyper-V (avec VMM) tooAzure, à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="8867e-103">Étape 5 : Préparer les ressources Azure pour tooAzure de réplication (avec VMM) Hyper-V</span><span class="sxs-lookup"><span data-stu-id="8867e-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="8867e-104">Après avoir vérifié [exigences réseau](vmm-to-azure-walkthrough-network.md), suivez les instructions de hello de cette tooprepare article Azure ressources afin que vous pouvez répliquer des machines virtuelles de Hyper-V sur site dans System Center Virtual Machine Manager (VMM) clouds tooAzure, à l’aide Hello [Azure Site Recovery](site-recovery-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="8867e-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="8867e-105">Après avoir lu cet article, validez les commentaires en bas de hello ou poser des questions techniques sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8867e-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="8867e-106">Configurer un compte Azure</span><span class="sxs-lookup"><span data-stu-id="8867e-106">Set up an Azure account</span></span>

- <span data-ttu-id="8867e-107">Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="8867e-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="8867e-108">Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8867e-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="8867e-109">Vérifiez les régions hello pris en charge pour la récupération de Site, sous géographique disponibilité dans [détails de la tarification de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="8867e-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="8867e-110">En savoir plus sur [Site Recovery tarification](site-recovery-faq.md#pricing)et obtenir hello [tarification](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="8867e-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="8867e-111">Assurez-vous que votre compte Azure a hello correct [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="8867e-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="8867e-112">[En savoir plus](../active-directory/role-based-access-built-in-roles.md) sur le contrôle d’accès en fonction du rôle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8867e-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="8867e-113">Configurer un réseau Azure</span><span class="sxs-lookup"><span data-stu-id="8867e-113">Set up an Azure network</span></span>

- <span data-ttu-id="8867e-114">Configurez un [réseau Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="8867e-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="8867e-115">Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="8867e-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="8867e-116">réseau de Hello doivent se trouver dans hello Services de récupération de la même région que hello coffre</span><span class="sxs-lookup"><span data-stu-id="8867e-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="8867e-117">Récupération de site Bonjour portail Azure peut utiliser des réseaux définis dans [le Gestionnaire de ressources](../resource-manager-deployment-model.md), ou en mode classique.</span><span class="sxs-lookup"><span data-stu-id="8867e-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="8867e-118">Nous vous recommandons de configurer un réseau avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8867e-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="8867e-119">Si vous ne le faites pas, vous devez toodo il durant le déploiement de la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="8867e-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="8867e-120">Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="8867e-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="8867e-121">Configurer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8867e-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="8867e-122">Récupération de site réplique le stockage de tooAzure d’ordinateurs locaux.</span><span class="sxs-lookup"><span data-stu-id="8867e-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="8867e-123">Machines virtuelles Azure sont créés à partir du stockage de hello après que le basculement se produit.</span><span class="sxs-lookup"><span data-stu-id="8867e-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="8867e-124">Configurer un standard/premium [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold répliquées tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8867e-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="8867e-125">[Stockage Premium](../storage/common/storage-premium-storage.md) est généralement utilisé pour les ordinateurs virtuels qui nécessitent un manière cohérente hautes performances d’e/s et à faible latence toohost e/s intensives les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="8867e-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="8867e-126">Si vous voulez toouse un toostore de compte premium des données répliquées, vous devez également un journaux de réplication de compte de stockage standard toostore que capture en cours devient tooon locale, les données.</span><span class="sxs-lookup"><span data-stu-id="8867e-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="8867e-127">Selon le modèle de ressource hello souhaitées toouse de basculement des machines virtuelles Azure, vous devez définir un compte dans [mode Resource Manager](../storage/common/storage-create-storage-account.md), ou [en mode classique](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8867e-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="8867e-128">Nous vous recommandons de configurer un compte de stockage avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8867e-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="8867e-129">Si vous ne vous devez toodo il durant le déploiement de la récupération de Site.</span><span class="sxs-lookup"><span data-stu-id="8867e-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="8867e-130">Hello doivent être dans hello Services de récupération de la même région que hello coffre.</span><span class="sxs-lookup"><span data-stu-id="8867e-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="8867e-131">Vous ne pouvez pas déplacer des comptes de stockage utilisé par la récupération de Site entre les groupes de ressources de hello même abonnement, ou entre différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="8867e-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8867e-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8867e-132">Next steps</span></span>

<span data-ttu-id="8867e-133">Accédez trop[étape 6 : préparation de VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="8867e-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
