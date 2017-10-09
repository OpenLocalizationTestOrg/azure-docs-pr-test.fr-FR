---
title: "modèles d’aaaProduct dans Gestion des API Azure | Documents Microsoft"
description: "Découvrez le fonctionnement des pages dans le portail des développeurs gestion des API Azure hello toocustomize le contenu hello du produit de hello."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="29642-103">Modèles Produit dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="29642-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="29642-104">Gestion des API Azure fournit que Hello de contenu de hello toocustomize possibilité de pages du portail développeur à l’aide d’un ensemble de modèles que configurer leur contenu.</span><span class="sxs-lookup"><span data-stu-id="29642-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="29642-105">À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et hello l’éditeur de votre choix, tel que [DotLiquid pour les concepteurs](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), et un ensemble fourni de localisée [ressources de type chaîne](api-management-template-resources.md#strings), [ Ressources de glyphe](api-management-template-resources.md#glyphs), et [Page les contrôles](api-management-page-controls.md), vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="29642-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="29642-106">modèles de Hello dans cette section vous autoriser le contenu de hello toocustomize de pages de produit hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="29642-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="29642-107">Liste de produits</span><span class="sxs-lookup"><span data-stu-id="29642-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="29642-108">Produit</span><span class="sxs-lookup"><span data-stu-id="29642-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="29642-109">Exemples de modèles par défaut sont inclus dans hello suivant la documentation, mais sont toochange sujet en raison des améliorations de toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="29642-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="29642-110">Vous pouvez afficher les modèles par défaut dynamique hello dans le portail des développeurs hello en naviguant toohello souhaitée des modèles individuels.</span><span class="sxs-lookup"><span data-stu-id="29642-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="29642-111">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="29642-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="29642-112"><a name="ProductList"></a> Liste de produits</span><span class="sxs-lookup"><span data-stu-id="29642-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="29642-113">Hello **liste de produits** modèle vous permet de corps de hello toocustomize de page de liste de produits hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="29642-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="29642-114">![Liste de produits](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="29642-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="29642-115">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="29642-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="29642-116">Commandes</span><span class="sxs-lookup"><span data-stu-id="29642-116">Controls</span></span>  
 <span data-ttu-id="29642-117">Hello `Product list` modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="29642-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="29642-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="29642-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="29642-119">search-control</span><span class="sxs-lookup"><span data-stu-id="29642-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="29642-120">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="29642-120">Data model</span></span>  
  
|<span data-ttu-id="29642-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="29642-121">Property</span></span>|<span data-ttu-id="29642-122">Type</span><span class="sxs-lookup"><span data-stu-id="29642-122">Type</span></span>|<span data-ttu-id="29642-123">Description</span><span class="sxs-lookup"><span data-stu-id="29642-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="29642-124">Pagination</span><span class="sxs-lookup"><span data-stu-id="29642-124">Paging</span></span>|<span data-ttu-id="29642-125">Entité [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="29642-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="29642-126">informations de pagination Hello pour la collection de produits hello.</span><span class="sxs-lookup"><span data-stu-id="29642-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="29642-127">Filtrage</span><span class="sxs-lookup"><span data-stu-id="29642-127">Filtering</span></span>|<span data-ttu-id="29642-128">Entité [Filtering](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="29642-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="29642-129">Hello d’informations de filtrage pour la page liste des produits de hello.</span><span class="sxs-lookup"><span data-stu-id="29642-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="29642-130">Produits</span><span class="sxs-lookup"><span data-stu-id="29642-130">Products</span></span>|<span data-ttu-id="29642-131">Collection d’entités [Product](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="29642-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="29642-132">Hello produits toohello visible l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="29642-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="29642-133">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="29642-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="29642-134"><a name="Product"></a> Produit</span><span class="sxs-lookup"><span data-stu-id="29642-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="29642-135">Hello **produit** modèle vous permet de corps de hello toocustomize de page du produit hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="29642-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="29642-136">![Page Produit dans le portail des développeurs](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="29642-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="29642-137">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="29642-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="29642-138">Commandes</span><span class="sxs-lookup"><span data-stu-id="29642-138">Controls</span></span>  
 <span data-ttu-id="29642-139">Hello `Product list` modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="29642-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="29642-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="29642-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="29642-141">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="29642-141">Data model</span></span>  
  
|<span data-ttu-id="29642-142">Propriété</span><span class="sxs-lookup"><span data-stu-id="29642-142">Property</span></span>|<span data-ttu-id="29642-143">Type</span><span class="sxs-lookup"><span data-stu-id="29642-143">Type</span></span>|<span data-ttu-id="29642-144">Description</span><span class="sxs-lookup"><span data-stu-id="29642-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="29642-145">Produit</span><span class="sxs-lookup"><span data-stu-id="29642-145">Product</span></span>|[<span data-ttu-id="29642-146">Produit</span><span class="sxs-lookup"><span data-stu-id="29642-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="29642-147">produit spécifié de Hello.</span><span class="sxs-lookup"><span data-stu-id="29642-147">hello specified product.</span></span>|  
|<span data-ttu-id="29642-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="29642-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="29642-149">booléenne</span><span class="sxs-lookup"><span data-stu-id="29642-149">boolean</span></span>|<span data-ttu-id="29642-150">Indique si l’utilisateur actuel hello est souscrit toothis produit.</span><span class="sxs-lookup"><span data-stu-id="29642-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="29642-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="29642-151">SubscriptionState</span></span>|<span data-ttu-id="29642-152">number</span><span class="sxs-lookup"><span data-stu-id="29642-152">number</span></span>|<span data-ttu-id="29642-153">état Hello d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="29642-153">hello state of hello subscription.</span></span> <span data-ttu-id="29642-154">Les états possibles sont :</span><span class="sxs-lookup"><span data-stu-id="29642-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="29642-155">-   `0 - suspended`– hello abonnement est bloqué et l’abonné de hello ne peut pas appeler aucune API du produit de hello.</span><span class="sxs-lookup"><span data-stu-id="29642-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="29642-156">-   `1 - active`– hello abonnement est actif.</span><span class="sxs-lookup"><span data-stu-id="29642-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="29642-157">-   `2 - expired`– les abonnement hello a atteint sa date d’expiration et a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="29642-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="29642-158">-   `3 - submitted`– demande d’abonnement hello a été effectuée par le développeur de hello, mais pas encore approuvé ou rejeté.</span><span class="sxs-lookup"><span data-stu-id="29642-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="29642-159">-   `4 - rejected`– demande d’abonnement hello a été refusée par un administrateur.</span><span class="sxs-lookup"><span data-stu-id="29642-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="29642-160">-   `5 - cancelled`– les abonnement hello a été annulée par le développeur de hello ou un administrateur.</span><span class="sxs-lookup"><span data-stu-id="29642-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="29642-161">limites</span><span class="sxs-lookup"><span data-stu-id="29642-161">Limits</span></span>|<span data-ttu-id="29642-162">array</span><span class="sxs-lookup"><span data-stu-id="29642-162">array</span></span>|<span data-ttu-id="29642-163">Cette propriété est déconseillée et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="29642-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="29642-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="29642-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="29642-165">booléenne</span><span class="sxs-lookup"><span data-stu-id="29642-165">boolean</span></span>|<span data-ttu-id="29642-166">Indique si la [délégation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) est activée pour cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="29642-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="29642-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="29642-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="29642-168">string</span><span class="sxs-lookup"><span data-stu-id="29642-168">string</span></span>|<span data-ttu-id="29642-169">Si la délégation est activée, hello déléguée URL d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="29642-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="29642-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="29642-170">IsAgreed</span></span>|<span data-ttu-id="29642-171">booléenne</span><span class="sxs-lookup"><span data-stu-id="29642-171">boolean</span></span>|<span data-ttu-id="29642-172">Si le produit de hello a des termes du contrat, si l’utilisateur actuel hello a accepté les termes du contrat de toohello.</span><span class="sxs-lookup"><span data-stu-id="29642-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="29642-173">Abonnements</span><span class="sxs-lookup"><span data-stu-id="29642-173">Subscriptions</span></span>|<span data-ttu-id="29642-174">Collection d’entités [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="29642-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="29642-175">produit de toohello Hello abonnements.</span><span class="sxs-lookup"><span data-stu-id="29642-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="29642-176">Apis</span><span class="sxs-lookup"><span data-stu-id="29642-176">Apis</span></span>|<span data-ttu-id="29642-177">Collection d’entités [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="29642-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="29642-178">API Hello dans ce produit.</span><span class="sxs-lookup"><span data-stu-id="29642-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="29642-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="29642-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="29642-180">booléenne</span><span class="sxs-lookup"><span data-stu-id="29642-180">boolean</span></span>|<span data-ttu-id="29642-181">Indique si l’utilisateur actuel hello est éligible toosubscribe toothis produit limite d’abonnement toohello tenir compte.</span><span class="sxs-lookup"><span data-stu-id="29642-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="29642-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="29642-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="29642-183">booléenne</span><span class="sxs-lookup"><span data-stu-id="29642-183">boolean</span></span>|<span data-ttu-id="29642-184">Indique si l’utilisateur actuel hello est éligible toosubscribe toothis produit abonnements toomultiple de compte qui est autorisé ou non.</span><span class="sxs-lookup"><span data-stu-id="29642-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="29642-185">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="29642-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="29642-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29642-186">Next steps</span></span>
<span data-ttu-id="29642-187">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="29642-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
