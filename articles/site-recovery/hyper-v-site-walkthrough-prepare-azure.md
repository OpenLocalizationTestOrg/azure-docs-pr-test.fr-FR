---
title: "Préparer les ressources Azure pour répliquer des machines virtuelles Hyper-V (sans System Center VMM) vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Décrit les éléments à mettre en place dans Azure avant de commencer la réplication de machines virtuelles Hyper-V (sans VMM) vers Azure à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="7ceab-103">Étape 5 : préparer les ressources Azure pour la réplication de Hyper-V vers Azure</span><span class="sxs-lookup"><span data-stu-id="7ceab-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="7ceab-104">Utilisez les instructions fournies dans cet article pour préparer les ressources Azure de manière à pouvoir répliquer des machines virtuelles Hyper-V locales (sans System Center VMM) vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ceab-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="7ceab-105">Après avoir lu cet article, envoyez vos commentaires en bas ou posez vos questions techniques sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7ceab-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7ceab-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7ceab-106">Before you start</span></span>

<span data-ttu-id="7ceab-107">Prenez connaissance des [conditions préalables](hyper-v-site-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="7ceab-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="7ceab-108">Configurer un compte Azure</span><span class="sxs-lookup"><span data-stu-id="7ceab-108">Set up an Azure account</span></span>

- <span data-ttu-id="7ceab-109">Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7ceab-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="7ceab-110">Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ceab-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="7ceab-111">Vérifiez les régions prises en charge pour Site Recovery dans la section Disponibilité géographique de la page [Tarification d’Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="7ceab-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="7ceab-112">Lisez les informations relatives à la [tarification de Site Recovery](site-recovery-faq.md#pricing) et prenez connaissance de la [tarification appliquée](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="7ceab-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="7ceab-113">Configurer un réseau Azure</span><span class="sxs-lookup"><span data-stu-id="7ceab-113">Set up an Azure network</span></span>

- <span data-ttu-id="7ceab-114">Configurez un réseau Azure</span><span class="sxs-lookup"><span data-stu-id="7ceab-114">Set up an Azure network.</span></span> <span data-ttu-id="7ceab-115">Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="7ceab-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="7ceab-116">Ce réseau doit se trouver dans la même région que le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="7ceab-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="7ceab-117">Site Recovery dans le portail Azure peut utiliser les réseaux configurés dans [Resource Manager](../resource-manager-deployment-model.md) ou en mode classique.</span><span class="sxs-lookup"><span data-stu-id="7ceab-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="7ceab-118">Nous vous recommandons de configurer un réseau avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="7ceab-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="7ceab-119">Sinon, vous devrez le faire lors du déploiement de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7ceab-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="7ceab-120">Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="7ceab-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="7ceab-121">Configurer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="7ceab-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="7ceab-122">Site Recovery réplique les machines virtuelles locales sur le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7ceab-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="7ceab-123">Des machines virtuelles Azure sont créées à partir du stockage après le basculement.</span><span class="sxs-lookup"><span data-stu-id="7ceab-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="7ceab-124">Configurez un [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) Standard ou Premium pour stocker les données répliquées vers Azure.</span><span class="sxs-lookup"><span data-stu-id="7ceab-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="7ceab-125">Le [stockage Premium](../storage/common/storage-premium-storage.md) est généralement utilisé pour les machines virtuelles nécessitant des performances d’E/S élevées et une faible latence pour héberger les charges de travail nécessitant beaucoup d’E/S.</span><span class="sxs-lookup"><span data-stu-id="7ceab-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="7ceab-126">Si vous souhaitez utiliser un compte Premium pour stocker les données répliquées, vous avez aussi besoin d’un compte de stockage standard afin de stocker les journaux de réplication qui capturent les modifications apportées en continu aux données locales.</span><span class="sxs-lookup"><span data-stu-id="7ceab-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="7ceab-127">Selon le modèle de ressource que vous souhaitez utiliser pour les machines virtuelles Azure ayant fait l’objet d’un basculement, vous allez configurer un compte en [mode Azure Resource Manager](../storage/common/storage-create-storage-account.md) ou en [mode Classic](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7ceab-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="7ceab-128">Nous vous recommandons de configurer un compte de stockage avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="7ceab-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="7ceab-129">Sinon, vous devrez le faire lors du déploiement de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7ceab-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="7ceab-130">Les comptes doivent se trouver dans la même région que le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="7ceab-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="7ceab-131">Vous ne pouvez pas déplacer de comptes de stockage utilisés par Site Recovery entre des groupes de ressources au sein du même abonnement, ou entre différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="7ceab-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ceab-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ceab-132">Next steps</span></span>

<span data-ttu-id="7ceab-133">Accédez à [Étape 6 : préparer les ressources Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="7ceab-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
