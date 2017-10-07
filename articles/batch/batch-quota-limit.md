---
title: aaaService quotas et limites pour le traitement par lots Azure | Documents Microsoft
description: "En savoir plus sur les quotas Azure Batch par défaut, les limites et les contraintes, et comment toorequest quota augmente"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="8453c-103">Quotas et limites du service Batch</span><span class="sxs-lookup"><span data-stu-id="8453c-103">Batch service quotas and limits</span></span>

<span data-ttu-id="8453c-104">Comme avec d’autres services Azure, il existe des limites sur certaines ressources associées hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="8453c-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="8453c-105">La plupart de ces limites sont des quotas par défaut appliqués par Azure à l’abonnement de hello ou au niveau du compte.</span><span class="sxs-lookup"><span data-stu-id="8453c-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="8453c-106">Cet article décrit ces paramètres par défaut, et comment vous pouvez demander une augmentation de ces quotas.</span><span class="sxs-lookup"><span data-stu-id="8453c-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="8453c-107">Gardez ces quotas à l’esprit lorsque vous concevez et mettez à l’échelle vos charges de travail Batch.</span><span class="sxs-lookup"><span data-stu-id="8453c-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="8453c-108">Par exemple, si votre pool n’est pas atteindre le nombre de cibles de hello de nœuds de calcul que vous avez spécifié, vous pourrez avoir atteint limite du quota de cœurs hello pour votre compte Batch ou d’un quota de cœurs de machine virtuelle régional pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8453c-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="8453c-109">Vous pouvez exécuter plusieurs charges de travail de traitement par lots dans un seul compte de traitement par lots, ou distribuer vos charges de travail entre les comptes de traitement par lots qui se trouvent hello même abonnement, mais dans différentes régions Azure.</span><span class="sxs-lookup"><span data-stu-id="8453c-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="8453c-110">Si vous envisagez des charges de production toorun dans un lot, vous devrez peut-être tooincrease une ou plusieurs des quotas hello ci-dessus par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="8453c-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="8453c-111">Si vous voulez tooraise un quota, vous pouvez ouvrir un en ligne [demande de support client](#increase-a-quota) sans frais.</span><span class="sxs-lookup"><span data-stu-id="8453c-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="8453c-112">Un quota est une limite de crédit, pas une garantie de capacité.</span><span class="sxs-lookup"><span data-stu-id="8453c-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="8453c-113">Si vous avez des besoins de capacité à grande échelle, contactez le support Azure.</span><span class="sxs-lookup"><span data-stu-id="8453c-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="8453c-114">Quotas de ressources</span><span class="sxs-lookup"><span data-stu-id="8453c-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="8453c-115">Quotas en mode Abonnement utilisateur</span><span class="sxs-lookup"><span data-stu-id="8453c-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="8453c-116">Pour un compte de traitement lorsque le mode d’allocation de pool défini trop**abonnement utilisateur**, ordinateurs virtuels et autres ressources, telles que les comptes de stockage du lot, sont créés directement dans votre abonnement lorsqu’un pool est créé.</span><span class="sxs-lookup"><span data-stu-id="8453c-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="8453c-117">quota de cœurs de traitement par lots Azure Hello n’applique pas de compte tooan créé dans ce mode.</span><span class="sxs-lookup"><span data-stu-id="8453c-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="8453c-118">Au lieu de cela, les quotas hello dans votre abonnement pour les cœurs de calcul régional et d’autres ressources sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="8453c-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="8453c-119">Pour en savoir plus sur ces quotas, consultez [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="8453c-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="8453c-120">Lorsque vous planifiez l’utilisation des ressources pour un compte créé dans le mode d’abonnement utilisateur, hello Remarque suivant des ressources de lot (dans les cœurs de toocompute ajout) sont requis pour toutes les machines virtuelles Linux 40 ou 20 ordinateurs virtuels de Windows :</span><span class="sxs-lookup"><span data-stu-id="8453c-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="8453c-121">Ressource</span><span class="sxs-lookup"><span data-stu-id="8453c-121">Resource</span></span> | <span data-ttu-id="8453c-122">Quota</span><span class="sxs-lookup"><span data-stu-id="8453c-122">Quota</span></span> | <span data-ttu-id="8453c-123">Fournisseur</span><span class="sxs-lookup"><span data-stu-id="8453c-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="8453c-124">Un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8453c-124">One storage account</span></span> | <span data-ttu-id="8453c-125">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="8453c-125">Storage Accounts</span></span> | <span data-ttu-id="8453c-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="8453c-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="8453c-127">Une seule adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="8453c-127">One public IP address</span></span> | <span data-ttu-id="8453c-128">Adresses IP publiques</span><span class="sxs-lookup"><span data-stu-id="8453c-128">Public IP Addresses</span></span> | <span data-ttu-id="8453c-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="8453c-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="8453c-130">Un seul réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="8453c-130">One virtual network</span></span> | <span data-ttu-id="8453c-131">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="8453c-131">Virtual Networks</span></span> | <span data-ttu-id="8453c-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="8453c-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="8453c-133">Un seul groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8453c-133">One network security group</span></span> | <span data-ttu-id="8453c-134">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8453c-134">Network Security Groups</span></span> | <span data-ttu-id="8453c-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="8453c-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="8453c-136">Un seul jeu de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8453c-136">One virtual machine scale set</span></span> | <span data-ttu-id="8453c-137">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8453c-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="8453c-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="8453c-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="8453c-139">Un seul équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="8453c-139">One load balancer</span></span> | <span data-ttu-id="8453c-140">Équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="8453c-140">Load Balancers</span></span> | <span data-ttu-id="8453c-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="8453c-141">Microsoft.Network</span></span> | 

<span data-ttu-id="8453c-142">quota de cœurs Hello au niveau régional ou par famille de machine virtuelle doit être ensemble conséquente toohello taille de machine virtuelle requis pour votre pool de traitement par lots ou des pools :</span><span class="sxs-lookup"><span data-stu-id="8453c-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="8453c-143">Quota</span><span class="sxs-lookup"><span data-stu-id="8453c-143">Quota</span></span> | <span data-ttu-id="8453c-144">Fournisseur</span><span class="sxs-lookup"><span data-stu-id="8453c-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="8453c-145">Nombre total de cœurs régionaux</span><span class="sxs-lookup"><span data-stu-id="8453c-145">Total Regional Cores</span></span> | <span data-ttu-id="8453c-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="8453c-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="8453c-147">…</span><span class="sxs-lookup"><span data-stu-id="8453c-147">…</span></span> <span data-ttu-id="8453c-148">Cœurs de famille</span><span class="sxs-lookup"><span data-stu-id="8453c-148">Family Cores</span></span> | <span data-ttu-id="8453c-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="8453c-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="8453c-150">Autres limites</span><span class="sxs-lookup"><span data-stu-id="8453c-150">Other limits</span></span>
| <span data-ttu-id="8453c-151">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="8453c-151">**Resource**</span></span> | <span data-ttu-id="8453c-152">**Limite maximale**</span><span class="sxs-lookup"><span data-stu-id="8453c-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="8453c-153">[Tâches simultanées](batch-parallel-node-tasks.md) par nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="8453c-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="8453c-154">4 x nombre de cœurs de nœud</span><span class="sxs-lookup"><span data-stu-id="8453c-154">4 x number of node cores</span></span> |
| <span data-ttu-id="8453c-155">[Applications](batch-application-packages.md) par compte Batch</span><span class="sxs-lookup"><span data-stu-id="8453c-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="8453c-156">20</span><span class="sxs-lookup"><span data-stu-id="8453c-156">20</span></span> |
| <span data-ttu-id="8453c-157">Packages d’applications par application</span><span class="sxs-lookup"><span data-stu-id="8453c-157">Application packages per application</span></span> |<span data-ttu-id="8453c-158">40</span><span class="sxs-lookup"><span data-stu-id="8453c-158">40</span></span> |
| <span data-ttu-id="8453c-159">Taille de package d’application (individuel)</span><span class="sxs-lookup"><span data-stu-id="8453c-159">Application package size (each)</span></span> |<span data-ttu-id="8453c-160">Environ 195 Go<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="8453c-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="8453c-161">Taille maximale de la tâche de début</span><span class="sxs-lookup"><span data-stu-id="8453c-161">Maximum start task size</span></span> | <span data-ttu-id="8453c-162">32 768 caractères<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="8453c-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="8453c-163"><sup>1</sup> Limite Azure Storage pour la taille d’objet blob de blocs maximale</span><span class="sxs-lookup"><span data-stu-id="8453c-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="8453c-164">
<sup>2</sup> inclut les fichiers de ressources et les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="8453c-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="8453c-165">Afficher les quotas Batch</span><span class="sxs-lookup"><span data-stu-id="8453c-165">View Batch quotas</span></span>
<span data-ttu-id="8453c-166">Afficher les quotas de compte de votre lot Bonjour [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="8453c-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="8453c-167">Sélectionnez **comptes du lot** dans hello portail, puis sélectionnez du compte Batch hello vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="8453c-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="8453c-168">Sélectionnez **propriétés** sur le panneau de menu du compte de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="8453c-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="8453c-169">panneau des propriétés Hello affiche hello **quotas** actuellement appliqué toohello du compte Batch</span><span class="sxs-lookup"><span data-stu-id="8453c-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Quotas de compte Batch][account_quotas]

<span data-ttu-id="8453c-171">Pour un compte de traitement par lots créé en mode d’abonnement utilisateur, hello de vue liée quotas d’abonnement Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8453c-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="8453c-172">Sélectionnez **abonnements**, puis sélectionnez l’abonnement hello que vous utilisez pour hello compte Batch.</span><span class="sxs-lookup"><span data-stu-id="8453c-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="8453c-173">Sur hello **abonnement** panneau, sélectionnez **utilisation + quotas**.</span><span class="sxs-lookup"><span data-stu-id="8453c-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="8453c-174">Augmenter un quota</span><span class="sxs-lookup"><span data-stu-id="8453c-174">Increase a quota</span></span>
<span data-ttu-id="8453c-175">Suivez ces toorequest étapes augmenter d’un quota de votre compte de traitement par lots ou de votre abonnement à l’aide de hello [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="8453c-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="8453c-176">type Hello d’augmentation du quota dépend du mode d’allocation de pool hello de votre compte de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="8453c-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="8453c-177">Augmenter un quota de cœurs Batch</span><span class="sxs-lookup"><span data-stu-id="8453c-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="8453c-178">Si votre compte Batch a été créé dans **lot service** mode, suivez ces étapes de toorequest une augmentation du quota de cœurs par lots :</span><span class="sxs-lookup"><span data-stu-id="8453c-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="8453c-179">Sélectionnez hello **aide + support** vignette sur votre tableau de bord de portail, ou hello point d’interrogation (**?**) dans le coin supérieur droit de hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="8453c-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="8453c-180">Sélectionnez **Nouvelle demande de support** > **De base**.</span><span class="sxs-lookup"><span data-stu-id="8453c-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="8453c-181">Sur hello **notions de base** panneau :</span><span class="sxs-lookup"><span data-stu-id="8453c-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="8453c-182">a.</span><span class="sxs-lookup"><span data-stu-id="8453c-182">a.</span></span> <span data-ttu-id="8453c-183">**Type de problème** > **Quota**</span><span class="sxs-lookup"><span data-stu-id="8453c-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="8453c-184">b.</span><span class="sxs-lookup"><span data-stu-id="8453c-184">b.</span></span> <span data-ttu-id="8453c-185">Sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8453c-185">Select your subscription.</span></span>
   
    <span data-ttu-id="8453c-186">c.</span><span class="sxs-lookup"><span data-stu-id="8453c-186">c.</span></span> <span data-ttu-id="8453c-187">**Type de quota** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="8453c-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="8453c-188">d.</span><span class="sxs-lookup"><span data-stu-id="8453c-188">d.</span></span> <span data-ttu-id="8453c-189">**Plan de support** > **Support quota - Inclus**</span><span class="sxs-lookup"><span data-stu-id="8453c-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="8453c-190">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8453c-190">Click **Next**.</span></span>
4. <span data-ttu-id="8453c-191">Sur hello **problème** panneau :</span><span class="sxs-lookup"><span data-stu-id="8453c-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="8453c-192">a.</span><span class="sxs-lookup"><span data-stu-id="8453c-192">a.</span></span> <span data-ttu-id="8453c-193">Sélectionnez un **gravité** selon tooyour [impact commercial][support_sev].</span><span class="sxs-lookup"><span data-stu-id="8453c-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="8453c-194">b.</span><span class="sxs-lookup"><span data-stu-id="8453c-194">b.</span></span> <span data-ttu-id="8453c-195">Dans **détails**, spécifiez chaque quota que vous voulez toochange, nom du compte Batch hello et nouvelle limite de hello.</span><span class="sxs-lookup"><span data-stu-id="8453c-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="8453c-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8453c-196">Click **Next**.</span></span>
5. <span data-ttu-id="8453c-197">Sur hello **les informations de Contact** panneau :</span><span class="sxs-lookup"><span data-stu-id="8453c-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="8453c-198">a.</span><span class="sxs-lookup"><span data-stu-id="8453c-198">a.</span></span> <span data-ttu-id="8453c-199">Sélectionnez une **méthode de contact préférée**.</span><span class="sxs-lookup"><span data-stu-id="8453c-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="8453c-200">b.</span><span class="sxs-lookup"><span data-stu-id="8453c-200">b.</span></span> <span data-ttu-id="8453c-201">Vérifier et entrez les détails du contact hello requis.</span><span class="sxs-lookup"><span data-stu-id="8453c-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="8453c-202">Cliquez sur **créer** toosubmit hello prise en charge de demande.</span><span class="sxs-lookup"><span data-stu-id="8453c-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="8453c-203">Une fois que vous avez envoyé votre demande de support, le support Azure vous contactera.</span><span class="sxs-lookup"><span data-stu-id="8453c-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="8453c-204">Notez que la fin de la demande de hello peut prendre jusqu'à too2 prochains jours ouvrables.</span><span class="sxs-lookup"><span data-stu-id="8453c-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="8453c-205">Augmenter un quota de cœurs d’abonnement</span><span class="sxs-lookup"><span data-stu-id="8453c-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="8453c-206">Si votre compte Batch a été créé en mode **Abonnement utilisateur** et si vous avez besoin de cœurs régionaux ou cœurs de familles de machine virtuelles supplémentaires, demandez une augmentation de quota dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8453c-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="8453c-207">Pour connaître la procédure, consultez [Demandes d’augmentation du quota de base d’Azure Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="8453c-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="8453c-208">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="8453c-208">Related topics</span></span>
* [<span data-ttu-id="8453c-209">Créer un compte Azure Batch hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8453c-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="8453c-210">Vue d'ensemble des fonctionnalités d'Azure Batch</span><span class="sxs-lookup"><span data-stu-id="8453c-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="8453c-211">Abonnement Azure et limites, quotas et contraintes de service</span><span class="sxs-lookup"><span data-stu-id="8453c-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
