---
title: "aaaTransfer données avec hello bibliothèque de déplacement des données de stockage Microsoft Azure | Documents Microsoft"
description: "Utilisez hello bibliothèque de déplacement des données toomove ou copie de données tooor à partir de l’objet blob et le fichier de contenu. Copier des données tooAzure stockage à partir de fichiers locales, ou copier des données dans ou entre des comptes de stockage. Migrer facilement vos données de tooAzure stockage."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Transfert de données avec hello bibliothèque de déplacement des données de Microsoft Azure Storage

## <a name="overview"></a>Vue d'ensemble
Hello bibliothèque de déplacement des données de Microsoft Azure Storage est une bibliothèque de multiplateforme open source qui est conçue pour des performances élevées, chargement, le téléchargement et copie des fichiers et des objets BLOB de stockage Azure. Cette bibliothèque est l’infrastructure de déplacement de données de base de hello donne toute sa puissance [AzCopy](../storage-use-azcopy.md). Hello bibliothèque de déplacement des données fournit des méthodes pratiques qui ne sont pas disponibles dans notre traditionnel [bibliothèque cliente de stockage de Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md). Cela inclut hello capacité tooset hello nombre d’opérations parallèles, suivre la progression du transfert, reprendre facilement un transfert annulé et bien plus encore.  

