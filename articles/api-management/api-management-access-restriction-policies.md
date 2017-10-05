---
title: "Stratégies de restriction des accès de la Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies de restriction des accès disponibles dans la Gestion des API Azure."
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="12ec9-103">Stratégies de restriction des accès de la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="12ec9-103">API Management access restriction policies</span></span>
<span data-ttu-id="12ec9-104">Cette rubrique est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="12ec9-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="12ec9-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="12ec9-106"><a name="AccessRestrictionPolicies"></a> Stratégies de restriction des accès</span><span class="sxs-lookup"><span data-stu-id="12ec9-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="12ec9-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) : applique l’existence et/ou la valeur d’un en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="12ec9-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="12ec9-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.</span><span class="sxs-lookup"><span data-stu-id="12ec9-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="12ec9-109">[Limit call rate by key](#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="12ec9-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtre (autorise/rejette) les appels de certaines adresses IP spécifiques et/ou de certaines plages d’adresses.</span><span class="sxs-lookup"><span data-stu-id="12ec9-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="12ec9-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) : vous permet d’appliquer un volume d’appel et/ou un quota de bande passante renouvelable ou illimité par abonnement.</span><span class="sxs-lookup"><span data-stu-id="12ec9-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="12ec9-112">[Set usage quota by key](#SetUsageQuotaByKey) : vous permet d’appliquer un volume d’appel et/ou un quota de bande passante renouvelable ou illimité par clé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="12ec9-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="12ec9-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="12ec9-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span><span class="sxs-lookup"><span data-stu-id="12ec9-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="12ec9-115">Utilisez la stratégie `check-header` pour imposer un en-tête HTTP donné à une demande.</span><span class="sxs-lookup"><span data-stu-id="12ec9-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="12ec9-116">Vous pouvez éventuellement vérifier si l’en-tête a une certaine valeur ou une valeur comprise dans une plage de valeurs autorisées.</span><span class="sxs-lookup"><span data-stu-id="12ec9-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="12ec9-117">Si la vérification échoue, la stratégie met fin au traitement de la demande et renvoie le message d’erreur et le code d’état HTTP spécifiés par la stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-118">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="12ec9-119">Exemple</span><span class="sxs-lookup"><span data-stu-id="12ec9-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="12ec9-120">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-120">Elements</span></span>  
  
