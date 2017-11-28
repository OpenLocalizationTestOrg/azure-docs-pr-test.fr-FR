---
title: "aaaAzure référence de stratégie de gestion des API"
description: "Découvrez hello stratégies tooconfigure disponible gestion des API."
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
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="40709-103">Référence sur les stratégies Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="40709-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="40709-104">Cette section fournit un index pour les stratégies hello Bonjour [référence de stratégie de gestion des API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="40709-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="40709-105">Pour plus d’informations sur l’ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="40709-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="40709-106">Expressions de stratégie peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans une des stratégies de gestion des API hello, sauf indication contraire de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="40709-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="40709-107">Certaines stratégies telles que hello [flux de contrôle] [ Control flow] et [Set variable] [ Set variable] stratégies basées sur des expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="40709-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="40709-108">Pour plus d’informations, consultez les pages [Stratégies avancées][Advanced policies] et [Expressions de stratégie][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="40709-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="40709-109">Index de référence de stratégie</span><span class="sxs-lookup"><span data-stu-id="40709-109">Policy reference index</span></span>
* <span data-ttu-id="40709-110">[Accès aux stratégies de restriction][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="40709-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="40709-111">[Check HTTP header][Check HTTP header] : applique l’existence et/ou la valeur d’un en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="40709-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="40709-112">[Limit call rate by subscription][Limit call rate by subscription] : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.</span><span class="sxs-lookup"><span data-stu-id="40709-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="40709-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.</span><span class="sxs-lookup"><span data-stu-id="40709-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="40709-114">[Restrict caller IPs][Restrict caller IPs] : filtre (autorise/rejette) les appels de certaines adresses IP et/ou plages d’adresses en particulier.</span><span class="sxs-lookup"><span data-stu-id="40709-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="40709-115">[Définir le quota d’utilisation par abonnement] [ Set usage quota by subscription] -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.</span><span class="sxs-lookup"><span data-stu-id="40709-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="40709-116">[Définir le quota d’utilisation par clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par clé.</span><span class="sxs-lookup"><span data-stu-id="40709-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="40709-117">[Validate JWT][Validate JWT] : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.</span><span class="sxs-lookup"><span data-stu-id="40709-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="40709-118">[Stratégies avancées][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="40709-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="40709-119">[Flux de contrôle] [ Control flow] - conditionnellement applique les instructions de stratégie basées sur les résultats d’évaluation hello booléen hello [expressions][expressions].</span><span class="sxs-lookup"><span data-stu-id="40709-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="40709-120">[Transférer la demande] [ Forward request] -transfère le service principal de hello demande toohello.</span><span class="sxs-lookup"><span data-stu-id="40709-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="40709-121">[Journal tooEvent Hub] [ Log tooEvent Hub] -envoie des messages hello format spécifié tooa cible de message défini par un [journal](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entité.</span><span class="sxs-lookup"><span data-stu-id="40709-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="40709-122">[Recommencez](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -l’exécution de nouvelles tentatives de hello placé entre les instructions de stratégie, si et jusqu'à ce que hello condition est remplie.</span><span class="sxs-lookup"><span data-stu-id="40709-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="40709-123">L’exécution est répété à hello des intervalles de temps spécifié de toohello spécifié le nombre de tentatives.</span><span class="sxs-lookup"><span data-stu-id="40709-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="40709-124">[Retourner une réponse](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -hello retourne et de l’exécution du pipeline abandons spécifié réponse directement toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="40709-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="40709-125">[Envoyer une demande unidirectionnelle](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -envoie une demande toohello spécifié des URL sans attendre une réponse.</span><span class="sxs-lookup"><span data-stu-id="40709-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="40709-126">[Envoyer la demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -envoie une demande toohello spécifié l’URL.</span><span class="sxs-lookup"><span data-stu-id="40709-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="40709-127">[Définir la méthode de demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -vous permet de méthode de hello HTTP toochange pour une demande.</span><span class="sxs-lookup"><span data-stu-id="40709-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="40709-128">[Définir le statut](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -modifications hello HTTP état code toohello de valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="40709-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="40709-129">[Set variable][Set variable] : conserve une valeur dans une variable de [contexte][context] nommée pour permettre d’y accéder ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="40709-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="40709-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -ajoute une chaîne en hello [API inspecteur](api-management-howto-api-inspector.md) sortie.</span><span class="sxs-lookup"><span data-stu-id="40709-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="40709-131">[Attente](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - attend envoi encadrée de demande, obtenir la valeur à partir du cache, ou contrôler toocomplete de stratégies de flux avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="40709-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="40709-132">[Stratégies d’authentification][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="40709-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="40709-133">[Authenticate with Basic][Authenticate with Basic] : authentification avec un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="40709-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="40709-134">[Authenticate with client certificate][Authenticate with client certificate] : authentification avec un service principal à l’aide de certificats clients.</span><span class="sxs-lookup"><span data-stu-id="40709-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="40709-135">[Stratégies de mise en cache][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="40709-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="40709-136">[Get from cache][Get from cache] : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.</span><span class="sxs-lookup"><span data-stu-id="40709-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="40709-137">[Stocker toocache] [ Store toocache] -réponse Caches selon toohello spécifié de configuration de contrôle du cache.</span><span class="sxs-lookup"><span data-stu-id="40709-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="40709-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : récupère un élément mis en cache par clé.</span><span class="sxs-lookup"><span data-stu-id="40709-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="40709-139">[Stockez la valeur dans le cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -stocker un élément dans le cache de hello par clé.</span><span class="sxs-lookup"><span data-stu-id="40709-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="40709-140">[Supprimez la valeur à partir du cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -supprimer un élément dans le cache de hello par clé.</span><span class="sxs-lookup"><span data-stu-id="40709-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="40709-141">[Stratégies interdomaines][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="40709-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="40709-142">[Autoriser les appels inter-domaines] [ Allow cross-domain calls] -rend hello API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="40709-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="40709-143">[CORS] [ CORS] -ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.</span><span class="sxs-lookup"><span data-stu-id="40709-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="40709-144">[JSONP] [ JSONP] - ajoute JSON padding (JSONP) de prise en charge tooan opération ou une API tooallow entre domaines appelle à partir de clients basés sur navigateur JavaScript.</span><span class="sxs-lookup"><span data-stu-id="40709-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="40709-145">[Stratégies de transformation][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="40709-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="40709-146">[Convertir en JSON tooXML] [ Convert JSON tooXML] - convertit demande ou le corps de la réponse de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="40709-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="40709-147">[Convertir XML tooJSON] [ Convert XML tooJSON] - convertit demande ou le corps de la réponse à partir de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="40709-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="40709-148">[Find and replace string in body][Find and replace string in body] : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="40709-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="40709-149">[Masquer des URL dans le contenu] [ Mask URLs in content] -réécrit (masque) des liens dans la réponse de hello corps afin qu’ils pointent toohello le lien équivalent via une passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="40709-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="40709-150">[Définir le service principal] [ Set backend service] -modifie le service principal de hello pour une demande entrante.</span><span class="sxs-lookup"><span data-stu-id="40709-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="40709-151">[Définir le corps] [ Set body] -définit le corps du message hello pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="40709-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="40709-152">[En-tête HTTP] [ Set HTTP header] - assigne une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="40709-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="40709-153">[Set query string parameter][Set query string parameter] : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="40709-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="40709-154">[Réécriture d’URL] [ Rewrite URL] -convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello.</span><span class="sxs-lookup"><span data-stu-id="40709-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40709-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40709-155">Next steps</span></span>
<span data-ttu-id="40709-156">Pour plus d’informations sur les expressions de stratégie, consultez hello suivant vidéo.</span><span class="sxs-lookup"><span data-stu-id="40709-156">For more information on policy expressions, see hello following video.</span></span>

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
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
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


