---
title: "une fonction dans Azure déclenché par des messages de la file d’attente d’aaaCreate | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par une les messages soumis file d’attente de stockage Azure tooan."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="9f55a-103">Créer une fonction déclenchée par une file d’attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9f55a-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="9f55a-104">Découvrez comment toocreate une fonction déclenchée lorsque les messages sont soumis la file d’attente de stockage Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="9f55a-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Afficher le message dans les journaux hello.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="9f55a-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9f55a-106">Prerequisites</span></span>

- <span data-ttu-id="9f55a-107">Téléchargez et installez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9f55a-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="9f55a-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9f55a-108">An Azure subscription.</span></span> <span data-ttu-id="9f55a-109">Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="9f55a-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9f55a-110">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="9f55a-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="9f55a-112">Ensuite, créez une fonction dans hello une nouvelle application de fonction.</span><span class="sxs-lookup"><span data-stu-id="9f55a-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="9f55a-113">Créer une fonction déclenchée par une file d’attente</span><span class="sxs-lookup"><span data-stu-id="9f55a-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="9f55a-114">Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="9f55a-115">S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="9f55a-116">Cela affiche le jeu complet de hello des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="9f55a-116">This displays hello complete set of function templates.</span></span>

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="9f55a-118">Sélectionnez hello **QueueTrigger** modèle pour votre langue de votre choix, puis utiliser les paramètres comme spécifié dans la table de hello hello.</span><span class="sxs-lookup"><span data-stu-id="9f55a-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Créer la fonction de file d’attente déclenchée stockage hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="9f55a-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="9f55a-120">Setting</span></span> | <span data-ttu-id="9f55a-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="9f55a-121">Suggested value</span></span> | <span data-ttu-id="9f55a-122">Description</span><span class="sxs-lookup"><span data-stu-id="9f55a-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="9f55a-123">**Nom de la file d’attente**</span><span class="sxs-lookup"><span data-stu-id="9f55a-123">**Queue name**</span></span>   | <span data-ttu-id="9f55a-124">éléments myqueue</span><span class="sxs-lookup"><span data-stu-id="9f55a-124">myqueue-items</span></span>    | <span data-ttu-id="9f55a-125">Nom de hello file d’attente tooconnect tooin votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9f55a-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="9f55a-126">**Connexion au compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="9f55a-126">**Storage account connection**</span></span> | <span data-ttu-id="9f55a-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="9f55a-127">AzureWebJobStorage</span></span> | <span data-ttu-id="9f55a-128">Vous pouvez utiliser la connexion au compte de stockage hello est déjà utilisée par votre application de la fonction, ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="9f55a-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="9f55a-129">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="9f55a-129">**Name your function**</span></span> | <span data-ttu-id="9f55a-130">Unique dans votre Function App</span><span class="sxs-lookup"><span data-stu-id="9f55a-130">Unique in your function app</span></span> | <span data-ttu-id="9f55a-131">Nom de cette fonction déclenchée par la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="9f55a-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="9f55a-132">Cliquez sur **créer** toocreate votre fonction.</span><span class="sxs-lookup"><span data-stu-id="9f55a-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="9f55a-133">Ensuite, vous vous connectez compte de stockage Azure tooyour et que vous créez hello **myqueue-éléments** file d’attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="9f55a-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="9f55a-134">Créer la file d’attente hello</span><span class="sxs-lookup"><span data-stu-id="9f55a-134">Create hello queue</span></span>

1. <span data-ttu-id="9f55a-135">Dans votre fonction, cliquez sur **Intégrer**, développez **Documentation** et copiez le **Nom du compte** et la **Clé du compte**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="9f55a-136">Vous utilisez ces informations d’identification tooconnect toohello stockage compte.</span><span class="sxs-lookup"><span data-stu-id="9f55a-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="9f55a-137">Si vous êtes déjà connecté votre compte de stockage, passez toostep 4.</span><span class="sxs-lookup"><span data-stu-id="9f55a-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obtenir des informations d’identification de connexion de compte de stockage hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="9f55a-139">v</span><span class="sxs-lookup"><span data-stu-id="9f55a-139">v</span></span>

1. <span data-ttu-id="9f55a-140">Exécutez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) outil, cliquez sur hello icône à gauche de hello de connexion, choisissez **utiliser un nom de compte de stockage et de la clé**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Exécuter l’outil Explorateur de compte de stockage de hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="9f55a-142">Entrez hello **nom de compte** et **clé de compte** à l’étape 1, cliquez sur **suivant** , puis **connexion**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Entrez les informations d’identification du stockage hello et se connecter.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="9f55a-144">Développez le compte de stockage hello attaché, cliquez sur **les files d’attente**, cliquez sur **Create queue**, type `myqueue-items`, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="9f55a-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Créez une file d’attente de stockage.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="9f55a-146">Maintenant que vous avez une file d’attente de stockage, vous pouvez tester la fonction hello en ajoutant une file d’attente de message toohello.</span><span class="sxs-lookup"><span data-stu-id="9f55a-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="9f55a-147">Fonction hello de test</span><span class="sxs-lookup"><span data-stu-id="9f55a-147">Test hello function</span></span>

1. <span data-ttu-id="9f55a-148">Dans hello portail Azure, parcourir tooyour fonction développez hello **journaux** bas hello page de hello et assurez-vous que ce journal de diffusion en continu n’est pas suspendue.</span><span class="sxs-lookup"><span data-stu-id="9f55a-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="9f55a-149">Dans l’Explorateur de stockage, développez votre compte de stockage, **Files d’attente**, et **myqueue-items**, puis cliquez sur **Ajouter message**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Ajouter une file d’attente de message toohello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="9f55a-151">Saisissez le message « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="9f55a-151">Type your "Hello World!"</span></span> <span data-ttu-id="9f55a-152">dans **Texte du message** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f55a-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="9f55a-153">Attendez quelques secondes, puis revenir en arrière tooyour fonction journaux et vérifiez que ce nouveau message de salutation a été lu à partir de la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="9f55a-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Afficher le message dans les journaux hello.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="9f55a-155">Dans l’Explorateur de stockage, cliquez sur **Actualiser** et vérifiez que ce message de type hello a été traité et n’est plus dans la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="9f55a-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9f55a-156">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="9f55a-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9f55a-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f55a-157">Next steps</span></span>

<span data-ttu-id="9f55a-158">Vous avez créé une fonction qui s’exécute lorsqu’un message est ajouté de file d’attente de stockage tooa.</span><span class="sxs-lookup"><span data-stu-id="9f55a-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9f55a-159">Pour en savoir plus sur les déclencheurs de stockage en file d’attente, consultez la page [Liaisons de file d’attente de stockage Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="9f55a-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>