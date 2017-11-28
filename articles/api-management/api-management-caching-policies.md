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
# <a name="api-management-caching-policies"></a><span data-ttu-id="80c0e-103">Stratégies de mise en cache dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="80c0e-103">API Management caching policies</span></span>
<span data-ttu-id="80c0e-104">Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="80c0e-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="80c0e-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="80c0e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="80c0e-106"><a name="CachingPolicies"></a> Stratégies de mise en cache</span><span class="sxs-lookup"><span data-stu-id="80c0e-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="80c0e-107">Stratégies de mise en cache des réponses</span><span class="sxs-lookup"><span data-stu-id="80c0e-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="80c0e-108">[Get from cache](api-management-caching-policies.md#GetFromCache) : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="80c0e-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="80c0e-109">[Stocker toocache](api-management-caching-policies.md#StoreToCache) - réponses Caches selon la configuration du contrôle toohello mise en cache spécifiée.</span><span class="sxs-lookup"><span data-stu-id="80c0e-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="80c0e-110">Stratégies de mise en cache des valeurs</span><span class="sxs-lookup"><span data-stu-id="80c0e-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="80c0e-111">[Get value from cache](#GetFromCacheByKey) : récupère un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="80c0e-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="80c0e-112">[Stockez la valeur dans le cache](#StoreToCacheByKey) -stocker un élément dans le cache de hello par clé.</span><span class="sxs-lookup"><span data-stu-id="80c0e-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="80c0e-113">[Supprimez la valeur à partir du cache](#RemoveCacheByKey) -supprimer un élément dans le cache de hello par clé.</span><span class="sxs-lookup"><span data-stu-id="80c0e-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="80c0e-114"><a name="GetFromCache"></a> Get from cache</span><span class="sxs-lookup"><span data-stu-id="80c0e-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="80c0e-115">Hello d’utilisation `cache-lookup` cache de stratégie tooperform rechercher et renvoyer une réponse mise en cache valide lorsqu’elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="80c0e-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="80c0e-116">Cette stratégie peut être appliquée dans les cas où le contenu de la réponse reste statique pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="80c0e-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="80c0e-117">Réponse mise en cache réduit la bande passante et les exigences de traitement imposée sur hello back-end web server ainsi que la latence perçue par les consommateurs d’API.</span><span class="sxs-lookup"><span data-stu-id="80c0e-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80c0e-118">Cette stratégie doit correspondre à une [magasin toocache](api-management-caching-policies.md#StoreToCache) stratégie.</span><span class="sxs-lookup"><span data-stu-id="80c0e-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="80c0e-119">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-119">Policy statement</span></span>  
  
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
  
### <a name="examples"></a><span data-ttu-id="80c0e-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="80c0e-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="80c0e-121">Exemple</span><span class="sxs-lookup"><span data-stu-id="80c0e-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="80c0e-122">Exemple utilisant des expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-122">Example using policy expressions</span></span>  
 <span data-ttu-id="80c0e-123">Cet exemple montre comment la réponse de gestion des API tootooconfigure mise en cache de la durée que correspondances hello la réponse mise en cache du service principal de hello tel que spécifié par hello sauvegardé du service `Cache-Control` directive.</span><span class="sxs-lookup"><span data-stu-id="80c0e-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="80c0e-124">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too25:25.</span><span class="sxs-lookup"><span data-stu-id="80c0e-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
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
  
 <span data-ttu-id="80c0e-125">Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="80c0e-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="80c0e-126">Éléments</span><span class="sxs-lookup"><span data-stu-id="80c0e-126">Elements</span></span>  
  
|<span data-ttu-id="80c0e-127">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-127">Name</span></span>|<span data-ttu-id="80c0e-128">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-128">Description</span></span>|<span data-ttu-id="80c0e-129">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="80c0e-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="80c0e-130">cache-lookup</span></span>|<span data-ttu-id="80c0e-131">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="80c0e-131">Root element.</span></span>|<span data-ttu-id="80c0e-132">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-132">Yes</span></span>|  
|<span data-ttu-id="80c0e-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="80c0e-133">vary-by-header</span></span>|<span data-ttu-id="80c0e-134">Commence par mettre en cache les réponses selon la valeur d’en-tête spécifiée, telle que Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="80c0e-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="80c0e-135">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-135">No</span></span>|  
|<span data-ttu-id="80c0e-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="80c0e-136">vary-by-query-parameter</span></span>|<span data-ttu-id="80c0e-137">Commencer la mise en cache des réponses selon la valeur des paramètres de requête spécifiés.</span><span class="sxs-lookup"><span data-stu-id="80c0e-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="80c0e-138">Entrez un ou plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="80c0e-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="80c0e-139">Utilisez un point-virgule comme séparateur.</span><span class="sxs-lookup"><span data-stu-id="80c0e-139">Use semicolon as a separator.</span></span> <span data-ttu-id="80c0e-140">Si vous n’en spécifiez aucun, tous les paramètres de la requête sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="80c0e-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="80c0e-141">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="80c0e-142">Attributs</span><span class="sxs-lookup"><span data-stu-id="80c0e-142">Attributes</span></span>  
  
|<span data-ttu-id="80c0e-143">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-143">Name</span></span>|<span data-ttu-id="80c0e-144">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-144">Description</span></span>|<span data-ttu-id="80c0e-145">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-145">Required</span></span>|<span data-ttu-id="80c0e-146">Default</span><span class="sxs-lookup"><span data-stu-id="80c0e-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="80c0e-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="80c0e-147">allow-private-response-caching</span></span>|<span data-ttu-id="80c0e-148">Lorsque la valeur trop`true`, permet la mise en cache des requêtes qui contiennent un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="80c0e-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="80c0e-149">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-149">No</span></span>|<span data-ttu-id="80c0e-150">false</span><span class="sxs-lookup"><span data-stu-id="80c0e-150">false</span></span>|  
|<span data-ttu-id="80c0e-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="80c0e-151">downstream-caching-type</span></span>|<span data-ttu-id="80c0e-152">Cet attribut doit être défini tooone Hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="80c0e-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="80c0e-153">- none : la mise en cache en aval n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="80c0e-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="80c0e-154">- private : la mise en cache privée en aval est autorisée.</span><span class="sxs-lookup"><span data-stu-id="80c0e-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="80c0e-155">- public : la mise en cache privée et partagée en aval est autorisée.</span><span class="sxs-lookup"><span data-stu-id="80c0e-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="80c0e-156">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-156">No</span></span>|<span data-ttu-id="80c0e-157">Aucun</span><span class="sxs-lookup"><span data-stu-id="80c0e-157">none</span></span>|  
|<span data-ttu-id="80c0e-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="80c0e-158">must-revalidate</span></span>|<span data-ttu-id="80c0e-159">Lors de la mise en cache en aval est activée cet attribut Active ou désactive hello `must-revalidate` directive de contrôle de cache dans les réponses de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="80c0e-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="80c0e-160">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-160">No</span></span>|<span data-ttu-id="80c0e-161">true</span><span class="sxs-lookup"><span data-stu-id="80c0e-161">true</span></span>|  
|<span data-ttu-id="80c0e-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="80c0e-162">vary-by-developer</span></span>|<span data-ttu-id="80c0e-163">Définir trop`true` toocache les réponses par clé de développeur.</span><span class="sxs-lookup"><span data-stu-id="80c0e-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="80c0e-164">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-164">No</span></span>|<span data-ttu-id="80c0e-165">false</span><span class="sxs-lookup"><span data-stu-id="80c0e-165">false</span></span>|  
|<span data-ttu-id="80c0e-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="80c0e-166">vary-by-developer-groups</span></span>|<span data-ttu-id="80c0e-167">Définir trop`true` toocache les réponses par rôle d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="80c0e-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="80c0e-168">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-168">No</span></span>|<span data-ttu-id="80c0e-169">false</span><span class="sxs-lookup"><span data-stu-id="80c0e-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="80c0e-170">Usage</span><span class="sxs-lookup"><span data-stu-id="80c0e-170">Usage</span></span>  
 <span data-ttu-id="80c0e-171">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="80c0e-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="80c0e-172">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="80c0e-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="80c0e-173">**Étendues de la stratégie :** API, operation, product (API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="80c0e-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="80c0e-174"><a name="StoreToCache"></a>Magasin toocache</span><span class="sxs-lookup"><span data-stu-id="80c0e-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="80c0e-175">Hello `cache-store` réponses de caches de stratégie selon toohello spécifié des paramètres de cache.</span><span class="sxs-lookup"><span data-stu-id="80c0e-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="80c0e-176">Cette stratégie peut être appliquée dans les cas où le contenu de la réponse reste statique pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="80c0e-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="80c0e-177">Réponse mise en cache réduit la bande passante et les exigences de traitement imposée sur hello back-end web server ainsi que la latence perçue par les consommateurs d’API.</span><span class="sxs-lookup"><span data-stu-id="80c0e-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80c0e-178">Cette stratégie avoir une stratégie [Get from cache](api-management-caching-policies.md#GetFromCache) correspondante.</span><span class="sxs-lookup"><span data-stu-id="80c0e-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="80c0e-179">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="80c0e-180">Exemples</span><span class="sxs-lookup"><span data-stu-id="80c0e-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="80c0e-181">Exemple</span><span class="sxs-lookup"><span data-stu-id="80c0e-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="80c0e-182">Exemple utilisant des expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-182">Example using policy expressions</span></span>  
 <span data-ttu-id="80c0e-183">Cet exemple montre comment la réponse de gestion des API tootooconfigure mise en cache de la durée que correspondances hello la réponse mise en cache du service principal de hello tel que spécifié par hello sauvegardé du service `Cache-Control` directive.</span><span class="sxs-lookup"><span data-stu-id="80c0e-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="80c0e-184">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too25:25.</span><span class="sxs-lookup"><span data-stu-id="80c0e-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
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
  
 <span data-ttu-id="80c0e-185">Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="80c0e-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="80c0e-186">Éléments</span><span class="sxs-lookup"><span data-stu-id="80c0e-186">Elements</span></span>  
  
|<span data-ttu-id="80c0e-187">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-187">Name</span></span>|<span data-ttu-id="80c0e-188">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-188">Description</span></span>|<span data-ttu-id="80c0e-189">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="80c0e-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="80c0e-190">cache-store</span></span>|<span data-ttu-id="80c0e-191">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="80c0e-191">Root element.</span></span>|<span data-ttu-id="80c0e-192">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="80c0e-193">Attributs</span><span class="sxs-lookup"><span data-stu-id="80c0e-193">Attributes</span></span>  
  
|<span data-ttu-id="80c0e-194">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-194">Name</span></span>|<span data-ttu-id="80c0e-195">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-195">Description</span></span>|<span data-ttu-id="80c0e-196">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-196">Required</span></span>|<span data-ttu-id="80c0e-197">Default</span><span class="sxs-lookup"><span data-stu-id="80c0e-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="80c0e-198">duration</span><span class="sxs-lookup"><span data-stu-id="80c0e-198">duration</span></span>|<span data-ttu-id="80c0e-199">Durée de vie de hello mis en cache les entrées, exprimées en secondes.</span><span class="sxs-lookup"><span data-stu-id="80c0e-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="80c0e-200">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-200">Yes</span></span>|<span data-ttu-id="80c0e-201">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="80c0e-202">Usage</span><span class="sxs-lookup"><span data-stu-id="80c0e-202">Usage</span></span>  
 <span data-ttu-id="80c0e-203">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="80c0e-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="80c0e-204">**Sections de la stratégie :** outbound (sortant)</span><span class="sxs-lookup"><span data-stu-id="80c0e-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="80c0e-205">**Étendues de la stratégie :** API, operation, product (API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="80c0e-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="80c0e-206"><a name="GetFromCacheByKey"></a> Get value from cache</span><span class="sxs-lookup"><span data-stu-id="80c0e-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="80c0e-207">Hello d’utilisation `cache-lookup-value` tooperform de stratégie de cache recherche par clé et retourner une valeur mis en cache.</span><span class="sxs-lookup"><span data-stu-id="80c0e-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="80c0e-208">clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="80c0e-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80c0e-209">Cette stratégie doit avoir une stratégie [Store value in cache](#StoreToCacheByKey) correspondante.</span><span class="sxs-lookup"><span data-stu-id="80c0e-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="80c0e-210">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="80c0e-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="80c0e-211">Example</span></span>  
 <span data-ttu-id="80c0e-212">Pour plus d’informations et d’exemples sur cette stratégie, consultez [Mise en cache personnalisée dans Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="80c0e-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="80c0e-213">Éléments</span><span class="sxs-lookup"><span data-stu-id="80c0e-213">Elements</span></span>  
  
|<span data-ttu-id="80c0e-214">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-214">Name</span></span>|<span data-ttu-id="80c0e-215">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-215">Description</span></span>|<span data-ttu-id="80c0e-216">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="80c0e-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="80c0e-217">cache-lookup-value</span></span>|<span data-ttu-id="80c0e-218">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="80c0e-218">Root element.</span></span>|<span data-ttu-id="80c0e-219">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="80c0e-220">Attributs</span><span class="sxs-lookup"><span data-stu-id="80c0e-220">Attributes</span></span>  
  
|<span data-ttu-id="80c0e-221">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-221">Name</span></span>|<span data-ttu-id="80c0e-222">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-222">Description</span></span>|<span data-ttu-id="80c0e-223">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-223">Required</span></span>|<span data-ttu-id="80c0e-224">Default</span><span class="sxs-lookup"><span data-stu-id="80c0e-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="80c0e-225">default-value</span><span class="sxs-lookup"><span data-stu-id="80c0e-225">default-value</span></span>|<span data-ttu-id="80c0e-226">Une valeur qui sera assignée toohello variable si la recherche de clé de cache hello a entraîné un échec.</span><span class="sxs-lookup"><span data-stu-id="80c0e-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="80c0e-227">Si cet attribut n’est pas spécifié, `null` est attribué.</span><span class="sxs-lookup"><span data-stu-id="80c0e-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="80c0e-228">Non</span><span class="sxs-lookup"><span data-stu-id="80c0e-228">No</span></span>|`null`|  
|<span data-ttu-id="80c0e-229">key</span><span class="sxs-lookup"><span data-stu-id="80c0e-229">key</span></span>|<span data-ttu-id="80c0e-230">Mettre en cache toouse de valeur de clé dans la recherche de hello.</span><span class="sxs-lookup"><span data-stu-id="80c0e-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="80c0e-231">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-231">Yes</span></span>|<span data-ttu-id="80c0e-232">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-232">N/A</span></span>|  
|<span data-ttu-id="80c0e-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="80c0e-233">variable-name</span></span>|<span data-ttu-id="80c0e-234">Nom de hello [variable contextuelle](api-management-policy-expressions.md#ContextVariables) hello effectue la recherche de valeur sera affectée, la recherche est réussie.</span><span class="sxs-lookup"><span data-stu-id="80c0e-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="80c0e-235">Si la recherche aboutit à un échec, la variable de hello sera attribuée valeur hello Hello `default-value` attribut ou `null`si hello `default-value` attribut est omis.</span><span class="sxs-lookup"><span data-stu-id="80c0e-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="80c0e-236">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-236">Yes</span></span>|<span data-ttu-id="80c0e-237">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="80c0e-238">Usage</span><span class="sxs-lookup"><span data-stu-id="80c0e-238">Usage</span></span>  
 <span data-ttu-id="80c0e-239">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="80c0e-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="80c0e-240">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="80c0e-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="80c0e-241">**Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="80c0e-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="80c0e-242"><a name="StoreToCacheByKey"></a> Store value in cache</span><span class="sxs-lookup"><span data-stu-id="80c0e-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="80c0e-243">Hello `cache-store-value` effectue le stockage de cache par clé.</span><span class="sxs-lookup"><span data-stu-id="80c0e-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="80c0e-244">clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="80c0e-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="80c0e-245">Cette stratégie avoir une stratégie [Get value from cache](#GetFromCacheByKey) correspondante.</span><span class="sxs-lookup"><span data-stu-id="80c0e-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="80c0e-246">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="80c0e-247">Exemple</span><span class="sxs-lookup"><span data-stu-id="80c0e-247">Example</span></span>  
 <span data-ttu-id="80c0e-248">Pour plus d’informations et d’exemples sur cette stratégie, consultez [Mise en cache personnalisée dans Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="80c0e-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="80c0e-249">Éléments</span><span class="sxs-lookup"><span data-stu-id="80c0e-249">Elements</span></span>  
  
|<span data-ttu-id="80c0e-250">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-250">Name</span></span>|<span data-ttu-id="80c0e-251">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-251">Description</span></span>|<span data-ttu-id="80c0e-252">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="80c0e-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="80c0e-253">cache-store-value</span></span>|<span data-ttu-id="80c0e-254">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="80c0e-254">Root element.</span></span>|<span data-ttu-id="80c0e-255">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="80c0e-256">Attributs</span><span class="sxs-lookup"><span data-stu-id="80c0e-256">Attributes</span></span>  
  
|<span data-ttu-id="80c0e-257">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-257">Name</span></span>|<span data-ttu-id="80c0e-258">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-258">Description</span></span>|<span data-ttu-id="80c0e-259">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-259">Required</span></span>|<span data-ttu-id="80c0e-260">Default</span><span class="sxs-lookup"><span data-stu-id="80c0e-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="80c0e-261">duration</span><span class="sxs-lookup"><span data-stu-id="80c0e-261">duration</span></span>|<span data-ttu-id="80c0e-262">Valeur est mises en cache pour hello fourni la valeur de durée, exprimée en secondes.</span><span class="sxs-lookup"><span data-stu-id="80c0e-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="80c0e-263">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-263">Yes</span></span>|<span data-ttu-id="80c0e-264">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-264">N/A</span></span>|  
|<span data-ttu-id="80c0e-265">key</span><span class="sxs-lookup"><span data-stu-id="80c0e-265">key</span></span>|<span data-ttu-id="80c0e-266">Valeur de clé hello du cache sera stocké sous.</span><span class="sxs-lookup"><span data-stu-id="80c0e-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="80c0e-267">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-267">Yes</span></span>|<span data-ttu-id="80c0e-268">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-268">N/A</span></span>|  
|<span data-ttu-id="80c0e-269">value</span><span class="sxs-lookup"><span data-stu-id="80c0e-269">value</span></span>|<span data-ttu-id="80c0e-270">Hello toobe de valeur mis en cache.</span><span class="sxs-lookup"><span data-stu-id="80c0e-270">hello value toobe cached.</span></span>|<span data-ttu-id="80c0e-271">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-271">Yes</span></span>|<span data-ttu-id="80c0e-272">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="80c0e-273">Usage</span><span class="sxs-lookup"><span data-stu-id="80c0e-273">Usage</span></span>  
 <span data-ttu-id="80c0e-274">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="80c0e-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="80c0e-275">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="80c0e-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="80c0e-276">**Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="80c0e-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="80c0e-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span><span class="sxs-lookup"><span data-stu-id="80c0e-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="80c0e-278">Hello `cache-remove-value` supprime un élément mis en cache identifié par sa clé.</span><span class="sxs-lookup"><span data-stu-id="80c0e-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="80c0e-279">clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="80c0e-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="80c0e-280">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="80c0e-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="80c0e-281">Exemple</span><span class="sxs-lookup"><span data-stu-id="80c0e-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="80c0e-282">Éléments</span><span class="sxs-lookup"><span data-stu-id="80c0e-282">Elements</span></span>  
  
|<span data-ttu-id="80c0e-283">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-283">Name</span></span>|<span data-ttu-id="80c0e-284">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-284">Description</span></span>|<span data-ttu-id="80c0e-285">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="80c0e-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="80c0e-286">cache-remove-value</span></span>|<span data-ttu-id="80c0e-287">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="80c0e-287">Root element.</span></span>|<span data-ttu-id="80c0e-288">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="80c0e-289">Attributs</span><span class="sxs-lookup"><span data-stu-id="80c0e-289">Attributes</span></span>  
  
|<span data-ttu-id="80c0e-290">Nom</span><span class="sxs-lookup"><span data-stu-id="80c0e-290">Name</span></span>|<span data-ttu-id="80c0e-291">Description</span><span class="sxs-lookup"><span data-stu-id="80c0e-291">Description</span></span>|<span data-ttu-id="80c0e-292">Requis</span><span class="sxs-lookup"><span data-stu-id="80c0e-292">Required</span></span>|<span data-ttu-id="80c0e-293">Default</span><span class="sxs-lookup"><span data-stu-id="80c0e-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="80c0e-294">key</span><span class="sxs-lookup"><span data-stu-id="80c0e-294">key</span></span>|<span data-ttu-id="80c0e-295">clé Hello Hello mis en cache précédemment toobe valeur supprimé du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="80c0e-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="80c0e-296">Oui</span><span class="sxs-lookup"><span data-stu-id="80c0e-296">Yes</span></span>|<span data-ttu-id="80c0e-297">N/A</span><span class="sxs-lookup"><span data-stu-id="80c0e-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="80c0e-298">Usage</span><span class="sxs-lookup"><span data-stu-id="80c0e-298">Usage</span></span>  
 <span data-ttu-id="80c0e-299">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="80c0e-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="80c0e-300">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="80c0e-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="80c0e-301">**Étendues de la stratégie :** global, API, opération, produit (global, API, opération, produit)</span><span class="sxs-lookup"><span data-stu-id="80c0e-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="80c0e-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80c0e-302">Next steps</span></span>
<span data-ttu-id="80c0e-303">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="80c0e-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  