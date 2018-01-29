---
title: "Télécharger de grandes quantités de données aléatoires depuis le stockage Azure | Microsoft Docs"
description: "Découvrez comment utiliser le Kit de développement logiciel (SDK) Azure pour télécharger de grandes quantités de données aléatoires à partir d’un compte de stockage Azure"
services: storage
documentationcenter: 
author: georgewallace
manager: jeconnoc
editor: 
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 12/12/2017
ms.author: gwallace
ms.custom: mvc
ms.openlocfilehash: 3842860acb1c0fdd9e07f6d2f678ac5d5304003b
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2018
---
# <a name="download-large-amounts-of-random-data-from-azure-storage"></a>Télécharger de grandes quantités de données aléatoires depuis le stockage Azure

Ce didacticiel est le troisième de la série. Ce didacticiel vous montre comment télécharger de grandes quantités de données à partir du stockage Azure.

Dans ce troisième volet, vous apprenez à :

> [!div class="checklist"]
> * Mettre à jour l’application
> * Exécution de l'application
> * Valider le nombre de connexions

## <a name="prerequisites"></a>Conditions préalables

Pour suivre ce didacticiel, vous devez avoir terminé le didacticiel précédent relatif au stockage : [Charger de grandes quantités de données aléatoires parallèlement au stockage Azure][previous-tutorial].

## <a name="remote-into-your-virtual-machine"></a>Ouvrir une session Bureau à distance sur votre machine virtuelle

 Pour créer une session Bureau à distance avec la machine virtuelle, utilisez la commande suivante sur la machine locale. Remplacez l’adresse IP par l’adresse publicIPAddress de votre machine virtuelle. À l'invite, saisissez les informations d’identification que vous avez utilisées lors de la création de la machine virtuelle.

```
mstsc /v:<publicIpAddress>
```

## <a name="update-the-application"></a>Mettre à jour l’application

Dans le didacticiel précédent, vous aviez seulement téléchargé des fichiers dans le compte de stockage. Ouvrez `D:\git\storage-dotnet-perf-scale-app\Program.cs` dans un éditeur de texte. Remplacez la méthode `Main` par le code suivant. Cette exemple supprime les commentaires de la tâche de chargement, de la tâche de téléchargement et de la tâche de suppression de contenus dans le compte de stockage lorsque vous avez terminé.

```csharp
public static void Main(string[] args)
{
    Console.WriteLine("Azure Blob storage performance and scalability sample");
    // Set threading and default connection limit to 100 to ensure multiple threads and connections can be opened.
    // This is in addition to parallelism with the storage client library that is defined in the functions below.
    ThreadPool.SetMinThreads(100, 4);
    ServicePointManager.DefaultConnectionLimit = 100; // (Or More)

    bool exception = false;
    try
    {
        // Call the UploadFilesAsync function.
        UploadFilesAsync().GetAwaiter().GetResult();

        // Uncomment the following line to enable downloading of files from the storage account.  This is commented out
        // initially to support the tutorial at https://docs.microsoft.com/azure/storage/blobs/storage-blob-scaleable-app-download-files.
        // DownloadFilesAsync().GetAwaiter().GetResult();
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
        exception = true;
    }
    finally
    {
        // The following function will delete the container and all files contained in them.  This is commented out initialy
        // As the tutorial at https://docs.microsoft.com/azure/storage/blobs/storage-blob-scaleable-app-download-files has you upload only for one tutorial and download for the other. 
        if (!exception)
        {
            // DeleteExistingContainersAsync().GetAwaiter().GetResult();
        }
        Console.WriteLine("Press any key to exit the application");
        Console.ReadKey();
    }
}
```

Une fois l’application mise à jour, vous devez regénérer l’application. Ouvrir une `Command Prompt` et accédez à `D:\git\storage-dotnet-perf-scale-app`. Regénérez l’application en exécutant `dotnet build` comme indiqué dans l’exemple suivant :

```
dotnet build
```

## <a name="run-the-application"></a>Exécution de l'application

Une fois l’application regénérée, il est temps d’exécuter l’application avec le code mis à jour. Si ce n’est déjà fait, ouvrez une `Command Prompt` et accédez à `D:\git\storage-dotnet-perf-scale-app`.

Saisissez `dotnet run` pour exécuter l’application.

```
dotnet run
```

L’application lit les conteneurs situés dans le compte de stockage spécifié dans **storageconnectionstring**. Il itère les objets BLOB 10 à la fois avec la méthode [ListBlobsSegmented](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobssegmented?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudBlobContainer_ListBlobsSegmented_System_String_System_Boolean_Microsoft_WindowsAzure_Storage_Blob_BlobListingDetails_System_Nullable_System_Int32__Microsoft_WindowsAzure_Storage_Blob_BlobContinuationToken_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) dans les conteneurs et les télécharge dans la machin locale à l’aide de la méthode [DownloadToFileAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadtofileasync?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadToFileAsync_System_String_System_IO_FileMode_Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_).
Le tableau suivant présente les [BlobRequestOptions](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions?view=azure-dotnet) définies pour chaque objet blob lors de son téléchargement.

