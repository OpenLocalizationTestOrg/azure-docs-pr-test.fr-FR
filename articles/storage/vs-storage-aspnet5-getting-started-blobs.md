---
title: "aaaGet a démarré avec le stockage d’objets blob et de Visual Studio services connectés (ASP.NET Core) | Documents Microsoft"
description: "Comment tooget démarrer l’utilisation du stockage d’objets Blob Azure dans un projet Visual Studio ASP.NET Core après avoir créé un compte de stockage à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="de3c0-103">Prendre en main Stockage Blob Azure et les services connectés de Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="de3c0-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="de3c0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="de3c0-104">Overview</span></span>
<span data-ttu-id="de3c0-105">Cet article décrit comment tooget démarrer à l’aide de stockage d’objets Blob Azure dans Visual Studio après avoir créé ou référencé d’un compte de stockage Azure dans un projet ASP.NET Core par à l’aide de la boîte de dialogue hello Visual Studio ajouter des Services connectés.</span><span class="sxs-lookup"><span data-stu-id="de3c0-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="de3c0-106">Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="de3c0-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="de3c0-107">Les objets blob peuvent être de toutes tailles.</span><span class="sxs-lookup"><span data-stu-id="de3c0-107">A single blob can be any size.</span></span> <span data-ttu-id="de3c0-108">Il peut s'agir d'images, de fichiers audio ou vidéo, de données brutes ou de fichiers de documents.</span><span class="sxs-lookup"><span data-stu-id="de3c0-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="de3c0-109">Cet article décrit comment tooget démarrer avec le stockage d’objets blob après avoir créé un compte de stockage Azure à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue dans un projet ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="de3c0-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="de3c0-110">De la même manière que les fichiers résident dans des dossiers, le stockage des objets blob s'effectue dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="de3c0-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="de3c0-111">Après avoir créé un stockage, vous créez un ou plusieurs conteneurs dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="de3c0-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="de3c0-112">Par exemple, dans un stockage appelé « Album », vous pouvez créer des conteneurs dans le stockage hello appelé images toostore de « images » et une autre appelée « audio » toostore fichiers audio.</span><span class="sxs-lookup"><span data-stu-id="de3c0-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="de3c0-113">Après avoir créé les conteneurs hello, vous pouvez télécharger toothem de fichiers blob individuels.</span><span class="sxs-lookup"><span data-stu-id="de3c0-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="de3c0-114">Pour plus d’informations sur la manipulation des objets blob par programme, consultez la page [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="de3c0-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="de3c0-115">Accès aux conteneurs d'objets blob dans le code</span><span class="sxs-lookup"><span data-stu-id="de3c0-115">Access blob containers in code</span></span>
<span data-ttu-id="de3c0-116">tooprogrammatically d’accéder aux objets BLOB dans les projets ASP.NET Core, vous devez hello tooadd suivant d’éléments, si elles ne sont pas déjà présentes.</span><span class="sxs-lookup"><span data-stu-id="de3c0-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="de3c0-117">Ajoutez hello suivant en haut toohello déclarations du code espace de noms de tous les fichiers c# dans lequel vous souhaitez l’accès tooprogrammatically stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="de3c0-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="de3c0-118">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="de3c0-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="de3c0-119">Utilisez hello suivant code tooget votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="de3c0-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="de3c0-120">**Remarque :** utilisent les hello ci-dessus code devant les code hello dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="de3c0-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="de3c0-121">Utilisez un **CloudBlobClient** objet tooget un **CloudBlobContainer** conteneur existant de référence tooan dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="de3c0-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="de3c0-122">Création d'un conteneur dans le code</span><span class="sxs-lookup"><span data-stu-id="de3c0-122">Create a container in code</span></span>
<span data-ttu-id="de3c0-123">Vous pouvez également utiliser hello **CloudBlobClient** toocreate un conteneur dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="de3c0-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="de3c0-124">Il vous suffit de toodo est tooadd un appel trop**CreateIfNotExistsAsync** comme hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="de3c0-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="de3c0-125">**Remarque :** hello API qui effectuent des appels tooAzure stockage dans ASP.NET Core sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="de3c0-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="de3c0-126">Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="de3c0-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="de3c0-127">code Hello ci-dessous suppose que les méthodes de programmation asynchrones sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="de3c0-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="de3c0-128">fichiers hello toomake tooeveryone de hello conteneur disponible, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="de3c0-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="de3c0-129">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="de3c0-129">Upload a blob into a container</span></span>
<span data-ttu-id="de3c0-130">tooupload un fichier blob dans un conteneur, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="de3c0-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="de3c0-131">Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **UploadFromStreamAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="de3c0-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="de3c0-132">Cette opération crée les objets blob de hello si elle y figure pas déjà, ou le remplace s’il existe.</span><span class="sxs-lookup"><span data-stu-id="de3c0-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="de3c0-133">Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="de3c0-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="de3c0-134">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="de3c0-134">List hello blobs in a container</span></span>
<span data-ttu-id="de3c0-135">objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur.</span><span class="sxs-lookup"><span data-stu-id="de3c0-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="de3c0-136">Vous pouvez ensuite appeler du conteneur hello **ListBlobsSegmentedAsync** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="de3c0-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="de3c0-137">tooaccess hello ensemble complet des propriétés et méthodes pour retourné **IListBlobItem**, vous devez effectuer un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objet.</span><span class="sxs-lookup"><span data-stu-id="de3c0-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="de3c0-138">Si vous ne connaissez pas les blob hello de type, vous pouvez utiliser un toodetermine de vérification de type qui toocast à.</span><span class="sxs-lookup"><span data-stu-id="de3c0-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="de3c0-139">Hello suivant de code montre comment tooretrieve et sortie hello URI de chaque élément dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="de3c0-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="de3c0-140">Il existe d’autres contenu de hello toolist manières d’un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="de3c0-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="de3c0-141">Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .</span><span class="sxs-lookup"><span data-stu-id="de3c0-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="de3c0-142">Téléchargement d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="de3c0-142">Download a blob</span></span>
<span data-ttu-id="de3c0-143">tout d’abord obtenir un objet blob de référence toohello toodownload un objet blob et puis appelez hello **DownloadToStreamAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="de3c0-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="de3c0-144">exemple Hello utilise hello **DownloadToStreamAsync** méthode tootransfer hello contenu tooa flux de données objet blob que vous pouvez ensuite enregistrer comme un fichier local.</span><span class="sxs-lookup"><span data-stu-id="de3c0-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="de3c0-145">Il existe autres façons toosave BLOB en tant que fichiers.</span><span class="sxs-lookup"><span data-stu-id="de3c0-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="de3c0-146">Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) .</span><span class="sxs-lookup"><span data-stu-id="de3c0-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="de3c0-147">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="de3c0-147">Delete a blob</span></span>
<span data-ttu-id="de3c0-148">tout d’abord obtenir un objet blob de référence toohello toodelete un objet blob et puis appelez hello **DeleteAsync** méthode dessus.</span><span class="sxs-lookup"><span data-stu-id="de3c0-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="de3c0-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de3c0-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

