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
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="ae099-103">Définir et récupérer des propriétés et métadonnées d’objet</span><span class="sxs-lookup"><span data-stu-id="ae099-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="ae099-104">Les objets dans les propriétés de prise en charge de système de stockage Azure et les métadonnées définies par l’utilisateur, en outre toohello les données qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="ae099-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="ae099-105">Cet article traite de la gestion des propriétés système et les métadonnées définies par l’utilisateur avec hello [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="ae099-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="ae099-106">**Propriétés système** : des propriétés système s’appliquent à chaque ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="ae099-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="ae099-107">Certaines d'entre elles peuvent être lues ou configurées, alors que d'autres sont en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="ae099-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="ae099-108">Dans les coulisses hello, certaines propriétés système correspondent toocertain des en-têtes HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="ae099-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="ae099-109">bibliothèque cliente de stockage Azure Hello gère pour vous.</span><span class="sxs-lookup"><span data-stu-id="ae099-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="ae099-110">**Les métadonnées définies par l’utilisateur**: les métadonnées définies par l’utilisateur sont spécifiés sur une ressource donnée sous forme de hello d’une paire nom-valeur.</span><span class="sxs-lookup"><span data-stu-id="ae099-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="ae099-111">Vous pouvez utiliser des valeurs de métadonnées toostore supplémentaires avec une ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="ae099-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="ae099-112">Ces valeurs de métadonnées supplémentaires pour votre usage propre et n’affectent pas le comporte de la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="ae099-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="ae099-113">La récupération des valeurs des propriétés et des métadonnées d’une ressource se déroule en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="ae099-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="ae099-114">Avant de pouvoir lire ces valeurs, vous devez explicitement les récupérer en appelant hello **FetchAttributes** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ae099-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae099-115">Les valeurs de propriété et des métadonnées pour une ressource de stockage ne sont pas remplies, sauf si vous appelez l’une des hello **FetchAttributes** méthodes.</span><span class="sxs-lookup"><span data-stu-id="ae099-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="ae099-116">Vous recevrez une erreur `400 Bad Request` si des paires nom/valeur contiennent des caractères non-ASCII.</span><span class="sxs-lookup"><span data-stu-id="ae099-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="ae099-117">Paires nom/valeur de métadonnées sont des en-têtes HTTP valides et par conséquent, doivent respecter les restrictions tooall régissant les en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ae099-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="ae099-118">Par conséquent, il est recommandé d’utiliser l’encodage URL ou l’encodage Base64 pour les noms et valeurs contenant des caractères non-ASCII.</span><span class="sxs-lookup"><span data-stu-id="ae099-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="ae099-119">Définition et récupération de propriétés</span><span class="sxs-lookup"><span data-stu-id="ae099-119">Setting and retrieving properties</span></span>
<span data-ttu-id="ae099-120">valeurs de propriété tooretrieve appel hello **FetchAttributes** méthode sur votre objet blob ou conteneur toopopulate hello propriétés, puis lire les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="ae099-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="ae099-121">propriétés de tooset sur un objet, spécifiez la valeur de la propriété hello, puis appelez hello **SetProperties** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ae099-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="ae099-122">Hello exemple de code suivant crée un conteneur, puis écrit une partie de sa fenêtre de console tooa propriété valeurs.</span><span class="sxs-lookup"><span data-stu-id="ae099-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

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

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="ae099-123">Définition et récupération de métadonnées</span><span class="sxs-lookup"><span data-stu-id="ae099-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="ae099-124">Vous pouvez indiquer des métadonnées sous la forme de paires nom-valeur sur une ressource d’objet blob ou de conteneur.</span><span class="sxs-lookup"><span data-stu-id="ae099-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="ae099-125">métadonnées de tooset, ajouter des paires nom-valeur toohello **métadonnées** collection sur la ressource de hello, puis appelez hello **SetMetadata** hello toosave de méthode valeurs toohello service.</span><span class="sxs-lookup"><span data-stu-id="ae099-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="ae099-126">nom Hello de vos métadonnées doit être conforme à toohello les conventions d’affectation de noms pour les identificateurs c#.</span><span class="sxs-lookup"><span data-stu-id="ae099-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="ae099-127">Hello exemple de code suivant définit métadonnées sur un conteneur.</span><span class="sxs-lookup"><span data-stu-id="ae099-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="ae099-128">Une valeur est définie à l’aide de la collection hello **ajouter** (méthode).</span><span class="sxs-lookup"><span data-stu-id="ae099-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="ae099-129">Hello autres a la valeur à l’aide de la syntaxe implicite clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="ae099-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="ae099-130">Les deux sont valides.</span><span class="sxs-lookup"><span data-stu-id="ae099-130">Both are valid.</span></span>

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

<span data-ttu-id="ae099-131">métadonnées tooretrieve, appel hello **FetchAttributes** méthode sur votre hello toopopulate objet blob ou conteneur **métadonnées** collection, puis lire les valeurs hello, comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae099-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ae099-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae099-132">Next steps</span></span>
* [<span data-ttu-id="ae099-133">Référence de la bibliothèque cliente Stockage Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ae099-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="ae099-134">Package NuGet de la bibliothèque cliente Stockage Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ae099-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
