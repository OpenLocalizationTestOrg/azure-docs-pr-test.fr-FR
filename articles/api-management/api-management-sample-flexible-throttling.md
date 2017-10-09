---
title: demande aaaAdvanced limitation avec gestion des API Azure
description: "Découvrez comment toocreate et appliquer le quota flexible et stratégies de gestion des API Azure de limitation du débit."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Limitation de requêtes avancée avec Gestion des API Azure
Les demandes entrantes en mesure de toothrottle est un rôle clé de la gestion des API Azure. Permet de gestion des API en contrôle taux hello de demandes ou hello total de demandes/données transférées, API fournisseurs tooprotect leurs API à partir des abus et créer une valeur pour les différents niveaux de produit d’API.

## <a name="product-based-throttling"></a>Limitation en fonction du produit
toodate, capacités de limitation des taux de hello ont été limitée toobeing étendue tooa particulier produit abonnement (essentiellement une clé), défini dans hello portail de gestion des API serveur de publication. Cela est utile pour les limites de tooapply fournisseur hello API aux développeurs de hello qui se sont inscrits toouse leur API, toutefois, il ne change rien, par exemple, dans la limitation des utilisateurs finaux de hello API. Il est possible que pour un utilisateur unique de tooconsume d’application du développeur hello hello quota entière et puis empêchent autres clients de développeur de hello application hello de toouse en mesure de. En outre, plusieurs clients qui peuvent générer un volume élevé de demandes peuvent limiter les utilisateurs toooccasional d’accès.

## <a name="custom-key-based-throttling"></a>Limitation basée sur une clé personnalisée
Hello nouvelle [taux limite par clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [par clé de quota](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) stratégies également fournir un contrôle de tootraffic solution beaucoup plus souple. Ces nouvelles stratégies autorisent toodefine expressions tooidentify hello les clés qui seront l’utilisation du trafic de tootrack utilisé. Hello bonne façon est le plus simple illustrée par un exemple. 

## <a name="ip-address-throttling"></a>Limitation par adresse IP
les stratégies suivantes Hello restreignent un seul client IP adresse tooonly 10 appelle chaque minute, avec un total d’appels de 1 000 000 et 10 000 kilo-octets de la bande passante par mois. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Si tous les clients sur Internet de hello utilisé une adresse IP unique, cela peut être un moyen efficace de limiter l’utilisation par l’utilisateur. Toutefois, il est probable que plusieurs utilisateurs seront partage une seule adresse IP publique échéance hello toothem l’accès à Internet via un périphérique NAT. En dépit de cela, pour les API qui permettent de hello d’accès non authentifié `IpAddress` peut être préférable de hello.

## <a name="user-identity-throttling"></a>Limitation par identité d'utilisateur
Si un utilisateur final est authentifié, une clé de limitation de la clé peut être générée en fonction d’informations qui identifient cet utilisateur de façon unique.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

Dans cet exemple nous extraire l’en-tête d’autorisation hello, convertissez-le trop`JWT` de l’objet et utiliser le sujet hello d’utilisateur de hello hello tooidentify jeton et l’utiliser comme clé de limitation du débit de hello. Si l’identité utilisateur hello est stockée dans hello `JWT` comme un des hello autres revendications ensuite que la valeur peut être utilisée à la place.

## <a name="combined-policies"></a>Stratégies combinées
Bien que hello nouvelles stratégies de limitation offrent davantage de contrôle que hello existante des stratégies de limitation, il est toujours valeur combinant deux fonctionnalités. Limitation de la clé de produit abonnement ([taux d’appels limite par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) est un excellent moyen tooenable monétisation d’une API en débitant basée sur les niveaux d’utilisation. Hello contrôle plus fin d’être en mesure de toothrottle par l’utilisateur est complémentaire et empêche le comportement de l’un utilisateur dégrader expérience hello d’un autre. 

## <a name="client-driven-throttling"></a>Limitation par client
Lorsque hello limitation de la clé est définie en utilisant un [expression de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx), il s’agit de fournisseur hello API qui consiste à choisir comment hello de limitation est étendue. Toutefois, un développeur peut décider d’évaluation de toocontrol limiter leurs propres clients. Cela peut être activé par le fournisseur d’API hello en introduisant client application toocommunicate hello clé toohello un en-tête personnalisé tooallow hello du développeur API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Cela permet de toochoose d’application du développeur hello client comment ils veulent toocreate clé de limitation du débit de hello. Avec un peu d’ingéniosité un développeur client peut créer leurs propres niveaux de taux en allouant des jeux de clés toousers et de rotation de l’utilisation de la clé de hello.

## <a name="summary"></a>Résumé
Gestion des API Azure fournit des devis limitation tooboth taux protéger et ajoutez le service de l’API tooyour valeur. Hello limitation de nouvelles stratégies avec les règles de portée personnalisées autorise que vous plus fine plus aisément un contrôle sur les stratégies de tooenable vos applications de meilleure toobuild clients. exemples de Hello dans cet article montrent utilisez hello de ces nouvelles stratégies par clés avec des adresses IP du client, identité des utilisateurs et des valeurs de client générée de limitation du débit de fabrication. Toutefois, il existe de nombreuses autres parties du message de type hello qui peuvent être utilisées telles que l’agent utilisateur, de fragments de chemin d’accès d’URL, de taille de message.

## <a name="next-steps"></a>Étapes suivantes
Veuillez envoyez-nous vos commentaires dans le thread de Disqus hello pour cette rubrique. Il serait très toohear sur les autres valeurs de clés potentielles qui ont été un choix logique dans vos scénarios.

## <a name="watch-a-video-overview-of-these-policies"></a>Regarder une vidéo de présentation de ces stratégies.
Pour plus d’informations sur hello [taux limite par clé](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [par clé de quota](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) stratégies abordées dans cet article, veuillez consulter hello suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

