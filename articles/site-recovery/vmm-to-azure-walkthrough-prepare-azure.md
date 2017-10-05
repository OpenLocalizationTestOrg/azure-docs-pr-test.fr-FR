---
title: "Préparation des ressources Azure pour répliquer des machines virtuelles Hyper-V (avec System Center VMM) vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Décrit les éléments à mettre en place dans Azure avant de commencer la réplication de machines virtuelles Hyper-V (avec VMM) vers Azure à l’aide d’Azure Site Recovery"
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
ms.openlocfilehash: 63b005f37ab5e15e8a1b4645446d65f1529f1bbd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="a94b4-103">Étape 5 : Préparer les ressources Azure pour la réplication de Hyper-V (avec VMM) vers Azure</span><span class="sxs-lookup"><span data-stu-id="a94b4-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="a94b4-104">Après avoir vérifié la [configuration réseau requise](vmm-to-azure-walkthrough-network.md), utilisez les instructions fournies dans cet article pour préparer les ressources Azure de manière à pouvoir répliquer des machines virtuelles Hyper-V locales dans les clouds System Center Virtual Machine Manager (VMM) vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a94b4-105">Après avoir lu cet article, envoyez vos commentaires en bas ou posez vos questions techniques sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a94b4-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="a94b4-106">Configurer un compte Azure</span><span class="sxs-lookup"><span data-stu-id="a94b4-106">Set up an Azure account</span></span>

- <span data-ttu-id="a94b4-107">Procurez-vous un [compte Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a94b4-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="a94b4-108">Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a94b4-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="a94b4-109">Vérifiez les régions prises en charge pour Site Recovery dans la section Disponibilité géographique de la page [Tarification d’Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="a94b4-109">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="a94b4-110">Lisez les informations relatives à la [tarification de Site Recovery](site-recovery-faq.md#pricing) et prenez connaissance de la [tarification appliquée](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a94b4-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="a94b4-111">Assurez-vous que votre compte Azure dispose des [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) nécessaires pour créer des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="a94b4-111">Make sure your Azure account has the correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)to create Azure VMs.</span></span> <span data-ttu-id="a94b4-112">[En savoir plus](../active-directory/role-based-access-built-in-roles.md) sur le contrôle d’accès en fonction du rôle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a94b4-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="a94b4-113">Configurer un réseau Azure</span><span class="sxs-lookup"><span data-stu-id="a94b4-113">Set up an Azure network</span></span>

- <span data-ttu-id="a94b4-114">Configurez un [réseau Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="a94b4-115">Les machines virtuelles Azure sont placées dans ce réseau une fois créées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="a94b4-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="a94b4-116">Ce réseau doit se trouver dans la même région que le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="a94b4-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="a94b4-117">Site Recovery dans le portail Azure peut utiliser les réseaux configurés dans [Resource Manager](../resource-manager-deployment-model.md) ou en mode classique.</span><span class="sxs-lookup"><span data-stu-id="a94b4-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="a94b4-118">Nous vous recommandons de configurer un réseau avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="a94b4-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="a94b4-119">Sinon, vous devrez le faire lors du déploiement de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a94b4-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="a94b4-120">Prenez connaissance de la [tarification des réseaux virtuels](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="a94b4-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="a94b4-121">Configurer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="a94b4-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="a94b4-122">Site Recovery réplique les machines virtuelles locales sur le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="a94b4-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="a94b4-123">Des machines virtuelles Azure sont créées à partir du stockage après le basculement.</span><span class="sxs-lookup"><span data-stu-id="a94b4-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="a94b4-124">Configurez un [compte de stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) Standard ou Premium pour stocker les données répliquées vers Azure.</span><span class="sxs-lookup"><span data-stu-id="a94b4-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="a94b4-125">Le [stockage Premium](../storage/common/storage-premium-storage.md) est généralement utilisé pour les machines virtuelles nécessitant des performances d’E/S élevées et une faible latence pour héberger les charges de travail nécessitant beaucoup d’E/S.</span><span class="sxs-lookup"><span data-stu-id="a94b4-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="a94b4-126">Si vous souhaitez utiliser un compte Premium pour stocker les données répliquées, vous avez aussi besoin d’un compte de stockage standard afin de stocker les journaux de réplication qui capturent les modifications apportées en continu aux données locales.</span><span class="sxs-lookup"><span data-stu-id="a94b4-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="a94b4-127">Selon le modèle de ressource que vous souhaitez utiliser pour les machines virtuelles Azure ayant fait l’objet d’un basculement, vous allez configurer un compte en [mode Azure Resource Manager](../storage/common/storage-create-storage-account.md) ou en [mode Classic](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a94b4-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="a94b4-128">Nous vous recommandons de configurer un compte de stockage avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="a94b4-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="a94b4-129">Sinon, vous devrez le faire lors du déploiement de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a94b4-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="a94b4-130">Les comptes doivent se trouver dans la même région que le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="a94b4-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="a94b4-131">Vous ne pouvez pas déplacer de comptes de stockage utilisés par Site Recovery entre des groupes de ressources au sein du même abonnement, ou entre différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="a94b4-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a94b4-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a94b4-132">Next steps</span></span>

<span data-ttu-id="a94b4-133">Aller à [Étape 6 : Préparer VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="a94b4-133">Go to [Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
