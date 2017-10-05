---
title: "Prise en main du stockage d’objets blob Azure à l’aide de .NET | Microsoft Docs"
description: "Stockez des données non structurées dans le cloud avec Azure Blob Storage (stockage d’objets)."
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
ms.openlocfilehash: 70c7d6a5e1b9aa9a13481893e0baa56538be097c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="f83ea-103">Prise en main du stockage d’objets blob Azure à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="f83ea-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="f83ea-104">Le stockage d’objets blob Azure est un service qui stocke des données non structurées dans le cloud en tant qu’objets/blobs.</span><span class="sxs-lookup"><span data-stu-id="f83ea-104">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="f83ea-105">Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application.</span><span class="sxs-lookup"><span data-stu-id="f83ea-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="f83ea-106">Le stockage d’objets blob est également appelé Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f83ea-106">Blob storage is also referred to as object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="f83ea-107">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="f83ea-107">About this tutorial</span></span>
<span data-ttu-id="f83ea-108">Ce didacticiel montre comment écrire du code .NET pour des scénarios courants d’utilisation du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f83ea-108">This tutorial shows how to write .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="f83ea-109">Les scénarios traités incluent le chargement, la création de listes, le téléchargement et la suppression d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="f83ea-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="f83ea-110">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="f83ea-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="f83ea-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f83ea-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="f83ea-112">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="f83ea-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="f83ea-113">Gestionnaire de configuration Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="f83ea-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="f83ea-114">Un [compte de stockage Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="f83ea-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="f83ea-115">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="f83ea-115">More samples</span></span>
<span data-ttu-id="f83ea-116">Pour obtenir des exemples supplémentaires utilisant Blob Storage, voir [Prise en main d’Azure Blob Storage dans .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="f83ea-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="f83ea-117">Vous pouvez télécharger l’exemple d’application et l’exécuter ou parcourir le code sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f83ea-117">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="f83ea-118">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="f83ea-118">Add using directives</span></span>
<span data-ttu-id="f83ea-119">Ajoutez les directives **d’utilisation** suivantes au fichier `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="f83ea-119">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="f83ea-120">Analyse de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="f83ea-120">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a><span data-ttu-id="f83ea-121">Créer le client du service Blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-121">Create the Blob service client</span></span>
<span data-ttu-id="f83ea-122">La classe **CloudBlobClient** vous permet de récupérer des conteneurs et des objets blob stockés dans Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f83ea-122">The **CloudBlobClient** class enables you to retrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="f83ea-123">Voici un moyen de créer le client du service :</span><span class="sxs-lookup"><span data-stu-id="f83ea-123">Here's one way to create the service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="f83ea-124">Vous êtes maintenant prêt à écrire du code qui lit et écrit des données dans le Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f83ea-124">Now you are ready to write code that reads data from and writes data to Blob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="f83ea-125">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="f83ea-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="f83ea-126">Cet exemple montre comment créer un conteneur, si celui-ci n’existe pas encore :</span><span class="sxs-lookup"><span data-stu-id="f83ea-126">This example shows how to create a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="f83ea-127">Le nouveau conteneur est privé par défaut, ce qui signifie que vous devez indiquer votre clé d’accès de stockage pour télécharger des objets blob depuis ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="f83ea-127">By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="f83ea-128">Si vous voulez que les fichiers du conteneur soient publics, vous pouvez configurer le conteneur en utilisant le code suivant :</span><span class="sxs-lookup"><span data-stu-id="f83ea-128">If you want to make the files within the container available to everyone, you can set the container to be public using the following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="f83ea-129">Tous les utilisateurs d’Internet peuvent afficher les objets blob d’un conteneur public.</span><span class="sxs-lookup"><span data-stu-id="f83ea-129">Anyone on the Internet can see blobs in a public container.</span></span> <span data-ttu-id="f83ea-130">Toutefois, vous ne pouvez les modifier ou les supprimer que si vous disposez de la clé d’accès du compte ou de la signature d’accès partagé adéquate.</span><span class="sxs-lookup"><span data-stu-id="f83ea-130">However, you can modify or delete them only if you have the appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f83ea-131">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="f83ea-131">Upload a blob into a container</span></span>
<span data-ttu-id="f83ea-132">Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.</span><span class="sxs-lookup"><span data-stu-id="f83ea-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="f83ea-133">En règle générale, il est recommandé d’utiliser le type d’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="f83ea-133">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="f83ea-134">Pour télécharger un fichier vers un objet blob de blocs, obtenez une référence de conteneur et utilisez-la pour obtenir une référence d’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="f83ea-134">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="f83ea-135">Lorsque vous disposez d’une référence d’objet blob, vous pouvez télécharger un flux de données vers cet objet en appelant la méthode **UploadFromStream**.</span><span class="sxs-lookup"><span data-stu-id="f83ea-135">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="f83ea-136">Cette opération crée l’objet blob s’il n’existait pas. S’il existe, il est remplacé.</span><span class="sxs-lookup"><span data-stu-id="f83ea-136">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="f83ea-137">L’exemple suivant illustre le chargement d’un objet blob dans un conteneur en partant du principe que le conteneur existe déjà.</span><span class="sxs-lookup"><span data-stu-id="f83ea-137">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite the "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="f83ea-138">Création d'une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="f83ea-138">List the blobs in a container</span></span>
<span data-ttu-id="f83ea-139">Pour créer une liste d’objets blob dans un conteneur, commencez par obtenir une référence pointant vers un conteneur.</span><span class="sxs-lookup"><span data-stu-id="f83ea-139">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="f83ea-140">Vous pouvez ensuite utiliser la méthode **ListBlobs** du conteneur pour récupérer les objets blob et/ou les répertoires qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="f83ea-140">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="f83ea-141">Pour accéder aux nombreuses propriétés et méthodes d’une **IListBlobItem** renvoyée, vous devez l’appeler vers un objet **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="f83ea-141">To access the  rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="f83ea-142">Si vous ne connaissez pas le type, vous pouvez lancer une vérification de type pour déterminer la cible de l’appel.</span><span class="sxs-lookup"><span data-stu-id="f83ea-142">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="f83ea-143">Le code suivant illustre la récupération et la génération de l’URI de chaque élément du conteneur _photos_ :</span><span class="sxs-lookup"><span data-stu-id="f83ea-143">The following code demonstrates how to retrieve and output the URI of each item in the _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within the container and output the length and URI.
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

<span data-ttu-id="f83ea-144">En incluant les informations de chemin d’accès aux noms des objets blob, vous obtenez alors une structure de répertoires virtuels que vous pouvez organiser et parcourir de la même manière qu’un système de fichiers traditionnel.</span><span class="sxs-lookup"><span data-stu-id="f83ea-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="f83ea-145">La structure de répertoires est uniquement virtuelle : les seules ressources disponibles dans le stockage d’objets blob sont des conteneurs et des objets blob.</span><span class="sxs-lookup"><span data-stu-id="f83ea-145">The directory structure is virtual only--the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="f83ea-146">Toutefois, la bibliothèque cliente de stockage fournit un objet **CloudBlobDirectory** pour faire référence à un répertoire virtuel et simplifier le processus d’utilisation des objets blob organisés de cette façon.</span><span class="sxs-lookup"><span data-stu-id="f83ea-146">However, the storage client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="f83ea-147">Par exemple, prenez l’ensemble d’objets blob de blocs suivant, situé dans un conteneur nommé *photos* :</span><span class="sxs-lookup"><span data-stu-id="f83ea-147">For example, consider the following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="f83ea-148">Quand vous appelez **ListBlobs** pour le conteneur *photos* (comme dans l’extrait de code précédent), une liste hiérarchique est retournée.</span><span class="sxs-lookup"><span data-stu-id="f83ea-148">When you call **ListBlobs** on the *photos* container (as in the preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="f83ea-149">Celle-ci contient à la fois des objets **CloudBlobDirectory** et **CloudBlockBlob** représentant respectivement les répertoires et les objets blob du conteneur.</span><span class="sxs-lookup"><span data-stu-id="f83ea-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing the directories and blobs in the container, respectively.</span></span> <span data-ttu-id="f83ea-150">La sortie obtenue ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="f83ea-150">The resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="f83ea-151">En option, vous pouvez définir le paramètre **UseFlatBlobListing** de la méthode **ListBlobs** sur la valeur **true**.</span><span class="sxs-lookup"><span data-stu-id="f83ea-151">Optionally, you can set the **UseFlatBlobListing** parameter of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="f83ea-152">Dans ce cas, chaque objet blob dans le conteneur est retourné en tant qu’objet **CloudBlockBlob** .</span><span class="sxs-lookup"><span data-stu-id="f83ea-152">In this case, every blob in the container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="f83ea-153">L’appel à **ListBlobs** pour retourner une liste plate ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="f83ea-153">The call to **ListBlobs** to return a flat listing looks like this:</span></span>

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="f83ea-154">Les résultats se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="f83ea-154">and the results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="f83ea-155">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-155">Download blobs</span></span>
<span data-ttu-id="f83ea-156">Pour télécharger des objets blob, commencez par récupérer une référence d’objet blob, puis appelez la méthode **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="f83ea-156">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="f83ea-157">L’exemple suivant utilise la méthode **DownloadToStream** pour transférer les contenus d’objets blob vers un objet de flux pouvant être rendu persistant dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="f83ea-157">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents to a file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="f83ea-158">Vous pouvez également utiliser la méthode **DownloadToStream** pour télécharger les contenus d’un objet blob en tant que chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="f83ea-158">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="f83ea-159">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-159">Delete blobs</span></span>
<span data-ttu-id="f83ea-160">Pour supprimer un objet blob, commencez par obtenir une référence d’objet blob, puis appelez la méthode **Delete** associée.</span><span class="sxs-lookup"><span data-stu-id="f83ea-160">To delete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete the blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="f83ea-161">Création d’une liste d’objets blob dans des pages de manière asynchrone</span><span class="sxs-lookup"><span data-stu-id="f83ea-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="f83ea-162">Si vous répertoriez un grand nombre d’objets blob ou que vous souhaitez contrôler le nombre de résultats renvoyés lors d’une opération de création de liste, vous pouvez répertorier les objets blob dans des pages de résultats.</span><span class="sxs-lookup"><span data-stu-id="f83ea-162">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="f83ea-163">Cet exemple montre comment renvoyer les résultats dans des pages de manière asynchrone afin que l’exécution ne soit pas bloquée lorsqu’un ensemble volumineux de résultats est attendu.</span><span class="sxs-lookup"><span data-stu-id="f83ea-163">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="f83ea-164">Cet exemple montre une liste plate d’objets blob. Vous pouvez également avoir une liste hiérarchique en définissant le paramètre _useFlatBlobListing_ de la méthode **ListBlobsSegmentedAsync** sur _false_.</span><span class="sxs-lookup"><span data-stu-id="f83ea-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the _useFlatBlobListing_ parameter of the **ListBlobsSegmentedAsync** method to _false_.</span></span>

<span data-ttu-id="f83ea-165">Comme l’exemple de méthode appelle une méthode asynchrone, il doit être précédé du mot clé _async_ et doit renvoyer un objet **Task**.</span><span class="sxs-lookup"><span data-stu-id="f83ea-165">Because the sample method calls an asynchronous method, it must be prefaced with the _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="f83ea-166">Le mot clé d’attente spécifié pour la méthode **ListBlobsSegmentedAsync** suspend l’exécution de l’exemple de méthode jusqu’à ce que la tâche de création de liste soit terminée.</span><span class="sxs-lookup"><span data-stu-id="f83ea-166">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs to the console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get the continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="f83ea-167">Écriture dans un objet blob d’ajout</span><span class="sxs-lookup"><span data-stu-id="f83ea-167">Writing to an append blob</span></span>
<span data-ttu-id="f83ea-168">Il est optimisé pour les opérations d’ajout, telles que la journalisation.</span><span class="sxs-lookup"><span data-stu-id="f83ea-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="f83ea-169">Comme un objet blob de blocs, un objet blob d’ajout est composé de blocs. Mais lorsqu’il est ajouté à un objet blob d’ajout, un nouveau bloc l’est toujours à la fin.</span><span class="sxs-lookup"><span data-stu-id="f83ea-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="f83ea-170">Vous ne pouvez pas mettre à jour ou supprimer un bloc dans un objet blob d’ajout.</span><span class="sxs-lookup"><span data-stu-id="f83ea-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="f83ea-171">Les ID de bloc dans un objet blob d’ajout ne sont pas visibles, comme pour un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="f83ea-171">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="f83ea-172">Chaque bloc d’un objet blob d’ajout peut avoir une taille différente (jusqu’à 4 Mo), et un objet blob d’ajout peut contenir au maximum 50 000 blocs.</span><span class="sxs-lookup"><span data-stu-id="f83ea-172">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="f83ea-173">La taille maximale d’un objet blob d’ajout est donc légèrement supérieure à 195 Go (4 Mo x 50 000 blocs).</span><span class="sxs-lookup"><span data-stu-id="f83ea-173">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="f83ea-174">L’exemple ci-dessous crée un objet blob d’ajout et y ajoute des données pour simuler une opération de journalisation simple.</span><span class="sxs-lookup"><span data-stu-id="f83ea-174">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```csharp
//Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create the container if it does not already exist.
container.CreateIfNotExists();

//Get a reference to an append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create the append blob. Note that if the blob already exists, the CreateOrReplace() method will overwrite it.
//You can check whether the blob exists to avoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data to the end of the append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read the append blob to the console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="f83ea-175">Pour plus d’informations sur les différences entre les trois types d’objets blob, consultez la page [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) .</span><span class="sxs-lookup"><span data-stu-id="f83ea-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about the differences between the three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="f83ea-176">Gestion de la sécurité pour les objets blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-176">Managing security for blobs</span></span>
<span data-ttu-id="f83ea-177">Par défaut, Azure Storage préserve la sécurité de vos données en limitant l’accès au propriétaire du compte, qui est en possession des clés d’accès au compte.</span><span class="sxs-lookup"><span data-stu-id="f83ea-177">By default, Azure Storage keeps your data secure by limiting access to the account owner, who is in possession of the account access keys.</span></span> <span data-ttu-id="f83ea-178">Lorsque vous avez besoin de partager des données d’objets blob de votre compte de stockage, il est important de le faire sans compromettre la sécurité de vos clés d’accès au compte.</span><span class="sxs-lookup"><span data-stu-id="f83ea-178">When you need to share blob data in your storage account, it is important to do so without compromising the security of your account access keys.</span></span> <span data-ttu-id="f83ea-179">En outre, vous pouvez chiffrer les données d’objets blob pour vous assurer qu’elles sont sécurisées lors de leur transfert et dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f83ea-179">Additionally, you can encrypt blob data to ensure that it is secure going over the wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a><span data-ttu-id="f83ea-180">Contrôle de l’accès aux données d’objets blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-180">Controlling access to blob data</span></span>
<span data-ttu-id="f83ea-181">Par défaut, les données d’objets blob de votre compte de stockage sont accessibles uniquement par le propriétaire du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f83ea-181">By default, the blob data in your storage account is accessible only to storage account owner.</span></span> <span data-ttu-id="f83ea-182">L’authentification des demandes vis-à-vis du stockage d’objets blob requiert la clé d’accès par défaut.</span><span class="sxs-lookup"><span data-stu-id="f83ea-182">Authenticating requests against Blob storage requires the account access key by default.</span></span> <span data-ttu-id="f83ea-183">Toutefois, vous pouvez rendre certaines données d’objets blob disponibles pour d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f83ea-183">However, you may wish to make certain blob data available to other users.</span></span> <span data-ttu-id="f83ea-184">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="f83ea-184">You have two options:</span></span>

* <span data-ttu-id="f83ea-185">**Accès anonyme :** vous pouvez rendre un conteneur ou ses objets blob disponibles publiquement pour un accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="f83ea-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="f83ea-186">Pour plus d'informations, consultez [Gestion de l'accès en lecture anonyme aux conteneurs et aux objets blob](storage-manage-access-to-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="f83ea-186">See [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="f83ea-187">**Signatures d’accès partagé :** vous pouvez fournir aux clients une signature d’accès partagé (SAP), qui fournit un accès délégué à une ressource de votre compte de stockage, avec des autorisations et sur un intervalle que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="f83ea-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access to a resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="f83ea-188">Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé (SAP)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="f83ea-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="f83ea-189">Chiffrement des données d’objets blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-189">Encrypting blob data</span></span>
<span data-ttu-id="f83ea-190">Azure Storage prend en charge le chiffrement des données d’objets blob côtés client et serveur :</span><span class="sxs-lookup"><span data-stu-id="f83ea-190">Azure Storage supports encrypting blob data both at the client and on the server:</span></span>

* <span data-ttu-id="f83ea-191">**Chiffrement côté client :** la bibliothèque cliente de stockage pour .NET prend en charge le chiffrement des données au sein des applications clientes, avant le chargement vers Azure Storage, et le déchiffrement des données pendant leur téléchargement vers le client.</span><span class="sxs-lookup"><span data-stu-id="f83ea-191">**Client-side encryption:** The Storage Client Library for .NET supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="f83ea-192">La bibliothèque prend également en charge l’intégration à Azure Key Vault pour la gestion des clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f83ea-192">The library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="f83ea-193">Pour plus d’informations, voir [Chiffrement côté client avec .NET pour Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="f83ea-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="f83ea-194">Voir également [Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l’aide d’Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f83ea-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="f83ea-195">**Chiffrement côté serveur**: Azure Storage prend désormais en charge le chiffrement côté serveur.</span><span class="sxs-lookup"><span data-stu-id="f83ea-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="f83ea-196">Voir [Azure Storage Service Encryption pour les données au repos (version préliminaire)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f83ea-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f83ea-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f83ea-197">Next steps</span></span>
<span data-ttu-id="f83ea-198">Maintenant que vous connaissez les bases du stockage d’objets blob, consultez les liens suivants pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="f83ea-198">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="f83ea-199">Explorateur Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f83ea-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="f83ea-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite qui vous permet d’exploiter visuellement les données Azure Storage sur Windows, Max OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="f83ea-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="f83ea-201">Exemples relatifs à Blob Storage</span><span class="sxs-lookup"><span data-stu-id="f83ea-201">Blob storage samples</span></span>
* [<span data-ttu-id="f83ea-202">Prise en main d’Azure Blob Storage dans .NET</span><span class="sxs-lookup"><span data-stu-id="f83ea-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="f83ea-203">Documentation de référence sur le stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="f83ea-203">Blob storage reference</span></span>
* [<span data-ttu-id="f83ea-204">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="f83ea-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="f83ea-205">Référence d’API REST</span><span class="sxs-lookup"><span data-stu-id="f83ea-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="f83ea-206">Guides conceptuels</span><span class="sxs-lookup"><span data-stu-id="f83ea-206">Conceptual guides</span></span>
* [<span data-ttu-id="f83ea-207">Transfert de données avec l’utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="f83ea-207">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="f83ea-208">Prise en main du stockage de fichier pour .NET</span><span class="sxs-lookup"><span data-stu-id="f83ea-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="f83ea-209">Utilisation du stockage d’objets blob Azure avec le Kit de développement logiciel (SDK) WebJobs</span><span class="sxs-lookup"><span data-stu-id="f83ea-209">How to use Azure blob storage with the WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
