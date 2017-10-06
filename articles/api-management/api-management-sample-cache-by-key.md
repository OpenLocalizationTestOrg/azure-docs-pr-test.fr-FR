---
title: aaaCustom mise en cache dans Gestion des API Azure
description: "Découvrez comment les éléments de toocache par clé de gestion des API Azure"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>Mise en cache personnalisée dans Azure API Management
Service de gestion des API Azure a une prise en charge intégrée pour [mise en cache de réponse HTTP](api-management-howto-cache.md) à l’aide des URL de ressource hello en tant que clé de hello. Hello clé peut être modifiée par des en-têtes de demande à l’aide de hello `vary-by` propriétés. Cela est utile pour la mise en cache les réponses HTTP entières (également appelé représentations), mais il est parfois utile toojust cache une partie d’une représentation. Hello nouvelle [valeur de recherche de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) et [valeur du magasin de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) stratégies permettent hello toostore et récupérer des éléments arbitraires de données à partir de définitions de stratégie. Cette possibilité ajoute également toohello valeur précédemment introduit [demande d’envoi](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) stratégie, car vous pouvez maintenant mettre en cache les réponses à partir des services externes.

## <a name="architecture"></a>Architecture
Service de gestion des API utilise un cache de données partagées par client, afin que, lorsque vous faites évoluer les unités toomultiple vous obtiendrez toujours accès toohello même les données mises en cache. Toutefois, lorsque vous travaillez avec un déploiement de plusieurs régions, il existe des caches indépendantes dans chacune des régions de hello. Échéance toothis, il est important de toonot traiter le cache de hello comme magasin de données, où il est la seule source de hello de certains éléments d’informations. Si vous avez et ultérieurement décidé parti tootake de déploiement de plusieurs régions hello, les clients avec des utilisateurs qui se déplacent peuvent perdre accéder à des données toothat mis en cache.

## <a name="fragment-caching"></a>Mise en cache de fragments
Il existe certains cas où les réponses renvoyées contiennent une partie des données qui sont coûteuse toodetermine encore restent à jour pour un délai raisonnable. Pensez, par exemple, à un service généré par une compagnie aérienne qui fournit des informations concernant les réservations de vol, l’état du vol, etc. Si l’utilisateur de hello est membre du programme de points hello airlines, ils auraient pas également des informations concernant l’état actuel de tootheir et mileage accumulées. Ces informations relatives à l’utilisateur peuvent être stockées dans un autre système, mais il peut être souhaitable tooinclude dans les réponses retournée sur le vol et les réservations. Cette opération peut être effectuée à l’aide d’un processus appelé « mise en cache de fragments ». Hello représentation primaire peut être retournée à partir du serveur d’origine hello à l’aide d’un type de jeton tooindicate où hello des informations utilisateur sont toobe inséré. 

Envisagez de hello suivant la réponse JSON à partir d’une API de service principal.

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

Voici la ressource secondaire disponible à l’emplacement `/userprofile/{userid}` :

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

Dans l’ordre toodetermine hello utilisateur approprié informations tooinclude, nous devons tooidentify qui est de l’utilisateur final de hello. Ce mécanisme dépend de l’implémentation. Par exemple, j’utilise hello `Subject` revendication d’un `JWT` jeton. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Nous stockons cette valeur `enduserid` dans une variable de contexte en vue d’une utilisation ultérieure. étape suivante de Hello est toodetermine si une demande précédente a déjà les informations utilisateur hello récupérées et stocké dans le cache de hello. Pour cela, nous utilisons hello `cache-lookup-value` stratégie.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

S’il n’existe aucune entrée dans le cache hello qui correspond la valeur de la clé toohello, puis non `userprofile` variable contextuelle sera créé. Nous vérifions réussite hello de recherche de hello à l’aide de hello `choose` stratégie de flux de contrôle.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Si hello `userprofile` variable contextuelle n’existe pas, puis nous sommes continu toohave toomake HTTP demande tooretrieve il.

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

Nous utilisons hello `enduserid` ressource de profil utilisateur tooconstruct hello URL toohello. Une fois que nous avons la réponse de hello, nous pouvons extraire le corps du texte hello en dehors de la réponse de hello et stockez-le dans une variable de contexte.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid de nous avoir toomake cette requête HTTP, lorsque le même utilisateur hello effectue une autre requête, nous pouvons stocker hello profil dans le cache de hello.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Nous stockons les valeur hello dans le cache de hello à l’aide de la clé exacte même hello que nous avons tenté initialement tooretrieve avec. Hello durée nous choisir la valeur de hello toostore doit être basée sur la fréquence à laquelle hello modification des informations et des utilisateurs à la tolérance de panne sont tooout d’informations de date. 

