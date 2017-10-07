---
title: "stratégies de mise en cache de gestion des API aaaAzure | Documents Microsoft"
description: "Découvrez hello mise en cache des stratégies disponibles pour une utilisation dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>Stratégies de mise en cache dans Gestion des API
Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a> Stratégies de mise en cache  
  
-   Stratégies de mise en cache des réponses  
  
    -   [Get from cache](api-management-caching-policies.md#GetFromCache) : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.  
  
    -   [Stocker toocache](api-management-caching-policies.md#StoreToCache) - réponses Caches selon la configuration du contrôle toohello mise en cache spécifiée.  
  
-   Stratégies de mise en cache des valeurs  
  
    -   [Get value from cache](#GetFromCacheByKey) : récupère un élément mis en cache par clé.  
  
    -   [Stockez la valeur dans le cache](#StoreToCacheByKey) -stocker un élément dans le cache de hello par clé.  
  
    -   [Supprimez la valeur à partir du cache](#RemoveCacheByKey) -supprimer un élément dans le cache de hello par clé.  
  
##  <a name="GetFromCache"></a> Get from cache  
 Hello d’utilisation `cache-lookup` cache de stratégie tooperform rechercher et renvoyer une réponse mise en cache valide lorsqu’elle est disponible. Cette stratégie peut être appliquée dans les cas où le contenu de la réponse reste statique pendant un certain temps. Réponse mise en cache réduit la bande passante et les exigences de traitement imposée sur hello back-end web server ainsi que la latence perçue par les consommateurs d’API.  
  
> [!NOTE]
>  Cette stratégie doit correspondre à une [magasin toocache](api-management-caching-policies.md#StoreToCache) stratégie.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Exemple utilisant des expressions de stratégie  
 Cet exemple montre comment la réponse de gestion des API tootooconfigure mise en cache de la durée que correspondances hello la réponse mise en cache du service principal de hello tel que spécifié par hello sauvegardé du service `Cache-Control` directive. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|cache-lookup|Élément racine.|Oui|  
|vary-by-header|Commence par mettre en cache les réponses selon la valeur d’en-tête spécifiée, telle que Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.|Non|  
|vary-by-query-parameter|Commencer la mise en cache des réponses selon la valeur des paramètres de requête spécifiés. Entrez un ou plusieurs paramètres. Utilisez un point-virgule comme séparateur. Si vous n’en spécifiez aucun, tous les paramètres de la requête sont utilisés.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|Lorsque la valeur trop`true`, permet la mise en cache des requêtes qui contiennent un en-tête d’autorisation.|Non|false|  
|downstream-caching-type|Cet attribut doit être défini tooone Hello valeurs suivantes.<br /><br /> - none : la mise en cache en aval n’est pas autorisée.<br />- private : la mise en cache privée en aval est autorisée.<br />- public : la mise en cache privée et partagée en aval est autorisée.|Non|Aucun|  
|must-revalidate|Lors de la mise en cache en aval est activée cet attribut Active ou désactive hello `must-revalidate` directive de contrôle de cache dans les réponses de la passerelle.|Non|true|  
|vary-by-developer|Définir trop`true` toocache les réponses par clé de développeur.|Non|false|  
|vary-by-developer-groups|Définir trop`true` toocache les réponses par rôle d’utilisateur.|Non|false|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** API, operation, product (API, opération, produit)  
  
##  <a name="StoreToCache"></a>Magasin toocache  
 Hello `cache-store` réponses de caches de stratégie selon toohello spécifié des paramètres de cache. Cette stratégie peut être appliquée dans les cas où le contenu de la réponse reste statique pendant un certain temps. Réponse mise en cache réduit la bande passante et les exigences de traitement imposée sur hello back-end web server ainsi que la latence perçue par les consommateurs d’API.  
  
> [!NOTE]
>  Cette stratégie avoir une stratégie [Get from cache](api-management-caching-policies.md#GetFromCache) correspondante.  
  
### <a name="policy-statement"></a>Déclaration de stratégie  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="example"></a>Exemple  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Exemple utilisant des expressions de stratégie  
 Cet exemple montre comment la réponse de gestion des API tootooconfigure mise en cache de la durée que correspondances hello la réponse mise en cache du service principal de hello tel que spécifié par hello sauvegardé du service `Cache-Control` directive. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|cache-store|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|duration|Durée de vie de hello mis en cache les entrées, exprimées en secondes.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** outbound (sortant)  
  
-   **Étendues de la stratégie :** API, operation, product (API, opération, produit)  
  
##  <a name="GetFromCacheByKey"></a> Get value from cache  
 Hello d’utilisation `cache-lookup-value` tooperform de stratégie de cache recherche par clé et retourner une valeur mis en cache. clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.  
  
> [!NOTE]
>  Cette stratégie doit avoir une stratégie [Store value in cache](#StoreToCacheByKey) correspondante.  
  
### <a name="policy-statement"></a>Déclaration de stratégie  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Exemple  
 Pour plus d’informations et d’exemples sur cette stratégie, consultez [Mise en cache personnalisée dans Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|cache-lookup-value|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|default-value|Une valeur qui sera assignée toohello variable si la recherche de clé de cache hello a entraîné un échec. Si cet attribut n’est pas spécifié, `null` est attribué.|Non|`null`|  
|key|Mettre en cache toouse de valeur de clé dans la recherche de hello.|Oui|N/A|  
|variable-name|Nom de hello [variable contextuelle](api-management-policy-expressions.md#ContextVariables) hello effectue la recherche de valeur sera affectée, la recherche est réussie. Si la recherche aboutit à un échec, la variable de hello sera attribuée valeur hello Hello `default-value` attribut ou `null`si hello `default-value` attribut est omis.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)  
  
##  <a name="StoreToCacheByKey"></a> Store value in cache  
 Hello `cache-store-value` effectue le stockage de cache par clé. clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.  
  
> [!NOTE]
>  Cette stratégie avoir une stratégie [Get value from cache](#GetFromCacheByKey) correspondante.  
  
### <a name="policy-statement"></a>Déclaration de stratégie  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Exemple  
 Pour plus d’informations et d’exemples sur cette stratégie, consultez [Mise en cache personnalisée dans Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|cache-store-value|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|duration|Valeur est mises en cache pour hello fourni la valeur de durée, exprimée en secondes.|Oui|N/A|  
|key|Valeur de clé hello du cache sera stocké sous.|Oui|N/A|  
|value|Hello toobe de valeur mis en cache.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)  
  
###  <a name="RemoveCacheByKey"></a> Remove value from cache  
 Hello `cache-remove-value` supprime un élément mis en cache identifié par sa clé. clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.  
  
#### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Exemple  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Éléments  
  
|Nom|Description|Requis|  
|----------|-----------------|--------------|  
|cache-remove-value|Élément racine.|Oui|  
  
#### <a name="attributes"></a>Attributs  
  
|Nom|Description|Requis|Default|  
|----------|-----------------|--------------|-------------|  
|key|clé Hello Hello mis en cache précédemment toobe valeur supprimé du cache de hello.|Oui|N/A|  
  
#### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)  
  

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  