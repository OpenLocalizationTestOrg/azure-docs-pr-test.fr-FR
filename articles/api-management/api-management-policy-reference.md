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
# <a name="azure-api-management-policy-reference"></a>Référence sur les stratégies Gestion des API Azure
Cette section fournit un index pour les stratégies hello Bonjour [référence de stratégie de gestion des API][API Management policy reference]. Pour plus d’informations sur l’ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API][Policies in API Management].

Expressions de stratégie peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans une des stratégies de gestion des API hello, sauf indication contraire de la stratégie de hello. Certaines stratégies telles que hello [flux de contrôle] [ Control flow] et [Set variable] [ Set variable] stratégies basées sur des expressions de stratégie. Pour plus d’informations, consultez les pages [Stratégies avancées][Advanced policies] et [Expressions de stratégie][Policy expressions].

## <a name="policy-reference-index"></a>Index de référence de stratégie
* [Accès aux stratégies de restriction][Access restriction policies]
  * [Check HTTP header][Check HTTP header] : applique l’existence et/ou la valeur d’un en-tête HTTP.
  * [Limit call rate by subscription][Limit call rate by subscription] : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.
  * [Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.
  * [Restrict caller IPs][Restrict caller IPs] : filtre (autorise/rejette) les appels de certaines adresses IP et/ou plages d’adresses en particulier.
  * [Définir le quota d’utilisation par abonnement] [ Set usage quota by subscription] -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.
  * [Définir le quota d’utilisation par clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par clé.
  * [Validate JWT][Validate JWT] : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.
* [Stratégies avancées][Advanced policies]
  * [Flux de contrôle] [ Control flow] - conditionnellement applique les instructions de stratégie basées sur les résultats d’évaluation hello booléen hello [expressions][expressions].
  * [Transférer la demande] [ Forward request] -transfère le service principal de hello demande toohello.
  * [Journal tooEvent Hub] [ Log tooEvent Hub] -envoie des messages hello format spécifié tooa cible de message défini par un [journal](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entité.
  * [Recommencez](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -l’exécution de nouvelles tentatives de hello placé entre les instructions de stratégie, si et jusqu'à ce que hello condition est remplie. L’exécution est répété à hello des intervalles de temps spécifié de toohello spécifié le nombre de tentatives.
  * [Retourner une réponse](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -hello retourne et de l’exécution du pipeline abandons spécifié réponse directement toohello appelant.
  * [Envoyer une demande unidirectionnelle](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -envoie une demande toohello spécifié des URL sans attendre une réponse.
  * [Envoyer la demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -envoie une demande toohello spécifié l’URL.
  * [Définir la méthode de demande](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -vous permet de méthode de hello HTTP toochange pour une demande.
  * [Définir le statut](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -modifications hello HTTP état code toohello de valeur spécifiée.
  * [Set variable][Set variable] : conserve une valeur dans une variable de [contexte][context] nommée pour permettre d’y accéder ultérieurement.
  * [Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -ajoute une chaîne en hello [API inspecteur](api-management-howto-api-inspector.md) sortie.
  * [Attente](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - attend envoi encadrée de demande, obtenir la valeur à partir du cache, ou contrôler toocomplete de stratégies de flux avant de continuer.
* [Stratégies d’authentification][Authentication policies]
  * [Authenticate with Basic][Authenticate with Basic] : authentification avec un service principal à l’aide de l’authentification de base.
  * [Authenticate with client certificate][Authenticate with client certificate] : authentification avec un service principal à l’aide de certificats clients.
* [Stratégies de mise en cache][Caching policies] 
  * [Get from cache][Get from cache] : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.
  * [Stocker toocache] [ Store toocache] -réponse Caches selon toohello spécifié de configuration de contrôle du cache.
  * [Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) : récupère un élément mis en cache par clé.
  * [Stockez la valeur dans le cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -stocker un élément dans le cache de hello par clé.
  * [Supprimez la valeur à partir du cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -supprimer un élément dans le cache de hello par clé.
* [Stratégies interdomaines][Cross domain policies] 
  * [Autoriser les appels inter-domaines] [ Allow cross-domain calls] -rend hello API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.
  * [CORS] [ CORS] -ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.
  * [JSONP] [ JSONP] - ajoute JSON padding (JSONP) de prise en charge tooan opération ou une API tooallow entre domaines appelle à partir de clients basés sur navigateur JavaScript.
* [Stratégies de transformation][Transformation policies] 
  * [Convertir en JSON tooXML] [ Convert JSON tooXML] - convertit demande ou le corps de la réponse de JSON tooXML.
  * [Convertir XML tooJSON] [ Convert XML tooJSON] - convertit demande ou le corps de la réponse à partir de XML tooJSON.
  * [Find and replace string in body][Find and replace string in body] : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.
  * [Masquer des URL dans le contenu] [ Mask URLs in content] -réécrit (masque) des liens dans la réponse de hello corps afin qu’ils pointent toohello le lien équivalent via une passerelle de hello.
  * [Définir le service principal] [ Set backend service] -modifie le service principal de hello pour une demande entrante.
  * [Définir le corps] [ Set body] -définit le corps du message hello pour les demandes entrantes et sortantes.
  * [En-tête HTTP] [ Set HTTP header] - assigne une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.
  * [Set query string parameter][Set query string parameter] : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.
  * [Réécriture d’URL] [ Rewrite URL] -convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les expressions de stratégie, consultez hello suivant vidéo.

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


