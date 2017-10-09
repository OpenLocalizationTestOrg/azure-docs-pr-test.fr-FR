---
title: aaaError & exceptions - Azure Logic Apps | Documents Microsoft
description: "Modèles de gestion des erreurs et des exceptions dans Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Gérer les erreurs et les exceptions dans Azure Logic Apps

Azure Logic Apps fournit des outils et modèles toohelp vous vérifiez que votre intégrations sont solide et fiable contre les défaillances. Architecture d’intégration pose problème hello de fabrication des temps d’arrêt tooappropriately que handle ou des problèmes à partir de systèmes dépendants. Logique d’applications facilite la gestion des erreurs une expérience de première classe, ce qui vous donne hello outils tooact sur les erreurs et exceptions dans vos workflows.

## <a name="retry-policies"></a>Stratégies de nouvelle tentative

Stratégie de nouvelle tentative est de type de base de hello d’exception et la gestion des erreurs. Si une demande initiale a expiré ou a échoué (toute demande qui entraîne un 429 ou réponse 5xx), cette stratégie définit si l’action de hello doit réessayer. Par défaut, toutes les actions font l’objet de 4 tentatives supplémentaires sur des intervalles de 20 secondes. Par conséquent, si la première demande de hello reçoit un `500 Internal Server Error` réponse, le moteur de flux de travail hello s’interrompt pendant 20 secondes et tentatives hello demande à nouveau. Si après toutes les nouvelles tentatives, hello réponse est toujours une exception ou une défaillance, le flux de travail de hello continue et marques hello l’état de l’action en tant que `Failed`.

Vous pouvez configurer des stratégies de nouvelle tentative dans hello **entrées** pour une action particulière. Par exemple, vous pouvez configurer un tootry de stratégie de nouvelle tentative jusqu'à 4 fois sur des intervalles de 1 heure. Pour plus d’informations sur les propriétés d’entrée, voir [Actions et déclencheurs de flux de travail][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Si vous souhaitiez votre tooretry d’action HTTP 4 fois et que vous attendez 10 minutes entre chaque tentative, vous utiliseriez hello définition :

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

