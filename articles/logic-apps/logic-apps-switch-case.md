---
title: "Instruction switch pour différentes actions dans Azure Logic Apps | Microsoft Docs"
description: "Choisissez les différentes actions à effectuer dans les applications logiques en fonction des valeurs d’une expression avec une instruction switch."
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
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="f0efd-104">Effectuer différentes actions dans les applications logiques avec une instruction switch</span><span class="sxs-lookup"><span data-stu-id="f0efd-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="f0efd-105">Lorsque vous créez un flux de travail, vous êtes souvent amené à exécuter des actions différentes selon la valeur d’un objet ou d’une expression.</span><span class="sxs-lookup"><span data-stu-id="f0efd-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="f0efd-106">Par exemple, vous pouvez avoir besoin que votre application logique se comporte différemment selon le code d’état d’une demande HTTP ou l’option sélectionnée dans un e-mail.</span><span class="sxs-lookup"><span data-stu-id="f0efd-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="f0efd-107">Vous pouvez utiliser une instruction switch pour mettre en place ces scénarios.</span><span class="sxs-lookup"><span data-stu-id="f0efd-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="f0efd-108">Votre application logique peut évaluer un jeton ou une expression, et choisir le cas correspondant à la même valeur pour exécuter les actions spécifiées.</span><span class="sxs-lookup"><span data-stu-id="f0efd-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="f0efd-109">L’instruction switch ne doit correspondre qu’à un seul cas de figure.</span><span class="sxs-lookup"><span data-stu-id="f0efd-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="f0efd-110">Comme dans tous les langages de programmation, les instructions switch ne prennent en charge que les opérateurs d’égalité.</span><span class="sxs-lookup"><span data-stu-id="f0efd-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="f0efd-111">Si vous avez besoin d’autres opérateurs relationnels, par exemple « supérieur à », utilisez une instruction de condition.</span><span class="sxs-lookup"><span data-stu-id="f0efd-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="f0efd-112">Pour garantir un comportement d’exécution constant, les cas de figure doivent contenir une valeur statique unique et non des jetons ou une expression dynamiques.</span><span class="sxs-lookup"><span data-stu-id="f0efd-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0efd-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f0efd-113">Prerequisites</span></span>

