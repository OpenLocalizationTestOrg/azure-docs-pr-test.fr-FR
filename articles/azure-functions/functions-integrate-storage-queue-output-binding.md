---
title: "Créer une fonction dans Azure déclenchée par des messages de file d’attente | Microsoft Docs"
description: "Utilisez Azure Functions pour créer une fonction sans serveur appelée par un message soumis à une file d’attente de stockage Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 57c59273a9da55f3e357764c522b444ae2d73cb5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="add-messages-to-an-azure-storage-queue-using-functions"></a><span data-ttu-id="5c73a-103">Ajouter des messages au stockage de files d’attente Azure, à l’aide de Functions</span><span class="sxs-lookup"><span data-stu-id="5c73a-103">Add messages to an Azure Storage queue using Functions</span></span>

<span data-ttu-id="5c73a-104">Dans Azure Functions, les liaisons d’entrée et de sortie fournissent une méthode déclarative pour se connecter à des données de service externe à partir de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="5c73a-104">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="5c73a-105">Dans cette rubrique, apprenez à mettre à jour une fonction existante en ajoutant une liaison de sortie qui envoie des messages au service Stockage File d’attente d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5c73a-105">In this topic, learn how to update an existing function by adding an output binding that sends messages to Azure Queue storage.</span></span>  