|Propriété|Valeur|DESCRIPTION|
|---|---|---|
|[DisableContentMD5Validation](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.disablecontentmd5validation?view=azure-dotnet)| true| Cette propriété désactive la vérification du hachage MD5 du contenu téléchargé. La désactivation de la validation MD5 produit un transfert plus rapide. Mais elle ne confirme ne pas la validité ou l’intégrité des fichiers transférés. |
|[StorBlobContentMD5](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.storeblobcontentmd5?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_StoreBlobContentMD5)| false| Cette propriété détermine si un hachage MD5 est calculé et stocké.   |

La tâche `DownloadFilesAsync` est illustrée dans l’exemple suivant :

```csharp
private static async Task DownloadFilesAsync()
{
    CloudBlobClient blobClient = GetCloudBlobClient();

    // Define the BlobRequestionOptions on the download, including disabling MD5 hash validation for this example, this improves the download speed.
    BlobRequestOptions options = new BlobRequestOptions
    {
        DisableContentMD5Validation = true,
        StoreBlobContentMD5 = false
    };

    // Retrieve the list of containers in the storage account.  Create a directory and configure variables for use later.
    BlobContinuationToken continuationToken = null;
    List<CloudBlobContainer> containers = new List<CloudBlobContainer>();
    do
    {
        var listingResult = await blobClient.ListContainersSegmentedAsync(continuationToken);
        continuationToken = listingResult.ContinuationToken;
        containers.AddRange(listingResult.Results);
    }
    while (continuationToken != null);

    var directory = Directory.CreateDirectory("download");
    BlobResultSegment resultSegment = null;
    Stopwatch time = Stopwatch.StartNew();

    // Download the blobs
    try
    {
        List<Task> tasks = new List<Task>();
        int max_outstanding = 100;
        int completed_count = 0;

        // Create a new instance of the SemaphoreSlim class to define the number of threads to use in the application.
        SemaphoreSlim sem = new SemaphoreSlim(max_outstanding, max_outstanding);

        // Iterate through the containers
        foreach (CloudBlobContainer container in containers)
        {
            do
            {
                // Return the blobs from the container lazily 10 at a time.
                resultSegment = await container.ListBlobsSegmentedAsync(null, true, BlobListingDetails.All, 10, continuationToken, null, null);
                continuationToken = resultSegment.ContinuationToken;
                {
                    foreach (var blobItem in resultSegment.Results)
                    {

                        if (((CloudBlob)blobItem).Properties.BlobType == BlobType.BlockBlob)
                        {
                            // Get the blob and add a task to download the blob asynchronously from the storage account.
                            CloudBlockBlob blockBlob = container.GetBlockBlobReference(((CloudBlockBlob)blobItem).Name);
                            Console.WriteLine("Downloading {0} from container {1}", blockBlob.Name, container.Name);
                            await sem.WaitAsync();
                            tasks.Add(blockBlob.DownloadToFileAsync(directory.FullName + "\\" + blockBlob.Name, FileMode.Create, null, options, null).ContinueWith((t) =>
                            {
                                sem.Release();
                                Interlocked.Increment(ref completed_count);
                            }));

                        }
                    }
                }
            }
            while (continuationToken != null);
        }

        // Creates an asynchronous task that completes when all the downloads complete.
        await Task.WhenAll(tasks);
    }
    catch (Exception e)
    {
        Console.WriteLine("\nError encountered during transfer: {0}", e.Message);
    }

    time.Stop();
    Console.WriteLine("Download has been completed in {0} seconds. Press any key to continue", time.Elapsed.TotalSeconds.ToString());
    Console.ReadLine();
}
```

### <a name="validate-the-connections"></a>Valider les connexions

Pendant le téléchargement des fichiers, vous pouvez vérifier le nombre de connexions simultanées à votre compte de stockage. Ouvrez une `Command Prompt` et tapez `netstat -a | find /c "blob:https"`. Cette commande affiche le nombre de connexions actuellement ouvertes à l’aide de `netstat`. L’exemple suivant montre une sortie similaire à celle que vous voyez lorsque vous suivez ce didacticiel. Comme vous pouvez le voir dans cet exemple, plus de 280 connexions étaient ouvertes lors du téléchargement de fichiers aléatoires à partir du compte de stockage.

```
C:\>netstat -a | find /c "blob:https"
289

C:\>
```

## <a name="next-steps"></a>étapes suivantes

Dans la troisième partie de la série, vous avez appris à télécharger de grandes quantités de données aléatoires à partir d’un compte de stockage, notamment comment :

> [!div class="checklist"]
> * Exécution de l'application
> * Valider le nombre de connexions

Passer à la quatrième partie de la série pour vérifier les mesures de débit et la latence dans le portail.

> [!div class="nextstepaction"]
> [Vérifier les mesures de débit et de latence dans le portail](storage-blob-scalable-app-verify-metrics.md)

[previous-tutorial]: storage-blob-scalable-app-upload-files.md