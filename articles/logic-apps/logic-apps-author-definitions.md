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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="50d5e-103">Créer des définitions de workflow pour les applications logiques à l’aide de JSON</span><span class="sxs-lookup"><span data-stu-id="50d5e-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="50d5e-104">Vous pouvez créer des définitions de workflow pour [Azure Logic Apps](logic-apps-what-are-logic-apps.md) à l’aide d’un langage JSON déclaratif simple.</span><span class="sxs-lookup"><span data-stu-id="50d5e-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="50d5e-105">Si vous n’avez pas encore, vous devez tout d’abord examiner [comment toocreate votre première application logique avec le Concepteur d’application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="50d5e-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="50d5e-106">Voir aussi hello [complète de référence pour le langage de définition de flux de travail de hello](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="50d5e-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="50d5e-107">Répéter des étapes dans une liste</span><span class="sxs-lookup"><span data-stu-id="50d5e-107">Repeat steps over a list</span></span>

<span data-ttu-id="50d5e-108">tooiterate via un tableau qui a des too10, 000 éléments et effectuer une action pour chaque élément, utilisez hello [foreach type](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="50d5e-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="50d5e-109">Gérer les échecs en cas de problème</span><span class="sxs-lookup"><span data-stu-id="50d5e-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="50d5e-110">En règle générale, vous voulez tooinclude un *étape de mise à jour* : une logique qui exécute *si et seulement si* un ou plusieurs de vos appels échouent.</span><span class="sxs-lookup"><span data-stu-id="50d5e-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="50d5e-111">Cet exemple obtient les données à partir d’emplacements différents, mais si hello appel échoue, nous voulons tooPOST un message quelque part et nous pouvons tracer cette défaillance ultérieurement :</span><span class="sxs-lookup"><span data-stu-id="50d5e-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="50d5e-112">toospecify qui `postToErrorMessageQueue` s’exécute uniquement après avoir `readData` a `Failed`, utilisez hello `runAfter` propriété, par exemple, toospecify une liste des valeurs possibles, afin que `runAfter` peut être `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="50d5e-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="50d5e-113">Enfin, étant donné que cet exemple gère désormais l’erreur de hello, nous indiquons ne sont plus les hello exécuter en tant que `Failed`.</span><span class="sxs-lookup"><span data-stu-id="50d5e-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="50d5e-114">Étant donné que nous avons ajouté étape hello pour la gestion de cet échec dans cet exemple, hello exécuter a `Succeeded` bien qu’une seule étape `Failed`.</span><span class="sxs-lookup"><span data-stu-id="50d5e-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="50d5e-115">Exécuter au moins deux étapes en parallèle</span><span class="sxs-lookup"><span data-stu-id="50d5e-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="50d5e-116">toorun plusieurs actions en parallèle, hello `runAfter` propriété doit être équivalente à l’exécution.</span><span class="sxs-lookup"><span data-stu-id="50d5e-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="50d5e-117">Dans cet exemple, les deux `branch1` et `branch2` sont définies toorun après `readData`.</span><span class="sxs-lookup"><span data-stu-id="50d5e-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="50d5e-118">Par conséquent, les deux branches s’exécutent en parallèle.</span><span class="sxs-lookup"><span data-stu-id="50d5e-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="50d5e-119">horodateur de Hello pour les deux branches est identique.</span><span class="sxs-lookup"><span data-stu-id="50d5e-119">hello timestamp for both branches is identical.</span></span>

![Parallèle](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="50d5e-121">Joindre deux branches parallèles</span><span class="sxs-lookup"><span data-stu-id="50d5e-121">Join two parallel branches</span></span>

<span data-ttu-id="50d5e-122">Vous pouvez joindre deux actions définies toorun en parallèle en ajoutant des éléments toohello `runAfter` propriété qu’à l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="50d5e-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="50d5e-124">Mapper configuration différente des tooa d’éléments de liste</span><span class="sxs-lookup"><span data-stu-id="50d5e-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="50d5e-125">Ensuite, supposons que nous souhaitons tooget un contenu différent en fonction de la valeur hello d’une propriété.</span><span class="sxs-lookup"><span data-stu-id="50d5e-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="50d5e-126">Nous pouvons créer un mappage des valeurs toodestinations en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="50d5e-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="50d5e-127">Dans ce cas, nous commençons par obtenir une liste d’articles.</span><span class="sxs-lookup"><span data-stu-id="50d5e-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="50d5e-128">En fonction de la catégorie hello qui a été défini en tant que paramètre, la deuxième étape de hello utilise un toolook carte hello URL pour l’obtention du contenu de hello.</span><span class="sxs-lookup"><span data-stu-id="50d5e-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="50d5e-129">Parfois toonote ici :</span><span class="sxs-lookup"><span data-stu-id="50d5e-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="50d5e-130">Hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) fonction vérifie si la catégorie de hello correspond à l’un de hello connu des catégories définies.</span><span class="sxs-lookup"><span data-stu-id="50d5e-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="50d5e-131">Une fois que nous obtenons la catégorie de hello, nous pouvons extraire l’élément hello de mappage de hello à l’aide de crochets :`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="50d5e-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="50d5e-132">Traiter des chaînes</span><span class="sxs-lookup"><span data-stu-id="50d5e-132">Process strings</span></span>

<span data-ttu-id="50d5e-133">Vous pouvez utiliser différentes chaînes toomanipulate de fonctions.</span><span class="sxs-lookup"><span data-stu-id="50d5e-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="50d5e-134">Par exemple, supposons que nous disposons d’une chaîne que nous toopass tooa système, mais nous ne sommes pas inspire gestion correcte pour l’encodage de caractères.</span><span class="sxs-lookup"><span data-stu-id="50d5e-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="50d5e-135">Une option consiste à toobase64 encodez cette chaîne.</span><span class="sxs-lookup"><span data-stu-id="50d5e-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="50d5e-136">Toutefois, tooavoid séquence d’échappement dans une URL, nous allons tooreplace quelques caractères.</span><span class="sxs-lookup"><span data-stu-id="50d5e-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="50d5e-137">Nous souhaitons également une sous-chaîne du nom de la commande hello, car les cinq premiers caractères de hello ne sont pas utilisés.</span><span class="sxs-lookup"><span data-stu-id="50d5e-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="50d5e-138">Travail à partir d’à l’intérieur de toooutside :</span><span class="sxs-lookup"><span data-stu-id="50d5e-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="50d5e-139">Obtenir hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) pour le nom de hello auteur de la commande, par conséquent, nous obtenons nombre total de hello de caractères.</span><span class="sxs-lookup"><span data-stu-id="50d5e-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="50d5e-140">Nous soustrayons la valeur 5, car nous voulons une chaîne plus courte.</span><span class="sxs-lookup"><span data-stu-id="50d5e-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="50d5e-141">Effectivement hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="50d5e-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="50d5e-142">Nous allons commencer à index `5` et accédez hello le reste de la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="50d5e-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="50d5e-143">Convertir cette tooa sous-chaîne [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) chaîne.</span><span class="sxs-lookup"><span data-stu-id="50d5e-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="50d5e-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)tous les hello `+` avec des caractères `-` caractères.</span><span class="sxs-lookup"><span data-stu-id="50d5e-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="50d5e-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)tous les hello `/` avec des caractères `_` caractères.</span><span class="sxs-lookup"><span data-stu-id="50d5e-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="50d5e-146">Utiliser des dates</span><span class="sxs-lookup"><span data-stu-id="50d5e-146">Work with Date Times</span></span>

