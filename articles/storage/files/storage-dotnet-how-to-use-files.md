---
title: "Développer pour Stockage Fichier Azure avec .NET | Microsoft Docs"
description: "Apprenez à développer des services et applications .NET qui utilisent Stockage Fichier Azure pour stocker les données de fichiers."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 7b94e70619324bb8dc8e7f8306f00f06e7476c1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="2f96e-103">Développer pour Stockage Fichier Azure avec .NET</span><span class="sxs-lookup"><span data-stu-id="2f96e-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="2f96e-104">Cet article explique comment gérer le stockage Fichier Azure avec du code .NET.</span><span class="sxs-lookup"><span data-stu-id="2f96e-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="2f96e-105">Pour en savoir plus sur Stockage Fichier Azure, consultez [Introduction à Stockage Fichier Azure](storage-files-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="2f96e-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="2f96e-106">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="2f96e-106">About this tutorial</span></span>
<span data-ttu-id="2f96e-107">Ce tutoriel vous montre les principes fondamentaux de l’utilisation de .NET pour développer des applications ou services qui utilisent Stockage Fichier Azure pour stocker les données de fichiers.</span><span class="sxs-lookup"><span data-stu-id="2f96e-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="2f96e-108">Dans ce tutoriel, vous allez créer une application console simple et effectuer des actions de base avec .NET et Stockage Fichier Azure :</span><span class="sxs-lookup"><span data-stu-id="2f96e-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="2f96e-109">Obtenir le contenu d’un fichier</span><span class="sxs-lookup"><span data-stu-id="2f96e-109">Get the contents of a file</span></span>
* <span data-ttu-id="2f96e-110">Définir le quota (taille maximale) pour le partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="2f96e-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="2f96e-111">Créer une signature d’accès partagé pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage</span><span class="sxs-lookup"><span data-stu-id="2f96e-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="2f96e-112">Copier un fichier dans un autre fichier au sein du même compte de stockage</span><span class="sxs-lookup"><span data-stu-id="2f96e-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="2f96e-113">Copier un fichier dans un objet blob au sein du même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="2f96e-114">Utiliser Azure Storage Metrics pour la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="2f96e-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="2f96e-115">Étant donné que Stockage Fichier Azure est accessible sur SMB, il est possible d’écrire de simples applications qui accèdent au partage de fichiers Azure à l’aide des classes System.IO standard pour les E/S de fichier.</span><span class="sxs-lookup"><span data-stu-id="2f96e-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="2f96e-116">Cet article indique comment écrire des applications qui utilisent le SDK .NET Stockage Azure, lequel utilise l’[API REST Stockage Fichier Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) pour communiquer avec Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="2f96e-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="2f96e-117">Création de l’application console et obtention de l’assembly</span><span class="sxs-lookup"><span data-stu-id="2f96e-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="2f96e-118">Dans Visual Studio, créez une application de console Windows.</span><span class="sxs-lookup"><span data-stu-id="2f96e-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="2f96e-119">Les étapes suivantes vous montrent comment créer une application de console dans Visual Studio 2017. Les étapes sont similaires à celles des autres versions de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f96e-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="2f96e-120">Sélectionnez **Fichier** > **Nouveau** > **Projet**</span><span class="sxs-lookup"><span data-stu-id="2f96e-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="2f96e-121">Sélectionnez **Installé** > **Modèles** > **Visual C#** > **Bureau classique Windows**</span><span class="sxs-lookup"><span data-stu-id="2f96e-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="2f96e-122">Sélectionnez **Application console (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="2f96e-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="2f96e-123">Entrez un nom pour votre application dans le champ **Nom :**</span><span class="sxs-lookup"><span data-stu-id="2f96e-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="2f96e-124">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f96e-124">Select **OK**</span></span>

<span data-ttu-id="2f96e-125">Tous les exemples de code figurant dans ce didacticiel peuvent être ajoutés à la méthode `Main()` du fichier `Program.cs` de votre application de console.</span><span class="sxs-lookup"><span data-stu-id="2f96e-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="2f96e-126">Vous pouvez utiliser la bibliothèque cliente d’Azure Storage dans n’importe quelle application .NET, y compris un service cloud Azure, une application web, une application de bureau ou une application mobile.</span><span class="sxs-lookup"><span data-stu-id="2f96e-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="2f96e-127">Dans ce guide, nous utilisons une application console pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="2f96e-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="2f96e-128">Utiliser NuGet pour installer les packages requis</span><span class="sxs-lookup"><span data-stu-id="2f96e-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="2f96e-129">Vous devez référencer deux packages dans votre projet pour terminer ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="2f96e-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="2f96e-130">[Bibliothèque cliente Microsoft Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ce package fournit un accès par programme aux ressources de données dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="2f96e-131">[Bibliothèque Microsoft Azure Configuration Manager pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) : ce package fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration, quel que soit l’emplacement d’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="2f96e-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="2f96e-132">Vous pouvez utiliser NuGet pour obtenir ces deux packages.</span><span class="sxs-lookup"><span data-stu-id="2f96e-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="2f96e-133">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f96e-133">Follow these steps:</span></span>

1. <span data-ttu-id="2f96e-134">Cliquez avec le bouton droit sur votre projet dans **l’Explorateur de solutions**, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2f96e-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="2f96e-135">Recherchez « WindowsAzure.Storage » en ligne, puis cliquez sur **Installer** pour installer la bibliothèque cliente Azure Storage et ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="2f96e-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="2f96e-136">Recherchez « WindowsAzure.ConfigurationManager » en ligne, puis cliquez sur **Installer** pour installer Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="2f96e-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="2f96e-137">Enregistrement des informations d’identification de votre compte de stockage dans le fichier app.config</span><span class="sxs-lookup"><span data-stu-id="2f96e-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="2f96e-138">Enregistrez ensuite vos informations d’identification dans le fichier app.config du projet.</span><span class="sxs-lookup"><span data-stu-id="2f96e-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="2f96e-139">Modifiez le fichier app.config de façon à ce qu’il soit similaire à l’exemple ci-après, en remplaçant `myaccount` par le nom de votre compte de stockage et `mykey` par la clé de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> La dernière version de l’émulateur de stockage Azure ne prend pas en charge Stockage Fichier Azure. <span data-ttu-id="2f96e-141">Votre chaîne de connexion doit cibler un compte de stockage Azure dans le cloud pour fonctionner avec Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="2f96e-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="2f96e-142">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="2f96e-142">Add using directives</span></span>
<span data-ttu-id="2f96e-143">Ouvrez le fichier `Program.cs` à partir de l’Explorateur de solutions. puis ajoutez les directives d’utilisation suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="2f96e-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="2f96e-144">Accès au partage de fichiers par programmation</span><span class="sxs-lookup"><span data-stu-id="2f96e-144">Access the file share programmatically</span></span>
<span data-ttu-id="2f96e-145">Ajoutez ensuite le code suivant à la méthode `Main()` (après le code montré ci-dessus) pour récupérer la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="2f96e-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="2f96e-146">Ce code obtient une référence vers le fichier créé plus tôt et renvoie son contenu dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="2f96e-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="2f96e-147">Exécutez l’application console pour voir le résultat.</span><span class="sxs-lookup"><span data-stu-id="2f96e-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="2f96e-148">Définition de la taille maximale d’un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="2f96e-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="2f96e-149">Depuis la version 5.x de la bibliothèque cliente Azure Storage, vous pouvez définir le quota (ou la taille maximale) pour un partage de fichier, en gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="2f96e-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="2f96e-150">Vous pouvez également vérifier la quantité de données actuellement stockée sur le partage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="2f96e-151">En définissant le quota pour un partage, vous pouvez limiter la taille totale des fichiers stockés sur ce partage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="2f96e-152">Si la taille totale des fichiers sur le partage dépasse le quota défini sur celui-ci, les clients ne peuvent pas augmenter la taille des fichiers existants ou créer des fichiers, sauf si ces fichiers sont vides.</span><span class="sxs-lookup"><span data-stu-id="2f96e-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="2f96e-153">L’exemple ci-dessous illustre comment vérifier l’utilisation actuelle pour un partage et comment définir le quota pour le partage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="2f96e-154">Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="2f96e-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="2f96e-155">Depuis la version 5.x de la bibliothèque cliente Azure Storage, vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier individuel.</span><span class="sxs-lookup"><span data-stu-id="2f96e-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="2f96e-156">Vous pouvez également créer une stratégie d’accès partagé sur un partage de fichiers pour gérer les signatures d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="2f96e-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="2f96e-157">Créer une stratégie d’accès partagé est recommandé, car cette opération permet de révoquer la SAP si elle doit être compromise.</span><span class="sxs-lookup"><span data-stu-id="2f96e-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="2f96e-158">L’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise cette stratégie pour fournir les contraintes pour une SAP sur un fichier du partage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="2f96e-159">Pour plus d’informations sur la création et l’utilisation de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) et [Créer et utiliser une signature d’accès partagé avec des blobs Azure](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="2f96e-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="2f96e-160">Copie des fichiers</span><span class="sxs-lookup"><span data-stu-id="2f96e-160">Copy files</span></span>
<span data-ttu-id="2f96e-161">Depuis la version 5.x de la bibliothèque cliente Azure Storage, vous pouvez copier un fichier dans un autre fichier, un fichier dans un objet blob ou un objet blob dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="2f96e-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="2f96e-162">Dans les sections suivantes, nous montrons comment effectuer ces opérations de copie par programmation.</span><span class="sxs-lookup"><span data-stu-id="2f96e-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="2f96e-163">Vous pouvez également utiliser AzCopy pour copier un fichier dans un autre ou pour copier un objet blob dans un fichier ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="2f96e-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="2f96e-164">Consultez l’article [Transfert de données avec l’utilitaire de ligne de commande AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f96e-164">See [Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="2f96e-165">Si vous copiez un objet blob dans un fichier ou un fichier dans un objet blob, vous devez utiliser une signature d’accès partagé (SAP) pour authentifier l’objet source, même si vous effectuez la copie dans le même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="2f96e-166">**Copier un fichier vers un autre** L’exemple suivant copie un fichier dans un autre fichier au sein du même partage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="2f96e-167">Étant donné que cette opération de copie a lieu entre des fichiers du même compte de stockage, vous pouvez utiliser l’authentification Clé partagée pour l’effectuer.</span><span class="sxs-lookup"><span data-stu-id="2f96e-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="2f96e-168">**Copier un fichier vers un blob** L’exemple ci-dessous crée un fichier et le copie dans un blob au sein du même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="2f96e-169">L’exemple crée une SAP pour le fichier source, que le service utilise pour authentifier l’accès au fichier source pendant l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="2f96e-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="2f96e-170">Vous pouvez copier un objet blob dans un fichier de la même façon.</span><span class="sxs-lookup"><span data-stu-id="2f96e-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="2f96e-171">Si l’objet source est un objet blob, créez une SAP pour authentifier l’accès à cet objet blob pendant l’opération de copie.</span><span class="sxs-lookup"><span data-stu-id="2f96e-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="2f96e-172">Résolution des problèmes Stockage Fichier Azure à l’aide de métriques</span><span class="sxs-lookup"><span data-stu-id="2f96e-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="2f96e-173">Azure Storage Analytics prend à présent en charge les métriques pour Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="2f96e-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="2f96e-174">Avec les données de métriques, vous pouvez suivre les demandes et diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="2f96e-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="2f96e-175">Vous pouvez activer les métriques pour Stockage Fichier Azure par le biais du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f96e-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="2f96e-176">Vous pouvez également activer les métriques par programmation en appelant l’opération de définition des propriétés du service de fichiers via l’API REST ou l’un de ses analogues dans la bibliothèque cliente de stockage.</span><span class="sxs-lookup"><span data-stu-id="2f96e-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="2f96e-177">L’exemple de code suivant explique comment utiliser la bibliothèque cliente Stockage Azure pour .NET afin d’activer les métriques Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="2f96e-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="2f96e-178">Commencez par ajouter les directives `using` suivantes à votre fichier `Program.cs`, en plus de celles que vous avez ajoutées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="2f96e-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="2f96e-179">Bien que les services Blob, Table et File d’attente Azure utilisent le type `ServiceProperties` partagé dans l’espace de noms `Microsoft.WindowsAzure.Storage.Shared.Protocol`, Stockage Fichier Azure utilise son propre type (`FileServiceProperties`) dans l’espace de noms `Microsoft.WindowsAzure.Storage.File.Protocol`.</span><span class="sxs-lookup"><span data-stu-id="2f96e-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="2f96e-180">Pour pouvoir compiler le code suivant, vous devez cependant référencer les deux espaces de noms à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="2f96e-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read the metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="2f96e-181">Vous pouvez également vous référer à [l’article Résolution des problèmes relatifs à Stockage Fichier Azure](storage-troubleshoot-windows-file-connection-problems.md) pour obtenir une aide de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="2f96e-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f96e-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f96e-182">Next steps</span></span>
<span data-ttu-id="2f96e-183">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="2f96e-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="2f96e-184">Vidéos et articles conceptuels</span><span class="sxs-lookup"><span data-stu-id="2f96e-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="2f96e-185">Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="2f96e-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="2f96e-186">Utilisation de Stockage Fichier Azure avec Linux</span><span class="sxs-lookup"><span data-stu-id="2f96e-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="2f96e-187">Outils pris en charge pour le stockage de fichiers</span><span class="sxs-lookup"><span data-stu-id="2f96e-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="2f96e-188">Utilisation de AzCopy avec Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2f96e-188">How to use AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="2f96e-189">Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2f96e-189">Using the Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="2f96e-190">Résolution des problèmes de stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="2f96e-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="2f96e-191">Référence</span><span class="sxs-lookup"><span data-stu-id="2f96e-191">Reference</span></span>
* [<span data-ttu-id="2f96e-192">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="2f96e-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="2f96e-193">Référence de l’API REST du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="2f96e-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="2f96e-194">Billets de blog :</span><span class="sxs-lookup"><span data-stu-id="2f96e-194">Blog posts</span></span>
* [<span data-ttu-id="2f96e-195">Le stockage de fichiers Azure est désormais mis à la disposition générale</span><span class="sxs-lookup"><span data-stu-id="2f96e-195">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="2f96e-196">Dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="2f96e-196">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="2f96e-197">Présentation de Microsoft Azure File Service</span><span class="sxs-lookup"><span data-stu-id="2f96e-197">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* <span data-ttu-id="2f96e-198">[Persisting connections to Microsoft Azure File storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx) (Conservation des connexions vers Stockage Fichier Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="2f96e-198">[Persisting connections to Microsoft Azure File storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)</span></span>