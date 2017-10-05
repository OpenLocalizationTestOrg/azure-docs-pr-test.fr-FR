---
title: "Mises à jour de schéma du 1er juin 2016 - Azure Logic Apps | Microsoft Docs"
description: "Créer des définitions JSON pour Azure Logic Apps avec la version de schéma 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="5b29d-103">Mises à jour de schéma pour Azure Logic Apps - 1er juin 2016</span><span class="sxs-lookup"><span data-stu-id="5b29d-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="5b29d-104">Cette nouvelle version de schéma et d’API intègre différentes améliorations clés destinées à accroître la fiabilité et la simplicité d’utilisation des applications logiques :</span><span class="sxs-lookup"><span data-stu-id="5b29d-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="5b29d-105">Les [étendues](#scopes) vous permettent de regrouper ou d’imbriquer des actions sous la forme d’un ensemble d’actions.</span><span class="sxs-lookup"><span data-stu-id="5b29d-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="5b29d-106">Les [conditions et les boucles](#conditions-loops) sont désormais des actions de première classe.</span><span class="sxs-lookup"><span data-stu-id="5b29d-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="5b29d-107">La précision de l’ordre d’exécution des actions a été améliorée grâce au remplacement de la propriété `dependsOn` par la propriété `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="5b29d-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="5b29d-108">Pour mettre à niveau vos applications logiques à partir du schéma en version préliminaire du 1er août 2015 vers le schéma du 1er juin 2016, [consultez la section relative à la mise à niveau](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="5b29d-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="5b29d-109">Étendues</span><span class="sxs-lookup"><span data-stu-id="5b29d-109">Scopes</span></span>

<span data-ttu-id="5b29d-110">Ce schéma comporte des étendues, qui vous permettent de regrouper ou d’imbriquer des actions.</span><span class="sxs-lookup"><span data-stu-id="5b29d-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="5b29d-111">Par exemple, une condition peut en contenir une autre.</span><span class="sxs-lookup"><span data-stu-id="5b29d-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="5b29d-112">Apprenez-en davantage sur la [syntaxe des étendues](../logic-apps/logic-apps-loops-and-scopes.md), ou examinez l’exemple d’étendue de base ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b29d-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="5b29d-113">Modifications des conditions et boucles</span><span class="sxs-lookup"><span data-stu-id="5b29d-113">Conditions and loops changes</span></span>

<span data-ttu-id="5b29d-114">Dans les versions de schéma précédentes, les conditions et les boucles étaient des paramètres associés avec une seule action.</span><span class="sxs-lookup"><span data-stu-id="5b29d-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="5b29d-115">Cette limitation a été levée dans ce schéma, de sorte que les conditions et les boucles apparaissent à présent sous forme de types d’actions.</span><span class="sxs-lookup"><span data-stu-id="5b29d-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="5b29d-116">Apprenez-en davantage sur les [boucles et étendues](../logic-apps/logic-apps-loops-and-scopes.md), ou examinez l’exemple d’action de condition de base ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5b29d-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="5b29d-117">Propriété « runAfter »</span><span class="sxs-lookup"><span data-stu-id="5b29d-117">'runAfter' property</span></span>

<span data-ttu-id="5b29d-118">La propriété `runAfter` remplace `dependsOn`, ce qui vous permet de spécifier plus précisément l’ordre d’exécution des actions en fonction de l’état des actions précédentes.</span><span class="sxs-lookup"><span data-stu-id="5b29d-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="5b29d-119">La propriété `dependsOn` signifiait « l’action a été exécutée et a réussi » et ne tenait pas compte du nombre de fois où vous vouliez exécuter une action en fonction de la réussite, de l’échec ou de l’omission de l’action précédente.</span><span class="sxs-lookup"><span data-stu-id="5b29d-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="5b29d-120">La propriété `runAfter` vous offre cette souplesse sous la forme d’un objet spécifiant le nom de toutes les actions après lesquelles l’objet doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="5b29d-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="5b29d-121">Cette propriété définit également un tableau d’états acceptables en tant que déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="5b29d-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="5b29d-122">Par exemple, si vous souhaitez exécuter une action après la réussite de l’étape A, ainsi qu’après la réussite ou l’échec de l’étape B, vous construisez la propriété `runAfter` suivante :</span><span class="sxs-lookup"><span data-stu-id="5b29d-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="5b29d-123">Mettre à niveau votre schéma</span><span class="sxs-lookup"><span data-stu-id="5b29d-123">Upgrade your schema</span></span>

<span data-ttu-id="5b29d-124">La mise à niveau vers le nouveau schéma se déroule en quelques étapes seulement.</span><span class="sxs-lookup"><span data-stu-id="5b29d-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="5b29d-125">Le processus de mise à niveau implique l’exécution du script de mise à niveau, l’enregistrement en tant que nouvelle application logique et, si vous le souhaitez, le remplacement éventuel de l’application logique précédente.</span><span class="sxs-lookup"><span data-stu-id="5b29d-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="5b29d-126">Dans le Portail Azure, ouvrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="5b29d-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="5b29d-127">Accédez à **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="5b29d-127">Go to **Overview**.</span></span> <span data-ttu-id="5b29d-128">Dans la barre d’outils de l’application logique, choisissez **Mettre à jour le schéma**.</span><span class="sxs-lookup"><span data-stu-id="5b29d-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Choisir l’option Mettre à jour le schéma][1]
   
    <span data-ttu-id="5b29d-130">Le portail vous renvoie la définition mise à niveau, que vous pouvez copier et coller dans une définition de ressource si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5b29d-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="5b29d-131">Toutefois, nous vous **recommandons vivement** de choisir l’option **Enregistrer sous** pour vérifier que toutes les références de connexion sont valides dans l’application logique mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="5b29d-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="5b29d-132">Dans la barre d’outils du panneau de mise à niveau, choisissez **Enregistrer sous**.</span><span class="sxs-lookup"><span data-stu-id="5b29d-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="5b29d-133">Entrez le nom et l’état de l’application logique.</span><span class="sxs-lookup"><span data-stu-id="5b29d-133">Enter the logic name and status.</span></span> <span data-ttu-id="5b29d-134">Pour déployer votre application logique mise à niveau, choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5b29d-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="5b29d-135">Vérifiez que votre application logique mise à niveau fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="5b29d-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5b29d-136">Si vous utilisez un déclencheur manuel ou sur demande, l’URL de rappel change dans votre nouvelle application logique.</span><span class="sxs-lookup"><span data-stu-id="5b29d-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="5b29d-137">Testez la nouvelle URL pour vérifier son fonctionnement de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="5b29d-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="5b29d-138">Pour conserver les URL précédentes, vous pouvez cloner votre application logique existante.</span><span class="sxs-lookup"><span data-stu-id="5b29d-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="5b29d-139">*Facultatif* Pour remplacer votre application logique précédente par la nouvelle version du schéma, dans la barre d’outils, choisissez **Cloner** en regard de l’option **Mettre à jour le schéma**.</span><span class="sxs-lookup"><span data-stu-id="5b29d-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="5b29d-140">Cette étape n’est requise que si vous souhaitez conserver les mêmes ID de ressource ou URL du déclencheur sur demande de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="5b29d-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="5b29d-141">Notes de l’outil de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="5b29d-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="5b29d-142">Mappage de conditions</span><span class="sxs-lookup"><span data-stu-id="5b29d-142">Mapping conditions</span></span>

