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
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="a63bd-103">Boucles, étendues et décomposition dans Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a63bd-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="a63bd-104">Logique d’applications fournit un certain nombre de toowork manières avec les tableaux, les collections, les lots et les boucles au sein d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a63bd-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="a63bd-105">Boucle ForEach et tableaux</span><span class="sxs-lookup"><span data-stu-id="a63bd-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="a63bd-106">Logique d’applications vous permet de tooloop sur un jeu de données et effectuer une action pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="a63bd-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="a63bd-107">Cela est possible via hello `foreach` action.</span><span class="sxs-lookup"><span data-stu-id="a63bd-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="a63bd-108">Dans le Concepteur de hello, vous pouvez spécifier tooadd une boucle for each.</span><span class="sxs-lookup"><span data-stu-id="a63bd-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="a63bd-109">Après avoir sélectionné le tableau hello sur que vous souhaitez tooiterate, vous pouvez commencer l’ajout d’actions.</span><span class="sxs-lookup"><span data-stu-id="a63bd-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="a63bd-110">Actuellement, vous êtes limité tooonly une action par boucle foreach, mais cette restriction sera levée Bonjour semaines à venir.</span><span class="sxs-lookup"><span data-stu-id="a63bd-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="a63bd-111">Une fois au sein de la boucle de hello, vous pouvez commencer toospecify ce qui doit se produire à chaque valeur du tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="a63bd-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="a63bd-112">Si vous utilisez le mode code, vous pouvez spécifier une boucle foreach comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a63bd-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="a63bd-113">Dans cet exemple, une boucle foreach envoie un e-mail à chaque adresse contenant « microsoft.com » :</span><span class="sxs-lookup"><span data-stu-id="a63bd-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="a63bd-114">A `foreach` action peut itérer sur des tableaux de too5, 000 lignes.</span><span class="sxs-lookup"><span data-stu-id="a63bd-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="a63bd-115">Chaque itération s’exécute en parallèle par défaut.</span><span class="sxs-lookup"><span data-stu-id="a63bd-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="a63bd-116">Boucles ForEach séquentielles</span><span class="sxs-lookup"><span data-stu-id="a63bd-116">Sequential ForEach loops</span></span>

<span data-ttu-id="a63bd-117">tooenable un tooexecute de boucle foreach de manière séquentielle, hello `Sequential` option de l’opération doit être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="a63bd-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="a63bd-118">Boucle Until</span><span class="sxs-lookup"><span data-stu-id="a63bd-118">Until loop</span></span>
  
  <span data-ttu-id="a63bd-119">Vous pouvez effectuer une action ou une série d’actions jusqu’à ce qu’une condition soit remplie.</span><span class="sxs-lookup"><span data-stu-id="a63bd-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="a63bd-120">Hello pour ce scénario le plus courant appelle un point de terminaison jusqu'à ce que vous obtenez la réponse hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="a63bd-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="a63bd-121">Dans le Concepteur de hello, vous pouvez spécifier tooadd une boucle.</span><span class="sxs-lookup"><span data-stu-id="a63bd-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="a63bd-122">Après avoir ajouté les actions à l’intérieur de la boucle de hello, vous pouvez définir la condition de sortie hello, ainsi hello des limites de la boucle.</span><span class="sxs-lookup"><span data-stu-id="a63bd-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="a63bd-123">Il existe un délai de 1 minute entre les cycles de la boucle.</span><span class="sxs-lookup"><span data-stu-id="a63bd-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="a63bd-124">Si vous utilisez le mode code, vous pouvez spécifier une boucle until comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a63bd-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="a63bd-125">Il s’agit d’un exemple d’appel d’un point de terminaison HTTP jusqu'à ce que le corps de la réponse hello a la valeur de hello 'Terminé'.</span><span class="sxs-lookup"><span data-stu-id="a63bd-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="a63bd-126">La procédure se termine quand l’une des conditions suivantes est remplie :</span><span class="sxs-lookup"><span data-stu-id="a63bd-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="a63bd-127">L’état de la réponse HTTP est « Completed ».</span><span class="sxs-lookup"><span data-stu-id="a63bd-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="a63bd-128">La procédure a duré 1 heure.</span><span class="sxs-lookup"><span data-stu-id="a63bd-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="a63bd-129">Elle a effectué 100 cycles de boucle.</span><span class="sxs-lookup"><span data-stu-id="a63bd-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="a63bd-130">SplitOn et décomposition</span><span class="sxs-lookup"><span data-stu-id="a63bd-130">SplitOn and debatching</span></span>

<span data-ttu-id="a63bd-131">Parfois, un déclencheur peut s’afficher un tableau d’éléments que vous souhaitez toodebatch et démarrez un flux de travail par article.</span><span class="sxs-lookup"><span data-stu-id="a63bd-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="a63bd-132">Cela peut être effectuée via hello `spliton` commande.</span><span class="sxs-lookup"><span data-stu-id="a63bd-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="a63bd-133">Par défaut, si votre swagger de déclencheur spécifie une charge utile qui est un tableau, un `spliton` est ajouté et lance une exécution par élément.</span><span class="sxs-lookup"><span data-stu-id="a63bd-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="a63bd-134">Tooa déclencheur peut uniquement être ajouté à SplitOn.</span><span class="sxs-lookup"><span data-stu-id="a63bd-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="a63bd-135">Ce paramétrage peut être configuré ou remplacé manuellement dans la définition en mode code.</span><span class="sxs-lookup"><span data-stu-id="a63bd-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="a63bd-136">Actuellement SplitOn pouvez debatch tableaux des too5, 000 éléments.</span><span class="sxs-lookup"><span data-stu-id="a63bd-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="a63bd-137">Vous ne pouvez avoir un `spliton` et également implémenter le modèle de réponse synchrone hello.</span><span class="sxs-lookup"><span data-stu-id="a63bd-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="a63bd-138">Les flux de travail appelée qui a un `response` action en outre trop`spliton` sera exécuté de façon asynchrone et d’envoi immédiat `202 Accepted` réponse.</span><span class="sxs-lookup"><span data-stu-id="a63bd-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="a63bd-139">SplitOn peut être spécifié dans la vue de code comme hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a63bd-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="a63bd-140">Dans cet exemple, un tableau d’éléments est reçu et chacune de ses lignes fait l’objet d’une décomposition.</span><span class="sxs-lookup"><span data-stu-id="a63bd-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="a63bd-141">Étendues</span><span class="sxs-lookup"><span data-stu-id="a63bd-141">Scopes</span></span>

<span data-ttu-id="a63bd-142">Il est possible de toogroup une série d’actions à l’aide d’une étendue.</span><span class="sxs-lookup"><span data-stu-id="a63bd-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="a63bd-143">Cette opération est particulièrement utile pour implémenter la gestion des exceptions.</span><span class="sxs-lookup"><span data-stu-id="a63bd-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="a63bd-144">Dans le Concepteur de hello, vous pouvez ajouter une nouvelle étendue et commencer l’ajout de toutes les actions à l’intérieur.</span><span class="sxs-lookup"><span data-stu-id="a63bd-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="a63bd-145">Vous pouvez définir des étendues dans la vue code hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a63bd-145">You can define scopes in code-view like hello following:</span></span>


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