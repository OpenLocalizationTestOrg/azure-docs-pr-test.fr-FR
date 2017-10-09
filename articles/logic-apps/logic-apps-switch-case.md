---
title: "instruction aaaSwitch pour différentes actions dans Azure Logic Apps | Documents Microsoft"
description: "Choisissez tooperform de différentes actions dans les applications de la logique selon les valeurs de l’expression à l’aide d’une instruction switch"
services: logic-apps
keywords: instruction switch
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="70e76-104">Effectuer différentes actions dans les applications logiques avec une instruction switch</span><span class="sxs-lookup"><span data-stu-id="70e76-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="70e76-105">Lorsque vous créez un flux de travail, vous avez généralement tootake différentes actions selon la valeur hello d’un objet ou une expression.</span><span class="sxs-lookup"><span data-stu-id="70e76-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="70e76-106">Par exemple, vous pourriez votre toobehave d’application logique varie en fonction de code d’état hello d’une requête HTTP, ou une option sélectionnée dans un message électronique.</span><span class="sxs-lookup"><span data-stu-id="70e76-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="70e76-107">Ces scénarios, vous pouvez utiliser un tooimplement d’instruction switch.</span><span class="sxs-lookup"><span data-stu-id="70e76-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="70e76-108">Votre application logique peut évaluer un jeton ou une expression, puis choisissez cas hello avec hello même hello tooexecute de valeur spécifiée des actions.</span><span class="sxs-lookup"><span data-stu-id="70e76-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="70e76-109">Qu’un seul cas doit correspondre à l’instruction switch hello.</span><span class="sxs-lookup"><span data-stu-id="70e76-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="70e76-110">Comme dans tous les langages de programmation, les instructions switch ne prennent en charge que les opérateurs d’égalité.</span><span class="sxs-lookup"><span data-stu-id="70e76-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="70e76-111">Si vous avez besoin d’autres opérateurs relationnels, par exemple « supérieur à », utilisez une instruction de condition.</span><span class="sxs-lookup"><span data-stu-id="70e76-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="70e76-112">comportement de l’exécution déterministe tooensure, cas doivent contenir une valeur unique et statique au lieu de jetons dynamiques ou une expression.</span><span class="sxs-lookup"><span data-stu-id="70e76-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70e76-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="70e76-113">Prerequisites</span></span>

