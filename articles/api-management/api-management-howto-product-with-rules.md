---
title: aaaProtect votre API avec gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooprotect votre API avec les quotas et la limitation des stratégies (débit maximal)."
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
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="7cc8e-103">Protéger votre API avec des limites de débit à l’aide de la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="7cc8e-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="7cc8e-104">Ce guide vous explique comment il est facile de protection tooadd pour votre serveur principal API en configurant des stratégies de quota et la limite de taux avec gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="7cc8e-105">Dans ce didacticiel, vous allez créer un produit « Version d’évaluation gratuite « API qui permet aux développeurs toomake too10 des appels par minute et au maximum de 200 appels par semaine tooyour API est à l’aide de hello tooa [taux d’appels limite par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [ Définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) stratégies.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="7cc8e-106">Puis vous publiez hello API et tester la stratégie de limite de taux hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="7cc8e-107">Plus avancés de la limitation des scénarios à l’aide de hello [taux limite par clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [par clé de quota](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) stratégies, consultez [demande avancée limitation avec gestion des API Azure](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="7cc8e-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="7cc8e-108"><a name="create-product"></a>toocreate un produit</span><span class="sxs-lookup"><span data-stu-id="7cc8e-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="7cc8e-109">Dans cette étape, vous allez créer un produit en version d’évaluation gratuite, qui ne requiert aucune approbation d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="7cc8e-110">Si vous avez déjà disposer d’un produit configuré et que vous souhaitez toouse il pour ce didacticiel, vous pouvez sauter trop[configurer les stratégies de quota et la limite de taux d’appels] [ Configure call rate limit and quota policies] et suivez le didacticiel de hello à partir de là, l’utilisation du produit à la place de produit d’évaluation gratuite de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="7cc8e-111">tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="7cc8e-113">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [gérer votre première API de gestion des API Azure] [ Manage your first API in Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="7cc8e-114">Cliquez sur **produits** Bonjour **gestion des API** menu Bonjour toodisplay gauche Bonjour **produits** page.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="7cc8e-116">Cliquez sur **ajouter produit** toodisplay hello **ajouter un nouveau produit** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Ajouter un nouveau produit][api-management-new-product-window]

<span data-ttu-id="7cc8e-118">Bonjour **titre** , tapez **version d’évaluation gratuite**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="7cc8e-119">Bonjour **Description** boîte, hello du type suivant de texte : **abonnés peuvent être en mesure de toorun 10 appels/minute jusqu'à tooa maximum 200 appels par semaine, après laquelle l’accès est refusé.**</span><span class="sxs-lookup"><span data-stu-id="7cc8e-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="7cc8e-120">Les produits de Gestion des API peuvent être protégés ou ouverts.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="7cc8e-121">Produits protégés doivent être souscrit toobefore ils peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="7cc8e-122">Les produits ouverts sont utilisables sans abonnement.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="7cc8e-123">Vérifiez que **abonnement** toocreate sélectionné n’est un produit protégé qui nécessite un abonnement.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="7cc8e-124">Il s’agit de paramètre par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-124">This is hello default setting.</span></span>

