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
# <a name="product-templates-in-azure-api-management"></a>Modèles Produit dans Gestion des API Azure
Gestion des API Azure fournit que Hello de contenu de hello toocustomize possibilité de pages du portail développeur à l’aide d’un ensemble de modèles que configurer leur contenu. À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et hello l’éditeur de votre choix, tel que [DotLiquid pour les concepteurs](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), et un ensemble fourni de localisée [ressources de type chaîne](api-management-template-resources.md#strings), [ Ressources de glyphe](api-management-template-resources.md#glyphs), et [Page les contrôles](api-management-page-controls.md), vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez à l’aide de ces modèles.  
  
 modèles de Hello dans cette section vous autoriser le contenu de hello toocustomize de pages de produit hello dans le portail des développeurs hello.  
  
-   [Liste de produits](#ProductList)  
  
-   [Produit](#Product)  
  
> [!NOTE]
>  Exemples de modèles par défaut sont inclus dans hello suivant la documentation, mais sont toochange sujet en raison des améliorations de toocontinuous. Vous pouvez afficher les modèles par défaut dynamique hello dans le portail des développeurs hello en naviguant toohello souhaitée des modèles individuels. Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a> Liste de produits  
 Hello **liste de produits** modèle vous permet de corps de hello toocustomize de page de liste de produits hello dans le portail des développeurs hello.  
  
 ![Liste de produits](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Modèle par défaut  
  
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
  
### <a name="controls"></a>Commandes  
 Hello `Product list` modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).  
  
-   [paging-control](api-management-page-controls.md#paging-control)  
  
-   [search-control](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Modèle de données  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Pagination|Entité [Paging](api-management-template-data-model-reference.md#Paging).|informations de pagination Hello pour la collection de produits hello.|  
|Filtrage|Entité [Filtering](api-management-template-data-model-reference.md#Filtering).|Hello d’informations de filtrage pour la page liste des produits de hello.|  
|Produits|Collection d’entités [Product](api-management-template-data-model-reference.md#Product).|Hello produits toohello visible l’utilisateur actuel.|  
  
### <a name="sample-template-data"></a>Données d’un exemple de modèle  
  
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
  
##  <a name="Product"></a> Produit  
 Hello **produit** modèle vous permet de corps de hello toocustomize de page du produit hello dans le portail des développeurs hello.  
  
 ![Page Produit dans le portail des développeurs](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Modèle par défaut  
  
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
  
### <a name="controls"></a>Commandes  
 Hello `Product list` modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).  
  
-   [subscribe-button](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Modèle de données  
  
|Propriété|Type|Description|  
|--------------|----------|-----------------|  
|Produit|[Produit](api-management-template-data-model-reference.md#Product)|produit spécifié de Hello.|  
|IsDeveloperSubscribed|booléenne|Indique si l’utilisateur actuel hello est souscrit toothis produit.|  
|SubscriptionState|number|état Hello d’abonnement de hello. Les états possibles sont :<br /><br /> -   `0 - suspended`– hello abonnement est bloqué et l’abonné de hello ne peut pas appeler aucune API du produit de hello.<br />-   `1 - active`– hello abonnement est actif.<br />-   `2 - expired`– les abonnement hello a atteint sa date d’expiration et a été désactivé.<br />-   `3 - submitted`– demande d’abonnement hello a été effectuée par le développeur de hello, mais pas encore approuvé ou rejeté.<br />-   `4 - rejected`– demande d’abonnement hello a été refusée par un administrateur.<br />-   `5 - cancelled`– les abonnement hello a été annulée par le développeur de hello ou un administrateur.|  
|limites|array|Cette propriété est déconseillée et ne doit pas être utilisée.|  
|DelegatedSubscriptionEnabled|booléenne|Indique si la [délégation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) est activée pour cet abonnement.|  
|DelegatedSubscriptionUrl|string|Si la délégation est activée, hello déléguée URL d’abonnement.|  
|IsAgreed|booléenne|Si le produit de hello a des termes du contrat, si l’utilisateur actuel hello a accepté les termes du contrat de toohello.|  
|Abonnements|Collection d’entités [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary).|produit de toohello Hello abonnements.|  
|Apis|Collection d’entités [API](api-management-template-data-model-reference.md#API).|API Hello dans ce produit.|  
|CannotAddBecauseSubscriptionNumberLimitReached|booléenne|Indique si l’utilisateur actuel hello est éligible toosubscribe toothis produit limite d’abonnement toohello tenir compte.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|booléenne|Indique si l’utilisateur actuel hello est éligible toosubscribe toothis produit abonnements toomultiple de compte qui est autorisé ou non.|  
  
### <a name="sample-template-data"></a>Données d’un exemple de modèle  
  
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

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).
