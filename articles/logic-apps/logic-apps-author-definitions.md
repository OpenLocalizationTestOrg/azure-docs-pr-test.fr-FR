---
title: flux de travail aaaDefine avec JSON - Azure Logic Apps | Documents Microsoft
description: "Comment les définitions de workflow toowrite dans JSON pour logic apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Créer des définitions de workflow pour les applications logiques à l’aide de JSON

Vous pouvez créer des définitions de workflow pour [Azure Logic Apps](logic-apps-what-are-logic-apps.md) à l’aide d’un langage JSON déclaratif simple. Si vous n’avez pas encore, vous devez tout d’abord examiner [comment toocreate votre première application logique avec le Concepteur d’application logique](logic-apps-create-a-logic-app.md). Voir aussi hello [complète de référence pour le langage de définition de flux de travail de hello](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Répéter des étapes dans une liste

tooiterate via un tableau qui a des too10, 000 éléments et effectuer une action pour chaque élément, utilisez hello [foreach type](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Gérer les échecs en cas de problème

En règle générale, vous voulez tooinclude un *étape de mise à jour* : une logique qui exécute *si et seulement si* un ou plusieurs de vos appels échouent. Cet exemple obtient les données à partir d’emplacements différents, mais si hello appel échoue, nous voulons tooPOST un message quelque part et nous pouvons tracer cette défaillance ultérieurement :  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify qui `postToErrorMessageQueue` s’exécute uniquement après avoir `readData` a `Failed`, utilisez hello `runAfter` propriété, par exemple, toospecify une liste des valeurs possibles, afin que `runAfter` peut être `["Succeeded", "Failed"]`.

Enfin, étant donné que cet exemple gère désormais l’erreur de hello, nous indiquons ne sont plus les hello exécuter en tant que `Failed`. Étant donné que nous avons ajouté étape hello pour la gestion de cet échec dans cet exemple, hello exécuter a `Succeeded` bien qu’une seule étape `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Exécuter au moins deux étapes en parallèle

toorun plusieurs actions en parallèle, hello `runAfter` propriété doit être équivalente à l’exécution. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

Dans cet exemple, les deux `branch1` et `branch2` sont définies toorun après `readData`. Par conséquent, les deux branches s’exécutent en parallèle. horodateur de Hello pour les deux branches est identique.

![Parallèle](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Joindre deux branches parallèles

Vous pouvez joindre deux actions définies toorun en parallèle en ajoutant des éléments toohello `runAfter` propriété qu’à l’exemple précédent de hello.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Parallèle](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>Mapper configuration différente des tooa d’éléments de liste

Ensuite, supposons que nous souhaitons tooget un contenu différent en fonction de la valeur hello d’une propriété. Nous pouvons créer un mappage des valeurs toodestinations en tant que paramètre :  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

Dans ce cas, nous commençons par obtenir une liste d’articles. En fonction de la catégorie hello qui a été défini en tant que paramètre, la deuxième étape de hello utilise un toolook carte hello URL pour l’obtention du contenu de hello.

Parfois toonote ici : 

*   Hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) fonction vérifie si la catégorie de hello correspond à l’un de hello connu des catégories définies.

*   Une fois que nous obtenons la catégorie de hello, nous pouvons extraire l’élément hello de mappage de hello à l’aide de crochets :`parameters[...]`

## <a name="process-strings"></a>Traiter des chaînes

Vous pouvez utiliser différentes chaînes toomanipulate de fonctions. Par exemple, supposons que nous disposons d’une chaîne que nous toopass tooa système, mais nous ne sommes pas inspire gestion correcte pour l’encodage de caractères. Une option consiste à toobase64 encodez cette chaîne. Toutefois, tooavoid séquence d’échappement dans une URL, nous allons tooreplace quelques caractères. 

Nous souhaitons également une sous-chaîne du nom de la commande hello, car les cinq premiers caractères de hello ne sont pas utilisés.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Travail à partir d’à l’intérieur de toooutside :

1. Obtenir hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) pour le nom de hello auteur de la commande, par conséquent, nous obtenons nombre total de hello de caractères.

2. Nous soustrayons la valeur 5, car nous voulons une chaîne plus courte.

3. Effectivement hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Nous allons commencer à index `5` et accédez hello le reste de la chaîne de hello.

4. Convertir cette tooa sous-chaîne [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) chaîne.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)tous les hello `+` avec des caractères `-` caractères.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)tous les hello `/` avec des caractères `_` caractères.

## <a name="work-with-date-times"></a>Utiliser des dates

Dates peut être utile, particulièrement lorsque vous essayez de toopull des données à partir d’une source de données qui ne gère pas naturellement *déclencheurs*. Vous pouvez également utiliser les dates pour déterminer la durée d’exécution des différentes étapes.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

Dans cet exemple, nous extraire hello `startTime` à partir de l’étape précédente de hello. Nous hello d’obtenir l’heure actuelle et la soustraction d’une seconde :

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

Vous pouvez utiliser d’autres unités de temps, par exemple `minutes` ou `hours`. Enfin, nous pouvons comparer ces deux valeurs. Si hello première valeur est inférieure à la valeur de seconde hello, puis plus d’une seconde a passé depuis hello de première commande.

les dates tooformat, nous pouvons utiliser des modules de formatage de chaîne. Par exemple, tooget hello RFC1123, nous utilisons [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). toolearn sur le format de date, consultez [langage de définition de flux de travail](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Paramètres de déploiement pour différents environnements

Généralement, les cycles de vie de déploiement comprennent un environnement de développement, un environnement intermédiaire et un environnement de production. Par exemple, vous pouvez utiliser hello même définition dans tous ces environnements, mais utiliser différentes bases de données. De même, vous pourriez toouse hello même définition sur différentes régions pour la haute disponibilité mais la base de données de chaque logique application instance tootalk toothat région.
Ce scénario diffère des paramètres à *runtime* où au lieu de cela, vous devez utiliser hello `trigger()` fonctionne comme l’exemple précédent de hello.

Vous pouvez commencer par une définition de base comme celle-ci :

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

Bonjour réel `PUT` demande pour hello logic apps, vous pouvez fournir le paramètre hello `uri`. Charge utile d’application logique hello requiert une valeur par défaut n’existe plus, ce paramètre :

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

Dans chaque environnement, vous pouvez fournir une valeur différente pour hello `connection` paramètre. 

Pour tous les hello options dont vous disposez pour créer et gérer des applications de la logique, consultez hello [documentation de l’API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
