---
title: "aaaWorkflow actions et les déclencheurs - Azure Logic Apps | Documents Microsoft"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Actions et déclencheurs de workflow pour Azure Logic Apps

Les applications logiques se composent de déclencheurs et d’actions. Il existe six types de déclencheurs. Chaque type présente une interface et un comportement différents. Vous pouvez également découvrir les autres détails en examinant les détails de hello Hello [langage de définition de flux de travail](logic-apps-workflow-definition-language.md).  
  
Lisez la suite toolearn en savoir plus sur les déclencheurs et les actions et comment vous pouvez utiliser les toobuild logique applications tooimprove votre processus d’entreprise et le flux de travail.  
  
### <a name="triggers"></a>Déclencheurs  

Un déclencheur spécifie les appels hello autorisés à initier une exécution de votre flux de travail application logique. Voici deux façons différentes de hello tooinitiate une exécution de votre flux de travail :  
  
-   Un déclencheur d’interrogation  

-   Un déclencheur d’émission - en appelant hello [API REST de Service de flux de travail](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Tous les déclencheurs contiennent ces éléments de niveau supérieur :  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Types de déclencheurs et entrées associées  

Vous pouvez utiliser les types de déclencheurs suivants :
  
-   **Demande** \- rend application logique de hello un point de terminaison pour vous toocall  
  
-   **Recurrence** \- Se déclenche selon une planification définie.  
  
-   **HTTP**\- Interroge un point de terminaison web HTTP. point de terminaison Hello HTTP doit respecter le contrat de déclenchement spécifique tooa \- à l’aide d’un message 202\-un modèle asynchrone, ou en retournant un tableau  
  
-   **ApiConnection** \- interroge comme hello HTTP déclenche, toutefois, elle tire parti de hello [gérée par Microsoft des API](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- ouvre un point de terminaison, similaire toohello déclencheur manuel, toutefois, il appelle également out tooa spécifié URL tooregister et annuler l’inscription  
  
-   **ApiConnectionWebhook** \- fonctionne comme hello HTTPWebhook déclencheur en tirant parti de hello gérée par Microsoft des API       
    Chaque type de déclencheur présente un ensemble différent d’**entrées** qui définissent son comportement.  
  
## <a name="request-trigger"></a>Déclencheur de requête  

Ce déclencheur sert un point de terminaison que vous appelez votre application logique via un tooinvoke de requête HTTP. Un déclencheur request se présente comme dans cet exemple :  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Il existe également une propriété facultative appelée **schema** :  
  
|Nom de l'élément|Requis|Description|  
|----------------|------------|---------------|  
|schema|Non|Un schéma JSON qui valide la demande entrante de hello. Utile pour aider les étapes du flux de travail suivant savoir quels tooreference de propriétés.|

tooinvoke ce point de terminaison, vous devez toocall hello *listCallbackUrl* API. Consultez [API REST du service de workflow](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Déclencheur recurrence  

Un déclencheur recurrence s’exécute selon une planification définie. Ce type de déclencheur peut se présenter comme dans cet exemple :  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Comme vous pouvez le voir, il s’agit d’un moyen simple de toorun un flux de travail.  
  
|Nom de l'élément|Requis|Description|  
|----------------|------------|---------------|  
|frequency|Oui|La fréquence à laquelle hello déclencheur s’exécute. Utilisez une seule de ces valeurs possibles : second (seconde), minute, hour (heure), day (jour), week (semaine), month (mois) ou year (année).|  
|interval|Oui|Intervalle de hello attribué à la fréquence de récurrence de hello|  
|startTime|Non|Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire (timeZone) est utilisé.|  
|timeZone|no|Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire (timeZone) est utilisé.|  
  
Vous pouvez également programmer le déclencheur toostart l’exécution à un moment donné dans hello futures. Par exemple, si vous souhaitez toostart hebdomadaire signaler tous les lundis vous pouvez planifier hello logique application toostart tous les lundis en créant hello suivant déclencheur :  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>Déclencheur HTTP  

Les déclencheurs HTTP interrogent un point de terminaison spécifié et vérifiez hello réponse toodetermine si le flux de travail hello doit être exécutée. objet d’entrées Hello prend ensemble hello de tooconstruct de paramètres requis un appel HTTP :  
  
|Nom de l'élément|Requis|Description|Type|  
|----------------|------------|---------------|--------|  
|method|yes|Peut s’agir de hello suivant les méthodes HTTP : GET, POST, PUT, HEAD, PATCH ou DELETE|String|  
|URI|yes|Bonjour le point de terminaison http ou https est appelé. La longueur maximale est de 2 Ko.|String|  
|queries|Non|Objet représentant l’URL toohello tooadd de paramètres de requête hello. Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.|Object|  
|headers|Non|Objet représentant chacun des en-tête de hello toohello demande est envoyée. Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Object|  
|body|Non|Objet représentant la charge utile hello envoyé toohello le point de terminaison.|Object|  
|retryPolicy|Non|Objet qui vous permet de personnaliser le comportement des nouvelles tentatives hello pour les erreurs 4xx ou 5xx.|Object|  
|authentication|Non|Méthode hello représente hello demande doit être authentifié. Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). En plus de Scheduler, une autre propriété est prise en charge : `authority`. Par défaut, cette propriété est définie sur `https://login.windows.net` lorsqu’aucune valeur n’est spécifiée, mais vous pouvez utiliser une autre audience comme `https://login.windows\-ppe.net`.|Object|  
  
déclencheur HTTP Hello nécessite tooconform d’API HTTP hello avec un toowork de modèle spécifique avec votre application logique. Il requiert hello champs qui suivent :  
  
|Réponse|Description|  
|------------|---------------|  
|Code d’état|Code d’état 200 \(OK\) toocause une série de tests. Les autres codes d’état ne déclenchent pas d’exécution.|  
|En-tête Retry\-After|Nombre de secondes jusqu'à ce que l’application logique de hello interroge le point de terminaison hello à nouveau.|  
|En-tête Location|Bonjour toocall d’URL sur le prochain intervalle d’interrogation de hello. Si non spécifié, l’URL d’origine de hello est utilisé.|  
  
Voici quelques exemples de comportements différents pour les différents types de requêtes :  
  
|Response code|Retry\-After|Comportement|  
|-----------------|----------------|------------|  
|200|\(Aucune\)|N’est pas un déclencheur valid, nouvelle tentative\-After est moteur de hello requis, ou bien jamais interroge la prochaine demande de hello.|  
|202|60|Ne déclenchent pas de flux de travail hello. tentative de Hello suivante se produit dans une minute.|  
|200|10|Exécuter les flux de travail hello et vérifiez de nouveau pour le contenu de plus de 10 secondes.|  
|400|\(Aucune\)|Demande incorrecte, ne pas exécuter les flux de travail hello. S’il existe aucune **stratégie de nouvelle tentative** défini, la stratégie par défaut de hello est utilisée. Une fois le nombre de hello de tentatives a été atteint, le déclencheur de hello n’est plus valide.|  
|500|\(Aucune\)|Erreur de serveur, n’exécutez ne pas le flux de travail hello.  S’il existe aucune **stratégie de nouvelle tentative** défini, la stratégie par défaut de hello est utilisée. Une fois le nombre de hello de tentatives a été atteint, le déclencheur de hello n’est plus valide.|  
  
sorties Hello d’un déclencheur HTTP ressemblent à cet exemple :  
  
|Nom de l'élément|Description|Type|  
|----------------|---------------|--------|  
|headers|en-têtes de réponse http de hello de Hello.|Object|  
|body|corps de réponse http de hello de Hello.|Object|  
  
## <a name="api-connection-trigger"></a>Déclencheur ApiConnection  

déclencheur de connexion API Hello est similaire HTTP défini toohello dans ses fonctionnalités de base. Toutefois, les paramètres hello pour identifier l’action de hello sont différents. Voici un exemple :  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Nom de l'élément|Requis|Type|Description|  
|----------------|------------|--------|---------------|  
|host|Oui||Hello ApiApp hébergé passerelle et l’id.|  
|method|Oui|String|Peut s’agir de hello suivant les méthodes HTTP : **obtenir**, **POST**, **PUT**, **supprimer**, **correctif**, ou  **HEAD**|  
|queries|Non|Object|Toobe de paramètres de requête de hello représente ajouté toohello URL. Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.|  
|headers|Non|Object|Représente chacun des en-tête de hello toohello demande est envoyée. Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Non|Object|Représente la charge utile hello envoyé toohello le point de terminaison.|  
|retryPolicy|Non|Object|Vous permet de comportement des nouvelles tentatives toocustomize hello pour les erreurs 4xx ou 5xx.|  
|authentication|Non|Object|Méthode hello représente hello demande doit être authentifié. Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).|  
  
propriétés Hello pour l’hôte sont :  
  
|Nom de l'élément|Requis|Description|  
|----------------|------------|---------------|  
|api runtimeUrl|Oui|point de terminaison Hello Hello les API managée.|  
|connection name||Un paramètre de tooa de référence doit être appelé `$connection` et nom hello de connexion hello géré API hello utilise des flux de travail.|
  
Hello les sorties d’un déclencheur de connexion d’API sont :
  
|Nom de l'élément|Type|Description|  
|----------------|--------|---------------|  
|headers|Object|en-têtes de réponse http de hello de Hello.|  
|body|Object|corps de réponse http de hello de Hello.|  
  
## <a name="httpwebhook-trigger"></a>Déclencheur HTTPWebhook  

s’ouvre déclencheur Hello HTTPWebhook un point de terminaison, déclencheur manuel des toohello similaire, mais hello HTTPWebhook déclencheur appelle également tooa spécifié URL tooregister et annuler l’inscription. Un déclencheur HTTPWebhook peut se présenter comme dans cet exemple :  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

La plupart de ces sections sont facultatifs et comportement de hello Hello Webhook varie selon les sections fournies ou omises.  
propriétés de Hello d’un Webhook sont les suivantes :  
  
|Nom de l'élément|Requis|Description|  
|----------------|------------|---------------|  
|subscribe|Non|Hello sortant demande qui est appelée lorsque le déclencheur de hello est créé et effectue l’inscription initiale de hello.|  
|unsubscribe|Non|Hello sortant demande lorsque hello déclencheur est supprimé.|  
  
-   **S’abonner** hello sortant appel qui a effectué les tooevents écoute toostart. Cet appel commence par hello faire de même jeu de paramètres qui hello normales actions HTTP. Cet appel sortant est effectué hello de n’importe quel moment les modifications de workflow en aucune façon, par exemple, chaque fois que les informations d’identification de hello sont annulées ou modification des paramètres d’entrée de déclencheur de hello.
  
    toosupport cet appel, il existe une nouvelle fonction : `@listCallbackUrl()`. Cette fonction renvoie une URL unique pour ce déclencheur spécifique dans ce workflow. Il représente identificateur unique de hello pour les points de terminaison hello utilisant hello Service REST.  
  
-   **unsubscribe** est appelé lorsqu’une opération rend ce déclencheur non valide, notamment dans les cas suivants :  
  
    -   Supprimer ou désactiver le déclencheur de hello  
  
    -   Supprimez ou désactivez le flux de travail hello  
  
    -   Supprimez ou désactivez les abonnement hello  
  
    application de la logique de Hello appelle automatiquement hello vous désabonner d’action. paramètres Hello toothis fonction sont même hello en tant que déclencheur HTTP hello.  
  
    Hello sorties du déclencheur de HTTPWebhook hello sont contenu hello de demande entrante de hello :  
  
|Nom de l'élément|Type|Description|  
|-----------------|--------|---------------|  
|headers|Object|en-têtes de requête http de hello de Hello.|  
|body|Object|corps Hello de requête http de hello.|  

Limites lors d’une action de webhook peuvent être spécifiés dans hello comme [limites asynchrone HTTP](#asynchronous-limits).
  

## <a name="conditions"></a>Conditions  

Pour n’importe quel déclencheur, vous pouvez utiliser un ou plusieurs toodetermine de conditions si le flux de travail hello doit s’exécuter ou non. Par exemple :  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Dans ce cas, hello seuls les déclencheurs rapport lors du flux de travail hello `sendReports` paramètre a la valeur tootrue. Enfin, conditions peuvent faire référence de code d’état hello du déclencheur de hello. Par exemple, vous pouvez lancer un workflow uniquement lorsque votre site web renvoie un code d’état 500, comme suit :
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Lorsque n’importe quelle expression fait référence au code d’état hello du déclencheur de hello \(en aucune façon\), hello le comportement par défaut \(déclencheur uniquement sur 200 \(OK\) \) est remplacé. Par exemple, si vous souhaitez tootrigger sur le code d’état 200 et code d’état 201, vous avez tooinclude : `@or(equals(triggers().code, 200),equals(triggers().code,201))` comme condition.  
  
## <a name="start-multiple-runs-for-a-request"></a>Démarrer plusieurs exécutions pour une requête

tookick off pour une demande unique, plusieurs séries de `splitOn` est utile, par exemple, lorsque vous souhaitez toopoll un point de terminaison qui peut avoir plusieurs nouveaux éléments entre les intervalles d’interrogation.
  
Avec `splitOn`, vous spécifiez la propriété hello au sein de la charge utile de réponse hello qui contient le tableau hello d’éléments, chacun d’eux toouse toostart une exécution du déclencheur de hello. Par exemple, imaginez qu'une API qui renvoie hello suivant la réponse :  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
Votre application logique doit uniquement le contenu de lignes hello, donc vous pouvez construire votre déclencheur à l’exemple suivant :  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Ensuite, dans la définition de flux de travail hello `@triggerBody().name` retourne `mycoolrow` pour hello première exécution, et `another row` pour la deuxième exécution de hello. Hello déclencheur sorties ressemble cet exemple :  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Par conséquent, si vous utilisez `SplitOn`, vous ne pouvez pas obtenir les propriétés de hello situés en dehors de tableau de hello, dans ce cas, hello `Status` champ.  
  
> [!NOTE]  
> Dans cet exemple, nous utilisons hello `?` tooavoid en mesure d’opérateur toobe un échec si hello `Rows` propriété n’est pas présente. 
  
## <a name="single-run-instance"></a>Instance d’exécution unique

Vous pouvez configurer les déclencheurs qui ont un incendie tooonly de propriété périodicité si toutes les exécutions actives s’est terminé. Si une périodicité planifiée se produit alors qu’il est en cours d’exécution, déclencheur de hello ignore et attend jusqu'à hello suivant périodicité planifiée intervalle toocheck à nouveau.

Vous pouvez configurer ce paramètre via les options d’opération hello :

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Types et entrées  

Il existe de nombreux types d’actions, chacune présentant un comportement unique. Les actions de collection peuvent contenir de nombreuses autres actions.

### <a name="standard-actions"></a>Actions standard  

-   **HTTP** - Cette action appelle un point de terminaison web HTTP.  
  
-   **ApiConnection** \- cette action se comporte comme hello action HTTP, mais il utilise hello gérée par Microsoft des API.  
  
-   **ApiConnectionWebhook** \- comme HTTPWebhook, mais utilise hello gérée par Microsoft des API.  
  
-   **Response** \- Cette action définit une réponse pour un appel entrant.  
  
-   **Wait** \- Cette action simple déclenche une attente pendant une durée définie ou jusqu’à un moment spécifique.  
  
-   **Workflow** \- Cette action représente un workflow imbriqué.  

-   **Function**\- Cette action représente une fonction d’Azure.

### <a name="collection-actions"></a>Actions de collection

-   **Scope** \- Cette action est un regroupement logique d’autres actions.

-   **Condition** \- cette action évalue une expression et exécute la branche de résultat hello correspondante.

-   **ForEach** \- Cette action en boucle effectue une itération dans un tableau et exécute des actions internes pour chaque élément.

-   **Jusqu'à ce que** \- cette action en boucle exécute les actions internes jusqu'à ce qu’une condition entraîne tootrue.
  
Chaque type d’action présente un ensemble différent d’**entrées** qui définissent le comportement d’une action.  
  
## <a name="http-action"></a>Action HTTP  

Actions HTTP appellent un point de terminaison spécifié et vérifiez hello réponse toodetermine si le flux de travail hello doit s’exécuter. Hello **entrées** objet prend ensemble hello de paramètres requis tooconstruct hello HTTP appel :  
  
|Nom de l'élément|Requis|Type|Description|  
|----------------|------------|--------|---------------|  
|method|Oui|String|Peut s’agir de hello suivant les méthodes HTTP : **obtenir**, **POST**, **PUT**, **supprimer**, **correctif**, ou  **HEAD**|  
|URI|Oui|String|Bonjour le point de terminaison http ou https est appelé. La longueur maximale est de 2 Ko.|  
|queries|Non|Object|Représente l’URL toohello tooadd de paramètres de requête hello. Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.|  
|headers|Non|Object|Représente chacun des en-tête de hello toohello demande est envoyée. Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Non|Object|Représente la charge utile hello envoyé toohello le point de terminaison.|  
|retryPolicy|Non|Object|Vous permet de personnaliser le comportement des nouvelles tentatives hello pour les erreurs 4xx ou 5xx.|  
|operationsOptions|Non|String|Définit un jeu hello de comportements spéciaux toooverride.|  
|authentication|Non|Object|Méthode hello représente hello demande doit être authentifié. Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). En plus de Scheduler, une autre propriété est prise en charge : `authority`. Par défaut, cette propriété est définie sur `https://login.windows.net` lorsqu’aucune valeur n’est spécifiée, mais vous pouvez utiliser une autre audience comme `https://login.windows\-ppe.net`|  
  
Les actions HTTP \(et ApiConnection\) prennent en charge les stratégies de nouvelle tentative. Stratégie de nouvelle tentative s’applique à des échecs de toointermittent, caractérisées en tant que l’état HTTP 408 429 et 5xx, exceptions de connectivité tooany Ajout des codes. Cette stratégie est décrit à l’aide de hello *retryPolicy* objet défini comme indiqué ici :
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
intervalle avant nouvelle tentative de Hello est spécifié au format de hello ISO 8601. Cet intervalle a une valeur par défaut et la valeur minimale de 20 secondes, alors que la valeur maximale de hello est d’une heure. nombre de tentatives par défaut et maximale Hello correspond à quatre heures. Si la définition de stratégie de nouvelle tentative hello n’est pas spécifiée, un `fixed` stratégie est utilisée avec les valeurs de compteur et d’intervalle de nouvelle tentative par défaut. stratégie de nouvelle tentative toodisable hello, définissez son type trop`None`.  
  
Par exemple, hello action suivante effectue une nouvelle tentative extraction actualité hello deux fois, s’il existe des défaillances intermittentes, pour un total de trois exécutions, avec un délai de 30 secondes entre chaque tentative :  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Modèles asynchrones

Par défaut, toutes les actions basées sur HTTP prend en charge le modèle d’opération asynchrone standard hello. Donc si le serveur distant de hello indique cette demande hello est accepté pour traitement avec un message 202 \(accepté\) réponse, moteur de Logic Apps hello conserve l’interrogation des URL de hello spécifiée dans l’en-tête d’emplacement de la réponse hello jusqu'à atteindre un terminal état \(pas\-réponse 202\).  
  
comportement asynchrone de hello toodisable précédemment décrit, définie un `DisableAsyncPattern` option dans les entrées d’action hello. Dans ce cas, sortie hello d’action de hello est basée sur hello initiale 202 réponse hello serveur.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Limites asynchrones

Un modèle asynchrone peut être limité dans son intervalle de temps spécifique tooa durée.  Si l’intervalle de temps hello s’écoule sans atteindre un état terminal, état hello d’action de hello est marquée `Cancelled` avec un code `ActionTimedOut`.  délai d’expiration de la limite Hello est spécifié au format ISO 8601.  Les limites peuvent être spécifiées avec la syntaxe de hello :

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>ApiConnection  

ApiConnection est une action qui fait référence à un connecteur géré par Microsoft.
Cette action nécessite une connexion valide au tooa de référence et des informations sur hello API et les paramètres requis.

|Nom de l'élément|Requis|Type|Description|  
|----------------|------------|--------|---------------|  
|host|Oui|Object|Représente les informations de connecteur hello comme objet de connexion toohello runtimeUrl et référence des hello|
|method|Oui|String|Peut s’agir de hello suivant les méthodes HTTP : **obtenir**, **POST**, **PUT**, **supprimer**, **correctif**, ou  **HEAD**|  
|path|Oui|String|chemin d’accès de Hello d’opération de hello API.|  
|queries|Non|Object|Représente l’URL toohello tooadd de paramètres de requête hello. Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.|  
|headers|Non|Object|Représente chacun des en-tête de hello toohello demande est envoyée. Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Non|Object|Représente la charge utile hello envoyé toohello le point de terminaison.|  
|retryPolicy|Non|Object|Vous permet de personnaliser le comportement des nouvelles tentatives hello pour les erreurs 4xx ou 5xx.|  
|operationsOptions|Non|String|Définit un jeu hello de comportements spéciaux toooverride.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>Action ApiConnectionWebhook

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Limites lors d’une action de webhook peuvent être spécifiés dans hello comme [limites asynchrone HTTP](#asynchronous-limits).
  
## <a name="response-action"></a>Action de réponse  

Ce type d’action contient hello charge utile de réponse entière à partir d’une requête HTTP et inclut un statusCode, corps et en-têtes :  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
action de réponse Hello présente des restrictions spéciales qui ne s’appliquent pas tooother actions. Plus précisément :  
  
-   Actions de réponse ne peut pas être parallèles dans une définition, car une demande entrante de réponse déterministe toohello est nécessaire.  
  
-   Si une action de réponse est atteinte après la demande entrante de hello a reçu une réponse, action de hello est considéré comme défectueux \(conflit\), et par conséquent, hello exécuter `Failed`.  
  
-   Un workflow comportant des actions response ne peut pas avoir `splitOn` dans son déclencheur, car un seul appel entraîne de nombreuses exécutions. Par conséquent, il doit être validé lorsque le flux de hello est PUT et cause une erreur demande incorrecte.  
  
## <a name="wait-action"></a>Action wait  

Hello `wait` action interrompt l’exécution de flux de travail pour l’intervalle de salutation spécifié. Par exemple, toowait 15 minutes, vous pouvez utiliser cet extrait de code :  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
Vous pouvez également toowait jusqu'à un moment précis, vous pouvez utiliser cet exemple :  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> durée d’attente Hello peut soit être spécifiée à l’aide de hello **intervalle** objet ou hello **jusqu'à ce que** objet, mais pas les deux.  
  
|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|interval|Non|Object|durée, en fonction de la quantité de temps d’attente de Hello.|  
|interval unit|Oui|String|Un de ces intervalles : second (seconde), minute (minute), hour (heure), day (jour), week (semaine), month (mois), year (année).|  
|interval count|Oui|String|Durée en fonction des hello donné d’unité interne.|  
|until|Non|Object|durée basée sur un point dans le temps d’attente de Hello.|  
|until timestamp|Oui|String|Chaîne &#124; hello un point dans le temps au format UTC lorsque hello attente arrive à expiration.|  

## <a name="query-action"></a>Action de requête

Hello `query` action vous permet de filtrer un tableau en fonction d’une condition. Par exemple, les numéros de tooselect supérieures à 2, vous pouvez utiliser :

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Hello sortie de hello `query` action est un tableau qui contient des éléments qui satisfont la condition de hello hello tableau d’entrée.

> [!NOTE]
> Si aucune valeur ne satisfaire hello `where` de condition, hello résultat est un tableau vide.

|Nom|Requis|Type|Description|
|--------|------------|--------|---------------|
|from|Oui|Tableau|tableau de source de Hello.|
|où|Oui|String|Hello condition tooapply tooeach élément du tableau source de hello.|

## <a name="select-action"></a>Action select

Hello `select` action vous permet de projeter de chaque élément d’un tableau dans une nouvelle valeur.
Par exemple, tooconvert un tableau de nombres dans un tableau d’objets, vous pouvez utiliser :

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Hello sortie Hello `select` action est un tableau ayant hello même cardinalité comme hello du tableau d’entrée, chaque élément transformé comme définie par hello `select` propriété. Si l’entrée de hello est un tableau vide, hello sortie est également un tableau vide.

|Nom|Requis|Type|Description|
|--------|------------|--------|---------------|
|from|Oui|Tableau|tableau de source de Hello.|
|select|Oui|Quelconque|Hello projection tooapply tooeach élément du tableau source de hello.|

## <a name="terminate-action"></a>Action terminate

Hello Terminate action arrête l’exécution du workflow hello exécuter, abandon de toutes les actions en cours et en ignorant les actions restantes. Par exemple, tooterminate une exécution avec l’état **n’a pas pu**, vous pouvez utiliser hello suivant extrait de code :

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Déjà effectuées des actions ne sont pas affectées par hello terminer l’action.

|Nom|Requis|Type|Description|
|--------|------------|--------|---------------|
|runStatus|Oui|String|cible de Hello statut d’exécution. Peut être défini sur **Failed** (Échec) ou **Cancelled** (Annulée).|
|runError|Non|Object|Détails de l’erreur Hello. Uniquement pris en charge lorsque **runStatus** est défini trop**n’a pas pu**.|
|runError code|Non|String|Hello d’exécuter le code d’erreur.|
|runError message|Non|String|Hello exécuter le message d’erreur.|

## <a name="compose-action"></a>Action compose

Hello message action vous permet de construire un objet arbitraire. sortie Hello Hello composer action hello ne résulte de l’évaluation de ses entrées. Par exemple, vous pouvez utiliser hello composer des sorties de toomerge d’action de plusieurs actions :

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Hello **composition** action peut être utilisé tooconstruct de sortie, y compris les objets, tableaux et tout autre type de prise en charge par la logique des applications telles que XML et binaire.

## <a name="table-action"></a>Action table

Hello `table` vous permet de tooconvert un tableau d’éléments dans un **CSV** ou **HTML** table.

Supposons que @triggerBody() est

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

Et vous permettent d’être défini en tant qu’action de hello

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Hello ci-dessus se produirait

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>pommes</td></tr><tr><td>1</td><td>oranges</td></tr></tbody></table>"

Dans la table de commande toocustomize hello, vous pouvez spécifier explicitement les colonnes de hello. Par exemple :

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

Hello ci-dessus se produirait

<table><thead><tr><th>produce id</th><th>Description</th></tr></thead><tbody><tr><td>0</td><td>pommes fraîches</td></tr><tr><td>1</td><td>oranges fraîches</td></tr></tbody></table>"

Si hello `from` valeur de propriété est un tableau vide, la sortie de hello est une table vide.

|Nom|Requis|Type|Description|
|--------|------------|--------|---------------|
|from|Oui|Tableau|tableau de source de Hello.|
|format|Oui|String|Hello format, soit **CSV** ou **HTML**.|
|colonnes|Non|Tableau|colonnes de Hello. Permet la forme de valeur par défaut toooverride hello de table de hello.|
|column header|Non|String|en-tête de colonne de hello de Hello.|
|column value|Oui|String|valeur de Hello de colonne de hello.|

## <a name="workflow-action"></a>Action workflow   

|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|host id|Oui|String|ID de ressource Hello du flux de travail hello que vous souhaitez toocall.|  
|host triggerName|Oui|String|nom de Hello du déclencheur hello que vous souhaitez tooinvoke.|  
|queries|Non|Object|Représente l’URL toohello tooadd de paramètres de requête hello. Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.|  
|headers|Non|Object|Représente chacun des en-tête de hello toohello demande est envoyée. Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|Non|Object|Représente la charge utile hello toohello le point de terminaison.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Une vérification d’accès est effectuée sur le flux de travail hello \(plus spécifiquement, les déclencheurs hello\), ce qui signifie que vous devez accéder toohello le flux de travail.  
  
Hello sorties de hello `workflow` action sont basées sur ce que vous avez définies dans hello `response` action dans le flux de travail enfant hello. Si vous n’avez pas défini un `response` action, puis hello sorties sont vides.  

## <a name="function-action"></a>Action function   

|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|function id|Oui|String|ID de la fonction hello que vous souhaitez tooinvoke Hello ressources.|  
|method|Non|String|Hello méthode HTTP utilisée (fonction) hello tooinvoke. Par défaut, a la valeur `POST` lorsqu’elle n’est pas spécifiée.|  
|queries|Non|Object|Représente l’URL toohello tooadd de paramètres de requête hello. Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.|  
|headers|Non|Object|Représente chacun des en-tête de hello toohello demande est envoyée. Par exemple, langage de hello tooset et le type dans une demande : `"headers" : { "Accept-Language": "en-us" }`.|  
|body|Non|Object|Représente la charge utile hello toohello le point de terminaison.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Lorsque vous enregistrez application logique de hello, nous effectuer des vérifications de la fonction hello référencé :
-   Vous devez toohave toohello access (fonction).
-   Seuls le déclencheur HTTP standard ou un déclencheur webhook JSON générique sont autorisés.
-   Aucune route ne doit être définie.
-   Seuls les niveaux d’autorisation « fonction » et « anonyme » sont autorisés.

URL du déclencheur Hello est récupéré, mis en cache et utilisé lors de l’exécution. Par conséquent, si une opération invalide les URL hello mis en cache, action de hello échoue lors de l’exécution. toowork résoudre ce problème, enregistrez hello application logique, ce qui entraîne la logique application tooretrieve et mettre en cache des URL du déclencheur hello à nouveau.

## <a name="collection-actions-scopes-and-loops"></a>Actions de collection (étendues et boucles)

Certains types d’actions peuvent contenir d’autres actions. Actions de référence dans une collection peuvent être référencées directement en dehors de la collection de hello. Si vous avez défini `http` dans une étendue (scope), `@body('http')` est toujours valide n’importe où dans un workflow. Les actions au sein d’une collection peuvent `runAfter` uniquement d’autres actions dans hello même collection.

## <a name="scope-action"></a>Action scope

Hello `scope` action vous permet de logiquement regrouper les actions d’un flux de travail.

|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|actions|Oui|Object|Tooexecute actions interne étendue hello|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>Action foreach

Cette action en boucle effectue une itération dans un tableau et exécute des actions internes pour chaque élément. Par défaut, la boucle foreach de hello exécutée en parallèle (20 exécutions en parallèle à la fois). Vous pouvez définir des règles de l’exécution à l’aide de hello `operationOptions` paramètre.

|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|actions|Oui|Object|Tooexecute actions interne au sein de la boucle de hello|
|foreach|Oui|string|tooiterate de tableau Hello sur|
|operationOptions|no|string|Toutes les options d’opération pour le comportement. Actuellement prend uniquement en charge `sequential` tooexecute itérations séquentiellement (comportement par défaut est parallèle)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Action until

Cette action en boucle exécute les actions internes jusqu'à ce qu’une condition entraîne tootrue.

|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|actions|Oui|Object|Tooexecute actions interne au sein de la boucle de hello|
|expression|Oui|string|Hello expression tooevaluate après chaque itération|
|limit|yes|Object|limites de Hello pour boucle hello - au moins une limite doivent être définis.|
|count|no|int|Hello limiter toohello le nombre d’itérations qui peuvent être effectuées.|
|timeout|no|string|Bonjour délai d’expiration de la durée pendant laquelle il doit effectuer une boucle.  Format ISO 8601|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Conditions : action If

Hello `If` action vous permet d’évaluer une condition et d’exécuter une branche en fonction de si hello expression prend la valeur trop`true`.

|Nom|Requis|Type|Description|  
|--------|------------|--------|---------------|  
|actions|Oui|Object|Actions interne tooexecute lorsque l’expression renvoie la valeur trop`true`|
|expression|Oui|string|Hello expression tooevaluate|
|else|no|Object|Actions interne tooexecute lorsque l’expression renvoie la valeur trop`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Hello tableau suivant présente des exemples de conditions d’utilisation des expressions dans une action :  
  
|Valeur JSON|Résultat|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Toute valeur qui est évalué tootrue entraîne toopass de cette condition. Seules les expressions booléennes sont prises en charge. tooconvert autres types tooBoolean, utiliser des fonctions `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Les fonctions de comparaison sont prises en charge. Par exemple hello ici, action de hello s’exécute uniquement lors de la sortie de hello d’act1 est supérieure au seuil de hello.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Fonctions logiques sont également pris en charge toocreate imbriqués expressions booléennes. Dans ce cas, hello action est exécutée lors de la sortie de hello d’act1 est au-dessus du seuil de hello ou inférieure à 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Vous pouvez utiliser toocheck des fonctions de tableau si un tableau possède des éléments. Dans ce cas, hello action est exécutée lorsque hello erreurs tableau est vide.| 
|`"expression": "parameters('hasSpecialAction')"`|Erreur : cette condition n’est pas valide, car @ est requis pour les conditions.|  
  
Si une condition a la valeur avec succès, la condition de hello est marquée comme `Succeeded`. Actions dans soit hello `actions` ou `else` objets évaluent trop`Succeeded` lors de l’exécution et a réussi, `Failed` lorsque exécutée et a échoué, ou `Skipped` lorsque cette branche n’est pas exécutée.

## <a name="next-steps"></a>Étapes suivantes

[API REST du service de workflow](https://docs.microsoft.com/rest/api/logic/workflows)