|<span data-ttu-id="12ec9-121">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-121">Name</span></span>|<span data-ttu-id="12ec9-122">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-122">Description</span></span>|<span data-ttu-id="12ec9-123">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="12ec9-124">check-header</span><span class="sxs-lookup"><span data-stu-id="12ec9-124">check-header</span></span>|<span data-ttu-id="12ec9-125">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-125">Root element.</span></span>|<span data-ttu-id="12ec9-126">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-126">Yes</span></span>|  
|<span data-ttu-id="12ec9-127">value</span><span class="sxs-lookup"><span data-stu-id="12ec9-127">value</span></span>|<span data-ttu-id="12ec9-128">Valeur autorisée de l’en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="12ec9-128">Allowed HTTP header value.</span></span> <span data-ttu-id="12ec9-129">Lorsque plusieurs éléments de valeurs sont spécifiés, la vérification est considérée comme réussie si l’une des valeurs correspond.</span><span class="sxs-lookup"><span data-stu-id="12ec9-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="12ec9-130">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-131">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-131">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-132">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-132">Name</span></span>|<span data-ttu-id="12ec9-133">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-133">Description</span></span>|<span data-ttu-id="12ec9-134">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-134">Required</span></span>|<span data-ttu-id="12ec9-135">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="12ec9-136">failed-check-error-message</span></span>|<span data-ttu-id="12ec9-137">Message d’erreur à renvoyer dans le corps de la réponse HTTP si l’en-tête n’existe pas ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="12ec9-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="12ec9-138">Les éventuels caractères spéciaux de ce message doivent être correctement placés dans une séquence d’échappement.</span><span class="sxs-lookup"><span data-stu-id="12ec9-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="12ec9-139">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-139">Yes</span></span>|<span data-ttu-id="12ec9-140">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-140">N/A</span></span>|  
|<span data-ttu-id="12ec9-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="12ec9-141">failed-check-httpcode</span></span>|<span data-ttu-id="12ec9-142">Code d’état HTTP à renvoyer si l’en-tête n’existe pas ou a une valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="12ec9-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="12ec9-143">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-143">Yes</span></span>|<span data-ttu-id="12ec9-144">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-144">N/A</span></span>|  
|<span data-ttu-id="12ec9-145">header-name</span><span class="sxs-lookup"><span data-stu-id="12ec9-145">header-name</span></span>|<span data-ttu-id="12ec9-146">Nom de l’en-tête HTTP à vérifier.</span><span class="sxs-lookup"><span data-stu-id="12ec9-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="12ec9-147">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-147">Yes</span></span>|<span data-ttu-id="12ec9-148">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-148">N/A</span></span>|  
|<span data-ttu-id="12ec9-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="12ec9-149">ignore-case</span></span>|<span data-ttu-id="12ec9-150">Peut avoir la valeur True ou False.</span><span class="sxs-lookup"><span data-stu-id="12ec9-150">Can be set to True or False.</span></span> <span data-ttu-id="12ec9-151">S’il a la valeur True, la casse est ignorée lors de la comparaison de la valeur de l’en-tête à l’ensemble des valeurs acceptables.</span><span class="sxs-lookup"><span data-stu-id="12ec9-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="12ec9-152">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-152">Yes</span></span>|<span data-ttu-id="12ec9-153">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-154">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-154">Usage</span></span>  
 <span data-ttu-id="12ec9-155">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-156">**Sections de la stratégie :** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="12ec9-157">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="12ec9-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span><span class="sxs-lookup"><span data-stu-id="12ec9-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="12ec9-159">La stratégie `rate-limit` évite les pics d’utilisation des API par abonnement en limitant le débit d’appels à un nombre spécifié pour une période donnée.</span><span class="sxs-lookup"><span data-stu-id="12ec9-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="12ec9-160">Lorsque cette stratégie est déclenchée, l’appelant reçoit le code d’état de réponse `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="12ec9-161">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="12ec9-162">Les [expressions de stratégie](api-management-policy-expressions.md) ne peuvent être utilisées dans aucun attribut de cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-163">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="12ec9-164">Exemple</span><span class="sxs-lookup"><span data-stu-id="12ec9-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="12ec9-165">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-165">Elements</span></span>  
  
|<span data-ttu-id="12ec9-166">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-166">Name</span></span>|<span data-ttu-id="12ec9-167">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-167">Description</span></span>|<span data-ttu-id="12ec9-168">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="12ec9-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="12ec9-169">set-limit</span></span>|<span data-ttu-id="12ec9-170">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-170">Root element.</span></span>|<span data-ttu-id="12ec9-171">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-171">Yes</span></span>|  
|<span data-ttu-id="12ec9-172">api</span><span class="sxs-lookup"><span data-stu-id="12ec9-172">api</span></span>|<span data-ttu-id="12ec9-173">Ajoutez un ou plusieurs éléments de ce type pour imposer une limite de débit d’appels aux API au sein du produit.</span><span class="sxs-lookup"><span data-stu-id="12ec9-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="12ec9-174">Les limites de débit d’appels au niveau du produit et de l’API s’appliquent indépendamment les unes des autres.</span><span class="sxs-lookup"><span data-stu-id="12ec9-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="12ec9-175">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-175">No</span></span>|  
|<span data-ttu-id="12ec9-176">operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-176">operation</span></span>|<span data-ttu-id="12ec9-177">Ajoutez un ou plusieurs éléments de ce type pour imposer une limite de débit d’appels aux opérations au sein d’une API.</span><span class="sxs-lookup"><span data-stu-id="12ec9-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="12ec9-178">Les limites de débit d’appels au niveau du produit, de l’API et de l’opération s’appliquent indépendamment les unes des autres.</span><span class="sxs-lookup"><span data-stu-id="12ec9-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="12ec9-179">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-180">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-180">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-181">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-181">Name</span></span>|<span data-ttu-id="12ec9-182">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-182">Description</span></span>|<span data-ttu-id="12ec9-183">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-183">Required</span></span>|<span data-ttu-id="12ec9-184">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-185">name</span><span class="sxs-lookup"><span data-stu-id="12ec9-185">name</span></span>|<span data-ttu-id="12ec9-186">Nom de l’API à laquelle la limite de débit s’applique.</span><span class="sxs-lookup"><span data-stu-id="12ec9-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="12ec9-187">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-187">Yes</span></span>|<span data-ttu-id="12ec9-188">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-188">N/A</span></span>|  
|<span data-ttu-id="12ec9-189">calls</span><span class="sxs-lookup"><span data-stu-id="12ec9-189">calls</span></span>|<span data-ttu-id="12ec9-190">Nombre maximal d’appels autorisés au cours de l’intervalle de temps spécifié dans le paramètre `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="12ec9-191">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-191">Yes</span></span>|<span data-ttu-id="12ec9-192">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-192">N/A</span></span>|  
|<span data-ttu-id="12ec9-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="12ec9-193">renewal-period</span></span>|<span data-ttu-id="12ec9-194">Période en secondes après laquelle le quota se réinitialise.</span><span class="sxs-lookup"><span data-stu-id="12ec9-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="12ec9-195">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-195">Yes</span></span>|<span data-ttu-id="12ec9-196">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-197">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-197">Usage</span></span>  
 <span data-ttu-id="12ec9-198">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-199">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="12ec9-200">**Étendues de la stratégie :** product</span><span class="sxs-lookup"><span data-stu-id="12ec9-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="12ec9-201"><a name="LimitCallRateByKey"></a> Limite de débit d’appels par clé</span><span class="sxs-lookup"><span data-stu-id="12ec9-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="12ec9-202">La stratégie `rate-limit-by-key` évite les pics d’utilisation des API par clé en limitant le débit d’appels à un nombre spécifié pour une période donnée.</span><span class="sxs-lookup"><span data-stu-id="12ec9-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="12ec9-203">La clé peut avoir une valeur de chaîne arbitraire ; elle est généralement fournie par le biais d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="12ec9-204">Une condition d’incrément facultative peut être ajoutée pour spécifier quelles demandes doivent être comptées dans la limite.</span><span class="sxs-lookup"><span data-stu-id="12ec9-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="12ec9-205">Lorsque cette stratégie est déclenchée, l’appelant reçoit le code d’état de réponse `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="12ec9-206">Pour plus d’informations et d’exemples sur cette stratégie, consultez la page [Limitation avancée des demandes dans la Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="12ec9-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="12ec9-207">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-208">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="12ec9-209">Exemple</span><span class="sxs-lookup"><span data-stu-id="12ec9-209">Example</span></span>  
 <span data-ttu-id="12ec9-210">Dans l’exemple suivant, la limite de débit est indexée par l’adresse IP de l’appelant.</span><span class="sxs-lookup"><span data-stu-id="12ec9-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="12ec9-211">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-211">Elements</span></span>  
  
