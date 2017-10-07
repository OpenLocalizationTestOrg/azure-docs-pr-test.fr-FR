---
title: "stratégies de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies de hello disponibles pour une utilisation dans la gestion des API Azure."
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a>Stratégies API Management
Cette section fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](api-management-howto-policies.md).  
  
 Les stratégies sont une fonctionnalité puissante du système hello autoriser la publication de hello toochange hello du comportement de hello API via la configuration. Les stratégies sont une collection d’instructions qui sont exécutées séquentiellement sur la demande de hello ou de réponse d’une API. Les instructions populaires incluent une conversion de format à partir de XML tooJSON et limiter ainsi toorestrict hello d’appels entrants à partir d’un développeur de taux d’appels. De nombreuses stratégies supplémentaires sont disponibles en dehors de la zone de hello.  
  
 Expressions de stratégie peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans une des stratégies de gestion des API hello, sauf indication contraire de la stratégie de hello. Certaines stratégies telles que hello [flux de contrôle](api-management-advanced-policies.md#choose) et [Set variable](api-management-advanced-policies.md#set-variable) stratégies basées sur des expressions de stratégie. Pour plus d’informations, consultez les rubriques [Stratégies avancées](api-management-advanced-policies.md#AdvancedPolicies) et [Expressions de stratégie](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a> Stratégies  
  
-   [Accès aux stratégies de restriction](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) : applique l’existence et/ou la valeur d’un en-tête HTTP.  
  
    -   [Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par abonnement.  
  
    -   [Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) : empêche les pics d’utilisation de l’API en limitant le débit d’appels par clé.  
  
    -   [Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) : filtre (autorise/rejette) les appels de certaines adresses IP spécifiques et/ou de certaines plages d’adresses.  
  
    -   [Définir le quota d’utilisation par abonnement](api-management-access-restriction-policies.md#SetUsageQuota) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par abonnement.  
  
    -   [Définir le quota d’utilisation par clé](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -vous permet de tooenforce un quota renouvelable ou à durée de vie appel volume et/ou de la bande passante, sur une base par clé.  
  
    -   [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) : applique l’existence et la validité d’un JWT extrait d’un en-tête HTTP ou d’un paramètre de requête spécifié.  
  
-   [Stratégies avancées](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Flux de contrôle](api-management-advanced-policies.md#choose) - conditionnellement applique les instructions de stratégie basées sur l’évaluation d’expressions booléennes hello.  
  
    -   [Transférer la demande](api-management-advanced-policies.md#ForwardRequest) -transfère le service principal de hello demande toohello.  
  
    -   [Journal tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) -envoie des messages hello format spécifié tooa cible de message défini par une entité de l’enregistreur d’événements.  
  
    -   [Recommencez](api-management-advanced-policies.md#Retry) -l’exécution de nouvelles tentatives de hello placé entre les instructions de stratégie, si et jusqu'à ce que hello condition est remplie. L’exécution est répété à hello des intervalles de temps spécifié de toohello spécifié le nombre de tentatives.  
  
    -   [Retourner une réponse](api-management-advanced-policies.md#ReturnResponse) -hello retourne et de l’exécution du pipeline abandons spécifié réponse directement toohello appelant.  
  
    -   [Envoyer une demande unidirectionnelle](api-management-advanced-policies.md#SendOneWayRequest) -envoie une demande toohello spécifié des URL sans attendre une réponse.  
  
    -   [Envoyer la demande](api-management-advanced-policies.md#SendRequest) -envoie une demande toohello spécifié l’URL.  
  
    -   [Set variable](api-management-advanced-policies.md#set-variable) : conserve une valeur dans une variable de contexte nommée pour permettre d’y accéder ultérieurement.  
  
    -   [Définir la méthode de demande](api-management-advanced-policies.md#SetRequestMethod) -vous permet de méthode de hello HTTP toochange pour une demande.  
  
    -   [Définir le code d’état](api-management-advanced-policies.md#SetStatus) -modifications hello HTTP état code toohello de valeur spécifiée.  
  
    -   [Trace](api-management-advanced-policies.md#Trace) -ajoute une chaîne en hello [API inspecteur](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) sortie.  
  
    -   [Attente](api-management-advanced-policies.md#Wait) -attend placée entre [demande d’envoi](api-management-advanced-policies.md#SendRequest), [obtenir la valeur à partir du cache](api-management-caching-policies.md#GetFromCacheByKey), ou [flux de contrôle](api-management-advanced-policies.md#choose) toocomplete stratégies avant de continuer.  
  
-   [Stratégies d’authentification](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Authenticate with Basic](api-management-authentication-policies.md#Basic) : authentification avec un service principal à l’aide de l’authentification de base.  
  
    -   [Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) : authentification avec un service principal à l’aide de certificats clients.  
  
-   [Stratégies de mise en cache](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Get from cache](api-management-caching-policies.md#GetFromCache) : effectue une recherche dans le cache et renvoie une réponse mise en cache valide si elle est disponible.  
  
    -   [Stocker toocache](api-management-caching-policies.md#StoreToCache) -réponse Caches selon toohello spécifié de configuration de contrôle du cache.  
  
    -   [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) : récupère un élément mis en cache par clé.  
  
    -   [Stockez la valeur dans le cache](api-management-caching-policies.md#StoreToCacheByKey) -stocker un élément dans le cache de hello par clé.  
  
    -   [Supprimez la valeur à partir du cache](api-management-caching-policies.md#RemoveCacheByKey) -supprimer un élément dans le cache de hello par clé.  
  
-   [Stratégies interdomaines](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Autoriser les appels inter-domaines](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -rend hello API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) - ajoute JSON padding (JSONP) de prise en charge tooan opération ou une API tooallow entre domaines appelle à partir de clients basés sur navigateur JavaScript.  
  
-   [Stratégies de transformation](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Convertir en JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - convertit demande ou le corps de la réponse de JSON tooXML.  
  
    -   [Convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - convertit demande ou le corps de la réponse à partir de XML tooJSON.  
  
    -   [Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.  
  
    -   [Masquer des URL dans le contenu](api-management-transformation-policies.md#MaskURLSContent) -réécrit (masque) des liens dans la réponse de hello corps afin qu’ils pointent toohello le lien équivalent via une passerelle de hello.  
  
    -   [Définir le service principal](api-management-transformation-policies.md#SetBackendService) -modifie le service principal de hello pour une demande entrante.  
  
    -   [Définir le corps](api-management-transformation-policies.md#SetBody) -définit le corps du message hello pour les demandes entrantes et sortantes.  
  
    -   [En-tête HTTP](api-management-transformation-policies.md#SetHTTPheader) - assigne une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.  
  
    -   [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.  
  
    -   [Réécriture d’URL](api-management-transformation-policies.md#RewriteURL) -convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello.  
  
    -   [Transformer du code XML à l’aide d’une transformation XSLT](api-management-transformation-policies.md#XSLTransform) -applique un tooXML de la transformation XSL dans le corps de demande ou réponse hello.  
  
## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).  