Pour plus d’informations sur la syntaxe prise en charge, consultez hello [section stratégie de nouvelle tentative dans les Actions de flux de travail et les déclencheurs][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Intercepter des échecs avec hello RunAfter propriété

Chaque action d’application logique déclare les actions que doivent se terminer avant le début d’action hello, telles que l’ordre des étapes de hello dans votre flux de travail. Dans la définition d’action hello, ce classement est connu comme hello `runAfter` propriété. Cette propriété est un objet qui décrit les actions et les États de l’action exécutent l’action de hello. Par défaut, toutes les actions sont ajoutées via hello Concepteur de logique d’application sont définies trop`runAfter` hello précédemment si hello étape précédente `Succeeded`. Toutefois, vous pouvez personnaliser cette actions toofire la valeur lorsque les actions précédentes ont `Failed`, `Skipped`, ou un ensemble possible de ces valeurs. Si vous souhaitiez tooadd un tooa élément désigné rubrique Service Bus après une action spécifique `Insert_Row` échoue, vous pouvez utiliser hello suivant `runAfter` configuration :

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

Hello d’avis `runAfter` propriété a la valeur toofire si hello `Insert_Row` action est `Failed`. action de hello toorun si l’état de l’action hello est `Succeeded`, `Failed`, ou `Skipped`, utilisez la syntaxe suivante :

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Les actions qui s’exécutent suite à l’échec d’une action précédente et qui sont correctement exécutées seront marquées comme `Succeeded`. Cela signifie que si vous avec succès toutes les défaillances dans un flux de travail, hello exécuter lui-même est marqué comme `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Actions de tooevaluate étendues et les résultats

Toohow similaires que vous pouvez exécuter après des actions individuelles, vous pouvez également regrouper actions à l’intérieur d’un [étendue](../logic-apps/logic-apps-loops-and-scopes.md), qui agissent comme un regroupement logique des actions. Les étendues sont utiles pour organiser des actions de votre logique d’application et pour effectuer des évaluations d’agrégation sur état hello d’une étendue. étendue Hello lui-même reçoit un état une fois toutes les actions dans une portée ont terminé. état de l’étendue Hello est déterminé par hello mêmes critères comme une série de tests. Si la dernière action de hello dans une branche de l’exécution est `Failed` ou `Aborted`, l’état hello est `Failed`.

toofire des actions spécifiques pour les erreurs qui se sont produits au sein de la portée de hello, vous pouvez utiliser `runAfter` avec une étendue qui est marqué comme `Failed`. Si *tout* actions dans la portée de hello échouent, en cours d’exécution après l’échec d’une étendue vous permet de vous créer un toocatch action unique échecs.

### <a name="getting-hello-context-of-failures-with-results"></a>Lors de l’obtention de contexte hello d’échecs de résultats

Bien qu’il est utile d’intercepter les défaillances d’une étendue, vous pouvez également vous toohelp de contexte que vous comprenez exactement quelles actions a échoué, et les erreurs ou les codes d’état retournés. Hello `@result()` fonction de workflow fournit le contexte relatif résultat hello de toutes les actions dans une étendue.

`@result()`prend un seul paramètre, le nom de l’étendue et retourne un tableau de tous les résultats d’action hello à partir de cette étendue. Ces objets action incluent hello même attributs sous la forme d’hello `@actions()` sort de l’objet, y compris l’heure de début d’action, heure de fin d’action, état de l’action, entrées d’action, ID de corrélation action et action. contexte toosend de toutes les actions qui ont échoué dans une étendue, vous pouvez facilement associer un `@result()` fonctionne avec un `runAfter`.

tooexecute une action *pour chaque* action dans une étendue qui `Failed`, tableau de hello de filtre de tooactions de résultats qui ont échoué, vous pouvez également associer des `@result()` avec un  **[filtre tableau](../connectors/connectors-native-query.md)**  action et un  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  boucle. Vous pouvez prendre le tableau de résultats filtré hello et effectuer une action pour chaque défaillance à l’aide de hello **ForEach** boucle. Voici un exemple, suivi d’une explication détaillée, qui envoie une demande HTTP POST avec un corps de la réponse de toutes les actions qui ont échoué hello étendue hello `My_Scope`.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

Voici un toodescribe de procédure pas à pas détaillées que se passe-t-il :

1. résultat de hello tooget de toutes les actions dans `My_Scope`, hello **filtre tableau** filtres d’action `@result('My_Scope')`.

2. Hello condition pour **filtre tableau** toute `@result()` élément ayant l’état égal trop`Failed`. Cette condition de filtre de tableau hello avec tous les résultats d’action à partir de `My_Scope` tableau tooan avec uniquement échec des résultats d’action.

3. Effectuer un **pour chaque** action sur hello **filtrée de tableau** génère. Cette étape exécute une action *pour chaque* résultat d’action ayant échoué filtré précédemment.

    En cas d’échec d’une action unique dans la portée de hello, hello actions Bonjour `foreach` n'exécuter qu’une seule fois. 
    De nombreuses actions ayant échoué peuvent provoquer une action par échec.

4. Envoyer une requête HTTP POST sur hello `foreach` élément corps de réponse, ou `@item()['outputs']['body']`. Hello `@result()` forme d’élément est de même hello comme hello `@actions()` mettre en forme et peut être analysé hello même façon.

5. Inclure les deux en-têtes personnalisés avec le nom de l’action ayant échoué hello `@item()['name']` et Échec de l’exécution de client ID de suivi hello `@item()['clientTrackingId']`.

Pour référence, Voici un exemple d’un seul `@result()` élément, montrant hello `name`, `body`, et `clientTrackingId` les propriétés qui sont analysées dans l’exemple précédent de hello. En dehors de `foreach`, `@result()` retourne un tableau de ces objets.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform la gestion des exceptions de différents modèles, vous pouvez utiliser des expressions hello indiquées précédemment. Vous pouvez choisir tooexecute une action en dehors de la portée hello qui accepte hello ensemble tableau filtré d’échecs d’exceptions unique et supprimer hello `foreach`. Vous pouvez également inclure d’autres propriétés utiles à partir de hello `@result()` réponse illustré précédemment.

## <a name="azure-diagnostics-and-telemetry"></a>Azure Diagnostics et télémétrie

Hello modèles précédents sont aisément toohandle et exceptions lors d’une exécution, mais vous pouvez également identifier et répondre tooerrors indépendant de hello exécuter lui-même. 
[Diagnostics Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fournit un moyen simple de toosend compte de stockage Azure tooan tous les flux de travail (y compris tous les États d’exécution et action) ou un concentrateur d’événements Azure. tooevaluate exécuter des États, vous pouvez surveiller les métriques et les journaux de hello, ou les publier dans n’importe quel outil de surveillance que vous préférez. Une option potentielle est toostream tous les événements hello via un concentrateur d’événements Azure dans [flux Analytique](https://azure.microsoft.com/services/stream-analytics/). Dans le flux de données Analytique, vous pouvez écrire des requêtes actives hors des anomalies, moyennes ou des défaillances de hello des journaux de diagnostic. Analytique de flux de sortie peut facilement tooother des sources de données, les files d’attente, rubriques, SQL, base de données Azure Cosmos et Power BI.

## <a name="next-steps"></a>Étapes suivantes

* [Voir comment un client conçoit la gestion des erreurs avec Azure Logic Apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Consultez d’autres exemples et scénarios Logic Apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Découvrez comment toocreate automatisé des déploiements pour logic apps](../logic-apps/logic-apps-create-deploy-template.md)
* [Créer et déployer des applications logiques avec Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
