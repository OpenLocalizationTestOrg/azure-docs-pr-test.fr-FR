---
title: "aaaAzure avancée des stratégies de gestion des API | Documents Microsoft"
description: "Découvrez hello avancée des stratégies disponibles pour une utilisation dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="ad170-103">Stratégies avancées de la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="ad170-103">API Management advanced policies</span></span>
<span data-ttu-id="ad170-104">Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="ad170-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="ad170-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="ad170-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="ad170-106"><a name="AdvancedPolicies"></a> Stratégies avancées</span><span class="sxs-lookup"><span data-stu-id="ad170-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="ad170-107">[Flux de contrôle](api-management-advanced-policies.md#choose) - conditionnellement applique les instructions de stratégie basées sur les résultats d’évaluation hello booléen hello [expressions](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="ad170-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="ad170-108">[Transférer la demande](#ForwardRequest) -transfère le service principal de hello demande toohello.</span><span class="sxs-lookup"><span data-stu-id="ad170-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="ad170-109">[Limiter l’accès concurrentiel](#LimitConcurrency) -empêche entre les stratégies à partir de l’exécution en plus de hello du nombre spécifié de demandes à la fois.</span><span class="sxs-lookup"><span data-stu-id="ad170-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="ad170-110">[Journal tooEvent Hub](#log-to-eventhub) -envoie des messages hello spécifié tooan format concentrateur d’événements défini par une entité de l’enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="ad170-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="ad170-111">[Simuler la réponse](#mock-response) -abandons de l’exécution du pipeline et renvoie une réponse factices directement toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="ad170-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="ad170-112">[Recommencez](#Retry) -l’exécution de nouvelles tentatives de hello placé entre les instructions de stratégie, si et jusqu'à ce que hello condition est remplie.</span><span class="sxs-lookup"><span data-stu-id="ad170-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="ad170-113">L’exécution est répété à hello des intervalles de temps spécifié de toohello spécifié le nombre de tentatives.</span><span class="sxs-lookup"><span data-stu-id="ad170-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="ad170-114">[Retourner une réponse](#ReturnResponse) -hello retourne et de l’exécution du pipeline abandons spécifié réponse directement toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="ad170-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="ad170-115">[Envoyer une demande unidirectionnelle](#SendOneWayRequest) -envoie une demande toohello spécifié des URL sans attendre une réponse.</span><span class="sxs-lookup"><span data-stu-id="ad170-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="ad170-116">[Envoyer la demande](#SendRequest) -envoie une demande toohello spécifié l’URL.</span><span class="sxs-lookup"><span data-stu-id="ad170-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="ad170-117">[Définir le proxy HTTP](#SetHttpProxy) -vous permet de demandes tooroute transmis via un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="ad170-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="ad170-118">[Définir la méthode de demande](#SetRequestMethod) -vous permet de méthode de hello HTTP toochange pour une demande.</span><span class="sxs-lookup"><span data-stu-id="ad170-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="ad170-119">[Définir le code d’état](#SetStatus) -modifications hello HTTP état code toohello de valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="ad170-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="ad170-120">[Set variable](api-management-advanced-policies.md#set-variable) : conserve une valeur dans une variable de [contexte](api-management-policy-expressions.md#ContextVariables) nommée pour permettre d’y accéder ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ad170-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="ad170-121">[Trace](#Trace) -ajoute une chaîne en hello [API inspecteur](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) sortie.</span><span class="sxs-lookup"><span data-stu-id="ad170-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="ad170-122">[Attente](#Wait) -attend placée entre [demande d’envoi](api-management-advanced-policies.md#SendRequest), [obtenir la valeur à partir du cache](api-management-caching-policies.md#GetFromCacheByKey), ou [flux de contrôle](api-management-advanced-policies.md#choose) toocomplete stratégies avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="ad170-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="ad170-123"><a name="choose"></a> Control flow</span><span class="sxs-lookup"><span data-stu-id="ad170-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="ad170-124">Hello `choose` stratégie applique la stratégie entre crochets de construisent des instructions en fonction de résultat hello d’évaluation des expressions booléennes, similaires tooan if-then-else ou un commutateur dans un langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="ad170-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="ad170-125"><a name="ChoosePolicyStatement"></a> Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="ad170-126">Hello stratégie de flux de contrôle doit contenir au moins un `<when/>` élément.</span><span class="sxs-lookup"><span data-stu-id="ad170-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="ad170-127">Hello `<otherwise/>` élément est facultatif.</span><span class="sxs-lookup"><span data-stu-id="ad170-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="ad170-128">Dans les conditions `<when/>` éléments sont évalués dans leur ordre d’apparition dans la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="ad170-129">Déclarations de stratégie incluses dans hello tout d’abord `<when/>` élément avec l’attribut de condition est égal à `true` seront appliqués.</span><span class="sxs-lookup"><span data-stu-id="ad170-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="ad170-130">Stratégies encadrées hello `<otherwise/>` élément, le cas échéant, est appliquée si tous les Hello `<when/>` sont des attributs de l’élément condition `false`.</span><span class="sxs-lookup"><span data-stu-id="ad170-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="ad170-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="ad170-131">Examples</span></span>  
  
####  <span data-ttu-id="ad170-132"><a name="ChooseExample"></a> Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="ad170-133">Hello exemple suivant montre un [set-variable](api-management-advanced-policies.md#set-variable) stratégie et deux stratégies de flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="ad170-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="ad170-134">stratégie de variable Hello définie est dans hello section entrante et crée un `isMobile` booléenne [contexte](api-management-policy-expressions.md#ContextVariables) variable a la valeur tootrue si hello `User-Agent` demande en-tête contient le texte hello `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="ad170-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="ad170-135">stratégie de flux de contrôle de première Hello est également dans hello section entrante et applique de manière conditionnelle une des deux [définir le paramètre de chaîne de requête](api-management-transformation-policies.md#SetQueryStringParameter) stratégies en fonction de la valeur hello hello `isMobile` variable contextuelle.</span><span class="sxs-lookup"><span data-stu-id="ad170-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="ad170-136">stratégie de flux de contrôle de deuxième Hello est dans la section sortante de hello et applique de façon conditionnelle hello [tooJSON de convertir le XML](api-management-transformation-policies.md#ConvertXMLtoJSON) stratégie lorsque `isMobile` est défini trop`true`.</span><span class="sxs-lookup"><span data-stu-id="ad170-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="ad170-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-137">Example</span></span>  
 <span data-ttu-id="ad170-138">Cet exemple montre comment tooperform le filtrage de contenu en supprimant des éléments de données à partir de la réponse de hello reçu hello principal service lors de l’utilisation de hello `Starter` produit.</span><span class="sxs-lookup"><span data-stu-id="ad170-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="ad170-139">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too34:30.</span><span class="sxs-lookup"><span data-stu-id="ad170-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="ad170-140">Démarrer à 31:50 toosee une vue d’ensemble de [hello API de prévision ciel foncé](https://developer.forecast.io/) utilisée pour cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="ad170-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-141">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-141">Elements</span></span>  
  
|<span data-ttu-id="ad170-142">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-142">Element</span></span>|<span data-ttu-id="ad170-143">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-143">Description</span></span>|<span data-ttu-id="ad170-144">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-145">choose</span><span class="sxs-lookup"><span data-stu-id="ad170-145">choose</span></span>|<span data-ttu-id="ad170-146">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-146">Root element.</span></span>|<span data-ttu-id="ad170-147">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-147">Yes</span></span>|  
|<span data-ttu-id="ad170-148">when</span><span class="sxs-lookup"><span data-stu-id="ad170-148">when</span></span>|<span data-ttu-id="ad170-149">Hello toouse condition pour hello `if` ou `ifelse` parties Hello `choose` stratégie.</span><span class="sxs-lookup"><span data-stu-id="ad170-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="ad170-150">Si hello `choose` stratégie possède plusieurs `when` sections, elles sont évaluées de façon séquentielle.</span><span class="sxs-lookup"><span data-stu-id="ad170-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="ad170-151">Une fois hello `condition` d’une lorsqu’élément évalue trop`true`, aucune autre `when` conditions sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="ad170-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="ad170-152">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-152">Yes</span></span>|  
|<span data-ttu-id="ad170-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="ad170-153">otherwise</span></span>|<span data-ttu-id="ad170-154">Contient des hello stratégie extrait toobe est utilisé si aucun des hello `when` conditions ont trop`true`.</span><span class="sxs-lookup"><span data-stu-id="ad170-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="ad170-155">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-156">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-156">Attributes</span></span>  
  
|<span data-ttu-id="ad170-157">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-157">Attribute</span></span>|<span data-ttu-id="ad170-158">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-158">Description</span></span>|<span data-ttu-id="ad170-159">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ad170-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="ad170-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="ad170-161">expression booléenne de Hello ou constante tooevaluated lorsque hello contenant `when` l’instruction de stratégie est évaluée.</span><span class="sxs-lookup"><span data-stu-id="ad170-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="ad170-162">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-162">Yes</span></span>|  
  
###  <span data-ttu-id="ad170-163"><a name="ChooseUsage"></a> Utilisation</span><span class="sxs-lookup"><span data-stu-id="ad170-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="ad170-164">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-165">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-166">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-167"><a name="ForwardRequest"></a> Forward request</span><span class="sxs-lookup"><span data-stu-id="ad170-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="ad170-168">Hello `forward-request` stratégie transfère hello entrants demande toohello service principal spécifié dans la demande de hello [contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="ad170-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="ad170-169">URL du service principal Hello est spécifié dans hello API [paramètres](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) et peuvent être modifiés à l’aide de hello [définir le service principal](api-management-transformation-policies.md) stratégie.</span><span class="sxs-lookup"><span data-stu-id="ad170-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ad170-170">Supprimer les résultats de cette stratégie de demande hello ne pas transmis principal toohello service et hello des stratégies dans la section sortante de hello sont évaluées immédiatement à l’achèvement réussi de hello de stratégies de hello hello entrants de section.</span><span class="sxs-lookup"><span data-stu-id="ad170-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-171">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="ad170-172">Exemples</span><span class="sxs-lookup"><span data-stu-id="ad170-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="ad170-173">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-173">Example</span></span>  
 <span data-ttu-id="ad170-174">Hello stratégie au niveau d’API suivante transfère toutes les demandes de service principal de toohello avec un intervalle de délai d’attente de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="ad170-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="ad170-175">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-175">Example</span></span>  
 <span data-ttu-id="ad170-176">Stratégie de niveau de cette opération utilise hello `base` stratégie de serveur principal élément tooinherit hello à partir de l’étendue de niveau parent API hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="ad170-177">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-177">Example</span></span>  
 <span data-ttu-id="ad170-178">Stratégie de niveau de cette opération transfère tous les service principal toohello de demandes avec un délai d’attente de 120 explicitement et n’hérite pas de parent de hello stratégie principales au niveau d’API.</span><span class="sxs-lookup"><span data-stu-id="ad170-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="ad170-179">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-179">Example</span></span>  
 <span data-ttu-id="ad170-180">Stratégie de niveau de cette opération ne transfère pas les demandes de service principal de toohello.</span><span class="sxs-lookup"><span data-stu-id="ad170-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-181">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-181">Elements</span></span>  
  
|<span data-ttu-id="ad170-182">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-182">Element</span></span>|<span data-ttu-id="ad170-183">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-183">Description</span></span>|<span data-ttu-id="ad170-184">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="ad170-185">forward-request</span></span>|<span data-ttu-id="ad170-186">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-186">Root element.</span></span>|<span data-ttu-id="ad170-187">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-188">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-188">Attributes</span></span>  
  
|<span data-ttu-id="ad170-189">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-189">Attribute</span></span>|<span data-ttu-id="ad170-190">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-190">Description</span></span>|<span data-ttu-id="ad170-191">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-191">Required</span></span>|<span data-ttu-id="ad170-192">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="ad170-193">timeout="integer"</span></span>|<span data-ttu-id="ad170-194">intervalle de délai d’attente Hello en secondes avant que le service principal de hello appel toohello échoue.</span><span class="sxs-lookup"><span data-stu-id="ad170-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="ad170-195">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-195">No</span></span>|<span data-ttu-id="ad170-196">Aucun délai d’expiration</span><span class="sxs-lookup"><span data-stu-id="ad170-196">No timeout</span></span>|  
|<span data-ttu-id="ad170-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="ad170-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="ad170-198">Spécifie si les redirections à partir du service principal de hello sont suivies par la passerelle de hello ou retournées toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="ad170-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="ad170-199">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-199">No</span></span>|<span data-ttu-id="ad170-200">false</span><span class="sxs-lookup"><span data-stu-id="ad170-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-201">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-201">Usage</span></span>  
 <span data-ttu-id="ad170-202">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-203">**Sections de la stratégie :** backend</span><span class="sxs-lookup"><span data-stu-id="ad170-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="ad170-204">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-205"><a name="LimitConcurrency"></a> Limit concurrency</span><span class="sxs-lookup"><span data-stu-id="ad170-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="ad170-206">Hello `limit-concurrency` stratégie empêche entre les stratégies de s’exécuter par plusieurs hello du nombre spécifié de demandes à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="ad170-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="ad170-207">Fonction dépassant le seuil de hello, nouvelles demandes sont ajoutés tooa file d’attente jusqu'à ce que la longueur de file d’attente maximale hello est atteint.</span><span class="sxs-lookup"><span data-stu-id="ad170-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="ad170-208">Lorsque la file est pleine, les nouvelles requêtes échouent immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ad170-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="ad170-209"><a name="LimitConcurrencyStatement"></a> Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="ad170-210">Exemples</span><span class="sxs-lookup"><span data-stu-id="ad170-210">Examples</span></span>  
  
####  <span data-ttu-id="ad170-211"><a name="ChooseExample"></a> Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="ad170-212">Hello exemple suivant montre comment nombre toolimit de demandes transmises principal tooa selon la valeur hello d’une variable contextuelle.</span><span class="sxs-lookup"><span data-stu-id="ad170-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="ad170-213">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-213">Elements</span></span>  
  
|<span data-ttu-id="ad170-214">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-214">Element</span></span>|<span data-ttu-id="ad170-215">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-215">Description</span></span>|<span data-ttu-id="ad170-216">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="ad170-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="ad170-217">limit-concurrency</span></span>|<span data-ttu-id="ad170-218">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-218">Root element.</span></span>|<span data-ttu-id="ad170-219">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-220">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-220">Attributes</span></span>  
  
|<span data-ttu-id="ad170-221">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-221">Attribute</span></span>|<span data-ttu-id="ad170-222">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-222">Description</span></span>|<span data-ttu-id="ad170-223">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-223">Required</span></span>|<span data-ttu-id="ad170-224">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="ad170-225">key</span><span class="sxs-lookup"><span data-stu-id="ad170-225">key</span></span>|<span data-ttu-id="ad170-226">Une chaîne.</span><span class="sxs-lookup"><span data-stu-id="ad170-226">A string.</span></span> <span data-ttu-id="ad170-227">Expression autorisée.</span><span class="sxs-lookup"><span data-stu-id="ad170-227">Expression allowed.</span></span> <span data-ttu-id="ad170-228">Spécifie l’étendue d’accès concurrentiel hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="ad170-229">Peut être partagée par plusieurs stratégies.</span><span class="sxs-lookup"><span data-stu-id="ad170-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="ad170-230">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-230">Yes</span></span>|<span data-ttu-id="ad170-231">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-231">N/A</span></span>|  
|<span data-ttu-id="ad170-232">max-count</span><span class="sxs-lookup"><span data-stu-id="ad170-232">max-count</span></span>|<span data-ttu-id="ad170-233">Nombre entier.</span><span class="sxs-lookup"><span data-stu-id="ad170-233">An integer.</span></span> <span data-ttu-id="ad170-234">Spécifie un nombre maximal de demandes autorisées stratégie de hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="ad170-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="ad170-235">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-235">Yes</span></span>|<span data-ttu-id="ad170-236">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-236">N/A</span></span>|  
|<span data-ttu-id="ad170-237">timeout</span><span class="sxs-lookup"><span data-stu-id="ad170-237">timeout</span></span>|<span data-ttu-id="ad170-238">Nombre entier.</span><span class="sxs-lookup"><span data-stu-id="ad170-238">An integer.</span></span> <span data-ttu-id="ad170-239">Expression autorisée.</span><span class="sxs-lookup"><span data-stu-id="ad170-239">Expression allowed.</span></span> <span data-ttu-id="ad170-240">Spécifie le nombre de hello de secondes pendant lesquelles une demande doit attendre tooenter avant d’échouer avec une étendue de « 403 trop grand nombre de demandes »</span><span class="sxs-lookup"><span data-stu-id="ad170-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="ad170-241">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-241">No</span></span>|<span data-ttu-id="ad170-242">Infini</span><span class="sxs-lookup"><span data-stu-id="ad170-242">Infinity</span></span>|  
|<span data-ttu-id="ad170-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="ad170-243">max-queue-length</span></span>|<span data-ttu-id="ad170-244">Nombre entier.</span><span class="sxs-lookup"><span data-stu-id="ad170-244">An integer.</span></span> <span data-ttu-id="ad170-245">Expression autorisée.</span><span class="sxs-lookup"><span data-stu-id="ad170-245">Expression allowed.</span></span> <span data-ttu-id="ad170-246">Spécifie la longueur de file d’attente maximale hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="ad170-247">Les demandes entrantes lors de la tentative tooenter cette stratégie va se terminer avec « 403 trop grand nombre de demandes « immédiatement lorsque la file d’attente hello est épuisée.</span><span class="sxs-lookup"><span data-stu-id="ad170-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="ad170-248">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-248">No</span></span>|<span data-ttu-id="ad170-249">Infini</span><span class="sxs-lookup"><span data-stu-id="ad170-249">Infinity</span></span>|  
  
###  <span data-ttu-id="ad170-250"><a name="ChooseUsage"></a> Utilisation</span><span class="sxs-lookup"><span data-stu-id="ad170-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="ad170-251">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-252">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-253">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ad170-254"><a name="log-to-eventhub"></a>Journal tooEvent Hub</span><span class="sxs-lookup"><span data-stu-id="ad170-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="ad170-255">Hello `log-to-eventhub` envoie stratégie messages Bonjour spécifiés format tooan concentrateur d’événements définis par une entité de l’enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="ad170-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="ad170-256">Comme son nom l’indique, la stratégie de hello est utilisé pour l’enregistrement sélectionné demande ou réponse les informations de contexte pour l’analyse en ligne ou hors connexion.</span><span class="sxs-lookup"><span data-stu-id="ad170-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ad170-257">Pour obtenir un guide pas à pas sur la configuration d’un concentrateur d’événements et de journalisation des événements, consultez [comment toolog les événements de gestion des API avec Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="ad170-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-258">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-259">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-259">Example</span></span>  
 <span data-ttu-id="ad170-260">Toute chaîne peut être utilisée en tant que hello valeur toobe est enregistré dans les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="ad170-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="ad170-261">Dans cet exemple hello date et l’heure, le nom de service de déploiement, id de demande, adresse ip et nom de l’opération pour tous les appels entrants sont concentrateur d’événements connecté toohello journal enregistré avec hello `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="ad170-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-262">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-262">Elements</span></span>  
  
|<span data-ttu-id="ad170-263">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-263">Element</span></span>|<span data-ttu-id="ad170-264">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-264">Description</span></span>|<span data-ttu-id="ad170-265">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="ad170-266">log-to-eventhub</span></span>|<span data-ttu-id="ad170-267">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-267">Root element.</span></span> <span data-ttu-id="ad170-268">valeur Hello de cet élément est un concentrateur d’événements hello chaîne toolog tooyour.</span><span class="sxs-lookup"><span data-stu-id="ad170-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="ad170-269">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-270">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-270">Attributes</span></span>  
  
|<span data-ttu-id="ad170-271">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-271">Attribute</span></span>|<span data-ttu-id="ad170-272">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-272">Description</span></span>|<span data-ttu-id="ad170-273">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ad170-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="ad170-274">logger-id</span></span>|<span data-ttu-id="ad170-275">id de Hello Hello enregistreur d’événements inscrits auprès du service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="ad170-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="ad170-276">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-276">Yes</span></span>|  
|<span data-ttu-id="ad170-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="ad170-277">partition-id</span></span>|<span data-ttu-id="ad170-278">Spécifie l’index hello de partition hello où les messages sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="ad170-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="ad170-279">facultatif.</span><span class="sxs-lookup"><span data-stu-id="ad170-279">Optional.</span></span> <span data-ttu-id="ad170-280">Cet attribut peut ne pas être utilisé si `partition-key` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ad170-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="ad170-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="ad170-281">partition-key</span></span>|<span data-ttu-id="ad170-282">Spécifie la valeur hello utilisé pour l’attribution de partition lorsque des messages sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="ad170-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="ad170-283">facultatif.</span><span class="sxs-lookup"><span data-stu-id="ad170-283">Optional.</span></span> <span data-ttu-id="ad170-284">Cet attribut peut ne pas être utilisé si `partition-id` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ad170-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-285">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-285">Usage</span></span>  
 <span data-ttu-id="ad170-286">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-287">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-288">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ad170-289"><a name="mock-response"></a> Réponse factice</span><span class="sxs-lookup"><span data-stu-id="ad170-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="ad170-290">Hello `mock-response`, en tant que nom de hello implique, est utilisé toomock API et les opérations.</span><span class="sxs-lookup"><span data-stu-id="ad170-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="ad170-291">Il interrompt l’exécution du pipeline normal et retourne un appelant toohello de réponse factices.</span><span class="sxs-lookup"><span data-stu-id="ad170-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="ad170-292">stratégie de Hello tente toujours de réponses tooreturn de plus haute fidélité.</span><span class="sxs-lookup"><span data-stu-id="ad170-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="ad170-293">Elle préfère les exemples de contenu de réponse, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="ad170-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="ad170-294">Elle génère des exemples de réponses à partir de schémas, lorsque les schémas sont fournis et les exemples ne le sont pas.</span><span class="sxs-lookup"><span data-stu-id="ad170-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="ad170-295">Si aucun exemple ou schéma n’est trouvé, des réponses sans contenu sont retournées.</span><span class="sxs-lookup"><span data-stu-id="ad170-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-296">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="ad170-297">Exemples</span><span class="sxs-lookup"><span data-stu-id="ad170-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-298">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-298">Elements</span></span>  
  
|<span data-ttu-id="ad170-299">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-299">Element</span></span>|<span data-ttu-id="ad170-300">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-300">Description</span></span>|<span data-ttu-id="ad170-301">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="ad170-302">mock-response</span></span>|<span data-ttu-id="ad170-303">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-303">Root element.</span></span>|<span data-ttu-id="ad170-304">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-305">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-305">Attributes</span></span>  
  
|<span data-ttu-id="ad170-306">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-306">Attribute</span></span>|<span data-ttu-id="ad170-307">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-307">Description</span></span>|<span data-ttu-id="ad170-308">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-308">Required</span></span>|<span data-ttu-id="ad170-309">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="ad170-310">status-code</span><span class="sxs-lookup"><span data-stu-id="ad170-310">status-code</span></span>|<span data-ttu-id="ad170-311">Spécifie le code d’état de réponse et exemple tooselect utilisé ou le schéma.</span><span class="sxs-lookup"><span data-stu-id="ad170-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="ad170-312">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-312">No</span></span>|<span data-ttu-id="ad170-313">200</span><span class="sxs-lookup"><span data-stu-id="ad170-313">200</span></span>|  
|<span data-ttu-id="ad170-314">content-type</span><span class="sxs-lookup"><span data-stu-id="ad170-314">content-type</span></span>|<span data-ttu-id="ad170-315">Spécifie `Content-Type` valeur d’en-tête de réponse et est utilisé tooselect exemple ou le schéma.</span><span class="sxs-lookup"><span data-stu-id="ad170-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="ad170-316">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-316">No</span></span>|<span data-ttu-id="ad170-317">Aucune</span><span class="sxs-lookup"><span data-stu-id="ad170-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-318">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-318">Usage</span></span>  
 <span data-ttu-id="ad170-319">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-320">**Sections de la stratégie :** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="ad170-321">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="ad170-322"><a name="Retry"></a> Retry</span><span class="sxs-lookup"><span data-stu-id="ad170-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="ad170-323">Hello `retry` stratégie exécute une fois les stratégies de ses enfants et puis de tentatives de leur exécution jusqu'à ce que la nouvelle tentative de hello `condition` devient `false` ou réessayez `count` est épuisé.</span><span class="sxs-lookup"><span data-stu-id="ad170-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-324">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-325">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-325">Example</span></span>  
 <span data-ttu-id="ad170-326">Bonjour suivant exemple demande forewarding est retentée des tooten heures à l’aide d’algorithme de tentative exponentielle.</span><span class="sxs-lookup"><span data-stu-id="ad170-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="ad170-327">Étant donné que `first-fast-retry` a la valeur toofalse, toutes les nouvelles tentatives sont l’algorithme de tentative de sujet toohello exponsntial.</span><span class="sxs-lookup"><span data-stu-id="ad170-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-328">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-328">Elements</span></span>  
  
|<span data-ttu-id="ad170-329">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-329">Element</span></span>|<span data-ttu-id="ad170-330">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-330">Description</span></span>|<span data-ttu-id="ad170-331">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-332">retry</span><span class="sxs-lookup"><span data-stu-id="ad170-332">retry</span></span>|<span data-ttu-id="ad170-333">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-333">Root element.</span></span> <span data-ttu-id="ad170-334">Peut contenir n’importe quelle autre stratégie sous forme d’élément enfant.</span><span class="sxs-lookup"><span data-stu-id="ad170-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="ad170-335">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-336">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-336">Attributes</span></span>  
  
|<span data-ttu-id="ad170-337">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-337">Attribute</span></span>|<span data-ttu-id="ad170-338">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-338">Description</span></span>|<span data-ttu-id="ad170-339">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-339">Required</span></span>|<span data-ttu-id="ad170-340">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-341">condition</span><span class="sxs-lookup"><span data-stu-id="ad170-341">condition</span></span>|<span data-ttu-id="ad170-342">[Expression](api-management-policy-expressions.md) ou littéral booléen spécifiant si les nouvelles tentatives doivent être arrêtées (`false`) ou poursuivies (`true`).</span><span class="sxs-lookup"><span data-stu-id="ad170-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="ad170-343">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-343">Yes</span></span>|<span data-ttu-id="ad170-344">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-344">N/A</span></span>|  
|<span data-ttu-id="ad170-345">count</span><span class="sxs-lookup"><span data-stu-id="ad170-345">count</span></span>|<span data-ttu-id="ad170-346">Un nombre positif spécifiant hello le nombre maximal de nouvelles tentatives tooattempt.</span><span class="sxs-lookup"><span data-stu-id="ad170-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="ad170-347">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-347">Yes</span></span>|<span data-ttu-id="ad170-348">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-348">N/A</span></span>|  
|<span data-ttu-id="ad170-349">interval</span><span class="sxs-lookup"><span data-stu-id="ad170-349">interval</span></span>|<span data-ttu-id="ad170-350">Un nombre positif, en secondes, en spécifiant le délai d’attente hello entre chaque tentative hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="ad170-351">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-351">Yes</span></span>|<span data-ttu-id="ad170-352">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-352">N/A</span></span>|  
|<span data-ttu-id="ad170-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="ad170-353">max-interval</span></span>|<span data-ttu-id="ad170-354">Un nombre positif, en secondes, en spécifiant le délai d’attente maximal du hello entre chaque tentative hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="ad170-355">Il est tooimplement utilisé un algorithme de nouvelle tentative exponentielle.</span><span class="sxs-lookup"><span data-stu-id="ad170-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="ad170-356">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-356">No</span></span>|<span data-ttu-id="ad170-357">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-357">N/A</span></span>|  
|<span data-ttu-id="ad170-358">delta</span><span class="sxs-lookup"><span data-stu-id="ad170-358">delta</span></span>|<span data-ttu-id="ad170-359">Un nombre positif, en secondes spécifiant l’incrément d’intervalle d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="ad170-360">Il s’agit des algorithmes de nouvelle tentative linéaire et exponentielle hello tooimplement utilisé.</span><span class="sxs-lookup"><span data-stu-id="ad170-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="ad170-361">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-361">No</span></span>|<span data-ttu-id="ad170-362">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-362">N/A</span></span>|  
|<span data-ttu-id="ad170-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="ad170-363">first-fast-retry</span></span>|<span data-ttu-id="ad170-364">Si défini trop `true` , hello première nouvelle tentative est effectuée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ad170-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="ad170-365">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="ad170-366">Lorsque uniquement hello `interval` est spécifié, **fixe** nouvelles tentatives d’intervalle sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="ad170-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="ad170-367">Lorsque uniquement hello `interval` et `delta` sont spécifiés, un **linéaire** algorithme de tentative d’intervalle est utilisé, où les temps d’attente entre deux tentatives est calculé hello en fonction de formule - suivante `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="ad170-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="ad170-368">Hello lorsque `interval`, `max-interval` et `delta` sont spécifiés, **exponentielle** algorithme de tentative d’intervalle est appliqué, où les temps d’attente hello entre les tentatives de hello augmentent de manière exponentielle à partir de la valeur hello `interval`toohello valeur `max-interval` selon toohello suivant forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="ad170-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="ad170-369">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-369">Usage</span></span>  
 <span data-ttu-id="ad170-370">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="ad170-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="ad170-371">Notez que des restrictions d’utilisation des stratégies enfants seront héritées par cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="ad170-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="ad170-372">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-373">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-374"><a name="ReturnResponse"></a> Return response</span><span class="sxs-lookup"><span data-stu-id="ad170-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="ad170-375">Hello `return-response` stratégie interrompt l’exécution du pipeline et retourne une valeur par défaut ou un appelant toohello de réponse personnalisée.</span><span class="sxs-lookup"><span data-stu-id="ad170-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="ad170-376">La réponse par défaut est `200 OK` sans corps.</span><span class="sxs-lookup"><span data-stu-id="ad170-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="ad170-377">La réponse personnalisée peut être spécifiée par le biais d’instructions de stratégie ou d’une variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="ad170-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="ad170-378">Lorsque les deux sont fournis, réponse hello contenue dans la variable de contexte hello est modifié par les instructions de stratégie hello avant d’être retourné à l’appelant de toohello.</span><span class="sxs-lookup"><span data-stu-id="ad170-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-379">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-380">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-381">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-381">Elements</span></span>  
  
|<span data-ttu-id="ad170-382">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-382">Element</span></span>|<span data-ttu-id="ad170-383">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-383">Description</span></span>|<span data-ttu-id="ad170-384">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-385">return-response</span><span class="sxs-lookup"><span data-stu-id="ad170-385">return-response</span></span>|<span data-ttu-id="ad170-386">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-386">Root element.</span></span>|<span data-ttu-id="ad170-387">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-387">Yes</span></span>|  
|<span data-ttu-id="ad170-388">set-header</span><span class="sxs-lookup"><span data-stu-id="ad170-388">set-header</span></span>|<span data-ttu-id="ad170-389">Instruction de stratégie [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="ad170-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="ad170-390">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-390">No</span></span>|  
|<span data-ttu-id="ad170-391">set-body</span><span class="sxs-lookup"><span data-stu-id="ad170-391">set-body</span></span>|<span data-ttu-id="ad170-392">Instruction de stratégie [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="ad170-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="ad170-393">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-393">No</span></span>|  
|<span data-ttu-id="ad170-394">set-status</span><span class="sxs-lookup"><span data-stu-id="ad170-394">set-status</span></span>|<span data-ttu-id="ad170-395">Instruction de stratégie [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="ad170-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="ad170-396">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-397">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-397">Attributes</span></span>  
  
|<span data-ttu-id="ad170-398">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-398">Attribute</span></span>|<span data-ttu-id="ad170-399">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-399">Description</span></span>|<span data-ttu-id="ad170-400">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ad170-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="ad170-401">response-variable-name</span></span>|<span data-ttu-id="ad170-402">Hello nom de variable de contexte hello référencé à partir, par exemple, un en amont [demande d’envoi](api-management-advanced-policies.md#SendRequest) stratégie et contenant un `Response` objet</span><span class="sxs-lookup"><span data-stu-id="ad170-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="ad170-403">facultatif.</span><span class="sxs-lookup"><span data-stu-id="ad170-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-404">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-404">Usage</span></span>  
 <span data-ttu-id="ad170-405">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-406">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-407">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-408"><a name="SendOneWayRequest"></a> Send one way request</span><span class="sxs-lookup"><span data-stu-id="ad170-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="ad170-409">Hello `send-one-way-request` stratégie envoie la demande hello fourni toohello spécifié des URL sans attendre une réponse.</span><span class="sxs-lookup"><span data-stu-id="ad170-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-410">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-411">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-411">Example</span></span>  
 <span data-ttu-id="ad170-412">Cette stratégie de l’exemple montre un exemple d’utilisation hello `send-one-way-request` stratégie toosend message tooa Slack salle de conversation si hello code de réponse HTTP est supérieur ou égal too500.</span><span class="sxs-lookup"><span data-stu-id="ad170-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="ad170-413">Pour plus d’informations sur cet exemple, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="ad170-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-414">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-414">Elements</span></span>  
  
|<span data-ttu-id="ad170-415">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-415">Element</span></span>|<span data-ttu-id="ad170-416">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-416">Description</span></span>|<span data-ttu-id="ad170-417">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="ad170-418">send-one-way-request</span></span>|<span data-ttu-id="ad170-419">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-419">Root element.</span></span>|<span data-ttu-id="ad170-420">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-420">Yes</span></span>|  
|<span data-ttu-id="ad170-421">url</span><span class="sxs-lookup"><span data-stu-id="ad170-421">url</span></span>|<span data-ttu-id="ad170-422">Hello l’URL de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-422">hello URL of hello request.</span></span>|<span data-ttu-id="ad170-423">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="ad170-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ad170-424">method</span><span class="sxs-lookup"><span data-stu-id="ad170-424">method</span></span>|<span data-ttu-id="ad170-425">méthode HTTP pour la demande de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="ad170-426">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="ad170-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ad170-427">en-tête</span><span class="sxs-lookup"><span data-stu-id="ad170-427">header</span></span>|<span data-ttu-id="ad170-428">En-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="ad170-428">Request header.</span></span> <span data-ttu-id="ad170-429">Utilisez un élément d’en-tête pour chaque en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="ad170-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="ad170-430">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-430">No</span></span>|  
|<span data-ttu-id="ad170-431">body</span><span class="sxs-lookup"><span data-stu-id="ad170-431">body</span></span>|<span data-ttu-id="ad170-432">corps de la demande Hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-432">hello request body.</span></span>|<span data-ttu-id="ad170-433">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-434">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-434">Attributes</span></span>  
  
|<span data-ttu-id="ad170-435">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-435">Attribute</span></span>|<span data-ttu-id="ad170-436">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-436">Description</span></span>|<span data-ttu-id="ad170-437">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-437">Required</span></span>|<span data-ttu-id="ad170-438">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="ad170-439">mode="string"</span></span>|<span data-ttu-id="ad170-440">Détermine s’il s’agit d’une nouvelle demande ou une copie de la demande en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="ad170-441">En mode de sortie, mode = copie n’initialise pas le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="ad170-442">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-442">No</span></span>|<span data-ttu-id="ad170-443">Nouveau</span><span class="sxs-lookup"><span data-stu-id="ad170-443">New</span></span>|  
|<span data-ttu-id="ad170-444">name</span><span class="sxs-lookup"><span data-stu-id="ad170-444">name</span></span>|<span data-ttu-id="ad170-445">Spécifie le nom hello de hello en-tête toobe ensemble.</span><span class="sxs-lookup"><span data-stu-id="ad170-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="ad170-446">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-446">Yes</span></span>|<span data-ttu-id="ad170-447">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-447">N/A</span></span>|  
|<span data-ttu-id="ad170-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="ad170-448">exists-action</span></span>|<span data-ttu-id="ad170-449">Spécifie quelles tootake action lorsque hello en-tête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="ad170-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="ad170-450">Cet attribut doit avoir une des valeurs suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="ad170-451">-remplacer - valeur de hello remplace d’en-tête existant de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="ad170-452">-ignorer - ne remplace pas la valeur d’en-tête hello existant.</span><span class="sxs-lookup"><span data-stu-id="ad170-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="ad170-453">-Ajouter - ajoute la valeur d’en-tête existant hello valeur toohello.</span><span class="sxs-lookup"><span data-stu-id="ad170-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="ad170-454">-Supprimer - supprime les en-tête de hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="ad170-455">Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans l’en-tête de hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="ad170-456">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-456">No</span></span>|<span data-ttu-id="ad170-457">override</span><span class="sxs-lookup"><span data-stu-id="ad170-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-458">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-458">Usage</span></span>  
 <span data-ttu-id="ad170-459">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-460">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-461">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-462"><a name="SendRequest"></a> Send request</span><span class="sxs-lookup"><span data-stu-id="ad170-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="ad170-463">Hello `send-request` stratégie envoie la demande hello fourni toohello spécifié l’URL, en attente n’est plus que hello définie la valeur de délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="ad170-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-464">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-465">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-465">Example</span></span>  
 <span data-ttu-id="ad170-466">Cet exemple montre une façon tooverify un jeton de référence avec un serveur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="ad170-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="ad170-467">Pour plus d’informations sur cet exemple, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="ad170-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-468">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-468">Elements</span></span>  
  
|<span data-ttu-id="ad170-469">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-469">Element</span></span>|<span data-ttu-id="ad170-470">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-470">Description</span></span>|<span data-ttu-id="ad170-471">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-472">send-request</span><span class="sxs-lookup"><span data-stu-id="ad170-472">send-request</span></span>|<span data-ttu-id="ad170-473">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-473">Root element.</span></span>|<span data-ttu-id="ad170-474">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-474">Yes</span></span>|  
|<span data-ttu-id="ad170-475">url</span><span class="sxs-lookup"><span data-stu-id="ad170-475">url</span></span>|<span data-ttu-id="ad170-476">Hello l’URL de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-476">hello URL of hello request.</span></span>|<span data-ttu-id="ad170-477">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="ad170-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ad170-478">method</span><span class="sxs-lookup"><span data-stu-id="ad170-478">method</span></span>|<span data-ttu-id="ad170-479">méthode HTTP pour la demande de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="ad170-480">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="ad170-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="ad170-481">en-tête</span><span class="sxs-lookup"><span data-stu-id="ad170-481">header</span></span>|<span data-ttu-id="ad170-482">En-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="ad170-482">Request header.</span></span> <span data-ttu-id="ad170-483">Utilisez un élément d’en-tête pour chaque en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="ad170-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="ad170-484">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-484">No</span></span>|  
|<span data-ttu-id="ad170-485">body</span><span class="sxs-lookup"><span data-stu-id="ad170-485">body</span></span>|<span data-ttu-id="ad170-486">corps de la demande Hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-486">hello request body.</span></span>|<span data-ttu-id="ad170-487">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-488">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-488">Attributes</span></span>  
  
|<span data-ttu-id="ad170-489">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-489">Attribute</span></span>|<span data-ttu-id="ad170-490">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-490">Description</span></span>|<span data-ttu-id="ad170-491">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-491">Required</span></span>|<span data-ttu-id="ad170-492">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="ad170-493">mode="string"</span></span>|<span data-ttu-id="ad170-494">Détermine s’il s’agit d’une nouvelle demande ou une copie de la demande en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="ad170-495">En mode de sortie, mode = copie n’initialise pas le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="ad170-496">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-496">No</span></span>|<span data-ttu-id="ad170-497">Nouveau</span><span class="sxs-lookup"><span data-stu-id="ad170-497">New</span></span>|  
|<span data-ttu-id="ad170-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="ad170-498">response-variable-name="string"</span></span>|<span data-ttu-id="ad170-499">En son absence, `context.Response` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ad170-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="ad170-500">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-500">No</span></span>|<span data-ttu-id="ad170-501">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-501">N/A</span></span>|  
|<span data-ttu-id="ad170-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="ad170-502">timeout="integer"</span></span>|<span data-ttu-id="ad170-503">intervalle de délai d’attente Hello en secondes avant l’appel de hello toohello URL échoue.</span><span class="sxs-lookup"><span data-stu-id="ad170-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="ad170-504">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-504">No</span></span>|<span data-ttu-id="ad170-505">60</span><span class="sxs-lookup"><span data-stu-id="ad170-505">60</span></span>|  
|<span data-ttu-id="ad170-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="ad170-506">ignore-error</span></span>|<span data-ttu-id="ad170-507">Si la valeur true et hello demande entraîne une erreur :</span><span class="sxs-lookup"><span data-stu-id="ad170-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="ad170-508">- Si response-variable-name a été spécifié, il contiendra une valeur Null.</span><span class="sxs-lookup"><span data-stu-id="ad170-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="ad170-509">- Si response-variable-nam n’est pas spécifié, context.Request ne sera pas mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ad170-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="ad170-510">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-510">No</span></span>|<span data-ttu-id="ad170-511">false</span><span class="sxs-lookup"><span data-stu-id="ad170-511">false</span></span>|  
|<span data-ttu-id="ad170-512">name</span><span class="sxs-lookup"><span data-stu-id="ad170-512">name</span></span>|<span data-ttu-id="ad170-513">Spécifie le nom hello de hello en-tête toobe ensemble.</span><span class="sxs-lookup"><span data-stu-id="ad170-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="ad170-514">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-514">Yes</span></span>|<span data-ttu-id="ad170-515">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-515">N/A</span></span>|  
|<span data-ttu-id="ad170-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="ad170-516">exists-action</span></span>|<span data-ttu-id="ad170-517">Spécifie quelles tootake action lorsque hello en-tête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="ad170-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="ad170-518">Cet attribut doit avoir une des valeurs suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="ad170-519">-remplacer - valeur de hello remplace d’en-tête existant de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="ad170-520">-ignorer - ne remplace pas la valeur d’en-tête hello existant.</span><span class="sxs-lookup"><span data-stu-id="ad170-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="ad170-521">-Ajouter - ajoute la valeur d’en-tête existant hello valeur toohello.</span><span class="sxs-lookup"><span data-stu-id="ad170-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="ad170-522">-Supprimer - supprime les en-tête de hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="ad170-523">Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans l’en-tête de hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="ad170-524">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-524">No</span></span>|<span data-ttu-id="ad170-525">override</span><span class="sxs-lookup"><span data-stu-id="ad170-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-526">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-526">Usage</span></span>  
 <span data-ttu-id="ad170-527">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-528">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-529">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-530"><a name="SetHttpProxy"></a> Définir le proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="ad170-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="ad170-531">Hello `proxy` stratégie vous permet de tooroute les toobackends de demandes transmises via un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="ad170-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="ad170-532">Seul le protocole HTTP (pas le protocole HTTPS) est prise en charge entre hello et de proxy de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="ad170-533">Authentification de base et NTLM uniquement.</span><span class="sxs-lookup"><span data-stu-id="ad170-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-534">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-535">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-535">Example</span></span>  
<span data-ttu-id="ad170-536">Notez que hello [propriétés](api-management-howto-properties.md) en tant que valeurs de hello tooavoid nom d’utilisateur et mot de passe le stockage des informations sensibles dans le document de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-537">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-537">Elements</span></span>  
  
|<span data-ttu-id="ad170-538">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-538">Element</span></span>|<span data-ttu-id="ad170-539">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-539">Description</span></span>|<span data-ttu-id="ad170-540">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-541">proxy</span><span class="sxs-lookup"><span data-stu-id="ad170-541">proxy</span></span>|<span data-ttu-id="ad170-542">Élément racine</span><span class="sxs-lookup"><span data-stu-id="ad170-542">Root element</span></span>|<span data-ttu-id="ad170-543">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="ad170-544">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-544">Attributes</span></span>  
  
|<span data-ttu-id="ad170-545">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-545">Attribute</span></span>|<span data-ttu-id="ad170-546">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-546">Description</span></span>|<span data-ttu-id="ad170-547">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-547">Required</span></span>|<span data-ttu-id="ad170-548">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-549">url="chaîne"</span><span class="sxs-lookup"><span data-stu-id="ad170-549">url="string"</span></span>|<span data-ttu-id="ad170-550">URL du proxy sous forme http://Host :port) hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="ad170-551">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-551">Yes</span></span>|<span data-ttu-id="ad170-552">N/A </span><span class="sxs-lookup"><span data-stu-id="ad170-552">N/A</span></span>|  
|<span data-ttu-id="ad170-553">username="chaîne"</span><span class="sxs-lookup"><span data-stu-id="ad170-553">username="string"</span></span>|<span data-ttu-id="ad170-554">Toobe de nom d’utilisateur utilisé pour l’authentification avec le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="ad170-555">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-555">No</span></span>|<span data-ttu-id="ad170-556">N/A </span><span class="sxs-lookup"><span data-stu-id="ad170-556">N/A</span></span>|  
|<span data-ttu-id="ad170-557">password="chaîne"</span><span class="sxs-lookup"><span data-stu-id="ad170-557">password="string"</span></span>|<span data-ttu-id="ad170-558">Toobe de mot de passe utilisé pour l’authentification avec le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="ad170-559">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-559">No</span></span>|<span data-ttu-id="ad170-560">N/A </span><span class="sxs-lookup"><span data-stu-id="ad170-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="ad170-561">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-561">Usage</span></span>  
 <span data-ttu-id="ad170-562">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-563">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="ad170-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="ad170-564">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ad170-565"><a name="SetRequestMethod"></a> Set request method</span><span class="sxs-lookup"><span data-stu-id="ad170-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="ad170-566">Hello `set-method` stratégie vous permet de méthode de demande toochange hello HTTP pour une demande.</span><span class="sxs-lookup"><span data-stu-id="ad170-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-567">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-568">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-568">Example</span></span>  
 <span data-ttu-id="ad170-569">Cet exemple de stratégie qui utilise hello `set-method` stratégie montre un exemple d’envoi d’une salle de conversation Slack message tooa si hello code de réponse HTTP est supérieur à ou égal too500.</span><span class="sxs-lookup"><span data-stu-id="ad170-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="ad170-570">Pour plus d’informations sur cet exemple, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="ad170-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-571">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-571">Elements</span></span>  
  
|<span data-ttu-id="ad170-572">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-572">Element</span></span>|<span data-ttu-id="ad170-573">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-573">Description</span></span>|<span data-ttu-id="ad170-574">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-575">set-method</span><span class="sxs-lookup"><span data-stu-id="ad170-575">set-method</span></span>|<span data-ttu-id="ad170-576">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-576">Root element.</span></span> <span data-ttu-id="ad170-577">valeur Hello d’élément de hello spécifie la méthode HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="ad170-578">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-579">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-579">Usage</span></span>  
 <span data-ttu-id="ad170-580">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-581">**Sections de la stratégie :** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="ad170-582">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-583"><a name="SetStatus"></a> Set status code</span><span class="sxs-lookup"><span data-stu-id="ad170-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="ad170-584">Hello `set-status` stratégie jeux hello HTTP état code toohello de valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="ad170-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-585">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-586">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-586">Example</span></span>  
 <span data-ttu-id="ad170-587">Cet exemple montre comment tooreturn une réponse 401 si le jeton d’autorisation hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="ad170-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="ad170-588">Pour plus d’informations, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="ad170-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-589">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-589">Elements</span></span>  
  
|<span data-ttu-id="ad170-590">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-590">Element</span></span>|<span data-ttu-id="ad170-591">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-591">Description</span></span>|<span data-ttu-id="ad170-592">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-593">set-status</span><span class="sxs-lookup"><span data-stu-id="ad170-593">set-status</span></span>|<span data-ttu-id="ad170-594">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-594">Root element.</span></span>|<span data-ttu-id="ad170-595">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-596">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-596">Attributes</span></span>  
  
|<span data-ttu-id="ad170-597">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-597">Attribute</span></span>|<span data-ttu-id="ad170-598">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-598">Description</span></span>|<span data-ttu-id="ad170-599">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-599">Required</span></span>|<span data-ttu-id="ad170-600">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="ad170-601">code="integer"</span></span>|<span data-ttu-id="ad170-602">tooreturn de code de statut HTTP de Hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="ad170-603">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-603">Yes</span></span>|<span data-ttu-id="ad170-604">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-604">N/A</span></span>|  
|<span data-ttu-id="ad170-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="ad170-605">reason="string"</span></span>|<span data-ttu-id="ad170-606">Description du motif hello pour retourner le code d’état hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="ad170-607">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-607">Yes</span></span>|<span data-ttu-id="ad170-608">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-609">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-609">Usage</span></span>  
 <span data-ttu-id="ad170-610">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-611">**Sections de la stratégie :** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-612">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="ad170-613"><a name="set-variable"></a> Set variable</span><span class="sxs-lookup"><span data-stu-id="ad170-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="ad170-614">Hello `set-variable` stratégie déclare un [contexte](api-management-policy-expressions.md#ContextVariables) variable et lui assigne une valeur spécifiée via une [expression](api-management-policy-expressions.md) ou un littéral de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ad170-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="ad170-615">Si expression de hello contient un littéral, il sera converti tooa hello et la chaîne de valeur de hello sera `System.String`.</span><span class="sxs-lookup"><span data-stu-id="ad170-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="ad170-616"><a name="set-variablePolicyStatement"></a> Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="ad170-617"><a name="set-variableExample"></a> Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="ad170-618">exemple Hello illustre une stratégie de variable définie dans hello entrants de section.</span><span class="sxs-lookup"><span data-stu-id="ad170-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="ad170-619">Cette stratégie de variable définie crée un `isMobile` booléenne [contexte](api-management-policy-expressions.md#ContextVariables) variable a la valeur tootrue si hello `User-Agent` demande en-tête contient le texte hello `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="ad170-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-620">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-620">Elements</span></span>  
  
|<span data-ttu-id="ad170-621">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-621">Element</span></span>|<span data-ttu-id="ad170-622">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-622">Description</span></span>|<span data-ttu-id="ad170-623">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="ad170-624">set-variable</span></span>|<span data-ttu-id="ad170-625">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-625">Root element.</span></span>|<span data-ttu-id="ad170-626">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-627">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-627">Attributes</span></span>  
  
|<span data-ttu-id="ad170-628">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-628">Attribute</span></span>|<span data-ttu-id="ad170-629">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-629">Description</span></span>|<span data-ttu-id="ad170-630">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="ad170-631">name</span><span class="sxs-lookup"><span data-stu-id="ad170-631">name</span></span>|<span data-ttu-id="ad170-632">nom de Hello de variable de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-632">hello name of hello variable.</span></span>|<span data-ttu-id="ad170-633">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-633">Yes</span></span>|  
|<span data-ttu-id="ad170-634">value</span><span class="sxs-lookup"><span data-stu-id="ad170-634">value</span></span>|<span data-ttu-id="ad170-635">valeur de Hello de variable de hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-635">hello value of hello variable.</span></span> <span data-ttu-id="ad170-636">Peut être une expression ou une valeur littérale.</span><span class="sxs-lookup"><span data-stu-id="ad170-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="ad170-637">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-638">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-638">Usage</span></span>  
 <span data-ttu-id="ad170-639">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-640">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-641">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="ad170-642"><a name="set-variableAllowedTypes"></a> Types autorisés</span><span class="sxs-lookup"><span data-stu-id="ad170-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="ad170-643">Les expressions utilisées dans hello `set-variable` stratégie doit retourner hello les types de base suivants.</span><span class="sxs-lookup"><span data-stu-id="ad170-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="ad170-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="ad170-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="ad170-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="ad170-645">System.SByte</span></span>  
  
-   <span data-ttu-id="ad170-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="ad170-646">System.Byte</span></span>  
  
-   <span data-ttu-id="ad170-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="ad170-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="ad170-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="ad170-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="ad170-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="ad170-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="ad170-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="ad170-650">System.Int16</span></span>  
  
-   <span data-ttu-id="ad170-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="ad170-651">System.Int32</span></span>  
  
-   <span data-ttu-id="ad170-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="ad170-652">System.Int64</span></span>  
  
-   <span data-ttu-id="ad170-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="ad170-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="ad170-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="ad170-654">System.Single</span></span>  
  
-   <span data-ttu-id="ad170-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="ad170-655">System.Double</span></span>  
  
-   <span data-ttu-id="ad170-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="ad170-656">System.Guid</span></span>  
  
-   <span data-ttu-id="ad170-657">System.String</span><span class="sxs-lookup"><span data-stu-id="ad170-657">System.String</span></span>  
  
-   <span data-ttu-id="ad170-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="ad170-658">System.Char</span></span>  
  
-   <span data-ttu-id="ad170-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="ad170-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="ad170-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ad170-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="ad170-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="ad170-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="ad170-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="ad170-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="ad170-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="ad170-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="ad170-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="ad170-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="ad170-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="ad170-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="ad170-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="ad170-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="ad170-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="ad170-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="ad170-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="ad170-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="ad170-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="ad170-669">System.Single?</span></span>  
  
-   <span data-ttu-id="ad170-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="ad170-670">System.Double?</span></span>  
  
-   <span data-ttu-id="ad170-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="ad170-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="ad170-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="ad170-672">System.String?</span></span>  
  
-   <span data-ttu-id="ad170-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="ad170-673">System.Char?</span></span>  
  
-   <span data-ttu-id="ad170-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="ad170-674">System.DateTime?</span></span>  

##  <span data-ttu-id="ad170-675"><a name="Trace"></a> Trace</span><span class="sxs-lookup"><span data-stu-id="ad170-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="ad170-676">Hello `trace` stratégie ajoute une chaîne en hello [API inspecteur](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) sortie.</span><span class="sxs-lookup"><span data-stu-id="ad170-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="ad170-677">Hello s’appliquera uniquement lorsque le traçage est déclenché, c'est-à-dire `Ocp-Apim-Trace` en-tête de demande est présent et défini trop`true` et `Ocp-Apim-Subscription-Key` en-tête de demande est présent et contient une clé valide associée au compte d’administrateur hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-678">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-679">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-679">Elements</span></span>  
  
|<span data-ttu-id="ad170-680">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-680">Element</span></span>|<span data-ttu-id="ad170-681">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-681">Description</span></span>|<span data-ttu-id="ad170-682">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-683">trace</span><span class="sxs-lookup"><span data-stu-id="ad170-683">trace</span></span>|<span data-ttu-id="ad170-684">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-684">Root element.</span></span>|<span data-ttu-id="ad170-685">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-686">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-686">Attributes</span></span>  
  
|<span data-ttu-id="ad170-687">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-687">Attribute</span></span>|<span data-ttu-id="ad170-688">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-688">Description</span></span>|<span data-ttu-id="ad170-689">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-689">Required</span></span>|<span data-ttu-id="ad170-690">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-691">source</span><span class="sxs-lookup"><span data-stu-id="ad170-691">source</span></span>|<span data-ttu-id="ad170-692">Visionneuse de trace toohello explicite littéral de chaîne et en spécifiant source hello de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="ad170-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="ad170-693">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-693">Yes</span></span>|<span data-ttu-id="ad170-694">N/A</span><span class="sxs-lookup"><span data-stu-id="ad170-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-695">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-695">Usage</span></span>  
 <span data-ttu-id="ad170-696">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="ad170-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="ad170-697">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="ad170-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="ad170-698">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="ad170-699"><a name="Wait"></a> Wait</span><span class="sxs-lookup"><span data-stu-id="ad170-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="ad170-700">Hello `wait` stratégie exécute ses stratégies enfants immédiats en parallèle et attend que tout ou une de ses toocomplete de stratégies enfants immédiats avant la fin.</span><span class="sxs-lookup"><span data-stu-id="ad170-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="ad170-701">Hello attente stratégie peut posséder ses stratégies enfants immédiats [demande d’envoi](api-management-advanced-policies.md#SendRequest), [obtenir la valeur à partir du cache](api-management-caching-policies.md#GetFromCacheByKey), et [flux de contrôle](api-management-advanced-policies.md#choose) stratégies.</span><span class="sxs-lookup"><span data-stu-id="ad170-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="ad170-702">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="ad170-703">Exemple</span><span class="sxs-lookup"><span data-stu-id="ad170-703">Example</span></span>  
 <span data-ttu-id="ad170-704">Bonjour exemple il y a deux `choose` stratégies en tant que stratégies des enfants immédiats de hello `wait` stratégie.</span><span class="sxs-lookup"><span data-stu-id="ad170-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="ad170-705">Ces deux stratégies `choose` s’exécutent en parallèle.</span><span class="sxs-lookup"><span data-stu-id="ad170-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="ad170-706">Chaque `choose` stratégie tente tooretrieve une valeur mise en cache.</span><span class="sxs-lookup"><span data-stu-id="ad170-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="ad170-707">S’il existe une absence dans le cache, un service principal est tooprovide hello appelée « valeur ».</span><span class="sxs-lookup"><span data-stu-id="ad170-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="ad170-708">Dans cette hello exemple `wait` stratégie ne se termine pas tant que toutes les stratégies de ses enfants immédiats d’effectuent, car hello `for` attribut est défini trop`all`.</span><span class="sxs-lookup"><span data-stu-id="ad170-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="ad170-709">Dans cette variables de contexte exemple hello (`execute-branch-one`, `value-one`, `execute-branch-two`, et `value-two`) sont déclarés en dehors de la portée de hello de cet exemple de stratégie.</span><span class="sxs-lookup"><span data-stu-id="ad170-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="ad170-710">Éléments</span><span class="sxs-lookup"><span data-stu-id="ad170-710">Elements</span></span>  
  
|<span data-ttu-id="ad170-711">Élément</span><span class="sxs-lookup"><span data-stu-id="ad170-711">Element</span></span>|<span data-ttu-id="ad170-712">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-712">Description</span></span>|<span data-ttu-id="ad170-713">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="ad170-714">wait</span><span class="sxs-lookup"><span data-stu-id="ad170-714">wait</span></span>|<span data-ttu-id="ad170-715">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="ad170-715">Root element.</span></span> <span data-ttu-id="ad170-716">Ne peut contenir comme éléments enfants que les stratégies `send-request`, `cache-lookup-value` et `choose`.</span><span class="sxs-lookup"><span data-stu-id="ad170-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="ad170-717">Oui</span><span class="sxs-lookup"><span data-stu-id="ad170-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="ad170-718">Attributs</span><span class="sxs-lookup"><span data-stu-id="ad170-718">Attributes</span></span>  
  
|<span data-ttu-id="ad170-719">Attribut</span><span class="sxs-lookup"><span data-stu-id="ad170-719">Attribute</span></span>|<span data-ttu-id="ad170-720">Description</span><span class="sxs-lookup"><span data-stu-id="ad170-720">Description</span></span>|<span data-ttu-id="ad170-721">Requis</span><span class="sxs-lookup"><span data-stu-id="ad170-721">Required</span></span>|<span data-ttu-id="ad170-722">Default</span><span class="sxs-lookup"><span data-stu-id="ad170-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="ad170-723">for</span><span class="sxs-lookup"><span data-stu-id="ad170-723">for</span></span>|<span data-ttu-id="ad170-724">Détermine si hello `wait` stratégie attend que tous les enfants immédiats stratégies toobe est terminée ou qu’un seul.</span><span class="sxs-lookup"><span data-stu-id="ad170-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="ad170-725">Les valeurs autorisées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="ad170-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="ad170-726">-   `all`-attendre toocomplete de stratégies tous les enfants immédiats</span><span class="sxs-lookup"><span data-stu-id="ad170-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="ad170-727">-any - attendre tout toocomplete de stratégie enfants immédiats.</span><span class="sxs-lookup"><span data-stu-id="ad170-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="ad170-728">Une fois la stratégie enfant immédiat de la première hello terminée, hello `wait` stratégie se termine et l’exécution de toutes les autres stratégies enfant immédiat est terminée.</span><span class="sxs-lookup"><span data-stu-id="ad170-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="ad170-729">Non</span><span class="sxs-lookup"><span data-stu-id="ad170-729">No</span></span>|<span data-ttu-id="ad170-730">tout</span><span class="sxs-lookup"><span data-stu-id="ad170-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="ad170-731">Usage</span><span class="sxs-lookup"><span data-stu-id="ad170-731">Usage</span></span>  
 <span data-ttu-id="ad170-732">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="ad170-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="ad170-733">**Sections de la stratégie :** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="ad170-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="ad170-734">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="ad170-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ad170-735">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad170-735">Next steps</span></span>
<span data-ttu-id="ad170-736">Pour plus d’informations sur l’utilisation de stratégies, consultez les pages :</span><span class="sxs-lookup"><span data-stu-id="ad170-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="ad170-737">Stratégies dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="ad170-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="ad170-738">Expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="ad170-738">Policy expressions</span></span>](api-management-policy-expressions.md)
