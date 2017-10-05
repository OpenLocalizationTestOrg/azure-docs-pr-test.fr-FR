---
title: "Stratégies dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies disponibles dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="bcd1b-103">Stratégies API Management</span><span class="sxs-lookup"><span data-stu-id="bcd1b-103">API Management policies</span></span>
<span data-ttu-id="bcd1b-104">Cette section est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="bcd1b-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bcd1b-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="bcd1b-106">Les stratégies sont une fonctionnalité puissante du système qui permet à l’éditeur de modifier le comportement de l’API grâce à la configuration.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="bcd1b-107">Les stratégies sont un ensemble d'instructions qui sont exécutées dans l'ordre sur demande ou sur réponse d'une API.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="bcd1b-108">Les instructions les plus utilisées comprennent la conversion du format XML au format JSON et la limitation du débit d'appels pour restreindre la quantité d'appels entrants d'un développeur.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="bcd1b-109">De nombreuses autres stratégies sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="bcd1b-110">Les expressions de stratégie peuvent être utilisées comme valeurs d’attribut ou valeurs de texte dans l’une des stratégies de Gestion des API, sauf si la stratégie le spécifie autrement.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="bcd1b-111">Certaines stratégies, telles que les stratégies [Control flow](api-management-advanced-policies.md#choose) et [Set variable](api-management-advanced-policies.md#set-variable), sont basées sur des expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="bcd1b-112">Pour plus d’informations, consultez les rubriques [Stratégies avancées](api-management-advanced-policies.md#AdvancedPolicies) et [Expressions de stratégie](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="bcd1b-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="bcd1b-113"><a name="ProxyPolicies"></a> Stratégies</span><span class="sxs-lookup"><span data-stu-id="bcd1b-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="bcd1b-114">Accès aux stratégies de restriction</span><span class="sxs-lookup"><span data-stu-id="bcd1b-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="bcd1b-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) : applique l’existence et/ou la valeur d’un en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="bcd1b-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="bcd1b-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="bcd1b-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtre (autorise/rejette) les appels de certaines adresses IP spécifiques et/ou de certaines plages d’adresses.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="bcd1b-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) : vous permet d’appliquer un volume d’appel et/ou un quota de bande passante renouvelable ou illimité par abonnement.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="bcd1b-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) : vous permet d’appliquer un volume d’appel et/ou un quota de bande passante renouvelable ou illimité par clé.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="bcd1b-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="bcd1b-122">Stratégies avancées</span><span class="sxs-lookup"><span data-stu-id="bcd1b-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="bcd1b-123">[Control flow](api-management-advanced-policies.md#choose) : applique de manière conditionnelle les instructions des stratégies en fonction de l’évaluation des expressions booléennes.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="bcd1b-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) : transfère la demande vers le service principal.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="bcd1b-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) : envoie des messages au format spécifié à une cible de message définie par une entité Enregistreur.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="bcd1b-126">[Retry](api-management-advanced-policies.md#Retry) : effectue une nouvelle tentative d’exécution des instructions de stratégie incluses, si la condition est remplie et jusqu’à ce qu’elle le soit.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="bcd1b-127">L’exécution se répète à intervalles réguliers et ce jusqu’au nombre de tentatives défini.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="bcd1b-128">[Return response](api-management-advanced-policies.md#ReturnResponse) : abandonne l’exécution du pipeline et renvoie la réponse indiquée directement à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="bcd1b-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) : envoie une demande à l’URL indiquée sans attendre de réponse.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="bcd1b-130">[Send request](api-management-advanced-policies.md#SendRequest) : envoie une demande à l’URL indiquée.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="bcd1b-131">[Set variable](api-management-advanced-policies.md#set-variable) : conserve une valeur dans une variable de contexte nommée pour permettre d’y accéder ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="bcd1b-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) : permet de modifier la méthode HTTP d’une demande.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="bcd1b-133">[Set status code](api-management-advanced-policies.md#SetStatus) : permet de donner la valeur spécifiée au code d’état HTTP.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="bcd1b-134">[Trace](api-management-advanced-policies.md#Trace) : ajoute une chaîne à la sortie de l’[inspecteur d’API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="bcd1b-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="bcd1b-135">[Wait](api-management-advanced-policies.md#Wait) : attend l’exécution des stratégies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) ou [Control flow](api-management-advanced-policies.md#choose) pour continuer.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="bcd1b-136">Stratégies d’authentification</span><span class="sxs-lookup"><span data-stu-id="bcd1b-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="bcd1b-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) : authentification avec un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="bcd1b-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) : authentification avec un service principal à l’aide de certificats clients.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="bcd1b-139">Stratégies de mise en cache</span><span class="sxs-lookup"><span data-stu-id="bcd1b-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="bcd1b-140">[Get from cache](api-management-caching-policies.md#GetFromCache) : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="bcd1b-141">[Store to cache](api-management-caching-policies.md#StoreToCache) : met en cache la réponse en fonction de la configuration de contrôle de cache spécifiée.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="bcd1b-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) : récupère un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="bcd1b-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) : stocke un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="bcd1b-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) : supprime un élément du cache par clé.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="bcd1b-145">Stratégies interdomaines</span><span class="sxs-lookup"><span data-stu-id="bcd1b-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="bcd1b-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) : rend l'API accessible depuis les navigateurs clients utilisant Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="bcd1b-147">[CORS](api-management-cross-domain-policies.md#CORS) : ajoute une prise en charge partage des ressources cross-origin (CORS) à une opération ou une API afin de permettre les appels interdomaines depuis les navigateurs clients.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="bcd1b-148">[JSONP](api-management-cross-domain-policies.md#JSONP) : ajoute une prise en charge de JSON avec remplissage (JSONP) à une opération ou une API afin de permettre les appels interdomaines depuis les navigateurs clients utilisant JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="bcd1b-149">Stratégies de transformation</span><span class="sxs-lookup"><span data-stu-id="bcd1b-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="bcd1b-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) : convertit le corps de la demande ou de la réponse de JSON en XML.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="bcd1b-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) :convertit le corps de la demande ou de la réponse de XML en JSON.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="bcd1b-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="bcd1b-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) : réécrit (masque) les liens dans le corps de la réponse afin qu’ils pointent vers un lien équivalent via la passerelle.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="bcd1b-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) : modifie le service principal pour une demande entrante.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="bcd1b-155">[Set body](api-management-transformation-policies.md#SetBody) : définit le corps du message pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="bcd1b-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) : affecte une valeur à un en-tête de réponse et/ou de demande existant ou bien ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="bcd1b-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="bcd1b-158">[URL de réécriture](api-management-transformation-policies.md#RewriteURL) : convertit une URL de demande de sa forme publique en une forme attendue par le service web.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="bcd1b-159">[Transformer du code XML à l’aide d’une transformation XSLT](api-management-transformation-policies.md#XSLTransform) : applique une transformation de XSL en XML dans le corps de la réponse ou de la demande.</span><span class="sxs-lookup"><span data-stu-id="bcd1b-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bcd1b-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcd1b-160">Next steps</span></span>
<span data-ttu-id="bcd1b-161">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bcd1b-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
