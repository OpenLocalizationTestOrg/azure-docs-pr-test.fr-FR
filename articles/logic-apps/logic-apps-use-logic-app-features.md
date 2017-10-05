---
title: "Ajouter des conditions pour exécuter les workflows - Azure Logic Apps | Microsoft Docs"
description: "Contrôlez le mode d’exécution des workflows dans Azure Logic Apps en ajoutant une logique conditionnelle, des déclencheurs, des actions et des paramètres."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="b64ef-103">Utiliser les fonctionnalités des applications logiques</span><span class="sxs-lookup"><span data-stu-id="b64ef-103">Use Logic Apps features</span></span>

<span data-ttu-id="b64ef-104">Dans une [rubrique précédente](../logic-apps/logic-apps-create-a-logic-app.md), vous avez créé votre première application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="b64ef-105">Pour contrôler le workflow de votre application logique, vous pouvez définir des chemins d’accès différents pour l’exécution de votre application logique et spécifier comment traiter les données dans des tableaux, des collections et des lots.</span><span class="sxs-lookup"><span data-stu-id="b64ef-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="b64ef-106">Vous pouvez inclure les éléments suivants dans le workflow de votre application logique :</span><span class="sxs-lookup"><span data-stu-id="b64ef-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="b64ef-107">Les conditions et les [instructions switch](../logic-apps/logic-apps-switch-case.md) permettent à votre application logique d’exécuter différentes actions si certaines conditions sont remplies ou non.</span><span class="sxs-lookup"><span data-stu-id="b64ef-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="b64ef-108">Les [boucles](../logic-apps/logic-apps-loops-and-scopes.md) permettent à votre application logique d’exécuter des étapes à plusieurs reprises.</span><span class="sxs-lookup"><span data-stu-id="b64ef-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="b64ef-109">Par exemple, vous pouvez répéter des actions sur un tableau en utilisant une boucle **For_each**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="b64ef-110">Vous pouvez également répéter des actions jusqu’à ce qu’une condition soit remplie à l’aide d’une boucle **Until**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="b64ef-111">Les [étendues](../logic-apps/logic-apps-loops-and-scopes.md) permettent de regrouper des séries d’actions, par exemple pour mettre en œuvre la gestion des exceptions.</span><span class="sxs-lookup"><span data-stu-id="b64ef-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="b64ef-112">La [décomposition](../logic-apps/logic-apps-loops-and-scopes.md) permet à votre application logique de démarrer des workflows distincts pour les éléments d’un tableau lorsque vous utilisez la commande **SplitOn**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="b64ef-113">Cette rubrique présente d’autres concepts utiles pour la création de votre application logique :</span><span class="sxs-lookup"><span data-stu-id="b64ef-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="b64ef-114">mode code pour modifier une application logique existante ;</span><span class="sxs-lookup"><span data-stu-id="b64ef-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="b64ef-115">options de démarrage d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="b64ef-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="b64ef-116">Conditions : exécuter des étapes uniquement lorsqu’une condition est remplie</span><span class="sxs-lookup"><span data-stu-id="b64ef-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="b64ef-117">Pour que votre application logique exécute des étapes uniquement lorsque les données remplissent des critères spécifiques, vous pouvez ajouter une condition qui compare les données du workflow à des champs ou des valeurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="b64ef-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="b64ef-118">Par exemple, supposons que vous disposez d’une application logique qui vous envoie un trop grand nombre d’e-mails pour des publications sur le flux RSS d’un site web.</span><span class="sxs-lookup"><span data-stu-id="b64ef-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="b64ef-119">Vous pouvez ajouter une condition afin que votre application logique envoie un e-mail uniquement lorsque la nouvelle publication appartient à une catégorie spécifique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="b64ef-120">Dans le [portail Azure](https://portal.azure.com), recherchez et ouvrez votre application logique dans le concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="b64ef-121">Ajoutez une condition dans le workflow à l’emplacement souhaité.</span><span class="sxs-lookup"><span data-stu-id="b64ef-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="b64ef-122">Pour ajouter la condition entre des étapes existantes du workflow de l’application logique, déplacez le pointeur sur la flèche où vous voulez ajouter la condition.</span><span class="sxs-lookup"><span data-stu-id="b64ef-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="b64ef-123">Cliquez sur le **signe plus** (**+**), puis choisissez **Ajouter une condition**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="b64ef-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b64ef-124">For example:</span></span>

   ![Ajouter une condition à l’application logique](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="b64ef-126">Si vous souhaitez ajouter une condition à la fin de votre workflow actuel, accédez au bas de votre application logique et sélectionnez **+ Nouvelle étape**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="b64ef-127">Maintenant, définissez la condition.</span><span class="sxs-lookup"><span data-stu-id="b64ef-127">Now define the condition.</span></span> <span data-ttu-id="b64ef-128">Spécifiez le champ source à évaluer, l’opération à effectuer et la valeur ou le champ cible.</span><span class="sxs-lookup"><span data-stu-id="b64ef-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="b64ef-129">Pour ajouter des champs existants à votre condition, utilisez la liste **Ajouter du contenu dynamique**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="b64ef-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b64ef-130">For example:</span></span>

   ![Modifier la condition en mode de base](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="b64ef-132">Voici la condition complète :</span><span class="sxs-lookup"><span data-stu-id="b64ef-132">Here's the complete condition:</span></span>

   ![Condition complète](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="b64ef-134">Pour définir la condition dans le code, choisissez **Modifier en mode Avancé**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="b64ef-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b64ef-135">For example:</span></span>
   > 
   > ![Modifier la condition dans le code](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="b64ef-137">Sous **SI OUI** et **SI NON**, ajoutez les étapes à effectuer si la condition est remplie ou non.</span><span class="sxs-lookup"><span data-stu-id="b64ef-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="b64ef-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b64ef-138">For example:</span></span>

   ![Condition avec les chemins SI OUI et SI NON](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="b64ef-140">Vous pouvez faire glisser des actions existantes dans les chemins **SI OUI** et **SI NON**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="b64ef-141">Lorsque vous avez terminé, enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="b64ef-142">À présent, vous ne recevrez des e-mails que lorsque les publications remplissent votre condition.</span><span class="sxs-lookup"><span data-stu-id="b64ef-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="b64ef-143">Répétition des actions sur une liste à l’aide de forEach</span><span class="sxs-lookup"><span data-stu-id="b64ef-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="b64ef-144">La boucle forEach spécifie un tableau sur lequel répéter une action.</span><span class="sxs-lookup"><span data-stu-id="b64ef-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="b64ef-145">Le flux échouera s’il ne se présente pas sous la forme d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="b64ef-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="b64ef-146">Par exemple, si action1 génère un tableau de messages et que vous souhaitez envoyer chaque message, vous pouvez inclure cette instruction forEach dans les propriétés de votre action : `forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="b64ef-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="b64ef-147">Modification de la définition du code pour une application logique</span><span class="sxs-lookup"><span data-stu-id="b64ef-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="b64ef-148">Même si vous avez le concepteur d’applications logiques, vous pouvez modifier directement le code qui définit une application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="b64ef-149">Dans la barre de commandes, choisissez **Mode Code**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="b64ef-150">Cela ouvre un éditeur complet qui affiche la définition que vous venez de modifier.</span><span class="sxs-lookup"><span data-stu-id="b64ef-150">A full editor opens and shows the definition you edited.</span></span>

    ![Mode code](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="b64ef-152">Dans l'éditeur de texte, vous pouvez copier et coller les actions de votre choix dans la même application logique ou d'une application logique vers une autre.</span><span class="sxs-lookup"><span data-stu-id="b64ef-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="b64ef-153">Vous pouvez aussi ajouter ou supprimer facilement des sections entières de la définition et partager des définitions avec d'autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b64ef-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="b64ef-154">Pour enregistrer vos modifications, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="b64ef-155">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b64ef-155">Parameters</span></span>

<span data-ttu-id="b64ef-156">Certaines fonctionnalités de Logic Apps sont disponibles uniquement en mode code, les paramètres par exemple.</span><span class="sxs-lookup"><span data-stu-id="b64ef-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="b64ef-157">Les paramètres simplifient la réutilisation des valeurs dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="b64ef-158">Par exemple, si vous avez une adresse de messagerie que vous souhaitez utiliser dans plusieurs actions, vous devez la définir en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="b64ef-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="b64ef-159">Les paramètres constituent un bon moyen d'extraire des valeurs que vous êtes susceptible de modifier souvent.</span><span class="sxs-lookup"><span data-stu-id="b64ef-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="b64ef-160">Ils sont particulièrement utiles quand vous devez substituer des paramètres dans différents environnements.</span><span class="sxs-lookup"><span data-stu-id="b64ef-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="b64ef-161">Pour découvrir comment substituer des paramètres en fonction de l’environnement, consultez [Créer des définitions d’application logique](../logic-apps/logic-apps-author-definitions.md) et la [documentation de l’API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="b64ef-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="b64ef-162">L’exemple montre comment mettre à jour votre application logique existante pour utiliser des paramètres pour le terme de requête.</span><span class="sxs-lookup"><span data-stu-id="b64ef-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="b64ef-163">En mode code, recherchez l’objet `parameters : {}` et ajoutez un objet `currentFeedUrl` :</span><span class="sxs-lookup"><span data-stu-id="b64ef-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="b64ef-164">Naviguez jusqu’à l’action `When_a_feed-item_is_published`, recherchez la section `queries` et remplacez la valeur de la requête par `"feedUrl": "#@{parameters('currentFeedUrl')}"`.</span><span class="sxs-lookup"><span data-stu-id="b64ef-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="b64ef-165">Pour joindre deux chaînes ou plus, vous pouvez également utiliser la fonction `concat`.</span><span class="sxs-lookup"><span data-stu-id="b64ef-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="b64ef-166">Par exemple, `"@concat('#',parameters('currentFeedUrl'))"` est la même que ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b64ef-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="b64ef-167">Une fois ces opérations effectuées, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b64ef-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="b64ef-168">Vous pouvez maintenant modifier le flux RSS du site web en transmettant une autre URL via l’objet `currentFeedURL`.</span><span class="sxs-lookup"><span data-stu-id="b64ef-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="b64ef-169">En savoir plus sur la [création de définitions d’application logique](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="b64ef-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="b64ef-170">Démarrage de workflows d’application logique</span><span class="sxs-lookup"><span data-stu-id="b64ef-170">Start logic app workflows</span></span>

<span data-ttu-id="b64ef-171">Vous avez plusieurs options pour démarrer le flux de travail défini dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="b64ef-172">Vous pouvez toujours démarrer un flux de travail à la demande dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="b64ef-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="b64ef-173">Déclencheurs de périodicité</span><span class="sxs-lookup"><span data-stu-id="b64ef-173">Recurrence triggers</span></span>

<span data-ttu-id="b64ef-174">Un déclencheur de périodicité s'exécute selon un intervalle que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="b64ef-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="b64ef-175">Quand le déclencheur a une logique conditionnelle, il détermine si le flux de travail doit s'exécuter ou non.</span><span class="sxs-lookup"><span data-stu-id="b64ef-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="b64ef-176">Un déclencheur indique que le workflow doit s’exécuter en retournant un code d’état `200` .</span><span class="sxs-lookup"><span data-stu-id="b64ef-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="b64ef-177">Lorsque le workflow n’a pas besoin de s’exécuter, le déclencheur renvoie un code d’état `202`.</span><span class="sxs-lookup"><span data-stu-id="b64ef-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="b64ef-178">Rappel à l'aide des API REST</span><span class="sxs-lookup"><span data-stu-id="b64ef-178">Callback using REST APIs</span></span>

<span data-ttu-id="b64ef-179">Pour démarrer un workflow, les services peuvent appeler un point de terminaison d'application logique.</span><span class="sxs-lookup"><span data-stu-id="b64ef-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="b64ef-180">Pour démarrer ce type d’application logique à la demande, choisissez **Exécuter maintenant** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="b64ef-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="b64ef-181">Consultez la page [Démarrage des flux de travail en appelant les points de terminaison en tant que déclencheurs](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b64ef-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="b64ef-182">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b64ef-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="b64ef-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b64ef-183">Next steps</span></span>

* [<span data-ttu-id="b64ef-184">Instructions switch</span><span class="sxs-lookup"><span data-stu-id="b64ef-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="b64ef-185">Boucles, étendues et décomposition</span><span class="sxs-lookup"><span data-stu-id="b64ef-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="b64ef-186">Créer des définitions d’application logique</span><span class="sxs-lookup"><span data-stu-id="b64ef-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)