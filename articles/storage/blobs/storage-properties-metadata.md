---
title: "aaaSet et récupérer l’objet de propriétés et des métadonnées dans le stockage Azure | Documents Microsoft"
description: "Stockez des métadonnées personnalisées sur des objets dans Azure Storage, et définissez et récupérez les propriétés système."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a>Définir et récupérer des propriétés et métadonnées d’objet

Les objets dans les propriétés de prise en charge de système de stockage Azure et les métadonnées définies par l’utilisateur, en outre toohello les données qu’ils contiennent. Cet article traite de la gestion des propriétés système et les métadonnées définies par l’utilisateur avec hello [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Propriétés système** : des propriétés système s’appliquent à chaque ressource de stockage. Certaines d'entre elles peuvent être lues ou configurées, alors que d'autres sont en lecture seule. Dans les coulisses hello, certaines propriétés système correspondent toocertain des en-têtes HTTP standard. bibliothèque cliente de stockage Azure Hello gère pour vous.

* **Les métadonnées définies par l’utilisateur**: les métadonnées définies par l’utilisateur sont spécifiés sur une ressource donnée sous forme de hello d’une paire nom-valeur. Vous pouvez utiliser des valeurs de métadonnées toostore supplémentaires avec une ressource de stockage. Ces valeurs de métadonnées supplémentaires pour votre usage propre et n’affectent pas le comporte de la ressource de hello.

La récupération des valeurs des propriétés et des métadonnées d’une ressource se déroule en deux étapes. Avant de pouvoir lire ces valeurs, vous devez explicitement les récupérer en appelant hello **FetchAttributes** (méthode).

> [!IMPORTANT]
> Les valeurs de propriété et des métadonnées pour une ressource de stockage ne sont pas remplies, sauf si vous appelez l’une des hello **FetchAttributes** méthodes.
>
> Vous recevrez une erreur `400 Bad Request` si des paires nom/valeur contiennent des caractères non-ASCII. Paires nom/valeur de métadonnées sont des en-têtes HTTP valides et par conséquent, doivent respecter les restrictions tooall régissant les en-têtes HTTP. Par conséquent, il est recommandé d’utiliser l’encodage URL ou l’encodage Base64 pour les noms et valeurs contenant des caractères non-ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Définition et récupération de propriétés
valeurs de propriété tooretrieve appel hello **FetchAttributes** méthode sur votre objet blob ou conteneur toopopulate hello propriétés, puis lire les valeurs hello.

propriétés de tooset sur un objet, spécifiez la valeur de la propriété hello, puis appelez hello **SetProperties** (méthode).

Hello exemple de code suivant crée un conteneur, puis écrit une partie de sa fenêtre de console tooa propriété valeurs.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>Définition et récupération de métadonnées
Vous pouvez indiquer des métadonnées sous la forme de paires nom-valeur sur une ressource d’objet blob ou de conteneur. métadonnées de tooset, ajouter des paires nom-valeur toohello **métadonnées** collection sur la ressource de hello, puis appelez hello **SetMetadata** hello toosave de méthode valeurs toohello service.

> [!NOTE]
> nom Hello de vos métadonnées doit être conforme à toohello les conventions d’affectation de noms pour les identificateurs c#.
>
>

Hello exemple de code suivant définit métadonnées sur un conteneur. Une valeur est définie à l’aide de la collection hello **ajouter** (méthode). Hello autres a la valeur à l’aide de la syntaxe implicite clé/valeur. Les deux sont valides.

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

métadonnées tooretrieve, appel hello **FetchAttributes** méthode sur votre hello toopopulate objet blob ou conteneur **métadonnées** collection, puis lire les valeurs hello, comme indiqué dans l’exemple hello ci-dessous.

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
* [Référence de la bibliothèque cliente Stockage Azure pour .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Package NuGet de la bibliothèque cliente Stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
