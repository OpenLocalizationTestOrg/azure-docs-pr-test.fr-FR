---
title: aaaDevelop pour le stockage de fichiers Azure avec Java | Documents Microsoft
description: "Découvrez comment des applications Java toodevelop et les services qui utilisent des fichiers Azure storage toostore fichier des données."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="c610f-103">Développer pour le stockage de fichiers Azure avec Java</span><span class="sxs-lookup"><span data-stu-id="c610f-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="c610f-104">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="c610f-104">About this tutorial</span></span>
<span data-ttu-id="c610f-105">Ce didacticiel va vous montrer bases hello de l’utilisation des applications Java toodevelop ou services qui utilisent des données de fichier toostore fichier Azure storage.</span><span class="sxs-lookup"><span data-stu-id="c610f-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="c610f-106">Dans ce didacticiel, nous crée une application console simple et montrent comment les actions de base tooperform avec Java et le fichier Azure storage :</span><span class="sxs-lookup"><span data-stu-id="c610f-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="c610f-107">Créer et supprimer des partages de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="c610f-108">Créer et supprimer des répertoires</span><span class="sxs-lookup"><span data-stu-id="c610f-108">Create and delete directories</span></span>
* <span data-ttu-id="c610f-109">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="c610f-110">Charger, télécharger et supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="c610f-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="c610f-111">Stockage de fichiers Azure sont accessibles sur SMB, il est toowrite possible les applications simples qui accéder au partage de fichiers Azure hello à l’aide des classes d’e/s Java standard hello.</span><span class="sxs-lookup"><span data-stu-id="c610f-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="c610f-112">Cet article décrit comment toowrite les applications qui utilisent hello SDK Java Azure Storage, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c610f-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="c610f-113">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="c610f-113">Create a Java application</span></span>
<span data-ttu-id="c610f-114">exemples de hello toobuild, vous devez hello Kit de développement Java (JDK) et [] de hello (SDK de stockage Azure pour Java).</span><span class="sxs-lookup"><span data-stu-id="c610f-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="c610f-115">Vous devez également avoir préalablement créé un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c610f-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="c610f-116">Le programme d’installation de votre application de toouse stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="c610f-117">toouse hello API, le stockage Azure ajouter hello suivant en haut de toohello instruction hello du fichier de Java où vous avez l’intention tooaccess hello service de stockage.</span><span class="sxs-lookup"><span data-stu-id="c610f-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="c610f-118">Configuration d’une chaîne de connexion de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="c610f-119">toouse stockage Azure, vous avez besoin de compte de stockage Azure tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c610f-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c610f-120">Hello première étape serait tooconfigure une chaîne de connexion que nous allons utiliser compte de stockage tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c610f-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="c610f-121">Nous allons définir une toodo variable statique qui.</span><span class="sxs-lookup"><span data-stu-id="c610f-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="c610f-122">Remplacez your_storage_account_name et your_storage_account_key par des valeurs réelles de hello pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c610f-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="c610f-123">Connexion de compte de stockage Azure tooan</span><span class="sxs-lookup"><span data-stu-id="c610f-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="c610f-124">compte de stockage tooconnect tooyour, vous devez toouse hello **CloudStorageAccount** objet, en passant un tooits de chaîne de connexion **analyser** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c610f-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="c610f-125">**CloudStorageAccount.parse** lève une InvalidKeyException et vous devrez donc tooput à l’intérieur d’une instruction try/catch bloquer.</span><span class="sxs-lookup"><span data-stu-id="c610f-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="c610f-126">Création d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-126">Create an Azure File share</span></span>
<span data-ttu-id="c610f-127">Tous les fichiers et répertoires d’un stockage de fichiers Azure se trouvent dans un conteneur appelé **Partage**.</span><span class="sxs-lookup"><span data-stu-id="c610f-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="c610f-128">Votre compte de stockage peut avoir autant de partages que le permet la capacité de votre compte.</span><span class="sxs-lookup"><span data-stu-id="c610f-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="c610f-129">partage de tooa accès tooobtain et son contenu, vous devez toouse un client de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="c610f-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="c610f-130">À l’aide du client de stockage de fichier Azure hello, vous pouvez ensuite obtenir un partage de tooa de référence.</span><span class="sxs-lookup"><span data-stu-id="c610f-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="c610f-131">tooactually créer le partage de hello, utilisez hello **createIfNotExists** méthode d’objet de CloudFileShare hello.</span><span class="sxs-lookup"><span data-stu-id="c610f-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="c610f-132">À ce stade, **partager** contient un partage de tooa référence nommé **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="c610f-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="c610f-133">Suppression d’un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-133">Delete an Azure File share</span></span>
<span data-ttu-id="c610f-134">Suppression d’un partage est effectuée en appelant hello **deleteIfExists** méthode sur un objet CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="c610f-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="c610f-135">Voici un exemple de code permettant d’effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="c610f-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="c610f-136">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="c610f-136">Create a directory</span></span>
<span data-ttu-id="c610f-137">Vous pouvez également organiser le stockage en plaçant les fichiers dans les sous-répertoires au lieu d’avoir tous les dans le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="c610f-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="c610f-138">Stockage de fichier Azure vous permet de toocreate que le permettent de répertoires car votre compte.</span><span class="sxs-lookup"><span data-stu-id="c610f-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="c610f-139">code Hello ci-dessous crée un sous-répertoire nommé **sampledir** sous le répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="c610f-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="c610f-140">Supprimer un répertoire</span><span class="sxs-lookup"><span data-stu-id="c610f-140">Delete a directory</span></span>
<span data-ttu-id="c610f-141">La suppression d’un répertoire est une tâche relativement simple, mais il convient de noter que vous ne pouvez pas supprimer de répertoire contenant des fichiers ou d’autres répertoires.</span><span class="sxs-lookup"><span data-stu-id="c610f-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="c610f-142">Énumérer des fichiers et répertoires dans un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="c610f-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="c610f-143">Il est facile d’obtenir la liste de fichiers et de répertoires d’un partage en appelant **listFilesAndDirectories** sur une référence CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="c610f-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="c610f-144">méthode Hello retourne une liste d’objets ListFileItem dont vous pouvez effectuer une itération sur.</span><span class="sxs-lookup"><span data-stu-id="c610f-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="c610f-145">Par exemple, hello de code suivant répertorie les fichiers et répertoires à l’intérieur du répertoire racine de hello.</span><span class="sxs-lookup"><span data-stu-id="c610f-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="c610f-146">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="c610f-146">Upload a file</span></span>
<span data-ttu-id="c610f-147">Un fichier Azure partage contient de hello très moins, un répertoire racine où les fichiers peuvent résider.</span><span class="sxs-lookup"><span data-stu-id="c610f-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="c610f-148">Dans cette section, vous allez apprendre comment tooupload un fichier à partir du stockage local sur hello racine du répertoire d’un partage.</span><span class="sxs-lookup"><span data-stu-id="c610f-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="c610f-149">première étape de Hello lors du téléchargement d’un fichier est tooobtain un répertoire toohello de référence où elle doit résider.</span><span class="sxs-lookup"><span data-stu-id="c610f-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="c610f-150">Pour ce faire, l’appelant hello **getRootDirectoryReference** méthode d’objet de partage hello.</span><span class="sxs-lookup"><span data-stu-id="c610f-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="c610f-151">Maintenant que vous avez un répertoire de racine référence toohello du partage de hello, vous pouvez télécharger un fichier sur celui-ci à l’aide de hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="c610f-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="c610f-152">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="c610f-152">Download a file</span></span>
<span data-ttu-id="c610f-153">Un des plus fréquentes sur le stockage de fichiers Azure, vous allez effectuer les opérations de hello est les fichiers toodownload.</span><span class="sxs-lookup"><span data-stu-id="c610f-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="c610f-154">Dans l’exemple suivant de hello, code de hello télécharge SampleFile.txt et affiche son contenu.</span><span class="sxs-lookup"><span data-stu-id="c610f-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="c610f-155">Supprimer un fichier</span><span class="sxs-lookup"><span data-stu-id="c610f-155">Delete a file</span></span>
<span data-ttu-id="c610f-156">La suppression de fichiers est également une opération courante liée au stockage des fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="c610f-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="c610f-157">Hello de code suivant supprime un fichier nommé SampleFile.txt stocké à l’intérieur d’un répertoire nommé **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="c610f-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="c610f-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c610f-158">Next steps</span></span>
<span data-ttu-id="c610f-159">Si vous souhaitez que toolearn plus d’informations sur d’autres API de stockage Azure, suivez ces liens.</span><span class="sxs-lookup"><span data-stu-id="c610f-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="c610f-160">[Azure pour les développeurs Java](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="c610f-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="c610f-161">Kit de développement logiciel (SDK) Azure Storage pour Java</span><span class="sxs-lookup"><span data-stu-id="c610f-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="c610f-162">Kit de développement logiciel (SDK) Azure Storage pour Android</span><span class="sxs-lookup"><span data-stu-id="c610f-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="c610f-163">Référence du Kit de développement logiciel (SDK) du client Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c610f-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="c610f-164">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c610f-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="c610f-165">Blog de l’équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c610f-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="c610f-166">[Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="c610f-166">[Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>