|<span data-ttu-id="12ec9-212">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-212">Name</span></span>|<span data-ttu-id="12ec9-213">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-213">Description</span></span>|<span data-ttu-id="12ec9-214">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="12ec9-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="12ec9-215">set-limit</span></span>|<span data-ttu-id="12ec9-216">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-216">Root element.</span></span>|<span data-ttu-id="12ec9-217">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-218">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-218">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-219">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-219">Name</span></span>|<span data-ttu-id="12ec9-220">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-220">Description</span></span>|<span data-ttu-id="12ec9-221">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-221">Required</span></span>|<span data-ttu-id="12ec9-222">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-223">calls</span><span class="sxs-lookup"><span data-stu-id="12ec9-223">calls</span></span>|<span data-ttu-id="12ec9-224">Nombre maximal d’appels autorisés au cours de l’intervalle de temps spécifié dans le paramètre `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="12ec9-225">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-225">Yes</span></span>|<span data-ttu-id="12ec9-226">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-226">N/A</span></span>|  
|<span data-ttu-id="12ec9-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="12ec9-227">counter-key</span></span>|<span data-ttu-id="12ec9-228">Clé à utiliser pour la stratégie de limite de débit.</span><span class="sxs-lookup"><span data-stu-id="12ec9-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="12ec9-229">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-229">Yes</span></span>|<span data-ttu-id="12ec9-230">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-230">N/A</span></span>|  
|<span data-ttu-id="12ec9-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="12ec9-231">increment-condition</span></span>|<span data-ttu-id="12ec9-232">Expression booléenne spécifiant si la demande doit être comptée dans le quota (`true`).</span><span class="sxs-lookup"><span data-stu-id="12ec9-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="12ec9-233">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-233">No</span></span>|<span data-ttu-id="12ec9-234">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-234">N/A</span></span>|  
|<span data-ttu-id="12ec9-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="12ec9-235">renewal-period</span></span>|<span data-ttu-id="12ec9-236">Période en secondes après laquelle le quota se réinitialise.</span><span class="sxs-lookup"><span data-stu-id="12ec9-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="12ec9-237">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-237">Yes</span></span>|<span data-ttu-id="12ec9-238">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-239">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-239">Usage</span></span>  
 <span data-ttu-id="12ec9-240">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-241">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="12ec9-242">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="12ec9-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span><span class="sxs-lookup"><span data-stu-id="12ec9-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="12ec9-244">La stratégie `ip-filter` filtre (autorise/rejette) les appels de certaines adresses IP et/ou de certaines plages d’adresses.</span><span class="sxs-lookup"><span data-stu-id="12ec9-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-245">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="12ec9-246">Exemple</span><span class="sxs-lookup"><span data-stu-id="12ec9-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="12ec9-247">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-247">Elements</span></span>  
  
