---
title: "aaaCreate boucles et des étendues ou debatch des données dans le flux de travail - Azure Logic Apps | Documents Microsoft"
description: "Créer tooiterate boucles dans les données, les actions de groupe dans les étendues, ou debatch toostart de données de plusieurs flux de travail dans Azure Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>Boucles, étendues et décomposition dans Logic Apps
  
Logique d’applications fournit un certain nombre de toowork manières avec les tableaux, les collections, les lots et les boucles au sein d’un flux de travail.
  
## <a name="foreach-loop-and-arrays"></a>Boucle ForEach et tableaux
  
Logique d’applications vous permet de tooloop sur un jeu de données et effectuer une action pour chaque élément.  Cela est possible via hello `foreach` action.  Dans le Concepteur de hello, vous pouvez spécifier tooadd une boucle for each.  Après avoir sélectionné le tableau hello sur que vous souhaitez tooiterate, vous pouvez commencer l’ajout d’actions.  Actuellement, vous êtes limité tooonly une action par boucle foreach, mais cette restriction sera levée Bonjour semaines à venir.  Une fois au sein de la boucle de hello, vous pouvez commencer toospecify ce qui doit se produire à chaque valeur du tableau de hello.

Si vous utilisez le mode code, vous pouvez spécifier une boucle foreach comme ci-dessous.  Dans cet exemple, une boucle foreach envoie un e-mail à chaque adresse contenant « microsoft.com » :

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
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
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  A `foreach` action peut itérer sur des tableaux de too5, 000 lignes.  Chaque itération s’exécute en parallèle par défaut.  

### <a name="sequential-foreach-loops"></a>Boucles ForEach séquentielles

tooenable un tooexecute de boucle foreach de manière séquentielle, hello `Sequential` option de l’opération doit être ajoutée.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Boucle Until
  
  Vous pouvez effectuer une action ou une série d’actions jusqu’à ce qu’une condition soit remplie.  Hello pour ce scénario le plus courant appelle un point de terminaison jusqu'à ce que vous obtenez la réponse hello souhaité.  Dans le Concepteur de hello, vous pouvez spécifier tooadd une boucle.  Après avoir ajouté les actions à l’intérieur de la boucle de hello, vous pouvez définir la condition de sortie hello, ainsi hello des limites de la boucle.  Il existe un délai de 1 minute entre les cycles de la boucle.
  
  Si vous utilisez le mode code, vous pouvez spécifier une boucle until comme ci-dessous.  Il s’agit d’un exemple d’appel d’un point de terminaison HTTP jusqu'à ce que le corps de la réponse hello a la valeur de hello 'Terminé'.  La procédure se termine quand l’une des conditions suivantes est remplie : 
  
  * L’état de la réponse HTTP est « Completed ».
  * La procédure a duré 1 heure.
  * Elle a effectué 100 cycles de boucle.
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn et décomposition

Parfois, un déclencheur peut s’afficher un tableau d’éléments que vous souhaitez toodebatch et démarrez un flux de travail par article.  Cela peut être effectuée via hello `spliton` commande.  Par défaut, si votre swagger de déclencheur spécifie une charge utile qui est un tableau, un `spliton` est ajouté et lance une exécution par élément.  Tooa déclencheur peut uniquement être ajouté à SplitOn.  Ce paramétrage peut être configuré ou remplacé manuellement dans la définition en mode code.  Actuellement SplitOn pouvez debatch tableaux des too5, 000 éléments.  Vous ne pouvez avoir un `spliton` et également implémenter le modèle de réponse synchrone hello.  Les flux de travail appelée qui a un `response` action en outre trop`spliton` sera exécuté de façon asynchrone et d’envoi immédiat `202 Accepted` réponse.  

SplitOn peut être spécifié dans la vue de code comme hello l’exemple suivant.  Dans cet exemple, un tableau d’éléments est reçu et chacune de ses lignes fait l’objet d’une décomposition.

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>Étendues

Il est possible de toogroup une série d’actions à l’aide d’une étendue.  Cette opération est particulièrement utile pour implémenter la gestion des exceptions.  Dans le Concepteur de hello, vous pouvez ajouter une nouvelle étendue et commencer l’ajout de toutes les actions à l’intérieur.  Vous pouvez définir des étendues dans la vue code hello suivante :


```
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