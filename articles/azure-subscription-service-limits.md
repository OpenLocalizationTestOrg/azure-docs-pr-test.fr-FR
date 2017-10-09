---
title: "abonnement d’aaaAzure limites et quotas | Documents Microsoft"
description: Fournit une liste des abonnements Azure et des limites, quotas et contraintes de service habituels. Cela inclut des informations sur comment tooincrease limite ainsi que les valeurs maximales.
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="3a12f-104">Abonnement Azure et limites, quotas et contraintes de service</span><span class="sxs-lookup"><span data-stu-id="3a12f-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="3a12f-105">Ce document répertorie quelques-unes des limites de Microsoft Azure courants hello, qui sont également appelées quotas.</span><span class="sxs-lookup"><span data-stu-id="3a12f-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="3a12f-106">Ce document ne couvre pas actuellement tous les services Azure.</span><span class="sxs-lookup"><span data-stu-id="3a12f-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="3a12f-107">Au fil du temps, liste de hello sera développé et mis à jour toocover plus de plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="3a12f-108">Visitez [vue d’ensemble de la tarification Azure](https://azure.microsoft.com/pricing/) toolearn plus d’informations sur la tarification Azure.</span><span class="sxs-lookup"><span data-stu-id="3a12f-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="3a12f-109">Là, vous pouvez estimer les coûts à l’aide de hello [calculatrice de tarification](https://azure.microsoft.com/pricing/calculator/) ou en visitant la page de détails pour un service de tarification de hello (par exemple, [les machines virtuelles Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="3a12f-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="3a12f-110">Pour obtenir des conseils toohelp gérer les coûts, consultez [empêcher les coûts inattendus avec la gestion des coûts et la facturation Azure](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3a12f-111">Si vous souhaitez limite de hello tooraise ou quota ci-dessus hello **par défaut de limite**, [ouvrir une demande de support technique en ligne sans frais](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="3a12f-112">Hello limites ne peuvent pas être déclenchés ci-dessus hello **limite maximale** valeur affichée dans les tableaux suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="3a12f-113">S’il existe aucune **limite maximale** colonne, les ressources hello puis ne limites réglables.</span><span class="sxs-lookup"><span data-stu-id="3a12f-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="3a12f-114">Les abonnements d’essai gratuit ne permettent pas de bénéficier d’augmentations de la limite ou du quota.</span><span class="sxs-lookup"><span data-stu-id="3a12f-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="3a12f-115">Si vous avez une version d’évaluation gratuite, vous pouvez mettre à niveau tooa [paiement à l’utilisation](https://azure.microsoft.com/offers/ms-azr-0003p/) abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a12f-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="3a12f-116">Pour plus d’informations, consultez [mise à niveau d’évaluation gratuite Azure tooPay-sous-vous-Go](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="3a12f-117">Limites et hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a12f-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="3a12f-118">Il est désormais possible toocombine plusieurs ressources Azure dans tooa un seul groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3a12f-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="3a12f-119">Lorsque vous utilisez des groupes de ressources, les limites qu’une seule fois étaient globaux gérées au niveau régional avec hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a12f-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="3a12f-120">Pour plus d’informations sur les groupes de ressources, consultez la [Vue d’ensemble d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="3a12f-121">Dans les limites de hello ci-dessous, une nouvelle table a été ajouté tooreflect toutes les différences dans les limites lors de l’utilisation de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3a12f-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="3a12f-122">Par exemple, vous disposez d’une table **Limites d’abonnement** et d’une table **Limites d’abonnement – Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="3a12f-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="3a12f-123">Lorsqu’une limite s’applique aux scénarios de tooboth, il ne s’affiche dans la première table de hello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="3a12f-124">Sauf indication contraire, les limites sont globales dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="3a12f-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="3a12f-125">Il est important tooemphasize que les quotas pour les ressources dans les groupes de ressources Azure sont accessibles par votre abonnement par région et par abonnement, ne sont pas hello service Gestion des quotas sont.</span><span class="sxs-lookup"><span data-stu-id="3a12f-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="3a12f-126">Nous allons utiliser des quotas de base à titre d'exemple.</span><span class="sxs-lookup"><span data-stu-id="3a12f-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="3a12f-127">Si vous avez besoin d’un quota augmenter avec prise en charge des cœurs de toorequest, vous devez toodecide comment un nombre de cœurs souhaité toouse dans les différentes régions, puis effectuer une demande spécifique pour un groupe de ressources Azure de base quotas pour les zones que vous souhaitez et les montants de hello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="3a12f-128">Par conséquent, si vous avez besoin de toouse 30 cœurs dans Europe de l’ouest toorun votre application Vous devez spécifiquement demander 30 cœurs dans Europe de l’ouest.</span><span class="sxs-lookup"><span data-stu-id="3a12f-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="3a12f-129">Mais vous n’avez pas un quota de cœurs augmenter dans n’importe quelle autre région--Europe de l’ouest uniquement aura un quota de cœur 30 hello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="3a12f-130">Par conséquent, il peut s’avérer utile tooconsider décider ce que les quotas de votre groupe de ressources Azure doivent toobe pour votre charge de travail dans une région et demande que le montant de chaque région dans laquelle vous envisagez de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3a12f-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="3a12f-131">Pour vous aider à découvrir vos quotas actuels pour des régions spécifiques, consultez la page [Dépannage de problèmes de déploiement](resource-manager-common-deployment-errors.md)</span><span class="sxs-lookup"><span data-stu-id="3a12f-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="3a12f-132">Limites de service spécifique</span><span class="sxs-lookup"><span data-stu-id="3a12f-132">Service-specific limits</span></span>
* [<span data-ttu-id="3a12f-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a12f-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="3a12f-134">Gestion des API</span><span class="sxs-lookup"><span data-stu-id="3a12f-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="3a12f-135">App Service</span><span class="sxs-lookup"><span data-stu-id="3a12f-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="3a12f-136">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3a12f-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="3a12f-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="3a12f-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="3a12f-138">Automation</span><span class="sxs-lookup"><span data-stu-id="3a12f-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="3a12f-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3a12f-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="3a12f-140">Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="3a12f-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="3a12f-141">Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="3a12f-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="3a12f-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3a12f-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="3a12f-143">Sauvegarde</span><span class="sxs-lookup"><span data-stu-id="3a12f-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="3a12f-144">Batch</span><span class="sxs-lookup"><span data-stu-id="3a12f-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="3a12f-145">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="3a12f-146">CDN</span><span class="sxs-lookup"><span data-stu-id="3a12f-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="3a12f-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="3a12f-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="3a12f-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="3a12f-149">Data Factory</span><span class="sxs-lookup"><span data-stu-id="3a12f-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="3a12f-150">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3a12f-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="3a12f-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3a12f-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="3a12f-152">DNS</span><span class="sxs-lookup"><span data-stu-id="3a12f-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="3a12f-153">Concentrateurs d'événements</span><span class="sxs-lookup"><span data-stu-id="3a12f-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="3a12f-154">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3a12f-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="3a12f-155">Key Vault</span><span class="sxs-lookup"><span data-stu-id="3a12f-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="3a12f-156">Log Analytics / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="3a12f-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="3a12f-157">Media Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="3a12f-158">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3a12f-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="3a12f-159">Mobile Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="3a12f-160">Surveiller</span><span class="sxs-lookup"><span data-stu-id="3a12f-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="3a12f-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3a12f-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="3a12f-162">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="3a12f-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="3a12f-163">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="3a12f-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="3a12f-164">Service de hub de notification</span><span class="sxs-lookup"><span data-stu-id="3a12f-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="3a12f-165">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3a12f-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="3a12f-166">Scheduler</span><span class="sxs-lookup"><span data-stu-id="3a12f-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="3a12f-167">action</span><span class="sxs-lookup"><span data-stu-id="3a12f-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="3a12f-168">Service Bus</span><span class="sxs-lookup"><span data-stu-id="3a12f-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="3a12f-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3a12f-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="3a12f-170">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="3a12f-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="3a12f-171">Stockage</span><span class="sxs-lookup"><span data-stu-id="3a12f-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="3a12f-172">Système StorSimple</span><span class="sxs-lookup"><span data-stu-id="3a12f-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="3a12f-173">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3a12f-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="3a12f-174">Abonnement</span><span class="sxs-lookup"><span data-stu-id="3a12f-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="3a12f-175">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="3a12f-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="3a12f-176">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3a12f-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="3a12f-177">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3a12f-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="3a12f-178">Limites d’abonnement</span><span class="sxs-lookup"><span data-stu-id="3a12f-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="3a12f-179">Limites d’abonnement</span><span class="sxs-lookup"><span data-stu-id="3a12f-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="3a12f-180">Limites d’abonnement – Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a12f-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="3a12f-181">Hello suivant limites s’appliquent lorsque vous utilisez hello Azure Resource Manager et les groupes de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3a12f-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="3a12f-182">Les limites qui n’ont pas changé avec hello Azure Resource Manager ne sont pas répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3a12f-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="3a12f-183">Pour ces limites, consultez le tableau précédent de toohello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="3a12f-184">Pour plus d’informations sur la gestion des limites sur les demandes Resource Manager, consultez [Limitation des requêtes Resource Manager](resource-manager-request-limits.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="3a12f-185">Limites de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3a12f-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="3a12f-186">Limites de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3a12f-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="3a12f-187">Limites de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3a12f-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="3a12f-188">Limites de machines virtuelles - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a12f-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="3a12f-189">Hello suivant limites s’appliquent lorsque vous utilisez hello Azure Resource Manager et les groupes de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3a12f-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="3a12f-190">Les limites qui n’ont pas changé avec hello Azure Resource Manager ne sont pas répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3a12f-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="3a12f-191">Pour ces limites, consultez le tableau précédent de toohello.</span><span class="sxs-lookup"><span data-stu-id="3a12f-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="3a12f-192">Limites des jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3a12f-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="3a12f-193">Limites de Container Instances</span><span class="sxs-lookup"><span data-stu-id="3a12f-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="3a12f-194">Limites de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="3a12f-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="3a12f-195">Limites de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="3a12f-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="3a12f-196">Limites d’Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3a12f-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="3a12f-197">Limites de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="3a12f-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="3a12f-198">Limites de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="3a12f-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="3a12f-199">Limites de DNS</span><span class="sxs-lookup"><span data-stu-id="3a12f-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="3a12f-200">Limites de stockage</span><span class="sxs-lookup"><span data-stu-id="3a12f-200">Storage limits</span></span>
<span data-ttu-id="3a12f-201">Pour plus d'informations sur les limites des comptes de stockage, consultez [Objectifs de performance et d’extensibilité Azure Storage](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="3a12f-202">Limites de service de stockage</span><span class="sxs-lookup"><span data-stu-id="3a12f-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="3a12f-203">Limites du nombre de disques de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3a12f-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="3a12f-204">Pour plus d'informations, consultez [Tailles des machines virtuelles](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="3a12f-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="3a12f-205">Disques de machines virtuelles gérées</span><span class="sxs-lookup"><span data-stu-id="3a12f-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="3a12f-206">Disques de machines virtuelles non gérées</span><span class="sxs-lookup"><span data-stu-id="3a12f-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="3a12f-207">Limites de fournisseur de ressources de stockage</span><span class="sxs-lookup"><span data-stu-id="3a12f-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="3a12f-208">Limites de services cloud</span><span class="sxs-lookup"><span data-stu-id="3a12f-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="3a12f-209">Limites App Service</span><span class="sxs-lookup"><span data-stu-id="3a12f-209">App Service limits</span></span>
<span data-ttu-id="3a12f-210">suit Hello que du Service d’applications limite inclure des limites pour les applications Web, les applications mobiles, les applications API et Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="3a12f-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="3a12f-211">Limites de planificateur</span><span class="sxs-lookup"><span data-stu-id="3a12f-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="3a12f-212">Limites Azure Batch</span><span class="sxs-lookup"><span data-stu-id="3a12f-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="3a12f-213">Limites de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-213">BizTalk Services limits</span></span>
<span data-ttu-id="3a12f-214">Hello tableau suivant présente les limites de hello pour Azure Biztalk Services.</span><span class="sxs-lookup"><span data-stu-id="3a12f-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="3a12f-215">Limites d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3a12f-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="3a12f-216">Base de données Cosmos Azure est une base de données à l’échelle mondiale dans lequel le débit et le stockage peut être mis à l’échelle toohandle tout ce que votre application requiert.</span><span class="sxs-lookup"><span data-stu-id="3a12f-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="3a12f-217">Si vous avez des questions sur l’échelle de hello fournit de la base de données Azure Cosmos, envoyez un courrier électronique tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="3a12f-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="3a12f-218">Limites Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3a12f-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="3a12f-219">Limites Azure Search</span><span class="sxs-lookup"><span data-stu-id="3a12f-219">Search limits</span></span>
<span data-ttu-id="3a12f-220">Niveaux de tarification déterminent la capacité de hello et les limites de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3a12f-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="3a12f-221">Les niveaux sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3a12f-221">Tiers include:</span></span>

* <span data-ttu-id="3a12f-222">*Gratuit* : service mutualisé, partagé avec d’autres abonnés Azure, destiné à des projets d’évaluation et de développement de petite taille.</span><span class="sxs-lookup"><span data-stu-id="3a12f-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="3a12f-223">*Base* fournit des ressources de calcul dédiés pour les charges de production à une plus petite échelle, avec des réplicas toothree pour les charges de travail requête hautement disponible.</span><span class="sxs-lookup"><span data-stu-id="3a12f-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="3a12f-224">*Standard (S1, S2, S3, S3 haute densité)* est approprié pour des charges de travail de production de plus grande taille.</span><span class="sxs-lookup"><span data-stu-id="3a12f-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="3a12f-225">Plusieurs niveaux se trouvent au sein du niveau standard de hello afin que vous pouvez choisir une configuration de ressource qui correspond le mieux à votre profil de charge de travail.</span><span class="sxs-lookup"><span data-stu-id="3a12f-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="3a12f-226">**Limites par abonnement**</span><span class="sxs-lookup"><span data-stu-id="3a12f-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="3a12f-227">**Limites par service de recherche**</span><span class="sxs-lookup"><span data-stu-id="3a12f-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="3a12f-228">toolearn savoir plus sur les limites relatives à un niveau plus granulaire, telles que la taille du document, les requêtes par seconde, les clés, les demandes et réponses, consultez [Service limites dans Azure Search](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="3a12f-229">Limites de Media Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="3a12f-230">Limites de CDN</span><span class="sxs-lookup"><span data-stu-id="3a12f-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="3a12f-231">Limites Mobile Services</span><span class="sxs-lookup"><span data-stu-id="3a12f-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="3a12f-232">Limites de Monitor</span><span class="sxs-lookup"><span data-stu-id="3a12f-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="3a12f-233">Limites du service Notification Hub</span><span class="sxs-lookup"><span data-stu-id="3a12f-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="3a12f-234">Limites de concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="3a12f-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="3a12f-235">Limites de Service Bus</span><span class="sxs-lookup"><span data-stu-id="3a12f-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="3a12f-236">Limites de hub IoT (IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="3a12f-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="3a12f-237">Limites de Data Factory</span><span class="sxs-lookup"><span data-stu-id="3a12f-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="3a12f-238">Limites Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3a12f-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="3a12f-239">Limite Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3a12f-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="3a12f-240">Limites Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3a12f-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="3a12f-241">Limites d'Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a12f-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="3a12f-242">Limites d’Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="3a12f-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="3a12f-243">Limites Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3a12f-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="3a12f-244">Limites du système StorSimple</span><span class="sxs-lookup"><span data-stu-id="3a12f-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="3a12f-245">Limites de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3a12f-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="3a12f-246">Limites Azure Backup</span><span class="sxs-lookup"><span data-stu-id="3a12f-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="3a12f-247">Limites Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="3a12f-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="3a12f-248">Limites d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="3a12f-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="3a12f-249">Limites Gestion des API</span><span class="sxs-lookup"><span data-stu-id="3a12f-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="3a12f-250">Limite du service Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="3a12f-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="3a12f-251">Limites du coffre de clés</span><span class="sxs-lookup"><span data-stu-id="3a12f-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="3a12f-252">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3a12f-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="3a12f-253">Limites du service Automation</span><span class="sxs-lookup"><span data-stu-id="3a12f-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="3a12f-254">Limites de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="3a12f-254">SQL Database limits</span></span>
<span data-ttu-id="3a12f-255">Pour connaître les limites de la base de données SQL, consultez [Limites de ressources de base de données SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="3a12f-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3a12f-256">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3a12f-256">See also</span></span>
[<span data-ttu-id="3a12f-257">Présentation des limites et des augmentations Azure</span><span class="sxs-lookup"><span data-stu-id="3a12f-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="3a12f-258">Tailles de machines virtuelles et services cloud pour Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3a12f-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="3a12f-259">Tailles de services cloud</span><span class="sxs-lookup"><span data-stu-id="3a12f-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