![Affichage du message dans les journaux.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="5c73a-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5c73a-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="5c73a-108">Installez [l’Explorateur de Stockage Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5c73a-108">Install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="5c73a-109"><a name="add-binding"></a>Ajoutez une liaison de sortie</span><span class="sxs-lookup"><span data-stu-id="5c73a-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="5c73a-110">Développez à la fois votre application de fonction et votre fonction.</span><span class="sxs-lookup"><span data-stu-id="5c73a-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="5c73a-111">Cliquez sur **Intégrer** et **+ Nouvelle sortie**, puis choisissez **Stockage File d’attente Azure** et **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Ajoutez une liaison de sortie de stockage de files d’attente à une fonction dans le Portail Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="5c73a-113">Utilisez les paramètres spécifiés dans le tableau :</span><span class="sxs-lookup"><span data-stu-id="5c73a-113">Use the settings as specified in the table:</span></span> 

    ![Ajoutez une liaison de sortie de stockage de files d’attente à une fonction dans le Portail Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="5c73a-115">Paramètre</span><span class="sxs-lookup"><span data-stu-id="5c73a-115">Setting</span></span>      |  <span data-ttu-id="5c73a-116">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="5c73a-116">Suggested value</span></span>   | <span data-ttu-id="5c73a-117">Description</span><span class="sxs-lookup"><span data-stu-id="5c73a-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="5c73a-118">**Nom de la file d’attente**</span><span class="sxs-lookup"><span data-stu-id="5c73a-118">**Queue name**</span></span>   | <span data-ttu-id="5c73a-119">éléments myqueue</span><span class="sxs-lookup"><span data-stu-id="5c73a-119">myqueue-items</span></span>    | <span data-ttu-id="5c73a-120">Le nom de la file d’attente à connecter à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5c73a-120">The name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="5c73a-121">**Connexion au compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="5c73a-121">**Storage account connection**</span></span> | <span data-ttu-id="5c73a-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="5c73a-122">AzureWebJobStorage</span></span> | <span data-ttu-id="5c73a-123">Vous pouvez utiliser la connexion de compte de stockage qui est déjà utilisée par votre application de fonction, ou créez-en une.</span><span class="sxs-lookup"><span data-stu-id="5c73a-123">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="5c73a-124">**Nom de message de paramètre**</span><span class="sxs-lookup"><span data-stu-id="5c73a-124">**Message parameter name**</span></span> | <span data-ttu-id="5c73a-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="5c73a-125">outputQueueItem</span></span> | <span data-ttu-id="5c73a-126">Le nom du paramètre de liaison de sortie.</span><span class="sxs-lookup"><span data-stu-id="5c73a-126">The name of the output binding parameter.</span></span> | 

4. <span data-ttu-id="5c73a-127">Cliquez sur **Enregistrer** pour ajouter la liaison.</span><span class="sxs-lookup"><span data-stu-id="5c73a-127">Click **Save** to add the binding.</span></span>
 
<span data-ttu-id="5c73a-128">Maintenant que vous avez défini une liaison de sortie, vous devez mettre à jour le code afin d’utiliser la liaison pour ajouter des messages à une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5c73a-128">Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.</span></span>  

## <a name="update-the-function-code"></a><span data-ttu-id="5c73a-129">Mettre à jour le code de fonction</span><span class="sxs-lookup"><span data-stu-id="5c73a-129">Update the function code</span></span>

1. <span data-ttu-id="5c73a-130">Sélectionnez la fonction pour afficher le code de fonction dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="5c73a-130">Select your function to display the function code in the editor.</span></span> 

2. <span data-ttu-id="5c73a-131">Pour une fonction C#, mettez à jour la définition de fonction comme suit, afin d’ajouter le paramètre de liaison de stockage **outputQueueItem**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-131">For a C# function, update your function definition as follows to add the **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="5c73a-132">Ignorez cette étape pour une fonction JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5c73a-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="5c73a-133">Ajoutez le code suivant à la fonction, juste avant que la méthode ne revienne.</span><span class="sxs-lookup"><span data-stu-id="5c73a-133">Add the following code to the function just before the method returns.</span></span> <span data-ttu-id="5c73a-134">Utilisez l’extrait de code approprié pour la langue de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="5c73a-134">Use the appropriate snippet for the language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed to the function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed to the function: " + name);     
    ```

4. <span data-ttu-id="5c73a-135">Sélectionnez **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="5c73a-135">Select **Save** to save changes.</span></span>

<span data-ttu-id="5c73a-136">La valeur passée au déclencheur HTTP est comprise dans un message ajouté à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5c73a-136">The value passed to the HTTP trigger is included in a message added to the queue.</span></span>
 
## <a name="test-the-function"></a><span data-ttu-id="5c73a-137">Tester la fonction</span><span class="sxs-lookup"><span data-stu-id="5c73a-137">Test the function</span></span> 

1. <span data-ttu-id="5c73a-138">Après avoir enregistré les modifications de code, sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-138">After the code changes are saved, select **Run**.</span></span> 

    ![Ajoutez une liaison de sortie de stockage de files d’attente à une fonction dans le Portail Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="5c73a-140">Vérifiez les journaux pour vous assurer que la fonction a réussi.</span><span class="sxs-lookup"><span data-stu-id="5c73a-140">Check the logs to make sure that the function succeeded.</span></span> <span data-ttu-id="5c73a-141">Une nouvelle file d’attente nommée **outqueue** est créée dans votre compte de stockage, par le runtime des fonctions, lorsque la liaison de sortie est utilisée pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="5c73a-141">A new queue named **outqueue** is created in your Storage account by the Functions runtime when the output binding is first used.</span></span>

<span data-ttu-id="5c73a-142">Par la suite, vous pouvez vous connecter à votre compte de stockage afin de vérifier la nouvelle file d’attente et le nouveau message que vous avez ajouté au compte.</span><span class="sxs-lookup"><span data-stu-id="5c73a-142">Next, you can connect to your storage account to verify the new queue and the message you added to it.</span></span> 

## <a name="connect-to-the-queue"></a><span data-ttu-id="5c73a-143">Connexion à la file d’attente</span><span class="sxs-lookup"><span data-stu-id="5c73a-143">Connect to the queue</span></span>

<span data-ttu-id="5c73a-144">Ignorez les trois premières étapes si vous avez déjà installé l’Explorateur de stockage et si vous l’avez connecté à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5c73a-144">Skip the first three steps if you have already installed Storage Explorer and connected it to your storage account.</span></span>    

1. <span data-ttu-id="5c73a-145">Dans votre fonction, sélectionnez **Intégrer**, et choisissez la nouvelle liaison de sortie **Stockage de files d’attente Azure**, puis développez **Documentation**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-145">In your function, choose **Integrate** and the new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="5c73a-146">Copiez le **Nom de compte** et la **Clé de compte**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="5c73a-147">Vous utilisez ces informations d’identification pour vous connecter au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5c73a-147">You use these credentials to connect to the storage account.</span></span>
 
    ![Obtenez les informations d’identification de connexion au compte de stockage.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="5c73a-149">Exécutez [l’Explorateur de stockage Microsoft Azure](http://storageexplorer.com/), sélectionnez l’icône de connexion située sur la gauche, choisissez **Utiliser un nom et une clé de compte de stockage**, puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-149">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select the connect icon on the left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Exécutez l’outil Explorateur de compte de stockage.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="5c73a-151">Collez le **Nom de compte** et la **Clé de compte** de l’étape 1 dans les champs correspondants, puis sélectionnez **Suivant**, et **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="5c73a-151">Paste the **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![Collez les informations d’identification de stockage et connectez-vous.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="5c73a-153">Développez le compte de stockage attaché, puis **Files d’attente**, et vérifiez qu’une file d’attente nommée **myqueue-items** existe.</span><span class="sxs-lookup"><span data-stu-id="5c73a-153">Expand the attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="5c73a-154">Vous devriez également déjà voir un message dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5c73a-154">You should also see a message already in the queue.</span></span>  
 
    ![Créez une file d’attente de stockage.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="5c73a-156">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="5c73a-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="5c73a-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c73a-157">Next steps</span></span>

<span data-ttu-id="5c73a-158">Vous avez ajouté une liaison de sortie à une fonction existante.</span><span class="sxs-lookup"><span data-stu-id="5c73a-158">You have added an output binding to an existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="5c73a-159">Pour en savoir plus sur la liaison vers le stockage de files d’attente, consultez la page [Liaisons de file d’attente de stockage Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="5c73a-159">For more information about binding to Queue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



