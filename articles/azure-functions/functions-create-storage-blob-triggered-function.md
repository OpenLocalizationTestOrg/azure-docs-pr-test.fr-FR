---
title: "Créer une fonction dans Azure déclenchée par le stockage Blob | Microsoft Docs"
description: "Utilisez Azure Functions pour créer une fonction sans serveur appelée par les éléments ajoutés au stockage Blob Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 1ddd056903b1a2f973a58bd7054ea2b8281607c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="7bdbb-103">Créer une fonction déclenchée par un stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="7bdbb-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="7bdbb-104">Apprenez à créer une fonction déclenchée lorsque des fichiers sont chargés dans ou mis à jour dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-104">Learn how to create a function triggered when files are uploaded to or updated in Azure Blob storage.</span></span>

![Affichez le message dans les journaux.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="7bdbb-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7bdbb-106">Prerequisites</span></span>

+ <span data-ttu-id="7bdbb-107">Télécharger et installer l’[Explorateur de Stockage Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7bdbb-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="7bdbb-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-108">An Azure subscription.</span></span> <span data-ttu-id="7bdbb-109">Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7bdbb-110">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="7bdbb-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="7bdbb-112">Créez ensuite une fonction dans la nouvelle Function App.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="7bdbb-113">Créer une fonction déclenchée par le stockage Blob</span><span class="sxs-lookup"><span data-stu-id="7bdbb-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="7bdbb-114">Développez votre Function App, puis cliquez sur le bouton **+** en regard de **Fonctions**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="7bdbb-115">S’il s’agit de la première fonction de votre Function App, sélectionnez **Fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="7bdbb-116">Cela affiche l’ensemble complet des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-116">This displays the complete set of function templates.</span></span>

    ![Page de démarrage rapide des fonctions sur le portail Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="7bdbb-118">Sélectionnez le modèle **BlobTrigger** de la langue de votre choix, puis utilisez les paramètres comme indiqué dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-118">Select the **BlobTrigger** template for your desired language, and use the settings as specified in the table.</span></span>

    ![Création de la fonction déclenchée par le stockage Blob.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="7bdbb-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7bdbb-120">Setting</span></span> | <span data-ttu-id="7bdbb-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="7bdbb-121">Suggested value</span></span> | <span data-ttu-id="7bdbb-122">Description</span><span class="sxs-lookup"><span data-stu-id="7bdbb-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="7bdbb-123">**Chemin d’accès**</span><span class="sxs-lookup"><span data-stu-id="7bdbb-123">**Path**</span></span>   | <span data-ttu-id="7bdbb-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="7bdbb-124">mycontainer/{name}</span></span>    | <span data-ttu-id="7bdbb-125">Emplacement du stockage Blob analysé.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="7bdbb-126">Le nom de fichier de l’objet Blob est transmis dans la liaison en tant que paramètre _name_.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-126">The file name of the blob is passed in the binding as the _name_ parameter.</span></span>  |
    | <span data-ttu-id="7bdbb-127">**Connexion au compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="7bdbb-127">**Storage account connection**</span></span> | <span data-ttu-id="7bdbb-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="7bdbb-128">AzureWebJobStorage</span></span> | <span data-ttu-id="7bdbb-129">Vous pouvez utiliser la connexion au compte de stockage qui est déjà utilisée par votre Function App ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-129">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="7bdbb-130">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="7bdbb-130">**Name your function**</span></span> | <span data-ttu-id="7bdbb-131">Unique dans votre Function App</span><span class="sxs-lookup"><span data-stu-id="7bdbb-131">Unique in your function app</span></span> | <span data-ttu-id="7bdbb-132">Nom de cette fonction déclenchée par l’objet Blob.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="7bdbb-133">Cliquez sur **Créer** pour créer votre fonction.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-133">Click **Create** to create your function.</span></span>

<span data-ttu-id="7bdbb-134">Ensuite, connectez-vous à votre compte de stockage Azure et créez le conteneur **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-134">Next, you connect to your Azure Storage account and create the **mycontainer** container.</span></span>

## <a name="create-the-container"></a><span data-ttu-id="7bdbb-135">Créer le conteneur</span><span class="sxs-lookup"><span data-stu-id="7bdbb-135">Create the container</span></span>

1. <span data-ttu-id="7bdbb-136">Dans votre fonction, cliquez sur **Intégrer**, développez **Documentation** et copiez le **Nom du compte** et la **Clé du compte**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="7bdbb-137">Vous utilisez ces informations d’identification pour vous connecter au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-137">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="7bdbb-138">Si vous avez déjà connecté votre compte de stockage, passez à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-138">If you have already connected your storage account, skip to step 4.</span></span>

    ![Obtention des informations d’identification de connexion du compte de stockage.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="7bdbb-140">Exécutez [l’Explorateur de stockage Microsoft Azure](http://storageexplorer.com/), cliquez sur l’icône de connexion situé sur la gauche, choisissez **Utiliser un nom et une clé de compte de stockage**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Exécutez l’outil Explorateur de compte de stockage.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="7bdbb-142">Saisissez le **Nom du compte** et la **Clé du compte** récupérés à l’étape 1, puis cliquez sur **Suivant** et sur **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Saisie des informations d’identification de stockage et connexion.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="7bdbb-144">Développez le compte de stockage attaché, cliquez avec le bouton droit sur **Conteneurs d’objets Blob**, puis sur **Créer un conteneur d’objets blob**, tapez `mycontainer` et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-144">Expand the attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Création d’une file d’attente de stockage.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="7bdbb-146">Une fois que vous avez un conteneur d’objets blob, vous pouvez tester la fonction en chargeant un fichier dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-146">Now that you have a blob container, you can test the function by uploading a file to the container.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="7bdbb-147">Tester la fonction</span><span class="sxs-lookup"><span data-stu-id="7bdbb-147">Test the function</span></span>

1. <span data-ttu-id="7bdbb-148">Dans le portail Azure, accédez à votre fonction, développez les **Journaux** en bas de la page et vérifiez que la diffusion de journaux n’est pas suspendue.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="7bdbb-149">Dans l’Explorateur de stockage, développez votre compte de stockage, **Conteneurs d’objets Blob** et **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="7bdbb-150">Cliquez sur **Charger**, puis sur **Charger des fichiers...**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Chargement d’un fichier dans le conteneur d’objets blob.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="7bdbb-152">Dans la boîte de dialogue **Charger des fichiers**, cliquez sur le champ **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-152">In the **Upload files** dialog box, click the **Files** field.</span></span> <span data-ttu-id="7bdbb-153">Accédez à un fichier sur votre ordinateur local, par exemple un fichier image, sélectionnez-le, puis cliquez sur **Ouvrir** et sur **Charger**.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-153">Browse to a file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="7bdbb-154">Revenez à vos journaux de fonction et vérifiez que l’objet blob a été lu.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-154">Go back to your function logs and verify that the blob has been read.</span></span>

   ![Affichage du message dans les journaux.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="7bdbb-156">Lorsque votre Function App s’exécute dans le plan de consommation par défaut, il peut s’écouler un délai de plusieurs minutes entre l’ajout ou la mise à jour de l’objet blob et le déclenchement de la fonction.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-156">When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered.</span></span> <span data-ttu-id="7bdbb-157">Si vous exigez une faible latence pour vos fonctions déclenchées par des objets Blob, exécutez plutôt votre Function App dans un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7bdbb-158">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="7bdbb-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="7bdbb-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bdbb-159">Next steps</span></span>

<span data-ttu-id="7bdbb-160">Vous avez créé une fonction qui s’exécute lorsqu’un objet blob est ajouté ou mis à jour dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="7bdbb-160">You have created a function that runs when a blob is added to or updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7bdbb-161">Pour plus d’informations sur les déclencheurs de stockage Blob, consultez [Liaisons de stockage Blob Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="7bdbb-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
