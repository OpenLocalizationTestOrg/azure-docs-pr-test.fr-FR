---
title: "une fonction dans Azure déclenchée par le stockage d’objets Blob d’aaaCreate | Documents Microsoft"
description: "Utilisez les fonctions Azure toocreate une fonction sans serveur qui est appelée par les éléments ajoutés tooAzure stockage d’objets Blob."
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
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="09ab8-103">Créer une fonction déclenchée par un stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="09ab8-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="09ab8-104">Découvrez comment toocreate une fonction déclenchée lorsque les fichiers sont téléchargés tooor mis à jour dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="09ab8-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Afficher le message dans les journaux hello.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="09ab8-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="09ab8-106">Prerequisites</span></span>

+ <span data-ttu-id="09ab8-107">Téléchargez et installez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="09ab8-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="09ab8-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="09ab8-108">An Azure subscription.</span></span> <span data-ttu-id="09ab8-109">Si vous n’en avez pas, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="09ab8-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="09ab8-110">Création d’une application Azure Function</span><span class="sxs-lookup"><span data-stu-id="09ab8-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="09ab8-112">Ensuite, créez une fonction dans hello une nouvelle application de fonction.</span><span class="sxs-lookup"><span data-stu-id="09ab8-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="09ab8-113">Créer une fonction déclenchée par le stockage Blob</span><span class="sxs-lookup"><span data-stu-id="09ab8-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="09ab8-114">Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="09ab8-115">S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="09ab8-116">Cela affiche le jeu complet de hello des modèles de fonction.</span><span class="sxs-lookup"><span data-stu-id="09ab8-116">This displays hello complete set of function templates.</span></span>

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="09ab8-118">Sélectionnez hello **BlobTrigger** modèle pour votre langue de votre choix, puis utiliser les paramètres comme spécifié dans la table de hello hello.</span><span class="sxs-lookup"><span data-stu-id="09ab8-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Créer la fonction de stockage déclenchée de Blob de hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="09ab8-120">Paramètre</span><span class="sxs-lookup"><span data-stu-id="09ab8-120">Setting</span></span> | <span data-ttu-id="09ab8-121">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="09ab8-121">Suggested value</span></span> | <span data-ttu-id="09ab8-122">Description</span><span class="sxs-lookup"><span data-stu-id="09ab8-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="09ab8-123">**Chemin d’accès**</span><span class="sxs-lookup"><span data-stu-id="09ab8-123">**Path**</span></span>   | <span data-ttu-id="09ab8-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="09ab8-124">mycontainer/{name}</span></span>    | <span data-ttu-id="09ab8-125">Emplacement du stockage Blob analysé.</span><span class="sxs-lookup"><span data-stu-id="09ab8-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="09ab8-126">nom du fichier d’objet blob de hello Hello est passé dans la liaison de hello en hello _nom_ paramètre.</span><span class="sxs-lookup"><span data-stu-id="09ab8-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="09ab8-127">**Connexion au compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="09ab8-127">**Storage account connection**</span></span> | <span data-ttu-id="09ab8-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="09ab8-128">AzureWebJobStorage</span></span> | <span data-ttu-id="09ab8-129">Vous pouvez utiliser la connexion au compte de stockage hello est déjà utilisée par votre application de la fonction, ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="09ab8-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="09ab8-130">**Nommer votre fonction**</span><span class="sxs-lookup"><span data-stu-id="09ab8-130">**Name your function**</span></span> | <span data-ttu-id="09ab8-131">Unique dans votre Function App</span><span class="sxs-lookup"><span data-stu-id="09ab8-131">Unique in your function app</span></span> | <span data-ttu-id="09ab8-132">Nom de cette fonction déclenchée par l’objet Blob.</span><span class="sxs-lookup"><span data-stu-id="09ab8-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="09ab8-133">Cliquez sur **créer** toocreate votre fonction.</span><span class="sxs-lookup"><span data-stu-id="09ab8-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="09ab8-134">Ensuite, vous vous connectez compte de stockage Azure tooyour et que vous créez hello **mycontainer** conteneur.</span><span class="sxs-lookup"><span data-stu-id="09ab8-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="09ab8-135">Créer un conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="09ab8-135">Create hello container</span></span>

