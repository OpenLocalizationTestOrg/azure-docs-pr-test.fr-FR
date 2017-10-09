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
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="64c71-103">Créer une fonction déclenchée par un webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="64c71-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="64c71-104">Découvrez comment toocreate une fonction qui est déclenchée par une demande de webhook HTTP avec une charge utile GitHub spécifiques.</span><span class="sxs-lookup"><span data-stu-id="64c71-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook a déclenché la fonction Bonjour portail Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="64c71-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64c71-106">Prerequisites</span></span>

+ <span data-ttu-id="64c71-107">Un compte GitHub avec au moins un projet.</span><span class="sxs-lookup"><span data-stu-id="64c71-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="64c71-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="64c71-108">An Azure subscription.</span></span> <span data-ttu-id="64c71-109">Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="64c71-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="64c71-110">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="64c71-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="64c71-112">Ensuite, créez une fonction dans hello une nouvelle application de fonction.</span><span class="sxs-lookup"><span data-stu-id="64c71-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="64c71-113">Créer une fonction de déclenchement de webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="64c71-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="64c71-114">Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**.</span><span class="sxs-lookup"><span data-stu-id="64c71-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="64c71-115">S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="64c71-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="64c71-116">Cela affiche le jeu complet de hello des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="64c71-116">This displays hello complete set of function templates.</span></span>

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="64c71-118">Sélectionnez hello **GitHub WebHook** modèle pour le langage de votre choix.</span><span class="sxs-lookup"><span data-stu-id="64c71-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="64c71-119">**Nommez votre fonction**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="64c71-119">**Name your function**, then select **Create**.</span></span>

     ![Créez une fonction de webhook déclenchée de GitHub dans hello portail Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="64c71-121">Dans votre nouvelle fonction, cliquez sur **<> / Get fonction URL**, puis copiez et enregistrez les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="64c71-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="64c71-122">Hello même chose pour **<> / obtenir le GitHub secret**.</span><span class="sxs-lookup"><span data-stu-id="64c71-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="64c71-123">Vous utilisez ces webhook de hello valeurs tooconfigure dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="64c71-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Passez en revue le code de la fonction hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="64c71-125">Ensuite, vous créez le webhook dans votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="64c71-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="64c71-126">Configurer hello webhook</span><span class="sxs-lookup"><span data-stu-id="64c71-126">Configure hello webhook</span></span>

1. <span data-ttu-id="64c71-127">Dans GitHub, accédez référentiel tooa dont vous êtes propriétaire.</span><span class="sxs-lookup"><span data-stu-id="64c71-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="64c71-128">Vous pouvez également utiliser l’un des référentiels que vous avez dupliqués.</span><span class="sxs-lookup"><span data-stu-id="64c71-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="64c71-129">Si vous avez besoin d’un référentiel de toofork, utilisez <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="64c71-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="64c71-130">Cliquez sur **Paramètres**, puis sur **Webhooks** et **Ajouter un webhook**.</span><span class="sxs-lookup"><span data-stu-id="64c71-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Ajouter un webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="64c71-132">Utilisez les paramètres comme spécifié dans la table de hello, puis cliquez sur **ajouter webhook**.</span><span class="sxs-lookup"><span data-stu-id="64c71-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Définir l’URL du webhook hello et la clé secrète](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="64c71-134">Paramètre</span><span class="sxs-lookup"><span data-stu-id="64c71-134">Setting</span></span> | <span data-ttu-id="64c71-135">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="64c71-135">Suggested value</span></span> | <span data-ttu-id="64c71-136">Description</span><span class="sxs-lookup"><span data-stu-id="64c71-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="64c71-137">**URL de charge utile**</span><span class="sxs-lookup"><span data-stu-id="64c71-137">**Payload URL**</span></span> | <span data-ttu-id="64c71-138">Valeur copiée</span><span class="sxs-lookup"><span data-stu-id="64c71-138">Copied value</span></span> | <span data-ttu-id="64c71-139">Utilisez la valeur hello retournée par **<> / Get fonction URL**.</span><span class="sxs-lookup"><span data-stu-id="64c71-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="64c71-140">**Secret**</span><span class="sxs-lookup"><span data-stu-id="64c71-140">**Secret**</span></span>   | <span data-ttu-id="64c71-141">Valeur copiée</span><span class="sxs-lookup"><span data-stu-id="64c71-141">Copied value</span></span> | <span data-ttu-id="64c71-142">Utilisez la valeur hello retournée par **<> / obtenir le GitHub secret**.</span><span class="sxs-lookup"><span data-stu-id="64c71-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="64c71-143">**Type de contenu**</span><span class="sxs-lookup"><span data-stu-id="64c71-143">**Content type**</span></span> | <span data-ttu-id="64c71-144">application/json</span><span class="sxs-lookup"><span data-stu-id="64c71-144">application/json</span></span> | <span data-ttu-id="64c71-145">fonction Hello attend une charge utile JSON.</span><span class="sxs-lookup"><span data-stu-id="64c71-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="64c71-146">Déclencheurs d’événement</span><span class="sxs-lookup"><span data-stu-id="64c71-146">Event triggers</span></span> | <span data-ttu-id="64c71-147">Je vais sélectionner les événements individuels</span><span class="sxs-lookup"><span data-stu-id="64c71-147">Let me select individual events</span></span> | <span data-ttu-id="64c71-148">Nous voulons uniquement tootrigger sur les événements de commentaire de problème.</span><span class="sxs-lookup"><span data-stu-id="64c71-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="64c71-149">Problème sous forme de commentaire</span><span class="sxs-lookup"><span data-stu-id="64c71-149">Issue comment</span></span> |  |

<span data-ttu-id="64c71-150">Maintenant, hello webhook est tootrigger configuré votre fonction lors de l’ajout d’un nouveau commentaire de problème.</span><span class="sxs-lookup"><span data-stu-id="64c71-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="64c71-151">Fonction hello de test</span><span class="sxs-lookup"><span data-stu-id="64c71-151">Test hello function</span></span>

1. <span data-ttu-id="64c71-152">Dans votre référentiel GitHub, ouvrez hello **problèmes** onglet dans une nouvelle fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="64c71-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="64c71-153">Dans la nouvelle fenêtre de hello, cliquez sur **nouveau problème**, tapez un titre, puis cliquez sur **soumettre un nouveau problème**.</span><span class="sxs-lookup"><span data-stu-id="64c71-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="64c71-154">Problème de hello, tapez un commentaire et cliquez sur **commentaire**.</span><span class="sxs-lookup"><span data-stu-id="64c71-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Ajoutez un problème GitHub sous forme de commentaire.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="64c71-156">Revenir en arrière toohello portal et afficher les journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="64c71-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="64c71-157">Vous devez voir une entrée de suivi par un nouveau texte de commentaire hello.</span><span class="sxs-lookup"><span data-stu-id="64c71-157">You should see a trace entry with hello new comment text.</span></span>

     ![Afficher le texte du commentaire hello dans les journaux hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="64c71-159">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="64c71-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="64c71-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64c71-160">Next steps</span></span>

<span data-ttu-id="64c71-161">Vous avez créé une fonction qui s’exécute lorsqu’une requête est reçue à partir d’un webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="64c71-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="64c71-162">Pour en savoir plus sur les déclencheurs webhook, consultez la page [Liaisons HTTP et webhook d’Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="64c71-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
