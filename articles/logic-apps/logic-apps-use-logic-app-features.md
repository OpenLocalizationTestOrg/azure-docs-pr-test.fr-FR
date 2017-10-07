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
# <a name="use-logic-apps-features"></a>Utiliser les fonctionnalités des applications logiques

Dans une [rubrique précédente](../logic-apps/logic-apps-create-a-logic-app.md), vous avez créé votre première application logique. toocontrol flux de travail de votre application logique, vous pouvez spécifier des chemins d’accès pour votre toorun d’application logique et comment trop de traiter les données dans les tableaux, les collections et les lots. Vous pouvez inclure les éléments suivants dans le workflow de votre application logique :

* Les conditions et les [instructions switch](../logic-apps/logic-apps-switch-case.md) permettent à votre application logique d’exécuter différentes actions si certaines conditions sont remplies ou non.

* Les [boucles](../logic-apps/logic-apps-loops-and-scopes.md) permettent à votre application logique d’exécuter des étapes à plusieurs reprises. Par exemple, vous pouvez répéter des actions sur un tableau en utilisant une boucle **For_each**. Vous pouvez également répéter des actions jusqu’à ce qu’une condition soit remplie à l’aide d’une boucle **Until**.

* [Étendues](../logic-apps/logic-apps-loops-and-scopes.md) permettent de vous regroupez série d’actions, par exemple, la gestion des exceptions tooimplement.

* [Debatching](../logic-apps/logic-apps-loops-and-scopes.md) permet à votre application logique de démarrer le flux de travail distinct pour les éléments dans un tableau quand vous utilisez hello **SplitOn** commande.

Cette rubrique présente d’autres concepts utiles pour la création de votre application logique :

* Vue tooedit une application existante de la logique du code
* options de démarrage d’un flux de travail.

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Conditions : exécuter des étapes uniquement lorsqu’une condition est remplie

toohave votre application logique exécutée des étapes uniquement lorsque les données satisfont aux critères spécifiques, vous pouvez ajouter une condition qui compare les données dans le flux de travail hello par rapport à des champs ou des valeurs.

Par exemple, supposons que vous disposez d’une application logique qui vous envoie un trop grand nombre d’e-mails pour des publications sur le flux RSS d’un site web. Vous pouvez ajouter une condition afin que votre application logique envoie un e-mail uniquement lorsque hello nouvelle validation appartienne catégorie spécifique de tooa.

