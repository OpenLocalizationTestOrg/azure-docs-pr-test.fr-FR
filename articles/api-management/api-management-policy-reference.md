---
title: "Référence sur les stratégies Gestion des API Azure"
description: "Découvrez les stratégies disponibles pour configurer Gestion des API."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: adc0c4415e10ddd0b4994cecef17f026546e91a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="37698-103">Référence sur les stratégies Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="37698-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="37698-104">Cette section fournit un index des stratégies dans la [Référence des stratégies de gestion des API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="37698-104">This section provides an index for the policies in the [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="37698-105">Pour plus d’informations sur l’ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="37698-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="37698-106">Les expressions de stratégie peuvent être utilisées comme valeurs d’attribut ou valeurs de texte dans l’une des stratégies de Gestion des API, sauf si la stratégie le spécifie autrement.</span><span class="sxs-lookup"><span data-stu-id="37698-106">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="37698-107">Certaines stratégies, telles que les stratégies [Contrôler le flux][Control flow] et [Définir la variable][Set variable], sont basées sur des expressions de stratégies.</span><span class="sxs-lookup"><span data-stu-id="37698-107">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="37698-108">Pour plus d’informations, consultez les pages [Stratégies avancées][Advanced policies] et [Expressions de stratégie][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="37698-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="37698-109">Index de référence de stratégie</span><span class="sxs-lookup"><span data-stu-id="37698-109">Policy reference index</span></span>
* <span data-ttu-id="37698-110">[Accès aux stratégies de restriction][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="37698-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="37698-111">[Check HTTP header][Check HTTP header] : applique l’existence et/ou la valeur d’un en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="37698-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="37698-112">[Limit call rate by subscription][Limit call rate by subscription] : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.</span><span class="sxs-lookup"><span data-stu-id="37698-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="37698-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.</span><span class="sxs-lookup"><span data-stu-id="37698-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="37698-114">[Restrict caller IPs][Restrict caller IPs] : filtre (autorise/rejette) les appels de certaines adresses IP et/ou plages d’adresses en particulier.</span><span class="sxs-lookup"><span data-stu-id="37698-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="37698-115">[Set usage quota by subscription][Set usage quota by subscription] : vous permet d’appliquer un volume d’appels et/ou un quota de bande passante renouvelable ou illimité par abonnement.</span><span class="sxs-lookup"><span data-stu-id="37698-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="37698-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) : vous permet d’appliquer un volume d’appel et/ou un quota de bande passante renouvelable ou illimité par clé.</span><span class="sxs-lookup"><span data-stu-id="37698-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="37698-117">[Validate JWT][Validate JWT] : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="37698-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="37698-118">[Stratégies avancées][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="37698-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="37698-119">[Control flow][Control flow] : applique de manière conditionnelle les instructions des stratégies en fonction des résultats de l’évaluation des [expressions][expressions] booléennes.</span><span class="sxs-lookup"><span data-stu-id="37698-119">[Control flow][Control flow] - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="37698-120">[Forward request][Forward request] : transfère la demande au service principal.</span><span class="sxs-lookup"><span data-stu-id="37698-120">[Forward request][Forward request] - Forwards the request to the backend service.</span></span>
  * <span data-ttu-id="37698-121">[Log to Event Hub][Log to Event Hub] : envoie des messages au format spécifié à une cible de message définie par une entité [Enregistreur](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger).</span><span class="sxs-lookup"><span data-stu-id="37698-121">[Log to Event Hub][Log to Event Hub] - Sends messages in the specified format to a message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="37698-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) : effectue une nouvelle tentative d’exécution des instructions de stratégie incluses, si la condition est remplie et jusqu’à ce qu’elle le soit.</span><span class="sxs-lookup"><span data-stu-id="37698-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="37698-123">L’exécution se répète à intervalles réguliers et ce jusqu’au nombre de tentatives défini.</span><span class="sxs-lookup"><span data-stu-id="37698-123">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>
  * <span data-ttu-id="37698-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) : abandonne l’exécution du pipeline et renvoie la réponse indiquée directement à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="37698-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>
  * <span data-ttu-id="37698-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) : envoie une demande à l’URL indiquée sans attendre de réponse.</span><span class="sxs-lookup"><span data-stu-id="37698-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="37698-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) : envoie une demande à l’URL indiquée.</span><span class="sxs-lookup"><span data-stu-id="37698-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request to the specified URL.</span></span>
  * <span data-ttu-id="37698-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) : permet de modifier la méthode HTTP d’une demande.</span><span class="sxs-lookup"><span data-stu-id="37698-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>
  * <span data-ttu-id="37698-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) : permet de définir le code d’état HTTP sur la valeur indiquée.</span><span class="sxs-lookup"><span data-stu-id="37698-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes the HTTP status code to the specified value.</span></span>
  * <span data-ttu-id="37698-129">[Set variable][Set variable] : conserve une valeur dans une variable de [contexte][context] nommée pour permettre d’y accéder ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="37698-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="37698-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) : ajoute une chaîne à la sortie de l’[inspecteur d’API](api-management-howto-api-inspector.md).</span><span class="sxs-lookup"><span data-stu-id="37698-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into the [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="37698-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) : attend l’exécution de la demande d’envoi intégré, la récupération de la valeur du cache ou le contrôle des stratégies du flux pour continuer.</span><span class="sxs-lookup"><span data-stu-id="37698-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies to complete before proceeding.</span></span>
