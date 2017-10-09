---
title: "aaaCreate une fonction dans Azure déclenchée par un webhook GitHub | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par un webhook GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Créer une fonction déclenchée par un webhook GitHub

Découvrez comment toocreate une fonction qui est déclenchée par une demande de webhook HTTP avec une charge utile GitHub spécifiques.

![Github Webhook a déclenché la fonction Bonjour portail Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Composants requis

+ Un compte GitHub avec au moins un projet.
+ Un abonnement Azure. Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Création d’une application Azure Function

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ensuite, créez une fonction dans hello une nouvelle application de fonction.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Créer une fonction de déclenchement de webhook GitHub

1. Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**. S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**. Cela affiche le jeu complet de hello des modèles de fonction.

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Sélectionnez hello **GitHub WebHook** modèle pour le langage de votre choix. **Nommez votre fonction**, puis cliquez sur **Créer**.

     ![Créez une fonction de webhook déclenchée de GitHub dans hello portail Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. Dans votre nouvelle fonction, cliquez sur **<> / Get fonction URL**, puis copiez et enregistrez les valeurs hello. Hello même chose pour **<> / obtenir le GitHub secret**. Vous utilisez ces webhook de hello valeurs tooconfigure dans GitHub.

    ![Passez en revue le code de la fonction hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Ensuite, vous créez le webhook dans votre référentiel GitHub.

## <a name="configure-hello-webhook"></a>Configurer hello webhook

1. Dans GitHub, accédez référentiel tooa dont vous êtes propriétaire. Vous pouvez également utiliser l’un des référentiels que vous avez dupliqués. Si vous avez besoin d’un référentiel de toofork, utilisez <https://github.com/Azure-Samples/functions-quickstart>.

1. Cliquez sur **Paramètres**, puis sur **Webhooks** et **Ajouter un webhook**.

    ![Ajouter un webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Utilisez les paramètres comme spécifié dans la table de hello, puis cliquez sur **ajouter webhook**.

    ![Définir l’URL du webhook hello et la clé secrète](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Paramètre | Valeur suggérée | Description |
|---|---|---|
| **URL de charge utile** | Valeur copiée | Utilisez la valeur hello retournée par **<> / Get fonction URL**. |
| **Secret**   | Valeur copiée | Utilisez la valeur hello retournée par **<> / obtenir le GitHub secret**. |
| **Type de contenu** | application/json | fonction Hello attend une charge utile JSON. |
| Déclencheurs d’événement | Je vais sélectionner les événements individuels | Nous voulons uniquement tootrigger sur les événements de commentaire de problème.  |
| | Problème sous forme de commentaire |  |

Maintenant, hello webhook est tootrigger configuré votre fonction lors de l’ajout d’un nouveau commentaire de problème.

## <a name="test-hello-function"></a>Fonction hello de test

1. Dans votre référentiel GitHub, ouvrez hello **problèmes** onglet dans une nouvelle fenêtre de navigateur.

1. Dans la nouvelle fenêtre de hello, cliquez sur **nouveau problème**, tapez un titre, puis cliquez sur **soumettre un nouveau problème**.

1. Problème de hello, tapez un commentaire et cliquez sur **commentaire**.

    ![Ajoutez un problème GitHub sous forme de commentaire.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Revenir en arrière toohello portal et afficher les journaux de hello. Vous devez voir une entrée de suivi par un nouveau texte de commentaire hello.

     ![Afficher le texte du commentaire hello dans les journaux hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé une fonction qui s’exécute lorsqu’une requête est reçue à partir d’un webhook GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour en savoir plus sur les déclencheurs webhook, consultez la page [Liaisons HTTP et webhook d’Azure Functions](functions-bindings-http-webhook.md).
