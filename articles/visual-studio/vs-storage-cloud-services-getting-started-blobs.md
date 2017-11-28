---
title: "aaaGet a démarré avec le stockage d’objets blob et de Visual Studio services connectés (services de cloud computing) | Documents Microsoft"
description: "Comment tooget démarrer à l’aide de stockage d’objets Blob Azure dans un projet de service cloud dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="26386-103">Prendre en main le stockage d’objets blob Azure et les services connectés de Visual Studio (projets services cloud)</span><span class="sxs-lookup"><span data-stu-id="26386-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="26386-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="26386-104">Overview</span></span>
<span data-ttu-id="26386-105">Cet article décrit comment tooget démarrer avec le stockage d’objets Blob Azure après avoir créé ou référencé d’un compte Azure Storage à l’aide de Visual Studio de hello **ajouter des Services connectés** projet de services de boîte de dialogue dans un cloud de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26386-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="26386-106">Nous allons vous montrer comment tooaccess et créer des conteneurs d’objets blob, et comment tooperform des tâches courantes que le chargement, la liste et le téléchargement d’objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="26386-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="26386-107">exemples de Hello sont écrits en C\# et utiliser hello [bibliothèque cliente Microsoft Azure Storage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="26386-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="26386-108">Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="26386-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="26386-109">Les objets blob peuvent être de toutes tailles.</span><span class="sxs-lookup"><span data-stu-id="26386-109">A single blob can be any size.</span></span> <span data-ttu-id="26386-110">Il peut s'agir d'images, de fichiers audio ou vidéo, de données brutes ou de fichiers de documents.</span><span class="sxs-lookup"><span data-stu-id="26386-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="26386-111">De la même manière que les fichiers résident dans des dossiers, le stockage des objets blob s'effectue dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="26386-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="26386-112">Après avoir créé un stockage, vous créez un ou plusieurs conteneurs dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="26386-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="26386-113">Par exemple, dans un stockage appelé « Album », vous pouvez créer des conteneurs dans le stockage hello appelé images toostore de « images » et une autre appelée « audio » toostore fichiers audio.</span><span class="sxs-lookup"><span data-stu-id="26386-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="26386-114">Après avoir créé les conteneurs hello, vous pouvez télécharger toothem de fichiers blob individuels.</span><span class="sxs-lookup"><span data-stu-id="26386-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="26386-115">Pour plus d’informations sur la manipulation des objets blob par programme, consultez la page [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="26386-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="26386-116">Pour obtenir des informations générales sur Azure Storage, consultez [Documentation du stockage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="26386-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="26386-117">Pour obtenir des informations générales sur Azure Cloud Services, consultez la [Documentation Azure Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="26386-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="26386-118">Pour plus d’informations sur la programmation d’applications ASP.NET, consultez [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="26386-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="26386-119">Accès aux conteneurs d'objets blob dans le code</span><span class="sxs-lookup"><span data-stu-id="26386-119">Access blob containers in code</span></span>
<span data-ttu-id="26386-120">tooprogrammatically d’accéder aux objets BLOB dans les projets de service cloud, vous devez hello tooadd suivant d’éléments, si elles ne sont pas déjà présentes.</span><span class="sxs-lookup"><span data-stu-id="26386-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="26386-121">Ajoutez hello suivant en haut toohello déclarations du code espace de noms de tous les fichiers c# dans lesquels vous souhaitez tooprogrammatically accès Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="26386-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="26386-122">Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="26386-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="26386-123">Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.</span><span class="sxs-lookup"><span data-stu-id="26386-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="26386-124">Obtenir un **CloudBlobClient** tooreference un conteneur existant dans votre compte de stockage de l’objet.</span><span class="sxs-lookup"><span data-stu-id="26386-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="26386-125">Obtenir un **CloudBlobContainer** tooreference un conteneur d’objets blob spécifique de l’objet.</span><span class="sxs-lookup"><span data-stu-id="26386-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="26386-126">Utilisez tout code hello indiqué dans la procédure précédente de hello devant code hello indiqué dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="26386-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="26386-127">Création d'un conteneur dans le code</span><span class="sxs-lookup"><span data-stu-id="26386-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="26386-128">Certaines API qui effectuent des appels de tooAzure stockage dans ASP.NET est asynchrones.</span><span class="sxs-lookup"><span data-stu-id="26386-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="26386-129">Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="26386-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="26386-130">code Hello Bonjour l’exemple suivant suppose que vous utilisez des méthodes de programmation asynchrone.</span><span class="sxs-lookup"><span data-stu-id="26386-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="26386-131">toocreate un conteneur dans votre compte de stockage, vous devez toodo est d’ajouter un appel trop**CreateIfNotExistsAsync** comme hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="26386-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="26386-132">fichiers hello toomake tooeveryone de hello conteneur disponible, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="26386-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="26386-133">Toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public, mais vous pouvez modifier ou les supprimer que si vous disposez de la clé d’accès appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="26386-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="26386-134">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="26386-134">Upload a blob into a container</span></span>
<span data-ttu-id="26386-135">Azure Storage prend en charge les objets blob de blocs et de pages.</span><span class="sxs-lookup"><span data-stu-id="26386-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="26386-136">Dans la majorité de hello des cas, objet blob de blocs est hello recommandé toouse de type.</span><span class="sxs-lookup"><span data-stu-id="26386-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="26386-137">tooupload fichier tooa objet blob de blocs, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob de bloc.</span><span class="sxs-lookup"><span data-stu-id="26386-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="26386-138">Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **UploadFromStream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="26386-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="26386-139">Cette opération crée l’objet blob de hello si elle n’existe pas déjà, ou le remplace s’il existe.</span><span class="sxs-lookup"><span data-stu-id="26386-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="26386-140">Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="26386-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="26386-141">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="26386-141">List hello blobs in a container</span></span>
<span data-ttu-id="26386-142">objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur.</span><span class="sxs-lookup"><span data-stu-id="26386-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="26386-143">Vous pouvez ensuite utiliser du conteneur hello **ListBlobs** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="26386-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="26386-144">tooaccess hello ensemble complet des propriétés et méthodes pour retourné **IListBlobItem**, vous devez effectuer un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objet.</span><span class="sxs-lookup"><span data-stu-id="26386-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="26386-145">Si le type de hello est inconnu, vous pouvez utiliser un toodetermine de vérification de type qui toocast à.</span><span class="sxs-lookup"><span data-stu-id="26386-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="26386-146">Hello de code suivant montre comment tooretrieve et sortie hello URI de chaque élément Bonjour **photos** conteneur :</span><span class="sxs-lookup"><span data-stu-id="26386-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="26386-147">Comme indiqué dans l’exemple de code précédent hello, service d’objets blob hello a concept hello de répertoires dans des conteneurs, également.</span><span class="sxs-lookup"><span data-stu-id="26386-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="26386-148">Vous pouvez donc organiser vos objets blob selon une structure proche de celle des dossiers.</span><span class="sxs-lookup"><span data-stu-id="26386-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="26386-149">Par exemple, considérez hello ensemble suivant d’objets BLOB de blocs dans un conteneur nommé **photos**:</span><span class="sxs-lookup"><span data-stu-id="26386-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="26386-150">Lorsque vous appelez **ListBlobs** sur conteneur hello (comme dans l’exemple précédent de hello), collection hello retournée contient **CloudBlobDirectory** et **CloudBlockBlob** objets représentant les répertoires hello et les objets BLOB contenus au niveau supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="26386-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="26386-151">Voici le résultat de hello :</span><span class="sxs-lookup"><span data-stu-id="26386-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="26386-152">Si vous le souhaitez, vous pouvez définir hello **UseFlatBlobListing** paramètre de Hello **ListBlobs** méthode **true**.</span><span class="sxs-lookup"><span data-stu-id="26386-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="26386-153">Cette opération se traduit par le renvoi de chaque objet blob en tant que **CloudBlockBlob**, indépendamment du répertoire.</span><span class="sxs-lookup"><span data-stu-id="26386-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="26386-154">Voici les appels hello trop**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="26386-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="26386-155">et Voici hello résultats :</span><span class="sxs-lookup"><span data-stu-id="26386-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="26386-156">Pour plus d’informations, consultez [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="26386-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="26386-157">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="26386-157">Download blobs</span></span>
<span data-ttu-id="26386-158">objets BLOB toodownload, tout d’abord extraire une référence d’objet blob et ensuite appeler hello **méthodes DownloadToStream** (méthode).</span><span class="sxs-lookup"><span data-stu-id="26386-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="26386-159">exemple Hello utilise hello **méthodes DownloadToStream** méthode tootransfer hello contenu tooa flux de données objet blob que peuvent alors être conservées tooa des fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="26386-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="26386-160">Vous pouvez également utiliser hello **méthodes DownloadToStream** contenu de hello toodownload de méthode d’un objet blob comme une chaîne de texte.</span><span class="sxs-lookup"><span data-stu-id="26386-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="26386-161">Suppression d’objets blob</span><span class="sxs-lookup"><span data-stu-id="26386-161">Delete blobs</span></span>
<span data-ttu-id="26386-162">toodelete un objet blob, commencez par obtenir une référence d’objet blob, puis appelez le **supprimer** (méthode).</span><span class="sxs-lookup"><span data-stu-id="26386-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="26386-163">Création d’une liste d’objets blob dans des pages de manière asynchrone</span><span class="sxs-lookup"><span data-stu-id="26386-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="26386-164">Si vous répertoriez un grand nombre d’objets BLOB, ou nombre de hello toocontrol de vous renvoyer dans une opération de liste de résultats, vous pouvez répertorier les objets BLOB dans les pages de résultats.</span><span class="sxs-lookup"><span data-stu-id="26386-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="26386-165">Cet exemple montre comment tooreturn produit des pages de façon asynchrone, afin que l’exécution n’est pas bloquée lors de l’attente tooreturn un grand ensemble de résultats.</span><span class="sxs-lookup"><span data-stu-id="26386-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="26386-166">Cet exemple montre un liste plate d’objets blob, mais vous pouvez également effectuer une liste hiérarchique, en définissant un hello **useFlatBlobListing** paramètre Hello **ListBlobsSegmentedAsync** méthode trop **false**.</span><span class="sxs-lookup"><span data-stu-id="26386-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="26386-167">Étant donné que la méthode d’échantillonnage hello appelle une méthode asynchrone, il doit commencer par hello **async** (mot clé) et doit retourner un **tâche** objet.</span><span class="sxs-lookup"><span data-stu-id="26386-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="26386-168">Hello await mot clé spécifié pour hello **ListBlobsSegmentedAsync** méthode suspend l’exécution de méthode d’échantillonnage hello jusqu'à la fin de tâche de liste hello.</span><span class="sxs-lookup"><span data-stu-id="26386-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="26386-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26386-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

