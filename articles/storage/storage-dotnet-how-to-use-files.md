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
# <a name="develop-for-azure-file-storage-with-net"></a>Développer pour Stockage Fichier Azure avec .NET 
> [!NOTE]
> Cet article explique comment toomanage stockage Azure files avec le code .NET. toolearn en savoir plus sur le stockage de fichiers Azure, consultez hello [Introduction tooAzure stockage de fichiers](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel va vous montrer des bases de hello de l’utilisation des applications de toodevelop .NET ou les services qui utilisent des données de fichier toostore fichier Azure storage. Dans ce didacticiel, nous crée une application console simple et montrent comment tooperform les actions de base avec un stockage .NET et des fichiers Azure :

* Obtenir le contenu de hello d’un fichier
* Définir le quota hello (taille maximale) pour le partage de fichiers hello.
* Créer une signature d’accès partagé (clé SAS) pour un fichier qui utilise une stratégie d’accès partagé définie sur le partage de hello.
* Copier un fichier tooanother Bonjour même compte de stockage.
* Copier un objet blob de fichier tooa Bonjour même compte de stockage.
* Utiliser Azure Storage Metrics pour la résolution des problèmes.

> [!Note]  
> Stockage de fichiers Azure sont accessibles sur SMB, il est possible toowrite applications simples qui accéder au partage de fichiers Azure hello à l’aide de classes de System.IO hello standard d’e/s de fichier. Cet article décrit comment toowrite les applications qui utilisent hello Azure stockage .NET SDK, qui utilise hello [le stockage de fichiers Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure stockage de fichiers. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Créer l’application de console hello et obtenir l’assembly hello
Dans Visual Studio, créez une application de console Windows. Hello suit vous montre comment toocreate une application de console dans Visual Studio 2017, toutefois, les étapes de hello sont similaires dans les autres versions de Visual Studio.

1. Sélectionnez **Fichier** > **Nouveau** > **Projet**
2. Sélectionnez **Installé** > **Modèles** > **Visual C#** > **Bureau classique Windows**
3. Sélectionnez **Application console (.NET Framework)**
4. Entrez un nom pour votre application dans hello **nom :** champ
5. Sélectionnez **OK**.

Tous les exemples de code dans ce didacticiel peuvent être ajoutés toohello `Main()` méthode de votre application de console `Program.cs` fichier.

Vous pouvez utiliser hello bibliothèque cliente de stockage Azure dans n’importe quel type d’application .NET, y compris une application web ou de service cloud Azure et les applications de bureau et mobiles. Dans ce guide, nous utilisons une application console pour plus de simplicité.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Utiliser les packages NuGet tooinstall hello requis
Il existe deux packages, vous devez tooreference dans votre projet toocomplete ce didacticiel :

* [Bibliothèque cliente Microsoft Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ce package fournit un accès par programmation toodata des ressources dans votre compte de stockage.
* [Bibliothèque Microsoft Azure Configuration Manager pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) : ce package fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration, quel que soit l’emplacement d’exécution de votre application.

Vous pouvez utiliser NuGet tooobtain les deux packages. Procédez comme suit :

1. Cliquez avec le bouton droit sur votre projet dans **l’Explorateur de solutions**, puis sélectionnez **Gérer les packages NuGet**.
2. Rechercher en ligne du terme « WindowsAzure.Storage » et cliquez sur **installer** tooinstall hello bibliothèque cliente de stockage et de ses dépendances.
3. Rechercher en ligne « WindowsAzure.ConfigurationManager » et cliquez sur **installer** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Enregistrez votre fichier app.config toohello d’informations d’identification de compte stockage
Enregistrez ensuite vos informations d’identification dans le fichier app.config du projet. Modifier le fichier app.config de hello afin qu’il apparaisse toohello similaire, l’exemple suivant, en remplaçant `myaccount` avec le nom de votre compte de stockage, et `mykey` avec votre clé de compte de stockage.

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
> version la plus récente de l’émulateur de stockage Azure hello Hello ne prend pas en charge le stockage Azure. Votre chaîne de connexion doit cibler un compte Azure Storage dans hello cloud toowork avec le stockage de fichiers Azure.

## <a name="add-using-directives"></a>Ajouter des directives d’utilisation
Ouvrez hello `Program.cs` à partir de l’Explorateur de solutions et ajoutez hello qui suit à l’aide de top toohello de directives de fichier de hello.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Un partage de fichiers de hello d’accès par programmation
Ensuite, ajoutez hello suivant code toohello `Main()` chaîne de connexion de hello tooretrieve (méthode) (après le code hello ci-dessus). Ce code obtient un fichier de toohello référence créée précédemment et renvoie sa fenêtre de console toohello contenu.

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

Exécutez la sortie de hello hello toosee de l’application console.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Taille maximale du jeu hello pour un partage de fichiers
Depuis la version 5.x de hello bibliothèque cliente de stockage Azure, vous pouvez définir ensemble hello quota (ou taille maximale) pour un partage de fichiers, en gigaoctets. Vous pouvez également vérifier toosee la quantité de données est actuellement stocké sur le partage de hello.

En définissant le quota de hello pour un partage, vous pouvez limiter la taille totale de hello hello les fichiers stockés sur le partage de hello. Si hello la taille totale des fichiers sur le partage de hello dépasse quota de hello défini sur le partage de hello, les clients seront taille de hello tooincrease impossible des fichiers existants ou créer de nouveaux fichiers, à moins que ces fichiers sont vides.

exemple Hello ci-dessous montre comment toocheck hello en cours d’utilisation pour un partage et comment tooset hello quota pour le partage de hello.

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Génération d’une signature d’accès partagé pour un fichier ou partage de fichiers
Depuis la version 5.x de hello bibliothèque cliente de stockage Azure, vous pouvez générer une signature d’accès partagé (SAP) pour un partage de fichiers ou un fichier. Vous pouvez également créer une stratégie d’accès partagé sur un toomanage partagé accès au partage de fichier signatures. Création d’une stratégie d’accès partagé est recommandée, car elle fournit un moyen de révocation hello SAS si elle doit être compromise.

Bonjour à l’exemple suivant crée une stratégie d’accès partagé sur un partage, puis utilise que tooprovide hello les contraintes de stratégie pour une SAP sur un fichier dans hello partagent.

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

Pour plus d’informations sur la création et l’utilisation de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) et [Créer et utiliser une signature d’accès partagé avec des blobs Azure](storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Copie des fichiers
Depuis la version 5.x de hello bibliothèque cliente de stockage Azure, vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier. Dans les sections suivantes hello, nous allons montrer comment tooperform ces copier les opérations par programme.

Vous pouvez également utiliser AzCopy toocopy un fichier tooanother ou toocopy un objet blob tooa fichier et inversement. Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

> [!NOTE]
> Si vous copiez un fichier de tooa blob ou d’un objet blob tooa de fichier, vous devez utiliser un objet de source accès partagé (SAS) de signature tooauthenticate hello, même si vous copiez dans hello même compte de stockage.
> 
> 

**Copier un fichier tooanother** hello exemple suivant copie un fichier tooanother Bonjour même partage. Étant donné que cette opération de copie entre les fichiers dans hello même compte de stockage, vous pouvez utiliser la copie de la clé partagée d’authentification tooperform hello.

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

**Copier un objet blob tooa de fichier** hello exemple suivant crée un fichier et le copie blob tooa dans hello même compte de stockage. exemple de Hello crée un SAS pour le fichier de source de hello, quel service hello utilise le fichier de source toohello tooauthenticate accès pendant l’opération de copie hello.

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

Vous pouvez copier un fichier de tooa blob Bonjour identique. Si l’objet de source de hello est un objet blob, vous devez ensuite créer un objet blob SAS tooauthenticate accès toothat au cours de l’opération de copie hello.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Résolution des problèmes Stockage Fichier Azure à l’aide de métriques
Azure Storage Analytics prend à présent en charge les métriques pour Stockage Fichier Azure. Avec les données de métriques, vous pouvez suivre les demandes et diagnostiquer les problèmes.


Vous pouvez activer les métriques pour le stockage de fichiers Azure à partir de hello [Azure Portal](https://portal.azure.com). Vous pouvez également activer les métriques par programme en appelant hello opération de définition des propriétés de Service fichier via l’API REST de hello, ou l’un de ses analogues Bonjour bibliothèque cliente de stockage.


Hello, exemple de code suivant montre comment toouse hello bibliothèque cliente de stockage pour les métriques de tooenable .NET pour le stockage de fichiers Azure.

Tout d’abord, ajoutez hello qui suit `using` directives tooyour `Program.cs` un fichier, en outre toothose que vous avez ajouté ci-dessus :

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Notez que, pendant que les objets BLOB Azure, la Table de Azure et files d’attente Azure, utilisez hello partagé `ServiceProperties` type Bonjour `Microsoft.WindowsAzure.Storage.Shared.Protocol` espace de noms, stockage de fichier Azure utilise son propre type, hello `FileServiceProperties` type Bonjour `Microsoft.WindowsAzure.Storage.File.Protocol` espace de noms. Les deux espaces de noms doivent être référencées à partir de votre code, toutefois, pour hello suivant toocompile de code.

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

En outre, vous pouvez faire référence trop[le stockage de fichiers Azure Article de résolution des problèmes](storage-troubleshoot-file-connection-problems.md) de bout en bout des conseils de dépannage.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

### <a name="conceptual-articles-and-videos"></a>Vidéos et articles conceptuels
* [Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Outils pris en charge pour le stockage de fichiers
* [Utilisation d'Azure PowerShell avec Azure Storage](storage-powershell-guide-full.md)
* [Comment toouse AzCopy avec Microsoft Azure Storage](storage-use-azcopy.md)
* [À l’aide de hello CLI d’Azure avec le stockage Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Résolution des problèmes de stockage de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Référence
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Billets de blog :
* [Le stockage de fichiers Azure est désormais mis à la disposition générale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Présentation de Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [TooMicrosoft connexions persistantes stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
