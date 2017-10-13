---
title: Gestion des erreurs et des exceptions - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Gérer les erreurs et les exceptions dans Azure Logic Apps

Azure Logic Apps propose un ensemble complet d’outils et de modèles afin de garantir la résistance et la fiabilité de vos intégrations contre les défaillances. Toute architecture d’intégration nécessite que les temps d’arrêt et les problèmes soient gérés de manière appropriée. Logic Apps optimise la gestion des erreurs, en vous offrant les outils dont vous avez besoin pour gérer les exceptions et les erreurs qui se produisent dans vos flux de travail.

## <a name="retry-policies"></a>Stratégies de nouvelle tentative

Le type de gestion des erreurs et des exceptions le plus simple consiste à utiliser une stratégie de nouvelle tentative. Cette stratégie définit si l’action doit faire l’objet d’une nouvelle tentative en cas d’expiration ou d’échec de la demande initiale (toute demande ayant entraîné une réponse 429 ou 5xx). Par défaut, toutes les actions font l’objet de 4 tentatives supplémentaires sur des intervalles de 20 secondes. Par conséquent, si la première demande reçoit une réponse `500 Internal Server Error`, le moteur de flux de travail s’interrompt pendant 20 secondes, puis tente à nouveau d’exécuter la demande. Si à l’issue de toutes les tentatives, la réponse renvoie toujours une exception ou un échec, le flux de travail continue et marque l’état de l’action comme `Failed`.

