---
title: "Protéger votre API avec Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment protéger votre API avec les quotas et les stratégies (limite de débit) de limitation."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 5553bcb8f9fd38630f694151dc644a684266387c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="1e072-103">Protéger votre API avec des limites de débit à l’aide de la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="1e072-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="1e072-104">Ce guide vous montre combien il est facile d’ajouter une protection à votre API principale en configurant des limites de débit et des stratégies de quota avec la gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="1e072-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="1e072-105">Dans ce didacticiel, vous allez créer une version d’évaluation gratuite d’un produit API qui permet aux développeurs de passer jusqu’à 10 appels par minute dans la limite de 200 appels par semaine vers votre API en utilisant les stratégies consistant à [Limiter la fréquence des appels par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et à [Définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="1e072-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="1e072-106">Vous pourrez ensuite publier l’API et tester la stratégie de limite de débit</span><span class="sxs-lookup"><span data-stu-id="1e072-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="1e072-107">Pour consulter des scénarios de limitation plus avancés utilisant les stratégies [limiter-fréquence-par-clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [quota-par-clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey), consultez l’article [Limitation de requêtes avancée avec la gestion des API Azure](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="1e072-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="1e072-108"><a name="create-product"> </a>Pour créer un produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="1e072-109">Dans cette étape, vous allez créer un produit en version d’évaluation gratuite, qui ne requiert aucune approbation d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e072-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="1e072-110">Si vous disposez déjà d’un produit configuré et que vous souhaitez l’utiliser pour ce didacticiel, vous pouvez passer directement à la rubrique [Configuration de la limite de débit d’appels et des stratégies de quota][Configure call rate limit and quota policies] et suivre le didacticiel à partir de là, en utilisant votre produit à la place de celui en version d’évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="1e072-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="1e072-111">Pour commencer, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="1e072-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="1e072-113">Si vous n’avez pas encore créé d’instance de service Gestion des API, consultez la page [Création d'une instance du service API Management][Create an API Management service instance] dans le didacticiel [Gérer votre première API dans Gestion des API Azure][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1e072-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="1e072-114">Cliquez sur **Produits** dans le menu **Gestion des API** sur la gauche pour afficher la page **Produits**.</span><span class="sxs-lookup"><span data-stu-id="1e072-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="1e072-116">Cliquez sur **Ajouter un produit** pour afficher la boîte de dialogue **Ajouter un nouveau produit**.</span><span class="sxs-lookup"><span data-stu-id="1e072-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![Ajouter un nouveau produit][api-management-new-product-window]

<span data-ttu-id="1e072-118">Dans la zone **Titre**, saisissez **Version d’évaluation gratuite**.</span><span class="sxs-lookup"><span data-stu-id="1e072-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="1e072-119">Dans la zone **Description**, saisissez le texte suivant : **Les abonnés pourront effectuer 10 appels/minute jusqu’à un maximum de 200 appels/semaine, après lesquels l’accès est refusé.**</span><span class="sxs-lookup"><span data-stu-id="1e072-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="1e072-120">Les produits de Gestion des API peuvent être protégés ou ouverts.</span><span class="sxs-lookup"><span data-stu-id="1e072-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="1e072-121">Pour pouvoir utiliser les produits protégés, vous devez vous y abonner au préalable.</span><span class="sxs-lookup"><span data-stu-id="1e072-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="1e072-122">Les produits ouverts sont utilisables sans abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e072-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="1e072-123">Vérifiez que la case à cocher **Require subscription (Abonnement obligatoire)** est activée afin de créer un produit protégé qui requiert un abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e072-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="1e072-124">Il s’agit du paramètre par défaut.</span><span class="sxs-lookup"><span data-stu-id="1e072-124">This is the default setting.</span></span>

<span data-ttu-id="1e072-125">Si vous souhaitez qu’un administrateur vérifie et accepte ou refuse les tentatives d’abonnement à ce produit, sélectionnez **Require subscription approval (Approbation d'abonnement obligatoire)**.</span><span class="sxs-lookup"><span data-stu-id="1e072-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="1e072-126">Si la case à cocher n’est pas activée, les tentatives d’abonnement sont approuvées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="1e072-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="1e072-127">Dans cet exemple, les abonnements sont approuvés automatiquement. Donc, inutile d’activer la case à cocher.</span><span class="sxs-lookup"><span data-stu-id="1e072-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="1e072-128">Pour autoriser les comptes de développeur à s’abonner plusieurs fois au nouveau produit, activez la case à cocher **Allow multiple simultaneous subscriptions (Autoriser plusieurs abonnements simultanés)**.</span><span class="sxs-lookup"><span data-stu-id="1e072-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="1e072-129">Ce didacticiel ne nécessite pas l’utilisation de plusieurs abonnements simultanés. Vous pouvez donc laisser cette case décochée.</span><span class="sxs-lookup"><span data-stu-id="1e072-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="1e072-130">Une fois toutes les valeurs saisies, cliquez sur **Enregistrer** pour créer le produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-130">After all values are entered, click **Save** to create the product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="1e072-132">Par défaut, les nouveaux produits sont visibles pour les utilisateurs dans le groupe **Administrateurs** .</span><span class="sxs-lookup"><span data-stu-id="1e072-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="1e072-133">Nous allons ajouter le groupe **Développeurs** .</span><span class="sxs-lookup"><span data-stu-id="1e072-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="1e072-134">Cliquez sur **Version d’évaluation gratuite**, puis sur l’onglet **Visibilité**.</span><span class="sxs-lookup"><span data-stu-id="1e072-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="1e072-135">Dans Gestion des API, les groupes permettent de gérer la visibilité des produits pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="1e072-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="1e072-136">Les produits accordent de la visibilité aux groupes. Les développeurs peuvent afficher les produits visibles pour les groupes auxquels ils appartiennent et s'y abonner.</span><span class="sxs-lookup"><span data-stu-id="1e072-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="1e072-137">Pour plus d'informations, consultez la page [Création et utilisation de groupes dans Gestion des API Azure][How to create and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1e072-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="1e072-139">Activez la case à cocher **Développeurs**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1e072-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="1e072-140"><a name="add-api"> </a>Ajout d’une API au produit</span><span class="sxs-lookup"><span data-stu-id="1e072-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="1e072-141">Dans cette étape du didacticiel, nous allons ajouter l'API Echo au nouveau produit en version d'évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="1e072-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="1e072-142">Chaque instance du service Gestion des API est pré-configurée avec une API Echo qui peut être utilisée pour faire des expériences et en savoir plus sur la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="1e072-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="1e072-143">Pour plus d’informations, consultez [Gérer votre première API dans Gestion des API Azure][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1e072-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="1e072-144">Cliquez sur **Produits** dans le menu **Gestion des API** sur la gauche, puis cliquez sur **Version d’évaluation gratuite** pour configurer le produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="1e072-146">Cliquez sur **Ajouter l'API au produit**.</span><span class="sxs-lookup"><span data-stu-id="1e072-146">Click **Add API to product**.</span></span>

![Ajouter l'API au produit][api-management-add-api]

<span data-ttu-id="1e072-148">Sélectionnez **API Echo**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1e072-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="1e072-150"><a name="policies"> </a>Configuration de la limite de débit d’appels et des stratégies de quota</span><span class="sxs-lookup"><span data-stu-id="1e072-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="1e072-151">Les limites de débit et les quotas sont configurés dans l'éditeur de stratégie.</span><span class="sxs-lookup"><span data-stu-id="1e072-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="1e072-152">Les deux stratégies que nous ajouterons dans ce didacticiel sont les stratégies [Limiter la fréquence des appels par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [Définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="1e072-152">The two policies we will be adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="1e072-153">Elles doivent être appliquées dans l’étendue du produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-153">These policies must be applied at the product scope.</span></span>

<span data-ttu-id="1e072-154">Cliquez sur **Stratégies** sous le menu **Gestion des API** sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="1e072-154">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="1e072-155">Dans la liste **Produit** cliquez sur **Version d’évaluation gratuite**.</span><span class="sxs-lookup"><span data-stu-id="1e072-155">In the **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="1e072-157">Cliquez sur **Ajouter une stratégie** pour importer le modèle de stratégie et commencer à créer la limite de débit et les stratégies de quota.</span><span class="sxs-lookup"><span data-stu-id="1e072-157">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![Add policy][api-management-add-policy]

<span data-ttu-id="1e072-159">La limite de débit et les stratégies de quota sont des stratégies entrantes. Positionnez donc le curseur sur l'élément entrant.</span><span class="sxs-lookup"><span data-stu-id="1e072-159">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="1e072-161">Parcourez la liste déroulante des stratégies et recherchez l’entrée de la stratégie **Limiter la fréquence des appels par abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1e072-161">Scroll through the list of policies and locate the **Limit call rate per subscription** policy entry.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="1e072-163">Une fois le curseur positionné dans l’élément de stratégie **inbound**, cliquez sur la flèche en regard de **Limiter la fréquence des appels par abonnement** pour insérer son modèle de stratégie.</span><span class="sxs-lookup"><span data-stu-id="1e072-163">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="1e072-164">Comme vous pouvez le voir à partir de l’extrait de code, la stratégie permet de définir des limites pour les opérations et les API du produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-164">As you can see from the snippet, the policy allows setting limits for the product's APIs and operations.</span></span> <span data-ttu-id="1e072-165">Dans ce didacticiel, nous n’utiliserons pas cette fonctionnalité, supprimez donc les éléments **api** et **operation** de l’élément **rate-limit** pour ne laisser que l’élément externe **rate-limit**, comme le montre l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1e072-165">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **rate-limit** element, such that only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="1e072-166">Dans le produit en version d’évaluation gratuite, le débit d’appels maximum autorisé est de 10 appels par minute. Tapez **10** en tant que valeur pour l’attribut **calls** et **60** pour l’attribut **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="1e072-166">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="1e072-167">Pour configurer la stratégie **Définir le quota d’utilisation par abonnement**, positionnez votre curseur immédiatement sous l’élément **rate-limit** nouvellement ajouté dans l’élément **inbound**, puis recherchez et cliquez sur la flèche à gauche de **Définir le quota d’utilisation par abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1e072-167">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then locate and click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="1e072-168">Comme la stratégie **Limiter la fréquence des appels par abonnement**, la stratégie **Définir le quota d’utilisation par abonnement** permet de définir des plafonds pour les opérations et les API sur le produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-168">Similarly to the **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on the product's APIs and operations.</span></span> <span data-ttu-id="1e072-169">Dans ce didacticiel, nous n’utiliserons pas cette fonctionnalité, supprimez donc les éléments **api** et **operation** de l’élément **quota**, comme le montre l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1e072-169">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **quota** element, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="1e072-170">Les quotas peuvent être basés sur le nombre d’appels par intervalle et/ou par bande passante.</span><span class="sxs-lookup"><span data-stu-id="1e072-170">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="1e072-171">Dans ce didacticiel, nous ne définirons pas de limitation de bande passante. Supprimez donc l’attribut **bandwidth**.</span><span class="sxs-lookup"><span data-stu-id="1e072-171">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="1e072-172">Dans le produit en version d'évaluation gratuite, le quota est de 200 appels par semaine.</span><span class="sxs-lookup"><span data-stu-id="1e072-172">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="1e072-173">Indiquez **200** en tant que valeur pour l’attribut **calls**, puis indiquez **604800** en tant que valeur pour l’attribut **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="1e072-173">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="1e072-174">Les intervalles de stratégie sont spécifiés en secondes.</span><span class="sxs-lookup"><span data-stu-id="1e072-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="1e072-175">Pour calculer l’intervalle pour une semaine, vous pouvez multiplier le nombre de jours (7) par le nombre d’heures dans une journée (24) par le nombre de minutes dans une heure (60) par le nombre de secondes dans une minute (60) : 7 * 24 * 60 * 60 = 604 800.</span><span class="sxs-lookup"><span data-stu-id="1e072-175">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="1e072-176">Lorsque vous avez terminé la configuration de la stratégie, elle doit correspondre à l'exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1e072-176">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="1e072-177">Une fois les stratégies de votre choix configurées, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1e072-177">After the desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="1e072-179"><a name="publish-product"> </a> Publication du produit</span><span class="sxs-lookup"><span data-stu-id="1e072-179"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="1e072-180">Maintenant que les API sont ajoutées et les stratégies configurées, le produit doit être publié pour pouvoir être utilisé par des développeurs.</span><span class="sxs-lookup"><span data-stu-id="1e072-180">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="1e072-181">Cliquez sur **Produits** dans le menu **Gestion des API** sur la gauche, puis cliquez sur **Version d’évaluation gratuite** pour configurer le produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-181">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="1e072-183">Cliquez sur **Publier**, puis sur **Oui, publier** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="1e072-183">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="1e072-185"><a name="subscribe-account"> </a>Abonnement d’un compte de développeur au produit</span><span class="sxs-lookup"><span data-stu-id="1e072-185"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="1e072-186">Maintenant que le produit est publié, il est disponible pour abonnement et utilisation par les développeurs.</span><span class="sxs-lookup"><span data-stu-id="1e072-186">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="1e072-187">Les administrateurs d'une instance Gestion des API sont automatiquement abonnés à chaque produit.</span><span class="sxs-lookup"><span data-stu-id="1e072-187">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="1e072-188">Dans cette étape du didacticiel, nous abonnerons l’un des comptes de développeur non administrateurs au produit en version d’évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="1e072-188">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="1e072-189">Si votre compte de développeur fait partie du rôle Administrateur, vous pouvez suivre cette étape, même si vous êtes déjà abonné.</span><span class="sxs-lookup"><span data-stu-id="1e072-189">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="1e072-190">Cliquez sur **Utilisateurs** sur le menu **Gestion des API** situé à gauche, puis cliquez sur le nom de votre compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="1e072-190">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="1e072-191">Dans cet exemple, nous utilisons le compte de développeur **Clayton Gragg** .</span><span class="sxs-lookup"><span data-stu-id="1e072-191">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="1e072-193">Cliquez sur **Ajouter un abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1e072-193">Click **Add Subscription**.</span></span>

![Ajouter un abonnement][api-management-add-subscription-menu]

<span data-ttu-id="1e072-195">Sélectionnez **Version d’évaluation gratuite**, puis cliquez sur **S’abonner**.</span><span class="sxs-lookup"><span data-stu-id="1e072-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Ajouter un abonnement][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="1e072-197">Dans ce didacticiel, l’option autorisant plusieurs abonnements simultanés est désactivée pour le produit en version d’évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="1e072-197">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="1e072-198">Dans le cas contraire, vous auriez été invité à indiquer le nom de l’abonnement, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1e072-198">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![Ajouter un abonnement][api-management-add-subscription-multiple]

<span data-ttu-id="1e072-200">Après avoir cliqué sur **S’abonner**, le produit s’affiche dans la liste **Abonnement** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1e072-200">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![Abonnement ajouté][api-management-subscription-added]

## <span data-ttu-id="1e072-202"><a name="test-rate-limit"> </a>Appel d’une opération et test de la limite de débit</span><span class="sxs-lookup"><span data-stu-id="1e072-202"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="1e072-203">Maintenant que le produit en version d'évaluation gratuite est configuré et publié, nous pouvons appeler des opérations et tester la stratégie de limite de débit.</span><span class="sxs-lookup"><span data-stu-id="1e072-203">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="1e072-204">Basculez vers le portail de développeur en cliquant sur **Portail des développeurs** dans le menu supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="1e072-204">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="1e072-206">Cliquez sur **API** dans le menu supérieur, puis sélectionnez **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="1e072-206">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![Portail des développeurs][api-management-developer-portal-api-menu]

<span data-ttu-id="1e072-208">Cliquez sur **Ressource GET**, puis sur **Essayez-le**.</span><span class="sxs-lookup"><span data-stu-id="1e072-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="1e072-210">Conservez la valeur par défaut des paramètres et sélectionnez votre clé d’abonnement pour le produit en version d’évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="1e072-210">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![Clé d’abonnement][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="1e072-212">Si vous possédez plusieurs abonnements, pensez à sélectionner la clé pour la **Version d’évaluation gratuite**, sinon, les stratégies configurées aux étapes précédentes ne seront pas effectives.</span><span class="sxs-lookup"><span data-stu-id="1e072-212">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="1e072-213">Cliquez sur **Envoyer**, puis affichez la réponse.</span><span class="sxs-lookup"><span data-stu-id="1e072-213">Click **Send**, and then view the response.</span></span> <span data-ttu-id="1e072-214">Notez l'**État de réponse** **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="1e072-214">Note the **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="1e072-216">Cliquez sur **Envoyer** à une fréquence supérieure à la stratégie de limite de fréquence de 10 appels par minute.</span><span class="sxs-lookup"><span data-stu-id="1e072-216">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="1e072-217">Une fois la stratégie de limite de débit dépassée, un état de réponse **429 Trop de requêtes** est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="1e072-217">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="1e072-219">Le **Contenu de réponse** indique l’intervalle restant avant la réussite des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="1e072-219">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="1e072-220">Lorsque la stratégie de limite de débit de 10 appels par minute est appliquée, les appels suivants échouent jusqu’à ce que 60 secondes se soient écoulées à partir du premier des 10 appels réussis vers le produit avant le dépassement de la limite de débit.</span><span class="sxs-lookup"><span data-stu-id="1e072-220">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="1e072-221">Dans cet exemple, l’intervalle restant est de 54 secondes.</span><span class="sxs-lookup"><span data-stu-id="1e072-221">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="1e072-222"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e072-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="1e072-223">Consultez une démonstration relative à la définition de limites de débit et de quotas dans la vidéo suivante.</span><span class="sxs-lookup"><span data-stu-id="1e072-223">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
