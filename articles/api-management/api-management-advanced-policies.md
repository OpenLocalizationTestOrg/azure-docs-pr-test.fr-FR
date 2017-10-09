---
title: "aaaAzure avancée des stratégies de gestion des API | Documents Microsoft"
description: "Découvrez hello avancée des stratégies disponibles pour une utilisation dans la gestion des API Azure."
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
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>Stratégies avancées de la Gestion des API
Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API. Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a> Stratégies avancées  
  
-   [Flux de contrôle](api-management-advanced-policies.md#choose) - conditionnellement applique les instructions de stratégie basées sur les résultats d’évaluation hello booléen hello [expressions](api-management-policy-expressions.md).  
  
-   [Transférer la demande](#ForwardRequest) -transfère le service principal de hello demande toohello.

-   [Limiter l’accès concurrentiel](#LimitConcurrency) -empêche entre les stratégies à partir de l’exécution en plus de hello du nombre spécifié de demandes à la fois.
  
-   [Journal tooEvent Hub](#log-to-eventhub) -envoie des messages hello spécifié tooan format concentrateur d’événements défini par une entité de l’enregistreur d’événements. 

-   [Simuler la réponse](#mock-response) -abandons de l’exécution du pipeline et renvoie une réponse factices directement toohello appelant.
  
-   [Recommencez](#Retry) -l’exécution de nouvelles tentatives de hello placé entre les instructions de stratégie, si et jusqu'à ce que hello condition est remplie. L’exécution est répété à hello des intervalles de temps spécifié de toohello spécifié le nombre de tentatives.  
  
-   [Retourner une réponse](#ReturnResponse) -hello retourne et de l’exécution du pipeline abandons spécifié réponse directement toohello appelant. 
  
-   [Envoyer une demande unidirectionnelle](#SendOneWayRequest) -envoie une demande toohello spécifié des URL sans attendre une réponse.  
  
-   [Envoyer la demande](#SendRequest) -envoie une demande toohello spécifié l’URL.  

-   [Définir le proxy HTTP](#SetHttpProxy) -vous permet de demandes tooroute transmis via un proxy HTTP.  

-   [Définir la méthode de demande](#SetRequestMethod) -vous permet de méthode de hello HTTP toochange pour une demande.  
  
-   [Définir le code d’état](#SetStatus) -modifications hello HTTP état code toohello de valeur spécifiée.  
  
-   [Set variable](api-management-advanced-policies.md#set-variable) : conserve une valeur dans une variable de [contexte](api-management-policy-expressions.md#ContextVariables) nommée pour permettre d’y accéder ultérieurement.  

-   [Trace](#Trace) -ajoute une chaîne en hello [API inspecteur](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) sortie.  
  
-   [Attente](#Wait) -attend placée entre [demande d’envoi](api-management-advanced-policies.md#SendRequest), [obtenir la valeur à partir du cache](api-management-caching-policies.md#GetFromCacheByKey), ou [flux de contrôle](api-management-advanced-policies.md#choose) toocomplete stratégies avant de continuer.  
  
##  <a name="choose"></a> Control flow  
 Hello `choose` stratégie applique la stratégie entre crochets de construisent des instructions en fonction de résultat hello d’évaluation des expressions booléennes, similaires tooan if-then-else ou un commutateur dans un langage de programmation.  
  
###  <a name="ChoosePolicyStatement"></a> Instruction de la stratégie  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 Hello stratégie de flux de contrôle doit contenir au moins un `<when/>` élément. Hello `<otherwise/>` élément est facultatif. Dans les conditions `<when/>` éléments sont évalués dans leur ordre d’apparition dans la stratégie de hello. Déclarations de stratégie incluses dans hello tout d’abord `<when/>` élément avec l’attribut de condition est égal à `true` seront appliqués. Stratégies encadrées hello `<otherwise/>` élément, le cas échéant, est appliquée si tous les Hello `<when/>` sont des attributs de l’élément condition `false`.  
  
### <a name="examples"></a>Exemples  
  
####  <a name="ChooseExample"></a> Exemple  
 Hello exemple suivant montre un [set-variable](api-management-advanced-policies.md#set-variable) stratégie et deux stratégies de flux de contrôle.  
  
 stratégie de variable Hello définie est dans hello section entrante et crée un `isMobile` booléenne [contexte](api-management-policy-expressions.md#ContextVariables) variable a la valeur tootrue si hello `User-Agent` demande en-tête contient le texte hello `iPad` ou `iPhone`.  
  
 stratégie de flux de contrôle de première Hello est également dans hello section entrante et applique de manière conditionnelle une des deux [définir le paramètre de chaîne de requête](api-management-transformation-policies.md#SetQueryStringParameter) stratégies en fonction de la valeur hello hello `isMobile` variable contextuelle.  
  
 stratégie de flux de contrôle de deuxième Hello est dans la section sortante de hello et applique de façon conditionnelle hello [tooJSON de convertir le XML](api-management-transformation-policies.md#ConvertXMLtoJSON) stratégie lorsque `isMobile` est défini trop`true`.  
  
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
  
#### <a name="example"></a>Exemple  
 Cet exemple montre comment tooperform le filtrage de contenu en supprimant des éléments de données à partir de la réponse de hello reçu hello principal service lors de l’utilisation de hello `Starter` produit. Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too34:30. Démarrer à 31:50 toosee une vue d’ensemble de [hello API de prévision ciel foncé](https://developer.forecast.io/) utilisée pour cette démonstration.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|choose|Élément racine.|Oui|  
|when|Hello toouse condition pour hello `if` ou `ifelse` parties Hello `choose` stratégie. Si hello `choose` stratégie possède plusieurs `when` sections, elles sont évaluées de façon séquentielle. Une fois hello `condition` d’une lorsqu’élément évalue trop`true`, aucune autre `when` conditions sont évaluées.|Oui|  
|otherwise|Contient des hello stratégie extrait toobe est utilisé si aucun des hello `when` conditions ont trop`true`.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|  
|---------------|-----------------|--------------|  
|condition="Boolean expression &#124; Boolean constant"|expression booléenne de Hello ou constante tooevaluated lorsque hello contenant `when` l’instruction de stratégie est évaluée.|Oui|  
  
###  <a name="ChooseUsage"></a> Utilisation  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="ForwardRequest"></a> Forward request  
 Hello `forward-request` stratégie transfère hello entrants demande toohello service principal spécifié dans la demande de hello [contexte](api-management-policy-expressions.md#ContextVariables). URL du service principal Hello est spécifié dans hello API [paramètres](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) et peuvent être modifiés à l’aide de hello [définir le service principal](api-management-transformation-policies.md) stratégie.  
  
> [!NOTE]
>  Supprimer les résultats de cette stratégie de demande hello ne pas transmis principal toohello service et hello des stratégies dans la section sortante de hello sont évaluées immédiatement à l’achèvement réussi de hello de stratégies de hello hello entrants de section.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Exemples  
  
#### <a name="example"></a>Exemple  
 Hello stratégie au niveau d’API suivante transfère toutes les demandes de service principal de toohello avec un intervalle de délai d’attente de 60 secondes.  
  
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
  
#### <a name="example"></a>Exemple  
 Stratégie de niveau de cette opération utilise hello `base` stratégie de serveur principal élément tooinherit hello à partir de l’étendue de niveau parent API hello.  
  
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
  
#### <a name="example"></a>Exemple  
 Stratégie de niveau de cette opération transfère tous les service principal toohello de demandes avec un délai d’attente de 120 explicitement et n’hérite pas de parent de hello stratégie principales au niveau d’API.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Exemple  
 Stratégie de niveau de cette opération ne transfère pas les demandes de service principal de toohello.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|forward-request|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|timeout="integer"|intervalle de délai d’attente Hello en secondes avant que le service principal de hello appel toohello échoue.|Non|Aucun délai d’expiration|  
|follow-redirects="true &#124; false"|Spécifie si les redirections à partir du service principal de hello sont suivies par la passerelle de hello ou retournées toohello appelant.|Non|false|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** backend  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="LimitConcurrency"></a> Limit concurrency  
 Hello `limit-concurrency` stratégie empêche entre les stratégies de s’exécuter par plusieurs hello du nombre spécifié de demandes à un moment donné. Fonction dépassant le seuil de hello, nouvelles demandes sont ajoutés tooa file d’attente jusqu'à ce que la longueur de file d’attente maximale hello est atteint. Lorsque la file est pleine, les nouvelles requêtes échouent immédiatement.
  
###  <a name="LimitConcurrencyStatement"></a> Instruction de la stratégie  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Exemples  
  
####  <a name="ChooseExample"></a> Exemple  
 Hello exemple suivant montre comment nombre toolimit de demandes transmises principal tooa selon la valeur hello d’une variable contextuelle.
 
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

### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|    
|limit-concurrency|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|--------------|  
|key|Une chaîne. Expression autorisée. Spécifie l’étendue d’accès concurrentiel hello. Peut être partagée par plusieurs stratégies.|Oui|N/A|  
|max-count|Nombre entier. Spécifie un nombre maximal de demandes autorisées stratégie de hello tooenter.|Oui|N/A|  
|timeout|Nombre entier. Expression autorisée. Spécifie le nombre de hello de secondes pendant lesquelles une demande doit attendre tooenter avant d’échouer avec une étendue de « 403 trop grand nombre de demandes »|Non|Infini|  
|max-queue-length|Nombre entier. Expression autorisée. Spécifie la longueur de file d’attente maximale hello. Les demandes entrantes lors de la tentative tooenter cette stratégie va se terminer avec « 403 trop grand nombre de demandes « immédiatement lorsque la file d’attente hello est épuisée.|Non|Infini|  
  
###  <a name="ChooseUsage"></a> Utilisation  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  

##  <a name="log-to-eventhub"></a>Journal tooEvent Hub  
 Hello `log-to-eventhub` envoie stratégie messages Bonjour spécifiés format tooan concentrateur d’événements définis par une entité de l’enregistreur d’événements. Comme son nom l’indique, la stratégie de hello est utilisé pour l’enregistrement sélectionné demande ou réponse les informations de contexte pour l’analyse en ligne ou hors connexion.  
  
> [!NOTE]
>  Pour obtenir un guide pas à pas sur la configuration d’un concentrateur d’événements et de journalisation des événements, consultez [comment toolog les événements de gestion des API avec Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Exemple  
 Toute chaîne peut être utilisée en tant que hello valeur toobe est enregistré dans les concentrateurs d’événements. Dans cet exemple hello date et l’heure, le nom de service de déploiement, id de demande, adresse ip et nom de l’opération pour tous les appels entrants sont concentrateur d’événements connecté toohello journal enregistré avec hello `contoso-logger` id.  
  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|log-to-eventhub|Élément racine. valeur Hello de cet élément est un concentrateur d’événements hello chaîne toolog tooyour.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|  
|---------------|-----------------|--------------|  
|logger-id|id de Hello Hello enregistreur d’événements inscrits auprès du service Gestion des API.|Oui|  
|partition-id|Spécifie l’index hello de partition hello où les messages sont envoyés.|facultatif. Cet attribut peut ne pas être utilisé si `partition-key` est utilisé.|  
|partition-key|Spécifie la valeur hello utilisé pour l’attribution de partition lorsque des messages sont envoyés.|facultatif. Cet attribut peut ne pas être utilisé si `partition-id` est utilisé.|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  

##  <a name="mock-response"></a> Réponse factice  
Hello `mock-response`, en tant que nom de hello implique, est utilisé toomock API et les opérations. Il interrompt l’exécution du pipeline normal et retourne un appelant toohello de réponse factices. stratégie de Hello tente toujours de réponses tooreturn de plus haute fidélité. Elle préfère les exemples de contenu de réponse, le cas échéant. Elle génère des exemples de réponses à partir de schémas, lorsque les schémas sont fournis et les exemples ne le sont pas. Si aucun exemple ou schéma n’est trouvé, des réponses sans contenu sont retournées.
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Exemples  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|mock-response|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|--------------|  
|status-code|Spécifie le code d’état de réponse et exemple tooselect utilisé ou le schéma.|Non|200|  
|content-type|Spécifie `Content-Type` valeur d’en-tête de réponse et est utilisé tooselect exemple ou le schéma.|Non|Aucune|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues

##  <a name="Retry"></a> Retry  
 Hello `retry` stratégie exécute une fois les stratégies de ses enfants et puis de tentatives de leur exécution jusqu'à ce que la nouvelle tentative de hello `condition` devient `false` ou réessayez `count` est épuisé.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
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
  
### <a name="example"></a>Exemple  
 Bonjour suivant exemple demande forewarding est retentée des tooten heures à l’aide d’algorithme de tentative exponentielle. Étant donné que `first-fast-retry` a la valeur toofalse, toutes les nouvelles tentatives sont l’algorithme de tentative de sujet toohello exponsntial.  
  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|retry|Élément racine. Peut contenir n’importe quelle autre stratégie sous forme d’élément enfant.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|condition|[Expression](api-management-policy-expressions.md) ou littéral booléen spécifiant si les nouvelles tentatives doivent être arrêtées (`false`) ou poursuivies (`true`).|Oui|N/A|  
|count|Un nombre positif spécifiant hello le nombre maximal de nouvelles tentatives tooattempt.|Oui|N/A|  
|interval|Un nombre positif, en secondes, en spécifiant le délai d’attente hello entre chaque tentative hello.|Oui|N/A|  
|max-interval|Un nombre positif, en secondes, en spécifiant le délai d’attente maximal du hello entre chaque tentative hello. Il est tooimplement utilisé un algorithme de nouvelle tentative exponentielle.|Non|N/A|  
|delta|Un nombre positif, en secondes spécifiant l’incrément d’intervalle d’attente hello. Il s’agit des algorithmes de nouvelle tentative linéaire et exponentielle hello tooimplement utilisé.|Non|N/A|  
|first-fast-retry|Si défini trop `true` , hello première nouvelle tentative est effectuée immédiatement.|Non|`false`|  
  
> [!NOTE]
>  Lorsque uniquement hello `interval` est spécifié, **fixe** nouvelles tentatives d’intervalle sont effectuées.  
>  Lorsque uniquement hello `interval` et `delta` sont spécifiés, un **linéaire** algorithme de tentative d’intervalle est utilisé, où les temps d’attente entre deux tentatives est calculé hello en fonction de formule - suivante `interval + (count - 1)*delta`.  
>  Hello lorsque `interval`, `max-interval` et `delta` sont spécifiés, **exponentielle** algorithme de tentative d’intervalle est appliqué, où les temps d’attente hello entre les tentatives de hello augmentent de manière exponentielle à partir de la valeur hello `interval`toohello valeur `max-interval` selon toohello suivant forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Notez que des restrictions d’utilisation des stratégies enfants seront héritées par cette stratégie.  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="ReturnResponse"></a> Return response  
 Hello `return-response` stratégie interrompt l’exécution du pipeline et retourne une valeur par défaut ou un appelant toohello de réponse personnalisée. La réponse par défaut est `200 OK` sans corps. La réponse personnalisée peut être spécifiée par le biais d’instructions de stratégie ou d’une variable de contexte. Lorsque les deux sont fournis, réponse hello contenue dans la variable de contexte hello est modifié par les instructions de stratégie hello avant d’être retourné à l’appelant de toohello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Exemple  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|return-response|Élément racine.|Oui|  
|set-header|Instruction de stratégie [set-header](api-management-transformation-policies.md#SetHTTPheader).|Non|  
|set-body|Instruction de stratégie [set-body](api-management-transformation-policies.md#SetBody).|Non|  
|set-status|Instruction de stratégie [set-status](api-management-advanced-policies.md#SetStatus).|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|  
|---------------|-----------------|--------------|  
|response-variable-name|Hello nom de variable de contexte hello référencé à partir, par exemple, un en amont [demande d’envoi](api-management-advanced-policies.md#SendRequest) stratégie et contenant un `Response` objet|facultatif.|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="SendOneWayRequest"></a> Send one way request  
 Hello `send-one-way-request` stratégie envoie la demande hello fourni toohello spécifié des URL sans attendre une réponse.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Exemple  
 Cette stratégie de l’exemple montre un exemple d’utilisation hello `send-one-way-request` stratégie toosend message tooa Slack salle de conversation si hello code de réponse HTTP est supérieur ou égal too500. Pour plus d’informations sur cet exemple, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|send-one-way-request|Élément racine.|Oui|  
|url|Hello l’URL de demande de hello.|Non si mode=copy ; sinon, oui.|  
|method|méthode HTTP pour la demande de hello de Hello.|Non si mode=copy ; sinon, oui.|  
|en-tête|En-tête de demande. Utilisez un élément d’en-tête pour chaque en-tête de demande.|Non|  
|body|corps de la demande Hello.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|Détermine s’il s’agit d’une nouvelle demande ou une copie de la demande en cours de hello. En mode de sortie, mode = copie n’initialise pas le corps de la demande hello.|Non|Nouveau|  
|name|Spécifie le nom hello de hello en-tête toobe ensemble.|Oui|N/A|  
|exists-action|Spécifie quelles tootake action lorsque hello en-tête est déjà spécifié. Cet attribut doit avoir une des valeurs suivantes de hello.<br /><br /> -remplacer - valeur de hello remplace d’en-tête existant de hello.<br />-ignorer - ne remplace pas la valeur d’en-tête hello existant.<br />-Ajouter - ajoute la valeur d’en-tête existant hello valeur toohello.<br />-Supprimer - supprime les en-tête de hello de demande de hello.<br /><br /> Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans l’en-tête de hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.|Non|override|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="SendRequest"></a> Send request  
 Hello `send-request` stratégie envoie la demande hello fourni toohello spécifié l’URL, en attente n’est plus que hello définie la valeur de délai d’attente.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Exemple  
 Cet exemple montre une façon tooverify un jeton de référence avec un serveur d’autorisation. Pour plus d’informations sur cet exemple, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|send-request|Élément racine.|Oui|  
|url|Hello l’URL de demande de hello.|Non si mode=copy ; sinon, oui.|  
|method|méthode HTTP pour la demande de hello de Hello.|Non si mode=copy ; sinon, oui.|  
|en-tête|En-tête de demande. Utilisez un élément d’en-tête pour chaque en-tête de demande.|Non|  
|body|corps de la demande Hello.|Non|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|Détermine s’il s’agit d’une nouvelle demande ou une copie de la demande en cours de hello. En mode de sortie, mode = copie n’initialise pas le corps de la demande hello.|Non|Nouveau|  
|response-variable-name="string"|En son absence, `context.Response` est utilisé.|Non|N/A|  
|timeout="integer"|intervalle de délai d’attente Hello en secondes avant l’appel de hello toohello URL échoue.|Non|60|  
|ignore-error|Si la valeur true et hello demande entraîne une erreur :<br /><br /> - Si response-variable-name a été spécifié, il contiendra une valeur Null.<br />- Si response-variable-nam n’est pas spécifié, context.Request ne sera pas mis à jour.|Non|false|  
|name|Spécifie le nom hello de hello en-tête toobe ensemble.|Oui|N/A|  
|exists-action|Spécifie quelles tootake action lorsque hello en-tête est déjà spécifié. Cet attribut doit avoir une des valeurs suivantes de hello.<br /><br /> -remplacer - valeur de hello remplace d’en-tête existant de hello.<br />-ignorer - ne remplace pas la valeur d’en-tête hello existant.<br />-Ajouter - ajoute la valeur d’en-tête existant hello valeur toohello.<br />-Supprimer - supprime les en-tête de hello de demande de hello.<br /><br /> Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans l’en-tête de hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.|Non|override|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="SetHttpProxy"></a> Définir le proxy HTTP  
 Hello `proxy` stratégie vous permet de tooroute les toobackends de demandes transmises via un proxy HTTP. Seul le protocole HTTP (pas le protocole HTTPS) est prise en charge entre hello et de proxy de hello. Authentification de base et NTLM uniquement.
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Exemple  
Notez que hello [propriétés](api-management-howto-properties.md) en tant que valeurs de hello tooavoid nom d’utilisateur et mot de passe le stockage des informations sensibles dans le document de stratégie hello.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|proxy|Élément racine|Oui|  

### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|url="chaîne"|URL du proxy sous forme http://Host :port) hello.|Oui|N/A |  
|username="chaîne"|Toobe de nom d’utilisateur utilisé pour l’authentification avec le proxy hello.|Non|N/A |  
|password="chaîne"|Toobe de mot de passe utilisé pour l’authentification avec le proxy hello.|Non|N/A |  

### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound  
  
-   **Étendues de la stratégie :** toutes les étendues  

##  <a name="SetRequestMethod"></a> Set request method  
 Hello `set-method` stratégie vous permet de méthode de demande toochange hello HTTP pour une demande.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Exemple  
 Cet exemple de stratégie qui utilise hello `set-method` stratégie montre un exemple d’envoi d’une salle de conversation Slack message tooa si hello code de réponse HTTP est supérieur à ou égal too500. Pour plus d’informations sur cet exemple, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|set-method|Élément racine. valeur Hello d’élément de hello spécifie la méthode HTTP de hello.|Oui|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="SetStatus"></a> Set status code  
 Hello `set-status` stratégie jeux hello HTTP état code toohello de valeur spécifiée.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Exemple  
 Cet exemple montre comment tooreturn une réponse 401 si le jeton d’autorisation hello n’est pas valide. Pour plus d’informations, consultez [à l’aide des services externes à partir de hello service de gestion des API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|set-status|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|code="integer"|tooreturn de code de statut HTTP de Hello.|Oui|N/A|  
|reason="string"|Description du motif hello pour retourner le code d’état hello.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  

##  <a name="set-variable"></a> Set variable  
 Hello `set-variable` stratégie déclare un [contexte](api-management-policy-expressions.md#ContextVariables) variable et lui assigne une valeur spécifiée via une [expression](api-management-policy-expressions.md) ou un littéral de chaîne. Si expression de hello contient un littéral, il sera converti tooa hello et la chaîne de valeur de hello sera `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a> Instruction de la stratégie  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a> Exemple  
 exemple Hello illustre une stratégie de variable définie dans hello entrants de section. Cette stratégie de variable définie crée un `isMobile` booléenne [contexte](api-management-policy-expressions.md#ContextVariables) variable a la valeur tootrue si hello `User-Agent` demande en-tête contient le texte hello `iPad` ou `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|set-variable|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|  
|---------------|-----------------|--------------|  
|name|nom de Hello de variable de hello.|Oui|  
|value|valeur de Hello de variable de hello. Peut être une expression ou une valeur littérale.|Oui|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
###  <a name="set-variableAllowedTypes"></a> Types autorisés  
 Les expressions utilisées dans hello `set-variable` stratégie doit retourner hello les types de base suivants.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a> Trace  
 Hello `trace` stratégie ajoute une chaîne en hello [API inspecteur](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) sortie. Hello s’appliquera uniquement lorsque le traçage est déclenché, c'est-à-dire `Ocp-Apim-Trace` en-tête de demande est présent et défini trop`true` et `Ocp-Apim-Subscription-Key` en-tête de demande est présent et contient une clé valide associée au compte d’administrateur hello.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|trace|Élément racine.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|source|Visionneuse de trace toohello explicite littéral de chaîne et en spécifiant source hello de message de type hello.|Oui|N/A|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Sections de la stratégie :** inbound, outbound, backend, on-error  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
##  <a name="Wait"></a> Wait  
 Hello `wait` stratégie exécute ses stratégies enfants immédiats en parallèle et attend que tout ou une de ses toocomplete de stratégies enfants immédiats avant la fin. Hello attente stratégie peut posséder ses stratégies enfants immédiats [demande d’envoi](api-management-advanced-policies.md#SendRequest), [obtenir la valeur à partir du cache](api-management-caching-policies.md#GetFromCacheByKey), et [flux de contrôle](api-management-advanced-policies.md#choose) stratégies.  
  
### <a name="policy-statement"></a>Instruction de la stratégie  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Exemple  
 Bonjour exemple il y a deux `choose` stratégies en tant que stratégies des enfants immédiats de hello `wait` stratégie. Ces deux stratégies `choose` s’exécutent en parallèle. Chaque `choose` stratégie tente tooretrieve une valeur mise en cache. S’il existe une absence dans le cache, un service principal est tooprovide hello appelée « valeur ». Dans cette hello exemple `wait` stratégie ne se termine pas tant que toutes les stratégies de ses enfants immédiats d’effectuent, car hello `for` attribut est défini trop`all`.   Dans cette variables de contexte exemple hello (`execute-branch-one`, `value-one`, `execute-branch-two`, et `value-two`) sont déclarés en dehors de la portée de hello de cet exemple de stratégie.  
  
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
  
### <a name="elements"></a>Éléments  
  
|Élément|Description|Requis|  
|-------------|-----------------|--------------|  
|wait|Élément racine. Ne peut contenir comme éléments enfants que les stratégies `send-request`, `cache-lookup-value` et `choose`.|Oui|  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|Requis|Default|  
|---------------|-----------------|--------------|-------------|  
|for|Détermine si hello `wait` stratégie attend que tous les enfants immédiats stratégies toobe est terminée ou qu’un seul. Les valeurs autorisées sont les suivantes :<br /><br /> -   `all`-attendre toocomplete de stratégies tous les enfants immédiats<br />-any - attendre tout toocomplete de stratégie enfants immédiats. Une fois la stratégie enfant immédiat de la première hello terminée, hello `wait` stratégie se termine et l’exécution de toutes les autres stratégies enfant immédiat est terminée.|Non|tout|  
  
### <a name="usage"></a>Usage  
 Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sections de la stratégie :** inbound, outbound, backend  
  
-   **Étendues de la stratégie :** toutes les étendues  
  
## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation de stratégies, consultez les pages :
-   [Stratégies dans Gestion des API](api-management-howto-policies.md) 
-   [Expressions de stratégie](api-management-policy-expressions.md)