Cette bibliothèque utilise également .NET Core, ce qui signifie que vous pouvez l’utiliser pour créer des applications .NET pour Windows, Linux et macOS. toolearn savoir plus sur .NET Core, consultez toohello [documentation de .NET Core](https://dotnet.github.io/). Cette bibliothèque fonctionne également pour les applications .NET Framework classiques pour Windows. 

Ce document montre comment toocreate un .NET Core console application qui s’exécute sur Windows, Linux et macOS qu’effectue hello les scénarios suivants :

- Télécharger les fichiers et répertoires tooBlob stockage.
- Définir le nombre de hello d’opérations parallèles lors du transfert de données.
- suivre la progression du transfert de données ;
- reprendre les transferts de données annulés ; 
- Copiez le fichier à partir de l’URL tooBlob stockage. 
- Copier à partir du stockage d’objets Blob tooBlob stockage.

**Ce dont vous avez besoin :**

* [Visual Studio Code](https://code.visualstudio.com/)
* Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Ce guide part du principe que vous êtes déjà familiarisé avec [Azure Storage](https://azure.microsoft.com/services/storage/). Si non, la lecture hello [Introduction tooAzure stockage](storage-introduction.md) documentation est utile. Plus important encore, vous devez trop[créer un compte de stockage](storage-create-storage-account.md#create-a-storage-account) toostart à l’aide de hello bibliothèque de déplacement des données.
> 
> 

## <a name="setup"></a>Paramétrage  

1. Visitez hello [Guide d’Installation de .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Lors de la sélection de votre environnement, choisissez l’option de ligne de commande hello. 
2. À partir de la ligne de commande hello, créez un répertoire pour votre projet. Naviguer dans ce répertoire, puis tapez `dotnet new` projet de console toocreate c#.
3. Ouvrez ce répertoire dans Visual Studio Code. Cette étape peut être effectuée rapidement via la ligne de commande hello en tapant `code .`.  
4. Installer hello [c# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) à partir de Visual Studio Code Marketplace de hello. Redémarrez Visual Studio Code. 
5. À ce stade, vous devez voir deux invites. Un permet d’ajouter des « toobuild de ressources requis et débogage ». Cliquez sur « Oui ». L’autre invite permet de restaurer les dépendances non résolues. Cliquez sur « Restaurer ».
6. Votre application doit maintenant contenir un `launch.json` fichier sous hello `.vscode` active. Dans ce fichier, modifiez hello `externalConsole` valeur trop`true`.
7. Code Visual Studio vous permet de toodebug les applications .NET Core. Accès `F5` toorun votre application et vérifiez que votre programme d’installation fonctionne. « Hello World! » doit console de toohello imprimé. 

## <a name="add-data-movement-library-tooyour-project"></a>Ajouter le projet de bibliothèque de déplacement des données de tooyour

1. Ajouter la version la plus récente de hello bibliothèque de déplacement des données toohello hello `dependencies` section de votre `project.json` fichier. Au moment de l’écriture de hello, serait cette version`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Ajouter `"portable-net45+win8"` toohello `imports` section. 
3. Une invite doit s’afficher toorestore votre projet. Cliquez sur le bouton de « restaurer » hello. Vous pouvez également restaurer votre projet à partir de la ligne de commande hello en tapant la commande hello `dotnet restore` dans votre répertoire de projet racine hello.

Modifiez `project.json` :

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Configurer la structure de hello de votre application
Hello première chose à que faire est définir hello « squelette » code d’application. Ce code, nous vous invite à entrer pour une clé de compte et le nom du compte de stockage et utilise ces informations d’identification toocreate un `CloudStorageAccount` objet. Cet objet est utilisé toointeract avec notre compte de stockage dans tous les scénarios de transfert. Hello code nous invite également type hello de toochoose de l’opération de transfert, nous souhaiterions tooexecute. 

Modifiez `Program.cs` :

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Transfert de fichier local tooAzure Blob
Ajouter des méthodes hello `GetSourcePath` et `GetBlob` trop`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Modifier hello `TransferLocalFileToAzureBlob` méthode :

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Ce code nous demande hello chemin d’accès tooa local, hello nom d’un conteneur de nouveau ou existant et le fichier nom hello d’un nouvel objet blob. Hello `TransferManager.UploadAsync` méthode effectue le téléchargement de hello à l’aide de ces informations. 

Accès `F5` toorun votre application. Vous pouvez vérifier ce téléchargement hello s’est produite en affichant votre compte de stockage avec hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Définir un nombre d’opérations parallèles
Une fonctionnalité intéressante offerte par hello que bibliothèque de déplacement des données est le nombre de hello tooset hello capacité de débit de transfert de données des opérations parallèles tooincrease hello. Par défaut, hello bibliothèque de déplacement de données définit le nombre hello d’opérations parallèles too8 * hello du nombre de cœurs sur votre ordinateur. 

Gardez à l’esprit que nombreuses opérations parallèles dans un environnement à faible bande passante peuvent éviter tout problème de connexion de réseau hello et empêche réellement entièrement l’exécution des opérations. Vous devez tooexperiment avec toodetermine de ce paramètre qui vous convient le mieux en fonction sur votre bande passante réseau disponible. 

Vous allez ajouter du code qui nous permet un nombre de hello tooset d’opérations parallèles. Nous allons également ajouter le code de la durée de toocomplete de transfert hello.

Ajouter un `SetNumberOfParallelOperations` méthode trop`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Modifier hello `ExecuteChoice` méthode toouse `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Modifier hello `TransferLocalFileToAzureBlob` méthode toouse un minuteur :

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Suivre la progression des transferts
Il est très utile de connaître le temps nécessaire pour notre tootransfer de données. Toutefois, le fait progression de hello toosee en mesure de notre transfert *pendant* est même préférable d’opération de transfert hello. tooachieve ce scénario, nous devons toocreate un `TransferContext` objet. Hello `TransferContext` objet se présente sous deux formes : `SingleTransferContext` et `DirectoryTransferContext`. Hello précédent est pour le transfert d’un seul fichier (c'est-à-dire que nous allons faire maintenant) et hello ce dernier est pour le transfert d’un répertoire de fichiers (ce qui nous ajoutons ultérieurement).

Ajouter des méthodes hello `GetSingleTransferContext` et `GetDirectoryTransferContext` trop`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Modifier hello `TransferLocalFileToAzureBlob` méthode toouse `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>Reprendre un transfert annulé
Une autre fonctionnalité pratique offerte par hello bibliothèque de déplacement des données est hello capacité tooresume un transfert annulé. Vous allez ajouter du code qui permet le transfert de hello tootemporarily annuler en tapant `c`, puis reprendre le transfert de hello 3 secondes plus tard.

Modifiez `TransferLocalFileToAzureBlob` :

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Jusqu'à présent, notre `checkpoint` a toujours été la valeur trop`null`. Maintenant, si nous annulons le transfert de hello, nous extraire hello dernier point de contrôle de notre transfert, puis utiliser ce nouveau point de contrôle dans notre contexte de transfert. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Transfert de répertoire d’objets Blob tooAzure répertoire local
Il serait décevants hello bibliothèque de déplacement des données peut transférer un fichier à la fois. Heureusement, ce n’est pas le cas de hello. Hello bibliothèque de déplacement des données fournit hello capacité tootransfer un répertoire de fichiers et de tous ses sous-répertoires. Vous allez ajouter du code qui permet de toodo rien de plus.

D’abord, ajoutez la méthode hello `GetBlobDirectory` trop`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

Ensuite, modifiez `TransferLocalDirectoryToAzureBlobDirectory` :

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Il existe quelques différences entre cette méthode et la méthode hello pour télécharger un fichier unique. Nous utilisons maintenant `TransferManager.UploadDirectoryAsync` et hello `getDirectoryTransferContext` méthode que nous avons créés précédemment. En outre, nous proposons désormais une `options` valeur opération de téléchargement tooour, qui permet de tooindicate que nous souhaitons que dans les sous-répertoires tooinclude dans notre téléchargement. 

## <a name="copy-file-from-url-tooazure-blob"></a>Copiez le fichier de l’URL tooAzure Blob
Maintenant, nous allons ajouter du code qui permet de toocopy un fichier à partir d’une URL de tooan objets Blob Azure. 

Modifiez `TransferUrlToAzureBlob` :

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Un cas d’utilisation importante de cette fonctionnalité est lorsque vous avez besoin des données toomove à partir d’un autre tooAzure de service (par exemple, AWS) cloud. Tant que vous disposez d’une URL qui donne accès à toohello ressource, vous pouvez facilement déplacer cette ressource dans des objets BLOB Azure à l’aide de hello `TransferManager.CopyAsync` (méthode). Cette méthode introduit également un nouveau paramètre booléen. Ce paramètre trop`true` indique que nous voulons toodo une côté serveur asynchrone copie. Ce paramètre trop`false` indique une copie synchrone - ce qui signifie que les ressources hello sont téléchargés tooour les ordinateur local tout d’abord, puis téléchargé tooAzure Blob. Toutefois, copie synchrone est actuellement uniquement disponible pour la copie à partir d’un tooanother de ressource de stockage Azure. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Transfert de tooAzure d’objets Blob Azure Blob
Une autre fonctionnalité qui identifie de façon unique fournie par hello bibliothèque de déplacement de données est toocopy de capacité hello à partir d’un tooanother de ressource de stockage Azure. 

Modifiez `TransferAzureBlobToAzureBlob` :

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Dans cet exemple, nous avons défini le paramètre boolean hello `TransferManager.CopyAsync` trop`false` tooindicate que nous souhaitons toodo une copie synchrone. Cela signifie que les ressources hello sont téléchargés tooour les ordinateur local en premier, puis téléchargement tooAzure Blob. option de copie synchrone Hello est un tooensure idéal que votre opération de copie a une vitesse cohérente. En revanche, vitesse hello d’une copie côté serveur asynchrone est dépendante de la bande passante du réseau disponible hello sur serveur hello, qui peut varier. Toutefois, copie synchrone peut générer une copie de tooasynchronous de coût par rapport de sortie supplémentaires. Hello recommandé consiste toouse de copie synchrone dans une machine virtuelle Azure qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.

## <a name="conclusion"></a>Conclusion
Notre application de déplacement des données est à présent terminée. [exemple de code complet Hello est disponible sur GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Étapes suivantes
Dans ce guide de prise en main, nous avons créé une application qui interagit avec le Stockage Azure et s’exécute sur Windows, Linux et macOS. Il se concentre sur le Stockage Blob. Toutefois, cette même base de connaissances peut être appliqué tooFile de stockage. toolearn plus, consultez [documentation de référence de bibliothèque de déplacement des données de stockage Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