Vous pouvez configurer des stratégies de nouvelle tentative dans les **entrées** d’une action en particulier. Une stratégie de nouvelle tentative peut par exemple être configurée pour effectuer jusqu’à 4 tentatives avec des intervalles d’1 heure. Pour plus d’informations sur les propriétés d’entrée, voir [Actions et déclencheurs de flux de travail][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Si vous voulez que votre action HTTP effectue 4 tentatives et attende 10 minutes entre chacune d’entre elles, vous devez utiliser la définition suivante :

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

Pour plus d’informations sur la syntaxe prise en charge, consultez la [section relative aux stratégies de nouvelle tentative sous Actions et déclencheurs de flux de travail][retryPolicyMSDN].

## <a name="catch-failures-with-the-runafter-property"></a>Identification des échecs avec la propriété RunAfter

Chaque action d’application logique déclare quelles actions doivent se terminer avant de démarrer une autre action, hiérarchisant ainsi les étapes de votre flux de travail. Ce classement est connu sous le nom de propriété `runAfter` dans la définition de l’action. Cette propriété est un objet qui décrit les actions et les états d’action qui exécutent l’action. Par défaut, toutes les actions ajoutées par le biais du Concepteur d’application logique sont définies avec la propriété `runAfter` par rapport à l’étape précédente, si celle-ci était `Succeeded`. Toutefois, vous pouvez personnaliser cette valeur pour déclencher des actions lorsque les actions précédentes sont `Failed`, `Skipped` ou un ensemble de valeurs possible. Si vous souhaitez ajouter un élément à une rubrique Service Bus désignée suite à l’échec d’une action spécifique `Insert_Row`, vous pouvez utiliser la configuration `runAfter` suivante :

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

Notez que la propriété `runAfter` est définie pour se déclencher si l’action `Insert_Row` est `Failed`. Pour exécuter l’action si l’état de l’action est `Succeeded`, `Failed` ou `Skipped`, utilisez cette syntaxe :

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Les actions qui s’exécutent suite à l’échec d’une action précédente et qui sont correctement exécutées seront marquées comme `Succeeded`. Ce comportement signifie que si vous avez correctement intercepté tous les échecs dans un flux de travail, l’exécution elle-même est marquée comme `Succeeded`.

## <a name="scopes-and-results-to-evaluate-actions"></a>Étendues et résultats permettant d’évaluer les actions

De la même manière que vous pouvez exécuter des actions individuelles, vous pouvez également regrouper des actions au sein d’une [étendue](../logic-apps/logic-apps-loops-and-scopes.md) qui agit comme un regroupement logique d’actions. Les étendues sont utiles pour organiser vos actions d’application logique et pour effectuer des évaluations d’agrégation sur l’état d’une étendue. L’étendue elle-même se voit attribuer un état une fois toutes les actions de l’étendue effectuées. L’état de l’étendue est déterminé avec les mêmes critères que pour une exécution. Si la dernière action dans une branche de l’exécution est `Failed` ou `Aborted`, l’état est `Failed`.

Vous pouvez utiliser la propriété `runAfter` sur une étendue qui a été marquée comme `Failed` pour déclencher des actions spécifiques en raison d’échecs survenus dans l’étendue. L’exécution suite à l’échec d’une étendue vous permet de créer une seule action pour intercepter des échecs, si *des* actions figurent dans l’étendue.

### <a name="getting-the-context-of-failures-with-results"></a>Obtention du contexte des échecs avec les résultats

Bien que l’interception des échecs d’une étendue soit très utile, vous aurez peut-être également besoin du contexte pour identifier précisément les actions qui ont échoué, ainsi que les codes d’erreur ou d’état renvoyés. La fonction de flux de travail `@result()` fournit le contexte dans le résultat de toutes les actions au sein d’une étendue.

`@result()` prend un paramètre unique, le nom de l’étendue, et renvoie un tableau de tous les résultats d’action dans cette étendue. Ces objets d’action incluent les mêmes attributs que l’objet `@actions()` , y compris l’heure de début de l’action, l’heure de fin de l’action, l’état de l’action, les entrées de l’action, les ID de corrélation d’action, ainsi que ses résultats. Vous pouvez facilement associer une fonction `@result()` avec une propriété `runAfter` pour envoyer le contexte de toutes les actions qui ont échoué dans une étendue.

Pour exécuter une action *pour chaque* action dans une étendue marquée comme `Failed`, filtrez les résultats sur les actions ayant échoué, et associez `@result()` avec une action **[Filtrer le tableau](../connectors/connectors-native-query.md)** et une boucle **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**. Vous pouvez prendre le tableau des résultats filtrés et effectuer une action pour chaque échec à l’aide de la boucle **ForEach** . Cet exemple, suivi d’une explication détaillée, envoie une demande HTTP POST avec le corps de réponse de toutes les actions qui ont échoué dans l’étendue `My_Scope`.

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

Voici la procédure détaillée pour décrire ce qui se produit :

1. Pour obtenir le résultat de toutes les actions au sein de `My_Scope`, l’action **Filtrer le tableau** permet de filtrer `@result('My_Scope')`.

2. La condition de l’action **Filtrer le tableau** est tout élément `@result()` dont l’état est égal à `Failed`. Cette condition filtre le tableau de tous les résultats d’action de `My_Scope` selon un tableau contenant uniquement les résultats d’action ayant échoué.

3. Exécution d’une action **For Each** sur les résultats du **tableau filtré**. Cette étape exécute une action *pour chaque* résultat d’action ayant échoué filtré précédemment.

    Si une action unique dans l’étendue a échoué, les actions de `foreach` s’exécutent une seule fois. 
    De nombreuses actions ayant échoué peuvent provoquer une action par échec.

4. Envoi d’une requête HTTP POST sur le corps de réponse de l’élément `foreach`, ou `@item()['outputs']['body']`. La forme de l’élément `@result()` est identique à la forme `@actions()` et peut être analysée de la même façon.

5. Deux en-têtes personnalisés avec le nom de l’action qui a échoué `@item()['name']` sont également inclus, ainsi que l’ID de suivi du client d’exécution qui a échoué `@item()['clientTrackingId']`.

Pour référence, voici un exemple d’un seul élément `@result()`, montrant le `name`, le `body`, et les propriétés `clientTrackingId` analysés dans l’exemple précédent. En dehors de `foreach`, `@result()` retourne un tableau de ces objets.

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

Vous pouvez utiliser les expressions ci-dessus pour exécuter différents modèles de gestion des exceptions. Vous pouvez choisir d’exécuter une seule action de gestion en dehors de l’étendue qui accepte l’intégralité du tableau filtré d’échecs et de supprimer `foreach`. Vous pouvez également inclure d’autres propriétés utiles à partir de la réponse `@result()` obtenue précédemment.

## <a name="azure-diagnostics-and-telemetry"></a>Azure Diagnostics et télémétrie

Les précédents modèles sont très utiles pour gérer les erreurs et les exceptions d’une exécution, mais vous pouvez également identifier les erreurs et y répondre indépendamment de l’exécution elle-même. 
[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) fournit un moyen simple d’envoyer tous les événements de flux de travail (y compris tous les états d’exécution et d’action) à un compte Azure Storage ou un concentrateur d’événements Azure. Vous pouvez surveiller les journaux et les mesures ou les publier dans n’importe quel outil de surveillance de votre choix pour évaluer les états d’exécution. Vous avez également la possibilité de transmettre tous les événements via le concentrateur d’événements Azure dans [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). Dans Stream Analytics, vous pouvez écrire des requêtes actives sans aucune anomalie, des moyennes ou des échecs dans les journaux de diagnostic. Stream Analytics peut facilement exporter ses résultats vers d’autres sources de données, telles que les files d’attente, les rubriques, SQL, Azure Cosmos DB et Power BI.

## <a name="next-steps"></a>Étapes suivantes

* [Voir comment un client conçoit la gestion des erreurs avec Azure Logic Apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Consultez d’autres exemples et scénarios Logic Apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Découvrez comment créer des déploiements automatisés pour des applications logiques](../logic-apps/logic-apps-create-deploy-template.md)
* [Créer et déployer des applications logiques avec Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
