---
title: "met à jour aaaSchema juin-01-2016 - Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="da735-103">Mises à jour de schéma pour Azure Logic Apps - 1er juin 2016</span><span class="sxs-lookup"><span data-stu-id="da735-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="da735-104">Ce schéma et une API version pour Azure Logic Apps inclut des améliorations clés qui rendent les applications logique plus fiable et plus facile de toouse :</span><span class="sxs-lookup"><span data-stu-id="da735-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="da735-105">Les [étendues](#scopes) vous permettent de regrouper ou d’imbriquer des actions sous la forme d’un ensemble d’actions.</span><span class="sxs-lookup"><span data-stu-id="da735-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="da735-106">Les [conditions et les boucles](#conditions-loops) sont désormais des actions de première classe.</span><span class="sxs-lookup"><span data-stu-id="da735-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="da735-107">Le classement plus précis pour l’exécution des actions avec hello `runAfter` propriété, en remplaçant`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="da735-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="da735-108">afficher un aperçu de tooupgrade vos applications logiques à partir de hello au 1er août 2015 1er juin 2016 schéma, toohello [extraire la section de mise à niveau hello](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="da735-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="da735-109">Étendues</span><span class="sxs-lookup"><span data-stu-id="da735-109">Scopes</span></span>

<span data-ttu-id="da735-110">Ce schéma comporte des étendues, qui vous permettent de regrouper ou d’imbriquer des actions.</span><span class="sxs-lookup"><span data-stu-id="da735-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="da735-111">Par exemple, une condition peut en contenir une autre.</span><span class="sxs-lookup"><span data-stu-id="da735-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="da735-112">Apprenez-en davantage sur la [syntaxe des étendues](../logic-apps/logic-apps-loops-and-scopes.md), ou examinez l’exemple d’étendue de base ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="da735-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

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
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="da735-113">Modifications des conditions et boucles</span><span class="sxs-lookup"><span data-stu-id="da735-113">Conditions and loops changes</span></span>

<span data-ttu-id="da735-114">Dans les versions de schéma précédentes, les conditions et les boucles étaient des paramètres associés avec une seule action.</span><span class="sxs-lookup"><span data-stu-id="da735-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="da735-115">Cette limitation a été levée dans ce schéma, de sorte que les conditions et les boucles apparaissent à présent sous forme de types d’actions.</span><span class="sxs-lookup"><span data-stu-id="da735-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="da735-116">Apprenez-en davantage sur les [boucles et étendues](../logic-apps/logic-apps-loops-and-scopes.md), ou examinez l’exemple d’action de condition de base ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="da735-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

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
## <a name="runafter-property"></a><span data-ttu-id="da735-117">Propriété « runAfter »</span><span class="sxs-lookup"><span data-stu-id="da735-117">'runAfter' property</span></span>

<span data-ttu-id="da735-118">Hello `runAfter` propriété remplace `dependsOn`, en fournissant une plus grande précision lorsque vous spécifiez la commande hello exécuter pour les actions basé sur l’état de hello des actions précédentes.</span><span class="sxs-lookup"><span data-stu-id="da735-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="da735-119">Hello `dependsOn` de la propriété est synonyme de « action de hello exécuté et a réussi », quel que soit le nombre de fois que vous souhaitiez tooexecute une action, en fonction de l’action précédente de hello réussite, échec ou ignorée.</span><span class="sxs-lookup"><span data-stu-id="da735-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="da735-120">Hello `runAfter` propriété souplesse que comme un objet qui spécifie tous les hello qui hello objet une fois les noms d’actions.</span><span class="sxs-lookup"><span data-stu-id="da735-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="da735-121">Cette propriété définit également un tableau d’états acceptables en tant que déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="da735-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="da735-122">Par exemple, si vous souhaitiez toorun après une réussite et également après étape B réussit ou échoue, vous construisez ce `runAfter` propriété :</span><span class="sxs-lookup"><span data-stu-id="da735-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="da735-123">Mettre à niveau votre schéma</span><span class="sxs-lookup"><span data-stu-id="da735-123">Upgrade your schema</span></span>

<span data-ttu-id="da735-124">Nouveau schéma de la mise à niveau toohello ne prend que quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="da735-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="da735-125">Hello mise à niveau implique l’exécution du script de mise à niveau hello, l’enregistrement comme nouvelle application logique et si vous le souhaitez, en remplaçant éventuellement application logique de la précédente hello.</span><span class="sxs-lookup"><span data-stu-id="da735-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="da735-126">Bonjour portail Azure, ouvrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="da735-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="da735-127">Accédez trop**vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="da735-127">Go too**Overview**.</span></span> <span data-ttu-id="da735-128">Dans la barre d’outils hello logique application, choisissez **mise à jour de schéma**.</span><span class="sxs-lookup"><span data-stu-id="da735-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Choisir l’option Mettre à jour le schéma][1]
   
    <span data-ttu-id="da735-130">Hello définition mise à niveau est retournée, que vous pouvez copier et coller dans une définition de ressource, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="da735-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="da735-131">Toutefois, nous **recommandons** vous choisissez **enregistrer en tant que** toomake assurer que toutes les références de connexion sont valides dans hello mis à niveau l’application logique.</span><span class="sxs-lookup"><span data-stu-id="da735-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="da735-132">Dans la barre d’outils du Panneau de mise à niveau de hello, choisissez **Enregistrer sous**.</span><span class="sxs-lookup"><span data-stu-id="da735-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="da735-133">Entrez l’état et le nom logique de hello.</span><span class="sxs-lookup"><span data-stu-id="da735-133">Enter hello logic name and status.</span></span> <span data-ttu-id="da735-134">toodeploy votre application de la logique de mise à niveau, choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="da735-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="da735-135">Vérifiez que votre application logique mise à niveau fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="da735-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="da735-136">Si vous utilisez un déclencheur manuel ou de la demande, URL de rappel hello change dans votre nouvelle application logique.</span><span class="sxs-lookup"><span data-stu-id="da735-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="da735-137">Fonctionnement de l’expérience test hello nouvelle URL toomake vraiment hello de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="da735-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="da735-138">toopreserve des URL précédentes, vous pouvez cloner sur votre application logique existant.</span><span class="sxs-lookup"><span data-stu-id="da735-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="da735-139">*Facultatif* choisir de votre application logique précédente avec hello nouvelle version du schéma, la barre d’outils hello toooverwrite **Clone**, en regard de trop**mise à jour de schéma**.</span><span class="sxs-lookup"><span data-stu-id="da735-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="da735-140">Cette étape est nécessaire uniquement si vous voulez tookeep hello même ressource ID ou demande URL du déclencheur de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="da735-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="da735-141">Notes de l’outil de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="da735-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="da735-142">Mappage de conditions</span><span class="sxs-lookup"><span data-stu-id="da735-142">Mapping conditions</span></span>

