---
title: "aaaGet a démarré avec le stockage d’objets blob et de Visual Studio services connectés (services de cloud computing) | Documents Microsoft"
description: "Comment tooget démarrer à l’aide de stockage d’objets Blob Azure dans un projet de service cloud dans Visual Studio une fois la connexion de compte de stockage tooa à l’aide de Visual Studio services connectés"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Prendre en main le stockage d’objets blob Azure et les services connectés de Visual Studio (projets services cloud)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment tooget démarrer avec le stockage d’objets Blob Azure après avoir créé ou référencé d’un compte Azure Storage à l’aide de Visual Studio de hello **ajouter des Services connectés** projet de services de boîte de dialogue dans un cloud de Visual Studio. Nous allons vous montrer comment tooaccess et créer des conteneurs d’objets blob, et comment tooperform des tâches courantes que le chargement, la liste et le téléchargement d’objets BLOB. exemples de Hello sont écrits en C\# et utiliser hello [bibliothèque cliente Microsoft Azure Storage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS. Les objets blob peuvent être de toutes tailles. Il peut s'agir d'images, de fichiers audio ou vidéo, de données brutes ou de fichiers de documents.

De la même manière que les fichiers résident dans des dossiers, le stockage des objets blob s'effectue dans des conteneurs. Après avoir créé un stockage, vous créez un ou plusieurs conteneurs dans le stockage hello. Par exemple, dans un stockage appelé « Album », vous pouvez créer des conteneurs dans le stockage hello appelé images toostore de « images » et une autre appelée « audio » toostore fichiers audio. Après avoir créé les conteneurs hello, vous pouvez télécharger toothem de fichiers blob individuels.

* Pour plus d’informations sur la manipulation des objets blob par programme, consultez la page [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md).
* Pour obtenir des informations générales sur Azure Storage, consultez [Documentation du stockage](https://azure.microsoft.com/documentation/services/storage/).
* Pour obtenir des informations générales sur Azure Cloud Services, consultez la [Documentation Azure Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/).
* Pour plus d’informations sur la programmation d’applications ASP.NET, consultez [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Accès aux conteneurs d'objets blob dans le code
tooprogrammatically d’accéder aux objets BLOB dans les projets de service cloud, vous devez hello tooadd suivant d’éléments, si elles ne sont pas déjà présentes.

1. Ajoutez hello suivant en haut toohello déclarations du code espace de noms de tous les fichiers c# dans lesquels vous souhaitez tooprogrammatically accès Azure Storage.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage. Hello utilisation suivant tooget de code hello votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Obtenir un **CloudBlobClient** tooreference un conteneur existant dans votre compte de stockage de l’objet.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Obtenir un **CloudBlobContainer** tooreference un conteneur d’objets blob spécifique de l’objet.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Utilisez tout code hello indiqué dans la procédure précédente de hello devant code hello indiqué dans les sections suivantes de hello.
> 
> 

## <a name="create-a-container-in-code"></a>Création d'un conteneur dans le code
> [!NOTE]
> Certaines API qui effectuent des appels de tooAzure stockage dans ASP.NET est asynchrones. Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) . code Hello Bonjour l’exemple suivant suppose que vous utilisez des méthodes de programmation asynchrone.
> 
> 

toocreate un conteneur dans votre compte de stockage, vous devez toodo est d’ajouter un appel trop**CreateIfNotExistsAsync** comme hello suivant de code :

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


fichiers hello toomake tooeveryone de hello conteneur disponible, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public, mais vous pouvez modifier ou les supprimer que si vous disposez de la clé d’accès appropriées hello.

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
Azure Storage prend en charge les objets blob de blocs et de pages. Dans la majorité de hello des cas, objet blob de blocs est hello recommandé toouse de type.

tooupload fichier tooa objet blob de blocs, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob de bloc. Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **UploadFromStream** (méthode). Cette opération crée l’objet blob de hello si elle n’existe pas déjà, ou le remplace s’il existe. Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur. Vous pouvez ensuite utiliser du conteneur hello **ListBlobs** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient. tooaccess hello ensemble complet des propriétés et méthodes pour retourné **IListBlobItem**, vous devez effectuer un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objet. Si le type de hello est inconnu, vous pouvez utiliser un toodetermine de vérification de type qui toocast à. Hello de code suivant montre comment tooretrieve et sortie hello URI de chaque élément Bonjour **photos** conteneur :

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

Comme indiqué dans l’exemple de code précédent hello, service d’objets blob hello a concept hello de répertoires dans des conteneurs, également. Vous pouvez donc organiser vos objets blob selon une structure proche de celle des dossiers. Par exemple, considérez hello ensemble suivant d’objets BLOB de blocs dans un conteneur nommé **photos**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Lorsque vous appelez **ListBlobs** sur conteneur hello (comme dans l’exemple précédent de hello), collection hello retournée contient **CloudBlobDirectory** et **CloudBlockBlob** objets représentant les répertoires hello et les objets BLOB contenus au niveau supérieur de hello. Voici le résultat de hello :

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Si vous le souhaitez, vous pouvez définir hello **UseFlatBlobListing** paramètre de Hello **ListBlobs** méthode **true**. Cette opération se traduit par le renvoi de chaque objet blob en tant que **CloudBlockBlob**, indépendamment du répertoire. Voici les appels hello trop**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

et Voici hello résultats :

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Pour plus d’informations, consultez [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Télécharger des objets blob
objets BLOB toodownload, tout d’abord extraire une référence d’objet blob et ensuite appeler hello **méthodes DownloadToStream** (méthode). exemple Hello utilise hello **méthodes DownloadToStream** méthode tootransfer hello contenu tooa flux de données objet blob que peuvent alors être conservées tooa des fichiers locaux.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Vous pouvez également utiliser hello **méthodes DownloadToStream** contenu de hello toodownload de méthode d’un objet blob comme une chaîne de texte.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Suppression d’objets blob
toodelete un objet blob, commencez par obtenir une référence d’objet blob, puis appelez le **supprimer** (méthode).

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Création d’une liste d’objets blob dans des pages de manière asynchrone
Si vous répertoriez un grand nombre d’objets BLOB, ou nombre de hello toocontrol de vous renvoyer dans une opération de liste de résultats, vous pouvez répertorier les objets BLOB dans les pages de résultats. Cet exemple montre comment tooreturn produit des pages de façon asynchrone, afin que l’exécution n’est pas bloquée lors de l’attente tooreturn un grand ensemble de résultats.

Cet exemple montre un liste plate d’objets blob, mais vous pouvez également effectuer une liste hiérarchique, en définissant un hello **useFlatBlobListing** paramètre Hello **ListBlobsSegmentedAsync** méthode trop **false**.

Étant donné que la méthode d’échantillonnage hello appelle une méthode asynchrone, il doit commencer par hello **async** (mot clé) et doit retourner un **tâche** objet. Hello await mot clé spécifié pour hello **ListBlobsSegmentedAsync** méthode suspend l’exécution de méthode d’échantillonnage hello jusqu'à la fin de tâche de liste hello.

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

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

