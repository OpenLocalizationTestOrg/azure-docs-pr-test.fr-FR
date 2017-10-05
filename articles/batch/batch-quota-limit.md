---
title: Quotas et limites du service Azure Batch | Microsoft Docs
description: "En savoir plus sur les contraintes, les limites et les quotas par défaut d’Azure Batch, et comment demander une augmentation de quota"
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="0cef7-103">Quotas et limites du service Batch</span><span class="sxs-lookup"><span data-stu-id="0cef7-103">Batch service quotas and limits</span></span>

<span data-ttu-id="0cef7-104">Comme avec d’autres services Azure, il existe des limites concernant certaines ressources associées au service Batch.</span><span class="sxs-lookup"><span data-stu-id="0cef7-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="0cef7-105">La plupart de ces limites représentent des quotas par défaut appliqués par Azure au niveau de l’abonnement ou du compte.</span><span class="sxs-lookup"><span data-stu-id="0cef7-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="0cef7-106">Cet article décrit ces paramètres par défaut, et comment vous pouvez demander une augmentation de ces quotas.</span><span class="sxs-lookup"><span data-stu-id="0cef7-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="0cef7-107">Gardez ces quotas à l’esprit lorsque vous concevez et mettez à l’échelle vos charges de travail Batch.</span><span class="sxs-lookup"><span data-stu-id="0cef7-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="0cef7-108">Par exemple, si votre pool n’atteint pas le nombre de nœuds de calcul que vous avez spécifiés, il se peut que vous ayez atteint le quota limite de votre compte Batch ou un quota de cœurs de machine virtuelle régionaux pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cef7-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="0cef7-109">Vous pouvez exécuter plusieurs charges de travail Batch dans un compte Batch ou répartir vos charges de travail entre plusieurs comptes Batch se trouvant dans le même abonnement mais dans différentes régions Azure.</span><span class="sxs-lookup"><span data-stu-id="0cef7-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="0cef7-110">Si vous envisagez d’exécuter des charges de travail de production dans Batch, vous devrez peut-être affecter à un ou plusieurs des quotas une valeur supérieure à la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="0cef7-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="0cef7-111">Si vous souhaitez augmenter un quota, vous pouvez ouvrir une [demande de service clientèle](#increase-a-quota) en ligne gratuitement.</span><span class="sxs-lookup"><span data-stu-id="0cef7-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="0cef7-112">Un quota est une limite de crédit, pas une garantie de capacité.</span><span class="sxs-lookup"><span data-stu-id="0cef7-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="0cef7-113">Si vous avez des besoins de capacité à grande échelle, contactez le support Azure.</span><span class="sxs-lookup"><span data-stu-id="0cef7-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="0cef7-114">Quotas de ressources</span><span class="sxs-lookup"><span data-stu-id="0cef7-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="0cef7-115">Quotas en mode Abonnement utilisateur</span><span class="sxs-lookup"><span data-stu-id="0cef7-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="0cef7-116">Pour un compte Batch en mode d’allocation de pool défini sur **abonnement utilisateur**, les machines virtuelle Batch et les autres ressources, telles que les comptes de stockage, sont créées directement dans votre abonnement lors de la création d’un pool.</span><span class="sxs-lookup"><span data-stu-id="0cef7-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="0cef7-117">Le quota de cœurs Azure Batch ne s’applique pas à un compte créé dans ce mode.</span><span class="sxs-lookup"><span data-stu-id="0cef7-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="0cef7-118">Seuls s’appliquent les quotas de votre abonnement imposés aux cœurs de calcul régionaux et aux autres ressources.</span><span class="sxs-lookup"><span data-stu-id="0cef7-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="0cef7-119">Pour en savoir plus sur ces quotas, consultez [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0cef7-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="0cef7-120">Lorsque vous planifiez l’utilisation des ressources pour un compte créé en mode Abonnement utilisateur, notez que les ressources Batch suivantes (en plus des cœurs de calcul) sont requises pour toute tranche de 40 machines virtuelles Linux ou de 20 machines virtuelles Windows :</span><span class="sxs-lookup"><span data-stu-id="0cef7-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="0cef7-121">Ressource</span><span class="sxs-lookup"><span data-stu-id="0cef7-121">Resource</span></span> | <span data-ttu-id="0cef7-122">Quota</span><span class="sxs-lookup"><span data-stu-id="0cef7-122">Quota</span></span> | <span data-ttu-id="0cef7-123">Fournisseur</span><span class="sxs-lookup"><span data-stu-id="0cef7-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="0cef7-124">Un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0cef7-124">One storage account</span></span> | <span data-ttu-id="0cef7-125">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="0cef7-125">Storage Accounts</span></span> | <span data-ttu-id="0cef7-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="0cef7-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="0cef7-127">Une seule adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="0cef7-127">One public IP address</span></span> | <span data-ttu-id="0cef7-128">Adresses IP publiques</span><span class="sxs-lookup"><span data-stu-id="0cef7-128">Public IP Addresses</span></span> | <span data-ttu-id="0cef7-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="0cef7-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="0cef7-130">Un seul réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="0cef7-130">One virtual network</span></span> | <span data-ttu-id="0cef7-131">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="0cef7-131">Virtual Networks</span></span> | <span data-ttu-id="0cef7-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="0cef7-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="0cef7-133">Un seul groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="0cef7-133">One network security group</span></span> | <span data-ttu-id="0cef7-134">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="0cef7-134">Network Security Groups</span></span> | <span data-ttu-id="0cef7-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="0cef7-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="0cef7-136">Un seul jeu de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0cef7-136">One virtual machine scale set</span></span> | <span data-ttu-id="0cef7-137">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0cef7-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="0cef7-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="0cef7-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="0cef7-139">Un seul équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="0cef7-139">One load balancer</span></span> | <span data-ttu-id="0cef7-140">Équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="0cef7-140">Load Balancers</span></span> | <span data-ttu-id="0cef7-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="0cef7-141">Microsoft.Network</span></span> | 

<span data-ttu-id="0cef7-142">Le quota de cœurs au niveau régional ou par famille de machine virtuelle doit être défini en fonction de la taille de machine virtuelle nécessaire pour votre ou vos pool(s) Batch :</span><span class="sxs-lookup"><span data-stu-id="0cef7-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="0cef7-143">Quota</span><span class="sxs-lookup"><span data-stu-id="0cef7-143">Quota</span></span> | <span data-ttu-id="0cef7-144">Fournisseur</span><span class="sxs-lookup"><span data-stu-id="0cef7-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="0cef7-145">Nombre total de cœurs régionaux</span><span class="sxs-lookup"><span data-stu-id="0cef7-145">Total Regional Cores</span></span> | <span data-ttu-id="0cef7-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="0cef7-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="0cef7-147">…</span><span class="sxs-lookup"><span data-stu-id="0cef7-147">…</span></span> <span data-ttu-id="0cef7-148">Cœurs de famille</span><span class="sxs-lookup"><span data-stu-id="0cef7-148">Family Cores</span></span> | <span data-ttu-id="0cef7-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="0cef7-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="0cef7-150">Autres limites</span><span class="sxs-lookup"><span data-stu-id="0cef7-150">Other limits</span></span>
| <span data-ttu-id="0cef7-151">**Ressource**</span><span class="sxs-lookup"><span data-stu-id="0cef7-151">**Resource**</span></span> | <span data-ttu-id="0cef7-152">**Limite maximale**</span><span class="sxs-lookup"><span data-stu-id="0cef7-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="0cef7-153">[Tâches simultanées](batch-parallel-node-tasks.md) par nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="0cef7-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="0cef7-154">4 x nombre de cœurs de nœud</span><span class="sxs-lookup"><span data-stu-id="0cef7-154">4 x number of node cores</span></span> |
| <span data-ttu-id="0cef7-155">[Applications](batch-application-packages.md) par compte Batch</span><span class="sxs-lookup"><span data-stu-id="0cef7-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="0cef7-156">20</span><span class="sxs-lookup"><span data-stu-id="0cef7-156">20</span></span> |
| <span data-ttu-id="0cef7-157">Packages d’applications par application</span><span class="sxs-lookup"><span data-stu-id="0cef7-157">Application packages per application</span></span> |<span data-ttu-id="0cef7-158">40</span><span class="sxs-lookup"><span data-stu-id="0cef7-158">40</span></span> |
| <span data-ttu-id="0cef7-159">Taille de package d’application (individuel)</span><span class="sxs-lookup"><span data-stu-id="0cef7-159">Application package size (each)</span></span> |<span data-ttu-id="0cef7-160">Environ 195 Go<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0cef7-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="0cef7-161">Taille maximale de la tâche de début</span><span class="sxs-lookup"><span data-stu-id="0cef7-161">Maximum start task size</span></span> | <span data-ttu-id="0cef7-162">32 768 caractères<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="0cef7-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="0cef7-163"><sup>1</sup> Limite Azure Storage pour la taille d’objet blob de blocs maximale</span><span class="sxs-lookup"><span data-stu-id="0cef7-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="0cef7-164">
<sup>2</sup> inclut les fichiers de ressources et les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="0cef7-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="0cef7-165">Afficher les quotas Batch</span><span class="sxs-lookup"><span data-stu-id="0cef7-165">View Batch quotas</span></span>
<span data-ttu-id="0cef7-166">Affichez vos quotas de compte Batch dans le [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="0cef7-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="0cef7-167">Sélectionnez **Comptes Batch** dans le portail, puis sélectionnez le compte Batch qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="0cef7-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="0cef7-168">Sélectionnez **Propriétés** dans le panneau de menu du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="0cef7-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="0cef7-169">Le panneau Propriétés affiche les **quotas** actuellement appliqués au compte Batch</span><span class="sxs-lookup"><span data-stu-id="0cef7-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Quotas de compte Batch][account_quotas]

<span data-ttu-id="0cef7-171">Pour un compte Batch créé en mode Abonnement utilisateur, affichez les quotas d’abonnement associés dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0cef7-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="0cef7-172">Sélectionnez **Abonnements**, puis sélectionnez l’abonnement que vous utilisez pour le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="0cef7-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="0cef7-173">Dans le panneau **Abonnement**, sélectionnez **Utilisation + quotas**.</span><span class="sxs-lookup"><span data-stu-id="0cef7-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="0cef7-174">Augmenter un quota</span><span class="sxs-lookup"><span data-stu-id="0cef7-174">Increase a quota</span></span>
<span data-ttu-id="0cef7-175">Suivez ces étapes pour demander une augmentation de quota pour votre compte Batch ou votre abonnement à l’aide du [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="0cef7-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="0cef7-176">Le type d’augmentation de quota varie selon le mode d’allocation de pool de votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="0cef7-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="0cef7-177">Augmenter un quota de cœurs Batch</span><span class="sxs-lookup"><span data-stu-id="0cef7-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="0cef7-178">Si votre compte Batch a été créé en mode **Service Batch**, suivez ces étapes pour demander une augmentation du quota de cœurs Batch :</span><span class="sxs-lookup"><span data-stu-id="0cef7-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="0cef7-179">Sélectionnez la mosaïque **Aide + Support** dans le tableau de bord du portail, ou le point d’interrogation (**?**) dans le coin supérieur droit du portail.</span><span class="sxs-lookup"><span data-stu-id="0cef7-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="0cef7-180">Sélectionnez **Nouvelle demande de support** > **De base**.</span><span class="sxs-lookup"><span data-stu-id="0cef7-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="0cef7-181">Sur le panneau **De base** :</span><span class="sxs-lookup"><span data-stu-id="0cef7-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="0cef7-182">a.</span><span class="sxs-lookup"><span data-stu-id="0cef7-182">a.</span></span> <span data-ttu-id="0cef7-183">**Type de problème** > **Quota**</span><span class="sxs-lookup"><span data-stu-id="0cef7-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="0cef7-184">b.</span><span class="sxs-lookup"><span data-stu-id="0cef7-184">b.</span></span> <span data-ttu-id="0cef7-185">Sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cef7-185">Select your subscription.</span></span>
   
    <span data-ttu-id="0cef7-186">c.</span><span class="sxs-lookup"><span data-stu-id="0cef7-186">c.</span></span> <span data-ttu-id="0cef7-187">**Type de quota** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="0cef7-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="0cef7-188">d.</span><span class="sxs-lookup"><span data-stu-id="0cef7-188">d.</span></span> <span data-ttu-id="0cef7-189">**Plan de support** > **Support quota - Inclus**</span><span class="sxs-lookup"><span data-stu-id="0cef7-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="0cef7-190">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0cef7-190">Click **Next**.</span></span>
4. <span data-ttu-id="0cef7-191">Sur le panneau **Problème** :</span><span class="sxs-lookup"><span data-stu-id="0cef7-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="0cef7-192">a.</span><span class="sxs-lookup"><span data-stu-id="0cef7-192">a.</span></span> <span data-ttu-id="0cef7-193">Sélectionnez un **niveau de gravité** en fonction de [l’impact sur votre activité][support_sev].</span><span class="sxs-lookup"><span data-stu-id="0cef7-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="0cef7-194">b.</span><span class="sxs-lookup"><span data-stu-id="0cef7-194">b.</span></span> <span data-ttu-id="0cef7-195">Dans **Détails**, spécifiez chaque quota que vous souhaitez modifier, le nom du compte Batch et la nouvelle limite.</span><span class="sxs-lookup"><span data-stu-id="0cef7-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="0cef7-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0cef7-196">Click **Next**.</span></span>
5. <span data-ttu-id="0cef7-197">Sur le panneau **Informations de contact** :</span><span class="sxs-lookup"><span data-stu-id="0cef7-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="0cef7-198">a.</span><span class="sxs-lookup"><span data-stu-id="0cef7-198">a.</span></span> <span data-ttu-id="0cef7-199">Sélectionnez une **méthode de contact préférée**.</span><span class="sxs-lookup"><span data-stu-id="0cef7-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="0cef7-200">b.</span><span class="sxs-lookup"><span data-stu-id="0cef7-200">b.</span></span> <span data-ttu-id="0cef7-201">Vérifiez et entrez les informations de contact requises.</span><span class="sxs-lookup"><span data-stu-id="0cef7-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="0cef7-202">Cliquez sur **Créer** pour envoyer la demande de support.</span><span class="sxs-lookup"><span data-stu-id="0cef7-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="0cef7-203">Une fois que vous avez envoyé votre demande de support, le support Azure vous contactera.</span><span class="sxs-lookup"><span data-stu-id="0cef7-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="0cef7-204">Notez que le traitement de la demande peut prendre jusqu’à 2 jours ouvrés.</span><span class="sxs-lookup"><span data-stu-id="0cef7-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="0cef7-205">Augmenter un quota de cœurs d’abonnement</span><span class="sxs-lookup"><span data-stu-id="0cef7-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="0cef7-206">Si votre compte Batch a été créé en mode **Abonnement utilisateur** et si vous avez besoin de cœurs régionaux ou cœurs de familles de machine virtuelles supplémentaires, demandez une augmentation de quota dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cef7-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="0cef7-207">Pour connaître la procédure, consultez [Demandes d’augmentation du quota de base d’Azure Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="0cef7-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="0cef7-208">Rubriques connexes</span><span class="sxs-lookup"><span data-stu-id="0cef7-208">Related topics</span></span>
* [<span data-ttu-id="0cef7-209">Création et gestion d’un compte Azure Batch dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0cef7-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="0cef7-210">Vue d'ensemble des fonctionnalités d'Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0cef7-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="0cef7-211">Abonnement Azure et limites, quotas et contraintes de service</span><span class="sxs-lookup"><span data-stu-id="0cef7-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