<span data-ttu-id="5b29d-143">Dans la définition mise à niveau, l’outil s’efforce de regrouper les actions des branches true et false sous la forme d’une étendue.</span><span class="sxs-lookup"><span data-stu-id="5b29d-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="5b29d-144">Le modèle de concepteur de `@equals(actions('a').status, 'Skipped')` doit notamment apparaître en tant qu’action `else`.</span><span class="sxs-lookup"><span data-stu-id="5b29d-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="5b29d-145">Toutefois, si l’outil détecte des modèles non reconnaissables, il peut éventuellement créer des conditions distinctes pour les branches true et false.</span><span class="sxs-lookup"><span data-stu-id="5b29d-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="5b29d-146">Vous pouvez remapper les actions après la mise à niveau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5b29d-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="5b29d-147">Boucle « foreach » avec condition</span><span class="sxs-lookup"><span data-stu-id="5b29d-147">'foreach' loop with condition</span></span>

<span data-ttu-id="5b29d-148">Dans le nouveau schéma, vous pouvez utiliser l’action de filtrage pour répliquer le modèle d’une boucle `foreach` avec une condition par élément, mais cette modification doit se produire automatiquement lorsque vous procédez à la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="5b29d-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="5b29d-149">La condition devient une action de filtrage avant la boucle foreach de façon à renvoyer uniquement un tableau d’éléments correspondant à cette condition, puis ce tableau est transmis dans l’action foreach.</span><span class="sxs-lookup"><span data-stu-id="5b29d-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="5b29d-150">Pour découvrir un exemple, consultez l’article relatif aux [boucles et étendues](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="5b29d-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="5b29d-151">Balises de ressource</span><span class="sxs-lookup"><span data-stu-id="5b29d-151">Resource tags</span></span>

<span data-ttu-id="5b29d-152">Après la mise à niveau, les balises de ressource sont supprimées. Vous devez donc les redéfinir pour le workflow mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="5b29d-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="5b29d-153">Autres modifications</span><span class="sxs-lookup"><span data-stu-id="5b29d-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="5b29d-154">Déclencheur « manual » (manuel) renommé déclencheur « request » (sur demande)</span><span class="sxs-lookup"><span data-stu-id="5b29d-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="5b29d-155">Le type de déclencheur `manual` est déconseillé et a été renommé sous la forme `request` avec le type `http`.</span><span class="sxs-lookup"><span data-stu-id="5b29d-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="5b29d-156">Cette modification est plus cohérente avec le type de modèle pour la génération duquel le déclencheur est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5b29d-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="5b29d-157">Nouvelle action de « filtre »</span><span class="sxs-lookup"><span data-stu-id="5b29d-157">New 'filter' action</span></span>

<span data-ttu-id="5b29d-158">Pour filtrer un tableau d’éléments volumineux de façon à obtenir un sous-ensemble d’éléments plus restreint, le nouveau type `filter` accepte un tableau et une condition, évalue la condition pour chaque élément, puis renvoie un tableau d’éléments correspondant à la condition.</span><span class="sxs-lookup"><span data-stu-id="5b29d-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="5b29d-159">Restrictions relatives aux actions « foreach » et « until »</span><span class="sxs-lookup"><span data-stu-id="5b29d-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="5b29d-160">La boucle `foreach` et `until` est limitée à une seule action.</span><span class="sxs-lookup"><span data-stu-id="5b29d-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="5b29d-161">Nouvelle propriété « trackedProperties » relative aux actions</span><span class="sxs-lookup"><span data-stu-id="5b29d-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="5b29d-162">Les actions peuvent désormais comporter une propriété supplémentaire appelée `trackedProperties`, sœur des propriétés `runAfter` et `type`.</span><span class="sxs-lookup"><span data-stu-id="5b29d-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="5b29d-163">Cet objet spécifie certaines entrées ou sorties d’action que vous souhaitez inclure dans la télémétrie de diagnostic Azure, dont l’émission intervient dans le cadre d’un workflow.</span><span class="sxs-lookup"><span data-stu-id="5b29d-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="5b29d-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5b29d-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5b29d-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b29d-165">Next Steps</span></span>
* [<span data-ttu-id="5b29d-166">Créer des définitions d’application logique</span><span class="sxs-lookup"><span data-stu-id="5b29d-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="5b29d-167">Création d’un modèle de déploiement d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="5b29d-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
