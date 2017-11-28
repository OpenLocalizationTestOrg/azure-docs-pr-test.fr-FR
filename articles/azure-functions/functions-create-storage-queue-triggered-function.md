---
title: "Créer une fonction dans Azure déclenchée par des messages de file d’attente | Microsoft Docs"
description: "Utilisez Azure Functions pour créer une fonction sans serveur appelée par un message soumis à une file d’attente de stockage Azure."
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="ed9d0-103">Créer une fonction déclenchée par une file d’attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ed9d0-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="ed9d0-104">Apprenez à créer une fonction se déclenchant lorsque des messages sont envoyés à une file d’attente de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Affichage du message dans les journaux.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="ed9d0-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ed9d0-106">Prerequisites</span></span>

- <span data-ttu-id="ed9d0-107">Télécharger et installer l’[Explorateur de Stockage Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ed9d0-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="ed9d0-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-108">An Azure subscription.</span></span> <span data-ttu-id="ed9d0-109">Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="ed9d0-110">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="ed9d0-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="ed9d0-112">Créez ensuite une fonction dans la nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="ed9d0-113">Créer une fonction déclenchée par une file d’attente</span><span class="sxs-lookup"><span data-stu-id="ed9d0-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="ed9d0-114">Développez votre Function App, puis cliquez sur le bouton **+** en regard de **Fonctions**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="ed9d0-115">S’il s’agit de la première fonction de votre Function App, sélectionnez **Fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="ed9d0-116">Cela affiche l’ensemble complet des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-116">This displays the complete set of function templates.</span></span>

    ![Page de démarrage rapide des fonctions sur le portail Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="ed9d0-118">Sélectionnez le modèle **QueueTrigger** de la langue de votre choix, puis utilisez les paramètres comme indiqué dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Créez la fonction déclenchée par la file d’attente de stockage.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="ed9d0-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ed9d0-120">Setting</span></span> | <span data-ttu-id="ed9d0-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="ed9d0-121">Suggested value</span></span> | <span data-ttu-id="ed9d0-122">Description</span><span class="sxs-lookup"><span data-stu-id="ed9d0-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="ed9d0-123">**Nom de la file d’attente**</span><span class="sxs-lookup"><span data-stu-id="ed9d0-123">**Queue name**</span></span>   | <span data-ttu-id="ed9d0-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="ed9d0-124">myqueue-items</span></span>    | <span data-ttu-id="ed9d0-125">Le nom de la file d’attente à connecter à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="ed9d0-126">**Connexion au compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="ed9d0-126">**Storage account connection**</span></span> | <span data-ttu-id="ed9d0-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="ed9d0-127">AzureWebJobStorage</span></span> | <span data-ttu-id="ed9d0-128">Vous pouvez utiliser la connexion au compte de stockage qui est déjà utilisée par votre Function App ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="ed9d0-129">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="ed9d0-129">**Name your function**</span></span> | <span data-ttu-id="ed9d0-130">Unique dans votre Function App</span><span class="sxs-lookup"><span data-stu-id="ed9d0-130">Unique in your function app</span></span> | <span data-ttu-id="ed9d0-131">Nom de cette fonction déclenchée par la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="ed9d0-132">Cliquez sur **Créer** pour créer votre fonction.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="ed9d0-133">Ensuite, connectez-vous à votre compte de stockage Azure et créez la file d’attente de stockage **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="ed9d0-134">Créer la file d’attente</span><span class="sxs-lookup"><span data-stu-id="ed9d0-134">Create the queue</span></span>

1. <span data-ttu-id="ed9d0-135">Dans votre fonction, cliquez sur **Intégrer**, développez **Documentation** et copiez le **Nom du compte** et la **Clé du compte**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="ed9d0-136">Vous utilisez ces informations d’identification pour vous connecter au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="ed9d0-137">Si vous avez déjà connecté votre compte de stockage, passez à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Obtenez les informations d’identification de connexion au compte de stockage.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="ed9d0-139">v</span><span class="sxs-lookup"><span data-stu-id="ed9d0-139">v</span></span>

1. <span data-ttu-id="ed9d0-140">Exécutez [l’Explorateur de stockage Microsoft Azure](http://storageexplorer.com/), cliquez sur l’icône de connexion située sur la gauche, choisissez **Utiliser un nom et une clé de compte de stockage**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Exécutez l’outil Explorateur de compte de stockage.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="ed9d0-142">Saisissez le **Nom du compte** et la **Clé du compte** récupérés à l’étape 1, puis cliquez sur **Suivant** et sur **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Entrez les informations d’identification de stockage et connectez-vous.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="ed9d0-144">Développez le compte de stockage attaché, cliquez avec le bouton droit sur **Files d’attente**, puis sur **Créer une file d’attente**, saisissez `myqueue-items` et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Créez une file d’attente de stockage.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="ed9d0-146">Maintenant que vous disposez d’une file d’attente de stockage, vous pouvez tester la fonction en ajoutant un message à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="ed9d0-147">Tester la fonction</span><span class="sxs-lookup"><span data-stu-id="ed9d0-147">Test the function</span></span>

1. <span data-ttu-id="ed9d0-148">Dans le portail Azure, accédez à votre fonction, développez les **Journaux** en bas de la page et vérifiez que la diffusion de journaux n’est pas suspendue.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="ed9d0-149">Dans l’Explorateur de stockage, développez votre compte de stockage, **Files d’attente**, et **myqueue-items**, puis cliquez sur **Ajouter message**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Ajoutez un message dans la file d’attente.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="ed9d0-151">Saisissez le message « Hello World ! »</span><span class="sxs-lookup"><span data-stu-id="ed9d0-151">Type your "Hello World!"</span></span> <span data-ttu-id="ed9d0-152">dans **Texte du message** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="ed9d0-153">Attendez quelques secondes, puis retournez à vos journaux de fonction et vérifiez que le nouveau message a été lu à partir de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Affichez le message dans les journaux.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="ed9d0-155">Dans l’Explorateur de stockage, cliquez sur **Actualiser** et vérifiez que le message a été traité et qu’il ne se trouve plus dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ed9d0-156">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="ed9d0-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="ed9d0-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ed9d0-157">Next steps</span></span>

<span data-ttu-id="ed9d0-158">Vous avez créé une fonction qui s’exécute lorsqu’un message est ajouté à une file d’attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="ed9d0-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="ed9d0-159">Pour en savoir plus sur les déclencheurs de stockage en file d’attente, consultez la page [Liaisons de file d’attente de stockage Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="ed9d0-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>