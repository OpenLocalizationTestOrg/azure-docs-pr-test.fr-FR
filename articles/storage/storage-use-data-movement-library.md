---
title: "Transférer des données avec la bibliothèque de déplacement des données du Stockage Microsoft Azure | Microsoft Docs"
description: "Utilisez la bibliothèque de déplacement des données pour déplacer ou copier des données vers ou à partir du contenu d'objets blob et de fichiers. Copiez des données vers Azure Storage à partir de fichiers locaux ou copiez des données dans ou entre des comptes de stockage. Migrez facilement vos données vers Azure Storage."
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="bb49b-105">Transférer des données avec la bibliothèque de déplacement des données du Stockage Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bb49b-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="bb49b-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bb49b-106">Overview</span></span>
<span data-ttu-id="bb49b-107">La bibliothèque de déplacement des données du Stockage Microsoft Azure est une bibliothèque multiplateforme open source conçue pour charger, télécharger et copier des objets blob et des fichiers du Stockage Azure avec des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="bb49b-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="bb49b-108">Cette bibliothèque est l’infrastructure centrale de déplacement des données [d’AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="bb49b-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="bb49b-109">La bibliothèque de déplacement des données fournit des méthodes utiles qui ne sont pas disponibles dans notre [bibliothèque cliente classique du Stockage Azure .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bb49b-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bb49b-110">Parmi elles figure la capacité à définir le nombre d’opérations parallèles, à suivre la progression des transferts, à reprendre facilement un transfert annulé et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="bb49b-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="bb49b-111">Cette bibliothèque utilise également .NET Core, ce qui signifie que vous pouvez l’utiliser pour créer des applications .NET pour Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="bb49b-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="bb49b-112">Pour en savoir plus sur .NET Core, consultez la [Documentation .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="bb49b-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="bb49b-113">Cette bibliothèque fonctionne également pour les applications .NET Framework classiques pour Windows.</span><span class="sxs-lookup"><span data-stu-id="bb49b-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="bb49b-114">Ce document montre comment créer une application de console .NET Core qui s’exécute sous Windows, Linux et macOS et effectue les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="bb49b-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="bb49b-115">charger des fichiers et des répertoires vers le Stockage Blob ;</span><span class="sxs-lookup"><span data-stu-id="bb49b-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="bb49b-116">définir le nombre d’opérations parallèles lors du transfert de données ;</span><span class="sxs-lookup"><span data-stu-id="bb49b-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="bb49b-117">suivre la progression du transfert de données ;</span><span class="sxs-lookup"><span data-stu-id="bb49b-117">Track data transfer progress.</span></span>
- <span data-ttu-id="bb49b-118">reprendre les transferts de données annulés ;</span><span class="sxs-lookup"><span data-stu-id="bb49b-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="bb49b-119">copier des fichiers de l’URL vers le Stockage Blob ;</span><span class="sxs-lookup"><span data-stu-id="bb49b-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="bb49b-120">copier d’un Stockage Blob à un autre.</span><span class="sxs-lookup"><span data-stu-id="bb49b-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="bb49b-121">**Ce dont vous avez besoin :**</span><span class="sxs-lookup"><span data-stu-id="bb49b-121">**What you need:**</span></span>

* [<span data-ttu-id="bb49b-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bb49b-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="bb49b-123">Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="bb49b-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="bb49b-124">Ce guide part du principe que vous êtes déjà familiarisé avec [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="bb49b-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="bb49b-125">Sinon, il est utile de lire la documentation [Introduction au Stockage Azure](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb49b-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="bb49b-126">Plus important encore, vous devez [créer un compte de Stockage](storage-create-storage-account.md#create-a-storage-account) pour pouvoir utiliser la bibliothèque de déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="bb49b-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="bb49b-127">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="bb49b-127">Setup</span></span>  

1. <span data-ttu-id="bb49b-128">Consultez le [Guide d’installation de .NET Core](https://www.microsoft.com/net/core) pour installer .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bb49b-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="bb49b-129">Lorsque vous sélectionnez votre environnement, choisissez l’option de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="bb49b-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="bb49b-130">En ligne de commande, créez un répertoire pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="bb49b-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="bb49b-131">Accédez à ce répertoire, puis tapez `dotnet new` pour créer un projet de console C#.</span><span class="sxs-lookup"><span data-stu-id="bb49b-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="bb49b-132">Ouvrez ce répertoire dans Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bb49b-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="bb49b-133">Vous pouvez effectuer rapidement cette étape en tapant `code .` en ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="bb49b-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="bb49b-134">Installez [l’extension C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) à partir de la Place de marché Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb49b-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="bb49b-135">Redémarrez Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bb49b-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="bb49b-136">À ce stade, vous devez voir deux invites.</span><span class="sxs-lookup"><span data-stu-id="bb49b-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="bb49b-137">L’une permet d’ajouter les « composants requis pour générer et déboguer ».</span><span class="sxs-lookup"><span data-stu-id="bb49b-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="bb49b-138">Cliquez sur « Oui ».</span><span class="sxs-lookup"><span data-stu-id="bb49b-138">Click "yes."</span></span> <span data-ttu-id="bb49b-139">L’autre invite permet de restaurer les dépendances non résolues.</span><span class="sxs-lookup"><span data-stu-id="bb49b-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="bb49b-140">Cliquez sur « Restaurer ».</span><span class="sxs-lookup"><span data-stu-id="bb49b-140">Click "restore."</span></span>
6. <span data-ttu-id="bb49b-141">Votre application doit maintenant contenir un fichier `launch.json` sous le répertoire `.vscode`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="bb49b-142">Dans ce fichier, donnez la valeur `true` à `externalConsole`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="bb49b-143">Visual Studio Code vous permet de déboguer les applications .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bb49b-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="bb49b-144">Appuyez sur `F5` pour exécuter votre application et vérifier que votre configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="bb49b-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="bb49b-145">« Hello World! » doit</span><span class="sxs-lookup"><span data-stu-id="bb49b-145">You should see "Hello World!"</span></span> <span data-ttu-id="bb49b-146">s’imprimer dans la console.</span><span class="sxs-lookup"><span data-stu-id="bb49b-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="bb49b-147">Ajouter la bibliothèque de déplacement des données à votre projet</span><span class="sxs-lookup"><span data-stu-id="bb49b-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="bb49b-148">Ajoutez la dernière version de la bibliothèque de déplacement des données à la section `dependencies` de votre fichier `project.json`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="bb49b-149">Au moment de la rédaction de cette page, il s’agit de la version `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="bb49b-150">Ajoutez `"portable-net45+win8"` à la section `imports`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="bb49b-151">Une invite doit s’afficher pour restaurer votre projet.</span><span class="sxs-lookup"><span data-stu-id="bb49b-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="bb49b-152">Cliquez sur le bouton « Restaurer ».</span><span class="sxs-lookup"><span data-stu-id="bb49b-152">Click the "restore" button.</span></span> <span data-ttu-id="bb49b-153">Vous pouvez également restaurer votre projet en ligne de commande en tapant la commande `dotnet restore` à la racine du répertoire de votre projet.</span><span class="sxs-lookup"><span data-stu-id="bb49b-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="bb49b-154">Modifiez `project.json` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="bb49b-155">Définir le squelette de votre application</span><span class="sxs-lookup"><span data-stu-id="bb49b-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="bb49b-156">La première chose à faire est de définir le « squelette » de code de votre application.</span><span class="sxs-lookup"><span data-stu-id="bb49b-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="bb49b-157">Ce code nous demande une clé et un nom de compte de Stockage et utilise ces informations d’identification pour créer un objet `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="bb49b-158">Cet objet est utilisé pour interagir avec notre compte de Stockage dans tous les scénarios de transfert.</span><span class="sxs-lookup"><span data-stu-id="bb49b-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="bb49b-159">Le code nous invite également à choisir le type d’opération de transfert que nous souhaitons exécuter.</span><span class="sxs-lookup"><span data-stu-id="bb49b-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="bb49b-160">Modifiez `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="bb49b-161">Transférer un fichier local dans le Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="bb49b-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="bb49b-162">Ajoutez les méthodes `GetSourcePath` et `GetBlob` à `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="bb49b-163">Modifiez la méthode `TransferLocalFileToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="bb49b-164">Ce code nous demande le chemin d’accès à un fichier local, le nom d’un conteneur nouveau ou existant et le nom d’un nouvel objet blob.</span><span class="sxs-lookup"><span data-stu-id="bb49b-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="bb49b-165">La méthode `TransferManager.UploadAsync` effectue le chargement suivant ces informations.</span><span class="sxs-lookup"><span data-stu-id="bb49b-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="bb49b-166">Appuyez sur `F5` pour exécuter votre application.</span><span class="sxs-lookup"><span data-stu-id="bb49b-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="bb49b-167">Vous pouvez vérifier que le chargement a bien été effectué en affichant votre compte de Stockage avec [l’Explorateur de Stockage Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="bb49b-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="bb49b-168">Définir un nombre d’opérations parallèles</span><span class="sxs-lookup"><span data-stu-id="bb49b-168">Set number of parallel operations</span></span>
<span data-ttu-id="bb49b-169">L’une des fonctionnalités intéressantes offertes par la bibliothèque de déplacement des données consiste à définir le nombre d’opérations parallèles pour augmenter le débit du transfert de données.</span><span class="sxs-lookup"><span data-stu-id="bb49b-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="bb49b-170">Par défaut, la bibliothèque de déplacement des données fixe le nombre d’opérations parallèles à 8 * le nombre de cœurs sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bb49b-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="bb49b-171">Remarque : un grand nombre d’opérations parallèles dans un environnement à faible bande passante peut surcharger la connexion réseau et en réalité entraver le bon déroulement des opérations.</span><span class="sxs-lookup"><span data-stu-id="bb49b-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="bb49b-172">Vous devrez faire des essais avec ce paramètre pour déterminer ce qui fonctionne le mieux en fonction de votre bande passante réseau disponible.</span><span class="sxs-lookup"><span data-stu-id="bb49b-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="bb49b-173">Nous allons ajouter du code pour pouvoir définir le nombre d’opérations parallèles.</span><span class="sxs-lookup"><span data-stu-id="bb49b-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="bb49b-174">Ajoutons du code afin de chronométrer la durée du transfert.</span><span class="sxs-lookup"><span data-stu-id="bb49b-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="bb49b-175">Ajoutez une méthode `SetNumberOfParallelOperations` à `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="bb49b-176">Modifiez la méthode `ExecuteChoice` de sorte qu’elle utilise `SetNumberOfParallelOperations` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="bb49b-177">Modifiez la méthode `TransferLocalFileToAzureBlob` de sorte qu’elle utilise un minuteur :</span><span class="sxs-lookup"><span data-stu-id="bb49b-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="bb49b-178">Suivre la progression des transferts</span><span class="sxs-lookup"><span data-stu-id="bb49b-178">Track transfer progress</span></span>
<span data-ttu-id="bb49b-179">Il est très utile de connaître la durée du transfert des données.</span><span class="sxs-lookup"><span data-stu-id="bb49b-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="bb49b-180">Toutefois, il serait encore mieux de pouvoir voir la progression du transfert *pendant* l’opération de transfert.</span><span class="sxs-lookup"><span data-stu-id="bb49b-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="bb49b-181">Pour appliquer ce scénario, nous devons créer un objet `TransferContext`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="bb49b-182">L’objet `TransferContext` se présente sous deux formes : `SingleTransferContext` et `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="bb49b-183">La première permet de transférer un seul fichier (ce que nous faisons actuellement) et la seconde concerne le transfert d’un répertoire de fichiers (que nous ajouterons plus tard).</span><span class="sxs-lookup"><span data-stu-id="bb49b-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="bb49b-184">Ajoutez les méthodes `GetSingleTransferContext` et `GetDirectoryTransferContext` à `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="bb49b-185">Modifiez la méthode `TransferLocalFileToAzureBlob` de sorte qu’elle utilise `GetSingleTransferContext` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="bb49b-186">Reprendre un transfert annulé</span><span class="sxs-lookup"><span data-stu-id="bb49b-186">Resume a canceled transfer</span></span>
<span data-ttu-id="bb49b-187">Une autre fonctionnalité pratique offerte par la bibliothèque de déplacement des données consiste à pouvoir reprendre un transfert annulé.</span><span class="sxs-lookup"><span data-stu-id="bb49b-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="bb49b-188">Nous allons ajouter du code qui nous permettra d’annuler temporairement le transfert en tapant `c`, puis de le reprendre trois secondes plus tard.</span><span class="sxs-lookup"><span data-stu-id="bb49b-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="bb49b-189">Modifiez `TransferLocalFileToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="bb49b-190">Jusqu'à présent, notre `checkpoint` a toujours eu la valeur `null`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="bb49b-191">Maintenant, si nous annulons le transfert, nous récupérons le dernier point de contrôle de notre transfert, puis nous utilisons ce nouveau point de contrôle dans notre contexte de transfert.</span><span class="sxs-lookup"><span data-stu-id="bb49b-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="bb49b-192">Transférer un répertoire local de transfert dans un répertoire Blob Azure</span><span class="sxs-lookup"><span data-stu-id="bb49b-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="bb49b-193">Il serait décevant que la bibliothèque de déplacement des données ne puisse transférer qu’un fichier à la fois.</span><span class="sxs-lookup"><span data-stu-id="bb49b-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="bb49b-194">Heureusement, ce n’est pas le cas.</span><span class="sxs-lookup"><span data-stu-id="bb49b-194">Luckily, this is not the case.</span></span> <span data-ttu-id="bb49b-195">La bibliothèque de déplacement des données offre la capacité à transférer un répertoire de fichiers et tous ses sous-répertoires.</span><span class="sxs-lookup"><span data-stu-id="bb49b-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="bb49b-196">Nous allons ajouter du code pour pouvoir effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="bb49b-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="bb49b-197">Tout d’abord, ajoutez la méthode `GetBlobDirectory` à `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="bb49b-198">Ensuite, modifiez `TransferLocalDirectoryToAzureBlobDirectory` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="bb49b-199">Il existe quelques différences entre cette méthode et la méthode de chargement d’un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="bb49b-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="bb49b-200">Nous utilisons maintenant `TransferManager.UploadDirectoryAsync` et la méthode `getDirectoryTransferContext` créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="bb49b-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="bb49b-201">En outre, nous fournissons à présent une valeur `options` à notre opération de chargement, ce qui nous permet d’indiquer que nous souhaitons inclure les sous-répertoires à notre chargement.</span><span class="sxs-lookup"><span data-stu-id="bb49b-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="bb49b-202">Copier des fichiers de l’URL vers le Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="bb49b-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="bb49b-203">À présent, nous allons ajouter du code permettant de copier un fichier à partir d’une URL vers un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bb49b-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="bb49b-204">Modifiez `TransferUrlToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="bb49b-205">L’un des cas d’utilisation les plus importants de cette fonctionnalité est le déplacement de données d’un autre service cloud (par exemple, AWS) vers Azure.</span><span class="sxs-lookup"><span data-stu-id="bb49b-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="bb49b-206">Tant que vous disposez d’une URL qui vous permet d’accéder à la ressource, vous pouvez facilement déplacer cette ressource dans des objets blob Azure à l’aide de la méthode `TransferManager.CopyAsync`.</span><span class="sxs-lookup"><span data-stu-id="bb49b-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="bb49b-207">Cette méthode introduit également un nouveau paramètre booléen.</span><span class="sxs-lookup"><span data-stu-id="bb49b-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="bb49b-208">La valeur `true` de ce paramètre indique que nous souhaitons faire une copie asynchrone côté serveur.</span><span class="sxs-lookup"><span data-stu-id="bb49b-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="bb49b-209">La valeur `false` de ce paramètre indique une copie synchrone, ce qui signifie que la ressource est d’abord téléchargée sur notre ordinateur local, puis chargée vers le Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bb49b-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="bb49b-210">Toutefois, la copie synchrone n’est actuellement disponible que pour copier d’une ressource de Stockage Azure vers une autre.</span><span class="sxs-lookup"><span data-stu-id="bb49b-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="bb49b-211">Copier d’un Stockage Blob Azure à un autre</span><span class="sxs-lookup"><span data-stu-id="bb49b-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="bb49b-212">Une autre fonctionnalité offerte uniquement par la bibliothèque de déplacement des données est la capacité à copier d’une ressource de Stockage Azure vers une autre.</span><span class="sxs-lookup"><span data-stu-id="bb49b-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="bb49b-213">Modifiez `TransferAzureBlobToAzureBlob` :</span><span class="sxs-lookup"><span data-stu-id="bb49b-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="bb49b-214">Dans cet exemple, nous donnons la valeur `false` au paramètre booléen `TransferManager.CopyAsync` pour indiquer que nous souhaitons effectuer une copie synchrone.</span><span class="sxs-lookup"><span data-stu-id="bb49b-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="bb49b-215">Cela signifie que la ressource est d’abord téléchargée sur notre ordinateur local, puis chargée vers le Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bb49b-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="bb49b-216">L’option de copie synchrone est un excellent moyen de veiller à ce que l’opération de copie ait une vitesse constante.</span><span class="sxs-lookup"><span data-stu-id="bb49b-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="bb49b-217">À l’inverse, la vitesse de la copie asynchrone côté serveur dépend de la bande passante réseau disponible sur le serveur, qui peut varier.</span><span class="sxs-lookup"><span data-stu-id="bb49b-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="bb49b-218">Toutefois, la copie synchrone peut générer des coûts de sortie supplémentaires par rapport à la copie asynchrone.</span><span class="sxs-lookup"><span data-stu-id="bb49b-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="bb49b-219">L’approche recommandée consiste à utiliser la copie synchrone dans une machine virtuelle Azure qui se trouve dans la même région que votre compte de stockage source afin d’éviter les frais de sortie.</span><span class="sxs-lookup"><span data-stu-id="bb49b-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bb49b-220">Conclusion</span><span class="sxs-lookup"><span data-stu-id="bb49b-220">Conclusion</span></span>
<span data-ttu-id="bb49b-221">Notre application de déplacement des données est à présent terminée.</span><span class="sxs-lookup"><span data-stu-id="bb49b-221">Our data movement application is now complete.</span></span> <span data-ttu-id="bb49b-222">[L’exemple de code complet est disponible sur GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="bb49b-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb49b-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb49b-223">Next steps</span></span>
<span data-ttu-id="bb49b-224">Dans ce guide de prise en main, nous avons créé une application qui interagit avec le Stockage Azure et s’exécute sur Windows, Linux et macOS.</span><span class="sxs-lookup"><span data-stu-id="bb49b-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="bb49b-225">Il se concentre sur le Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="bb49b-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="bb49b-226">Toutefois, ces mêmes connaissances peuvent s’appliquer au Stockage Fichier.</span><span class="sxs-lookup"><span data-stu-id="bb49b-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="bb49b-227">Pour plus d’informations, consultez la [Documentation de référence de la bibliothèque de déplacement des données du Stockage Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="bb49b-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