- <span data-ttu-id="70e76-114">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="70e76-114">An active Azure subscription.</span></span> <span data-ttu-id="70e76-115">Si vous n’avez pas d’abonnement Azure actif, créez un [compte gratuit](https://azure.microsoft.com/free/) ou essayez [Logic Apps gratuitement](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="70e76-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="70e76-116">Connaissance de base des applications logiques</span><span class="sxs-lookup"><span data-stu-id="70e76-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="70e76-117">Ajouter un flux de travail du tooyour instruction switch</span><span class="sxs-lookup"><span data-stu-id="70e76-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="70e76-118">tooshow le fonctionne d’une instruction switch, cet exemple crée une application de la logique que surveille les fichiers téléchargement tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="70e76-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="70e76-119">Lorsque de nouveaux fichiers de hello sont téléchargés, application logique de hello envoie par courrier électronique tooan approbateur choisit si tootransfer tooSharePoint de ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="70e76-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="70e76-120">application Hello utilise une instruction switch qui effectue des actions différentes en fonction de la valeur de hello hello approbateur sélectionne.</span><span class="sxs-lookup"><span data-stu-id="70e76-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="70e76-121">Créez une application logique, puis sélectionnez ce déclencheur : **Dropbox - Lorsqu’un fichier est créé**.</span><span class="sxs-lookup"><span data-stu-id="70e76-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Utiliser le déclencheur Dropbox - When a file is created (Dropbox - Lorsqu’un fichier est créé)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="70e76-123">Sous le déclencheur de hello, ajoutez cette action : **Outlook.com - envoyer un e-mail approbation**</span><span class="sxs-lookup"><span data-stu-id="70e76-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="70e76-124">Les applications logiques prennent également en charge les scénarios d’envoi d’un e-mail d’approbation à partir d’un compte Outlook Office 365.</span><span class="sxs-lookup"><span data-stu-id="70e76-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="70e76-125">Si vous n’avez pas une connexion existante, vous êtes invité à entrer toocreate une.</span><span class="sxs-lookup"><span data-stu-id="70e76-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="70e76-126">Renseignez les champs hello requis.</span><span class="sxs-lookup"><span data-stu-id="70e76-126">Fill in hello required fields.</span></span> <span data-ttu-id="70e76-127">Par exemple, sous **à**, spécifier l’adresse de messagerie hello approbateur hello est envoyé.</span><span class="sxs-lookup"><span data-stu-id="70e76-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="70e76-128">Sous **Options utilisateur**, entrez `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="70e76-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configurer la connexion](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="70e76-130">Ajoutez une instruction switch.</span><span class="sxs-lookup"><span data-stu-id="70e76-130">Add a switch statement.</span></span>

   - <span data-ttu-id="70e76-131">Sélectionnez **+ Nouvelle étape** > **... Plus** > **Ajouter un cas switch**.</span><span class="sxs-lookup"><span data-stu-id="70e76-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="70e76-132">Maintenant, nous souhaitons tooselect hello action tooperform selon hello `SelectedOptions` la sortie à partir de hello *envoyer un courrier électronique d’approbation* action.</span><span class="sxs-lookup"><span data-stu-id="70e76-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="70e76-133">Vous pouvez trouver ce champ Bonjour **ajouter du contenu dynamique** sélecteur.</span><span class="sxs-lookup"><span data-stu-id="70e76-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="70e76-134">Utilisez *cas 1* toohandle lors de l’approbateur de hello sélectionne `Approve`.</span><span class="sxs-lookup"><span data-stu-id="70e76-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="70e76-135">Si approuvée, copiez hello d’origine fichier tooSharePoint en ligne avec hello [ **SharePoint Online - créer le fichier** action](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="70e76-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="70e76-136">Ajouter une autre action, les utilisateurs de cas toonotify hello qu’un nouveau fichier est disponible sur SharePoint.</span><span class="sxs-lookup"><span data-stu-id="70e76-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="70e76-137">Ajouter un autre toohandle cas lorsque l’utilisateur sélectionne `Reject`.</span><span class="sxs-lookup"><span data-stu-id="70e76-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="70e76-138">Si rejetée, envoyez un courrier électronique de notification pour informer les autres approbateurs que le fichier hello est rejeté et aucune action supplémentaire n’est requise.</span><span class="sxs-lookup"><span data-stu-id="70e76-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="70e76-139">`SelectedOptions`fournit uniquement deux options, donc nous pouvons conserver hello **par défaut** cas vide.</span><span class="sxs-lookup"><span data-stu-id="70e76-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Instruction switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="70e76-141">Une instruction switch a besoin d’au moins un cas dans le cas par défaut de toohello Ajout.</span><span class="sxs-lookup"><span data-stu-id="70e76-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="70e76-142">Après l’instruction switch hello, supprimer hello d’origine fichier téléchargé tooDropbox en ajoutant cette action : **Dropbox - supprimer le fichier**</span><span class="sxs-lookup"><span data-stu-id="70e76-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="70e76-143">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="70e76-143">Save your logic app.</span></span> <span data-ttu-id="70e76-144">Testez votre application en chargeant un fichier tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="70e76-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="70e76-145">Vous recevrez sous peu un e-mail d’approbation.</span><span class="sxs-lookup"><span data-stu-id="70e76-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="70e76-146">Sélectionnez une option et observer le comportement de hello.</span><span class="sxs-lookup"><span data-stu-id="70e76-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="70e76-147">Découvrez comment faire trop[surveiller vos applications logiques](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="70e76-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="70e76-148">Comprendre le code hello derrière les instructions switch</span><span class="sxs-lookup"><span data-stu-id="70e76-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="70e76-149">Maintenant que vous avez créé avec succès une application de logique à l’aide d’une instruction switch, examinons définition de code hello derrière l’instruction switch hello.</span><span class="sxs-lookup"><span data-stu-id="70e76-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="70e76-150">`"Switch"`désigne hello hello de l’instruction switch, que vous pouvez renommer pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="70e76-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="70e76-151">`"type": "Switch"`Indique que les actions hello sont une instruction switch.</span><span class="sxs-lookup"><span data-stu-id="70e76-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="70e76-152">`"expression"`est l’option sélectionnée de l’approbateur hello dans cet exemple et est évaluée par rapport à chaque cas déclarée plus loin dans la définition de hello.</span><span class="sxs-lookup"><span data-stu-id="70e76-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="70e76-153">`"cases"` peut contenir une infinité de cas.</span><span class="sxs-lookup"><span data-stu-id="70e76-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="70e76-154">Pour chaque cas, `"Case *"` est le nom par défaut hello cas hello, que vous pouvez renommer pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="70e76-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="70e76-155">`"case"`Spécifie l’étiquette case hello, qui hello commutateur utilisation d’expressions de comparaison et doit être une valeur constante et unique.</span><span class="sxs-lookup"><span data-stu-id="70e76-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="70e76-156">Si aucun des cas de hello correspond à l’expression de switch hello, actions sous `"default"` sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="70e76-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="70e76-157">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="70e76-157">Get help</span></span>

<span data-ttu-id="70e76-158">tooask questions, répondez aux questions et voir les autres utilisateurs Azure Logic Apps font, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="70e76-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="70e76-159">toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="70e76-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70e76-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70e76-160">Next steps</span></span>

- <span data-ttu-id="70e76-161">Découvrez comment trop[ajouter des conditions](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="70e76-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="70e76-162">En savoir plus sur la [gestion des erreurs et des exceptions](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="70e76-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="70e76-163">Découvrir d’autres [fonctionnalités en matière de langage de flux de travail](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="70e76-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>