---
title: "Stratégies de mise en cache dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies de mise en cache disponibles dans Gestion des API Azure."
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
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="0988e-103">Stratégies de mise en cache dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="0988e-103">API Management caching policies</span></span>
<span data-ttu-id="0988e-104">Cette rubrique est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="0988e-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="0988e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="0988e-106"><a name="CachingPolicies"></a> Stratégies de mise en cache</span><span class="sxs-lookup"><span data-stu-id="0988e-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="0988e-107">Stratégies de mise en cache des réponses</span><span class="sxs-lookup"><span data-stu-id="0988e-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="0988e-108">[Get from cache](api-management-caching-policies.md#GetFromCache) : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="0988e-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="0988e-109">[Store to cache](api-management-caching-policies.md#StoreToCache) : met en cache la réponse en fonction de la configuration de contrôle de cache spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0988e-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="0988e-110">Stratégies de mise en cache des valeurs</span><span class="sxs-lookup"><span data-stu-id="0988e-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="0988e-111">[Get value from cache](#GetFromCacheByKey) : récupère un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="0988e-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="0988e-112">[Store value in cache](#StoreToCacheByKey) : stocke un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="0988e-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="0988e-113">[Remove value from cache](#RemoveCacheByKey) : supprime un élément du cache par clé.</span><span class="sxs-lookup"><span data-stu-id="0988e-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="0988e-114"><a name="GetFromCache"></a> Get from cache</span><span class="sxs-lookup"><span data-stu-id="0988e-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="0988e-115">La stratégie `cache-lookup` permet d’effectuer une recherche dans le cache et de renvoyer une réponse mise en cache valide si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="0988e-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="0988e-116">Cette stratégie peut être appliquée dans les cas où le contenu de la réponse reste statique pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="0988e-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="0988e-117">La mise en cache de la réponse réduit les besoins en bande passante et en calcul imposés par le serveur web principal et limite la latence perçue par les consommateurs de l’API.</span><span class="sxs-lookup"><span data-stu-id="0988e-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0988e-118">Cette stratégie doit avoir une stratégie [Store to cache](api-management-caching-policies.md#StoreToCache) correspondante.</span><span class="sxs-lookup"><span data-stu-id="0988e-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0988e-119">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="0988e-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="0988e-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="0988e-121">Exemple</span><span class="sxs-lookup"><span data-stu-id="0988e-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="0988e-122">Exemple utilisant des expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-122">Example using policy expressions</span></span>  
 <span data-ttu-id="0988e-123">Cet exemple montre comment configurer la durée de mise en cache des réponses de Gestion des API qui correspond à la mise en cache de la réponse du service principal comme spécifié par la directive `Cache-Control` du service sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="0988e-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="0988e-124">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Plus de fonctionnalités de Gestion des API) avec Vlad Vinogradsky et rendez-vous directement à 25’25’’.</span><span class="sxs-lookup"><span data-stu-id="0988e-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="0988e-125">Pour plus d’informations, consultez [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="0988e-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="0988e-126">Éléments</span><span class="sxs-lookup"><span data-stu-id="0988e-126">Elements</span></span>  
  
|<span data-ttu-id="0988e-127">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-127">Name</span></span>|<span data-ttu-id="0988e-128">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-128">Description</span></span>|<span data-ttu-id="0988e-129">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0988e-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="0988e-130">cache-lookup</span></span>|<span data-ttu-id="0988e-131">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="0988e-131">Root element.</span></span>|<span data-ttu-id="0988e-132">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-132">Yes</span></span>|  
|<span data-ttu-id="0988e-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="0988e-133">vary-by-header</span></span>|<span data-ttu-id="0988e-134">Commence par mettre en cache les réponses selon la valeur d’en-tête spécifiée, telle que Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="0988e-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="0988e-135">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-135">No</span></span>|  
|<span data-ttu-id="0988e-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="0988e-136">vary-by-query-parameter</span></span>|<span data-ttu-id="0988e-137">Commencer la mise en cache des réponses selon la valeur des paramètres de requête spécifiés.</span><span class="sxs-lookup"><span data-stu-id="0988e-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="0988e-138">Entrez un ou plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="0988e-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="0988e-139">Utilisez un point-virgule comme séparateur.</span><span class="sxs-lookup"><span data-stu-id="0988e-139">Use semicolon as a separator.</span></span> <span data-ttu-id="0988e-140">Si vous n’en spécifiez aucun, tous les paramètres de la requête sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="0988e-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="0988e-141">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0988e-142">Attributs</span><span class="sxs-lookup"><span data-stu-id="0988e-142">Attributes</span></span>  
  
|<span data-ttu-id="0988e-143">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-143">Name</span></span>|<span data-ttu-id="0988e-144">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-144">Description</span></span>|<span data-ttu-id="0988e-145">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-145">Required</span></span>|<span data-ttu-id="0988e-146">Default</span><span class="sxs-lookup"><span data-stu-id="0988e-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0988e-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="0988e-147">allow-private-response-caching</span></span>|<span data-ttu-id="0988e-148">Lorsque l’attribut est défini sur `true`, permet la mise en cache des requêtes qui contiennent un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="0988e-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="0988e-149">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-149">No</span></span>|<span data-ttu-id="0988e-150">false</span><span class="sxs-lookup"><span data-stu-id="0988e-150">false</span></span>|  
|<span data-ttu-id="0988e-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="0988e-151">downstream-caching-type</span></span>|<span data-ttu-id="0988e-152">Cet attribut doit avoir l’une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="0988e-153">- none : la mise en cache en aval n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="0988e-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="0988e-154">- private : la mise en cache privée en aval est autorisée.</span><span class="sxs-lookup"><span data-stu-id="0988e-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="0988e-155">- public : la mise en cache privée et partagée en aval est autorisée.</span><span class="sxs-lookup"><span data-stu-id="0988e-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="0988e-156">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-156">No</span></span>|<span data-ttu-id="0988e-157">Aucun</span><span class="sxs-lookup"><span data-stu-id="0988e-157">none</span></span>|  
|<span data-ttu-id="0988e-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="0988e-158">must-revalidate</span></span>|<span data-ttu-id="0988e-159">Lorsque la mise en cache en aval est activée, cet attribut active ou désactive la directive de contrôle de cache `must-revalidate` dans les réponses de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0988e-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="0988e-160">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-160">No</span></span>|<span data-ttu-id="0988e-161">true</span><span class="sxs-lookup"><span data-stu-id="0988e-161">true</span></span>|  
|<span data-ttu-id="0988e-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="0988e-162">vary-by-developer</span></span>|<span data-ttu-id="0988e-163">Attribut défini sur `true` pour mettre en cache des réponses par clé de développeur.</span><span class="sxs-lookup"><span data-stu-id="0988e-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="0988e-164">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-164">No</span></span>|<span data-ttu-id="0988e-165">false</span><span class="sxs-lookup"><span data-stu-id="0988e-165">false</span></span>|  
|<span data-ttu-id="0988e-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="0988e-166">vary-by-developer-groups</span></span>|<span data-ttu-id="0988e-167">Attribut défini sur `true` pour mettre en cache des réponses par rôle d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0988e-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="0988e-168">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-168">No</span></span>|<span data-ttu-id="0988e-169">false</span><span class="sxs-lookup"><span data-stu-id="0988e-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0988e-170">Usage</span><span class="sxs-lookup"><span data-stu-id="0988e-170">Usage</span></span>  
 <span data-ttu-id="0988e-171">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0988e-172">**Sections de la stratégie :** inbound (entrant)</span><span class="sxs-lookup"><span data-stu-id="0988e-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0988e-173">**Étendues de la stratégie :** API, operation, product (API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="0988e-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="0988e-174"><a name="StoreToCache"></a> Store to cache</span><span class="sxs-lookup"><span data-stu-id="0988e-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="0988e-175">La stratégie `cache-store` met en cache la réponse en fonction des paramètres de cache spécifiés.</span><span class="sxs-lookup"><span data-stu-id="0988e-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="0988e-176">Cette stratégie peut être appliquée dans les cas où le contenu de la réponse reste statique pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="0988e-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="0988e-177">La mise en cache de la réponse réduit les besoins en bande passante et en calcul imposés par le serveur web principal et limite la latence perçue par les consommateurs de l’API.</span><span class="sxs-lookup"><span data-stu-id="0988e-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0988e-178">Cette stratégie avoir une stratégie [Get from cache](api-management-caching-policies.md#GetFromCache) correspondante.</span><span class="sxs-lookup"><span data-stu-id="0988e-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0988e-179">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="0988e-180">Exemples</span><span class="sxs-lookup"><span data-stu-id="0988e-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="0988e-181">Exemple</span><span class="sxs-lookup"><span data-stu-id="0988e-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="0988e-182">Exemple utilisant des expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-182">Example using policy expressions</span></span>  
 <span data-ttu-id="0988e-183">Cet exemple montre comment configurer la durée de mise en cache des réponses de Gestion des API qui correspond à la mise en cache de la réponse du service principal comme spécifié par la directive `Cache-Control` du service sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="0988e-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="0988e-184">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Plus de fonctionnalités de Gestion des API) avec Vlad Vinogradsky et rendez-vous directement à 25’25’’.</span><span class="sxs-lookup"><span data-stu-id="0988e-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="0988e-185">Pour plus d’informations, consultez [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="0988e-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="0988e-186">Éléments</span><span class="sxs-lookup"><span data-stu-id="0988e-186">Elements</span></span>  
  
|<span data-ttu-id="0988e-187">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-187">Name</span></span>|<span data-ttu-id="0988e-188">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-188">Description</span></span>|<span data-ttu-id="0988e-189">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0988e-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="0988e-190">cache-store</span></span>|<span data-ttu-id="0988e-191">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="0988e-191">Root element.</span></span>|<span data-ttu-id="0988e-192">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0988e-193">Attributs</span><span class="sxs-lookup"><span data-stu-id="0988e-193">Attributes</span></span>  
  
|<span data-ttu-id="0988e-194">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-194">Name</span></span>|<span data-ttu-id="0988e-195">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-195">Description</span></span>|<span data-ttu-id="0988e-196">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-196">Required</span></span>|<span data-ttu-id="0988e-197">Default</span><span class="sxs-lookup"><span data-stu-id="0988e-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0988e-198">duration</span><span class="sxs-lookup"><span data-stu-id="0988e-198">duration</span></span>|<span data-ttu-id="0988e-199">Durée de vie des entrées mises en cache (en secondes).</span><span class="sxs-lookup"><span data-stu-id="0988e-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="0988e-200">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-200">Yes</span></span>|<span data-ttu-id="0988e-201">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0988e-202">Usage</span><span class="sxs-lookup"><span data-stu-id="0988e-202">Usage</span></span>  
 <span data-ttu-id="0988e-203">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0988e-204">**Sections de la stratégie :** outbound (sortant)</span><span class="sxs-lookup"><span data-stu-id="0988e-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="0988e-205">**Étendues de la stratégie :** API, operation, product (API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="0988e-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="0988e-206"><a name="GetFromCacheByKey"></a> Get value from cache</span><span class="sxs-lookup"><span data-stu-id="0988e-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="0988e-207">La stratégie `cache-lookup-value` permet d’effectuer une recherche dans le cache par clé et de renvoyer une valeur mise en cache.</span><span class="sxs-lookup"><span data-stu-id="0988e-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="0988e-208">La clé peut avoir une valeur de chaîne arbitraire. Elle est généralement fournie à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="0988e-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0988e-209">Cette stratégie doit avoir une stratégie [Store value in cache](#StoreToCacheByKey) correspondante.</span><span class="sxs-lookup"><span data-stu-id="0988e-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0988e-210">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="0988e-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="0988e-211">Example</span></span>  
 <span data-ttu-id="0988e-212">Pour plus d’informations et d’exemples sur cette stratégie, consultez [Mise en cache personnalisée dans Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="0988e-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="0988e-213">Éléments</span><span class="sxs-lookup"><span data-stu-id="0988e-213">Elements</span></span>  
  
|<span data-ttu-id="0988e-214">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-214">Name</span></span>|<span data-ttu-id="0988e-215">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-215">Description</span></span>|<span data-ttu-id="0988e-216">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0988e-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="0988e-217">cache-lookup-value</span></span>|<span data-ttu-id="0988e-218">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="0988e-218">Root element.</span></span>|<span data-ttu-id="0988e-219">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0988e-220">Attributs</span><span class="sxs-lookup"><span data-stu-id="0988e-220">Attributes</span></span>  
  
|<span data-ttu-id="0988e-221">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-221">Name</span></span>|<span data-ttu-id="0988e-222">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-222">Description</span></span>|<span data-ttu-id="0988e-223">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-223">Required</span></span>|<span data-ttu-id="0988e-224">Default</span><span class="sxs-lookup"><span data-stu-id="0988e-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0988e-225">default-value</span><span class="sxs-lookup"><span data-stu-id="0988e-225">default-value</span></span>|<span data-ttu-id="0988e-226">Valeur attribuée à la variable si la recherche de clés de cache a échoué.</span><span class="sxs-lookup"><span data-stu-id="0988e-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="0988e-227">Si cet attribut n’est pas spécifié, `null` est attribué.</span><span class="sxs-lookup"><span data-stu-id="0988e-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="0988e-228">Non</span><span class="sxs-lookup"><span data-stu-id="0988e-228">No</span></span>|`null`|  
|<span data-ttu-id="0988e-229">key</span><span class="sxs-lookup"><span data-stu-id="0988e-229">key</span></span>|<span data-ttu-id="0988e-230">Valeur de clé de cache à utiliser dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="0988e-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="0988e-231">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-231">Yes</span></span>|<span data-ttu-id="0988e-232">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-232">N/A</span></span>|  
|<span data-ttu-id="0988e-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="0988e-233">variable-name</span></span>|<span data-ttu-id="0988e-234">Nom de la [variable contextuelle](api-management-policy-expressions.md#ContextVariables) à laquelle la valeur recherchée est attribuée, si la recherche réussit.</span><span class="sxs-lookup"><span data-stu-id="0988e-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="0988e-235">Si la recherche aboutit à un échec, la variable reçoit la valeur de l’attribut `default-value` ou `null`, si l’attribut `default-value` est omis.</span><span class="sxs-lookup"><span data-stu-id="0988e-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="0988e-236">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-236">Yes</span></span>|<span data-ttu-id="0988e-237">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0988e-238">Usage</span><span class="sxs-lookup"><span data-stu-id="0988e-238">Usage</span></span>  
 <span data-ttu-id="0988e-239">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0988e-240">**Sections de la stratégie :** inbound, outbound, backend, on-error (entrant, sortant, principal, en cas d’erreur)</span><span class="sxs-lookup"><span data-stu-id="0988e-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="0988e-241">**Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="0988e-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="0988e-242"><a name="StoreToCacheByKey"></a> Store value in cache</span><span class="sxs-lookup"><span data-stu-id="0988e-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="0988e-243">La stratégie `cache-store-value` effectue le stockage du cache par clé.</span><span class="sxs-lookup"><span data-stu-id="0988e-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="0988e-244">La clé peut avoir une valeur de chaîne arbitraire. Elle est généralement fournie à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="0988e-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0988e-245">Cette stratégie avoir une stratégie [Get value from cache](#GetFromCacheByKey) correspondante.</span><span class="sxs-lookup"><span data-stu-id="0988e-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0988e-246">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="0988e-247">Exemple</span><span class="sxs-lookup"><span data-stu-id="0988e-247">Example</span></span>  
 <span data-ttu-id="0988e-248">Pour plus d’informations et d’exemples sur cette stratégie, consultez [Mise en cache personnalisée dans Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="0988e-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="0988e-249">Éléments</span><span class="sxs-lookup"><span data-stu-id="0988e-249">Elements</span></span>  
  
|<span data-ttu-id="0988e-250">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-250">Name</span></span>|<span data-ttu-id="0988e-251">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-251">Description</span></span>|<span data-ttu-id="0988e-252">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0988e-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="0988e-253">cache-store-value</span></span>|<span data-ttu-id="0988e-254">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="0988e-254">Root element.</span></span>|<span data-ttu-id="0988e-255">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0988e-256">Attributs</span><span class="sxs-lookup"><span data-stu-id="0988e-256">Attributes</span></span>  
  
|<span data-ttu-id="0988e-257">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-257">Name</span></span>|<span data-ttu-id="0988e-258">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-258">Description</span></span>|<span data-ttu-id="0988e-259">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-259">Required</span></span>|<span data-ttu-id="0988e-260">Default</span><span class="sxs-lookup"><span data-stu-id="0988e-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0988e-261">duration</span><span class="sxs-lookup"><span data-stu-id="0988e-261">duration</span></span>|<span data-ttu-id="0988e-262">La valeur est mise en cache pendant la durée spécifiée en secondes.</span><span class="sxs-lookup"><span data-stu-id="0988e-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="0988e-263">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-263">Yes</span></span>|<span data-ttu-id="0988e-264">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-264">N/A</span></span>|  
|<span data-ttu-id="0988e-265">key</span><span class="sxs-lookup"><span data-stu-id="0988e-265">key</span></span>|<span data-ttu-id="0988e-266">Clé de cache sous laquelle la valeur est stockée.</span><span class="sxs-lookup"><span data-stu-id="0988e-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="0988e-267">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-267">Yes</span></span>|<span data-ttu-id="0988e-268">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-268">N/A</span></span>|  
|<span data-ttu-id="0988e-269">value</span><span class="sxs-lookup"><span data-stu-id="0988e-269">value</span></span>|<span data-ttu-id="0988e-270">Valeur à mettre en cache.</span><span class="sxs-lookup"><span data-stu-id="0988e-270">The value to be cached.</span></span>|<span data-ttu-id="0988e-271">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-271">Yes</span></span>|<span data-ttu-id="0988e-272">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0988e-273">Usage</span><span class="sxs-lookup"><span data-stu-id="0988e-273">Usage</span></span>  
 <span data-ttu-id="0988e-274">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0988e-275">**Sections de la stratégie :** inbound, outbound, backend, on-error (entrant, sortant, principal, en cas d’erreur)</span><span class="sxs-lookup"><span data-stu-id="0988e-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="0988e-276">**Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="0988e-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="0988e-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span><span class="sxs-lookup"><span data-stu-id="0988e-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="0988e-278">La stratégie `cache-remove-value` supprime un élément mis en cache identifié par sa clé.</span><span class="sxs-lookup"><span data-stu-id="0988e-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="0988e-279">La clé peut avoir une valeur de chaîne arbitraire. Elle est généralement fournie à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="0988e-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="0988e-280">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="0988e-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="0988e-281">Exemple</span><span class="sxs-lookup"><span data-stu-id="0988e-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="0988e-282">Éléments</span><span class="sxs-lookup"><span data-stu-id="0988e-282">Elements</span></span>  
  
|<span data-ttu-id="0988e-283">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-283">Name</span></span>|<span data-ttu-id="0988e-284">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-284">Description</span></span>|<span data-ttu-id="0988e-285">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0988e-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="0988e-286">cache-remove-value</span></span>|<span data-ttu-id="0988e-287">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="0988e-287">Root element.</span></span>|<span data-ttu-id="0988e-288">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="0988e-289">Attributs</span><span class="sxs-lookup"><span data-stu-id="0988e-289">Attributes</span></span>  
  
|<span data-ttu-id="0988e-290">Nom</span><span class="sxs-lookup"><span data-stu-id="0988e-290">Name</span></span>|<span data-ttu-id="0988e-291">Description</span><span class="sxs-lookup"><span data-stu-id="0988e-291">Description</span></span>|<span data-ttu-id="0988e-292">Requis</span><span class="sxs-lookup"><span data-stu-id="0988e-292">Required</span></span>|<span data-ttu-id="0988e-293">Default</span><span class="sxs-lookup"><span data-stu-id="0988e-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0988e-294">key</span><span class="sxs-lookup"><span data-stu-id="0988e-294">key</span></span>|<span data-ttu-id="0988e-295">Clé de la valeur précédemment mise en cache à supprimer du cache.</span><span class="sxs-lookup"><span data-stu-id="0988e-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="0988e-296">Oui</span><span class="sxs-lookup"><span data-stu-id="0988e-296">Yes</span></span>|<span data-ttu-id="0988e-297">N/A</span><span class="sxs-lookup"><span data-stu-id="0988e-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="0988e-298">Usage</span><span class="sxs-lookup"><span data-stu-id="0988e-298">Usage</span></span>  
 <span data-ttu-id="0988e-299">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="0988e-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="0988e-300">**Sections de la stratégie :** inbound, outbound, backend, on-error (entrant, sortant, principal, en cas d’erreur)</span><span class="sxs-lookup"><span data-stu-id="0988e-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="0988e-301">**Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="0988e-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="0988e-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0988e-302">Next steps</span></span>
<span data-ttu-id="0988e-303">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0988e-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  