---
title: "stratégies de restriction de l’accès de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies de restriction hello accès disponibles pour une utilisation dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="48c1e-103">Stratégies de restriction des accès de la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="48c1e-103">API Management access restriction policies</span></span>
<span data-ttu-id="48c1e-104">Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="48c1e-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="48c1e-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="48c1e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="48c1e-106"><a name="AccessRestrictionPolicies"></a> Stratégies de restriction des accès</span><span class="sxs-lookup"><span data-stu-id="48c1e-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="48c1e-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) : applique l’existence et/ou la valeur d’un en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48c1e-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="48c1e-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.</span><span class="sxs-lookup"><span data-stu-id="48c1e-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="48c1e-109">[Limit call rate by key](#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="48c1e-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtre (autorise/rejette) les appels de certaines adresses IP spécifiques et/ou de certaines plages d’adresses.</span><span class="sxs-lookup"><span data-stu-id="48c1e-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="48c1e-111">[Définir le quota d’utilisation par abonnement](api-management-access-restriction-policies.md#SetUsageQuota) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.</span><span class="sxs-lookup"><span data-stu-id="48c1e-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="48c1e-112">[Définir le quota d’utilisation par clé](#SetUsageQuotaByKey) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par clé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="48c1e-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="48c1e-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="48c1e-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span><span class="sxs-lookup"><span data-stu-id="48c1e-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="48c1e-115">Hello d’utilisation `check-header` tooenforce stratégie qu’une demande ait un en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48c1e-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="48c1e-116">Vous pouvez éventuellement vérifier toosee si l’en-tête hello a une valeur spécifique ou une vérification pour une plage de valeurs autorisées.</span><span class="sxs-lookup"><span data-stu-id="48c1e-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="48c1e-117">Si hello vérification échoue, stratégie de hello termine le traitement de la demande et renvoie hello erreur et le code message d’état HTTP spécifié par la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-118">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="48c1e-119">Exemple</span><span class="sxs-lookup"><span data-stu-id="48c1e-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-120">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-120">Elements</span></span>  
  
|<span data-ttu-id="48c1e-121">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-121">Name</span></span>|<span data-ttu-id="48c1e-122">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-122">Description</span></span>|<span data-ttu-id="48c1e-123">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="48c1e-124">check-header</span><span class="sxs-lookup"><span data-stu-id="48c1e-124">check-header</span></span>|<span data-ttu-id="48c1e-125">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-125">Root element.</span></span>|<span data-ttu-id="48c1e-126">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-126">Yes</span></span>|  
|<span data-ttu-id="48c1e-127">value</span><span class="sxs-lookup"><span data-stu-id="48c1e-127">value</span></span>|<span data-ttu-id="48c1e-128">Valeur autorisée de l’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48c1e-128">Allowed HTTP header value.</span></span> <span data-ttu-id="48c1e-129">Lorsque plusieurs éléments de valeur sont spécifiées, la vérification de hello est considérée comme un succès si l’une des valeurs de hello est une correspondance.</span><span class="sxs-lookup"><span data-stu-id="48c1e-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="48c1e-130">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-131">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-131">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-132">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-132">Name</span></span>|<span data-ttu-id="48c1e-133">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-133">Description</span></span>|<span data-ttu-id="48c1e-134">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-134">Required</span></span>|<span data-ttu-id="48c1e-135">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="48c1e-136">failed-check-error-message</span></span>|<span data-ttu-id="48c1e-137">Erreur tooreturn de message dans le corps de la réponse hello HTTP si l’en-tête de hello n’existe pas ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="48c1e-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="48c1e-138">Les éventuels caractères spéciaux de ce message doivent être correctement placés dans une séquence d’échappement.</span><span class="sxs-lookup"><span data-stu-id="48c1e-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="48c1e-139">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-139">Yes</span></span>|<span data-ttu-id="48c1e-140">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-140">N/A</span></span>|  
|<span data-ttu-id="48c1e-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="48c1e-141">failed-check-httpcode</span></span>|<span data-ttu-id="48c1e-142">État HTTP code tooreturn si l’en-tête de hello n’existe pas ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="48c1e-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="48c1e-143">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-143">Yes</span></span>|<span data-ttu-id="48c1e-144">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-144">N/A</span></span>|  
|<span data-ttu-id="48c1e-145">header-name</span><span class="sxs-lookup"><span data-stu-id="48c1e-145">header-name</span></span>|<span data-ttu-id="48c1e-146">nom Hello Hello toocheck d’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48c1e-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="48c1e-147">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-147">Yes</span></span>|<span data-ttu-id="48c1e-148">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-148">N/A</span></span>|  
|<span data-ttu-id="48c1e-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="48c1e-149">ignore-case</span></span>|<span data-ttu-id="48c1e-150">Peut être défini tooTrue ou False.</span><span class="sxs-lookup"><span data-stu-id="48c1e-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="48c1e-151">Si le cas de tooTrue set est ignoré lorsque la valeur d’en-tête hello est comparée à ensemble hello des valeurs acceptables.</span><span class="sxs-lookup"><span data-stu-id="48c1e-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="48c1e-152">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-152">Yes</span></span>|<span data-ttu-id="48c1e-153">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-154">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-154">Usage</span></span>  
 <span data-ttu-id="48c1e-155">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-156">**Sections de la stratégie :** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="48c1e-157">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="48c1e-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span><span class="sxs-lookup"><span data-stu-id="48c1e-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="48c1e-159">Hello `rate-limit` stratégie empêche l’utilisation de l’API pics sur une base par abonnement en limitant hello numéro d’appel de tooa taux spécifié par une période de temps.</span><span class="sxs-lookup"><span data-stu-id="48c1e-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="48c1e-160">Lorsque cette stratégie est déclenchée appelant de hello reçoit un `429 Too Many Requests` code d’état de réponse.</span><span class="sxs-lookup"><span data-stu-id="48c1e-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="48c1e-161">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="48c1e-162">[Expressions de stratégie](api-management-policy-expressions.md) ne peut pas être utilisé dans un des attributs de stratégie hello pour cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-163">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="48c1e-164">Exemple</span><span class="sxs-lookup"><span data-stu-id="48c1e-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-165">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-165">Elements</span></span>  
  
|<span data-ttu-id="48c1e-166">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-166">Name</span></span>|<span data-ttu-id="48c1e-167">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-167">Description</span></span>|<span data-ttu-id="48c1e-168">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="48c1e-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="48c1e-169">set-limit</span></span>|<span data-ttu-id="48c1e-170">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-170">Root element.</span></span>|<span data-ttu-id="48c1e-171">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-171">Yes</span></span>|  
|<span data-ttu-id="48c1e-172">api</span><span class="sxs-lookup"><span data-stu-id="48c1e-172">api</span></span>|<span data-ttu-id="48c1e-173">Ajoutez un ou plusieurs de ces éléments de tooimpose une limite de taux d’appels sur les API au sein du produit de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="48c1e-174">Les limites de débit d’appels au niveau du produit et de l’API s’appliquent indépendamment les unes des autres.</span><span class="sxs-lookup"><span data-stu-id="48c1e-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="48c1e-175">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-175">No</span></span>|  
|<span data-ttu-id="48c1e-176">operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-176">operation</span></span>|<span data-ttu-id="48c1e-177">Ajouter un ou plusieurs de ces éléments de tooimpose une limite de taux d’appels sur les opérations à l’intérieur d’une API.</span><span class="sxs-lookup"><span data-stu-id="48c1e-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="48c1e-178">Les limites de débit d’appels au niveau du produit, de l’API et de l’opération s’appliquent indépendamment les unes des autres.</span><span class="sxs-lookup"><span data-stu-id="48c1e-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="48c1e-179">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-180">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-180">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-181">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-181">Name</span></span>|<span data-ttu-id="48c1e-182">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-182">Description</span></span>|<span data-ttu-id="48c1e-183">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-183">Required</span></span>|<span data-ttu-id="48c1e-184">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-185">name</span><span class="sxs-lookup"><span data-stu-id="48c1e-185">name</span></span>|<span data-ttu-id="48c1e-186">nom de Hello Hello API pour lesquelles limite de taux tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="48c1e-187">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-187">Yes</span></span>|<span data-ttu-id="48c1e-188">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-188">N/A</span></span>|  
|<span data-ttu-id="48c1e-189">calls</span><span class="sxs-lookup"><span data-stu-id="48c1e-189">calls</span></span>|<span data-ttu-id="48c1e-190">Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="48c1e-191">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-191">Yes</span></span>|<span data-ttu-id="48c1e-192">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-192">N/A</span></span>|  
|<span data-ttu-id="48c1e-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="48c1e-193">renewal-period</span></span>|<span data-ttu-id="48c1e-194">Hello laps de temps en secondes après lequel hello quota est réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="48c1e-195">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-195">Yes</span></span>|<span data-ttu-id="48c1e-196">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-197">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-197">Usage</span></span>  
 <span data-ttu-id="48c1e-198">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-199">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="48c1e-200">**Étendues de la stratégie :** product</span><span class="sxs-lookup"><span data-stu-id="48c1e-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="48c1e-201"><a name="LimitCallRateByKey"></a> Limite de débit d’appels par clé</span><span class="sxs-lookup"><span data-stu-id="48c1e-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="48c1e-202">Hello `rate-limit-by-key` stratégie empêche l’utilisation de l’API pics sur une base par clé en limitant hello numéro d’appel de tooa taux spécifié par une période de temps.</span><span class="sxs-lookup"><span data-stu-id="48c1e-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="48c1e-203">clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="48c1e-204">Condition d’incrément facultatif peut être ajoutée toospecify les requêtes qui doivent être comptés dans nombre maximal de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="48c1e-205">Lorsque cette stratégie est déclenchée appelant de hello reçoit un `429 Too Many Requests` code d’état de réponse.</span><span class="sxs-lookup"><span data-stu-id="48c1e-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="48c1e-206">Pour plus d’informations et d’exemples sur cette stratégie, consultez la page [Limitation avancée des demandes dans la Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="48c1e-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="48c1e-207">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-208">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="48c1e-209">Exemple</span><span class="sxs-lookup"><span data-stu-id="48c1e-209">Example</span></span>  
 <span data-ttu-id="48c1e-210">Dans l’exemple suivant de hello, limite de taux hello est indexé par adresse IP de l’appelant hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-211">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-211">Elements</span></span>  
  
|<span data-ttu-id="48c1e-212">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-212">Name</span></span>|<span data-ttu-id="48c1e-213">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-213">Description</span></span>|<span data-ttu-id="48c1e-214">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="48c1e-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="48c1e-215">set-limit</span></span>|<span data-ttu-id="48c1e-216">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-216">Root element.</span></span>|<span data-ttu-id="48c1e-217">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-218">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-218">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-219">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-219">Name</span></span>|<span data-ttu-id="48c1e-220">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-220">Description</span></span>|<span data-ttu-id="48c1e-221">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-221">Required</span></span>|<span data-ttu-id="48c1e-222">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-223">calls</span><span class="sxs-lookup"><span data-stu-id="48c1e-223">calls</span></span>|<span data-ttu-id="48c1e-224">Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="48c1e-225">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-225">Yes</span></span>|<span data-ttu-id="48c1e-226">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-226">N/A</span></span>|  
|<span data-ttu-id="48c1e-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="48c1e-227">counter-key</span></span>|<span data-ttu-id="48c1e-228">Hello toouse clé pour la stratégie de limite de taux de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="48c1e-229">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-229">Yes</span></span>|<span data-ttu-id="48c1e-230">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-230">N/A</span></span>|  
|<span data-ttu-id="48c1e-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="48c1e-231">increment-condition</span></span>|<span data-ttu-id="48c1e-232">expression booléenne de Hello spécifiant si la demande de hello doit être comptée vers le quota de hello (`true`).</span><span class="sxs-lookup"><span data-stu-id="48c1e-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="48c1e-233">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-233">No</span></span>|<span data-ttu-id="48c1e-234">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-234">N/A</span></span>|  
|<span data-ttu-id="48c1e-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="48c1e-235">renewal-period</span></span>|<span data-ttu-id="48c1e-236">Hello laps de temps en secondes après lequel hello quota est réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="48c1e-237">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-237">Yes</span></span>|<span data-ttu-id="48c1e-238">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-239">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-239">Usage</span></span>  
 <span data-ttu-id="48c1e-240">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-241">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="48c1e-242">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="48c1e-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span><span class="sxs-lookup"><span data-stu-id="48c1e-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="48c1e-244">Hello `ip-filter` stratégie filtre (autorise/refuse) des appels à partir de plages d’adresses et/ou des adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="48c1e-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-245">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="48c1e-246">Exemple</span><span class="sxs-lookup"><span data-stu-id="48c1e-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-247">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-247">Elements</span></span>  
  
|<span data-ttu-id="48c1e-248">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-248">Name</span></span>|<span data-ttu-id="48c1e-249">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-249">Description</span></span>|<span data-ttu-id="48c1e-250">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="48c1e-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="48c1e-251">ip-filter</span></span>|<span data-ttu-id="48c1e-252">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-252">Root element.</span></span>|<span data-ttu-id="48c1e-253">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-253">Yes</span></span>|  
|<span data-ttu-id="48c1e-254">address</span><span class="sxs-lookup"><span data-stu-id="48c1e-254">address</span></span>|<span data-ttu-id="48c1e-255">Spécifie une adresse IP unique sur le toofilter.</span><span class="sxs-lookup"><span data-stu-id="48c1e-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="48c1e-256">Au moins un élément `address` ou `address-range` est requis.</span><span class="sxs-lookup"><span data-stu-id="48c1e-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="48c1e-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="48c1e-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="48c1e-258">Spécifie une plage d’adresses IP sur quel toofilter.</span><span class="sxs-lookup"><span data-stu-id="48c1e-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="48c1e-259">Au moins un élément `address` ou `address-range` est requis.</span><span class="sxs-lookup"><span data-stu-id="48c1e-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-260">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-260">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-261">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-261">Name</span></span>|<span data-ttu-id="48c1e-262">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-262">Description</span></span>|<span data-ttu-id="48c1e-263">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-263">Required</span></span>|<span data-ttu-id="48c1e-264">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="48c1e-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="48c1e-266">Une plage d’adresse IP, adresses tooallow ou refuser l’accès.</span><span class="sxs-lookup"><span data-stu-id="48c1e-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="48c1e-267">Obligatoire lorsque hello `address-range` élément est utilisé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="48c1e-268">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-268">N/A</span></span>|  
|<span data-ttu-id="48c1e-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="48c1e-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="48c1e-270">Spécifie si les appels doivent être autorisés ou non pour hello spécifié adresses IP et plages.</span><span class="sxs-lookup"><span data-stu-id="48c1e-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="48c1e-271">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-271">Yes</span></span>|<span data-ttu-id="48c1e-272">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-273">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-273">Usage</span></span>  
 <span data-ttu-id="48c1e-274">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-275">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="48c1e-276">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="48c1e-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span><span class="sxs-lookup"><span data-stu-id="48c1e-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="48c1e-278">Hello `quota` stratégie applique un quota renouvelable ou durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.</span><span class="sxs-lookup"><span data-stu-id="48c1e-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="48c1e-279">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="48c1e-280">[Expressions de stratégie](api-management-policy-expressions.md) ne peut pas être utilisé dans un des attributs de stratégie hello pour cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-281">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="48c1e-282">Exemple</span><span class="sxs-lookup"><span data-stu-id="48c1e-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-283">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-283">Elements</span></span>  
  
|<span data-ttu-id="48c1e-284">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-284">Name</span></span>|<span data-ttu-id="48c1e-285">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-285">Description</span></span>|<span data-ttu-id="48c1e-286">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="48c1e-287">quota</span><span class="sxs-lookup"><span data-stu-id="48c1e-287">quota</span></span>|<span data-ttu-id="48c1e-288">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-288">Root element.</span></span>|<span data-ttu-id="48c1e-289">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-289">Yes</span></span>|  
|<span data-ttu-id="48c1e-290">api</span><span class="sxs-lookup"><span data-stu-id="48c1e-290">api</span></span>|<span data-ttu-id="48c1e-291">Ajoutez un ou plusieurs de ces éléments de tooimpose un quota sur les API au sein du produit de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="48c1e-292">Les quotas au niveau du produit et de l’API s’appliquent indépendamment les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="48c1e-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="48c1e-293">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-293">No</span></span>|  
|<span data-ttu-id="48c1e-294">operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-294">operation</span></span>|<span data-ttu-id="48c1e-295">Ajouter un ou plusieurs de ces éléments de tooimpose un quota sur les opérations à l’intérieur d’une API.</span><span class="sxs-lookup"><span data-stu-id="48c1e-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="48c1e-296">Les quotas au niveau du produit, de l’API et de l’opération s’appliquent indépendamment les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="48c1e-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="48c1e-297">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-298">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-298">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-299">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-299">Name</span></span>|<span data-ttu-id="48c1e-300">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-300">Description</span></span>|<span data-ttu-id="48c1e-301">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-301">Required</span></span>|<span data-ttu-id="48c1e-302">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-303">name</span><span class="sxs-lookup"><span data-stu-id="48c1e-303">name</span></span>|<span data-ttu-id="48c1e-304">nom de Hello de hello API ou l’opération pour le hello quota s’applique.</span><span class="sxs-lookup"><span data-stu-id="48c1e-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="48c1e-305">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-305">Yes</span></span>|<span data-ttu-id="48c1e-306">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-306">N/A</span></span>|  
|<span data-ttu-id="48c1e-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="48c1e-307">bandwidth</span></span>|<span data-ttu-id="48c1e-308">Hello nombre total maximal de kilo-octets autorisé durant la période hello spécifié dans hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="48c1e-309">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="48c1e-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="48c1e-310">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-310">N/A</span></span>|  
|<span data-ttu-id="48c1e-311">calls</span><span class="sxs-lookup"><span data-stu-id="48c1e-311">calls</span></span>|<span data-ttu-id="48c1e-312">Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="48c1e-313">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="48c1e-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="48c1e-314">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-314">N/A</span></span>|  
|<span data-ttu-id="48c1e-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="48c1e-315">renewal-period</span></span>|<span data-ttu-id="48c1e-316">Hello laps de temps en secondes après lequel hello quota est réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="48c1e-317">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-317">Yes</span></span>|<span data-ttu-id="48c1e-318">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-319">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-319">Usage</span></span>  
 <span data-ttu-id="48c1e-320">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-321">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="48c1e-322">**Étendues de la stratégie :** product</span><span class="sxs-lookup"><span data-stu-id="48c1e-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="48c1e-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span><span class="sxs-lookup"><span data-stu-id="48c1e-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="48c1e-324">Hello `quota-by-key` stratégie applique un quota renouvelable ou durée de vie appel volume et/ou de la bande passante, sur une base par clé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="48c1e-325">clé de Hello peut avoir une valeur de chaîne arbitraire et est généralement fourni à l’aide d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="48c1e-326">Condition d’incrément facultatif peut être ajoutée toospecify quelles demandes doivent être comptabilisées dans le quota de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="48c1e-327">Pour plus d’informations et d’exemples sur cette stratégie, consultez la page [Limitation avancée des demandes dans la Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="48c1e-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="48c1e-328">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="48c1e-329">[Expressions de stratégie](api-management-policy-expressions.md) ne peut pas être utilisé dans un des attributs de stratégie hello pour cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="48c1e-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-330">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="48c1e-331">Exemple</span><span class="sxs-lookup"><span data-stu-id="48c1e-331">Example</span></span>  
 <span data-ttu-id="48c1e-332">Dans l’exemple suivant de hello, quota de hello est indexé par adresse IP de l’appelant hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-333">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-333">Elements</span></span>  
  
|<span data-ttu-id="48c1e-334">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-334">Name</span></span>|<span data-ttu-id="48c1e-335">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-335">Description</span></span>|<span data-ttu-id="48c1e-336">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="48c1e-337">quota</span><span class="sxs-lookup"><span data-stu-id="48c1e-337">quota</span></span>|<span data-ttu-id="48c1e-338">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-338">Root element.</span></span>|<span data-ttu-id="48c1e-339">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-340">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-340">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-341">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-341">Name</span></span>|<span data-ttu-id="48c1e-342">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-342">Description</span></span>|<span data-ttu-id="48c1e-343">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-343">Required</span></span>|<span data-ttu-id="48c1e-344">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="48c1e-345">bandwidth</span></span>|<span data-ttu-id="48c1e-346">Hello nombre total maximal de kilo-octets autorisé durant la période hello spécifié dans hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="48c1e-347">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="48c1e-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="48c1e-348">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-348">N/A</span></span>|  
|<span data-ttu-id="48c1e-349">calls</span><span class="sxs-lookup"><span data-stu-id="48c1e-349">calls</span></span>|<span data-ttu-id="48c1e-350">Hello nombre maximal d’appels autorisés au cours de l’intervalle de temps hello spécifié dans hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="48c1e-351">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="48c1e-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="48c1e-352">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-352">N/A</span></span>|  
|<span data-ttu-id="48c1e-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="48c1e-353">counter-key</span></span>|<span data-ttu-id="48c1e-354">Hello toouse clé pour la stratégie de quota hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="48c1e-355">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-355">Yes</span></span>|<span data-ttu-id="48c1e-356">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-356">N/A</span></span>|  
|<span data-ttu-id="48c1e-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="48c1e-357">increment-condition</span></span>|<span data-ttu-id="48c1e-358">expression booléenne de Hello spécifiant si la demande de hello doit être comptée vers le quota de hello (`true`)</span><span class="sxs-lookup"><span data-stu-id="48c1e-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="48c1e-359">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-359">No</span></span>|<span data-ttu-id="48c1e-360">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-360">N/A</span></span>|  
|<span data-ttu-id="48c1e-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="48c1e-361">renewal-period</span></span>|<span data-ttu-id="48c1e-362">Hello laps de temps en secondes après lequel hello quota est réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="48c1e-363">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-363">Yes</span></span>|<span data-ttu-id="48c1e-364">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-365">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-365">Usage</span></span>  
 <span data-ttu-id="48c1e-366">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-367">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="48c1e-368">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="48c1e-369"><a name="ValidateJWT"></a> Validate JWT</span><span class="sxs-lookup"><span data-stu-id="48c1e-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="48c1e-370">Hello `validate-jwt` stratégie applique l’existence et la validité d’un jeton JWT extrait de soit un en-tête HTTP ou un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="48c1e-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="48c1e-371">Hello `validate-jwt` stratégie nécessite que hello `exp` revendication inscrite est inclus dans le jeton JWT de hello, sauf si `require-expiration-time` attribut est spécifié et possède trop`false`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="48c1e-372">Hello `validate-jwt` stratégie prend en charge les algorithmes de signature HS256 et RS256.</span><span class="sxs-lookup"><span data-stu-id="48c1e-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="48c1e-373">Pour HS256 clé de hello doit être fourni inline dans la stratégie hello sous forme de codé en base64 hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="48c1e-374">Pour RS256 hello fait clé toobe fournir via un point de terminaison de configuration Open ID.</span><span class="sxs-lookup"><span data-stu-id="48c1e-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="48c1e-375">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="48c1e-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="48c1e-376">Exemples</span><span class="sxs-lookup"><span data-stu-id="48c1e-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="48c1e-377">Validation d’un jeton Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="48c1e-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="48c1e-378">Validation d’un jeton Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48c1e-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="48c1e-379">Validation d’un jeton Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="48c1e-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="48c1e-380">Autoriser les toooperations d’accès basées sur les revendications de jeton</span><span class="sxs-lookup"><span data-stu-id="48c1e-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="48c1e-381">Cet exemple montre comment toouse hello [valider les jetons Web JSON](api-management-access-restriction-policies.md#ValidateJWT) stratégie toopre-autoriser toooperations d’accès basées sur les revendications de jeton.</span><span class="sxs-lookup"><span data-stu-id="48c1e-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="48c1e-382">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too13:50.</span><span class="sxs-lookup"><span data-stu-id="48c1e-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="48c1e-383">Avance rapide too15:00 les stratégies de hello toosee configurées dans l’éditeur de stratégie hello et puis too18:50 pour une démonstration de l’appel d’une opération à partir du portail des développeurs hello avec et sans hello requis jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="48c1e-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="48c1e-384">Éléments</span><span class="sxs-lookup"><span data-stu-id="48c1e-384">Elements</span></span>  
  
|<span data-ttu-id="48c1e-385">Élément</span><span class="sxs-lookup"><span data-stu-id="48c1e-385">Element</span></span>|<span data-ttu-id="48c1e-386">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-386">Description</span></span>|<span data-ttu-id="48c1e-387">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="48c1e-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="48c1e-388">validate-jwt</span></span>|<span data-ttu-id="48c1e-389">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="48c1e-389">Root element.</span></span>|<span data-ttu-id="48c1e-390">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-390">Yes</span></span>|  
|<span data-ttu-id="48c1e-391">audiences</span><span class="sxs-lookup"><span data-stu-id="48c1e-391">audiences</span></span>|<span data-ttu-id="48c1e-392">Contient une liste de revendications d’audience acceptables qui peuvent être présents sur le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="48c1e-393">Si plusieurs valeurs d’audience sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse.</span><span class="sxs-lookup"><span data-stu-id="48c1e-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="48c1e-394">Au moins une audience doit être spécifiée.</span><span class="sxs-lookup"><span data-stu-id="48c1e-394">At least one audience must be specified.</span></span>|<span data-ttu-id="48c1e-395">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-395">No</span></span>|  
|<span data-ttu-id="48c1e-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="48c1e-396">issuer-signing-keys</span></span>|<span data-ttu-id="48c1e-397">Une liste de codée en Base64 de sécurité clés utilisées toovalidate signé des jetons.</span><span class="sxs-lookup"><span data-stu-id="48c1e-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="48c1e-398">Si plusieurs clés de sécurité sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse (utile pour la substitution de jeton).</span><span class="sxs-lookup"><span data-stu-id="48c1e-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="48c1e-399">Éléments clés ont une option `id` toomatch attribut utilisé par rapport à `kid` de revendication.</span><span class="sxs-lookup"><span data-stu-id="48c1e-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="48c1e-400">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-400">No</span></span>|  
|<span data-ttu-id="48c1e-401">issuers</span><span class="sxs-lookup"><span data-stu-id="48c1e-401">issuers</span></span>|<span data-ttu-id="48c1e-402">Une liste des principaux acceptables qui a émis le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="48c1e-403">Si plusieurs valeurs d’émetteur sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse.</span><span class="sxs-lookup"><span data-stu-id="48c1e-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="48c1e-404">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-404">No</span></span>|  
|<span data-ttu-id="48c1e-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="48c1e-405">openid-config</span></span>|<span data-ttu-id="48c1e-406">élément Hello utilisée pour spécifier une extrémité de configuration Open ID conformes à partir de laquelle des clés et l’émetteur de signature peut être obtenue.</span><span class="sxs-lookup"><span data-stu-id="48c1e-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="48c1e-407">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-407">No</span></span>|  
|<span data-ttu-id="48c1e-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="48c1e-408">required-claims</span></span>|<span data-ttu-id="48c1e-409">Contient une liste de toobe attendues des revendications présente sur le jeton de hello pour qu’il toobe considéré comme valide.</span><span class="sxs-lookup"><span data-stu-id="48c1e-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="48c1e-410">Hello lorsque `match` attribut est défini trop`all` chaque valeur de revendication dans la stratégie de hello doit être présent dans le jeton de hello pour toosucceed de validation.</span><span class="sxs-lookup"><span data-stu-id="48c1e-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="48c1e-411">Hello lorsque `match` attribut est défini trop`any` au moins une revendication doit être présente dans le jeton de hello pour toosucceed de validation.</span><span class="sxs-lookup"><span data-stu-id="48c1e-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="48c1e-412">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-412">No</span></span>|  
|<span data-ttu-id="48c1e-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="48c1e-413">zumo-master-key</span></span>|<span data-ttu-id="48c1e-414">Clé principale pour les jetons émis par Azure Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="48c1e-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="48c1e-415">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="48c1e-416">Attributs</span><span class="sxs-lookup"><span data-stu-id="48c1e-416">Attributes</span></span>  
  
|<span data-ttu-id="48c1e-417">Nom</span><span class="sxs-lookup"><span data-stu-id="48c1e-417">Name</span></span>|<span data-ttu-id="48c1e-418">Description</span><span class="sxs-lookup"><span data-stu-id="48c1e-418">Description</span></span>|<span data-ttu-id="48c1e-419">Requis</span><span class="sxs-lookup"><span data-stu-id="48c1e-419">Required</span></span>|<span data-ttu-id="48c1e-420">Default</span><span class="sxs-lookup"><span data-stu-id="48c1e-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="48c1e-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="48c1e-421">clock-skew</span></span>|<span data-ttu-id="48c1e-422">Intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="48c1e-422">Timespan.</span></span> <span data-ttu-id="48c1e-423">Fournit certains manœuvre petite en cas de revendication d’expiration du jeton hello est présente dans le jeton de hello et est en cours de hello au-delà de date / heure.</span><span class="sxs-lookup"><span data-stu-id="48c1e-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="48c1e-424">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-424">No</span></span>|<span data-ttu-id="48c1e-425">0 seconde</span><span class="sxs-lookup"><span data-stu-id="48c1e-425">0 seconds</span></span>|  
|<span data-ttu-id="48c1e-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="48c1e-426">failed-validation-error-message</span></span>|<span data-ttu-id="48c1e-427">Erreur tooreturn de message dans les corps de réponse HTTP de hello si hello JSON n’est pas validé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="48c1e-428">Les éventuels caractères spéciaux de ce message doivent être correctement placés dans une séquence d’échappement.</span><span class="sxs-lookup"><span data-stu-id="48c1e-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="48c1e-429">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-429">No</span></span>|<span data-ttu-id="48c1e-430">Le message d’erreur par défaut dépend du problème de validation, par exemple « JWT absent ».</span><span class="sxs-lookup"><span data-stu-id="48c1e-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="48c1e-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="48c1e-431">failed-validation-httpcode</span></span>|<span data-ttu-id="48c1e-432">État HTTP code tooreturn si hello JSON ne sont pas validées.</span><span class="sxs-lookup"><span data-stu-id="48c1e-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="48c1e-433">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-433">No</span></span>|<span data-ttu-id="48c1e-434">401</span><span class="sxs-lookup"><span data-stu-id="48c1e-434">401</span></span>|  
|<span data-ttu-id="48c1e-435">header-name</span><span class="sxs-lookup"><span data-stu-id="48c1e-435">header-name</span></span>|<span data-ttu-id="48c1e-436">nom Hello d’en-tête hello HTTP contenant hello jeton.</span><span class="sxs-lookup"><span data-stu-id="48c1e-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="48c1e-437">Soit `header-name`, soit `query-paremeter-name` doit être spécifié, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="48c1e-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="48c1e-438">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-438">N/A</span></span>|  
|<span data-ttu-id="48c1e-439">id</span><span class="sxs-lookup"><span data-stu-id="48c1e-439">id</span></span>|<span data-ttu-id="48c1e-440">Hello `id` attribut sur hello `key` élément vous permet de chaîne hello toospecify qui sera comparée à `kid` toofind de jeton (le cas échéant) hello out hello approprié toouse clés pour la validation des signatures de revendication.</span><span class="sxs-lookup"><span data-stu-id="48c1e-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="48c1e-441">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-441">No</span></span>|<span data-ttu-id="48c1e-442">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-442">N/A</span></span>|  
|<span data-ttu-id="48c1e-443">match</span><span class="sxs-lookup"><span data-stu-id="48c1e-443">match</span></span>|<span data-ttu-id="48c1e-444">Hello `match` attribut sur hello `claim` élément indique si chaque valeur de revendication dans la stratégie de hello doit être présent dans le jeton de hello pour toosucceed de validation.</span><span class="sxs-lookup"><span data-stu-id="48c1e-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="48c1e-445">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="48c1e-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="48c1e-446">-                          `all`-chaque valeur de revendication dans la stratégie de hello doit être présent dans le jeton de hello pour toosucceed de validation.</span><span class="sxs-lookup"><span data-stu-id="48c1e-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="48c1e-447">-                          `any`-valeur d’au moins une revendication doit être présent dans le jeton de hello pour toosucceed de validation.</span><span class="sxs-lookup"><span data-stu-id="48c1e-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="48c1e-448">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-448">No</span></span>|<span data-ttu-id="48c1e-449">tout</span><span class="sxs-lookup"><span data-stu-id="48c1e-449">all</span></span>|  
|<span data-ttu-id="48c1e-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="48c1e-450">query-paremeter-name</span></span>|<span data-ttu-id="48c1e-451">nom Hello hello hello du paramètre de requête contenant le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="48c1e-452">Soit `header-name`, soit `query-paremeter-name` doit être spécifié, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="48c1e-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="48c1e-453">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-453">N/A</span></span>|  
|<span data-ttu-id="48c1e-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="48c1e-454">require-expiration-time</span></span>|<span data-ttu-id="48c1e-455">Booléen.</span><span class="sxs-lookup"><span data-stu-id="48c1e-455">Boolean.</span></span> <span data-ttu-id="48c1e-456">Spécifie si une revendication d’expiration est requise dans le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="48c1e-457">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-457">No</span></span>|<span data-ttu-id="48c1e-458">true</span><span class="sxs-lookup"><span data-stu-id="48c1e-458">true</span></span>|
|<span data-ttu-id="48c1e-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="48c1e-459">require-scheme</span></span>|<span data-ttu-id="48c1e-460">Hello nom du schéma de jeton hello, par exemple « Support ».</span><span class="sxs-lookup"><span data-stu-id="48c1e-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="48c1e-461">Lorsque cet attribut est défini, stratégie de hello garantit que spécifié de schéma est présent dans la valeur de l’en-tête d’autorisation de hello.</span><span class="sxs-lookup"><span data-stu-id="48c1e-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="48c1e-462">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-462">No</span></span>|<span data-ttu-id="48c1e-463">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-463">N/A</span></span>|
|<span data-ttu-id="48c1e-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="48c1e-464">require-signed-tokens</span></span>|<span data-ttu-id="48c1e-465">Booléen.</span><span class="sxs-lookup"><span data-stu-id="48c1e-465">Boolean.</span></span> <span data-ttu-id="48c1e-466">Spécifie si un jeton est requis toobe signé.</span><span class="sxs-lookup"><span data-stu-id="48c1e-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="48c1e-467">Non</span><span class="sxs-lookup"><span data-stu-id="48c1e-467">No</span></span>|<span data-ttu-id="48c1e-468">true</span><span class="sxs-lookup"><span data-stu-id="48c1e-468">true</span></span>|  
|<span data-ttu-id="48c1e-469">url</span><span class="sxs-lookup"><span data-stu-id="48c1e-469">url</span></span>|<span data-ttu-id="48c1e-470">URL du point de terminaison de configuration Open ID à partir de laquelle les métadonnées de configuration Open ID peuvent être récupérées.</span><span class="sxs-lookup"><span data-stu-id="48c1e-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="48c1e-471">Pour Azure Active Directory, utilisez hello suivant URL : `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` en remplaçant votre nom de client de répertoire, par exemple, `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="48c1e-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="48c1e-472">Oui</span><span class="sxs-lookup"><span data-stu-id="48c1e-472">Yes</span></span>|<span data-ttu-id="48c1e-473">N/A</span><span class="sxs-lookup"><span data-stu-id="48c1e-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="48c1e-474">Usage</span><span class="sxs-lookup"><span data-stu-id="48c1e-474">Usage</span></span>  
 <span data-ttu-id="48c1e-475">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="48c1e-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="48c1e-476">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="48c1e-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="48c1e-477">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="48c1e-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="48c1e-478">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48c1e-478">Next steps</span></span>
<span data-ttu-id="48c1e-479">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="48c1e-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
