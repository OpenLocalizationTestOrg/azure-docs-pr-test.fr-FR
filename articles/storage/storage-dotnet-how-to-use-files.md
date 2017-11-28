---
title: aaaDevelop pour le stockage de fichiers Azure avec .NET | Documents Microsoft
description: "Découvrez comment toodevelop applications et services .NET qui utilisent des fichiers Azure storage toostore fichier de données."
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
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="be32c-103">Développer pour Stockage Fichier Azure avec .NET</span><span class="sxs-lookup"><span data-stu-id="be32c-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="be32c-104">Cet article explique comment toomanage stockage Azure files avec le code .NET.</span><span class="sxs-lookup"><span data-stu-id="be32c-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="be32c-105">toolearn en savoir plus sur le stockage de fichiers Azure, consultez hello [Introduction tooAzure stockage de fichiers](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be32c-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="be32c-106">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="be32c-106">About this tutorial</span></span>
<span data-ttu-id="be32c-107">Ce didacticiel va vous montrer des bases de hello de l’utilisation des applications de toodevelop .NET ou les services qui utilisent des données de fichier toostore fichier Azure storage.</span><span class="sxs-lookup"><span data-stu-id="be32c-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="be32c-108">Dans ce didacticiel, nous crée une application console simple et montrent comment tooperform les actions de base avec un stockage .NET et des fichiers Azure :</span><span class="sxs-lookup"><span data-stu-id="be32c-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="be32c-109">Obtenir le contenu de hello d’un fichier</span><span class="sxs-lookup"><span data-stu-id="be32c-109">Get hello contents of a file</span></span>
* <span data-ttu-id="be32c-110">Définir le quota hello (taille maximale) pour le partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="be32c-111">Créer une signature d’accès partagé (clé SAS) pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="be32c-112">Copier un fichier tooanother Bonjour même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="be32c-113">Copier un objet blob de fichier tooa Bonjour même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="be32c-114">Utiliser Azure Storage Metrics pour la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="be32c-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="be32c-115">Stockage de fichiers Azure sont accessibles sur SMB, il est possible toowrite applications simples qui accéder au partage de fichiers Azure hello à l’aide de classes de System.IO hello standard d’e/s de fichier.</span><span class="sxs-lookup"><span data-stu-id="be32c-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="be32c-116">Cet article décrit comment toowrite les applications qui utilisent hello Azure stockage .NET SDK, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="be32c-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="be32c-117">Créer l’application de console hello et obtenir l’assembly hello</span><span class="sxs-lookup"><span data-stu-id="be32c-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="be32c-118">Dans Visual Studio, créez une application de console Windows.</span><span class="sxs-lookup"><span data-stu-id="be32c-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="be32c-119">Hello suit vous montre comment toocreate une application de console dans Visual Studio 2017, toutefois, les étapes de hello sont similaires dans les autres versions de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be32c-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="be32c-120">Sélectionnez **Fichier** > **Nouveau** > **Projet**</span><span class="sxs-lookup"><span data-stu-id="be32c-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="be32c-121">Sélectionnez **Installé** > **Modèles** > **Visual C#** > **Bureau classique Windows**</span><span class="sxs-lookup"><span data-stu-id="be32c-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="be32c-122">Sélectionnez **Application console (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="be32c-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="be32c-123">Entrez un nom pour votre application dans hello **nom :** champ</span><span class="sxs-lookup"><span data-stu-id="be32c-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="be32c-124">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="be32c-124">Select **OK**</span></span>

<span data-ttu-id="be32c-125">Tous les exemples de code dans ce didacticiel peuvent être ajoutés toohello `Main()` méthode de votre application de console `Program.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="be32c-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="be32c-126">Vous pouvez utiliser hello bibliothèque cliente de stockage Azure dans n’importe quel type d’application .NET, y compris une application web ou de service cloud Azure et les applications de bureau et mobiles.</span><span class="sxs-lookup"><span data-stu-id="be32c-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="be32c-127">Dans ce guide, nous utilisons une application console pour plus de simplicité.</span><span class="sxs-lookup"><span data-stu-id="be32c-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="be32c-128">Utiliser les packages NuGet tooinstall hello requis</span><span class="sxs-lookup"><span data-stu-id="be32c-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="be32c-129">Il existe deux packages, vous devez tooreference dans votre projet toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="be32c-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="be32c-130">[Bibliothèque cliente Microsoft Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ce package fournit un accès par programmation toodata des ressources dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="be32c-131">[Bibliothèque Microsoft Azure Configuration Manager pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) : ce package fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration, quel que soit l’emplacement d’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="be32c-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="be32c-132">Vous pouvez utiliser NuGet tooobtain les deux packages.</span><span class="sxs-lookup"><span data-stu-id="be32c-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="be32c-133">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="be32c-133">Follow these steps:</span></span>

1. <span data-ttu-id="be32c-134">Cliquez avec le bouton droit sur votre projet dans **l’Explorateur de solutions**, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="be32c-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="be32c-135">Rechercher en ligne du terme « WindowsAzure.Storage » et cliquez sur **installer** tooinstall hello bibliothèque cliente de stockage et de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="be32c-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="be32c-136">Rechercher en ligne « WindowsAzure.ConfigurationManager » et cliquez sur **installer** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="be32c-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="be32c-137">Enregistrez votre fichier app.config toohello d’informations d’identification de compte stockage</span><span class="sxs-lookup"><span data-stu-id="be32c-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="be32c-138">Enregistrez ensuite vos informations d’identification dans le fichier app.config du projet.</span><span class="sxs-lookup"><span data-stu-id="be32c-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="be32c-139">Modifier le fichier app.config de hello afin qu’il apparaisse toohello similaire, l’exemple suivant, en remplaçant `myaccount` avec le nom de votre compte de stockage, et `mykey` avec votre clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> version la plus récente de l’émulateur de stockage Azure hello Hello ne prend pas en charge le stockage Azure. <span data-ttu-id="be32c-141">Votre chaîne de connexion doit cibler un compte Azure Storage dans hello cloud toowork avec le stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="be32c-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="be32c-142">Ajouter des directives d’utilisation</span><span class="sxs-lookup"><span data-stu-id="be32c-142">Add using directives</span></span>
<span data-ttu-id="be32c-143">Ouvrez hello `Program.cs` à partir de l’Explorateur de solutions et ajoutez hello qui suit à l’aide de top toohello de directives de fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="be32c-144">Un partage de fichiers de hello d’accès par programmation</span><span class="sxs-lookup"><span data-stu-id="be32c-144">Access hello file share programmatically</span></span>
<span data-ttu-id="be32c-145">Ensuite, ajoutez hello suivant code toohello `Main()` chaîne de connexion de hello tooretrieve (méthode) (après le code hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="be32c-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="be32c-146">Ce code obtient un fichier de toohello référence créée précédemment et renvoie sa fenêtre de console toohello contenu.</span><span class="sxs-lookup"><span data-stu-id="be32c-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="be32c-147">Exécutez la sortie de hello hello toosee de l’application console.</span><span class="sxs-lookup"><span data-stu-id="be32c-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="be32c-148">Taille maximale du jeu hello pour un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="be32c-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="be32c-149">Depuis la version 5.x de hello bibliothèque cliente de stockage Azure, vous pouvez définir ensemble hello quota (ou taille maximale) pour un partage de fichiers, en gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="be32c-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="be32c-150">Vous pouvez également vérifier toosee la quantité de données est actuellement stocké sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="be32c-151">En définissant le quota de hello pour un partage, vous pouvez limiter la taille totale de hello hello les fichiers stockés sur le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="be32c-152">Si hello la taille totale des fichiers sur le partage de hello dépasse quota de hello défini sur le partage de hello, les clients seront taille de hello tooincrease impossible des fichiers existants ou créer de nouveaux fichiers, à moins que ces fichiers sont vides.</span><span class="sxs-lookup"><span data-stu-id="be32c-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="be32c-153">exemple Hello ci-dessous montre comment toocheck hello en cours d’utilisation pour un partage et comment tooset hello quota pour le partage de hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="be32c-154">Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="be32c-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="be32c-155">Depuis la version 5.x de hello bibliothèque cliente de stockage Azure, vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier.</span><span class="sxs-lookup"><span data-stu-id="be32c-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="be32c-156">Vous pouvez également créer une stratégie d’accès partagé sur un toomanage partagé accès au partage de fichier signatures.</span><span class="sxs-lookup"><span data-stu-id="be32c-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="be32c-157">Création d’une stratégie d’accès partagé est recommandée, car elle fournit un moyen de révocation hello SAS si elle doit être compromise.</span><span class="sxs-lookup"><span data-stu-id="be32c-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="be32c-158">Bonjour à l’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise que tooprovide hello les contraintes de stratégie pour une SAP sur un fichier dans hello partagent.</span><span class="sxs-lookup"><span data-stu-id="be32c-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="be32c-159">Pour plus d’informations sur la création et l’utilisation de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) et [Créer et utiliser une signature d’accès partagé avec des blobs Azure](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="be32c-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="be32c-160">Copie des fichiers</span><span class="sxs-lookup"><span data-stu-id="be32c-160">Copy files</span></span>
<span data-ttu-id="be32c-161">Depuis la version 5.x de hello bibliothèque cliente de stockage Azure, vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="be32c-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="be32c-162">Dans les sections suivantes hello, nous allons montrer comment tooperform ces copier les opérations par programme.</span><span class="sxs-lookup"><span data-stu-id="be32c-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="be32c-163">Vous pouvez également utiliser AzCopy toocopy un fichier tooanother ou toocopy un objet blob tooa fichier et inversement.</span><span class="sxs-lookup"><span data-stu-id="be32c-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="be32c-164">Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="be32c-164">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="be32c-165">Si vous copiez un fichier de tooa blob ou d’un objet blob tooa de fichier, vous devez utiliser un objet de source accès partagé (SAS) de signature tooauthenticate hello, même si vous copiez dans hello même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="be32c-166">**Copier un fichier tooanother** hello exemple suivant copie un fichier tooanother Bonjour même partage.</span><span class="sxs-lookup"><span data-stu-id="be32c-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="be32c-167">Étant donné que cette opération de copie entre les fichiers dans hello même compte de stockage, vous pouvez utiliser la copie de la clé partagée d’authentification tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="be32c-168">**Copier un objet blob tooa de fichier** hello exemple suivant crée un fichier et le copie blob tooa dans hello même compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="be32c-169">exemple de Hello crée un SAS pour le fichier de source de hello, quel service hello utilise le fichier de source toohello tooauthenticate accès pendant l’opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="be32c-170">Vous pouvez copier un fichier de tooa blob Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="be32c-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="be32c-171">Si l’objet de source de hello est un objet blob, vous devez ensuite créer un objet blob SAS tooauthenticate accès toothat au cours de l’opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="be32c-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="be32c-172">Résolution des problèmes Stockage Fichier Azure à l’aide de métriques</span><span class="sxs-lookup"><span data-stu-id="be32c-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="be32c-173">Azure Storage Analytics prend à présent en charge les métriques pour Stockage Fichier Azure.</span><span class="sxs-lookup"><span data-stu-id="be32c-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="be32c-174">Avec les données de métriques, vous pouvez suivre les demandes et diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="be32c-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="be32c-175">Vous pouvez activer les métriques pour le stockage de fichiers Azure à partir de hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="be32c-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="be32c-176">Vous pouvez également activer les métriques par programme en appelant hello opération de définition des propriétés de Service fichier via l’API REST de hello, ou l’un de ses analogues Bonjour bibliothèque cliente de stockage.</span><span class="sxs-lookup"><span data-stu-id="be32c-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="be32c-177">Hello, exemple de code suivant montre comment toouse hello bibliothèque cliente de stockage pour les métriques de tooenable .NET pour le stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="be32c-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="be32c-178">Tout d’abord, ajoutez hello qui suit `using` directives tooyour `Program.cs` un fichier, en outre toothose que vous avez ajouté ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="be32c-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="be32c-179">Notez que, pendant que les objets BLOB Azure, la Table de Azure et files d’attente Azure, utilisez hello partagé `ServiceProperties` type Bonjour `Microsoft.WindowsAzure.Storage.Shared.Protocol` espace de noms, stockage de fichier Azure utilise son propre type, hello `FileServiceProperties` type Bonjour `Microsoft.WindowsAzure.Storage.File.Protocol` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="be32c-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="be32c-180">Les deux espaces de noms doivent être référencées à partir de votre code, toutefois, pour hello suivant toocompile de code.</span><span class="sxs-lookup"><span data-stu-id="be32c-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read hello metrics properties we just set.
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

<span data-ttu-id="be32c-181">En outre, vous pouvez faire référence trop[le stockage de fichiers Azure Article de résolution des problèmes](storage-troubleshoot-file-connection-problems.md) de bout en bout des conseils de dépannage.</span><span class="sxs-lookup"><span data-stu-id="be32c-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be32c-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be32c-182">Next steps</span></span>
<span data-ttu-id="be32c-183">Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.</span><span class="sxs-lookup"><span data-stu-id="be32c-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="be32c-184">Vidéos et articles conceptuels</span><span class="sxs-lookup"><span data-stu-id="be32c-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="be32c-185">Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux</span><span class="sxs-lookup"><span data-stu-id="be32c-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="be32c-186">Comment toouse stockage Azure files avec Linux</span><span class="sxs-lookup"><span data-stu-id="be32c-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="be32c-187">Outils pris en charge pour le stockage de fichiers</span><span class="sxs-lookup"><span data-stu-id="be32c-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="be32c-188">Utilisation d'Azure PowerShell avec Azure Storage</span><span class="sxs-lookup"><span data-stu-id="be32c-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="be32c-189">Comment toouse AzCopy avec Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="be32c-189">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="be32c-190">À l’aide de hello CLI d’Azure avec le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="be32c-190">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="be32c-191">Résolution des problèmes de stockage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="be32c-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="be32c-192">Référence</span><span class="sxs-lookup"><span data-stu-id="be32c-192">Reference</span></span>
* [<span data-ttu-id="be32c-193">Référence de la bibliothèque cliente de stockage pour .NET</span><span class="sxs-lookup"><span data-stu-id="be32c-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="be32c-194">Référence de l’API REST du service de fichiers</span><span class="sxs-lookup"><span data-stu-id="be32c-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="be32c-195">Billets de blog :</span><span class="sxs-lookup"><span data-stu-id="be32c-195">Blog posts</span></span>
* [<span data-ttu-id="be32c-196">Le stockage de fichiers Azure est désormais mis à la disposition générale</span><span class="sxs-lookup"><span data-stu-id="be32c-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="be32c-197">Dans le Stockage Fichier Azure</span><span class="sxs-lookup"><span data-stu-id="be32c-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="be32c-198">Présentation de Microsoft Azure File Service</span><span class="sxs-lookup"><span data-stu-id="be32c-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="be32c-199">TooMicrosoft connexions persistantes stockage Azure</span><span class="sxs-lookup"><span data-stu-id="be32c-199">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
