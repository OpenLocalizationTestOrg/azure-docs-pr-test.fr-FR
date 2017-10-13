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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Prendre en main Stockage Blob Azure et les services connectés de Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Cet article explique comment prendre en main Stockage Blob Azure dans Visual Studio, après avoir créé ou référencé un compte de stockage Azure dans un projet ASP.NET Core via la boîte de dialogue Ajouter des services connectés de Visual Studio.

Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS. Les objets blob peuvent être de toutes tailles. Il peut s'agir d'images, de fichiers audio ou vidéo, de données brutes ou de fichiers de documents. Cet article explique comment prendre en main Stockage Blob après avoir créé un compte de stockage Azure via la boîte de dialogue **Ajouter des services connectés** de Visual Studio dans un projet ASP.NET Core.

De la même manière que les fichiers résident dans des dossiers, le stockage des objets blob s'effectue dans des conteneurs. Après avoir créé un stockage, créez un ou plusieurs conteneurs dans le stockage. Par exemple, dans un stockage appelé « Scrapbook », vous pouvez créer des conteneurs dans le stockage : un conteneur nommé « images » pour stocker des photos et un autre nommé « audio » pour stocker des fichiers audio. Une fois que vous avez créé les conteneurs, vous pouvez y charger des fichiers blob. Pour plus d’informations sur la manipulation des objets blob par programme, consultez la page [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .

## <a name="access-blob-containers-in-code"></a>Accès aux conteneurs d'objets blob dans le code
Pour accéder aux objets blob de projets ASP.NET Core par programmation, vous devez ajouter les éléments suivants, s’ils ne sont pas déjà présents.

1. Ajoutez les déclarations d’espace de noms suivantes en haut de chaque fichier C# dans lequel vous voulez accéder au stockage Azure par programmation.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Obtenez un objet **CloudStorageAccount** qui représente les informations de votre compte de stockage. Le code suivant permet d'obtenir votre chaîne de connexion de stockage et les informations de compte de stockage à partir de la configuration du service Azure.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **REMARQUE :** placez tout le code ci-dessus avant celui des sections suivantes.
3. Utilisez un objet **CloudBlobClient** pour obtenir une référence **CloudBlobContainer** à un conteneur existant dans votre compte de stockage.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Création d'un conteneur dans le code
Vous pouvez aussi utiliser **CloudBlobClient** pour créer un conteneur dans votre compte de stockage. Pour cela, il suffit d’ajouter un appel à **CreateIfNotExistsAsync** comme dans le code suivant :

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**REMARQUE :** les API qui effectuent des appels au stockage Azure dans ASP.NET Core sont asynchrones. Pour plus d’informations, consultez l’article [Programmation asynchrone avec Async et Await](http://msdn.microsoft.com/library/hh191443.aspx) . Le code ci-dessous suppose que les méthodes de programmation asynchrone sont utilisées.

Pour rendre publics les fichiers présents dans le conteneur, vous pouvez configurer le conteneur en conséquence à l’aide du code suivant :

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
Pour télécharger un fichier blob vers un conteneur, obtenez la référence du conteneur et utilisez-la pour celle de l'objet blob. Dès que vous disposez d’une référence d’objet blob, vous pouvez télécharger un flux de données vers cet objet en appelant la méthode **UploadFromStreamAsync** . Cette opération crée l’objet blob ou le remplace s’il existe. L’exemple suivant illustre le chargement d’un objet blob dans un conteneur en partant du principe que le conteneur existe déjà.

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a>Création d'une liste d'objets blob dans un conteneur
Pour créer une liste d’objets blob dans un conteneur, commencez par obtenir une référence pointant vers un conteneur. Vous pouvez ensuite appeler la méthode **ListBlobsSegmentedAsync** du conteneur pour récupérer les objets blob et/ou les répertoires figurant dans ce conteneur. Pour accéder aux nombreuses propriétés et méthodes d’une **IListBlobItem** renvoyée, vous devez l’appeler vers un objet **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**. Si vous ne savez pas de quel type d’objet blob il s’agit, vous pouvez lancer une vérification de type pour déterminer la cible de l’appel. Le code suivant illustre la récupération et la génération de l'URI de chaque élément d'un conteneur.

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

D'autres méthodes permettent de répertorier le contenu d'un conteneur d'objets blob. Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .

## <a name="download-a-blob"></a>Téléchargement d’un objet blob
Pour télécharger un objet blob, commencez par en obtenir la référence, puis appelez la méthode **DownloadToStreamAsync** . L’exemple ci-après utilise la méthode **DownloadToStreamAsync** pour transférer le contenu des objets blob vers un objet de flux que vous pouvez ensuite enregistrer sous la forme d’un fichier local.

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Il existe plusieurs façons d'enregistrer les objets blob sous forme de fichiers. Pour plus d’informations, consultez la section [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) .

## <a name="delete-a-blob"></a>Supprimer un objet blob
Pour supprimer un objet blob, commencez par en obtenir la référence, puis appelez la méthode **DeleteAsync** .

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