* <span data-ttu-id="37698-132">[Stratégies d’authentification][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="37698-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="37698-133">[Authenticate with Basic][Authenticate with Basic] : authentification avec un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="37698-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="37698-134">[Authenticate with client certificate][Authenticate with client certificate] : authentification avec un service principal à l’aide de certificats clients.</span><span class="sxs-lookup"><span data-stu-id="37698-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="37698-135">[Stratégies de mise en cache][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="37698-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="37698-136">[Get from cache][Get from cache] : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="37698-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="37698-137">[Store to cache][Store to cache] : met en cache la réponse en fonction de la configuration de contrôle de cache spécifiée.</span><span class="sxs-lookup"><span data-stu-id="37698-137">[Store to cache][Store to cache] - Caches response according to the specified cache control configuration.</span></span>
  * <span data-ttu-id="37698-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : récupère un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="37698-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="37698-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) : stocke un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="37698-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in the cache by key.</span></span>
  * <span data-ttu-id="37698-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) : supprime un élément du cache par clé.</span><span class="sxs-lookup"><span data-stu-id="37698-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>
* <span data-ttu-id="37698-141">[Stratégies interdomaines][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="37698-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="37698-142">[Allow cross-domain calls][Allow cross-domain calls] : rend l’API accessible à partir des navigateurs clients utilisant Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="37698-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="37698-143">[CORS][CORS] : ajoute une prise en charge partage des ressources cross-origin (CORS) à une opération ou une API afin de permettre les appels interdomaines à partir des navigateurs clients.</span><span class="sxs-lookup"><span data-stu-id="37698-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="37698-144">[JSONP][JSONP] : ajoute une prise en charge de JSON avec remplissage (JSONP) à une opération ou une API afin de permettre les appels interdomaines à partir des navigateurs clients utilisant JavaScript.</span><span class="sxs-lookup"><span data-stu-id="37698-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="37698-145">[Stratégies de transformation][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="37698-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="37698-146">[Convert JSON to XML][Convert JSON to XML] : convertit le corps de la demande ou de la réponse de JSON en XML.</span><span class="sxs-lookup"><span data-stu-id="37698-146">[Convert JSON to XML][Convert JSON to XML] - Converts request or response body from JSON to XML.</span></span>
  * <span data-ttu-id="37698-147">[Convert XML to JSON][Convert XML to JSON] : convertit le corps de la demande ou de la réponse de XML en JSON.</span><span class="sxs-lookup"><span data-stu-id="37698-147">[Convert XML to JSON][Convert XML to JSON] - Converts request or response body from XML to JSON.</span></span>
  * <span data-ttu-id="37698-148">[Find and replace string in body][Find and replace string in body] : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="37698-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="37698-149">[Mask URLs in content][Mask URLs in content] : réécrit (masque) les liens dans le corps de la réponse afin qu’ils pointent vers un lien équivalent par l’intermédiaire de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="37698-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>
  * <span data-ttu-id="37698-150">[Set backend service][Set backend service] : modifie le service principal pour une demande entrante.</span><span class="sxs-lookup"><span data-stu-id="37698-150">[Set backend service][Set backend service] - Changes the backend service for an incoming request.</span></span>
  * <span data-ttu-id="37698-151">[Set body][Set body] : définit le corps du message pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="37698-151">[Set body][Set body] - Sets the message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="37698-152">[Set HTTP header][Set HTTP header] : affecte une valeur à un en-tête de réponse et/ou de demande existant ou bien ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="37698-152">[Set HTTP header][Set HTTP header] - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="37698-153">[Set query string parameter][Set query string parameter] : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="37698-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="37698-154">[URL de réécriture][Rewrite URL] : convertit une URL de demande de sa forme publique en une forme attendue par le service web.</span><span class="sxs-lookup"><span data-stu-id="37698-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form to the form expected by the web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37698-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37698-155">Next steps</span></span>
<span data-ttu-id="37698-156">Pour plus d’informations sur les expressions de stratégie, regardez la vidéo suivante.</span><span class="sxs-lookup"><span data-stu-id="37698-156">For more information on policy expressions, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log to Event Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store to cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON to XML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML to JSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


