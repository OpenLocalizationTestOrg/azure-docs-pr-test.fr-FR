---
title: "conditions d’aaaAdd et démarrer le flux de travail - Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="5b2c5-103">Utiliser les fonctionnalités des applications logiques</span><span class="sxs-lookup"><span data-stu-id="5b2c5-103">Use Logic Apps features</span></span>

<span data-ttu-id="5b2c5-104">Dans une [rubrique précédente](../logic-apps/logic-apps-create-a-logic-app.md), vous avez créé votre première application logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="5b2c5-105">toocontrol flux de travail de votre application logique, vous pouvez spécifier des chemins d’accès pour votre toorun d’application logique et comment trop de traiter les données dans les tableaux, les collections et les lots.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="5b2c5-106">Vous pouvez inclure les éléments suivants dans le workflow de votre application logique :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="5b2c5-107">Les conditions et les [instructions switch](../logic-apps/logic-apps-switch-case.md) permettent à votre application logique d’exécuter différentes actions si certaines conditions sont remplies ou non.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="5b2c5-108">Les [boucles](../logic-apps/logic-apps-loops-and-scopes.md) permettent à votre application logique d’exécuter des étapes à plusieurs reprises.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="5b2c5-109">Par exemple, vous pouvez répéter des actions sur un tableau en utilisant une boucle **For_each**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="5b2c5-110">Vous pouvez également répéter des actions jusqu’à ce qu’une condition soit remplie à l’aide d’une boucle **Until**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="5b2c5-111">[Étendues](../logic-apps/logic-apps-loops-and-scopes.md) permettent de vous regroupez série d’actions, par exemple, la gestion des exceptions tooimplement.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="5b2c5-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) permet à votre application logique de démarrer le flux de travail distinct pour les éléments dans un tableau quand vous utilisez hello **SplitOn** commande.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="5b2c5-113">Cette rubrique présente d’autres concepts utiles pour la création de votre application logique :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="5b2c5-114">Vue tooedit une application existante de la logique du code</span><span class="sxs-lookup"><span data-stu-id="5b2c5-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="5b2c5-115">options de démarrage d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="5b2c5-116">Conditions : exécuter des étapes uniquement lorsqu’une condition est remplie</span><span class="sxs-lookup"><span data-stu-id="5b2c5-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="5b2c5-117">toohave votre application logique exécutée des étapes uniquement lorsque les données satisfont aux critères spécifiques, vous pouvez ajouter une condition qui compare les données dans le flux de travail hello par rapport à des champs ou des valeurs.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="5b2c5-118">Par exemple, supposons que vous disposez d’une application logique qui vous envoie un trop grand nombre d’e-mails pour des publications sur le flux RSS d’un site web.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="5b2c5-119">Vous pouvez ajouter une condition afin que votre application logique envoie un e-mail uniquement lorsque hello nouvelle validation appartienne catégorie spécifique de tooa.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="5b2c5-120">Bonjour [portail Azure](https://portal.azure.com), recherchez et ouvrez votre application de logique dans le Concepteur de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="5b2c5-121">Ajouter un emplacement de flux de travail toohello condition que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="5b2c5-122">condition de hello tooadd entre les étapes d’un workflow d’application hello logique, pointent hello sur la flèche de hello où vous souhaitez la condition de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="5b2c5-123">Choisissez hello **signe** (**+**), puis choisissez **ajouter une condition**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="5b2c5-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-124">For example:</span></span>

   ![Ajouter une condition toologic application](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="5b2c5-126">Si vous souhaitez tooadd une condition à fin hello votre flux de travail en cours, accédez bas toohello de votre application logique, puis choisissez **+ nouvelle étape**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="5b2c5-127">Maintenant définir la condition de hello.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-127">Now define hello condition.</span></span> <span data-ttu-id="5b2c5-128">Spécifier le champ de source de hello que vous souhaitez tooevaluate, hello opération tooperform et valeur de cible de hello ou le champ.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="5b2c5-129">tooadd existant champs tooyour condition, choisissez hello **ajouter une liste de contenu dynamique**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="5b2c5-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-130">For example:</span></span>

   ![Modifier la condition en mode de base](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="5b2c5-132">Voici les conditions de saisie hello :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-132">Here's hello complete condition:</span></span>

   ![Condition complète](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="5b2c5-134">condition de hello toodefine dans le code, choisissez **modifier en mode avancé**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="5b2c5-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-135">For example:</span></span>
   > 
   > ![Modifier la condition dans le code](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="5b2c5-137">Sous **si Oui** et **si aucun**, ajouter tooperform d’étapes hello selon si hello condition est remplie.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="5b2c5-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-138">For example:</span></span>

   ![Condition avec les chemins SI OUI et SI NON](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="5b2c5-140">Vous pouvez faire glisser des actions existantes hello **si Oui** et **si aucun** chemins d’accès.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="5b2c5-141">Lorsque vous avez terminé, enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="5b2c5-142">Vous n’êtes e-mails uniquement lorsque hello publications répondent à la condition.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="5b2c5-143">Répétition des actions sur une liste à l’aide de forEach</span><span class="sxs-lookup"><span data-stu-id="5b2c5-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="5b2c5-144">boucle forEach de Hello spécifie un tableau de toorepeat une action de pointage.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="5b2c5-145">Si elle n’est pas un tableau, les flux hello échoue.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="5b2c5-146">Par exemple, si vous avez action1 qui génère un tableau de messages, et que vous souhaitez toosend chaque message, vous pouvez inclure cette instruction forEach dans les propriétés de votre action hello :`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="5b2c5-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="5b2c5-147">Modifier la définition de code hello pour une application de logique</span><span class="sxs-lookup"><span data-stu-id="5b2c5-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="5b2c5-148">Bien que vous avez hello Concepteur d’application logique, vous pouvez modifier directement le code hello qui définit une application logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="5b2c5-149">Dans la barre de commandes hello, choisissez **mode Code**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="5b2c5-150">Un éditeur complète s’ouvre et affiche les définition hello que vous avez modifié.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Mode code](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="5b2c5-152">Dans l’éditeur de texte hello, vous pouvez copier et coller n’importe quel nombre d’actions au sein de hello même application logique ou entre les applications de la logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="5b2c5-153">Vous pouvez également facilement ajouter ou supprimer des sections entières à partir de la définition de hello, et vous pouvez également partager les définitions avec d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="5b2c5-154">Choisissez de vos modifications, toosave **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="5b2c5-155">Paramètres</span><span class="sxs-lookup"><span data-stu-id="5b2c5-155">Parameters</span></span>

<span data-ttu-id="5b2c5-156">Certaines fonctionnalités de Logic Apps sont disponibles uniquement en mode code, les paramètres par exemple.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="5b2c5-157">Paramètres rendent tooreuse facile des valeurs dans l’ensemble de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="5b2c5-158">Par exemple, si vous avez une adresse de messagerie que vous souhaitez utiliser dans plusieurs actions, vous devez la définir en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="5b2c5-159">Les paramètres sont adaptés pour extraire les valeurs que vous êtes probablement toochange beaucoup.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="5b2c5-160">Ils sont particulièrement utiles lorsque vous avez besoin des paramètres toooverride dans différents environnements.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="5b2c5-161">toolearn toooverride basés sur l’environnement, voir [créer des définitions d’application logique](../logic-apps/logic-apps-author-definitions.md) et [documentation de l’API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="5b2c5-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="5b2c5-162">Cet exemple montre comment tooupdate votre application logique existant afin que vous pouvez utiliser des paramètres pour un terme de requête hello.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="5b2c5-163">Dans la vue code, recherchez hello `parameters : {}` de l’objet, puis ajoutez un `currentFeedUrl` objet :</span><span class="sxs-lookup"><span data-stu-id="5b2c5-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="5b2c5-164">Accédez toohello `When_a_feed-item_is_published` action, rechercher hello `queries` section et remplacez la valeur de requête hello avec :`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="5b2c5-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="5b2c5-165">toojoin deux ou plusieurs chaînes, vous pouvez également utiliser hello `concat` (fonction).</span><span class="sxs-lookup"><span data-stu-id="5b2c5-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="5b2c5-166">Par exemple, `"@concat('#',parameters('currentFeedUrl'))"` fonctionne même hello comme hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="5b2c5-167">Une fois ces opérations effectuées, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="5b2c5-168">Maintenant vous pouvez modifier flux RSS du hello du site Web en passant une autre URL via hello `currentFeedURL` objet.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="5b2c5-169">En savoir plus sur [comment définitions d’application logique tooauthor](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="5b2c5-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="5b2c5-170">Démarrage de workflows d’application logique</span><span class="sxs-lookup"><span data-stu-id="5b2c5-170">Start logic app workflows</span></span>

<span data-ttu-id="5b2c5-171">Vous disposez des options différentes pour le démarrage du workflow hello défini dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="5b2c5-172">Vous pouvez toujours démarrer une flux de travail à la demande dans hello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="5b2c5-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="5b2c5-173">Déclencheurs de périodicité</span><span class="sxs-lookup"><span data-stu-id="5b2c5-173">Recurrence triggers</span></span>

<span data-ttu-id="5b2c5-174">Un déclencheur de périodicité s'exécute selon un intervalle que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="5b2c5-175">Lorsque le déclencheur de hello possède une logique conditionnelle, déclencheur de hello détermine si le flux de travail hello doit toorun.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="5b2c5-176">Un déclencheur indique le flux de travail hello doit s’exécuter en retournant un `200` code d’état.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="5b2c5-177">Lorsque le flux de travail hello n’a pas besoin de toorun, le déclencheur de hello retourne un `202` code d’état.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="5b2c5-178">Rappel à l'aide des API REST</span><span class="sxs-lookup"><span data-stu-id="5b2c5-178">Callback using REST APIs</span></span>

<span data-ttu-id="5b2c5-179">toostart un flux de travail, les services peuvent appeler un point de terminaison application logique.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="5b2c5-180">Choisissez de ce genre de logique application à la demande, toostart **exécuter maintenant** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="5b2c5-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="5b2c5-181">Consultez la page [Démarrage des flux de travail en appelant les points de terminaison en tant que déclencheurs](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="5b2c5-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[portail Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="5b2c5-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b2c5-183">Next steps</span></span>

* [<span data-ttu-id="5b2c5-184">Instructions switch</span><span class="sxs-lookup"><span data-stu-id="5b2c5-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="5b2c5-185">Boucles, étendues et décomposition</span><span class="sxs-lookup"><span data-stu-id="5b2c5-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="5b2c5-186">Créer des définitions d’application logique</span><span class="sxs-lookup"><span data-stu-id="5b2c5-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)