<span data-ttu-id="da735-143">Dans la définition de hello mis à niveau, outil de hello permet un meilleur effort à regrouper les actions de la branche true et false en tant qu’étendue.</span><span class="sxs-lookup"><span data-stu-id="da735-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="da735-144">Plus précisément, hello concepteur motif de `@equals(actions('a').status, 'Skipped')` doivent apparaître comme un `else` action.</span><span class="sxs-lookup"><span data-stu-id="da735-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="da735-145">Toutefois, si l’outil de hello détecte des séquences non reconnaissables, outil de hello peut créer des conditions séparées pour hello true et branche de false hello.</span><span class="sxs-lookup"><span data-stu-id="da735-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="da735-146">Vous pouvez remapper les actions après la mise à niveau si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="da735-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="da735-147">Boucle « foreach » avec condition</span><span class="sxs-lookup"><span data-stu-id="da735-147">'foreach' loop with condition</span></span>

<span data-ttu-id="da735-148">Dans le nouveau schéma de hello, vous pouvez utiliser le modèle de hello hello filtre action tooreplicate d’un `foreach` boucle avec une condition par élément, mais cette modification devrait se produire automatiquement lorsque vous mettez à niveau.</span><span class="sxs-lookup"><span data-stu-id="da735-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="da735-149">condition de Hello devienne une action de filtrage avant de boucle foreach de hello pour retourner uniquement un tableau d’éléments qui correspondent à la condition de hello, et ce tableau est passé à l’action de foreach hello.</span><span class="sxs-lookup"><span data-stu-id="da735-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="da735-150">Pour découvrir un exemple, consultez l’article relatif aux [boucles et étendues](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="da735-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="da735-151">Balises de ressource</span><span class="sxs-lookup"><span data-stu-id="da735-151">Resource tags</span></span>

<span data-ttu-id="da735-152">Une fois que vous mettez à niveau, les balises de ressources sont supprimés, donc vous devez les réinitialiser pour les flux de travail hello mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="da735-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="da735-153">Autres modifications</span><span class="sxs-lookup"><span data-stu-id="da735-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="da735-154">Renommer le déclencheur 'manual' too'request' déclencheur</span><span class="sxs-lookup"><span data-stu-id="da735-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="da735-155">Hello `manual` type de déclencheur a été déconseillée et renommé trop`request` avec le type `http`.</span><span class="sxs-lookup"><span data-stu-id="da735-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="da735-156">Cette modification crée plus de cohérence de type hello du modèle qui hello déclencheur est toobuild utilisé.</span><span class="sxs-lookup"><span data-stu-id="da735-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="da735-157">Nouvelle action de « filtre »</span><span class="sxs-lookup"><span data-stu-id="da735-157">New 'filter' action</span></span>

<span data-ttu-id="da735-158">toofilter un grand tableau vers le bas tooa plus petit jeu d’éléments, hello new `filter` type accepte un tableau et une condition, évalue la condition hello pour chaque élément et retourne un tableau avec les éléments répondant à la condition de hello.</span><span class="sxs-lookup"><span data-stu-id="da735-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="da735-159">Restrictions relatives aux actions « foreach » et « until »</span><span class="sxs-lookup"><span data-stu-id="da735-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="da735-160">Hello `foreach` et `until` boucle sont restreintes tooa une seule action.</span><span class="sxs-lookup"><span data-stu-id="da735-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="da735-161">Nouvelle propriété « trackedProperties » relative aux actions</span><span class="sxs-lookup"><span data-stu-id="da735-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="da735-162">Actions peuvent avoir maintenant une propriété supplémentaire appelée `trackedProperties`, qui est le frère toohello `runAfter` et `type` propriétés.</span><span class="sxs-lookup"><span data-stu-id="da735-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="da735-163">Cet objet spécifie certaines entrées d’action ou sorties que vous souhaitez tooinclude de télémétrie de Diagnostic Azure hello, émis dans le cadre d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="da735-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="da735-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="da735-164">For example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="da735-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da735-165">Next Steps</span></span>
* [<span data-ttu-id="da735-166">Créer des définitions d’application logique</span><span class="sxs-lookup"><span data-stu-id="da735-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="da735-167">Création d’un modèle de déploiement d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="da735-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