|<span data-ttu-id="12ec9-248">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-248">Name</span></span>|<span data-ttu-id="12ec9-249">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-249">Description</span></span>|<span data-ttu-id="12ec9-250">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="12ec9-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="12ec9-251">ip-filter</span></span>|<span data-ttu-id="12ec9-252">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-252">Root element.</span></span>|<span data-ttu-id="12ec9-253">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-253">Yes</span></span>|  
|<span data-ttu-id="12ec9-254">address</span><span class="sxs-lookup"><span data-stu-id="12ec9-254">address</span></span>|<span data-ttu-id="12ec9-255">Spécifie une adresse IP unique à filtrer.</span><span class="sxs-lookup"><span data-stu-id="12ec9-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="12ec9-256">Au moins un élément `address` ou `address-range` est requis.</span><span class="sxs-lookup"><span data-stu-id="12ec9-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="12ec9-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="12ec9-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="12ec9-258">Spécifie une plage d’adresses IP à filtrer.</span><span class="sxs-lookup"><span data-stu-id="12ec9-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="12ec9-259">Au moins un élément `address` ou `address-range` est requis.</span><span class="sxs-lookup"><span data-stu-id="12ec9-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-260">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-260">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-261">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-261">Name</span></span>|<span data-ttu-id="12ec9-262">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-262">Description</span></span>|<span data-ttu-id="12ec9-263">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-263">Required</span></span>|<span data-ttu-id="12ec9-264">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="12ec9-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="12ec9-266">Plage d'adresses IP pour lesquelles autoriser ou refuser l'accès.</span><span class="sxs-lookup"><span data-stu-id="12ec9-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="12ec9-267">Obligatoire lorsque l’élément `address-range` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="12ec9-268">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-268">N/A</span></span>|  
|<span data-ttu-id="12ec9-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="12ec9-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="12ec9-270">Spécifie si les appels doivent être autorisés ou non pour les adresses IP et plages spécifiées.</span><span class="sxs-lookup"><span data-stu-id="12ec9-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="12ec9-271">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-271">Yes</span></span>|<span data-ttu-id="12ec9-272">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-273">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-273">Usage</span></span>  
 <span data-ttu-id="12ec9-274">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-275">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="12ec9-276">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="12ec9-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span><span class="sxs-lookup"><span data-stu-id="12ec9-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="12ec9-278">La stratégie `quota` applique un volume d’appels et/ou un quota de bande passante renouvelable ou illimité par abonnement.</span><span class="sxs-lookup"><span data-stu-id="12ec9-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="12ec9-279">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="12ec9-280">Les [expressions de stratégie](api-management-policy-expressions.md) ne peuvent être utilisées dans aucun attribut de cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-281">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="12ec9-282">Exemple</span><span class="sxs-lookup"><span data-stu-id="12ec9-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="12ec9-283">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-283">Elements</span></span>  
  
