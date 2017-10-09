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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Prise en main du stockage d’objets blob Azure et des services connectés de Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble

Stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

Ce didacticiel montre comment toowrite ASP.NET de code pour les scénarios courants à l’aide du stockage d’objets blob Azure. Ces scénarios incluent la création d’un conteneur d’objets blob, ainsi que le chargement, la création d’une liste, le téléchargement et la suppression d’objets blob.

##<a name="prerequisites"></a>Composants requis

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Créer un contrôleur MVC 

1. Bonjour **l’Explorateur de solutions**, avec le bouton droit **contrôleurs**et, dans le menu contextuel de hello, sélectionnez **Ajouter -> contrôleur**.

    ![Ajouter une application ASP.NET MVC de tooan contrôleur](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. Sur hello **ajouter une vue de structure** boîte de dialogue, sélectionnez **contrôleur MVC 5 - vide**, puis sélectionnez **ajouter**.

    ![Spécifier le type de contrôleur MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. Sur hello **ajouter un contrôleur** boîte de dialogue, nom hello du contrôleur *BlobsController*, puis sélectionnez **ajouter**.

    ![Contrôleur MVC de hello nom](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Ajoutez hello suivant *à l’aide de* directives toohello `BlobsController.cs` fichier :

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Création d’un conteneur d’objets blob

Un conteneur d’objets blob est une hiérarchie imbriquée d’objets blobs et de dossiers. Hello étapes suivantes illustrent comment toocreate un conteneur d’objets blob :

> [!NOTE]
> 
> Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `BlobsController.cs` fichier.

1. Ajoutez une méthode appelée **CreateBlobContainer** qui retourne un objet **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **CreateBlobContainer** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Utilisez hello suivant code tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello. (Modification  *&lt;storage-account-name >* nom toohello Hello compte de stockage Azure que vous êtes en train d’accéder.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur de référence toohello blob souhaité. Hello **CloudBlobClient.GetContainerReference** méthode ne rend pas une demande pour le stockage d’objets blob. référence de Hello est retournée que conteneur d’objets blob hello existe ou non. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Appelez hello **CloudBlobContainer.CreateIfNotExists** conteneur de hello toocreate méthode s’il n’existe pas encore. Hello **CloudBlobContainer.CreateIfNotExists** méthode retourne **true** si le conteneur de hello n’existe pas et a été correctement créé. Sinon, la valeur **false** est retournée.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Hello de mise à jour **ViewBag** par nom de hello du conteneur d’objets blob hello.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **BLOB**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **CreateBlobContainer** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `CreateBlobContainer.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Exécutez l’application hello et sélectionnez **créer un conteneur d’objets Blob** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Création du conteneur d’objets blob](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Comme mentionné précédemment, hello **CloudBlobContainer.CreateIfNotExists** méthode retourne **true** uniquement lorsque le conteneur de hello n’existe pas et est créé. Par conséquent, si vous exécutez une application hello lorsque hello conteneur existe, méthode hello retourne **false**. toorun hello application plusieurs fois, que vous devez supprimer le conteneur de hello avant de réexécuter l’application hello. Conteneur de hello suppression peut être effectuée via hello **CloudBlobContainer.Delete** (méthode). Vous pouvez également supprimer le conteneur de hello à l’aide de hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Charger un objet blob dans un conteneur d’objets blob

Une fois que vous avez [créé un conteneur d’objets blob](#create-a-blob-container), vous pouvez charger des fichiers dans ce conteneur. Cette section vous guide dans le processus de téléchargement d’un conteneur d’objets blob tooa fichier local. étapes de Hello supposent que vous avez créé un conteneur d’objets blob nommé *conteneur d’objets blob test*. 

> [!NOTE]
> 
> Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `BlobsController.cs` fichier.

1. Ajoutez une méthode appelée **UploadBlob** qui renvoie un objet **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Au sein de hello **UploadBlob** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Comme nous l’avons expliqué précédemment, le stockage Azure prend en charge différents types d’objets blob. tooretrieve référence tooa objet blob de pages, appel hello **CloudBlobContainer.GetPageBlobReference** (méthode). tooretrieve référence tooa objet blob de blocs, appel hello **CloudBlobContainer.GetBlockBlobReference** (méthode). En règle générale, objet blob de blocs est hello recommandé toouse de type. (Modification < nom d’objet blob > * nom toohello blob de hello toogive téléchargé qu’une seule fois.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Une fois que vous avez une référence d’objet blob, vous pouvez télécharger tout tooit de flux de données en appelant l’objet de référence blob hello **UploadFromStream** (méthode). Hello **UploadFromStream** méthode crée l’objet blob de hello si elle n’existe pas, ou le remplace s’il existe. (Modification  *&lt;de téléchargement de fichier >* tooa complet en chemin d’accès toohello fichier tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **BLOB**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Exécutez l’application hello et sélectionnez **téléchargement blob**.  
  
Hello section - [répertorier les objets BLOB de hello dans un conteneur d’objets blob](#list-the-blobs-in-a-blob-container) -illustre comment hello de toolist les objets BLOB dans un conteneur d’objets blob.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Répertorier les objets BLOB hello dans un conteneur d’objets blob

Cette section illustre comment hello de toolist les objets BLOB dans un conteneur d’objets blob. exemple de code Hello référence hello *conteneur d’objets blob test* créé dans la section de hello, [créer un conteneur d’objets blob](#create-a-blob-container).

> [!NOTE]
> 
> Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `BlobsController.cs` fichier.

1. Ajoutez une méthode appelée **ListBlobs** qui renvoie un objet **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Au sein de hello **ListBlobs** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. objets BLOB de hello toolist dans un conteneur d’objets blob, utilisez hello **CloudBlobContainer.ListBlobs** (méthode). Hello **CloudBlobContainer.ListBlobs** méthode retourne un **IListBlobItem** de l’objet que vous effectuez un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou **CloudBlobDirectory** objet. Hello extrait de code suivant énumère tous les objets BLOB de hello dans un conteneur d’objets blob. Chaque objet blob est l’objet approprié de cast toohello en fonction de son type et son nom (ou URI dans les cas de hello d’un **CloudBlobDirectory**) est ajouté à la liste de tooa.

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

    Dans tooblobs de plus, les conteneurs d’objets blob peuvent contenir des répertoires. Supposons que vous avez un conteneur d’objets blob appelé *conteneur d’objets blob test* avec hello suivant la hiérarchie :

        foo.png
        dir1/bar.png
        dir2/baz.png

    À l’aide de hello précédant l’exemple de code, hello **BLOB** liste des chaînes contient suivant toohello similaire de valeurs :

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Comme vous pouvez le voir, liste de hello inclut hello uniquement à des entités niveau supérieur ; hello pas imbriqués celles (*bar.png* et *baz.png*). toolist tous hello entités au sein d’un conteneur d’objets blob, vous devez appeler hello **CloudBlobContainer.ListBlobs** méthode et passe **true** pour hello **useFlatBlobListing** paramètre.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Hello du paramètre **useFlatBlobListing** paramètre trop**true** retourne une liste plate de toutes les entités dans le conteneur d’objets blob hello et produit hello suivant des résultats :

        foo.png
        dir1/bar.png
        dir2/baz.png

1. Bonjour **l’Explorateur de solutions**, développez hello **vues** dossier, avec le bouton droit **BLOB**, puis, dans le menu contextuel de hello, sélectionnez **Ajouter -> affichage**.

1. Sur hello **ajouter une vue** boîte de dialogue, entrez **ListBlobs** pour le nom de la vue hello, puis sélectionnez **ajouter**.

1. Ouvrez `ListBlobs.cshtml`et modifiez-le pour qu’il ressemble hello suivant extrait de code :

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

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Exécutez l’application hello et sélectionnez **répertorier les objets BLOB** toosee des résultats similaires toohello suivant capture d’écran :
  
    ![Création de la liste d’objets blob](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Télécharger des objets blob

Cette section illustre comment toodownload un objet blob et soit conserver il toolocal stockage ou lecture hello contenu dans une chaîne. exemple de code Hello référence hello *conteneur d’objets blob test* créé dans la section de hello, [créer un conteneur d’objets blob](#create-a-blob-container).

1. Ouvrez hello `BlobsController.cs` fichier.

1. Ajoutez une méthode appelée **DownloadBlob** qui renvoie un objet **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Au sein de hello **DownloadBlob** (méthode), obtenir un **CloudStorageAccount** objet qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Ajoutez un objet de référence d’objet blob en appelant la méthode **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**. (Modification  *&lt;-nom d’objet blob >* toohello les nom d’objet blob hello en cours de téléchargement.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload un objet blob, utilisez hello **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream** (méthode), selon le type d’objet blob hello. Hello extrait de code suivant utilise hello **CloudBlockBlob.DownloadToStream** tootransfer méthode flux de tooa contenu d’un objet blob de l’objet qui est ensuite rendue persistante fichier local de tooa : (modification  *&lt;nom de fichier local >* toohello complet représentant de nom du fichier où vous souhaitez blob hello téléchargé.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Exécutez l’application hello et sélectionnez **téléchargement blob** objet blob de toodownload hello. objet blob de Hello spécifié Bonjour **CloudBlobContainer.GetBlockBlobReference** appel de méthode télécharge emplacement toohello que vous spécifiez dans hello **File.OpenWrite** appel de méthode. 

## <a name="delete-blobs"></a>Suppression d’objets blob

Hello étapes suivantes illustrent comment toodelete un objet blob :

> [!NOTE]
> 
> Hello code dans cette section part du principe que vous avez effectué les étapes de hello dans la section de hello, [configuration d’environnement de développement hello](#set-up-the-development-environment). 

1. Ouvrez hello `BlobsController.cs` fichier.

1. Ajoutez une méthode appelée **DeleteBlob** qui renvoie un objet **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage. Tooget hello connexion chaîne et le stockage informations compte de stockage à partir de la configuration du service Azure hello de code suivant de hello utilisation : (modification  *&lt;storage-account-name >* nom toohello Hello stockage Azure compte qu'auquel vous accédez).
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ajoutez un objet **CloudBlobClient** représentant un client du service BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtenir un **CloudBlobContainer** objet qui représente un nom de conteneur toohello référence. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Ajoutez un objet de référence d’objet blob en appelant la méthode **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**. (Modification  *&lt;-nom d’objet blob >* toohello nom de hello blob que vous supprimez.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. Bonjour **l’Explorateur de solutions**, développez hello **vues -> Shared** dossier, puis ouvrez `_Layout.cshtml`.

1. Après avoir hello dernière **Html.ActionLink**, ajoutez hello suivant **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Exécutez l’application hello et sélectionnez **Delete blob** toodelete blob de hello spécifié dans hello **CloudBlobContainer.GetBlockBlobReference** appel de méthode. 

## <a name="next-steps"></a>Étapes suivantes
Permet d’afficher plusieurs toolearn de repères de fonctionnalité sur les options supplémentaires pour le stockage des données dans Azure.

  * [Prise en main du stockage de tables Azure et des services connectés de Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Prise en main du stockage de files d’attente Azure et des services connectés de Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-queues.md)