1. Bonjour [portail Azure](https://portal.azure.com), recherchez et ouvrez votre application de logique dans le Concepteur de la logique d’application.

2. Ajouter un emplacement de flux de travail toohello condition que vous le souhaitez. 

   condition de hello tooadd entre les étapes d’un workflow d’application hello logique, pointent hello sur la flèche de hello où vous souhaitez la condition de hello tooadd. 
   Choisissez hello **signe** (**+**), puis choisissez **ajouter une condition**. Par exemple :

   ![Ajouter une condition toologic application](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Si vous souhaitez tooadd une condition à fin hello votre flux de travail en cours, accédez bas toohello de votre application logique, puis choisissez **+ nouvelle étape**.

3. Maintenant définir la condition de hello. Spécifier le champ de source de hello que vous souhaitez tooevaluate, hello opération tooperform et valeur de cible de hello ou le champ. tooadd existant champs tooyour condition, choisissez hello **ajouter une liste de contenu dynamique**.

   Par exemple :

   ![Modifier la condition en mode de base](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Voici les conditions de saisie hello :

   ![Condition complète](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > condition de hello toodefine dans le code, choisissez **modifier en mode avancé**. Par exemple :
   > 
   > ![Modifier la condition dans le code](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. Sous **si Oui** et **si aucun**, ajouter tooperform d’étapes hello selon si hello condition est remplie.

   Par exemple :

   ![Condition avec les chemins SI OUI et SI NON](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Vous pouvez faire glisser des actions existantes hello **si Oui** et **si aucun** chemins d’accès.

5. Lorsque vous avez terminé, enregistrez votre application logique.

Vous n’êtes e-mails uniquement lorsque hello publications répondent à la condition.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Répétition des actions sur une liste à l’aide de forEach

boucle forEach de Hello spécifie un tableau de toorepeat une action de pointage. Si elle n’est pas un tableau, les flux hello échoue. Par exemple, si vous avez action1 qui génère un tableau de messages, et que vous souhaitez toosend chaque message, vous pouvez inclure cette instruction forEach dans les propriétés de votre action hello :`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Modifier la définition de code hello pour une application de logique

Bien que vous avez hello Concepteur d’application logique, vous pouvez modifier directement le code hello qui définit une application logique.

1. Dans la barre de commandes hello, choisissez **mode Code**.

    Un éditeur complète s’ouvre et affiche les définition hello que vous avez modifié.

    ![Mode code](media/logic-apps-use-logic-app-features/codeview.png)

    Dans l’éditeur de texte hello, vous pouvez copier et coller n’importe quel nombre d’actions au sein de hello même application logique ou entre les applications de la logique. 
    Vous pouvez également facilement ajouter ou supprimer des sections entières à partir de la définition de hello, et vous pouvez également partager les définitions avec d’autres utilisateurs.

2. Choisissez de vos modifications, toosave **enregistrer**.

## <a name="parameters"></a>Paramètres

Certaines fonctionnalités de Logic Apps sont disponibles uniquement en mode code, les paramètres par exemple. Paramètres rendent tooreuse facile des valeurs dans l’ensemble de votre application logique. Par exemple, si vous avez une adresse de messagerie que vous souhaitez utiliser dans plusieurs actions, vous devez la définir en tant que paramètre.

Les paramètres sont adaptés pour extraire les valeurs que vous êtes probablement toochange beaucoup. Ils sont particulièrement utiles lorsque vous avez besoin des paramètres toooverride dans différents environnements. toolearn toooverride basés sur l’environnement, voir [créer des définitions d’application logique](../logic-apps/logic-apps-author-definitions.md) et [documentation de l’API REST](https://docs.microsoft.com/rest/api/logic).

Cet exemple montre comment tooupdate votre application logique existant afin que vous pouvez utiliser des paramètres pour un terme de requête hello.

1. Dans la vue code, recherchez hello `parameters : {}` de l’objet, puis ajoutez un `currentFeedUrl` objet :

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Accédez toohello `When_a_feed-item_is_published` action, rechercher hello `queries` section et remplacez la valeur de requête hello avec :`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin deux ou plusieurs chaînes, vous pouvez également utiliser hello `concat` (fonction). 
    Par exemple, `"@concat('#',parameters('currentFeedUrl'))"` fonctionne même hello comme hello ci-dessus.

3.  Une fois ces opérations effectuées, sélectionnez **Enregistrer**. 

    Maintenant vous pouvez modifier flux RSS du hello du site Web en passant une autre URL via hello `currentFeedURL` objet.

En savoir plus sur [comment définitions d’application logique tooauthor](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Démarrage de workflows d’application logique

Vous disposez des options différentes pour le démarrage du workflow hello défini dans votre application logique. Vous pouvez toujours démarrer une flux de travail à la demande dans hello [portail Azure].

### <a name="recurrence-triggers"></a>Déclencheurs de périodicité

Un déclencheur de périodicité s'exécute selon un intervalle que vous spécifiez. Lorsque le déclencheur de hello possède une logique conditionnelle, déclencheur de hello détermine si le flux de travail hello doit toorun. Un déclencheur indique le flux de travail hello doit s’exécuter en retournant un `200` code d’état. Lorsque le flux de travail hello n’a pas besoin de toorun, le déclencheur de hello retourne un `202` code d’état.

### <a name="callback-using-rest-apis"></a>Rappel à l'aide des API REST

toostart un flux de travail, les services peuvent appeler un point de terminaison application logique. Choisissez de ce genre de logique application à la demande, toostart **exécuter maintenant** sur la barre de commandes hello. Consultez la page [Démarrage des flux de travail en appelant les points de terminaison en tant que déclencheurs](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[portail Azure]: https://portal.azure.com

## <a name="next-steps"></a>Étapes suivantes

* [Instructions switch](../logic-apps/logic-apps-switch-case.md) 
* [Boucles, étendues et décomposition](../logic-apps/logic-apps-loops-and-scopes.md)
* [Créer des définitions d’application logique](../logic-apps/logic-apps-author-definitions.md)