|<span data-ttu-id="12ec9-284">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-284">Name</span></span>|<span data-ttu-id="12ec9-285">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-285">Description</span></span>|<span data-ttu-id="12ec9-286">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="12ec9-287">quota</span><span class="sxs-lookup"><span data-stu-id="12ec9-287">quota</span></span>|<span data-ttu-id="12ec9-288">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-288">Root element.</span></span>|<span data-ttu-id="12ec9-289">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-289">Yes</span></span>|  
|<span data-ttu-id="12ec9-290">api</span><span class="sxs-lookup"><span data-stu-id="12ec9-290">api</span></span>|<span data-ttu-id="12ec9-291">Ajoutez un ou plusieurs éléments de ce type pour imposer un quota aux API au sein du produit.</span><span class="sxs-lookup"><span data-stu-id="12ec9-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="12ec9-292">Les quotas au niveau du produit et de l’API s’appliquent indépendamment les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="12ec9-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="12ec9-293">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-293">No</span></span>|  
|<span data-ttu-id="12ec9-294">operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-294">operation</span></span>|<span data-ttu-id="12ec9-295">Ajoutez un ou plusieurs éléments de ce type pour imposer un quota aux opérations au sein d’une API.</span><span class="sxs-lookup"><span data-stu-id="12ec9-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="12ec9-296">Les quotas au niveau du produit, de l’API et de l’opération s’appliquent indépendamment les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="12ec9-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="12ec9-297">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-298">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-298">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-299">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-299">Name</span></span>|<span data-ttu-id="12ec9-300">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-300">Description</span></span>|<span data-ttu-id="12ec9-301">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-301">Required</span></span>|<span data-ttu-id="12ec9-302">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-303">name</span><span class="sxs-lookup"><span data-stu-id="12ec9-303">name</span></span>|<span data-ttu-id="12ec9-304">Nom de l’API ou de l’opération à laquelle s’applique le quota.</span><span class="sxs-lookup"><span data-stu-id="12ec9-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="12ec9-305">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-305">Yes</span></span>|<span data-ttu-id="12ec9-306">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-306">N/A</span></span>|  
|<span data-ttu-id="12ec9-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="12ec9-307">bandwidth</span></span>|<span data-ttu-id="12ec9-308">Nombre maximal de kilo-octets autorisés au cours de l’intervalle de temps spécifié dans le paramètre `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="12ec9-309">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="12ec9-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="12ec9-310">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-310">N/A</span></span>|  
|<span data-ttu-id="12ec9-311">calls</span><span class="sxs-lookup"><span data-stu-id="12ec9-311">calls</span></span>|<span data-ttu-id="12ec9-312">Nombre maximal d’appels autorisés au cours de l’intervalle de temps spécifié dans le paramètre `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="12ec9-313">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="12ec9-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="12ec9-314">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-314">N/A</span></span>|  
|<span data-ttu-id="12ec9-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="12ec9-315">renewal-period</span></span>|<span data-ttu-id="12ec9-316">Période en secondes après laquelle le quota se réinitialise.</span><span class="sxs-lookup"><span data-stu-id="12ec9-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="12ec9-317">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-317">Yes</span></span>|<span data-ttu-id="12ec9-318">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-319">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-319">Usage</span></span>  
 <span data-ttu-id="12ec9-320">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-321">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="12ec9-322">**Étendues de la stratégie :** product</span><span class="sxs-lookup"><span data-stu-id="12ec9-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="12ec9-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span><span class="sxs-lookup"><span data-stu-id="12ec9-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="12ec9-324">La stratégie `quota-by-key` applique un volume d’appels et/ou un quota de bande passante renouvelable ou illimité par clé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="12ec9-325">La clé peut avoir une valeur de chaîne arbitraire ; elle est généralement fournie par le biais d’une expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="12ec9-326">Une condition d’incrément facultative peut être ajoutée pour spécifier quelles demandes doivent être comptées dans le quota.</span><span class="sxs-lookup"><span data-stu-id="12ec9-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="12ec9-327">Pour plus d’informations et d’exemples sur cette stratégie, consultez la page [Limitation avancée des demandes dans la Gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="12ec9-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="12ec9-328">Cette stratégie ne peut être utilisée qu’une seule fois par document de stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="12ec9-329">Les [expressions de stratégie](api-management-policy-expressions.md) ne peuvent être utilisées dans aucun attribut de cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="12ec9-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-330">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="12ec9-331">Exemple</span><span class="sxs-lookup"><span data-stu-id="12ec9-331">Example</span></span>  
 <span data-ttu-id="12ec9-332">Dans l’exemple suivant, le quota est indexé par l’adresse IP de l’appelant.</span><span class="sxs-lookup"><span data-stu-id="12ec9-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="12ec9-333">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-333">Elements</span></span>  
  
|<span data-ttu-id="12ec9-334">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-334">Name</span></span>|<span data-ttu-id="12ec9-335">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-335">Description</span></span>|<span data-ttu-id="12ec9-336">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="12ec9-337">quota</span><span class="sxs-lookup"><span data-stu-id="12ec9-337">quota</span></span>|<span data-ttu-id="12ec9-338">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-338">Root element.</span></span>|<span data-ttu-id="12ec9-339">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-340">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-340">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-341">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-341">Name</span></span>|<span data-ttu-id="12ec9-342">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-342">Description</span></span>|<span data-ttu-id="12ec9-343">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-343">Required</span></span>|<span data-ttu-id="12ec9-344">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="12ec9-345">bandwidth</span></span>|<span data-ttu-id="12ec9-346">Nombre maximal de kilo-octets autorisés au cours de l’intervalle de temps spécifié dans le paramètre `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="12ec9-347">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="12ec9-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="12ec9-348">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-348">N/A</span></span>|  
|<span data-ttu-id="12ec9-349">calls</span><span class="sxs-lookup"><span data-stu-id="12ec9-349">calls</span></span>|<span data-ttu-id="12ec9-350">Nombre maximal d’appels autorisés au cours de l’intervalle de temps spécifié dans le paramètre `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="12ec9-351">Il est obligatoire de spécifier `calls`, `bandwidth` ou les deux.</span><span class="sxs-lookup"><span data-stu-id="12ec9-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="12ec9-352">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-352">N/A</span></span>|  
|<span data-ttu-id="12ec9-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="12ec9-353">counter-key</span></span>|<span data-ttu-id="12ec9-354">Clé à utiliser pour la stratégie de quota.</span><span class="sxs-lookup"><span data-stu-id="12ec9-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="12ec9-355">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-355">Yes</span></span>|<span data-ttu-id="12ec9-356">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-356">N/A</span></span>|  
|<span data-ttu-id="12ec9-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="12ec9-357">increment-condition</span></span>|<span data-ttu-id="12ec9-358">Expression booléenne spécifiant si la demande doit être comptée dans le quota (`true`).</span><span class="sxs-lookup"><span data-stu-id="12ec9-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="12ec9-359">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-359">No</span></span>|<span data-ttu-id="12ec9-360">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-360">N/A</span></span>|  
|<span data-ttu-id="12ec9-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="12ec9-361">renewal-period</span></span>|<span data-ttu-id="12ec9-362">Période en secondes après laquelle le quota se réinitialise.</span><span class="sxs-lookup"><span data-stu-id="12ec9-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="12ec9-363">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-363">Yes</span></span>|<span data-ttu-id="12ec9-364">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-365">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-365">Usage</span></span>  
 <span data-ttu-id="12ec9-366">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-367">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="12ec9-368">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="12ec9-369"><a name="ValidateJWT"></a> Validate JWT</span><span class="sxs-lookup"><span data-stu-id="12ec9-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="12ec9-370">La stratégie `validate-jwt` applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="12ec9-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="12ec9-371">La stratégie `validate-jwt` exige que la revendication inscrite `exp` soit incluse dans le jeton JWT, sauf si l’attribut `require-expiration-time` est spécifié et a la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="12ec9-372">La stratégie `validate-jwt` prend en charge les algorithmes de signature HS256 et RS256.</span><span class="sxs-lookup"><span data-stu-id="12ec9-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="12ec9-373">Pour HS256, la clé doit être fournie en ligne au sein de la stratégie au format encodé en base 64.</span><span class="sxs-lookup"><span data-stu-id="12ec9-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="12ec9-374">Pour RS256, la clé doit être fournie par le biais d’un point de terminaison de configuration Open ID.</span><span class="sxs-lookup"><span data-stu-id="12ec9-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="12ec9-375">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="12ec9-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="12ec9-376">Exemples</span><span class="sxs-lookup"><span data-stu-id="12ec9-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="12ec9-377">Validation d’un jeton Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="12ec9-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="12ec9-378">Validation d’un jeton Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12ec9-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="12ec9-379">Validation d’un jeton Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="12ec9-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="12ec9-380">Autoriser l’accès aux opérations à partir de revendications de jetons</span><span class="sxs-lookup"><span data-stu-id="12ec9-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="12ec9-381">Cet exemple montre comment utiliser la stratégie [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) pour préautoriser l’accès aux opérations à partir de revendications de jetons.</span><span class="sxs-lookup"><span data-stu-id="12ec9-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="12ec9-382">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez la page [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, épisode 177 : Plus de fonctionnalités de la Gestion des API avec Vlad Vinogradsky) et rendez-vous directement à 13 min 50 s.</span><span class="sxs-lookup"><span data-stu-id="12ec9-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="12ec9-383">Rendez-vous directement à 15’00’’ pour afficher les stratégies configurées dans l’éditeur de stratégies, puis à 18’50’’ pour une démonstration de l’appel d’une opération à partir du portail des développeurs avec et sans le jeton d’autorisation requis.</span><span class="sxs-lookup"><span data-stu-id="12ec9-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="12ec9-384">Éléments</span><span class="sxs-lookup"><span data-stu-id="12ec9-384">Elements</span></span>  
  
|<span data-ttu-id="12ec9-385">Élément</span><span class="sxs-lookup"><span data-stu-id="12ec9-385">Element</span></span>|<span data-ttu-id="12ec9-386">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-386">Description</span></span>|<span data-ttu-id="12ec9-387">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="12ec9-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="12ec9-388">validate-jwt</span></span>|<span data-ttu-id="12ec9-389">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="12ec9-389">Root element.</span></span>|<span data-ttu-id="12ec9-390">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-390">Yes</span></span>|  
|<span data-ttu-id="12ec9-391">audiences</span><span class="sxs-lookup"><span data-stu-id="12ec9-391">audiences</span></span>|<span data-ttu-id="12ec9-392">Contient la liste des revendications d’audience acceptables qui peuvent être présentes sur le jeton.</span><span class="sxs-lookup"><span data-stu-id="12ec9-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="12ec9-393">Si plusieurs valeurs d’audience sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="12ec9-394">Au moins une audience doit être spécifiée.</span><span class="sxs-lookup"><span data-stu-id="12ec9-394">At least one audience must be specified.</span></span>|<span data-ttu-id="12ec9-395">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-395">No</span></span>|  
|<span data-ttu-id="12ec9-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="12ec9-396">issuer-signing-keys</span></span>|<span data-ttu-id="12ec9-397">Liste de clés de sécurité encodées en base 64 utilisé pour valider les jetons signés.</span><span class="sxs-lookup"><span data-stu-id="12ec9-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="12ec9-398">Si plusieurs clés de sécurité sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse (utile pour la substitution de jeton).</span><span class="sxs-lookup"><span data-stu-id="12ec9-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="12ec9-399">Les éléments clés ont un attribut `id` facultatif utilisé pour comparer à la revendication `kid`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="12ec9-400">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-400">No</span></span>|  
|<span data-ttu-id="12ec9-401">issuers</span><span class="sxs-lookup"><span data-stu-id="12ec9-401">issuers</span></span>|<span data-ttu-id="12ec9-402">Liste des services principaux acceptables qui ont émis le jeton.</span><span class="sxs-lookup"><span data-stu-id="12ec9-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="12ec9-403">Si plusieurs valeurs d’émetteur sont présentes, chacune est tentée jusqu’à ce que toutes soient épuisées (auquel cas la validation échoue) ou que l’une d’elles réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="12ec9-404">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-404">No</span></span>|  
|<span data-ttu-id="12ec9-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="12ec9-405">openid-config</span></span>|<span data-ttu-id="12ec9-406">Élément utilisé pour spécifier un point de terminaison de configuration Open ID conforme à partir duquel l’émetteur et les clés de signature peuvent être obtenus.</span><span class="sxs-lookup"><span data-stu-id="12ec9-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="12ec9-407">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-407">No</span></span>|  
|<span data-ttu-id="12ec9-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="12ec9-408">required-claims</span></span>|<span data-ttu-id="12ec9-409">Contient une liste de revendications censées être présentes sur le jeton pour qu’il soit considéré comme valide.</span><span class="sxs-lookup"><span data-stu-id="12ec9-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="12ec9-410">Si l’attribut `match` a la valeur `all`, toutes les valeurs de revendication de la stratégie doivent être présentes dans le jeton pour que la validation réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="12ec9-411">Si l’attribut `match` a la valeur `any`, au moins une revendication doit être présente dans le jeton pour que la validation réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="12ec9-412">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-412">No</span></span>|  
|<span data-ttu-id="12ec9-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="12ec9-413">zumo-master-key</span></span>|<span data-ttu-id="12ec9-414">Clé principale pour les jetons émis par Azure Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="12ec9-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="12ec9-415">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="12ec9-416">Attributs</span><span class="sxs-lookup"><span data-stu-id="12ec9-416">Attributes</span></span>  
  
|<span data-ttu-id="12ec9-417">Nom</span><span class="sxs-lookup"><span data-stu-id="12ec9-417">Name</span></span>|<span data-ttu-id="12ec9-418">Description</span><span class="sxs-lookup"><span data-stu-id="12ec9-418">Description</span></span>|<span data-ttu-id="12ec9-419">Requis</span><span class="sxs-lookup"><span data-stu-id="12ec9-419">Required</span></span>|<span data-ttu-id="12ec9-420">Default</span><span class="sxs-lookup"><span data-stu-id="12ec9-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="12ec9-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="12ec9-421">clock-skew</span></span>|<span data-ttu-id="12ec9-422">Intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="12ec9-422">Timespan.</span></span> <span data-ttu-id="12ec9-423">Permet une petite marge de manœuvre au cas où la revendication d’expiration du jeton serait présente dans le jeton et serait postérieure à la date / heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="12ec9-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="12ec9-424">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-424">No</span></span>|<span data-ttu-id="12ec9-425">0 seconde</span><span class="sxs-lookup"><span data-stu-id="12ec9-425">0 seconds</span></span>|  
|<span data-ttu-id="12ec9-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="12ec9-426">failed-validation-error-message</span></span>|<span data-ttu-id="12ec9-427">Message d’erreur à renvoyer dans le corps de la réponse HTTP si le JWT n’est pas validé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="12ec9-428">Les éventuels caractères spéciaux de ce message doivent être correctement placés dans une séquence d’échappement.</span><span class="sxs-lookup"><span data-stu-id="12ec9-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="12ec9-429">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-429">No</span></span>|<span data-ttu-id="12ec9-430">Le message d’erreur par défaut dépend du problème de validation, par exemple « JWT absent ».</span><span class="sxs-lookup"><span data-stu-id="12ec9-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="12ec9-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="12ec9-431">failed-validation-httpcode</span></span>|<span data-ttu-id="12ec9-432">Code d’état HTTP à renvoyer si le JWT n’est pas validé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="12ec9-433">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-433">No</span></span>|<span data-ttu-id="12ec9-434">401</span><span class="sxs-lookup"><span data-stu-id="12ec9-434">401</span></span>|  
|<span data-ttu-id="12ec9-435">header-name</span><span class="sxs-lookup"><span data-stu-id="12ec9-435">header-name</span></span>|<span data-ttu-id="12ec9-436">Nom de l’en-tête HTTP contenant le jeton.</span><span class="sxs-lookup"><span data-stu-id="12ec9-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="12ec9-437">Soit `header-name`, soit `query-paremeter-name` doit être spécifié, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="12ec9-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="12ec9-438">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-438">N/A</span></span>|  
|<span data-ttu-id="12ec9-439">id</span><span class="sxs-lookup"><span data-stu-id="12ec9-439">id</span></span>|<span data-ttu-id="12ec9-440">L’attribut `id` sur l’élément `key` vous permet de spécifier la chaîne qui sera comparée à la revendication `kid` dans le jeton (le cas échéant) pour déterminer la clé appropriée à utiliser pour la validation de la signature.</span><span class="sxs-lookup"><span data-stu-id="12ec9-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="12ec9-441">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-441">No</span></span>|<span data-ttu-id="12ec9-442">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-442">N/A</span></span>|  
|<span data-ttu-id="12ec9-443">match</span><span class="sxs-lookup"><span data-stu-id="12ec9-443">match</span></span>|<span data-ttu-id="12ec9-444">L’attribut `match` sur l’élément `claim` spécifie si toutes les valeurs de revendication de la stratégie doivent être présentes dans le jeton pour que la validation réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="12ec9-445">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="12ec9-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="12ec9-446">-                          `all` : toutes les valeurs de revendication de la stratégie doivent être présentes dans le jeton pour que la validation réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="12ec9-447">-                          `any` : au moins une valeur de revendication doit être présente dans le jeton pour que la validation réussisse.</span><span class="sxs-lookup"><span data-stu-id="12ec9-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="12ec9-448">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-448">No</span></span>|<span data-ttu-id="12ec9-449">tout</span><span class="sxs-lookup"><span data-stu-id="12ec9-449">all</span></span>|  
|<span data-ttu-id="12ec9-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="12ec9-450">query-paremeter-name</span></span>|<span data-ttu-id="12ec9-451">Nom du paramètre de la requête contenant le jeton.</span><span class="sxs-lookup"><span data-stu-id="12ec9-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="12ec9-452">Soit `header-name`, soit `query-paremeter-name` doit être spécifié, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="12ec9-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="12ec9-453">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-453">N/A</span></span>|  
|<span data-ttu-id="12ec9-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="12ec9-454">require-expiration-time</span></span>|<span data-ttu-id="12ec9-455">Booléen.</span><span class="sxs-lookup"><span data-stu-id="12ec9-455">Boolean.</span></span> <span data-ttu-id="12ec9-456">Spécifie si une revendication d’expiration est requise dans le jeton.</span><span class="sxs-lookup"><span data-stu-id="12ec9-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="12ec9-457">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-457">No</span></span>|<span data-ttu-id="12ec9-458">true</span><span class="sxs-lookup"><span data-stu-id="12ec9-458">true</span></span>|
|<span data-ttu-id="12ec9-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="12ec9-459">require-scheme</span></span>|<span data-ttu-id="12ec9-460">Le nom du schéma de jeton, par ex. « Support ».</span><span class="sxs-lookup"><span data-stu-id="12ec9-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="12ec9-461">Lorsque cet attribut est défini, la stratégie garantit que le schéma spécifié est présent dans la valeur d’en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="12ec9-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="12ec9-462">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-462">No</span></span>|<span data-ttu-id="12ec9-463">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-463">N/A</span></span>|
|<span data-ttu-id="12ec9-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="12ec9-464">require-signed-tokens</span></span>|<span data-ttu-id="12ec9-465">Booléen.</span><span class="sxs-lookup"><span data-stu-id="12ec9-465">Boolean.</span></span> <span data-ttu-id="12ec9-466">Spécifie si un jeton doit être signé.</span><span class="sxs-lookup"><span data-stu-id="12ec9-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="12ec9-467">Non</span><span class="sxs-lookup"><span data-stu-id="12ec9-467">No</span></span>|<span data-ttu-id="12ec9-468">true</span><span class="sxs-lookup"><span data-stu-id="12ec9-468">true</span></span>|  
|<span data-ttu-id="12ec9-469">url</span><span class="sxs-lookup"><span data-stu-id="12ec9-469">url</span></span>|<span data-ttu-id="12ec9-470">URL du point de terminaison de configuration Open ID à partir de laquelle les métadonnées de configuration Open ID peuvent être récupérées.</span><span class="sxs-lookup"><span data-stu-id="12ec9-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="12ec9-471">Pour Azure Active Directory, utilisez l’URL suivante : `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration`, en remplaçant par le nom de votre client d’annuaire, par exemple, `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="12ec9-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="12ec9-472">Oui</span><span class="sxs-lookup"><span data-stu-id="12ec9-472">Yes</span></span>|<span data-ttu-id="12ec9-473">N/A</span><span class="sxs-lookup"><span data-stu-id="12ec9-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="12ec9-474">Usage</span><span class="sxs-lookup"><span data-stu-id="12ec9-474">Usage</span></span>  
 <span data-ttu-id="12ec9-475">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="12ec9-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="12ec9-476">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="12ec9-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="12ec9-477">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="12ec9-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="12ec9-478">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12ec9-478">Next steps</span></span>
<span data-ttu-id="12ec9-479">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="12ec9-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
