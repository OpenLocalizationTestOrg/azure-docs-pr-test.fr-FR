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
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Effectuer différentes actions dans les applications logiques avec une instruction switch

Lorsque vous créez un flux de travail, vous avez généralement tootake différentes actions selon la valeur hello d’un objet ou une expression. Par exemple, vous pourriez votre toobehave d’application logique varie en fonction de code d’état hello d’une requête HTTP, ou une option sélectionnée dans un message électronique.

Ces scénarios, vous pouvez utiliser un tooimplement d’instruction switch. Votre application logique peut évaluer un jeton ou une expression, puis choisissez cas hello avec hello même hello tooexecute de valeur spécifiée des actions. Qu’un seul cas doit correspondre à l’instruction switch hello.

> [!TIP]
> Comme dans tous les langages de programmation, les instructions switch ne prennent en charge que les opérateurs d’égalité. Si vous avez besoin d’autres opérateurs relationnels, par exemple « supérieur à », utilisez une instruction de condition.
> comportement de l’exécution déterministe tooensure, cas doivent contenir une valeur unique et statique au lieu de jetons dynamiques ou une expression.

## <a name="prerequisites"></a>Composants requis

- Un abonnement Azure actif. Si vous n’avez pas d’abonnement Azure actif, créez un [compte gratuit](https://azure.microsoft.com/free/) ou essayez [Logic Apps gratuitement](https://tryappservice.azure.com/).
- [Connaissance de base des applications logiques](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Ajouter un flux de travail du tooyour instruction switch

tooshow le fonctionne d’une instruction switch, cet exemple crée une application de la logique que surveille les fichiers téléchargement tooDropbox. Lorsque de nouveaux fichiers de hello sont téléchargés, application logique de hello envoie par courrier électronique tooan approbateur choisit si tootransfer tooSharePoint de ces fichiers. application Hello utilise une instruction switch qui effectue des actions différentes en fonction de la valeur de hello hello approbateur sélectionne.

1. Créez une application logique, puis sélectionnez ce déclencheur : **Dropbox - Lorsqu’un fichier est créé**.

   ![Utiliser le déclencheur Dropbox - When a file is created (Dropbox - Lorsqu’un fichier est créé)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Sous le déclencheur de hello, ajoutez cette action : **Outlook.com - envoyer un e-mail approbation**

   > [!TIP]
   > Les applications logiques prennent également en charge les scénarios d’envoi d’un e-mail d’approbation à partir d’un compte Outlook Office 365.

   - Si vous n’avez pas une connexion existante, vous êtes invité à entrer toocreate une.
   - Renseignez les champs hello requis. Par exemple, sous **à**, spécifier l’adresse de messagerie hello approbateur hello est envoyé.
   - Sous **Options utilisateur**, entrez `Approve, Reject`.

   ![Configurer la connexion](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Ajoutez une instruction switch.

   - Sélectionnez **+ Nouvelle étape** > **... Plus** > **Ajouter un cas switch**. 
   - Maintenant, nous souhaitons tooselect hello action tooperform selon hello `SelectedOptions` la sortie à partir de hello *envoyer un courrier électronique d’approbation* action. 
   Vous pouvez trouver ce champ Bonjour **ajouter du contenu dynamique** sélecteur.
   - Utilisez *cas 1* toohandle lors de l’approbateur de hello sélectionne `Approve`.
     - Si approuvée, copiez hello d’origine fichier tooSharePoint en ligne avec hello [ **SharePoint Online - créer le fichier** action](../connectors/connectors-create-api-sharepointonline.md).
     - Ajouter une autre action, les utilisateurs de cas toonotify hello qu’un nouveau fichier est disponible sur SharePoint.
   - Ajouter un autre toohandle cas lorsque l’utilisateur sélectionne `Reject`.
     - Si rejetée, envoyez un courrier électronique de notification pour informer les autres approbateurs que le fichier hello est rejeté et aucune action supplémentaire n’est requise.
   - `SelectedOptions`fournit uniquement deux options, donc nous pouvons conserver hello **par défaut** cas vide.

   ![Instruction switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Une instruction switch a besoin d’au moins un cas dans le cas par défaut de toohello Ajout.

4. Après l’instruction switch hello, supprimer hello d’origine fichier téléchargé tooDropbox en ajoutant cette action : **Dropbox - supprimer le fichier**

5. Enregistrez votre application logique. Testez votre application en chargeant un fichier tooDropbox. Vous recevrez sous peu un e-mail d’approbation. Sélectionnez une option et observer le comportement de hello.

   > [!TIP]
   > Découvrez comment faire trop[surveiller vos applications logiques](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Comprendre le code hello derrière les instructions switch

Maintenant que vous avez créé avec succès une application de logique à l’aide d’une instruction switch, examinons définition de code hello derrière l’instruction switch hello.

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

* `"Switch"`désigne hello hello de l’instruction switch, que vous pouvez renommer pour une meilleure lisibilité. 
* `"type": "Switch"`Indique que les actions hello sont une instruction switch. 
* `"expression"`est l’option sélectionnée de l’approbateur hello dans cet exemple et est évaluée par rapport à chaque cas déclarée plus loin dans la définition de hello. 
* `"cases"` peut contenir une infinité de cas. Pour chaque cas, `"Case *"` est le nom par défaut hello cas hello, que vous pouvez renommer pour une meilleure lisibilité. 
`"case"`Spécifie l’étiquette case hello, qui hello commutateur utilisation d’expressions de comparaison et doit être une valeur constante et unique. Si aucun des cas de hello correspond à l’expression de switch hello, actions sous `"default"` sont exécutées.

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondez aux questions et voir les autres utilisateurs Azure Logic Apps font, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment trop[ajouter des conditions](logic-apps-use-logic-app-features.md)
- En savoir plus sur la [gestion des erreurs et des exceptions](logic-apps-exception-handling.md)
- Découvrir d’autres [fonctionnalités en matière de langage de flux de travail](logic-apps-author-definitions.md)