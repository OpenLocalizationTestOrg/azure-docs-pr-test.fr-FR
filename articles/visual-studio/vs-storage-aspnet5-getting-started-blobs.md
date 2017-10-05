---
title: "Prendre en main Stockage Blob et les services connectés de Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Comment prendre en main Stockage Blob Azure dans un projet ASP.NET Core Visual Studio après avoir créé un compte de stockage à l’aide des services connectés de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2e8060b44c395ad7c24e7778c0ef65148a3a45de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="d571a-103">Prendre en main Stockage Blob Azure et les services connectés de Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="d571a-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d571a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d571a-104">Overview</span></span>
<span data-ttu-id="d571a-105">Cet article explique comment prendre en main Stockage Blob Azure dans Visual Studio, après avoir créé ou référencé un compte de stockage Azure dans un projet ASP.NET Core via la boîte de dialogue Ajouter des services connectés de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d571a-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="d571a-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d571a-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="d571a-107">Les objets blob peuvent être de toutes tailles.</span><span class="sxs-lookup"><span data-stu-id="d571a-107">A single blob can be any size.</span></span> <span data-ttu-id="d571a-108">Il peut s'agir d'images, de fichiers audio ou vidéo, de données brutes ou de fichiers de documents.</span><span class="sxs-lookup"><span data-stu-id="d571a-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="d571a-109">Cet article explique comment prendre en main Stockage Blob après avoir créé un compte de stockage Azure via la boîte de dialogue **Ajouter des services connectés** de Visual Studio dans un projet ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d571a-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="d571a-110">De la même manière que les fichiers résident dans des dossiers, le stockage des objets blob s'effectue dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="d571a-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="d571a-111">Après avoir créé un stockage, créez un ou plusieurs conteneurs dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="d571a-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="d571a-112">Par exemple, dans un stockage appelé « Scrapbook », vous pouvez créer des conteneurs dans le stockage : un conteneur nommé « images » pour stocker des photos et un autre nommé « audio » pour stocker des fichiers audio.</span><span class="sxs-lookup"><span data-stu-id="d571a-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="d571a-113">Une fois que vous avez créé les conteneurs, vous pouvez y charger des fichiers blob.</span><span class="sxs-lookup"><span data-stu-id="d571a-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="d571a-114">Pour plus d’informations sur la manipulation des objets blob par programme, consultez la page [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="d571a-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="d571a-115">Accès aux conteneurs d'objets blob dans le code</span><span class="sxs-lookup"><span data-stu-id="d571a-115">Access blob containers in code</span></span>
<span data-ttu-id="d571a-116">Pour accéder aux objets blob de projets ASP.NET Core par programmation, vous devez ajouter les éléments suivants, s’ils ne sont pas déjà présents.</span><span class="sxs-lookup"><span data-stu-id="d571a-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="d571a-117">Ajoutez les déclarations d’espace de noms suivantes en haut de chaque fichier C# dans lequel vous voulez accéder au stockage Azure par programmation.</span><span class="sxs-lookup"><span data-stu-id="d571a-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="d571a-118">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d571a-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d571a-119">Le code suivant permet d'obtenir votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure.</span><span class="sxs-lookup"><span data-stu-id="d571a-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="d571a-120">**REMARQUE :** placez tout le code ci-dessus avant celui des sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="d571a-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="d571a-121">Utilisez un objet **CloudBlobClient** pour obtenir une référence **CloudBlobContainer** à un conteneur existant dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d571a-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="d571a-122">Création d'un conteneur dans le code</span><span class="sxs-lookup"><span data-stu-id="d571a-122">Create a container in code</span></span>
<span data-ttu-id="d571a-123">Vous pouvez aussi utiliser **CloudBlobClient** pour créer un conteneur dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d571a-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="d571a-124">Pour cela, il suffit d’ajouter un appel à **CreateIfNotExistsAsync** comme dans le code suivant :</span><span class="sxs-lookup"><span data-stu-id="d571a-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="d571a-125">**REMARQUE :** les API qui effectuent des appels au stockage Azure dans ASP.NET Core sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="d571a-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="d571a-126">Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d571a-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d571a-127">Le code ci-dessous suppose que les méthodes de programmation asynchrone sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="d571a-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="d571a-128">Pour rendre publics les fichiers présents dans le conteneur, vous pouvez configurer le conteneur en conséquence à l’aide du code suivant :</span><span class="sxs-lookup"><span data-stu-id="d571a-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d571a-129">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="d571a-129">Upload a blob into a container</span></span>
<span data-ttu-id="d571a-130">Pour télécharger un fichier blob vers un conteneur, obtenez la référence du conteneur et utilisez-la pour celle de l'objet blob.</span><span class="sxs-lookup"><span data-stu-id="d571a-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="d571a-131">Dès que vous disposez d’une référence d’objet blob, vous pouvez télécharger un flux de données vers cet objet en appelant la méthode **UploadFromStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="d571a-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="d571a-132">Cette opération crée l’objet blob ou le remplace s’il existe.</span><span class="sxs-lookup"><span data-stu-id="d571a-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="d571a-133">L’exemple suivant illustre le chargement d’un objet blob dans un conteneur en partant du principe que le conteneur existe déjà.</span><span class="sxs-lookup"><span data-stu-id="d571a-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d571a-134">Création d'une liste d'objets blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="d571a-134">List the blobs in a container</span></span>
<span data-ttu-id="d571a-135">Pour créer une liste d’objets blob dans un conteneur, commencez par obtenir une référence pointant vers un conteneur.</span><span class="sxs-lookup"><span data-stu-id="d571a-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="d571a-136">Vous pouvez ensuite appeler la méthode **ListBlobsSegmentedAsync** du conteneur pour récupérer les objets blob et/ou les répertoires figurant dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="d571a-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="d571a-137">Pour accéder aux nombreuses propriétés et méthodes d’une **IListBlobItem** renvoyée, vous devez l’appeler vers un objet **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="d571a-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="d571a-138">Si vous ne savez pas de quel type d’objet blob il s’agit, vous pouvez lancer une vérification de type pour déterminer la cible de l’appel.</span><span class="sxs-lookup"><span data-stu-id="d571a-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="d571a-139">Le code suivant illustre la récupération et la génération de l'URI de chaque élément d'un conteneur.</span><span class="sxs-lookup"><span data-stu-id="d571a-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="d571a-140">D'autres méthodes permettent de répertorier le contenu d'un conteneur d'objets blob.</span><span class="sxs-lookup"><span data-stu-id="d571a-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="d571a-141">Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .</span><span class="sxs-lookup"><span data-stu-id="d571a-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="d571a-142">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="d571a-142">Download a blob</span></span>
<span data-ttu-id="d571a-143">Pour télécharger un objet blob, commencez par en obtenir la référence, puis appelez la méthode **DownloadToStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="d571a-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="d571a-144">L’exemple ci-après utilise la méthode **DownloadToStreamAsync** pour transférer le contenu des objets blob vers un objet de flux que vous pouvez ensuite enregistrer sous la forme d’un fichier local.</span><span class="sxs-lookup"><span data-stu-id="d571a-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="d571a-145">Il existe plusieurs façons d'enregistrer les objets blob sous forme de fichiers.</span><span class="sxs-lookup"><span data-stu-id="d571a-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="d571a-146">Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) .</span><span class="sxs-lookup"><span data-stu-id="d571a-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="d571a-147">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="d571a-147">Delete a blob</span></span>
<span data-ttu-id="d571a-148">Pour supprimer un objet blob, commencez par en obtenir la référence, puis appelez la méthode **DeleteAsync** .</span><span class="sxs-lookup"><span data-stu-id="d571a-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="d571a-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d571a-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

