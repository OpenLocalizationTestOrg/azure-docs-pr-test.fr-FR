---
title: "Modèles Produit dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment personnaliser le contenu des pages Produit dans le portail des développeurs Gestion des API Azure."
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
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="dc285-103">Modèles Produit dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="dc285-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="dc285-104">Gestion des API Azure vous offre la possibilité de personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles qui configurent leur contenu.</span><span class="sxs-lookup"><span data-stu-id="dc285-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="dc285-105">En utilisant la syntaxe [DotLiquid](http://dotliquidmarkup.org/) et l’éditeur de votre choix, comme [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ainsi qu’un ensemble de [ressources de chaîne](api-management-template-resources.md#strings), de [ressources de glyphe](api-management-template-resources.md#glyphs) et de [contrôles de page](api-management-page-controls.md) localisés, vous disposez d’un large choix pour configurer le contenu des pages selon vos besoins à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="dc285-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="dc285-106">Les modèles de cette section vous permettent de personnaliser le contenu des pages Produit dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="dc285-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="dc285-107">Liste de produits</span><span class="sxs-lookup"><span data-stu-id="dc285-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="dc285-108">Produit</span><span class="sxs-lookup"><span data-stu-id="dc285-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="dc285-109">Les exemples de modèles par défaut inclus dans la documentation suivante sont susceptibles d’être modifiés et améliorés de façon régulière.</span><span class="sxs-lookup"><span data-stu-id="dc285-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="dc285-110">Vous pouvez afficher les modèles dynamiques par défaut dans le portail des développeurs en accédant aux modèles individuels souhaités.</span><span class="sxs-lookup"><span data-stu-id="dc285-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="dc285-111">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="dc285-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="dc285-112"><a name="ProductList"></a> Liste de produits</span><span class="sxs-lookup"><span data-stu-id="dc285-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="dc285-113">Le modèle **Liste de produits** vous permet de personnaliser le corps de la page Liste de produits dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="dc285-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="dc285-114">![Liste de produits](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="dc285-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="dc285-115">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="dc285-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="dc285-116">Commandes</span><span class="sxs-lookup"><span data-stu-id="dc285-116">Controls</span></span>  
 <span data-ttu-id="dc285-117">Le modèle `Product list` peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="dc285-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="dc285-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="dc285-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="dc285-119">search-control</span><span class="sxs-lookup"><span data-stu-id="dc285-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="dc285-120">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="dc285-120">Data model</span></span>  
  
|<span data-ttu-id="dc285-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="dc285-121">Property</span></span>|<span data-ttu-id="dc285-122">Type</span><span class="sxs-lookup"><span data-stu-id="dc285-122">Type</span></span>|<span data-ttu-id="dc285-123">Description</span><span class="sxs-lookup"><span data-stu-id="dc285-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="dc285-124">Pagination</span><span class="sxs-lookup"><span data-stu-id="dc285-124">Paging</span></span>|<span data-ttu-id="dc285-125">Entité [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="dc285-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="dc285-126">Informations de pagination de la collection de produits.</span><span class="sxs-lookup"><span data-stu-id="dc285-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="dc285-127">Filtrage</span><span class="sxs-lookup"><span data-stu-id="dc285-127">Filtering</span></span>|<span data-ttu-id="dc285-128">Entité [Filtering](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="dc285-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="dc285-129">Informations de filtrage de la page Liste de produits.</span><span class="sxs-lookup"><span data-stu-id="dc285-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="dc285-130">Produits</span><span class="sxs-lookup"><span data-stu-id="dc285-130">Products</span></span>|<span data-ttu-id="dc285-131">Collection d’entités [Product](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="dc285-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="dc285-132">Produits visibles par l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="dc285-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="dc285-133">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="dc285-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="dc285-134"><a name="Product"></a> Produit</span><span class="sxs-lookup"><span data-stu-id="dc285-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="dc285-135">Le modèle **Produit** vous permet de personnaliser le corps de la page Produit dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="dc285-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="dc285-136">![Page Produit dans le portail des développeurs](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="dc285-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="dc285-137">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="dc285-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="dc285-138">Commandes</span><span class="sxs-lookup"><span data-stu-id="dc285-138">Controls</span></span>  
 <span data-ttu-id="dc285-139">Le modèle `Product list` peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="dc285-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="dc285-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="dc285-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="dc285-141">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="dc285-141">Data model</span></span>  
  
|<span data-ttu-id="dc285-142">Propriété</span><span class="sxs-lookup"><span data-stu-id="dc285-142">Property</span></span>|<span data-ttu-id="dc285-143">Type</span><span class="sxs-lookup"><span data-stu-id="dc285-143">Type</span></span>|<span data-ttu-id="dc285-144">Description</span><span class="sxs-lookup"><span data-stu-id="dc285-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="dc285-145">Produit</span><span class="sxs-lookup"><span data-stu-id="dc285-145">Product</span></span>|[<span data-ttu-id="dc285-146">Produit</span><span class="sxs-lookup"><span data-stu-id="dc285-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="dc285-147">Produit spécifié.</span><span class="sxs-lookup"><span data-stu-id="dc285-147">The specified product.</span></span>|  
|<span data-ttu-id="dc285-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="dc285-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="dc285-149">booléenne</span><span class="sxs-lookup"><span data-stu-id="dc285-149">boolean</span></span>|<span data-ttu-id="dc285-150">Si l’utilisateur actuel est abonné à ce produit.</span><span class="sxs-lookup"><span data-stu-id="dc285-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="dc285-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="dc285-151">SubscriptionState</span></span>|<span data-ttu-id="dc285-152">number</span><span class="sxs-lookup"><span data-stu-id="dc285-152">number</span></span>|<span data-ttu-id="dc285-153">État de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="dc285-153">The state of the subscription.</span></span> <span data-ttu-id="dc285-154">Les états possibles sont :</span><span class="sxs-lookup"><span data-stu-id="dc285-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="dc285-155">-   `0 - suspended` : l’abonnement est bloqué et l’abonné ne peut appeler aucune API du produit.</span><span class="sxs-lookup"><span data-stu-id="dc285-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="dc285-156">-   `1 - active` : l’abonnement est actif.</span><span class="sxs-lookup"><span data-stu-id="dc285-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="dc285-157">-   `2 - expired` : l’abonnement a atteint sa date d’expiration et a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="dc285-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="dc285-158">-   `3 - submitted` : la demande d’abonnement a été effectuée par le développeur, mais n’a pas encore été approuvée ou rejetée.</span><span class="sxs-lookup"><span data-stu-id="dc285-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="dc285-159">-   `4 - rejected` : la demande d’abonnement a été refusée par un administrateur.</span><span class="sxs-lookup"><span data-stu-id="dc285-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="dc285-160">-   `5 - cancelled` : l’abonnement a été annulé par le développeur ou l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dc285-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="dc285-161">limites</span><span class="sxs-lookup"><span data-stu-id="dc285-161">Limits</span></span>|<span data-ttu-id="dc285-162">array</span><span class="sxs-lookup"><span data-stu-id="dc285-162">array</span></span>|<span data-ttu-id="dc285-163">Cette propriété est déconseillée et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="dc285-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="dc285-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="dc285-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="dc285-165">booléenne</span><span class="sxs-lookup"><span data-stu-id="dc285-165">boolean</span></span>|<span data-ttu-id="dc285-166">Indique si la [délégation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) est activée pour cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="dc285-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="dc285-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="dc285-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="dc285-168">string</span><span class="sxs-lookup"><span data-stu-id="dc285-168">string</span></span>|<span data-ttu-id="dc285-169">Si la délégation est activée, indique l’URL de l’abonnement délégué.</span><span class="sxs-lookup"><span data-stu-id="dc285-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="dc285-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="dc285-170">IsAgreed</span></span>|<span data-ttu-id="dc285-171">booléenne</span><span class="sxs-lookup"><span data-stu-id="dc285-171">boolean</span></span>|<span data-ttu-id="dc285-172">Si le produit est associé à un contrat, indique si l’utilisateur actuel a accepté les termes du contrat.</span><span class="sxs-lookup"><span data-stu-id="dc285-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="dc285-173">Abonnements</span><span class="sxs-lookup"><span data-stu-id="dc285-173">Subscriptions</span></span>|<span data-ttu-id="dc285-174">Collection d’entités [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="dc285-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="dc285-175">Abonnements au produit.</span><span class="sxs-lookup"><span data-stu-id="dc285-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="dc285-176">Apis</span><span class="sxs-lookup"><span data-stu-id="dc285-176">Apis</span></span>|<span data-ttu-id="dc285-177">Collection d’entités [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="dc285-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="dc285-178">API dans ce produit.</span><span class="sxs-lookup"><span data-stu-id="dc285-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="dc285-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="dc285-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="dc285-180">booléenne</span><span class="sxs-lookup"><span data-stu-id="dc285-180">boolean</span></span>|<span data-ttu-id="dc285-181">Indique si l’utilisateur actuel est autorisé à s’abonner à ce produit en fonction de la limite d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="dc285-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="dc285-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="dc285-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="dc285-183">booléenne</span><span class="sxs-lookup"><span data-stu-id="dc285-183">boolean</span></span>|<span data-ttu-id="dc285-184">Indique si l’utilisateur actuel est autorisé à s’abonner à ce produit en fonction de l’autorisation ou non de plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="dc285-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="dc285-185">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="dc285-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="dc285-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc285-186">Next steps</span></span>
<span data-ttu-id="dc285-187">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dc285-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>