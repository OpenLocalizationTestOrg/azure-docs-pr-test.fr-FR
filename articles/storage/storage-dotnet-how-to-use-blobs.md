---
title: "aaaGet main du stockage d’objets Blob Azure (stockage d’objets) à l’aide de .NET | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Prise en main du stockage d’objets blob Azure à l’aide de .NET

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

### <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel montre comment le code toowrite .NET pour les scénarios courants lors de l’utilisation du stockage d’objets Blob Azure. Les scénarios traités incluent le chargement, la création de listes, le téléchargement et la suppression d’objets blob.

**Configuration requise :**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Bibliothèque cliente Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestionnaire de configuration Azure pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Un [compte de stockage Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Autres exemples
Pour obtenir des exemples supplémentaires utilisant Blob Storage, voir [Prise en main d’Azure Blob Storage dans .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/). Vous pouvez télécharger l’exemple d’application hello et exécutez-le ou parcourir le code hello sur GitHub.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Ajouter des directives d’utilisation
Ajoutez hello suivant **à l’aide de** haut toohello de directives de hello `Program.cs` fichier :

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Analyser la chaîne de connexion hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Créer le client du service Blob hello
Hello **CloudBlobClient** classe vous permet de tooretrieve conteneurs et objets BLOB stockés dans le stockage d’objets Blob. Voici un moyen toocreate hello service client :

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Vous êtes maintenant code prêt toowrite qui lit les données à partir d’et écrit le stockage des données tooBlob.

## <a name="create-a-container"></a>Créez un conteneur.
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Cet exemple montre comment toocreate un conteneur s’il n’existe pas déjà :

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

Par défaut, le nouveau conteneur de hello est privé, ce qui signifie que vous devez spécifier vos objets BLOB de stockage accès toodownload clé à partir de ce conteneur. Si vous souhaitez que les fichiers hello toomake tooeveryone de hello conteneur disponible, vous pouvez définir hello conteneur toobe public à l’aide de hello suivant de code :

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public. Toutefois, vous pouvez modifier ou supprimer uniquement si vous avez une signature d’accès partagé ou de clé d’accès hello compte approprié.

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.  Dans la plupart des cas, objet blob de blocs est hello recommandé toouse de type.

tooupload fichier tooa objet blob de blocs, obtenir une référence de conteneur et utiliser tooget une référence d’objet blob de bloc. Une fois que vous avez une référence d’objet blob, vous pouvez télécharger n’importe quel flux de données tooit en appelant hello **UploadFromStream** (méthode). Cette opération crée l’objet blob de hello si elle n’existe pas déjà, ou le remplace s’il existe.

Hello suivant montre l’exemple de comment tooupload un objet blob dans un conteneur et suppose que le conteneur de hello a déjà été créé.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, d’abord obtenir une référence de conteneur. Vous pouvez ensuite utiliser du conteneur hello **ListBlobs** objets BLOB de méthode tooretrieve hello et/ou les répertoires qu’il contient. tooaccess hello ensemble complet des propriétés et méthodes pour retourné **IListBlobItem**, vous devez effectuer un cast tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objet. Si le type de hello est inconnu, vous pouvez utiliser un toodetermine de vérification de type qui toocast à. Hello de code suivant montre comment tooretrieve et sortie hello URI de chaque élément Bonjour _photos_ conteneur :

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
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
```

En incluant les informations de chemin d’accès aux noms des objets blob, vous obtenez alors une structure de répertoires virtuels que vous pouvez organiser et parcourir de la même manière qu’un système de fichiers traditionnel. structure de répertoire Hello est virtuel uniquement : hello uniquement les ressources disponibles dans le stockage d’objets Blob sont des conteneurs et objets BLOB. Toutefois, la bibliothèque cliente de stockage hello propose un **CloudBlobDirectory** répertoire virtuel de toorefer tooa de l’objet et de simplifier les processus de hello de travailler avec des objets BLOB qui sont organisées de cette façon.

Par exemple, considérez hello ensemble suivant d’objets BLOB de blocs dans un conteneur nommé *photos*:

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

Lorsque vous appelez **ListBlobs** sur hello *photos* conteneur (par exemple hello précédant l’extrait de code), une liste hiérarchique est retournée. Il contient à la fois **CloudBlobDirectory** et **CloudBlockBlob** objets représentant les répertoires de hello et les objets BLOB dans le conteneur de hello, respectivement. résultat de Hello ressemble à :

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Si vous le souhaitez, vous pouvez définir hello **UseFlatBlobListing** paramètre Hello **ListBlobs** méthode **true**. Dans ce cas, chaque objet blob dans le conteneur de hello est retourné comme un **CloudBlockBlob** objet. Hello appel trop**ListBlobs** tooreturn une liste plate ressemble à ceci :

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

et les résultats hello ressemblent à ceci :

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Télécharger des objets blob
objets BLOB toodownload, tout d’abord extraire une référence d’objet blob et ensuite appeler hello **méthodes DownloadToStream** (méthode). exemple Hello utilise hello **méthodes DownloadToStream** méthode tootransfer hello contenu tooa flux de données objet blob que peuvent alors être conservées tooa des fichiers locaux.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

Vous pouvez également utiliser hello **méthodes DownloadToStream** contenu de hello toodownload de méthode d’un objet blob comme une chaîne de texte.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a>Suppression d’objets blob
toodelete un objet blob, commencez par obtenir une référence d’objet blob, puis appelez le **supprimer** méthode dessus.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a>Création d’une liste d’objets blob dans des pages de manière asynchrone
Si vous répertoriez un grand nombre d’objets BLOB, ou nombre de hello toocontrol de vous renvoyer dans une opération de liste de résultats, vous pouvez répertorier les objets BLOB dans les pages de résultats. Cet exemple montre comment tooreturn produit des pages de façon asynchrone, afin que l’exécution n’est pas bloquée lors de l’attente tooreturn un grand ensemble de résultats.

Cet exemple montre un liste plate d’objets blob, mais vous pouvez également effectuer une liste hiérarchique, en définissant un hello _useFlatBlobListing_ paramètre Hello **ListBlobsSegmentedAsync** too_false_ de méthode.

Étant donné que la méthode d’échantillonnage hello appelle une méthode asynchrone, il doit commencer par hello _async_ (mot clé) et doit retourner un **tâche** objet. Hello await mot clé spécifié pour hello **ListBlobsSegmentedAsync** méthode suspend l’exécution de méthode d’échantillonnage hello jusqu'à la fin de tâche de liste hello.

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a>Écriture tooan ajouter des objets blob
Il est optimisé pour les opérations d’ajout, telles que la journalisation. Comme un objet blob de blocs, un objet blob d’ajout est constitué de blocs, mais lorsque vous ajoutez un nouvel objet blob bloc tooan append, il est toujours ajouté toohello de fin de l’objet blob de hello. Vous ne pouvez pas mettre à jour ou supprimer un bloc dans un objet blob d’ajout. ID de bloc Hello pour un objet blob d’ajout ne sont pas exposés à ceux d’un objet blob de blocs.

Chaque bloc dans un objet blob d’ajout peut avoir une taille différente, les tooa au maximum de 4 Mo, et un objet blob d’ajout peut inclure un maximum de 50 000 blocs. Hello taille maximale d’un objet blob d’ajout est par conséquent légèrement supérieur à 195 Go (4 Mo X avec 50 000 blocs).

exemple Hello ci-dessous crée un nouvel objet blob d’ajout et ajoute certaines tooit de données, en simulant une opération de journalisation simple.

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

Consultez [objets BLOB de blocs, objets BLOB de pages et ajouter des objets BLOB](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) pour plus d’informations sur les différences de hello entre types hello trois d’objets BLOB.

## <a name="managing-security-for-blobs"></a>Gestion de la sécurité pour les objets blob
Par défaut, le stockage Azure conserve vos données sécurisées en limitant le propriétaire du compte accès toohello, qui est en possession des clés d’accès compte hello. Lorsque vous avez besoin des données d’objet blob tooshare dans votre compte de stockage, il est important toodo c’est le cas sans compromettre la sécurité hello des clés d’accès de votre compte. En outre, vous pouvez chiffrer tooensure de données d’objet blob est sécurisé va acheminement hello et dans le stockage Azure.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Contrôle de l’accès aux données de tooblob
Par défaut, les données d’objet blob hello dans votre compte de stockage sont accessible uniquement propriétaire du compte toostorage. L’authentification des demandes sur le stockage d’objets Blob nécessite une clé d’accès compte hello à par défaut. Toutefois, vous souhaiterez peut-être toomake certains utilisateurs tooother disponibles des données d’objets blob. Deux options s'offrent à vous :

* **Accès anonyme :** vous pouvez rendre un conteneur ou ses objets blob disponibles publiquement pour un accès anonyme. Consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](storage-manage-access-to-resources.md) pour plus d’informations.
* **Signatures d’accès partagé :** vous pouvez fournir des clients avec une signature d’accès partagé (SAS), qui fournit des ressources de tooa accès délégué dans votre compte de stockage, avec des autorisations que vous spécifiez et sur un intervalle que vous spécifiez. Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) .

### <a name="encrypting-blob-data"></a>Chiffrement des données d’objets blob
Le stockage Azure prend en charge le chiffrement des données d’objet blob au client de hello et sur le serveur de hello :

* **Le chiffrement côté client :** hello bibliothèque cliente de stockage pour .NET prend en charge le chiffrement des données dans les applications clientes avant chargement tooAzure stockage et le déchiffrement des données lors du téléchargement de toohello client. bibliothèque de Hello prend également en charge l’intégration avec le coffre de clés Azure pour la gestion de clés de compte de stockage. Pour plus d’informations, voir [Chiffrement côté client avec .NET pour Microsoft Azure Storage](storage-client-side-encryption.md) . Voir également [Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l’aide d’Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).
* **Chiffrement côté serveur**: Azure Storage prend désormais en charge le chiffrement côté serveur. Voir [Azure Storage Service Encryption pour les données au repos (version préliminaire)](storage-service-encryption.md).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello du stockage Blob, suivez ces liens de toolearn plus.

### <a name="microsoft-azure-storage-explorer"></a>Explorateur Microsoft Azure Storage
* [Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.

### <a name="blob-storage-samples"></a>Exemples relatifs à Blob Storage
* [Prise en main d’Azure Blob Storage dans .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Documentation de référence sur le stockage d’objets blob
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Référence d’API REST](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Guides conceptuels
* [Transfert de données avec hello utilitaire de ligne de commande AzCopy](storage-use-azcopy.md)
* [Prise en main du stockage de fichier pour .NET](storage-dotnet-how-to-use-files.md)
* [Comment toouse Azure stockage d’objets blob par hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