- <span data-ttu-id="f0efd-114">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="f0efd-114">An active Azure subscription.</span></span> <span data-ttu-id="f0efd-115">Si vous n’avez pas d’abonnement Azure actif, créez un [compte gratuit](https://azure.microsoft.com/free/) ou essayez [Logic Apps gratuitement](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f0efd-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="f0efd-116">Connaissance de base des applications logiques</span><span class="sxs-lookup"><span data-stu-id="f0efd-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="f0efd-117">Ajouter une instruction switch à un flux de travail</span><span class="sxs-lookup"><span data-stu-id="f0efd-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="f0efd-118">Pour illustrer le fonctionnement d’une instruction switch, cet exemple crée une application logique qui surveille les fichiers chargés sur Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f0efd-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="f0efd-119">Lorsque les nouveaux fichiers sont chargés, l’application logique envoie un e-mail à un approbateur qui décide s’il faut transférer ces fichiers vers SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f0efd-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="f0efd-120">L’application utilise une instruction switch qui effectue des actions différentes selon la valeur sélectionnée de l’approbateur.</span><span class="sxs-lookup"><span data-stu-id="f0efd-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="f0efd-121">Créez une application logique, puis sélectionnez ce déclencheur : **Dropbox - Lorsqu’un fichier est créé**.</span><span class="sxs-lookup"><span data-stu-id="f0efd-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Utiliser le déclencheur Dropbox - When a file is created (Dropbox - Lorsqu’un fichier est créé)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="f0efd-123">Sous le déclencheur, ajoutez cette action : **Outlook.com - Envoyer un e-mail d’approbation**.</span><span class="sxs-lookup"><span data-stu-id="f0efd-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="f0efd-124">Les applications logiques prennent également en charge les scénarios d’envoi d’un e-mail d’approbation à partir d’un compte Outlook Office 365.</span><span class="sxs-lookup"><span data-stu-id="f0efd-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="f0efd-125">Si vous ne disposez pas d’une connexion, vous êtes invité à en créer une.</span><span class="sxs-lookup"><span data-stu-id="f0efd-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="f0efd-126">Renseignez les champs obligatoires.</span><span class="sxs-lookup"><span data-stu-id="f0efd-126">Fill in the required fields.</span></span> <span data-ttu-id="f0efd-127">Par exemple, sous **À**, spécifiez l’adresse e-mail à laquelle l’e-mail de l’approbateur sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="f0efd-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="f0efd-128">Sous **Options utilisateur**, entrez `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="f0efd-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configurer la connexion](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="f0efd-130">Ajoutez une instruction switch.</span><span class="sxs-lookup"><span data-stu-id="f0efd-130">Add a switch statement.</span></span>

   - <span data-ttu-id="f0efd-131">Sélectionnez **+ Nouvelle étape** > **... Plus** > **Ajouter un cas switch**.</span><span class="sxs-lookup"><span data-stu-id="f0efd-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="f0efd-132">Nous allons à présent sélectionner l’action à effectuer en fonction de la sortie `SelectedOptions` de l’action *Envoyer un e-mail d’approbation*.</span><span class="sxs-lookup"><span data-stu-id="f0efd-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="f0efd-133">Ce champ se trouve dans le sélecteur **Ajouter du contenu dynamique**.</span><span class="sxs-lookup"><span data-stu-id="f0efd-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="f0efd-134">Utilisez *Cas 1* pour gérer la sélection de `Approve` par l’approbateur.</span><span class="sxs-lookup"><span data-stu-id="f0efd-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="f0efd-135">En cas d’approbation, copiez le fichier d’origine dans SharePoint Online avec [l’action **SharePoint Online - Créer un fichier**](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="f0efd-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="f0efd-136">Ajoutez une autre action au cas de figure pour notifier les utilisateurs qu’un nouveau fichier est disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f0efd-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="f0efd-137">Ajoutez un autre cas de figure pour gérer la sélection de `Reject` par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f0efd-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="f0efd-138">En cas de refus, envoyez un message électronique de notification informant les autres approbateurs que le fichier a été rejeté et qu’aucune action supplémentaire n’est requise.</span><span class="sxs-lookup"><span data-stu-id="f0efd-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="f0efd-139">`SelectedOptions` fournit uniquement deux options ; nous pouvons donc laisser vide le cas **Par défaut**.</span><span class="sxs-lookup"><span data-stu-id="f0efd-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Instruction switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="f0efd-141">Une instruction switch requiert au moins un cas de figure en plus du cas par défaut.</span><span class="sxs-lookup"><span data-stu-id="f0efd-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="f0efd-142">Après l’instruction switch, supprimez le fichier d’origine chargé sur la Dropbox en ajoutant cette action : **Dropbox - Supprimer le fichier**.</span><span class="sxs-lookup"><span data-stu-id="f0efd-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="f0efd-143">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="f0efd-143">Save your logic app.</span></span> <span data-ttu-id="f0efd-144">Testez votre application en chargeant un fichier sur Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f0efd-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="f0efd-145">Vous recevrez sous peu un e-mail d’approbation.</span><span class="sxs-lookup"><span data-stu-id="f0efd-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="f0efd-146">Sélectionnez une option et observez le comportement.</span><span class="sxs-lookup"><span data-stu-id="f0efd-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="f0efd-147">Découvrez comment [surveiller vos applications logiques](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f0efd-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="f0efd-148">Comprendre le code derrière les instructions switch</span><span class="sxs-lookup"><span data-stu-id="f0efd-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="f0efd-149">Maintenant que vous avez créé une application logique avec une instruction switch, examinons la définition de code derrière l’instruction switch.</span><span class="sxs-lookup"><span data-stu-id="f0efd-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

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

* <span data-ttu-id="f0efd-150">`"Switch"` est le nom de l’instruction switch, que vous pouvez modifier pour plus de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="f0efd-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="f0efd-151">`"type": "Switch"` indique que l’action est une instruction switch.</span><span class="sxs-lookup"><span data-stu-id="f0efd-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="f0efd-152">`"expression"` est l’option sélectionnée par l’approbateur dans cet exemple ; elle est confrontée à chacun des cas déclarés plus loin dans la définition.</span><span class="sxs-lookup"><span data-stu-id="f0efd-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="f0efd-153">`"cases"` peut contenir une infinité de cas.</span><span class="sxs-lookup"><span data-stu-id="f0efd-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="f0efd-154">Pour chaque cas, `"Case *"` est le nom par défaut du cas, que vous pouvez modifier pour plus de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="f0efd-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="f0efd-155">`"case"` spécifie l’étiquette du cas, utilisée par l’expression switch à des fins de comparaison. Il doit s’agir d’une valeur unique et constante.</span><span class="sxs-lookup"><span data-stu-id="f0efd-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="f0efd-156">Si aucun des cas ne correspond à l’expression switch, les actions sous `"default"` sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="f0efd-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="f0efd-157">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="f0efd-157">Get help</span></span>

<span data-ttu-id="f0efd-158">Pour poser des questions, répondre aux questions et voir ce que font les autres utilisateurs d’Azure Logic Apps, visitez le [Forum Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="f0efd-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="f0efd-159">Afin d’améliorer Azure Logic Apps ainsi que les connecteurs, votez pour des idées ou soumettez-en sur le [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="f0efd-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0efd-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0efd-160">Next steps</span></span>

- <span data-ttu-id="f0efd-161">Apprendre à [ajouter des conditions](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="f0efd-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="f0efd-162">En savoir plus sur la [gestion des erreurs et des exceptions](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="f0efd-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="f0efd-163">Découvrir d’autres [fonctionnalités en matière de langage de flux de travail](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="f0efd-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>