<span data-ttu-id="50d5e-147">Dates peut être utile, particulièrement lorsque vous essayez de toopull des données à partir d’une source de données qui ne gère pas naturellement *déclencheurs*.</span><span class="sxs-lookup"><span data-stu-id="50d5e-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="50d5e-148">Vous pouvez également utiliser les dates pour déterminer la durée d’exécution des différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="50d5e-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="50d5e-149">Dans cet exemple, nous extraire hello `startTime` à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="50d5e-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="50d5e-150">Nous hello d’obtenir l’heure actuelle et la soustraction d’une seconde :</span><span class="sxs-lookup"><span data-stu-id="50d5e-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="50d5e-151">Vous pouvez utiliser d’autres unités de temps, par exemple `minutes` ou `hours`.</span><span class="sxs-lookup"><span data-stu-id="50d5e-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="50d5e-152">Enfin, nous pouvons comparer ces deux valeurs.</span><span class="sxs-lookup"><span data-stu-id="50d5e-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="50d5e-153">Si hello première valeur est inférieure à la valeur de seconde hello, puis plus d’une seconde a passé depuis hello de première commande.</span><span class="sxs-lookup"><span data-stu-id="50d5e-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="50d5e-154">les dates tooformat, nous pouvons utiliser des modules de formatage de chaîne.</span><span class="sxs-lookup"><span data-stu-id="50d5e-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="50d5e-155">Par exemple, tooget hello RFC1123, nous utilisons [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="50d5e-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="50d5e-156">toolearn sur le format de date, consultez [langage de définition de flux de travail](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="50d5e-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="50d5e-157">Paramètres de déploiement pour différents environnements</span><span class="sxs-lookup"><span data-stu-id="50d5e-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="50d5e-158">Généralement, les cycles de vie de déploiement comprennent un environnement de développement, un environnement intermédiaire et un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="50d5e-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="50d5e-159">Par exemple, vous pouvez utiliser hello même définition dans tous ces environnements, mais utiliser différentes bases de données.</span><span class="sxs-lookup"><span data-stu-id="50d5e-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="50d5e-160">De même, vous pourriez toouse hello même définition sur différentes régions pour la haute disponibilité mais la base de données de chaque logique application instance tootalk toothat région.</span><span class="sxs-lookup"><span data-stu-id="50d5e-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="50d5e-161">Ce scénario diffère des paramètres à *runtime* où au lieu de cela, vous devez utiliser hello `trigger()` fonctionne comme l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="50d5e-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="50d5e-162">Vous pouvez commencer par une définition de base comme celle-ci :</span><span class="sxs-lookup"><span data-stu-id="50d5e-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="50d5e-163">Bonjour réel `PUT` demande pour hello logic apps, vous pouvez fournir le paramètre hello `uri`.</span><span class="sxs-lookup"><span data-stu-id="50d5e-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="50d5e-164">Charge utile d’application logique hello requiert une valeur par défaut n’existe plus, ce paramètre :</span><span class="sxs-lookup"><span data-stu-id="50d5e-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

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

<span data-ttu-id="50d5e-165">Dans chaque environnement, vous pouvez fournir une valeur différente pour hello `connection` paramètre.</span><span class="sxs-lookup"><span data-stu-id="50d5e-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="50d5e-166">Pour tous les hello options dont vous disposez pour créer et gérer des applications de la logique, consultez hello [documentation de l’API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="50d5e-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
