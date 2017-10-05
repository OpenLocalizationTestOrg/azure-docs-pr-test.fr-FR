---
title: "Stratégies avancées de la Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies avancées disponibles dans la Gestion des API Azure."
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
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="8c4ee-103">Stratégies avancées de la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="8c4ee-103">API Management advanced policies</span></span>
<span data-ttu-id="8c4ee-104">Cette rubrique est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="8c4ee-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="8c4ee-106"><a name="AdvancedPolicies"></a> Stratégies avancées</span><span class="sxs-lookup"><span data-stu-id="8c4ee-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="8c4ee-107">[Control flow](api-management-advanced-policies.md#choose) : applique de manière conditionnelle les instructions de stratégie en fonction des résultats de l’évaluation des [expressions](api-management-policy-expressions.md) booléennes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="8c4ee-108">[Forward request](#ForwardRequest) : transfère la demande vers le service principal.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="8c4ee-109">[Limit concurrency](#LimitConcurrency) : empêche les stratégies incluses d’exécuter plus de requêtes simultanées que le nombre spécifié.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="8c4ee-110">[Log to Event Hub](#log-to-eventhub) : envoie des messages au format spécifié à un Event Hub défini par une entité Enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="8c4ee-111">[Mock response](#mock-response) : abandonne l’exécution du pipeline et renvoie une réponse factice indiquée directement à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="8c4ee-112">[Retry](#Retry) : effectue une nouvelle tentative d’exécution des instructions de stratégie incluses, si la condition est remplie et jusqu’à ce qu’elle le soit.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="8c4ee-113">L’exécution se répète à intervalles réguliers et ce jusqu’au nombre de tentatives défini.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="8c4ee-114">[Return response](#ReturnResponse) : abandonne l’exécution du pipeline et renvoie la réponse indiquée directement à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="8c4ee-115">[Send one way request](#SendOneWayRequest) : envoie une demande à l’URL indiquée sans attendre de réponse.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="8c4ee-116">[Send request](#SendRequest) : envoie une demande à l’URL indiquée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="8c4ee-117">[Définir le proxy HTTP](#SetHttpProxy) : vous permet de router les demandes transférées via un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="8c4ee-118">[Set request method](#SetRequestMethod) : permet de modifier la méthode HTTP d’une demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="8c4ee-119">[Set status code](#SetStatus) : permet de donner la valeur spécifiée au code d’état HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="8c4ee-120">[Set variable](api-management-advanced-policies.md#set-variable) : conserve une valeur dans une variable de [contexte](api-management-policy-expressions.md#ContextVariables) nommée pour permettre d’y accéder ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="8c4ee-121">[Trace](#Trace) : ajoute une chaîne à la sortie de l’[inspecteur d’API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="8c4ee-122">[Wait](#Wait) : attend l’exécution des stratégies incluses [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) et [Control flow](api-management-advanced-policies.md#choose) pour continuer.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="8c4ee-123"><a name="choose"></a> Control flow</span><span class="sxs-lookup"><span data-stu-id="8c4ee-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="8c4ee-124">La stratégie `choose` applique les instructions de stratégie incluses en fonction du résultat de l’évaluation d’expressions booléennes, de façon similaire à une construction de type if-then-else ou commutateur dans un langage de programmation.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="8c4ee-125"><a name="ChoosePolicyStatement"></a> Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="8c4ee-126">La stratégie de flux de contrôle doit contenir au moins un élément `<when/>`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="8c4ee-127">L’élément `<otherwise/>` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="8c4ee-128">Les conditions dans les éléments `<when/>` sont évaluées par ordre d’apparition dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="8c4ee-129">La ou les déclarations de stratégie incluses dans le premier élément `<when/>` avec attribut de condition égal à `true` seront appliquées.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="8c4ee-130">Les stratégies incluses dans l’élément `<otherwise/>`, le cas échéant, seront appliquées si tous les attributs de condition de l’élément `<when/>` sont `false`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="8c4ee-131">Exemples</span><span class="sxs-lookup"><span data-stu-id="8c4ee-131">Examples</span></span>  
  
####  <span data-ttu-id="8c4ee-132"><a name="ChooseExample"></a> Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="8c4ee-133">L’exemple suivant montre une stratégie [set-variable](api-management-advanced-policies.md#set-variable) ainsi que deux stratégies de contrôle de flux.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="8c4ee-134">La stratégie set variable se trouve dans la section inbound et crée une variable de [contexte](api-management-policy-expressions.md#ContextVariables) `isMobile` booléenne qui a la valeur true si l’en-tête de demande `User-Agent` contient le texte `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="8c4ee-135">La première stratégie de flux de contrôle se trouve également dans la section inbound et applique de manière conditionnelle une des deux stratégies [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) selon la valeur de la variable de contexte `isMobile`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="8c4ee-136">La deuxième stratégie de flux de contrôle se trouve dans la section outbound et applique de manière conditionnelle la stratégie [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) si `isMobile` a la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="8c4ee-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-137">Example</span></span>  
 <span data-ttu-id="8c4ee-138">Cet exemple montre comment effectuer un filtrage du contenu en supprimant des éléments de données de la réponse reçue du service principal en cas d’utilisation du produit `Starter`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="8c4ee-139">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez la page [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, épisode 177 : Plus de fonctionnalités de la Gestion des API avec Vlad Vinogradsky) et rendez-vous directement à 34 min 30 s.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="8c4ee-140">Commencez à 31 min 50 s pour voir une présentation de [l’API The Dark Sky Forecast](https://developer.forecast.io/) utilisée pour cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-141">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-141">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-142">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-142">Element</span></span>|<span data-ttu-id="8c4ee-143">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-143">Description</span></span>|<span data-ttu-id="8c4ee-144">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-145">choose</span><span class="sxs-lookup"><span data-stu-id="8c4ee-145">choose</span></span>|<span data-ttu-id="8c4ee-146">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-146">Root element.</span></span>|<span data-ttu-id="8c4ee-147">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-147">Yes</span></span>|  
|<span data-ttu-id="8c4ee-148">when</span><span class="sxs-lookup"><span data-stu-id="8c4ee-148">when</span></span>|<span data-ttu-id="8c4ee-149">Condition à utiliser pour les parties `if` ou `ifelse` de la stratégie `choose`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="8c4ee-150">Si la stratégie `choose` possède plusieurs sections `when`, elles sont évaluées de façon séquentielle.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="8c4ee-151">Une fois la `condition` d’un élément when évaluée à `true`, aucune autre condition `when` n’est évaluée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="8c4ee-152">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-152">Yes</span></span>|  
|<span data-ttu-id="8c4ee-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="8c4ee-153">otherwise</span></span>|<span data-ttu-id="8c4ee-154">Contient l’extrait de stratégie à utiliser si aucune des conditions `when` n’est évaluée à `true`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="8c4ee-155">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-156">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-156">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-157">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-157">Attribute</span></span>|<span data-ttu-id="8c4ee-158">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-158">Description</span></span>|<span data-ttu-id="8c4ee-159">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="8c4ee-161">Constante ou expression booléenne à évaluer lorsque la déclaration de stratégie `when` qui l’englobe est évaluée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="8c4ee-162">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-162">Yes</span></span>|  
  
###  <span data-ttu-id="8c4ee-163"><a name="ChooseUsage"></a> Utilisation</span><span class="sxs-lookup"><span data-stu-id="8c4ee-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="8c4ee-164">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-165">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-166">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-167"><a name="ForwardRequest"></a> Forward request</span><span class="sxs-lookup"><span data-stu-id="8c4ee-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="8c4ee-168">La stratégie `forward-request` transfère la demande entrante au service principal spécifié dans le [contexte](api-management-policy-expressions.md#ContextVariables) de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="8c4ee-169">L’URL du service principal est spécifiée dans les [paramètres](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) de l’API et peut être modifiée à l’aide de la stratégie [set backend service](api-management-transformation-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8c4ee-170">En cas de suppression cette stratégie, la demande n’est pas transférée au service principal et les stratégies de la section outbound sont évaluées immédiatement après la réussite des stratégies de la section inbound.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-171">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="8c4ee-172">Exemples</span><span class="sxs-lookup"><span data-stu-id="8c4ee-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="8c4ee-173">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-173">Example</span></span>  
 <span data-ttu-id="8c4ee-174">La stratégie au niveau de l’API suivante transfère toutes les demandes au service principal avec un délai d’expiration de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="8c4ee-175">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-175">Example</span></span>  
 <span data-ttu-id="8c4ee-176">Cette stratégie au niveau de l’opération utilise l’élément `base` pour hériter de la stratégie backend de l’étendue au niveau de l’API parente.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="8c4ee-177">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-177">Example</span></span>  
 <span data-ttu-id="8c4ee-178">Cette stratégie au niveau de l’opération transfère explicitement toutes les demandes au service principal avec un délai d’expiration de 120 secondes et n’hérite pas de la stratégie principale au niveau de l’API parente.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="8c4ee-179">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-179">Example</span></span>  
 <span data-ttu-id="8c4ee-180">Cette stratégie au niveau de l’opération ne transmet pas de demandes au service principal.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="8c4ee-181">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-181">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-182">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-182">Element</span></span>|<span data-ttu-id="8c4ee-183">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-183">Description</span></span>|<span data-ttu-id="8c4ee-184">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="8c4ee-185">forward-request</span></span>|<span data-ttu-id="8c4ee-186">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-186">Root element.</span></span>|<span data-ttu-id="8c4ee-187">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-188">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-188">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-189">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-189">Attribute</span></span>|<span data-ttu-id="8c4ee-190">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-190">Description</span></span>|<span data-ttu-id="8c4ee-191">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-191">Required</span></span>|<span data-ttu-id="8c4ee-192">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-193">timeout="integer"</span></span>|<span data-ttu-id="8c4ee-194">Délai d’expiration en secondes avant l’échec de l’appel au service principal.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="8c4ee-195">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-195">No</span></span>|<span data-ttu-id="8c4ee-196">Aucun délai d’expiration</span><span class="sxs-lookup"><span data-stu-id="8c4ee-196">No timeout</span></span>|  
|<span data-ttu-id="8c4ee-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="8c4ee-198">Indique si les redirections à partir du service principal sont suivies par la passerelle ou renvoyées à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="8c4ee-199">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-199">No</span></span>|<span data-ttu-id="8c4ee-200">false</span><span class="sxs-lookup"><span data-stu-id="8c4ee-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-201">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-201">Usage</span></span>  
 <span data-ttu-id="8c4ee-202">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-203">**Sections de la stratégie :** backend</span><span class="sxs-lookup"><span data-stu-id="8c4ee-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="8c4ee-204">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-205"><a name="LimitConcurrency"></a> Limit concurrency</span><span class="sxs-lookup"><span data-stu-id="8c4ee-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="8c4ee-206">La stratégie `limit-concurrency` empêche les stratégies incluses d’exécuter plus de requêtes simultanées que le nombre spécifié.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="8c4ee-207">En cas de dépassement du seuil, les requêtes sont ajoutées à la file d’attente jusqu’à ce que la longueur maximale de cette dernière soit atteinte.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="8c4ee-208">Lorsque la file est pleine, les nouvelles requêtes échouent immédiatement.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="8c4ee-209"><a name="LimitConcurrencyStatement"></a> Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="8c4ee-210">Exemples</span><span class="sxs-lookup"><span data-stu-id="8c4ee-210">Examples</span></span>  
  
####  <span data-ttu-id="8c4ee-211"><a name="ChooseExample"></a> Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="8c4ee-212">L’exemple suivant montre comment limiter le nombre de requêtes transmises à un serveur principal en fonction de la valeur d’une variable contextuelle.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="8c4ee-213">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-213">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-214">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-214">Element</span></span>|<span data-ttu-id="8c4ee-215">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-215">Description</span></span>|<span data-ttu-id="8c4ee-216">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="8c4ee-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="8c4ee-217">limit-concurrency</span></span>|<span data-ttu-id="8c4ee-218">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-218">Root element.</span></span>|<span data-ttu-id="8c4ee-219">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-220">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-220">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-221">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-221">Attribute</span></span>|<span data-ttu-id="8c4ee-222">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-222">Description</span></span>|<span data-ttu-id="8c4ee-223">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-223">Required</span></span>|<span data-ttu-id="8c4ee-224">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="8c4ee-225">key</span><span class="sxs-lookup"><span data-stu-id="8c4ee-225">key</span></span>|<span data-ttu-id="8c4ee-226">Une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-226">A string.</span></span> <span data-ttu-id="8c4ee-227">Expression autorisée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-227">Expression allowed.</span></span> <span data-ttu-id="8c4ee-228">Spécifie l’étendue de la simultanéité.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="8c4ee-229">Peut être partagée par plusieurs stratégies.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="8c4ee-230">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-230">Yes</span></span>|<span data-ttu-id="8c4ee-231">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-231">N/A</span></span>|  
|<span data-ttu-id="8c4ee-232">max-count</span><span class="sxs-lookup"><span data-stu-id="8c4ee-232">max-count</span></span>|<span data-ttu-id="8c4ee-233">Nombre entier.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-233">An integer.</span></span> <span data-ttu-id="8c4ee-234">Spécifie le nombre maximal de requêtes autorisées à entrer dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="8c4ee-235">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-235">Yes</span></span>|<span data-ttu-id="8c4ee-236">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-236">N/A</span></span>|  
|<span data-ttu-id="8c4ee-237">timeout</span><span class="sxs-lookup"><span data-stu-id="8c4ee-237">timeout</span></span>|<span data-ttu-id="8c4ee-238">Nombre entier.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-238">An integer.</span></span> <span data-ttu-id="8c4ee-239">Expression autorisée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-239">Expression allowed.</span></span> <span data-ttu-id="8c4ee-240">Spécifie le nombre de secondes pendant lesquelles une requête doit attendre avant d’échouer avec l’erreur « 403 Too Many Requests » (Trop de requêtes).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="8c4ee-241">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-241">No</span></span>|<span data-ttu-id="8c4ee-242">Infini</span><span class="sxs-lookup"><span data-stu-id="8c4ee-242">Infinity</span></span>|  
|<span data-ttu-id="8c4ee-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="8c4ee-243">max-queue-length</span></span>|<span data-ttu-id="8c4ee-244">Nombre entier.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-244">An integer.</span></span> <span data-ttu-id="8c4ee-245">Expression autorisée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-245">Expression allowed.</span></span> <span data-ttu-id="8c4ee-246">Spécifie la longueur maximale de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="8c4ee-247">Les requêtes entrantes essayant d’entrer dans cette stratégie échouent avec l’erreur « 403 Too Many Request » (Trop de requêtes) dès que la file est pleine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="8c4ee-248">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-248">No</span></span>|<span data-ttu-id="8c4ee-249">Infini</span><span class="sxs-lookup"><span data-stu-id="8c4ee-249">Infinity</span></span>|  
  
###  <span data-ttu-id="8c4ee-250"><a name="ChooseUsage"></a> Utilisation</span><span class="sxs-lookup"><span data-stu-id="8c4ee-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="8c4ee-251">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-252">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-253">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="8c4ee-254"><a name="log-to-eventhub"></a> Log to Event Hub</span><span class="sxs-lookup"><span data-stu-id="8c4ee-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="8c4ee-255">La stratégie `log-to-eventhub` envoie des messages au format spécifié à un Event Hub défini par une entité Enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="8c4ee-256">Comme son nom l’indique, la stratégie est utilisée pour enregistrer certaines informations sur le contexte de la réponse ou de la demande à des fins d’analyse en ligne ou hors ligne.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="8c4ee-257">Vous trouverez un guide de configuration étape par étape d’un Event Hub et des événements de journalisation à la page [Guide pratique de l’enregistrement d’événements de la Gestion des API avec Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-258">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-259">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-259">Example</span></span>  
 <span data-ttu-id="8c4ee-260">Toute chaîne peut être utilisée comme valeur à consigner dans Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="8c4ee-261">Dans cet exemple, la date et l’heure, le nom de service de déploiement, l’ID de la demande, l’adresse IP et le nom de l’opération de tous les appels inbound sont consignés dans l’Enregistreur d’événements Event Hubs avec l’ID `contoso-logger`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-262">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-262">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-263">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-263">Element</span></span>|<span data-ttu-id="8c4ee-264">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-264">Description</span></span>|<span data-ttu-id="8c4ee-265">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="8c4ee-266">log-to-eventhub</span></span>|<span data-ttu-id="8c4ee-267">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-267">Root element.</span></span> <span data-ttu-id="8c4ee-268">La valeur de cet élément est la chaîne à consigner dans votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="8c4ee-269">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-270">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-270">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-271">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-271">Attribute</span></span>|<span data-ttu-id="8c4ee-272">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-272">Description</span></span>|<span data-ttu-id="8c4ee-273">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="8c4ee-274">logger-id</span></span>|<span data-ttu-id="8c4ee-275">ID de l’Enregistreur d’événements inscrit auprès de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="8c4ee-276">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-276">Yes</span></span>|  
|<span data-ttu-id="8c4ee-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="8c4ee-277">partition-id</span></span>|<span data-ttu-id="8c4ee-278">Spécifie l’index de la partition où les messages sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="8c4ee-279">facultatif.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-279">Optional.</span></span> <span data-ttu-id="8c4ee-280">Cet attribut peut ne pas être utilisé si `partition-key` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="8c4ee-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="8c4ee-281">partition-key</span></span>|<span data-ttu-id="8c4ee-282">Spécifie la valeur utilisée pour l’affectation de partitions lorsque des messages sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="8c4ee-283">facultatif.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-283">Optional.</span></span> <span data-ttu-id="8c4ee-284">Cet attribut peut ne pas être utilisé si `partition-id` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-285">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-285">Usage</span></span>  
 <span data-ttu-id="8c4ee-286">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-287">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-288">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="8c4ee-289"><a name="mock-response"></a> Réponse factice</span><span class="sxs-lookup"><span data-stu-id="8c4ee-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="8c4ee-290">La `mock-response`, comme le nom l’indique, est utilisée pour simuler des API et des opérations.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="8c4ee-291">Elle interrompt l’exécution du pipeline et retourne une réponse factice à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="8c4ee-292">La stratégie essaie toujours de renvoyer des réponses de la plus haute fidélité.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="8c4ee-293">Elle préfère les exemples de contenu de réponse, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="8c4ee-294">Elle génère des exemples de réponses à partir de schémas, lorsque les schémas sont fournis et les exemples ne le sont pas.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="8c4ee-295">Si aucun exemple ou schéma n’est trouvé, des réponses sans contenu sont retournées.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-296">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="8c4ee-297">Exemples</span><span class="sxs-lookup"><span data-stu-id="8c4ee-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="8c4ee-298">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-298">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-299">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-299">Element</span></span>|<span data-ttu-id="8c4ee-300">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-300">Description</span></span>|<span data-ttu-id="8c4ee-301">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="8c4ee-302">mock-response</span></span>|<span data-ttu-id="8c4ee-303">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-303">Root element.</span></span>|<span data-ttu-id="8c4ee-304">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-305">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-305">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-306">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-306">Attribute</span></span>|<span data-ttu-id="8c4ee-307">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-307">Description</span></span>|<span data-ttu-id="8c4ee-308">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-308">Required</span></span>|<span data-ttu-id="8c4ee-309">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="8c4ee-310">status-code</span><span class="sxs-lookup"><span data-stu-id="8c4ee-310">status-code</span></span>|<span data-ttu-id="8c4ee-311">Spécifie le code d’état de réponse et permet de sélectionner l’exemple ou le schéma correspondant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="8c4ee-312">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-312">No</span></span>|<span data-ttu-id="8c4ee-313">200</span><span class="sxs-lookup"><span data-stu-id="8c4ee-313">200</span></span>|  
|<span data-ttu-id="8c4ee-314">content-type</span><span class="sxs-lookup"><span data-stu-id="8c4ee-314">content-type</span></span>|<span data-ttu-id="8c4ee-315">Spécifie la valeur d’état de réponse `Content-Type` et permet de sélectionner l’exemple ou le schéma correspondant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="8c4ee-316">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-316">No</span></span>|<span data-ttu-id="8c4ee-317">Aucune</span><span class="sxs-lookup"><span data-stu-id="8c4ee-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-318">Utilisation</span><span class="sxs-lookup"><span data-stu-id="8c4ee-318">Usage</span></span>  
 <span data-ttu-id="8c4ee-319">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-320">**Sections de la stratégie :** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-321">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="8c4ee-322"><a name="Retry"></a> Retry</span><span class="sxs-lookup"><span data-stu-id="8c4ee-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="8c4ee-323">La stratégie `retry` exécute ses stratégies enfants une fois, puis retente leur exécution jusqu’à ce que la `condition` de la nouvelle tentative devienne `false` ou que le `count` de nouvelles tentatives soit épuisé.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-324">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="8c4ee-325">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-325">Example</span></span>  
 <span data-ttu-id="8c4ee-326">Dans l’exemple suivant, le transfert de la demande est retenté jusqu’à dix fois suivant un algorithme de nouvelles tentatives exponentiel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="8c4ee-327">Étant donné que `first-fast-retry` a la valeur false, toutes les nouvelles tentatives sont soumises à l’algorithme de nouvelles tentatives exponentiel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-328">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-328">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-329">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-329">Element</span></span>|<span data-ttu-id="8c4ee-330">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-330">Description</span></span>|<span data-ttu-id="8c4ee-331">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-332">retry</span><span class="sxs-lookup"><span data-stu-id="8c4ee-332">retry</span></span>|<span data-ttu-id="8c4ee-333">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-333">Root element.</span></span> <span data-ttu-id="8c4ee-334">Peut contenir n’importe quelle autre stratégie sous forme d’élément enfant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="8c4ee-335">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-336">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-336">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-337">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-337">Attribute</span></span>|<span data-ttu-id="8c4ee-338">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-338">Description</span></span>|<span data-ttu-id="8c4ee-339">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-339">Required</span></span>|<span data-ttu-id="8c4ee-340">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-341">condition</span><span class="sxs-lookup"><span data-stu-id="8c4ee-341">condition</span></span>|<span data-ttu-id="8c4ee-342">[Expression](api-management-policy-expressions.md) ou littéral booléen spécifiant si les nouvelles tentatives doivent être arrêtées (`false`) ou poursuivies (`true`).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="8c4ee-343">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-343">Yes</span></span>|<span data-ttu-id="8c4ee-344">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-344">N/A</span></span>|  
|<span data-ttu-id="8c4ee-345">count</span><span class="sxs-lookup"><span data-stu-id="8c4ee-345">count</span></span>|<span data-ttu-id="8c4ee-346">Nombre positif spécifiant le nombre maximal de nouvelles tentatives à effectuer.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="8c4ee-347">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-347">Yes</span></span>|<span data-ttu-id="8c4ee-348">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-348">N/A</span></span>|  
|<span data-ttu-id="8c4ee-349">interval</span><span class="sxs-lookup"><span data-stu-id="8c4ee-349">interval</span></span>|<span data-ttu-id="8c4ee-350">Nombre positif en secondes spécifiant le délai d’attente entre les tentatives.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="8c4ee-351">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-351">Yes</span></span>|<span data-ttu-id="8c4ee-352">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-352">N/A</span></span>|  
|<span data-ttu-id="8c4ee-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="8c4ee-353">max-interval</span></span>|<span data-ttu-id="8c4ee-354">Nombre positif en secondes spécifiant le délai d’attente maximal entre les tentatives.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="8c4ee-355">Il est utilisé pour implémenter un algorithme de nouvelles tentatives exponentiel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="8c4ee-356">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-356">No</span></span>|<span data-ttu-id="8c4ee-357">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-357">N/A</span></span>|  
|<span data-ttu-id="8c4ee-358">delta</span><span class="sxs-lookup"><span data-stu-id="8c4ee-358">delta</span></span>|<span data-ttu-id="8c4ee-359">Nombre positif en secondes spécifiant l’incrément du délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="8c4ee-360">Il est utilisé pour implémenter les algorithmes de nouvelles tentatives linéaires et exponentiels.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="8c4ee-361">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-361">No</span></span>|<span data-ttu-id="8c4ee-362">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-362">N/A</span></span>|  
|<span data-ttu-id="8c4ee-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="8c4ee-363">first-fast-retry</span></span>|<span data-ttu-id="8c4ee-364">S’il a la valeur `true`, la première des nouvelles tentatives est effectuée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="8c4ee-365">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="8c4ee-366">Lorsque seul `interval` est spécifié, les nouvelles tentatives sont effectuées à intervalles **fixes**.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="8c4ee-367">Lorsque seuls `interval` et `delta` sont spécifiés, un algorithme de nouvelles tentatives à intervalle **linéaire** est utilisé, suivant lequel le temps d’attente entre les tentatives est calculé selon la formule suivante : `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="8c4ee-368">Lorsque `interval`, `max-interval` et `delta` sont spécifiés, l’algorithme de nouvelles tentatives à intervalle **exponentiel** s’applique, suivant lequel le temps d’attente entre les tentatives augmente de façon exponentielle entre la valeur `interval` et la valeur `max-interval` selon la formule suivante : `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-369">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-369">Usage</span></span>  
 <span data-ttu-id="8c4ee-370">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="8c4ee-371">Notez que des restrictions d’utilisation des stratégies enfants seront héritées par cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="8c4ee-372">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-373">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-374"><a name="ReturnResponse"></a> Return response</span><span class="sxs-lookup"><span data-stu-id="8c4ee-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="8c4ee-375">La stratégie `return-response` abandonne l’exécution du pipeline et renvoie une réponse par défaut ou personnalisée à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="8c4ee-376">La réponse par défaut est `200 OK` sans corps.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="8c4ee-377">La réponse personnalisée peut être spécifiée par le biais d’instructions de stratégie ou d’une variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="8c4ee-378">Lorsque les deux sont fournies, la réponse contenue dans la variable de contexte est modifiée par les instructions de stratégie avant d’être renvoyée à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-379">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-380">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="8c4ee-381">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-381">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-382">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-382">Element</span></span>|<span data-ttu-id="8c4ee-383">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-383">Description</span></span>|<span data-ttu-id="8c4ee-384">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-385">return-response</span><span class="sxs-lookup"><span data-stu-id="8c4ee-385">return-response</span></span>|<span data-ttu-id="8c4ee-386">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-386">Root element.</span></span>|<span data-ttu-id="8c4ee-387">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-387">Yes</span></span>|  
|<span data-ttu-id="8c4ee-388">set-header</span><span class="sxs-lookup"><span data-stu-id="8c4ee-388">set-header</span></span>|<span data-ttu-id="8c4ee-389">Instruction de stratégie [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="8c4ee-390">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-390">No</span></span>|  
|<span data-ttu-id="8c4ee-391">set-body</span><span class="sxs-lookup"><span data-stu-id="8c4ee-391">set-body</span></span>|<span data-ttu-id="8c4ee-392">Instruction de stratégie [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="8c4ee-393">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-393">No</span></span>|  
|<span data-ttu-id="8c4ee-394">set-status</span><span class="sxs-lookup"><span data-stu-id="8c4ee-394">set-status</span></span>|<span data-ttu-id="8c4ee-395">Instruction de stratégie [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="8c4ee-396">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-397">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-397">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-398">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-398">Attribute</span></span>|<span data-ttu-id="8c4ee-399">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-399">Description</span></span>|<span data-ttu-id="8c4ee-400">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="8c4ee-401">response-variable-name</span></span>|<span data-ttu-id="8c4ee-402">Nom de la variable de contexte référencée à partir, par exemple, d’une stratégie [send-request](api-management-advanced-policies.md#SendRequest) en amont et contenant un objet `Response`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="8c4ee-403">facultatif.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-404">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-404">Usage</span></span>  
 <span data-ttu-id="8c4ee-405">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-406">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-407">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-408"><a name="SendOneWayRequest"></a> Send one way request</span><span class="sxs-lookup"><span data-stu-id="8c4ee-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="8c4ee-409">La stratégie `send-one-way-request` envoie une demande à l’URL indiquée sans attendre de réponse.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-410">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-411">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-411">Example</span></span>  
 <span data-ttu-id="8c4ee-412">Cet exemple de stratégie montre un exemple d’utilisation de la stratégie `send-one-way-request` pour envoyer un message à une salle de conversation Slack si le code de la réponse HTTP est supérieur ou égal à 500.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="8c4ee-413">Pour plus d’informations sur cet exemple, consultez la page [Utilisation de services externes à partir du service Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-414">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-414">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-415">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-415">Element</span></span>|<span data-ttu-id="8c4ee-416">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-416">Description</span></span>|<span data-ttu-id="8c4ee-417">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="8c4ee-418">send-one-way-request</span></span>|<span data-ttu-id="8c4ee-419">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-419">Root element.</span></span>|<span data-ttu-id="8c4ee-420">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-420">Yes</span></span>|  
|<span data-ttu-id="8c4ee-421">url</span><span class="sxs-lookup"><span data-stu-id="8c4ee-421">url</span></span>|<span data-ttu-id="8c4ee-422">URL de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-422">The URL of the request.</span></span>|<span data-ttu-id="8c4ee-423">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="8c4ee-424">statique</span><span class="sxs-lookup"><span data-stu-id="8c4ee-424">method</span></span>|<span data-ttu-id="8c4ee-425">Méthode HTTP de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-425">The HTTP method for the request.</span></span>|<span data-ttu-id="8c4ee-426">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="8c4ee-427">en-tête</span><span class="sxs-lookup"><span data-stu-id="8c4ee-427">header</span></span>|<span data-ttu-id="8c4ee-428">En-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-428">Request header.</span></span> <span data-ttu-id="8c4ee-429">Utilisez un élément d’en-tête pour chaque en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="8c4ee-430">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-430">No</span></span>|  
|<span data-ttu-id="8c4ee-431">body</span><span class="sxs-lookup"><span data-stu-id="8c4ee-431">body</span></span>|<span data-ttu-id="8c4ee-432">Corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-432">The request body.</span></span>|<span data-ttu-id="8c4ee-433">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-434">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-434">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-435">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-435">Attribute</span></span>|<span data-ttu-id="8c4ee-436">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-436">Description</span></span>|<span data-ttu-id="8c4ee-437">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-437">Required</span></span>|<span data-ttu-id="8c4ee-438">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-439">mode="string"</span></span>|<span data-ttu-id="8c4ee-440">Détermine s’il s’agit d’une nouvelle demande ou d’une copie de la demande actuelle.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="8c4ee-441">En mode outbound, mode=copy n’initialise pas le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="8c4ee-442">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-442">No</span></span>|<span data-ttu-id="8c4ee-443">Nouveau</span><span class="sxs-lookup"><span data-stu-id="8c4ee-443">New</span></span>|  
|<span data-ttu-id="8c4ee-444">name</span><span class="sxs-lookup"><span data-stu-id="8c4ee-444">name</span></span>|<span data-ttu-id="8c4ee-445">Spécifie le nom de l’en-tête à définir.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="8c4ee-446">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-446">Yes</span></span>|<span data-ttu-id="8c4ee-447">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-447">N/A</span></span>|  
|<span data-ttu-id="8c4ee-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="8c4ee-448">exists-action</span></span>|<span data-ttu-id="8c4ee-449">Spécifie l’action à entreprendre lorsque l’en-tête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="8c4ee-450">Cet attribut doit avoir une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="8c4ee-451">- override : remplace la valeur de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="8c4ee-452">- skip : ne remplace pas la valeur de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="8c4ee-453">- append : ajoute la valeur à celle de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="8c4ee-454">- delete : supprime l’en-tête de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="8c4ee-455">S’il a la valeur `override`, l’inscription de plusieurs entrées portant le même nom fait que l’en-tête est défini selon toutes les entrées (qui figurent plusieurs fois) ; seules les valeurs listées seront définies dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="8c4ee-456">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-456">No</span></span>|<span data-ttu-id="8c4ee-457">override</span><span class="sxs-lookup"><span data-stu-id="8c4ee-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-458">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-458">Usage</span></span>  
 <span data-ttu-id="8c4ee-459">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-460">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-461">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-462"><a name="SendRequest"></a> Send request</span><span class="sxs-lookup"><span data-stu-id="8c4ee-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="8c4ee-463">La stratégie `send-request` envoie la demande fournie à l’URL spécifiée, sans attendre plus longtemps que la valeur du délai d’expiration définie.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-464">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-465">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-465">Example</span></span>  
 <span data-ttu-id="8c4ee-466">Cet exemple montre un moyen de vérifier un jeton de référence avec un serveur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="8c4ee-467">Pour plus d’informations sur cet exemple, consultez la page [Utilisation de services externes à partir du service Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-468">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-468">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-469">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-469">Element</span></span>|<span data-ttu-id="8c4ee-470">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-470">Description</span></span>|<span data-ttu-id="8c4ee-471">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-472">send-request</span><span class="sxs-lookup"><span data-stu-id="8c4ee-472">send-request</span></span>|<span data-ttu-id="8c4ee-473">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-473">Root element.</span></span>|<span data-ttu-id="8c4ee-474">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-474">Yes</span></span>|  
|<span data-ttu-id="8c4ee-475">url</span><span class="sxs-lookup"><span data-stu-id="8c4ee-475">url</span></span>|<span data-ttu-id="8c4ee-476">URL de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-476">The URL of the request.</span></span>|<span data-ttu-id="8c4ee-477">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="8c4ee-478">statique</span><span class="sxs-lookup"><span data-stu-id="8c4ee-478">method</span></span>|<span data-ttu-id="8c4ee-479">Méthode HTTP de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-479">The HTTP method for the request.</span></span>|<span data-ttu-id="8c4ee-480">Non si mode=copy ; sinon, oui.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="8c4ee-481">en-tête</span><span class="sxs-lookup"><span data-stu-id="8c4ee-481">header</span></span>|<span data-ttu-id="8c4ee-482">En-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-482">Request header.</span></span> <span data-ttu-id="8c4ee-483">Utilisez un élément d’en-tête pour chaque en-tête de demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="8c4ee-484">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-484">No</span></span>|  
|<span data-ttu-id="8c4ee-485">body</span><span class="sxs-lookup"><span data-stu-id="8c4ee-485">body</span></span>|<span data-ttu-id="8c4ee-486">Corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-486">The request body.</span></span>|<span data-ttu-id="8c4ee-487">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-488">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-488">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-489">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-489">Attribute</span></span>|<span data-ttu-id="8c4ee-490">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-490">Description</span></span>|<span data-ttu-id="8c4ee-491">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-491">Required</span></span>|<span data-ttu-id="8c4ee-492">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-493">mode="string"</span></span>|<span data-ttu-id="8c4ee-494">Détermine s’il s’agit d’une nouvelle demande ou d’une copie de la demande actuelle.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="8c4ee-495">En mode outbound, mode=copy n’initialise pas le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="8c4ee-496">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-496">No</span></span>|<span data-ttu-id="8c4ee-497">Nouveau</span><span class="sxs-lookup"><span data-stu-id="8c4ee-497">New</span></span>|  
|<span data-ttu-id="8c4ee-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-498">response-variable-name="string"</span></span>|<span data-ttu-id="8c4ee-499">En son absence, `context.Response` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="8c4ee-500">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-500">No</span></span>|<span data-ttu-id="8c4ee-501">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-501">N/A</span></span>|  
|<span data-ttu-id="8c4ee-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-502">timeout="integer"</span></span>|<span data-ttu-id="8c4ee-503">Délai d’expiration en secondes avant l’échec de l’appel à l’URL.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="8c4ee-504">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-504">No</span></span>|<span data-ttu-id="8c4ee-505">60</span><span class="sxs-lookup"><span data-stu-id="8c4ee-505">60</span></span>|  
|<span data-ttu-id="8c4ee-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-506">ignore-error</span></span>|<span data-ttu-id="8c4ee-507">S’il a la valeur true et que la demande aboutit à une erreur :</span><span class="sxs-lookup"><span data-stu-id="8c4ee-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="8c4ee-508">- Si response-variable-name a été spécifié, il contiendra une valeur Null.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="8c4ee-509">- Si response-variable-nam n’est pas spécifié, context.Request ne sera pas mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="8c4ee-510">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-510">No</span></span>|<span data-ttu-id="8c4ee-511">false</span><span class="sxs-lookup"><span data-stu-id="8c4ee-511">false</span></span>|  
|<span data-ttu-id="8c4ee-512">name</span><span class="sxs-lookup"><span data-stu-id="8c4ee-512">name</span></span>|<span data-ttu-id="8c4ee-513">Spécifie le nom de l’en-tête à définir.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="8c4ee-514">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-514">Yes</span></span>|<span data-ttu-id="8c4ee-515">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-515">N/A</span></span>|  
|<span data-ttu-id="8c4ee-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="8c4ee-516">exists-action</span></span>|<span data-ttu-id="8c4ee-517">Spécifie l’action à entreprendre lorsque l’en-tête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="8c4ee-518">Cet attribut doit avoir une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="8c4ee-519">- override : remplace la valeur de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="8c4ee-520">- skip : ne remplace pas la valeur de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="8c4ee-521">- append : ajoute la valeur à celle de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="8c4ee-522">- delete : supprime l’en-tête de la demande.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="8c4ee-523">S’il a la valeur `override`, l’inscription de plusieurs entrées portant le même nom fait que l’en-tête est défini selon toutes les entrées (qui figurent plusieurs fois) ; seules les valeurs listées seront définies dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="8c4ee-524">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-524">No</span></span>|<span data-ttu-id="8c4ee-525">override</span><span class="sxs-lookup"><span data-stu-id="8c4ee-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-526">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-526">Usage</span></span>  
 <span data-ttu-id="8c4ee-527">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-528">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-529">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-530"><a name="SetHttpProxy"></a> Définir le proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="8c4ee-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="8c4ee-531">La stratégie `proxy` vous permet de router les demandes transférées aux back-ends via un proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="8c4ee-532">Seul HTTP (et pas HTTPS) est pris en charge entre la passerelle et le proxy.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="8c4ee-533">Authentification de base et NTLM uniquement.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-534">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-535">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-535">Example</span></span>  
<span data-ttu-id="8c4ee-536">Notez l’utilisation de [propriétés](api-management-howto-properties.md) en tant que valeurs du nom d’utilisateur et du mot de passe pour éviter de stocker des informations sensibles dans le document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="8c4ee-537">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-537">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-538">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-538">Element</span></span>|<span data-ttu-id="8c4ee-539">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-539">Description</span></span>|<span data-ttu-id="8c4ee-540">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-541">proxy</span><span class="sxs-lookup"><span data-stu-id="8c4ee-541">proxy</span></span>|<span data-ttu-id="8c4ee-542">Élément racine</span><span class="sxs-lookup"><span data-stu-id="8c4ee-542">Root element</span></span>|<span data-ttu-id="8c4ee-543">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="8c4ee-544">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-544">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-545">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-545">Attribute</span></span>|<span data-ttu-id="8c4ee-546">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-546">Description</span></span>|<span data-ttu-id="8c4ee-547">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-547">Required</span></span>|<span data-ttu-id="8c4ee-548">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-549">url="chaîne"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-549">url="string"</span></span>|<span data-ttu-id="8c4ee-550">URL du proxy sous la forme http://host:port.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="8c4ee-551">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-551">Yes</span></span>|<span data-ttu-id="8c4ee-552">N/A </span><span class="sxs-lookup"><span data-stu-id="8c4ee-552">N/A</span></span>|  
|<span data-ttu-id="8c4ee-553">username="chaîne"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-553">username="string"</span></span>|<span data-ttu-id="8c4ee-554">Nom d’utilisateur à utiliser pour l’authentification auprès du proxy.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="8c4ee-555">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-555">No</span></span>|<span data-ttu-id="8c4ee-556">N/A </span><span class="sxs-lookup"><span data-stu-id="8c4ee-556">N/A</span></span>|  
|<span data-ttu-id="8c4ee-557">password="chaîne"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-557">password="string"</span></span>|<span data-ttu-id="8c4ee-558">Mot de passe à utiliser pour l’authentification auprès du proxy.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="8c4ee-559">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-559">No</span></span>|<span data-ttu-id="8c4ee-560">N/A </span><span class="sxs-lookup"><span data-stu-id="8c4ee-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="8c4ee-561">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-561">Usage</span></span>  
 <span data-ttu-id="8c4ee-562">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-563">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="8c4ee-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8c4ee-564">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="8c4ee-565"><a name="SetRequestMethod"></a> Set request method</span><span class="sxs-lookup"><span data-stu-id="8c4ee-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="8c4ee-566">La stratégie `set-method` permet de modifier la méthode d’une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-567">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-568">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-568">Example</span></span>  
 <span data-ttu-id="8c4ee-569">Cet exemple de stratégie, qui utilise la stratégie `set-method`, montre un exemple d’envoi d’un message à une salle de conversation Slack si le code de la réponse HTTP est supérieur ou égal à 500.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="8c4ee-570">Pour plus d’informations sur cet exemple, consultez la page [Utilisation de services externes à partir du service Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-571">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-571">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-572">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-572">Element</span></span>|<span data-ttu-id="8c4ee-573">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-573">Description</span></span>|<span data-ttu-id="8c4ee-574">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-575">set-method</span><span class="sxs-lookup"><span data-stu-id="8c4ee-575">set-method</span></span>|<span data-ttu-id="8c4ee-576">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-576">Root element.</span></span> <span data-ttu-id="8c4ee-577">La valeur de l’élément spécifie la méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="8c4ee-578">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-579">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-579">Usage</span></span>  
 <span data-ttu-id="8c4ee-580">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-581">**Sections de la stratégie :** inbound, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-582">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-583"><a name="SetStatus"></a> Set status code</span><span class="sxs-lookup"><span data-stu-id="8c4ee-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="8c4ee-584">La stratégie `set-status` permet de donner la valeur spécifiée au code d’état HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-585">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-586">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-586">Example</span></span>  
 <span data-ttu-id="8c4ee-587">Cet exemple montre comment renvoyer une réponse 401 si le jeton d’autorisation n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="8c4ee-588">Pour plus d’informations, consultez la page [Utiliser des services externes à partir du service Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-589">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-589">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-590">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-590">Element</span></span>|<span data-ttu-id="8c4ee-591">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-591">Description</span></span>|<span data-ttu-id="8c4ee-592">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-593">set-status</span><span class="sxs-lookup"><span data-stu-id="8c4ee-593">set-status</span></span>|<span data-ttu-id="8c4ee-594">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-594">Root element.</span></span>|<span data-ttu-id="8c4ee-595">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-596">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-596">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-597">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-597">Attribute</span></span>|<span data-ttu-id="8c4ee-598">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-598">Description</span></span>|<span data-ttu-id="8c4ee-599">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-599">Required</span></span>|<span data-ttu-id="8c4ee-600">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-601">code="integer"</span></span>|<span data-ttu-id="8c4ee-602">Code d’état HTTP à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-602">The HTTP status code to return.</span></span>|<span data-ttu-id="8c4ee-603">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-603">Yes</span></span>|<span data-ttu-id="8c4ee-604">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-604">N/A</span></span>|  
|<span data-ttu-id="8c4ee-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="8c4ee-605">reason="string"</span></span>|<span data-ttu-id="8c4ee-606">Description du motif pour lequel le code d’état est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="8c4ee-607">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-607">Yes</span></span>|<span data-ttu-id="8c4ee-608">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-609">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-609">Usage</span></span>  
 <span data-ttu-id="8c4ee-610">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-611">**Sections de la stratégie :** outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-612">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="8c4ee-613"><a name="set-variable"></a> Set variable</span><span class="sxs-lookup"><span data-stu-id="8c4ee-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="8c4ee-614">La stratégie `set-variable` déclare une variable de [contexte](api-management-policy-expressions.md#ContextVariables) et lui affecte une valeur spécifiée par le biais d’une [expression](api-management-policy-expressions.md) ou d’un littéral chaîne.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="8c4ee-615">Si l’expression contient un littéral, il sera converti en chaîne et le type de la valeur sera `System.String`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="8c4ee-616"><a name="set-variablePolicyStatement"></a> Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="8c4ee-617"><a name="set-variableExample"></a> Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="8c4ee-618">L’exemple suivant montre une stratégie set variable dans la section inbound.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="8c4ee-619">Cette stratégie set variable crée une variable de [contexte](api-management-policy-expressions.md#ContextVariables) `isMobile` booléenne qui a la valeur true si l’en-tête de demande `User-Agent` contient le texte `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="8c4ee-620">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-620">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-621">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-621">Element</span></span>|<span data-ttu-id="8c4ee-622">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-622">Description</span></span>|<span data-ttu-id="8c4ee-623">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="8c4ee-624">set-variable</span></span>|<span data-ttu-id="8c4ee-625">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-625">Root element.</span></span>|<span data-ttu-id="8c4ee-626">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-627">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-627">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-628">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-628">Attribute</span></span>|<span data-ttu-id="8c4ee-629">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-629">Description</span></span>|<span data-ttu-id="8c4ee-630">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-631">name</span><span class="sxs-lookup"><span data-stu-id="8c4ee-631">name</span></span>|<span data-ttu-id="8c4ee-632">Nom de la variable.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-632">The name of the variable.</span></span>|<span data-ttu-id="8c4ee-633">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-633">Yes</span></span>|  
|<span data-ttu-id="8c4ee-634">value</span><span class="sxs-lookup"><span data-stu-id="8c4ee-634">value</span></span>|<span data-ttu-id="8c4ee-635">Valeur de la variable.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-635">The value of the variable.</span></span> <span data-ttu-id="8c4ee-636">Peut être une expression ou une valeur littérale.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="8c4ee-637">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-638">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-638">Usage</span></span>  
 <span data-ttu-id="8c4ee-639">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-640">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-641">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="8c4ee-642"><a name="set-variableAllowedTypes"></a> Types autorisés</span><span class="sxs-lookup"><span data-stu-id="8c4ee-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="8c4ee-643">Les expressions utilisées dans la stratégie `set-variable` doivent renvoyer un des types de base suivants.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="8c4ee-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="8c4ee-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="8c4ee-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="8c4ee-645">System.SByte</span></span>  
  
-   <span data-ttu-id="8c4ee-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="8c4ee-646">System.Byte</span></span>  
  
-   <span data-ttu-id="8c4ee-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="8c4ee-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="8c4ee-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="8c4ee-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="8c4ee-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="8c4ee-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="8c4ee-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="8c4ee-650">System.Int16</span></span>  
  
-   <span data-ttu-id="8c4ee-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="8c4ee-651">System.Int32</span></span>  
  
-   <span data-ttu-id="8c4ee-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="8c4ee-652">System.Int64</span></span>  
  
-   <span data-ttu-id="8c4ee-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="8c4ee-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="8c4ee-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="8c4ee-654">System.Single</span></span>  
  
-   <span data-ttu-id="8c4ee-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="8c4ee-655">System.Double</span></span>  
  
-   <span data-ttu-id="8c4ee-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="8c4ee-656">System.Guid</span></span>  
  
-   <span data-ttu-id="8c4ee-657">System.String</span><span class="sxs-lookup"><span data-stu-id="8c4ee-657">System.String</span></span>  
  
-   <span data-ttu-id="8c4ee-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="8c4ee-658">System.Char</span></span>  
  
-   <span data-ttu-id="8c4ee-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="8c4ee-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="8c4ee-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8c4ee-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="8c4ee-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="8c4ee-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="8c4ee-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="8c4ee-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="8c4ee-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="8c4ee-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="8c4ee-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="8c4ee-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="8c4ee-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-669">System.Single?</span></span>  
  
-   <span data-ttu-id="8c4ee-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-670">System.Double?</span></span>  
  
-   <span data-ttu-id="8c4ee-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="8c4ee-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-672">System.String?</span></span>  
  
-   <span data-ttu-id="8c4ee-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-673">System.Char?</span></span>  
  
-   <span data-ttu-id="8c4ee-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="8c4ee-674">System.DateTime?</span></span>  

##  <span data-ttu-id="8c4ee-675"><a name="Trace"></a> Trace</span><span class="sxs-lookup"><span data-stu-id="8c4ee-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="8c4ee-676">La stratégie `trace` ajoute une chaîne à la sortie de [l’Inspecteur d’API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="8c4ee-677">La stratégie s’exécute uniquement lorsque le traçage est déclenché, c’est-à-dire que l’en-tête de la demande `Ocp-Apim-Trace` est présent et a la valeur `true` et que l’en-tête de la demande `Ocp-Apim-Subscription-Key` est présent et contient une clé valide associée au compte Administrateur.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-678">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="8c4ee-679">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-679">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-680">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-680">Element</span></span>|<span data-ttu-id="8c4ee-681">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-681">Description</span></span>|<span data-ttu-id="8c4ee-682">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-683">trace</span><span class="sxs-lookup"><span data-stu-id="8c4ee-683">trace</span></span>|<span data-ttu-id="8c4ee-684">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-684">Root element.</span></span>|<span data-ttu-id="8c4ee-685">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-686">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-686">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-687">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-687">Attribute</span></span>|<span data-ttu-id="8c4ee-688">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-688">Description</span></span>|<span data-ttu-id="8c4ee-689">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-689">Required</span></span>|<span data-ttu-id="8c4ee-690">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-691">source</span><span class="sxs-lookup"><span data-stu-id="8c4ee-691">source</span></span>|<span data-ttu-id="8c4ee-692">Littéral chaîne significatif pour la visionneuse de trace, qui spécifie la source du message.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="8c4ee-693">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-693">Yes</span></span>|<span data-ttu-id="8c4ee-694">N/A</span><span class="sxs-lookup"><span data-stu-id="8c4ee-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-695">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-695">Usage</span></span>  
 <span data-ttu-id="8c4ee-696">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="8c4ee-697">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="8c4ee-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="8c4ee-698">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="8c4ee-699"><a name="Wait"></a> Wait</span><span class="sxs-lookup"><span data-stu-id="8c4ee-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="8c4ee-700">La stratégie `wait` exécute ses stratégies enfants immédiates en parallèle et attend la fin de la totalité ou de l’une de ses stratégies enfants immédiates pour se terminer.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="8c4ee-701">La stratégie d’attente peut avoir comme stratégies enfants immédiates les stratégies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) et [Control flow](api-management-advanced-policies.md#choose).</span><span class="sxs-lookup"><span data-stu-id="8c4ee-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8c4ee-702">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="8c4ee-703">Exemple</span><span class="sxs-lookup"><span data-stu-id="8c4ee-703">Example</span></span>  
 <span data-ttu-id="8c4ee-704">Dans l’exemple suivant, deux stratégies `choose` sont les stratégies enfants immédiates de la stratégie `wait`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="8c4ee-705">Ces deux stratégies `choose` s’exécutent en parallèle.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="8c4ee-706">Chaque stratégie `choose` essaie de récupérer une valeur en cache.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="8c4ee-707">En cas d’échec de cache, un service principal est appelé pour fournir la valeur.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="8c4ee-708">Dans cet exemple, la stratégie `wait` ne se termine pas tant que toutes ses stratégies enfants immédiates ne sont pas terminées, car l’attribut `for` a la valeur `all`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="8c4ee-709">Dans cet exemple, les variables de contexte (`execute-branch-one`, `value-one`, `execute-branch-two` et `value-two`) sont déclarées hors de l’étendue de cet exemple de stratégie.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8c4ee-710">Éléments</span><span class="sxs-lookup"><span data-stu-id="8c4ee-710">Elements</span></span>  
  
|<span data-ttu-id="8c4ee-711">Élément</span><span class="sxs-lookup"><span data-stu-id="8c4ee-711">Element</span></span>|<span data-ttu-id="8c4ee-712">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-712">Description</span></span>|<span data-ttu-id="8c4ee-713">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="8c4ee-714">wait</span><span class="sxs-lookup"><span data-stu-id="8c4ee-714">wait</span></span>|<span data-ttu-id="8c4ee-715">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-715">Root element.</span></span> <span data-ttu-id="8c4ee-716">Ne peut contenir comme éléments enfants que les stratégies `send-request`, `cache-lookup-value` et `choose`.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="8c4ee-717">Oui</span><span class="sxs-lookup"><span data-stu-id="8c4ee-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8c4ee-718">Attributs</span><span class="sxs-lookup"><span data-stu-id="8c4ee-718">Attributes</span></span>  
  
|<span data-ttu-id="8c4ee-719">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c4ee-719">Attribute</span></span>|<span data-ttu-id="8c4ee-720">Description</span><span class="sxs-lookup"><span data-stu-id="8c4ee-720">Description</span></span>|<span data-ttu-id="8c4ee-721">Requis</span><span class="sxs-lookup"><span data-stu-id="8c4ee-721">Required</span></span>|<span data-ttu-id="8c4ee-722">Default</span><span class="sxs-lookup"><span data-stu-id="8c4ee-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="8c4ee-723">for</span><span class="sxs-lookup"><span data-stu-id="8c4ee-723">for</span></span>|<span data-ttu-id="8c4ee-724">Détermine si la stratégie `wait` attend la fin de toutes les stratégies enfants immédiates ou d’une seule.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="8c4ee-725">Les valeurs autorisées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c4ee-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="8c4ee-726">-   `all` : attend la fin de toutes les stratégies enfants immédiates.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="8c4ee-727">- any : attend la fin d’une stratégie enfant immédiate.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="8c4ee-728">Une fois la première stratégie enfant immédiate terminée, la stratégie `wait` se termine et l’exécution de toutes les autres stratégies enfants immédiates est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="8c4ee-729">Non</span><span class="sxs-lookup"><span data-stu-id="8c4ee-729">No</span></span>|<span data-ttu-id="8c4ee-730">tout</span><span class="sxs-lookup"><span data-stu-id="8c4ee-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8c4ee-731">Usage</span><span class="sxs-lookup"><span data-stu-id="8c4ee-731">Usage</span></span>  
 <span data-ttu-id="8c4ee-732">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8c4ee-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8c4ee-733">**Sections de la stratégie :** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="8c4ee-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="8c4ee-734">**Étendues de la stratégie :** toutes les étendues</span><span class="sxs-lookup"><span data-stu-id="8c4ee-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8c4ee-735">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c4ee-735">Next steps</span></span>
<span data-ttu-id="8c4ee-736">Pour plus d’informations sur l’utilisation de stratégies, consultez les pages :</span><span class="sxs-lookup"><span data-stu-id="8c4ee-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="8c4ee-737">Stratégies dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="8c4ee-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="8c4ee-738">Expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="8c4ee-738">Policy expressions</span></span>](api-management-policy-expressions.md)
