---
title: "aaaGet a démarré avec le stockage d’objets blob Azure et Visual Studio connecté Services (ASP.NET) | Documents Microsoft"
description: "Comment tooget démarrer à l’aide du stockage d’objets blob Azure dans un projet ASP.NET dans Visual Studio après la connexion de compte de stockage tooa à l’aide de Visual Studio Services connectés"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="eac75-103">Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="eac75-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="eac75-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="eac75-104">Overview</span></span>

<span data-ttu-id="eac75-105">Stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="eac75-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="eac75-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="eac75-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="eac75-107">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="eac75-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="eac75-108">Ce didacticiel montre comment toowrite ASP.NET de code pour les scénarios courants à l’aide du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="eac75-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="eac75-109">Ces scénarios incluent la création d’un conteneur d’objets blob, ainsi que le chargement, la création d’une liste, le téléchargement et la suppression d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="eac75-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="eac75-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eac75-110">Prerequisites</span></span>

* [<span data-ttu-id="eac75-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eac75-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="eac75-112">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="eac75-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="eac75-113">Créer un contrôleur MVC</span><span class="sxs-lookup"><span data-stu-id="eac75-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="eac75-114">Bonjour **l’Explorateur de solutions**, avec le bouton droit **contrôleurs**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="eac75-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Ajouter une application ASP.NET MVC de tooan contrôleur](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="eac75-116">Sur hello **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC 5 - vide**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eac75-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="eac75-118">Sur hello **ajouter un contrôleur** boîte de dialogue, nom hello du contrôleur *BlobsController*, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eac75-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Contrôleur MVC de hello nom](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="eac75-120">Ajoutez hello suivant *à l’aide de* directives toohello `BlobsController.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="eac75-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="eac75-121">Création d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="eac75-121">Create a blob container</span></span>

<span data-ttu-id="eac75-122">Un conteneur d’objets blob est une hiérarchie imbriquée d’objets blobs et de dossiers.</span><span class="sxs-lookup"><span data-stu-id="eac75-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="eac75-123">Hello étapes suivantes illustrent comment toocreate un conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="eac75-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="eac75-124">Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eac75-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eac75-125">Ouvrez hello `BlobsController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="eac75-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eac75-126">Ajoutez une méthode appelée **CreateBlobContainer** qui retourne un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eac75-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="eac75-127">Au sein de hello **CreateBlobContainer** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="eac75-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eac75-128">Utilisez hello suivant code tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="eac75-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="eac75-129">(Modification  *&lt;storage-account-name >* nom toohello Hello compte de stockage Azure que vous êtes en train d’accéder.)</span><span class="sxs-lookup"><span data-stu-id="eac75-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eac75-130">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="eac75-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eac75-131">Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur de référence toohello blob souhaité.</span><span class="sxs-lookup"><span data-stu-id="eac75-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="eac75-132">Hello **CloudBlobClient.GetContainerReference** méthode ne rend pas une demande pour le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="eac75-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="eac75-133">référence de Hello est retournée que conteneur d’objets blob hello existe ou non.</span><span class="sxs-lookup"><span data-stu-id="eac75-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eac75-134">Appelez hello **CloudBlobContainer.CreateIfNotExists** conteneur de hello toocreate méthode s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="eac75-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="eac75-135">Hello **CloudBlobContainer.CreateIfNotExists** méthode retourne **true** si le conteneur de hello n’existe pas et a été correctement créé.</span><span class="sxs-lookup"><span data-stu-id="eac75-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="eac75-136">Sinon, la valeur **false** est retournée.</span><span class="sxs-lookup"><span data-stu-id="eac75-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="eac75-137">Hello de mise à jour **ViewBag** par nom de hello du conteneur d’objets blob hello.</span><span class="sxs-lookup"><span data-stu-id="eac75-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="eac75-138">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **BLOB**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="eac75-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="eac75-139">Sur hello **ajouter une vue** boîte de dialogue, entrez **CreateBlobContainer** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eac75-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="eac75-140">Ouvrez `CreateBlobContainer.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="eac75-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="eac75-141">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eac75-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eac75-142">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eac75-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="eac75-143">Exécutez l’application hello et sélectionnez **créer un conteneur d’objets Blob** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="eac75-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Création du conteneur d’objets blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="eac75-145">Comme mentionné précédemment, hello **CloudBlobContainer.CreateIfNotExists** méthode retourne **true** uniquement lorsque le conteneur de hello n’existe pas et est créé.</span><span class="sxs-lookup"><span data-stu-id="eac75-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="eac75-146">Par conséquent, si vous exécutez une application hello lorsque hello conteneur existe, méthode hello retourne **false**.</span><span class="sxs-lookup"><span data-stu-id="eac75-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="eac75-147">toorun hello application plusieurs fois, que vous devez supprimer le conteneur de hello avant de réexécuter l’application hello.</span><span class="sxs-lookup"><span data-stu-id="eac75-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="eac75-148">Conteneur de hello suppression peut être effectuée via hello **CloudBlobContainer.Delete** (méthode).</span><span class="sxs-lookup"><span data-stu-id="eac75-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="eac75-149">Vous pouvez également supprimer le conteneur de hello à l’aide de hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="eac75-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="eac75-150">Charger un objet blob dans un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="eac75-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="eac75-151">Une fois que vous avez [créé un conteneur d’objets blob](#create-a-blob-container), vous pouvez charger des fichiers dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="eac75-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="eac75-152">Cette section vous guide dans le processus de téléchargement d’un conteneur d’objets blob tooa fichier local.</span><span class="sxs-lookup"><span data-stu-id="eac75-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="eac75-153">étapes de Hello supposent que vous avez créé un conteneur d’objets blob nommé *conteneur d’objets blob test*.</span><span class="sxs-lookup"><span data-stu-id="eac75-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="eac75-154">Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eac75-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eac75-155">Ouvrez hello `BlobsController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="eac75-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eac75-156">Ajoutez une méthode appelée **UploadBlob** qui renvoie un objet **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="eac75-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="eac75-157">Au sein de hello **UploadBlob** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="eac75-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eac75-158">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="eac75-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eac75-159">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="eac75-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eac75-160">Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence.</span><span class="sxs-lookup"><span data-stu-id="eac75-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eac75-161">Comme nous l’avons expliqué précédemment, le stockage Azure prend en charge différents types d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="eac75-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="eac75-162">tooretrieve référence tooa objet blob de pages, appel hello **CloudBlobContainer.GetPageBlobReference** (méthode).</span><span class="sxs-lookup"><span data-stu-id="eac75-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="eac75-163">tooretrieve référence tooa objet blob de blocs, appel hello **CloudBlobContainer.GetBlockBlobReference** (méthode).</span><span class="sxs-lookup"><span data-stu-id="eac75-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="eac75-164">En règle générale, objet blob de blocs est hello recommandé toouse de type.</span><span class="sxs-lookup"><span data-stu-id="eac75-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="eac75-165">(Modification < nom d’objet blob > * nom toohello blob de hello toogive téléchargé qu’une seule fois.)</span><span class="sxs-lookup"><span data-stu-id="eac75-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="eac75-166">Une fois que vous avez une référence d’objet blob, vous pouvez télécharger tout tooit de flux de données en appelant l’objet de référence blob hello **UploadFromStream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="eac75-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="eac75-167">Hello **UploadFromStream** méthode crée l’objet blob de hello si elle n’existe pas, ou le remplace s’il existe.</span><span class="sxs-lookup"><span data-stu-id="eac75-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="eac75-168">(Modification  *&lt;de téléchargement de fichier >* tooa complet en chemin d’accès toohello fichier tooupload.)</span><span class="sxs-lookup"><span data-stu-id="eac75-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="eac75-169">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **BLOB**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="eac75-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="eac75-170">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eac75-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eac75-171">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eac75-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="eac75-172">Exécutez l’application hello et sélectionnez **téléchargement blob**.</span><span class="sxs-lookup"><span data-stu-id="eac75-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="eac75-173">Hello section - [répertorier les objets BLOB de hello dans un conteneur d’objets blob](#list-the-blobs-in-a-blob-container) -illustre comment hello de toolist les objets BLOB dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="eac75-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="eac75-174">Répertorier les objets BLOB hello dans un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="eac75-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="eac75-175">Cette section illustre comment hello de toolist les objets BLOB dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="eac75-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="eac75-176">exemple de code Hello référence hello *conteneur d’objets blob test* créé dans la section de hello, [créer un conteneur d’objets blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="eac75-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="eac75-177">Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eac75-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eac75-178">Ouvrez hello `BlobsController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="eac75-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eac75-179">Ajoutez une méthode appelée **ListBlobs** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eac75-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="eac75-180">Au sein de hello **ListBlobs** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="eac75-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eac75-181">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="eac75-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eac75-182">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="eac75-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eac75-183">Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence.</span><span class="sxs-lookup"><span data-stu-id="eac75-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eac75-184">objets BLOB de hello toolist dans un conteneur d’objets blob, utilisez hello **CloudBlobContainer.ListBlobs** (méthode).</span><span class="sxs-lookup"><span data-stu-id="eac75-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="eac75-185">Hello **CloudBlobContainer.ListBlobs** méthode retourne un **IListBlobItem** de l’objet que vous effectuez un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou **CloudBlobDirectory** objet.</span><span class="sxs-lookup"><span data-stu-id="eac75-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="eac75-186">Hello extrait de code suivant énumère tous les objets BLOB de hello dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="eac75-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="eac75-187">Chaque objet blob est l’objet approprié de cast toohello en fonction de son type et son nom (ou URI dans les cas de hello d’un **CloudBlobDirectory**) est ajouté à la liste de tooa.</span><span class="sxs-lookup"><span data-stu-id="eac75-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="eac75-188">Dans tooblobs de plus, les conteneurs d’objets blob peuvent contenir des répertoires.</span><span class="sxs-lookup"><span data-stu-id="eac75-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="eac75-189">Supposons que vous avez un conteneur d’objets blob appelé *conteneur d’objets blob test* avec hello suivant la hiérarchie :</span><span class="sxs-lookup"><span data-stu-id="eac75-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="eac75-190">À l’aide de hello précédant l’exemple de code, hello **BLOB** liste des chaînes contient suivant toohello similaire de valeurs :</span><span class="sxs-lookup"><span data-stu-id="eac75-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="eac75-191">Comme vous pouvez le voir, liste de hello inclut hello uniquement à des entités niveau supérieur ; hello pas imbriqués celles (*bar.png* et *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="eac75-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="eac75-192">toolist tous hello entités au sein d’un conteneur d’objets blob, vous devez appeler hello **CloudBlobContainer.ListBlobs** méthode et passe **true** pour hello **useFlatBlobListing** paramètre.</span><span class="sxs-lookup"><span data-stu-id="eac75-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="eac75-193">Hello du paramètre **useFlatBlobListing** paramètre trop**true** retourne une liste plate de toutes les entités dans le conteneur d’objets blob hello et produit hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="eac75-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="eac75-194">Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **BLOB**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.</span><span class="sxs-lookup"><span data-stu-id="eac75-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="eac75-195">Sur hello **ajouter une vue** boîte de dialogue, entrez **ListBlobs** pour le nom de la vue hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eac75-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="eac75-196">Ouvrez `ListBlobs.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="eac75-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="eac75-197">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eac75-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eac75-198">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eac75-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="eac75-199">Exécutez l’application hello et sélectionnez **répertorier les objets BLOB** toosee des résultats similaires toohello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="eac75-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Création de la liste d’objets blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="eac75-201">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="eac75-201">Download blobs</span></span>

<span data-ttu-id="eac75-202">Cette section illustre comment toodownload un objet blob et soit conserver il toolocal stockage ou lecture hello contenu dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="eac75-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="eac75-203">exemple de code Hello référence hello *conteneur d’objets blob test* créé dans la section de hello, [créer un conteneur d’objets blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="eac75-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="eac75-204">Ouvrez hello `BlobsController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="eac75-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eac75-205">Ajoutez une méthode appelée **DownloadBlob** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eac75-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="eac75-206">Au sein de hello **DownloadBlob** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="eac75-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eac75-207">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="eac75-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eac75-208">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="eac75-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eac75-209">Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence.</span><span class="sxs-lookup"><span data-stu-id="eac75-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eac75-210">Ajoutez un objet de référence d’objet blob en appelant la méthode **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="eac75-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="eac75-211">(Modification  *&lt;-nom d’objet blob >* toohello les nom d’objet blob hello en cours de téléchargement.)</span><span class="sxs-lookup"><span data-stu-id="eac75-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="eac75-212">toodownload un objet blob, utilisez hello **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream** (méthode), selon le type d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="eac75-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="eac75-213">Hello extrait de code suivant utilise hello **CloudBlockBlob.DownloadToStream** tootransfer méthode flux de tooa contenu d’un objet blob de l’objet qui est ensuite rendue persistante fichier local de tooa : (modification  *&lt;nom de fichier local >* toohello complet représentant de nom du fichier où vous souhaitez blob hello téléchargé.)</span><span class="sxs-lookup"><span data-stu-id="eac75-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="eac75-214">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eac75-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eac75-215">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eac75-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="eac75-216">Exécutez l’application hello et sélectionnez **téléchargement blob** objet blob de toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="eac75-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="eac75-217">objet blob de Hello spécifié Bonjour **CloudBlobContainer.GetBlockBlobReference** appel de méthode télécharge emplacement toohello que vous spécifiez dans hello **File.OpenWrite** appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="eac75-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="eac75-218">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="eac75-218">Delete blobs</span></span>

<span data-ttu-id="eac75-219">Hello étapes suivantes illustrent comment toodelete un objet blob :</span><span class="sxs-lookup"><span data-stu-id="eac75-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="eac75-220">Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="eac75-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="eac75-221">Ouvrez hello `BlobsController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="eac75-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="eac75-222">Ajoutez une méthode appelée **DeleteBlob** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="eac75-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="eac75-223">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="eac75-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eac75-224">Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).</span><span class="sxs-lookup"><span data-stu-id="eac75-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="eac75-225">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="eac75-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="eac75-226">Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence.</span><span class="sxs-lookup"><span data-stu-id="eac75-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="eac75-227">Ajoutez un objet de référence d’objet blob en appelant la méthode **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="eac75-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="eac75-228">(Modification  *&lt;-nom d’objet blob >* toohello nom de hello blob que vous supprimez.)</span><span class="sxs-lookup"><span data-stu-id="eac75-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="eac75-229">Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="eac75-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="eac75-230">Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="eac75-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="eac75-231">Exécutez l’application hello et sélectionnez **Delete blob** toodelete blob de hello spécifié dans hello **CloudBlobContainer.GetBlockBlobReference** appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="eac75-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eac75-232">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eac75-232">Next steps</span></span>
<span data-ttu-id="eac75-233">Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eac75-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="eac75-234">Prise en main du stockage de tables Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="eac75-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="eac75-235">Prise en main du stockage de files d’attente Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="eac75-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