<span data-ttu-id="7cc8e-125">Si vous souhaitez un tooreview administrateur et l’accepter ou rejeter abonnement tente toothis produit, sélectionnez **exiger l’approbation de l’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="7cc8e-126">Si la case à cocher hello n’est pas sélectionnée, les tentatives d’abonnement sera approuvée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="7cc8e-127">Dans cet exemple, les abonnements sont automatiquement approuvées, n’activez ne pas hello à.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="7cc8e-128">tooallow développeur comptes toosubscribe plusieurs fois toohello nouveau produit, sélectionnez hello **autoriser plusieurs abonnements simultanés** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="7cc8e-129">Ce didacticiel ne nécessite pas l’utilisation de plusieurs abonnements simultanés. Vous pouvez donc laisser cette case décochée.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="7cc8e-130">Une fois toutes les valeurs sont entrées, cliquez sur **enregistrer** produit de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="7cc8e-132">Par défaut, les nouveaux produits sont visibles toousers Bonjour **administrateurs** groupe.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="7cc8e-133">Nous allons tooadd hello **les développeurs** groupe.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="7cc8e-134">Cliquez sur **version d’évaluation gratuite**, puis cliquez sur hello **visibilité** onglet.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="7cc8e-135">Gestion des API, les groupes sont visibilité de hello utilisé toomanage de toodevelopers de produits.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="7cc8e-136">Produits accorder toogroups de visibilité, et les développeurs peuvent afficher et s’abonner toohello les produits qui sont des groupes toohello visible dans laquelle ils appartiennent.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="7cc8e-137">Pour plus d’informations, consultez [comment toocreate et l’utilisation de groupes dans la gestion des API Azure][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="7cc8e-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="7cc8e-139">Sélectionnez hello **les développeurs** case à cocher, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="7cc8e-140"><a name="add-api"></a>tooadd une API toohello produit</span><span class="sxs-lookup"><span data-stu-id="7cc8e-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="7cc8e-141">Dans cette étape du didacticiel de hello, nous allons ajouter hello Echo produit API de toohello nouvelle version d’évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="7cc8e-142">Chaque instance de service de gestion des API est préconfigurée avec une API d’écho qui peuvent être utilisé tooexperiment avec et en savoir plus sur la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="7cc8e-143">Pour plus d’informations, consultez [Gérer votre première API dans Gestion des API Azure][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="7cc8e-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="7cc8e-144">Cliquez sur **produits** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **version d’évaluation gratuite** produit de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="7cc8e-146">Cliquez sur **tooproduct d’ajouter les API**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-146">Click **Add API tooproduct**.</span></span>

![Ajouter les API tooproduct][api-management-add-api]

<span data-ttu-id="7cc8e-148">Sélectionnez **API Echo**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="7cc8e-150"><a name="policies"></a>tooconfigure les stratégies de quota et la limite de taux d’appels</span><span class="sxs-lookup"><span data-stu-id="7cc8e-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="7cc8e-151">Quotas et limites de taux sont configurés dans l’éditeur de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="7cc8e-152">Dans ce didacticiel, nous allons ajouter des stratégies Hello deux sont hello [taux d’appels limite par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) stratégies.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="7cc8e-153">Ces stratégies doivent être appliquées à la portée du produit hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="7cc8e-154">Cliquez sur **stratégies** sous hello **gestion des API** menu à gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="7cc8e-155">Bonjour **produit** , cliquez sur **version d’évaluation gratuite**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-155">In hello **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="7cc8e-157">Cliquez sur **ajouter une stratégie** tooimport hello du modèle de stratégie et commencer à créer des stratégies de quota et la limite de taux hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Add policy][api-management-add-policy]

<span data-ttu-id="7cc8e-159">Stratégies de quota et la limite de taux sont des stratégies entrants, dans ce curseur hello de position dans l’élément d’entrants hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="7cc8e-161">Faites défiler la liste des stratégies hello et localiser hello **taux d’appels limite par abonnement** entrée de stratégie.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="7cc8e-163">Après avoir hello le curseur est positionné dans hello **entrant** élément de stratégie, cliquez sur la flèche de hello **taux d’appels limite par abonnement** tooinsert son modèle de stratégie.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="7cc8e-164">Comme vous pouvez le voir à partir de l’extrait de code hello, stratégie de hello permet de définition des limites pour les opérations et les API du produit hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="7cc8e-165">Dans ce didacticiel, nous allons ne sera pas utiliser cette fonctionnalité, donc supprimer hello **api** et **opération** éléments à partir de hello **limite de taux** élément, de sorte que seuls hello externe**limite de taux** élément reste, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="7cc8e-166">Dans le produit d’évaluation gratuite de hello, taux d’appels d’autorisée maximale de hello 10 appels par minute, tapez **10** en tant que valeur hello pour hello **appelle** attribut, et **60** pour hello **période de renouvellement** attribut.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="7cc8e-167">tooconfigure hello **définir le quota d’utilisation par abonnement** stratégie, la position de votre curseur juste en dessous hello récemment ajouté **limite de taux** élément hello **entrant** élément, puis localisez et cliquez sur hello flèche toohello gauche **définir le quota d’utilisation par abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="7cc8e-168">De même toohello **définir le quota d’utilisation par abonnement** stratégie, **définir le quota d’utilisation par abonnement** stratégie permet de définir des majuscules pour sur les API du produit hello et des opérations.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="7cc8e-169">Dans ce didacticiel, nous allons ne sera pas utiliser cette fonctionnalité, donc supprimer hello **api** et **opération** éléments à partir de hello **quota** élément, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="7cc8e-170">Les quotas peuvent reposer sur le nombre de hello d’appels par intervalle, la bande passante ou les deux.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="7cc8e-171">Dans ce didacticiel, nous sommes sans limitation en fonction de la bande passante, donc supprimer hello **la bande passante** attribut.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="7cc8e-172">Dans le produit d’évaluation gratuite de hello, quota de hello est de 200 appels par semaine.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="7cc8e-173">Spécifiez **200** en tant que valeur hello pour hello **appelle** d’attribut et spécifiez **604800** en tant que valeur hello pour hello **période de renouvellement** attribut.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="7cc8e-174">Les intervalles de stratégie sont spécifiés en secondes.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="7cc8e-175">intervalle de salutation toocalculate pendant une semaine, vous pouvez multiplier hello nombre de jours (7) par nombre de hello d’heures par jour (24) par un nombre de minutes dans une heure (60) par un nombre de secondes dans une minute (60) hello hello : 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="7cc8e-176">Lorsque vous avez terminé la configuration de la stratégie de hello, elle doit correspondre à hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

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

<span data-ttu-id="7cc8e-177">Une fois hello souhaité de stratégies sont configurées, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-177">After hello desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="7cc8e-179"><a name="publish-product"></a> produit de hello toopublish</span><span class="sxs-lookup"><span data-stu-id="7cc8e-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="7cc8e-180">Maintenant que hello hello API ont été ajoutées et hello stratégies sont configurées, produit de hello doit être publié afin qu’il peut être utilisé par les développeurs.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="7cc8e-181">Cliquez sur **produits** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **version d’évaluation gratuite** produit de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="7cc8e-183">Cliquez sur **publier**, puis cliquez sur **Oui, publiez-le** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="7cc8e-185"><a name="subscribe-account"></a>toosubscribe un produit de toohello de compte de développeur</span><span class="sxs-lookup"><span data-stu-id="7cc8e-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="7cc8e-186">Maintenant ce produit hello est publié, il est tooand toobe disponible abonné utilisé par les développeurs.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="7cc8e-187">Les administrateurs d’une instance de la gestion des API sont automatiquement souscrit tooevery produit.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="7cc8e-188">Dans cette étape du didacticiel, nous peuvent s’abonner à un des comptes de développeur de non-administrateur hello toohello version d’évaluation gratuite produit.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="7cc8e-189">Si votre compte de développeur fait partie du rôle des administrateurs de hello, vous pouvez ensuite suivre en même temps que cette étape, même si vous êtes déjà inscrit.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="7cc8e-190">Cliquez sur **utilisateurs** sur hello **gestion des API** hello menu gauche, puis cliquez sur nom hello de votre compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="7cc8e-191">Dans cet exemple, nous utilisons hello **Clayton Gragg** compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="7cc8e-193">Cliquez sur **Ajouter un abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-193">Click **Add Subscription**.</span></span>

![Ajouter un abonnement][api-management-add-subscription-menu]

<span data-ttu-id="7cc8e-195">Sélectionnez **Version d’évaluation gratuite**, puis cliquez sur **S’abonner**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Ajouter un abonnement][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="7cc8e-197">Dans ce didacticiel, plusieurs abonnements simultanées ne sont pas activés pour le produit d’évaluation gratuite de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="7cc8e-198">S’il s’agissait, vous serait tooname demandées hello abonnement, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Ajouter un abonnement][api-management-add-subscription-multiple]

