---
title: "Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET) | Microsoft Docs"
description: "Comment prendre en main le stockage d’objets blob Azure dans le cadre d’un projet ASP.NET Visual Studio après s’être connecté à un compte de stockage à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: 8fd13efdbdd98c6d7dff1b88a6b232a08aa5a13d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="9a69a-103">Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9a69a-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="9a69a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9a69a-104">Overview</span></span>

<span data-ttu-id="9a69a-105">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="9a69a-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="9a69a-106">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="9a69a-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="9a69a-107">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9a69a-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="9a69a-108">Ce didacticiel montre comment écrire du code ASP.NET pour des scénarios courants d’utilisation du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="9a69a-109">Ces scénarios incluent la création d’un conteneur d’objets blob, ainsi que le chargement, la création d’une liste, le téléchargement et la suppression d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="9a69a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9a69a-110">Prerequisites</span></span>

* [<span data-ttu-id="9a69a-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9a69a-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="9a69a-112">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9a69a-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="9a69a-113">Créer un contrôleur MVC</span><span class="sxs-lookup"><span data-stu-id="9a69a-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="9a69a-114">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Contrôleurs**, puis sélectionnez **Ajouter -> Contrôleur** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="9a69a-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Ajouter un contrôleur à une application ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="9a69a-116">Dans la boîte de dialogue **Ajouter la structure**, cliquez sur **Contrôleur MVC 5 - vide**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="9a69a-118">Dans la boîte de dialogue **Ajouter un contrôleur**, nommez le contrôleur *BlobsController*, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![Nommer le contrôleur MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="9a69a-120">Ajoutez les directives *using* suivantes au fichier `BlobsController.cs` :</span><span class="sxs-lookup"><span data-stu-id="9a69a-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="9a69a-121">Création d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="9a69a-121">Create a blob container</span></span>

<span data-ttu-id="9a69a-122">Un conteneur d’objets blob est une hiérarchie imbriquée d’objets blobs et de dossiers.</span><span class="sxs-lookup"><span data-stu-id="9a69a-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="9a69a-123">Les étapes suivantes montrent comment créer un conteneur d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="9a69a-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9a69a-124">Le code de cette section part du principe que vous avez terminé les étapes décrites dans la section [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9a69a-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9a69a-125">Ouvrez le fichier `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="9a69a-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9a69a-126">Ajoutez une méthode appelée **CreateBlobContainer** qui retourne un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="9a69a-127">Dans la méthode **CreateBlobContainer**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9a69a-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9a69a-128">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure.</span><span class="sxs-lookup"><span data-stu-id="9a69a-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="9a69a-129">(Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9a69a-130">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="9a69a-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9a69a-131">Ajoutez un objet **CloudBlobContainer** représentant une référence au nom souhaité pour le conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="9a69a-132">La méthode **CloudBlobClient.GetContainerReference** n’effectue pas de demande auprès du stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="9a69a-133">La référence est renvoyée que le conteneur d’objets blob existe ou non.</span><span class="sxs-lookup"><span data-stu-id="9a69a-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9a69a-134">Appelez la méthode **CloudBlobContainer.CreateIfNotExists** pour créer le conteneur d’objets blob si celui-ci n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="9a69a-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="9a69a-135">La méthode **CloudBlobContainer.CreateIfNotExists** renvoie **true** si le conteneur n’existe pas et est créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="9a69a-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="9a69a-136">Sinon, la valeur **false** est retournée.</span><span class="sxs-lookup"><span data-stu-id="9a69a-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="9a69a-137">Mettez à jour l’objet **ViewBag** avec le nom du conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="9a69a-138">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Objets blob**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="9a69a-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="9a69a-139">Dans la boîte de dialogue **Ajouter une vue**, entrez **CreateBlobContainer** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="9a69a-140">Ouvrez le fichier `CreateBlobContainer.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="9a69a-141">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9a69a-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9a69a-142">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="9a69a-143">Exécutez l’application, puis sélectionnez **Créer un conteneur d’objets blob** pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="9a69a-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![Création du conteneur d’objets blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="9a69a-145">Comme mentionné précédemment, la méthode **CloudBlobContainer.CreateIfNotExists** renvoie **true** uniquement lorsque le conteneur n’existe pas et est créé.</span><span class="sxs-lookup"><span data-stu-id="9a69a-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="9a69a-146">Par conséquent, si vous exécutez l’application alors que le conteneur existe, la méthode renvoit la valeur **false**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="9a69a-147">Pour exécuter l’application plusieurs fois, vous devez supprimer le conteneur avant d’exécuter à nouveau l’application.</span><span class="sxs-lookup"><span data-stu-id="9a69a-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="9a69a-148">Le conteneur peut être supprimé à l’aide de la méthode **CloudBlobContainer.Delete**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="9a69a-149">Vous pouvez également le faire à partir du [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou de l’[Explorateur de stockage Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9a69a-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="9a69a-150">Charger un objet blob dans un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="9a69a-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="9a69a-151">Une fois que vous avez [créé un conteneur d’objets blob](#create-a-blob-container), vous pouvez charger des fichiers dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="9a69a-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="9a69a-152">Cette section présente la procédure à suivre pour charger un fichier local dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="9a69a-153">Dans ces étapes, le conteneur d’objets blob créé porte le nom *test-blob-container*.</span><span class="sxs-lookup"><span data-stu-id="9a69a-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="9a69a-154">Le code de cette section part du principe que vous avez terminé les étapes décrites dans la section [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9a69a-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9a69a-155">Ouvrez le fichier `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="9a69a-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9a69a-156">Ajoutez une méthode appelée **UploadBlob** qui renvoie un objet **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="9a69a-157">Dans la méthode **UploadBlob**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9a69a-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9a69a-158">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9a69a-159">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="9a69a-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9a69a-160">Ajoutez un objet **CloudBlobContainer** représentant une référence au nom du conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9a69a-161">Comme nous l’avons expliqué précédemment, le stockage Azure prend en charge différents types d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="9a69a-162">Pour récupérer une référence à un objet blob de pages, appelez la méthode **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="9a69a-163">Pour récupérer une référence à un objet blob de blocs, appelez la méthode **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="9a69a-164">En règle générale, il est recommandé d’utiliser le type d’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="9a69a-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="9a69a-165">(Remplacez <blob-name>* par le nom que vous souhaitez donner à l’objet blob une fois ce dernier chargé.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="9a69a-166">Une fois que vous disposez d’une référence d’objet blob, vous pouvez charger n’importe quel flux de données vers cet objet en appelant la méthode **UploadFromStream** pour l’objet de cette référence.</span><span class="sxs-lookup"><span data-stu-id="9a69a-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="9a69a-167">La méthode **UploadFromStream** crée l’objet blob s’il n’existe pas. S’il existe, elle le remplace.</span><span class="sxs-lookup"><span data-stu-id="9a69a-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="9a69a-168">(Remplacez *&lt;file-to-upload>* par le chemin d’accès complet au fichier à charger.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="9a69a-169">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Objets blob**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="9a69a-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="9a69a-170">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9a69a-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9a69a-171">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="9a69a-172">Exécutez l’application, puis sélectionnez **Upload blob** (Charger l’objet blob).</span><span class="sxs-lookup"><span data-stu-id="9a69a-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="9a69a-173">La section [Répertorier les objets blob d’un conteneur d’objets blob](#list-the-blobs-in-a-blob-container) explique comment répertorier les objets blob d’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="9a69a-174">Répertorier les objets blob d’un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="9a69a-174">List the blobs in a blob container</span></span>

<span data-ttu-id="9a69a-175">Cette section explique comment répertorier les objets blob d’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="9a69a-176">Les exemples de code font référence au conteneur *test-blob-container* créé dans la section [Création d’un conteneur d’objets blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="9a69a-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9a69a-177">Le code de cette section part du principe que vous avez terminé les étapes décrites dans la section [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9a69a-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9a69a-178">Ouvrez le fichier `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="9a69a-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9a69a-179">Ajoutez une méthode appelée **ListBlobs** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="9a69a-180">Dans la méthode **ListBlobs**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9a69a-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9a69a-181">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9a69a-182">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="9a69a-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9a69a-183">Ajoutez un objet **CloudBlobContainer** représentant une référence au nom du conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9a69a-184">Pour répertorier les objets blob d’un conteneur d’objets blob, utilisez la méthode **CloudBlobContainer.ListBlobs**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="9a69a-185">La méthode **CloudBlobContainer.ListBlobs** renvoie un objet **IListBlobItem** que vous convertissez en objet **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="9a69a-186">L’extrait de code suivant énumère tous les objets blob dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="9a69a-187">Chaque objet blob est converti en objet approprié en fonction de son type, puis son nom (ou son URI, dans le cas d’un **CloudBlobDirectory**) est ajouté à une liste.</span><span class="sxs-lookup"><span data-stu-id="9a69a-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

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

    <span data-ttu-id="9a69a-188">Outre des objets blobs, les conteneurs d’objets blob peuvent contenir des répertoires.</span><span class="sxs-lookup"><span data-stu-id="9a69a-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="9a69a-189">Supposons que vous disposiez d’un conteneur d’objets blob appelé *test-blob-container* et qui présente la hiérarchie suivante :</span><span class="sxs-lookup"><span data-stu-id="9a69a-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="9a69a-190">Avec l’exemple de code précédent, la liste de la chaîne **blobs** contient des valeurs similaires à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9a69a-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="9a69a-191">Comme vous pouvez le voir, la liste inclut uniquement les entités de niveau supérieur ; elle n’inclut pas celles qui sont imbriquées (*bar.png* et *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="9a69a-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="9a69a-192">Pour répertorier toutes les entités d’un conteneur d’objets blob, vous devez appeler la méthode **CloudBlobContainer.ListBlobs** et transmettre **true** pour le paramètre **useFlatBlobListing**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="9a69a-193">La définition du paramètre **useFlatBlobListing** sur **true** renvoie une liste plate de toutes les entités du conteneur d’objets blob et produit le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="9a69a-194">Dans l’**Explorateur de solutions** de Visual Studio, développez le dossier **Vues**, cliquez avec le bouton droit sur **Objets blob**, puis sélectionnez **Ajouter -> Vue** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="9a69a-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="9a69a-195">Dans la boîte de dialogue **Ajouter une vue**, entrez **ListBlobs** pour le nom de la vue, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="9a69a-196">Ouvrez le fichier `ListBlobs.cshtml` et modifiez-le pour qu’il se présente comme l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="9a69a-197">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9a69a-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9a69a-198">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="9a69a-199">Exécutez l’application, puis sélectionnez **List blobs** (Créer une liste d’objets blob) pour afficher des résultats similaires à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="9a69a-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![Création de la liste d’objets blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="9a69a-201">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="9a69a-201">Download blobs</span></span>

<span data-ttu-id="9a69a-202">Cette section montre comment télécharger un objet blob et le conserver dans le stockage local ou lire le contenu dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="9a69a-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="9a69a-203">Les exemples de code font référence au conteneur *test-blob-container* créé dans la section [Création d’un conteneur d’objets blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="9a69a-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="9a69a-204">Ouvrez le fichier `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="9a69a-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9a69a-205">Ajoutez une méthode appelée **DownloadBlob** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="9a69a-206">Dans la méthode **DownloadBlob**, ajoutez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9a69a-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9a69a-207">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9a69a-208">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="9a69a-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9a69a-209">Ajoutez un objet **CloudBlobContainer** représentant une référence au nom du conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9a69a-210">Ajoutez un objet de référence d’objet blob en appelant la méthode **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="9a69a-211">(Remplacez *&lt;blob-name>* par le nom de l’objet blob à télécharger.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="9a69a-212">Pour télécharger un objet blob, utilisez la méthode **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream**, selon le type d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="9a69a-213">L’exemple de code suivant utilise la méthode **CloudBlockBlob.DownloadToStream** pour transférer le contenu d’un objet blob vers un objet de flux qui est ensuite conservé dans un fichier local. (Remplacez *&lt;local-file-name>* par le nom de fichier complet représentant l’emplacement à utiliser pour le téléchargement de l’objet blob.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="9a69a-214">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9a69a-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9a69a-215">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="9a69a-216">Exécutez l’application, puis sélectionnez **Download blob** (Télécharger l’objet blob) pour télécharger l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="9a69a-217">L’objet blob spécifié dans la méthode **CloudBlobContainer.GetBlockBlobReference** est téléchargé à l’emplacement indiqué dans l’appel de méthode **File.OpenWrite**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="9a69a-218">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="9a69a-218">Delete blobs</span></span>

<span data-ttu-id="9a69a-219">Les étapes suivantes montrent comment supprimer un objet blob :</span><span class="sxs-lookup"><span data-stu-id="9a69a-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9a69a-220">Le code de cette section part du principe que vous avez terminé les étapes décrites dans la section [Configuration de l’environnement de développement](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9a69a-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9a69a-221">Ouvrez le fichier `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="9a69a-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9a69a-222">Ajoutez une méthode appelée **DeleteBlob** qui renvoie un objet **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="9a69a-223">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9a69a-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9a69a-224">Le code suivant permet d'obtenir la chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure : (Remplacez *&lt;storage-account-name>* par le nom du compte de stockage Azure auquel accéder.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9a69a-225">Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.</span><span class="sxs-lookup"><span data-stu-id="9a69a-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9a69a-226">Ajoutez un objet **CloudBlobContainer** représentant une référence au nom du conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="9a69a-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9a69a-227">Ajoutez un objet de référence d’objet blob en appelant la méthode **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="9a69a-228">(Remplacez *&lt;blob-name>* par le nom de l’objet blob à supprimer.)</span><span class="sxs-lookup"><span data-stu-id="9a69a-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="9a69a-229">Dans l’**Explorateur de solutions**, développez le dossier **Vues -> Partagé** et ouvrez le fichier `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9a69a-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9a69a-230">Après le dernier élément **Html.ActionLink**, ajoutez l’élément **Html.ActionLink** suivant :</span><span class="sxs-lookup"><span data-stu-id="9a69a-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="9a69a-231">Exécutez l’application, puis sélectionnez **Delete blob** (Supprimer l’objet blob) pour supprimer l’objet blob spécifié dans l’appel de méthode **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9a69a-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9a69a-232">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a69a-232">Next steps</span></span>
<span data-ttu-id="9a69a-233">Pour plus d’informations sur les autres options de stockage de données dans Azure, consultez d’autres guides de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9a69a-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="9a69a-234">Prise en main du stockage de tables Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9a69a-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="9a69a-235">Prise en main du stockage de files d’attente Azure et des services connectés de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9a69a-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
