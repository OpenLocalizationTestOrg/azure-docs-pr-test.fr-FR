---
title: "aaaGet main du stockage d’objets Blob Azure (stockage d’objets) à l’aide de .NET | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="ce63b-103">Prise en main du stockage d’objets blob Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="ce63b-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="ce63b-104">Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB.</span><span class="sxs-lookup"><span data-stu-id="ce63b-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ce63b-105">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="ce63b-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ce63b-106">Stockage d’objets BLOB est également référencé tooas stockage d’objets.</span><span class="sxs-lookup"><span data-stu-id="ce63b-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="ce63b-107">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="ce63b-107">About this tutorial</span></span>
<span data-ttu-id="ce63b-108">Ce didacticiel montre comment le code toowrite .NET pour les scénarios courants lors de l’utilisation du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ce63b-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="ce63b-109">Les scénarios traités incluent le chargement, la création de listes, le téléchargement et la suppression d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="ce63b-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="ce63b-110">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="ce63b-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="ce63b-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce63b-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="ce63b-112">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="ce63b-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="ce63b-113">Gestionnaire de configuration Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ce63b-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="ce63b-114">Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="ce63b-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="ce63b-115">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="ce63b-115">More samples</span></span>
<span data-ttu-id="ce63b-116">Pour obtenir des exemples supplémentaires utilisant Blob Storage, voir [Prise en main d’Azure Blob Storage dans .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="ce63b-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="ce63b-117">Vous pouvez télécharger l’exemple d’application hello et exécutez-le ou parcourir le code hello sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce63b-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="ce63b-118">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="ce63b-118">Add using directives</span></span>
<span data-ttu-id="ce63b-119">Ajoutez hello suivant **à l’aide de** haut toohello de directives de hello `Program.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="ce63b-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="ce63b-120">Analyser la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="ce63b-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="ce63b-121">Créer le client du service Blob hello</span><span class="sxs-lookup"><span data-stu-id="ce63b-121">Create hello Blob service client</span></span>
<span data-ttu-id="ce63b-122">Hello **CloudBlobClient** classe vous permet de tooretrieve conteneurs et objets BLOB stockés dans le stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="ce63b-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="ce63b-123">Voici un moyen toocreate hello service client :</span><span class="sxs-lookup"><span data-stu-id="ce63b-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="ce63b-124">Vous êtes maintenant code prêt toowrite qui lit les données à partir d’et écrit le stockage des données tooBlob.</span><span class="sxs-lookup"><span data-stu-id="ce63b-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ce63b-125">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="ce63b-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ce63b-126">Cet exemple montre comment toocreate un conteneur s’il n’existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="ce63b-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="ce63b-127">Par défaut, le nouveau conteneur de hello est privé, ce qui signifie que vous devez spécifier vos objets BLOB de stockage accès toodownload clé à partir de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="ce63b-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="ce63b-128">Si vous souhaitez que les fichiers hello toomake tooeveryone de hello conteneur disponible, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ce63b-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="ce63b-129">Toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public.</span><span class="sxs-lookup"><span data-stu-id="ce63b-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="ce63b-130">Toutefois, vous pouvez modifier ou supprimer uniquement si vous avez une signature d’accès partagé ou de clé d’accès hello compte approprié.</span><span class="sxs-lookup"><span data-stu-id="ce63b-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ce63b-131">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="ce63b-131">Upload a blob into a container</span></span>
<span data-ttu-id="ce63b-132">Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.</span><span class="sxs-lookup"><span data-stu-id="ce63b-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="ce63b-133">Dans la plupart des cas, objet blob de blocs est hello recommandé toouse de type.</span><span class="sxs-lookup"><span data-stu-id="ce63b-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="ce63b-134">tooupload fichier tooa objet blob de blocs, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob de bloc.</span><span class="sxs-lookup"><span data-stu-id="ce63b-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="ce63b-135">Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **UploadFromStream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ce63b-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="ce63b-136">Cette opération crée l’objet blob de hello si elle n’existe pas déjà, ou le remplace s’il existe.</span><span class="sxs-lookup"><span data-stu-id="ce63b-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="ce63b-137">Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="ce63b-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ce63b-138">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="ce63b-138">List hello blobs in a container</span></span>
<span data-ttu-id="ce63b-139">objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur.</span><span class="sxs-lookup"><span data-stu-id="ce63b-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="ce63b-140">Vous pouvez ensuite utiliser du conteneur hello **ListBlobs** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="ce63b-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="ce63b-141">tooaccess hello ensemble complet des propriétés et méthodes pour retourné **IListBlobItem**, vous devez effectuer un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objet.</span><span class="sxs-lookup"><span data-stu-id="ce63b-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="ce63b-142">Si le type de hello est inconnu, vous pouvez utiliser un toodetermine de vérification de type qui toocast à.</span><span class="sxs-lookup"><span data-stu-id="ce63b-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="ce63b-143">Hello de code suivant montre comment tooretrieve et sortie hello URI de chaque élément Bonjour _photos_ conteneur :</span><span class="sxs-lookup"><span data-stu-id="ce63b-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

<span data-ttu-id="ce63b-144">En incluant les informations de chemin d’accès aux noms des objets blob, vous obtenez alors une structure de répertoires virtuels que vous pouvez organiser et parcourir de la même manière qu’un système de fichiers traditionnel.</span><span class="sxs-lookup"><span data-stu-id="ce63b-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="ce63b-145">structure de répertoire Hello est virtuel uniquement : hello uniquement les ressources disponibles dans le stockage d’objets Blob sont des conteneurs et objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="ce63b-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="ce63b-146">Toutefois, la bibliothèque cliente de stockage hello propose un **CloudBlobDirectory** répertoire virtuel de toorefer tooa de l’objet et de simplifier les processus de hello de travailler avec des objets BLOB qui sont organisées de cette façon.</span><span class="sxs-lookup"><span data-stu-id="ce63b-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="ce63b-147">Par exemple, considérez hello ensemble suivant d’objets BLOB de blocs dans un conteneur nommé *photos*:</span><span class="sxs-lookup"><span data-stu-id="ce63b-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="ce63b-148">Lorsque vous appelez **ListBlobs** sur hello *photos* conteneur (par exemple hello précédant l’extrait de code), une liste hiérarchique est retournée.</span><span class="sxs-lookup"><span data-stu-id="ce63b-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="ce63b-149">Il contient à la fois **CloudBlobDirectory** et **CloudBlockBlob** objets représentant les répertoires de hello et les objets BLOB dans le conteneur de hello, respectivement.</span><span class="sxs-lookup"><span data-stu-id="ce63b-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="ce63b-150">résultat de Hello ressemble à :</span><span class="sxs-lookup"><span data-stu-id="ce63b-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="ce63b-151">Si vous le souhaitez, vous pouvez définir hello **UseFlatBlobListing** paramètre Hello **ListBlobs** méthode **true**.</span><span class="sxs-lookup"><span data-stu-id="ce63b-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="ce63b-152">Dans ce cas, chaque objet blob dans le conteneur de hello est retourné comme un **CloudBlockBlob** objet.</span><span class="sxs-lookup"><span data-stu-id="ce63b-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="ce63b-153">Hello appel trop**ListBlobs** tooreturn une liste plate ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="ce63b-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="ce63b-154">et les résultats hello ressemblent à ceci :</span><span class="sxs-lookup"><span data-stu-id="ce63b-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="ce63b-155">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="ce63b-155">Download blobs</span></span>
<span data-ttu-id="ce63b-156">objets BLOB toodownload, tout d’abord extraire une référence d’objet blob et ensuite appeler hello **méthodes DownloadToStream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ce63b-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="ce63b-157">exemple Hello utilise hello **méthodes DownloadToStream** méthode tootransfer hello contenu tooa flux de données objet blob que peuvent alors être conservées tooa des fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="ce63b-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="ce63b-158">Vous pouvez également utiliser hello **méthodes DownloadToStream** contenu de hello toodownload de méthode d’un objet blob comme une chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="ce63b-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="ce63b-159">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="ce63b-159">Delete blobs</span></span>
<span data-ttu-id="ce63b-160">toodelete un objet blob, commencez par obtenir une référence d’objet blob, puis appelez le **supprimer** méthode dessus.</span><span class="sxs-lookup"><span data-stu-id="ce63b-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="ce63b-161">Création d’une liste d’objets blob dans des pages de manière asynchrone</span><span class="sxs-lookup"><span data-stu-id="ce63b-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="ce63b-162">Si vous répertoriez un grand nombre d’objets BLOB, ou nombre de hello toocontrol de vous renvoyer dans une opération de liste de résultats, vous pouvez répertorier les objets BLOB dans les pages de résultats.</span><span class="sxs-lookup"><span data-stu-id="ce63b-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="ce63b-163">Cet exemple montre comment tooreturn produit des pages de façon asynchrone, afin que l’exécution n’est pas bloquée lors de l’attente tooreturn un grand ensemble de résultats.</span><span class="sxs-lookup"><span data-stu-id="ce63b-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="ce63b-164">Cet exemple montre un liste plate d’objets blob, mais vous pouvez également effectuer une liste hiérarchique, en définissant un hello _useFlatBlobListing_ paramètre Hello **ListBlobsSegmentedAsync** too_false_ de méthode.</span><span class="sxs-lookup"><span data-stu-id="ce63b-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="ce63b-165">Étant donné que la méthode d’échantillonnage hello appelle une méthode asynchrone, il doit commencer par hello _async_ (mot clé) et doit retourner un **tâche** objet.</span><span class="sxs-lookup"><span data-stu-id="ce63b-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="ce63b-166">Hello await mot clé spécifié pour hello **ListBlobsSegmentedAsync** méthode suspend l’exécution de méthode d’échantillonnage hello jusqu'à la fin de tâche de liste hello.</span><span class="sxs-lookup"><span data-stu-id="ce63b-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="ce63b-167">Écriture tooan ajouter des objets blob</span><span class="sxs-lookup"><span data-stu-id="ce63b-167">Writing tooan append blob</span></span>
<span data-ttu-id="ce63b-168">Il est optimisé pour les opérations d’ajout, telles que la journalisation.</span><span class="sxs-lookup"><span data-stu-id="ce63b-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="ce63b-169">Comme un objet blob de blocs, un objet blob d’ajout est constitué de blocs, mais lorsque vous ajoutez un nouvel objet blob bloc tooan append, il est toujours ajouté toohello de fin de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="ce63b-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="ce63b-170">Vous ne pouvez pas mettre à jour ou supprimer un bloc dans un objet blob d’ajout.</span><span class="sxs-lookup"><span data-stu-id="ce63b-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="ce63b-171">ID de bloc Hello pour un objet blob d’ajout ne sont pas exposés à ceux d’un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="ce63b-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="ce63b-172">Chaque bloc dans un objet blob d’ajout peut avoir une taille différente, les tooa au maximum de 4 Mo, et un objet blob d’ajout peut inclure un maximum de 50 000 blocs.</span><span class="sxs-lookup"><span data-stu-id="ce63b-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="ce63b-173">Hello taille maximale d’un objet blob d’ajout est par conséquent légèrement supérieur à 195 Go (4 Mo X avec 50 000 blocs).</span><span class="sxs-lookup"><span data-stu-id="ce63b-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="ce63b-174">exemple Hello ci-dessous crée un nouvel objet blob d’ajout et ajoute certaines tooit de données, en simulant une opération de journalisation simple.</span><span class="sxs-lookup"><span data-stu-id="ce63b-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="ce63b-175">Consultez [objets BLOB de blocs, objets BLOB de pages et ajouter des objets BLOB](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) pour plus d’informations sur les différences de hello entre types hello trois d’objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="ce63b-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="ce63b-176">Gestion de la sécurité pour les objets blob</span><span class="sxs-lookup"><span data-stu-id="ce63b-176">Managing security for blobs</span></span>
<span data-ttu-id="ce63b-177">Par défaut, le stockage Azure conserve vos données sécurisées en limitant le propriétaire du compte accès toohello, qui est en possession des clés d’accès compte hello.</span><span class="sxs-lookup"><span data-stu-id="ce63b-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="ce63b-178">Lorsque vous avez besoin des données d’objet blob tooshare dans votre compte de stockage, il est important toodo c’est le cas sans compromettre la sécurité hello des clés d’accès de votre compte.</span><span class="sxs-lookup"><span data-stu-id="ce63b-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="ce63b-179">En outre, vous pouvez chiffrer tooensure de données d’objet blob est sécurisé va acheminement hello et dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ce63b-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="ce63b-180">Contrôle de l’accès aux données de tooblob</span><span class="sxs-lookup"><span data-stu-id="ce63b-180">Controlling access tooblob data</span></span>
<span data-ttu-id="ce63b-181">Par défaut, les données d’objet blob hello dans votre compte de stockage sont accessible uniquement propriétaire du compte toostorage.</span><span class="sxs-lookup"><span data-stu-id="ce63b-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="ce63b-182">L’authentification des demandes sur le stockage d’objets Blob nécessite une clé d’accès compte hello à par défaut.</span><span class="sxs-lookup"><span data-stu-id="ce63b-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="ce63b-183">Toutefois, vous souhaiterez peut-être toomake certains utilisateurs tooother disponibles des données d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="ce63b-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="ce63b-184">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="ce63b-184">You have two options:</span></span>

* <span data-ttu-id="ce63b-185">**Accès anonyme :** vous pouvez rendre un conteneur ou ses objets blob disponibles publiquement pour un accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="ce63b-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="ce63b-186">Consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](storage-manage-access-to-resources.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ce63b-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="ce63b-187">**Signatures d’accès partagé :** vous pouvez fournir des clients avec une signature d’accès partagé (SAS), qui fournit des ressources de tooa accès délégué dans votre compte de stockage, avec des autorisations que vous spécifiez et sur un intervalle que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="ce63b-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="ce63b-188">Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="ce63b-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="ce63b-189">Chiffrement des données d’objets blob</span><span class="sxs-lookup"><span data-stu-id="ce63b-189">Encrypting blob data</span></span>
<span data-ttu-id="ce63b-190">Le stockage Azure prend en charge le chiffrement des données d’objet blob au client de hello et sur le serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="ce63b-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="ce63b-191">**Le chiffrement côté client :** hello bibliothèque cliente de stockage pour .NET prend en charge le chiffrement des données dans les applications clientes avant chargement tooAzure stockage et le déchiffrement des données lors du téléchargement de toohello client.</span><span class="sxs-lookup"><span data-stu-id="ce63b-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="ce63b-192">bibliothèque de Hello prend également en charge l’intégration avec le coffre de clés Azure pour la gestion de clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ce63b-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="ce63b-193">Pour plus d’informations, voir [Chiffrement côté client avec .NET pour Microsoft Azure Storage](storage-client-side-encryption.md) .</span><span class="sxs-lookup"><span data-stu-id="ce63b-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="ce63b-194">Voir également [Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l’aide d’Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ce63b-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="ce63b-195">**Chiffrement côté serveur**: Azure Storage prend désormais en charge le chiffrement côté serveur.</span><span class="sxs-lookup"><span data-stu-id="ce63b-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="ce63b-196">Voir [Azure Storage Service Encryption pour les données au repos (version préliminaire)](storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="ce63b-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce63b-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce63b-197">Next steps</span></span>
<span data-ttu-id="ce63b-198">Maintenant que vous avez appris les notions de base de hello du stockage Blob, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="ce63b-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="ce63b-199">Explorateur Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ce63b-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="ce63b-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="ce63b-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="ce63b-201">Exemples relatifs à Blob Storage</span><span class="sxs-lookup"><span data-stu-id="ce63b-201">Blob storage samples</span></span>
* [<span data-ttu-id="ce63b-202">Prise en main d’Azure Blob Storage dans .NET</span><span class="sxs-lookup"><span data-stu-id="ce63b-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="ce63b-203">Documentation de référence sur le stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="ce63b-203">Blob storage reference</span></span>
* [<span data-ttu-id="ce63b-204">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="ce63b-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="ce63b-205">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="ce63b-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="ce63b-206">Guides conceptuels</span><span class="sxs-lookup"><span data-stu-id="ce63b-206">Conceptual guides</span></span>
* [<span data-ttu-id="ce63b-207">Transfert de données avec hello utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="ce63b-207">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="ce63b-208">Prise en main du stockage de fichier pour .NET</span><span class="sxs-lookup"><span data-stu-id="ce63b-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="ce63b-209">Comment toouse Azure stockage d’objets blob par hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="ce63b-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
