---
title: "Définir des workflows avec JSON - Azure Logic Apps | Microsoft Docs"
description: "Procédure d’écriture de définitions de workflow au format JSON pour les applications logiques"
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
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="c8e2e-103">Créer des définitions de workflow pour les applications logiques à l’aide de JSON</span><span class="sxs-lookup"><span data-stu-id="c8e2e-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="c8e2e-104">Vous pouvez créer des définitions de workflow pour [Azure Logic Apps](logic-apps-what-are-logic-apps.md) à l’aide d’un langage JSON déclaratif simple.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="c8e2e-105">Si vous ne l’avez pas encore fait, commencez par consulter l’article décrivant la [procédure de création de votre première application logique avec le concepteur d’application logique](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="c8e2e-106">Vous pouvez également lire la [référence complète du langage de définition de workflow](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="c8e2e-107">Répéter des étapes dans une liste</span><span class="sxs-lookup"><span data-stu-id="c8e2e-107">Repeat steps over a list</span></span>

<span data-ttu-id="c8e2e-108">Pour itérer au sein d’un tableau comportant plus de 10 000 éléments et exécuter une action sur chaque élément, utilisez le [type foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="c8e2e-109">Gérer les échecs en cas de problème</span><span class="sxs-lookup"><span data-stu-id="c8e2e-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="c8e2e-110">Vous souhaitez généralement inclure une *étape de correction*, c’est-à-dire une logique qui s’exécute *si et seulement si* un ou plusieurs de vos appels échouent.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="c8e2e-111">Cet exemple obtient des données provenant de différents emplacements, mais si l’appel échoue, nous voulons PUBLIER un message à un endroit quelconque de façon à pouvoir repérer cet échec par la suite :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="c8e2e-112">Pour indiquer que l’action `postToErrorMessageQueue` s’exécute uniquement si l’action `readData` présente l’état `Failed`, utilisez la propriété `runAfter`, par exemple pour spécifier une liste de valeurs possibles, de sorte que `runAfter` peut présenter les valeurs `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="c8e2e-113">Enfin, étant donné que cet exemple gère désormais l’erreur, nous n’identifions plus l’exécution avec l’état `Failed`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="c8e2e-114">Puisque nous avons ajouté l’étape de gestion de cet échec dans cet exemple, l’exécution est indiquée comme `Succeeded`, même si une étape a présenté l’état `Failed`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="c8e2e-115">Exécuter au moins deux étapes en parallèle</span><span class="sxs-lookup"><span data-stu-id="c8e2e-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="c8e2e-116">Pour exécuter plusieurs actions en parallèle, la propriété `runAfter` doit être équivalente au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="c8e2e-117">Dans cet exemple, les éléments `branch1` et `branch2` sont tous deux définis comme devant s’exécuter après l’action `readData`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="c8e2e-118">Par conséquent, les deux branches s’exécutent en parallèle.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="c8e2e-119">Ces deux branches présentent le même horodateur.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-119">The timestamp for both branches is identical.</span></span>

![Parallèle](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="c8e2e-121">Joindre deux branches parallèles</span><span class="sxs-lookup"><span data-stu-id="c8e2e-121">Join two parallel branches</span></span>

<span data-ttu-id="c8e2e-122">Vous pouvez joindre deux actions définies comme devant s’exécuter en parallèle en ajoutant des éléments à la propriété `runAfter`, comme dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

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

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="c8e2e-124">Mapper les éléments d’une liste sur une autre configuration</span><span class="sxs-lookup"><span data-stu-id="c8e2e-124">Map list items to a different configuration</span></span>

<span data-ttu-id="c8e2e-125">À présent, supposons que nous voulions obtenir un contenu différent selon la valeur d’une propriété.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="c8e2e-126">Nous pouvons créer un mappage des valeurs aux destinations en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-126">We can create a map of values to destinations as a parameter:</span></span>  

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

<span data-ttu-id="c8e2e-127">Dans ce cas, nous commençons par obtenir une liste d’articles.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="c8e2e-128">Selon la catégorie définie en tant que paramètre, la deuxième étape utilise un mappage pour rechercher l’URL à partir de laquelle obtenir le contenu.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="c8e2e-129">Tenez compte des points suivants :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-129">Some times to note here:</span></span> 

*   <span data-ttu-id="c8e2e-130">La fonction [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) vérifie si la catégorie correspond ou non à l’une des catégories définies connues.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="c8e2e-131">Une fois que nous avons obtenu la catégorie, nous pouvons extraire l’élément du mappage à l’aide de crochets : `parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="c8e2e-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="c8e2e-132">Traiter des chaînes</span><span class="sxs-lookup"><span data-stu-id="c8e2e-132">Process strings</span></span>

<span data-ttu-id="c8e2e-133">Différentes fonctions vous permettent de manipuler les chaînes.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="c8e2e-134">Par exemple, supposons que nous souhaitions transmettre une chaîne à un système, mais que nous ne soyons pas certains de l’encodage de caractères à utiliser.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="c8e2e-135">Une option consiste à encoder cette chaîne en base64.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="c8e2e-136">Toutefois, pour éviter la séquence d’échappement dans une URL, nous allons remplacer plusieurs caractères.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="c8e2e-137">Nous voulons également disposer d’une sous-chaîne du nom de la commande, car les cinq premiers caractères ne sont pas utilisés.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

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

<span data-ttu-id="c8e2e-138">Voici le déroulement des opérations de l’intérieur vers l’extérieur :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="c8e2e-139">Nous obtenons l’élément [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) pour le nom de la commande afin de récupérer le nombre total de caractères.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="c8e2e-140">Nous soustrayons la valeur 5, car nous voulons une chaîne plus courte.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="c8e2e-141">Nous utilisons l’élément [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="c8e2e-142">Nous commençons à l'index `5` et suivons le reste de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="c8e2e-143">Nous convertissons cette sous-chaîne en une chaîne [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="c8e2e-144">Nous exécutons l’action [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) pour remplacer tous les caractères `+` par des caractères `-`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="c8e2e-145">Nous exécutons l’action [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) pour remplacer tous les caractères `/` par des caractères `_`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="c8e2e-146">Utiliser des dates</span><span class="sxs-lookup"><span data-stu-id="c8e2e-146">Work with Date Times</span></span>

<span data-ttu-id="c8e2e-147">Les dates peuvent vous être utiles, particulièrement lorsque vous tentez d’extraire des données à partir d’une source de données qui ne prend pas naturellement en charge les *déclencheurs*.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="c8e2e-148">Vous pouvez également utiliser les dates pour déterminer la durée d’exécution des différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="c8e2e-149">Dans cet exemple, nous extrayons l’élément `startTime` de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="c8e2e-150">Puis nous obtenons l’heure actuelle, et nous lui soustrayons une seconde :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="c8e2e-151">Vous pouvez utiliser d’autres unités de temps, par exemple `minutes` ou `hours`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="c8e2e-152">Enfin, nous pouvons comparer ces deux valeurs.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="c8e2e-153">Si la première valeur est inférieure à la seconde, plus d’une seconde s’est écoulée depuis que la commande a été passée.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="c8e2e-154">Pour formater les dates, nous pouvons utiliser des formateurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="c8e2e-155">Par exemple, pour obtenir RFC1123, nous utilisons [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="c8e2e-156">Pour plus d’informations sur le formatage des dates, consultez l’article [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow) (Langage de définition de workflow).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="c8e2e-157">Paramètres de déploiement pour différents environnements</span><span class="sxs-lookup"><span data-stu-id="c8e2e-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="c8e2e-158">Généralement, les cycles de vie de déploiement comprennent un environnement de développement, un environnement intermédiaire et un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="c8e2e-159">Par exemple, vous pouvez mettre en œuvre la même définition dans tous ces environnements, tout en utilisant des bases de données distinctes.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="c8e2e-160">De même, vous pouvez faire en sorte d’utiliser la même définition dans plusieurs régions à des fins de haute disponibilité, tout en souhaitant que chaque instance de l’application logique communique avec la base de données d’une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="c8e2e-161">Ce scénario diffère de l’utilisation de paramètres au moment de *l’exécution* dans lequel vous devez plutôt utiliser la fonction `trigger()`, comme indiqué dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="c8e2e-162">Vous pouvez commencer par une définition de base comme celle-ci :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="c8e2e-163">Puis, dans la requête `PUT` réelle pour les applications logiques, vous pouvez fournir le paramètre `uri`.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="c8e2e-164">Étant donné qu’il n’existe plus de valeur par défaut, la charge utile d’application logique nécessite le paramètre suivant :</span><span class="sxs-lookup"><span data-stu-id="c8e2e-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
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

<span data-ttu-id="c8e2e-165">Vous pouvez fournir une valeur différente pour le paramètre `connection` dans chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="c8e2e-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="c8e2e-166">Pour connaître toutes les options dont vous disposez pour créer et gérer des applications logiques, consultez la [documentation de l’API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8e2e-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
