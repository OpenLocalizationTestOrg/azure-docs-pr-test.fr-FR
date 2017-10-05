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
ms.openlocfilehash: e26da88ef1803d47d7286c5ae836ac9c041dadd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>Développer pour Stockage Fichier Azure avec .NET 
> [!NOTE]
> Cet article explique comment gérer le stockage Fichier Azure avec du code .NET. Pour en savoir plus sur Stockage Fichier Azure, consultez [Introduction à Stockage Fichier Azure](storage-files-introduction.md) .
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce tutoriel vous montre les principes fondamentaux de l’utilisation de .NET pour développer des applications ou services qui utilisent Stockage Fichier Azure pour stocker les données de fichiers. Dans ce tutoriel, vous allez créer une application console simple et effectuer des actions de base avec .NET et Stockage Fichier Azure :

* Obtenir le contenu d’un fichier
* Définir le quota (taille maximale) pour le partage de fichiers
* Créer une signature d’accès partagé pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage
* Copier un fichier dans un autre fichier au sein du même compte de stockage
* Copier un fichier dans un objet blob au sein du même compte de stockage.
* Utiliser Azure Storage Metrics pour la résolution des problèmes.

> [!Note]  
> Étant donné que Stockage Fichier Azure est accessible sur SMB, il est possible d’écrire de simples applications qui accèdent au partage de fichiers Azure à l’aide des classes System.IO standard pour les E/S de fichier. Cet article indique comment écrire des applications qui utilisent le SDK .NET Stockage Azure, lequel utilise l’[API REST Stockage Fichier Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) pour communiquer avec Stockage Fichier Azure. 


## <a name="create-the-console-application-and-obtain-the-assembly"></a>Création de l’application console et obtention de l’assembly
Dans Visual Studio, créez une application de console Windows. Les étapes suivantes vous montrent comment créer une application de console dans Visual Studio 2017. Les étapes sont similaires à celles des autres versions de Visual Studio.

1. Sélectionnez **Fichier** > **Nouveau** > **Projet**
2. Sélectionnez **Installé** > **Modèles** > **Visual C#** > **Bureau classique Windows**
3. Sélectionnez **Application console (.NET Framework)**
4. Entrez un nom pour votre application dans le champ **Nom :**
5. Sélectionnez **OK**.

Tous les exemples de code figurant dans ce didacticiel peuvent être ajoutés à la méthode `Main()` du fichier `Program.cs` de votre application de console.

Vous pouvez utiliser la bibliothèque cliente d’Azure Storage dans n’importe quelle application .NET, y compris un service cloud Azure, une application web, une application de bureau ou une application mobile. Dans ce guide, nous utilisons une application console pour plus de simplicité.

## <a name="use-nuget-to-install-the-required-packages"></a>Utiliser NuGet pour installer les packages requis
Vous devez référencer deux packages dans votre projet pour terminer ce didacticiel :

