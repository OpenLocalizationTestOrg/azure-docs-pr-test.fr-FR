---
title: "Charger en parallèle de grandes quantités de données aléatoires dans le stockage Azure | Microsoft Docs"
description: "Découvrir comment utiliser le SDK Azure pour charger en parallèle de grandes quantités de données aléatoires dans un compte de stockage Azure"
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
ms.openlocfilehash: 98f3f69c6025d61caac20e13b573651854952432
ms.sourcegitcommit: 4256ebfe683b08fedd1a63937328931a5d35b157
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="upload-large-amounts-of-random-data-in-parallel-to-azure-storage"></a>Charger en parallèle de grandes quantités de données aléatoires dans le stockage Azure

Ce didacticiel est le deuxième d’une série. Ce didacticiel décrit le déploiement d’une application qui charge une grande quantité de données aléatoires dans un compte de stockage Azure.

Dans ce deuxième volet, vous apprenez à :

> [!div class="checklist"]
> * Configurer la chaîne de connexion
> * Création de l'application
> * Exécution de l'application
> * Valider le nombre de connexions

Le Stockage blob Azure fournit un service évolutif pour stocker vos données. Pour que votre application soit aussi performante que possible, vous devez comprendre le fonctionnement du stockage blob. Vous devez connaître les limites des objets blob Azure. Pour en savoir plus sur ces limites, consultez : [Objectifs d’évolutivité du stockage blob](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#azure-blob-storage-scale-targets).

La [convention de nommage des partitions](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#subheading47) est un autre facteur important quand vous concevez une application hautement performante à l’aide d’objets blob. Le Stockage Azure utilise un schéma de partitionnement basé sur une plage pour mettre à l’échelle et équilibrer la charge. Cette configuration signifie que les fichiers qui ont des conventions de nommage ou des préfixes similaires sont dirigés dans la même partition. Cette logique inclut le nom du conteneur dans lequel les fichiers sont chargés. Dans ce didacticiel, vous utilisez des fichiers qui ont des GUID comme noms ainsi que du contenu généré aléatoirement. Ils sont ensuite chargés dans cinq conteneurs différents avec des noms aléatoires.

## <a name="prerequisites"></a>configuration requise

Pour effectuer ce didacticiel, vous devez avoir terminé le didacticiel précédent sur le stockage : [Créer une machine virtuelle et un compte de stockage pour une application évolutive][previous-tutorial].

## <a name="remote-into-your-virtual-machine"></a>Ouvrir une session Bureau à distance sur votre machine virtuelle

Exécutez la commande suivante sur votre machine locale pour créer une session Bureau à distance avec la machine virtuelle. Remplacez l’adresse IP par l’adresse publicIPAddress de votre machine virtuelle. À l’invite, entrez les informations d’identification que vous avez utilisées pour créer la machine virtuelle.

```
mstsc /v:<publicIpAddress>
```

## <a name="configure-the-connection-string"></a>Configurer la chaîne de connexion

Dans le portail Azure, accédez à votre compte de stockage. Sélectionnez **Clés d’accès** sous **Paramètres** dans votre compte de stockage. Copiez la **chaîne de connexion** de la clé primaire ou secondaire. Connectez-vous à la machine virtuelle créée dans le didacticiel précédent. Ouvrez une **invite de commandes** comme administrateur et exécutez la commande `setx` avec le commutateur `/m`, cette commande enregistre une variable d’environnement de paramètre de machine. La variable d’environnement n’est pas disponible tant que vous n’avez pas rechargé **l’invite de commandes**. Remplacez **\<storageConnectionString\>** dans l’exemple suivant :

```
setx storageconnectionstring "<storageConnectionString>" /m
```

Une fois que vous avez terminé, ouvrez une autre **invite de commandes**, accédez à `D:\git\storage-dotnet-perf-scale-app` et tapez `dotnet build` pour créer l’application.

## <a name="run-the-application"></a>Exécution de l'application

Accédez à `D:\git\storage-dotnet-perf-scale-app`.

Saisissez `dotnet run` pour exécuter l’application. La première fois que vous exécutez `dotnet`, il remplit votre cache de package local pour améliorer la vitesse de restauration et activer l’accès hors connexion. L’exécution de cette commande prend jusqu’à une minute et ne se produit qu’une seule fois.

```
dotnet run
```

L’application crée cinq conteneurs nommés de façon aléatoire et commence à charger les fichiers dans le répertoire de préproduction du compte de stockage. L’application définit 100 threads minimum et la valeur de [DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(v=vs.110).aspx) sur 100 pour garantir l’autorisation d’un grand nombre de connexions simultanées quand l’application est exécutée.

En plus de définir les paramètres de limite de threads et de connexion, les valeurs [BlobRequestOptions](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions?view=azure-dotnet) pour la méthode [UploadFromStreamAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstreamasync?view=azure-dotnet) sont configurées pour utiliser le parallélisme et désactiver la validation de hachage MD5. Les fichiers sont chargés dans des blocs de 100 Mo, cette configuration offre de meilleures performances, mais peut s’avérer coûteuse si vous utilisez un réseau peu performant, car, en cas d’échec, le bloc entier de 100 Mo est réessayé.

|Propriété|Valeur|DESCRIPTION|
|---|---|---|
|[ParallelOperationThreadCount](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.paralleloperationthreadcount?view=azure-dotnet)| 8| Le paramètre divise l’objet blob en blocs pendant le chargement. Pour optimiser les performances, cette valeur doit être 8 fois supérieure au nombre de cœurs. |
|[DisableContentMD5Validation](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.disablecontentmd5validation?view=azure-dotnet)| true| Cette propriété désactive la vérification du hachage MD5 du contenu chargé. La désactivation de la validation MD5 entraîne un transfert plus rapide. Toutefois, elle ne confirme pas la validité ou l’intégrité des fichiers transférés.   |
|[StorBlobContentMD5](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.storeblobcontentmd5?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_StoreBlobContentMD5)| false| Cette propriété détermine si un hachage MD5 est calculé et stocké avec le fichier.   |
| [RetryPolicy](/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.retrypolicy?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_RetryPolicy)| Interruption de 2 secondes avec 10 nouvelles tentatives au maximum |Détermine la stratégie de nouvelle tentative des demandes. Les connexions qui ont échoué sont réessayées, dans cet exemple une stratégie [ExponentialRetry](/dotnet/api/microsoft.windowsazure.storage.retrypolicies.exponentialretry?view=azure-dotnet) est configurée avec une interruption de 2 secondes et 10 nouvelles tentatives au maximum. Ce paramètre est important quand votre application se rapproche des [objectifs d’évolutivité du stockage blob](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#azure-blob-storage-scale-targets).  |

La tâche `UploadFilesAsync` est illustrée dans l’exemple suivant :

```csharp
private static async Task UploadFilesAsync()
{
    // Create random 5 characters containers to upload files to.
    CloudBlobContainer[] containers = await GetRandomContainersAsync();
    var currentdir = System.IO.Directory.GetCurrentDirectory();

    // path to the directory to upload
    string uploadPath = currentdir + "\\upload";
    Stopwatch time = Stopwatch.StartNew();
    try
    {
        Console.WriteLine("Iterating in directory: {0}", uploadPath);
        int count = 0;
        int max_outstanding = 100;
        int completed_count = 0;

        // Define the BlobRequestionOptions on the upload.
        // This includes defining an exponential retry policy to ensure that failed connections are retried with a backoff policy. As multiple large files are being uploaded
        // large block sizes this can cause an issue if an exponential retry policy is not defined.  Additionally parallel operations are enabled with a thread count of 8
        // This could be should be multiple of the number of cores that the machine has. Lastly MD5 hash validation is disabled for this example, this improves the upload speed.
        BlobRequestOptions options = new BlobRequestOptions
        {
            ParallelOperationThreadCount = 8,
            DisableContentMD5Validation = true,
            StoreBlobContentMD5 = false
        };
        // Create a new instance of the SemaphoreSlim class to define the number of threads to use in the application.
        SemaphoreSlim sem = new SemaphoreSlim(max_outstanding, max_outstanding);

        List<Task> tasks = new List<Task>();
        Console.WriteLine("Found {0} file(s)", Directory.GetFiles(uploadPath).Count());

        // Iterate through the files
        foreach (string path in Directory.GetFiles(uploadPath))
        {
            // Create random file names and set the block size that is used for the upload.
            var container = containers[count % 5];
            string fileName = Path.GetFileName(path);
            Console.WriteLine("Uploading {0} to container {1}.", path, container.Name);
            CloudBlockBlob blockBlob = container.GetBlockBlobReference(fileName);

            // Set block size to 100MB.
            blockBlob.StreamWriteSizeInBytes = 100 * 1024 * 1024;
            await sem.WaitAsync();

            // Create tasks for each file that is uploaded. This is added to a collection that executes them all asyncronously.  
            tasks.Add(blockBlob.UploadFromFileAsync(path, null, options, null).ContinueWith((t) =>
            {
                sem.Release();
                Interlocked.Increment(ref completed_count);
            }));
            count++;
        }

        // Creates an asynchronous task that completes when all the uploads complete.
        await Task.WhenAll(tasks);

        time.Stop();

        Console.WriteLine("Upload has been completed in {0} seconds. Press any key to continue", time.Elapsed.TotalSeconds.ToString());

        Console.ReadLine();
    }
    catch (DirectoryNotFoundException ex)
    {
        Console.WriteLine("Error parsing files in the directory: {0}", ex.Message);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
}
```

L’exemple suivant est une sortie d’application tronquée s’exécutant sur un système Windows.

```
Created container https://mystorageaccount.blob.core.windows.net/9efa7ecb-2b24-49ff-8e5b-1d25e5481076
Created container https://mystorageaccount.blob.core.windows.net/bbe5f0c8-be9e-4fc3-bcbd-2092433dbf6b
Created container https://mystorageaccount.blob.core.windows.net/9ac2f71c-6b44-40e7-b7be-8519d3ba4e8f
Created container https://mystorageaccount.blob.core.windows.net/47646f1a-c498-40cd-9dae-840f46072180
Created container https://mystorageaccount.blob.core.windows.net/38b2cdab-45fa-4cf9-94e7-d533837365aa
Iterating in directory: D:\git\storage-dotnet-perf-scale-app\upload
Found 50 file(s)
Starting upload of D:\git\storage-dotnet-perf-scale-app\upload\1d596d16-f6de-4c4c-8058-50ebd8141e4d.txt to container 9efa7ecb-2b24-49ff-8e5b-1d25e5481076.
Starting upload of D:\git\storage-dotnet-perf-scale-app\upload\242ff392-78be-41fb-b9d4-aee8152a6279.txt to container bbe5f0c8-be9e-4fc3-bcbd-2092433dbf6b.
Starting upload of D:\git\storage-dotnet-perf-scale-app\upload\38d4d7e2-acb4-4efc-ba39-f9611d0d55ef.txt to container 9ac2f71c-6b44-40e7-b7be-8519d3ba4e8f.
Starting upload of D:\git\storage-dotnet-perf-scale-app\upload\45930d63-b0d0-425f-a766-cda27ff00d32.txt to container 47646f1a-c498-40cd-9dae-840f46072180.
Starting upload of D:\git\storage-dotnet-perf-scale-app\upload\5129b385-5781-43be-8bac-e2fbb7d2bd82.txt to container 38b2cdab-45fa-4cf9-94e7-d533837365aa.
...
Upload has been completed in 142.0429536 seconds. Press any key to continue
```

### <a name="validate-the-connections"></a>Valider les connexions

Pendant le chargement des fichiers, vous pouvez vérifier le nombre de connexions simultanées sur votre compte de stockage. Ouvrez une **invite de commandes** et tapez `netstat -a | find /c "blob:https"`. Cette commande affiche le nombre de connexions actuellement ouvertes à l’aide de `netstat`. L’exemple suivant illustre une sortie similaire à celle que vous voyez quand vous suivez ce didacticiel. Comme vous pouvez le voir dans l’exemple, 800 connexions étaient ouvertes pendant le chargement des fichiers aléatoires dans le compte de stockage. Cette valeur change à mesure de l’exécution du chargement. En chargeant des segments de bloc en parallèle, la quantité de temps nécessaire pour transférer le contenu est considérablement réduite.

```
C:\>netstat -a | find /c "blob:https"
800

C:\>
```

## <a name="next-steps"></a>étapes suivantes

Dans la deuxième partie de la série, vous avez appris à charger de grandes quantités de données aléatoires dans un compte de stockage, notamment comment :

> [!div class="checklist"]
> * Configurer la chaîne de connexion
> * Création de l'application
> * Exécution de l'application
> * Valider le nombre de connexions

Passez à la troisième partie de la série pour télécharger de grandes quantités de données à partir d’un compte de stockage.

> [!div class="nextstepaction"]
> [Charger en parallèle de grandes quantités de fichiers volumineux dans un compte de stockage](storage-blob-scalable-app-download-files.md)

[previous-tutorial]: storage-blob-scalable-app-create-vm.md