1. <span data-ttu-id="09ab8-136">Dans votre fonction, cliquez sur **Intégrer**, développez **Documentation** et copiez le **Nom du compte** et la **Clé du compte**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="09ab8-137">Vous utilisez ces informations d’identification tooconnect toohello stockage compte.</span><span class="sxs-lookup"><span data-stu-id="09ab8-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="09ab8-138">Si vous êtes déjà connecté votre compte de stockage, passez toostep 4.</span><span class="sxs-lookup"><span data-stu-id="09ab8-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obtenir des informations d’identification de connexion de compte de stockage hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="09ab8-140">Exécutez hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) outil, cliquez sur hello icône à gauche de hello de connexion, choisissez **utiliser un nom de compte de stockage et de la clé**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Exécuter l’outil Explorateur de compte de stockage de hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="09ab8-142">Entrez hello **nom de compte** et **clé de compte** à l’étape 1, cliquez sur **suivant** , puis **connexion**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Entrez les informations d’identification du stockage hello et se connecter.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="09ab8-144">Développez le compte de stockage hello attaché, cliquez sur **conteneurs d’objets Blob**, cliquez sur **créer un conteneur blob**, type `mycontainer`, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="09ab8-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Créez une file d’attente de stockage.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="09ab8-146">Maintenant que vous avez un conteneur d’objets blob, vous pouvez tester la fonction hello en téléchargeant un conteneur toohello de fichier.</span><span class="sxs-lookup"><span data-stu-id="09ab8-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="09ab8-147">Fonction hello de test</span><span class="sxs-lookup"><span data-stu-id="09ab8-147">Test hello function</span></span>

1. <span data-ttu-id="09ab8-148">Dans hello portail Azure, parcourir tooyour fonction développez hello **journaux** bas hello page de hello et assurez-vous que ce journal de diffusion en continu n’est pas suspendue.</span><span class="sxs-lookup"><span data-stu-id="09ab8-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="09ab8-149">Dans l’Explorateur de stockage, développez votre compte de stockage, **Conteneurs d’objets Blob** et **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="09ab8-150">Cliquez sur **Charger**, puis sur **Charger des fichiers...**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Télécharger un conteneur d’objets blob toohello fichier.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="09ab8-152">Bonjour **télécharger des fichiers** boîte de dialogue, cliquez sur hello **fichiers** champ.</span><span class="sxs-lookup"><span data-stu-id="09ab8-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="09ab8-153">Rechercher le fichier tooa sur votre ordinateur local, tel qu’un fichier image, sélectionnez-le, puis cliquez sur **ouvrir** , puis **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="09ab8-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="09ab8-154">Revenir en arrière tooyour fonction journaux et vérifiez que cet objet blob hello a été lu.</span><span class="sxs-lookup"><span data-stu-id="09ab8-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Afficher le message dans les journaux hello.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="09ab8-156">Lorsque votre application de la fonction s’exécute dans le plan de la consommation hello par défaut, il peut y avoir un délai de configuration tooseveral minutes entre hello blob qui est ajouté ou mis à jour et hello fonction soit déclenchée.</span><span class="sxs-lookup"><span data-stu-id="09ab8-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="09ab8-157">Si vous exigez une faible latence pour vos fonctions déclenchées par des objets Blob, exécutez plutôt votre Function App dans un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="09ab8-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="09ab8-158">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="09ab8-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="09ab8-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09ab8-159">Next steps</span></span>

<span data-ttu-id="09ab8-160">Vous avez créé une fonction qui s’exécute lorsqu’un objet blob est ajouté tooor mis à jour dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="09ab8-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="09ab8-161">Pour plus d’informations sur les déclencheurs de stockage Blob, consultez [Liaisons de stockage Blob Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="09ab8-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