* [Bibliothèque cliente Microsoft Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ce package fournit un accès par programme aux ressources de données dans votre compte de stockage.
* [Bibliothèque Microsoft Azure Configuration Manager pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) : ce package fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration, quel que soit l’emplacement d’exécution de votre application.

Vous pouvez utiliser NuGet pour obtenir ces deux packages. Procédez comme suit :

1. Cliquez avec le bouton droit sur votre projet dans **l’Explorateur de solutions**, puis sélectionnez **Gérer les packages NuGet**.
2. Recherchez « WindowsAzure.Storage » en ligne, puis cliquez sur **Installer** pour installer la bibliothèque cliente Azure Storage et ses dépendances.
3. Recherchez « WindowsAzure.ConfigurationManager » en ligne, puis cliquez sur **Installer** pour installer Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a>Enregistrement des informations d’identification de votre compte de stockage dans le fichier app.config
Enregistrez ensuite vos informations d’identification dans le fichier app.config du projet. Modifiez le fichier app.config de façon à ce qu’il soit similaire à l’exemple ci-après, en remplaçant `myaccount` par le nom de votre compte de stockage et `mykey` par la clé de votre compte de stockage.

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
> La dernière version de l’émulateur de stockage Azure ne prend pas en charge Stockage Fichier Azure. Votre chaîne de connexion doit cibler un compte de stockage Azure dans le cloud pour fonctionner avec Stockage Fichier Azure.

## <a name="add-using-directives"></a>Ajouter des directives d’utilisation
Ouvrez le fichier `Program.cs` à partir de l’Explorateur de solutions. puis ajoutez les directives d’utilisation suivantes en haut du fichier.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a>Accès au partage de fichiers par programmation
Ajoutez ensuite le code suivant à la méthode `Main()` (après le code montré ci-dessus) pour récupérer la chaîne de connexion. Ce code obtient une référence vers le fichier créé plus tôt et renvoie son contenu dans la fenêtre de console.

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

Exécutez l’application console pour voir le résultat.

## <a name="set-the-maximum-size-for-a-file-share"></a>Définition de la taille maximale d’un partage de fichiers
Depuis la version 5.x de la bibliothèque cliente Azure Storage, vous pouvez définir le quota (ou la taille maximale) pour un partage de fichier, en gigaoctets. Vous pouvez également vérifier la quantité de données actuellement stockée sur le partage.

En définissant le quota pour un partage, vous pouvez limiter la taille totale des fichiers stockés sur ce partage. Si la taille totale des fichiers sur le partage dépasse le quota défini sur celui-ci, les clients ne peuvent pas augmenter la taille des fichiers existants ou créer des fichiers, sauf si ces fichiers sont vides.

L’exemple ci-dessous illustre comment vérifier l’utilisation actuelle pour un partage et comment définir le quota pour le partage.

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers
Depuis la version 5.x de la bibliothèque cliente Azure Storage, vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier individuel. Vous pouvez également créer une stratégie d’accès partagé sur un partage de fichiers pour gérer les signatures d’accès partagé. Créer une stratégie d’accès partagé est recommandé, car cette opération permet de révoquer la SAP si elle doit être compromise.

L’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise cette stratégie pour fournir les contraintes pour une SAP sur un fichier du partage.

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

Pour plus d’informations sur la création et l’utilisation de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) et [Créer et utiliser une signature d’accès partagé avec des blobs Azure](storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Copie des fichiers
Depuis la version 5.x de la bibliothèque cliente Azure Storage, vous pouvez copier un fichier dans un autre fichier, un fichier dans un objet blob ou un objet blob dans un fichier. Dans les sections suivantes, nous montrons comment effectuer ces opérations de copie par programmation.

Vous pouvez également utiliser AzCopy pour copier un fichier dans un autre ou pour copier un objet blob dans un fichier ou vice versa. Consultez l’article [Transfert de données avec l’utilitaire de ligne de commande AzCopy](storage-use-azcopy.md).

> [!NOTE]
> Si vous copiez un objet blob dans un fichier ou un fichier dans un objet blob, vous devez utiliser une signature d’accès partagé (SAP) pour authentifier l’objet source, même si vous effectuez la copie dans le même compte de stockage.
> 
> 

**Copier un fichier vers un autre** L’exemple suivant copie un fichier dans un autre fichier au sein du même partage. Étant donné que cette opération de copie a lieu entre des fichiers du même compte de stockage, vous pouvez utiliser l’authentification Clé partagée pour l’effectuer.

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

**Copier un fichier vers un blob** L’exemple ci-dessous crée un fichier et le copie dans un blob au sein du même compte de stockage. L’exemple crée une SAP pour le fichier source, que le service utilise pour authentifier l’accès au fichier source pendant l’opération de copie.

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

Vous pouvez copier un objet blob dans un fichier de la même façon. Si l’objet source est un objet blob, créez une SAP pour authentifier l’accès à cet objet blob pendant l’opération de copie.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Résolution des problèmes Stockage Fichier Azure à l’aide de métriques
Azure Storage Analytics prend à présent en charge les métriques pour Stockage Fichier Azure. Avec les données de métriques, vous pouvez suivre les demandes et diagnostiquer les problèmes.


Vous pouvez activer les métriques pour Stockage Fichier Azure par le biais du [portail Azure](https://portal.azure.com). Vous pouvez également activer les métriques par programmation en appelant l’opération de définition des propriétés du service de fichiers via l’API REST ou l’un de ses analogues dans la bibliothèque cliente de stockage.


L’exemple de code suivant explique comment utiliser la bibliothèque cliente Stockage Azure pour .NET afin d’activer les métriques Stockage Fichier Azure.

Commencez par ajouter les directives `using` suivantes à votre fichier `Program.cs`, en plus de celles que vous avez ajoutées ci-dessus :

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Bien que les services Blob, Table et File d’attente Azure utilisent le type `ServiceProperties` partagé dans l’espace de noms `Microsoft.WindowsAzure.Storage.Shared.Protocol`, Stockage Fichier Azure utilise son propre type (`FileServiceProperties`) dans l’espace de noms `Microsoft.WindowsAzure.Storage.File.Protocol`. Pour pouvoir compiler le code suivant, vous devez cependant référencer les deux espaces de noms à partir de votre code.

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

Vous pouvez également vous référer à [l’article Résolution des problèmes relatifs à Stockage Fichier Azure](storage-troubleshoot-file-connection-problems.md) pour obtenir une aide de bout en bout.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

### <a name="conceptual-articles-and-videos"></a>Vidéos et articles conceptuels
* [Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Utilisation de Stockage Fichier Azure avec Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Outils pris en charge pour le stockage de fichiers
* [Utilisation d'Azure PowerShell avec Azure Storage](storage-powershell-guide-full.md)
* [Utilisation de AzCopy avec Microsoft Azure Storage](storage-use-azcopy.md)
* [Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage](storage-azure-cli.md#create-and-manage-file-shares)
* [Résolution des problèmes de stockage de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Référence
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Billets de blog :
* [Le stockage de fichiers Azure est désormais mis à la disposition générale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Présentation de Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Persisting connections to Microsoft Azure File storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx) (Conservation des connexions vers Stockage Fichier Microsoft Azure)