Il est toorealize important que la récupération à partir du cache de hello est toujours un out-of-process, la demande réseau et potentiellement pouvez toujours ajouter des dizaines de millisecondes toohello demande. avantages de Hello sont fournis lorsque les informations de profil utilisateur hello déterminant dure plus longtemps que celle en raison de requêtes de base de données tooneeding toodo ou des informations d’agrégation à partir de plusieurs systèmes principaux.

Hello dernière étape du processus de hello est hello tooupdate a retourné une réponse avec ses informations de profil utilisateur.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

J’ai choisi tooinclude hello guillemets dans le cadre du jeton de hello afin que même lorsque hello remplacer ne se produit pas, réponse de hello a été JSON toujours valide. Il s’agit principalement les toomake débogage.

Une fois que vous combinez toutes ces étapes, le résultat final de hello est une stratégie qui ressemble à hello suivant un.

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

Cette approche de mise en cache est principalement utilisée dans les sites web où HTML est composé du côté serveur de hello afin qu’il peut être rendu en tant qu’une seule page. Toutefois, il peut également être utile dans les API dans lequel les clients ne peuvent pas faire client côté mise en cache HTTP ou il est préférable de tooput pas cette responsabilité sur le client de hello.

Ce même type de mise en cache de fragment peut également être effectué sur les serveurs web de hello principaux à l’aide d’un serveur de mise en cache de Redis, toutefois, à l’aide de tooperform de service de gestion des API hello ce travail est utile lorsque les fragments hello mises en cache provenant de différents systèmes principaux à hello réponses principales.

## <a name="transparent-versioning"></a>Contrôle de version transparent
Il est pratique courante pour plusieurs versions d’implémentation différente d’une toobe API prises en charge à la fois. Il s’agit peut-être toosupport différents environnements, tels que le développement, test, production, etc., ou il peut être toosupport des versions antérieures de temps de toogive hello API pour les versions d’API consommateurs toomigrate toonewer. 

Toohandling une approche ce à la place de demander aux clients aux développeurs toochange hello URL à partir de `/v1/customers` trop`/v2/customers` est toostore dans les données de profil du consommateur hello quelle version de hello API ils actuellement souhaitent toouse et appellent hello approprié URL du serveur principal. Dans toocall URL ordre toodetermine hello principal correct pour un client particulier, il est nécessaire tooquery certaines données de configuration. En mettant en cache les données de cette configuration, nous pouvons réduire baisse des performances de cette recherche hello.

Hello première étape est l’identificateur de hello toodetermine utilisait la version souhaitée de tooconfigure hello. Dans cet exemple, j’ai choisi de clé d’abonnement tooassociate hello version toohello produit. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

Nous avons ensuite procéder à une toosee de recherche de cache si nous avons déjà récupéré la version du client souhaité hello.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Puis nous vérifions toosee si nous n’a pas le trouvé dans le cache de hello.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Dans le cas contraire, il est alors possible de l’extraire.

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

Extrayez le texte du corps de réponse hello de réponse de hello.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Stockez-le dans cache hello pour une utilisation ultérieure.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

Et enfin à jour hello principal URL tooselect hello version de service hello souhaité par le client de hello.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Bonjour complètement stratégie est comme suit.

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

L’activation du contrôle de tootransparently consommateurs API version principale est accessible par les clients sans avoir tooupdate et redéployer les clients est une solution élégante qui traite de nombreux problèmes de contrôle de version d’API.

## <a name="tenant-isolation"></a>Isolation des locataires
Dans les déploiements mutualisés plus volumineux, certaines entreprises créent des groupes de locataires spécifiques sur des déploiements distincts de matériel du serveur principal. Cela réduit le nombre de hello de clients qui sont affectés à un problème matériel sur hello principal. Il permet également de nouvelles toobe de versions logicielles transférée par étapes. Dans l’idéal, cette architecture de serveur principal doit être transparent tooAPI consommateurs. Cela peut être effectuée dans un contrôle de version de tootransparent façon similaire, car il est basé sur hello même technique de manipulation des URL de serveur principal hello en utilisant l’état de configuration par clé d’API.  

Au lieu de retourner une version préférée du hello API pour chaque clé d’abonnement, vous devez retourner un identificateur qui est lié à un groupe de matériel client toohello attribué. Cet identificateur peut être utilisé tooconstruct hello principaux appropriés URL.

## <a name="summary"></a>Résumé
hello toouse de liberté Hello du cache de gestion des API Azure pour stocker n’importe quel type de données permet de données tooconfiguration un accès efficace qui peuvent affecter de manière hello qu'une demande entrante est traitée. Il peut également être utilisé toostore les fragments de données qui peuvent augmenter les réponses retournées à partir d’une API de service principal.

## <a name="next-steps"></a>Étapes suivantes
Veuillez envoyez-nous vos commentaires Bonjour Disqus thread de cette rubrique s’il existe d’autres scénarios que ces stratégies ont activé pour vous, ou s’il existe des scénarios vous aimeriez tooachieve mais que vous n’êtes pas sont actuellement possibles.