<span data-ttu-id="7cc8e-200">Après avoir cliqué sur **s’abonner**, produit de hello apparaît dans hello **abonnement** liste pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Abonnement ajouté][api-management-subscription-added]

## <span data-ttu-id="7cc8e-202"><a name="test-rate-limit"></a>toocall une limite de fréquence hello opération et de test</span><span class="sxs-lookup"><span data-stu-id="7cc8e-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="7cc8e-203">Maintenant hello produit de la version d’évaluation gratuite est configuré et publié, nous permet appeler certaines opérations et de tester la stratégie de limite de taux hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="7cc8e-204">Portail des développeurs commutateur toohello en cliquant sur **portail des développeurs** dans le menu supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="7cc8e-206">Cliquez sur **API** dans hello menu supérieur, puis cliquez sur **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![Portail des développeurs][api-management-developer-portal-api-menu]

<span data-ttu-id="7cc8e-208">Cliquez sur **Ressource GET**, puis sur **Essayez-le**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="7cc8e-210">Conserver les valeurs de paramètre par défaut de hello et sélectionnez votre clé d’abonnement pour le produit d’évaluation gratuite de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Clé d’abonnement][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="7cc8e-212">Si vous avez plusieurs abonnements, être Vérifiez que la touche tooselect hello pour **version d’évaluation gratuite**, ou autre stratégies hello qui ont été configurés dans les étapes précédentes hello ne sera pas en vigueur.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="7cc8e-213">Cliquez sur **envoyer**, puis affichez la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="7cc8e-214">Hello de note **état de la réponse** de **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-214">Note hello **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="7cc8e-216">Cliquez sur **envoyer** à une fréquence supérieure à la stratégie de limite de taux de hello 10 appels par minute.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="7cc8e-217">Une fois la stratégie de limite de taux de hello est dépassée, un état de réponse de **429 trop grand nombre de demandes** est retourné.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="7cc8e-219">Hello **contenu de la réponse** indique hello restant intervalle avant nouvelle tentative sera établie.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="7cc8e-220">Lors de la stratégie de limite de taux de hello 10 appels par minute, les appels suivants échoueront jusqu'à ce que 60 secondes à partir de hello premier du produit de toohello hello 10 appels réussis avant que la limite du taux de hello a été dépassé.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="7cc8e-221">Dans cet exemple, hello restant intervalle est 54 secondes.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="7cc8e-222"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7cc8e-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="7cc8e-223">Regarder une démonstration de la définition de quotas et limites de taux Bonjour suivant vidéo.</span><span class="sxs-lookup"><span data-stu-id="7cc8e-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
