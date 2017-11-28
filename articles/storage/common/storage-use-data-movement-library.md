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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="ba47f-105">Transfert de données avec hello bibliothèque de déplacement des données de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ba47f-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="ba47f-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ba47f-106">Overview</span></span>
<span data-ttu-id="ba47f-107">Hello bibliothèque de déplacement des données de Microsoft Azure Storage est une bibliothèque de multiplateforme open source qui est conçue pour des performances élevées, chargement, le téléchargement et copie des fichiers et des objets BLOB de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ba47f-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="ba47f-108">Cette bibliothèque est l’infrastructure de déplacement de données de base de hello donne toute sa puissance [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="ba47f-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="ba47f-109">Hello bibliothèque de déplacement des données fournit des méthodes pratiques qui ne sont pas disponibles dans notre traditionnel [bibliothèque cliente de stockage de Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="ba47f-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="ba47f-110">Cela inclut hello capacité tooset hello nombre d’opérations parallèles, suivre la progression du transfert, reprendre facilement un transfert annulé et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="ba47f-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="ba47f-111">Cette bibliothèque utilise également .NET Core, ce qui signifie que vous pouvez l’utiliser pour créer des applications .NET pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="ba47f-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="ba47f-112">toolearn savoir plus sur .NET Core, consultez toohello [documentation de .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="ba47f-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="ba47f-113">Cette bibliothèque fonctionne également pour les applications .NET Framework classiques pour Windows.</span><span class="sxs-lookup"><span data-stu-id="ba47f-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="ba47f-114">Ce document montre comment toocreate un .NET Core console application qui s’exécute sur Windows, Linux et macOS qu’effectue hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="ba47f-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="ba47f-115">Télécharger les fichiers et répertoires tooBlob stockage.</span><span class="sxs-lookup"><span data-stu-id="ba47f-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="ba47f-116">Définir le nombre de hello d’opérations parallèles lors du transfert de données.</span><span class="sxs-lookup"><span data-stu-id="ba47f-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="ba47f-117">suivre la progression du transfert de données ;</span><span class="sxs-lookup"><span data-stu-id="ba47f-117">Track data transfer progress.</span></span>
- <span data-ttu-id="ba47f-118">reprendre les transferts de données annulés ;</span><span class="sxs-lookup"><span data-stu-id="ba47f-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="ba47f-119">Copiez le fichier à partir de l’URL tooBlob stockage.</span><span class="sxs-lookup"><span data-stu-id="ba47f-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="ba47f-120">Copier à partir du stockage d’objets Blob tooBlob stockage.</span><span class="sxs-lookup"><span data-stu-id="ba47f-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="ba47f-121">**Ce dont vous avez besoin :**</span><span class="sxs-lookup"><span data-stu-id="ba47f-121">**What you need:**</span></span>

* [<span data-ttu-id="ba47f-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ba47f-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="ba47f-123">Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="ba47f-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="ba47f-124">Ce guide part du principe que vous êtes déjà familiarisé avec [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="ba47f-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="ba47f-125">Si non, la lecture hello [Introduction tooAzure stockage](storage-introduction.md) documentation est utile.</span><span class="sxs-lookup"><span data-stu-id="ba47f-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="ba47f-126">Plus important encore, vous devez trop[créer un compte de stockage](storage-create-storage-account.md#create-a-storage-account) toostart à l’aide de hello bibliothèque de déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="ba47f-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="ba47f-127">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="ba47f-127">Setup</span></span>  

1. <span data-ttu-id="ba47f-128">Visitez hello [Guide d’Installation de .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ba47f-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="ba47f-129">Lors de la sélection de votre environnement, choisissez l’option de ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="ba47f-130">À partir de la ligne de commande hello, créez un répertoire pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="ba47f-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="ba47f-131">Naviguer dans ce répertoire, puis tapez `dotnet new` projet de console toocreate c#.</span><span class="sxs-lookup"><span data-stu-id="ba47f-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="ba47f-132">Ouvrez ce répertoire dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ba47f-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="ba47f-133">Cette étape peut être effectuée rapidement via la ligne de commande hello en tapant `code .`.</span><span class="sxs-lookup"><span data-stu-id="ba47f-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="ba47f-134">Installer hello [c# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) à partir de Visual Studio Code Marketplace de hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="ba47f-135">Redémarrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ba47f-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="ba47f-136">À ce stade, vous devez voir deux invites.</span><span class="sxs-lookup"><span data-stu-id="ba47f-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="ba47f-137">Un permet d’ajouter des « toobuild de ressources requis et débogage ».</span><span class="sxs-lookup"><span data-stu-id="ba47f-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="ba47f-138">Cliquez sur « Oui ».</span><span class="sxs-lookup"><span data-stu-id="ba47f-138">Click "yes."</span></span> <span data-ttu-id="ba47f-139">L’autre invite permet de restaurer les dépendances non résolues.</span><span class="sxs-lookup"><span data-stu-id="ba47f-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="ba47f-140">Cliquez sur « Restaurer ».</span><span class="sxs-lookup"><span data-stu-id="ba47f-140">Click "restore."</span></span>
6. <span data-ttu-id="ba47f-141">Votre application doit maintenant contenir un `launch.json` fichier sous hello `.vscode` active.</span><span class="sxs-lookup"><span data-stu-id="ba47f-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="ba47f-142">Dans ce fichier, modifiez hello `externalConsole` valeur trop`true`.</span><span class="sxs-lookup"><span data-stu-id="ba47f-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="ba47f-143">Code Visual Studio vous permet de toodebug les applications .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ba47f-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="ba47f-144">Accès `F5` toorun votre application et vérifiez que votre programme d’installation fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ba47f-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="ba47f-145">« Hello World! » doit</span><span class="sxs-lookup"><span data-stu-id="ba47f-145">You should see "Hello World!"</span></span> <span data-ttu-id="ba47f-146">console de toohello imprimé.</span><span class="sxs-lookup"><span data-stu-id="ba47f-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="ba47f-147">Ajouter le projet de bibliothèque de déplacement des données de tooyour</span><span class="sxs-lookup"><span data-stu-id="ba47f-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="ba47f-148">Ajouter la version la plus récente de hello bibliothèque de déplacement des données toohello hello `dependencies` section de votre `project.json` fichier.</span><span class="sxs-lookup"><span data-stu-id="ba47f-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="ba47f-149">Au moment de l’écriture de hello, serait cette version`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="ba47f-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="ba47f-150">Ajouter `"portable-net45+win8"` toohello `imports` section.</span><span class="sxs-lookup"><span data-stu-id="ba47f-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="ba47f-151">Une invite doit s’afficher toorestore votre projet.</span><span class="sxs-lookup"><span data-stu-id="ba47f-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="ba47f-152">Cliquez sur le bouton de « restaurer » hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-152">Click hello "restore" button.</span></span> <span data-ttu-id="ba47f-153">Vous pouvez également restaurer votre projet à partir de la ligne de commande hello en tapant la commande hello `dotnet restore` dans votre répertoire de projet racine hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="ba47f-154">Modifiez `project.json` :</span><span class="sxs-lookup"><span data-stu-id="ba47f-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="ba47f-155">Configurer la structure de hello de votre application</span><span class="sxs-lookup"><span data-stu-id="ba47f-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="ba47f-156">Hello première chose à que faire est définir hello « squelette » code d’application.</span><span class="sxs-lookup"><span data-stu-id="ba47f-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="ba47f-157">Ce code, nous vous invite à entrer pour une clé de compte et le nom du compte de stockage et utilise ces informations d’identification toocreate un `CloudStorageAccount` objet.</span><span class="sxs-lookup"><span data-stu-id="ba47f-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="ba47f-158">Cet objet est utilisé toointeract avec notre compte de stockage dans tous les scénarios de transfert.</span><span class="sxs-lookup"><span data-stu-id="ba47f-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="ba47f-159">Hello code nous invite également type hello de toochoose de l’opération de transfert, nous souhaiterions tooexecute.</span><span class="sxs-lookup"><span data-stu-id="ba47f-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="ba47f-160">Modifiez `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="ba47f-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="ba47f-161">Transfert de fichier local tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="ba47f-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="ba47f-162">Ajouter des méthodes hello `GetSourcePath` et `GetBlob` trop`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="ba47f-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="ba47f-163">Modifier hello `TransferLocalFileToAzureBlob` méthode :</span><span class="sxs-lookup"><span data-stu-id="ba47f-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="ba47f-164">Ce code nous demande hello chemin d’accès tooa local, hello nom d’un conteneur de nouveau ou existant et le fichier nom hello d’un nouvel objet blob.</span><span class="sxs-lookup"><span data-stu-id="ba47f-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="ba47f-165">Hello `TransferManager.UploadAsync` méthode effectue le téléchargement de hello à l’aide de ces informations.</span><span class="sxs-lookup"><span data-stu-id="ba47f-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="ba47f-166">Accès `F5` toorun votre application.</span><span class="sxs-lookup"><span data-stu-id="ba47f-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="ba47f-167">Vous pouvez vérifier ce téléchargement hello s’est produite en affichant votre compte de stockage avec hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ba47f-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="ba47f-168">Définir un nombre d’opérations parallèles</span><span class="sxs-lookup"><span data-stu-id="ba47f-168">Set number of parallel operations</span></span>
<span data-ttu-id="ba47f-169">Une fonctionnalité intéressante offerte par hello que bibliothèque de déplacement des données est le nombre de hello tooset hello capacité de débit de transfert de données des opérations parallèles tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="ba47f-170">Par défaut, hello bibliothèque de déplacement de données définit le nombre hello d’opérations parallèles too8 * hello du nombre de cœurs sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ba47f-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="ba47f-171">Gardez à l’esprit que nombreuses opérations parallèles dans un environnement à faible bande passante peuvent éviter tout problème de connexion de réseau hello et empêche réellement entièrement l’exécution des opérations.</span><span class="sxs-lookup"><span data-stu-id="ba47f-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="ba47f-172">Vous devez tooexperiment avec toodetermine de ce paramètre qui vous convient le mieux en fonction sur votre bande passante réseau disponible.</span><span class="sxs-lookup"><span data-stu-id="ba47f-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="ba47f-173">Vous allez ajouter du code qui nous permet un nombre de hello tooset d’opérations parallèles.</span><span class="sxs-lookup"><span data-stu-id="ba47f-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="ba47f-174">Nous allons également ajouter le code de la durée de toocomplete de transfert hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="ba47f-175">Ajouter un `SetNumberOfParallelOperations` méthode trop`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="ba47f-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="ba47f-176">Modifier hello `ExecuteChoice` méthode toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="ba47f-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="ba47f-177">Modifier hello `TransferLocalFileToAzureBlob` méthode toouse un minuteur :</span><span class="sxs-lookup"><span data-stu-id="ba47f-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="ba47f-178">Suivre la progression des transferts</span><span class="sxs-lookup"><span data-stu-id="ba47f-178">Track transfer progress</span></span>
<span data-ttu-id="ba47f-179">Il est très utile de connaître le temps nécessaire pour notre tootransfer de données.</span><span class="sxs-lookup"><span data-stu-id="ba47f-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="ba47f-180">Toutefois, le fait progression de hello toosee en mesure de notre transfert *pendant* est même préférable d’opération de transfert hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="ba47f-181">tooachieve ce scénario, nous devons toocreate un `TransferContext` objet.</span><span class="sxs-lookup"><span data-stu-id="ba47f-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="ba47f-182">Hello `TransferContext` objet se présente sous deux formes : `SingleTransferContext` et `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="ba47f-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="ba47f-183">Hello précédent est pour le transfert d’un seul fichier (c'est-à-dire que nous allons faire maintenant) et hello ce dernier est pour le transfert d’un répertoire de fichiers (ce qui nous ajoutons ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="ba47f-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="ba47f-184">Ajouter des méthodes hello `GetSingleTransferContext` et `GetDirectoryTransferContext` trop`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="ba47f-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="ba47f-185">Modifier hello `TransferLocalFileToAzureBlob` méthode toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="ba47f-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="ba47f-186">Reprendre un transfert annulé</span><span class="sxs-lookup"><span data-stu-id="ba47f-186">Resume a canceled transfer</span></span>
<span data-ttu-id="ba47f-187">Une autre fonctionnalité pratique offerte par hello bibliothèque de déplacement des données est hello capacité tooresume un transfert annulé.</span><span class="sxs-lookup"><span data-stu-id="ba47f-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="ba47f-188">Vous allez ajouter du code qui permet le transfert de hello tootemporarily annuler en tapant `c`, puis reprendre le transfert de hello 3 secondes plus tard.</span><span class="sxs-lookup"><span data-stu-id="ba47f-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="ba47f-189">Modifiez `TransferLocalFileToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="ba47f-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="ba47f-190">Jusqu'à présent, notre `checkpoint` a toujours été la valeur trop`null`.</span><span class="sxs-lookup"><span data-stu-id="ba47f-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="ba47f-191">Maintenant, si nous annulons le transfert de hello, nous extraire hello dernier point de contrôle de notre transfert, puis utiliser ce nouveau point de contrôle dans notre contexte de transfert.</span><span class="sxs-lookup"><span data-stu-id="ba47f-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="ba47f-192">Transfert de répertoire d’objets Blob tooAzure répertoire local</span><span class="sxs-lookup"><span data-stu-id="ba47f-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="ba47f-193">Il serait décevants hello bibliothèque de déplacement des données peut transférer un fichier à la fois.</span><span class="sxs-lookup"><span data-stu-id="ba47f-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="ba47f-194">Heureusement, ce n’est pas le cas de hello.</span><span class="sxs-lookup"><span data-stu-id="ba47f-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="ba47f-195">Hello bibliothèque de déplacement des données fournit hello capacité tootransfer un répertoire de fichiers et de tous ses sous-répertoires.</span><span class="sxs-lookup"><span data-stu-id="ba47f-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="ba47f-196">Vous allez ajouter du code qui permet de toodo rien de plus.</span><span class="sxs-lookup"><span data-stu-id="ba47f-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="ba47f-197">D’abord, ajoutez la méthode hello `GetBlobDirectory` trop`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="ba47f-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="ba47f-198">Ensuite, modifiez `TransferLocalDirectoryToAzureBlobDirectory` :</span><span class="sxs-lookup"><span data-stu-id="ba47f-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="ba47f-199">Il existe quelques différences entre cette méthode et la méthode hello pour télécharger un fichier unique.</span><span class="sxs-lookup"><span data-stu-id="ba47f-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="ba47f-200">Nous utilisons maintenant `TransferManager.UploadDirectoryAsync` et hello `getDirectoryTransferContext` méthode que nous avons créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="ba47f-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="ba47f-201">En outre, nous proposons désormais une `options` valeur opération de téléchargement tooour, qui permet de tooindicate que nous souhaitons que dans les sous-répertoires tooinclude dans notre téléchargement.</span><span class="sxs-lookup"><span data-stu-id="ba47f-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="ba47f-202">Copiez le fichier de l’URL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="ba47f-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="ba47f-203">Maintenant, nous allons ajouter du code qui permet de toocopy un fichier à partir d’une URL de tooan objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ba47f-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="ba47f-204">Modifiez `TransferUrlToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="ba47f-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="ba47f-205">Un cas d’utilisation importante de cette fonctionnalité est lorsque vous avez besoin des données toomove à partir d’un autre tooAzure de service (par exemple, AWS) cloud.</span><span class="sxs-lookup"><span data-stu-id="ba47f-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="ba47f-206">Tant que vous disposez d’une URL qui donne accès à toohello ressource, vous pouvez facilement déplacer cette ressource dans des objets BLOB Azure à l’aide de hello `TransferManager.CopyAsync` (méthode).</span><span class="sxs-lookup"><span data-stu-id="ba47f-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="ba47f-207">Cette méthode introduit également un nouveau paramètre booléen.</span><span class="sxs-lookup"><span data-stu-id="ba47f-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="ba47f-208">Ce paramètre trop`true` indique que nous voulons toodo une côté serveur asynchrone copie.</span><span class="sxs-lookup"><span data-stu-id="ba47f-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="ba47f-209">Ce paramètre trop`false` indique une copie synchrone - ce qui signifie que les ressources hello sont téléchargés tooour les ordinateur local tout d’abord, puis téléchargé tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="ba47f-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="ba47f-210">Toutefois, copie synchrone est actuellement uniquement disponible pour la copie à partir d’un tooanother de ressource de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ba47f-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="ba47f-211">Transfert de tooAzure d’objets Blob Azure Blob</span><span class="sxs-lookup"><span data-stu-id="ba47f-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="ba47f-212">Une autre fonctionnalité qui identifie de façon unique fournie par hello bibliothèque de déplacement de données est toocopy de capacité hello à partir d’un tooanother de ressource de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ba47f-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="ba47f-213">Modifiez `TransferAzureBlobToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="ba47f-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="ba47f-214">Dans cet exemple, nous avons défini le paramètre boolean hello `TransferManager.CopyAsync` trop`false` tooindicate que nous souhaitons toodo une copie synchrone.</span><span class="sxs-lookup"><span data-stu-id="ba47f-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="ba47f-215">Cela signifie que les ressources hello sont téléchargés tooour les ordinateur local en premier, puis téléchargement tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="ba47f-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="ba47f-216">option de copie synchrone Hello est un tooensure idéal que votre opération de copie a une vitesse cohérente.</span><span class="sxs-lookup"><span data-stu-id="ba47f-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="ba47f-217">En revanche, vitesse hello d’une copie côté serveur asynchrone est dépendante de la bande passante du réseau disponible hello sur serveur hello, qui peut varier.</span><span class="sxs-lookup"><span data-stu-id="ba47f-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="ba47f-218">Toutefois, copie synchrone peut générer une copie de tooasynchronous de coût par rapport de sortie supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ba47f-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="ba47f-219">Hello recommandé consiste toouse de copie synchrone dans une machine virtuelle Azure qui se trouve dans hello même région que votre coût sortie tooavoid de compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="ba47f-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ba47f-220">Conclusion</span><span class="sxs-lookup"><span data-stu-id="ba47f-220">Conclusion</span></span>
<span data-ttu-id="ba47f-221">Notre application de déplacement des données est à présent terminée.</span><span class="sxs-lookup"><span data-stu-id="ba47f-221">Our data movement application is now complete.</span></span> <span data-ttu-id="ba47f-222">[exemple de code complet Hello est disponible sur GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="ba47f-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ba47f-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba47f-223">Next steps</span></span>
<span data-ttu-id="ba47f-224">Dans ce guide de prise en main, nous avons créé une application qui interagit avec le Stockage Azure et s’exécute sur Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="ba47f-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="ba47f-225">Il se concentre sur le Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="ba47f-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="ba47f-226">Toutefois, cette même base de connaissances peut être appliqué tooFile de stockage.</span><span class="sxs-lookup"><span data-stu-id="ba47f-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="ba47f-227">toolearn plus, consultez [documentation de référence de bibliothèque de déplacement des données de stockage Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="ba47f-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




