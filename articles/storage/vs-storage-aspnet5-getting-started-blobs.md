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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Prendre en main Stockage Blob Azure et les services connectés de Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment tooget démarrer à l’aide de stockage d’objets Blob Azure dans Visual Studio après avoir créé ou référencé d’un compte de stockage Azure dans un projet ASP.NET Core par à l’aide de la boîte de dialogue hello Visual Studio ajouter des Services connectés.

Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS. Les objets blob peuvent être de toutes tailles. Il peut s'agir d'images, de fichiers audio ou vidéo, de données brutes ou de fichiers de documents. Cet article décrit comment tooget démarrer avec le stockage d’objets blob après avoir créé un compte de stockage Azure à l’aide de Visual Studio de hello **ajouter des Services connectés** boîte de dialogue dans un projet ASP.NET Core.

De la même manière que les fichiers résident dans des dossiers, le stockage des objets blob s'effectue dans des conteneurs. Après avoir créé un stockage, vous créez un ou plusieurs conteneurs dans le stockage hello. Par exemple, dans un stockage appelé « Album », vous pouvez créer des conteneurs dans le stockage hello appelé images toostore de « images » et une autre appelée « audio » toostore fichiers audio. Après avoir créé les conteneurs hello, vous pouvez télécharger toothem de fichiers blob individuels. Pour plus d’informations sur la manipulation des objets blob par programme, consultez la page [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) .

## <a name="access-blob-containers-in-code"></a>Accès aux conteneurs d'objets blob dans le code
tooprogrammatically d’accéder aux objets BLOB dans les projets ASP.NET Core, vous devez hello tooadd suivant d’éléments, si elles ne sont pas déjà présentes.

1. Ajoutez hello suivant en haut toohello déclarations du code espace de noms de tous les fichiers c# dans lequel vous souhaitez l’accès tooprogrammatically stockage Azure.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage. Utilisez hello suivant code tooget votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure hello.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Remarque :** utilisent les hello ci-dessus code devant les code hello dans les sections suivantes de hello.
3. Utilisez un **CloudBlobClient** objet tooget un **CloudBlobContainer** conteneur existant de référence tooan dans votre compte de stockage.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Création d'un conteneur dans le code
Vous pouvez également utiliser hello **CloudBlobClient** toocreate un conteneur dans votre compte de stockage. Il vous suffit de toodo est tooadd un appel trop**CreateIfNotExistsAsync** comme hello suivant de code :

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Remarque :** hello API qui effectuent des appels tooAzure stockage dans ASP.NET Core sont asynchrones. Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) . code Hello ci-dessous suppose que les méthodes de programmation asynchrones sont utilisées.

fichiers hello toomake tooeveryone de hello conteneur disponible, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
tooupload un fichier blob dans un conteneur, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob. Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **UploadFromStreamAsync** (méthode). Cette opération crée les objets blob de hello si elle y figure pas déjà, ou le remplace s’il existe. Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur. Vous pouvez ensuite appeler du conteneur hello **ListBlobsSegmentedAsync** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient. tooaccess hello ensemble complet des propriétés et méthodes pour retourné **IListBlobItem**, vous devez effectuer un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objet. Si vous ne connaissez pas les blob hello de type, vous pouvez utiliser un toodetermine de vérification de type qui toocast à. Hello suivant de code montre comment tooretrieve et sortie hello URI de chaque élément dans un conteneur.

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

Il existe d’autres contenu de hello toolist manières d’un conteneur d’objets blob. Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .

## <a name="download-a-blob"></a>Téléchargement d’un objet blob
tout d’abord obtenir un objet blob de référence toohello toodownload un objet blob et puis appelez hello **DownloadToStreamAsync** (méthode). exemple Hello utilise hello **DownloadToStreamAsync** méthode tootransfer hello contenu tooa flux de données objet blob que vous pouvez ensuite enregistrer comme un fichier local.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Il existe autres façons toosave BLOB en tant que fichiers. Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) .

## <a name="delete-a-blob"></a>Supprimer un objet blob
tout d’abord obtenir un objet blob de référence toohello toodelete un objet blob et puis appelez hello **DeleteAsync** méthode dessus.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

