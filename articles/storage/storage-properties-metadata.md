---
title: "Définir et récupérer des propriétés et métadonnées d’objet dans Stockage Azure | Documents Microsoft"
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
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="ff8c2-103">Définir et récupérer des propriétés et métadonnées d’objet</span><span class="sxs-lookup"><span data-stu-id="ff8c2-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="ff8c2-104">Les objets dans Stockage Azure prennent en charge des propriétés système et des métadonnées définies par l’utilisateur, en plus des données qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="ff8c2-105">Cet article décrit la gestion des propriétés système et des métadonnées définies par l’utilisateur avec la [Bibliothèque cliente Stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="ff8c2-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="ff8c2-106">**Propriétés système** : des propriétés système s’appliquent à chaque ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="ff8c2-107">Certaines d'entre elles peuvent être lues ou configurées, alors que d'autres sont en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="ff8c2-108">En arrière-plan, certaines propriétés système correspondent à certains en-têtes HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="ff8c2-109">La bibliothèque cliente de stockage Azure gère ces en-têtes pour vous.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="ff8c2-110">**Métadonnées définies par l’utilisateur** : il s’agit de métadonnées que vous spécifiez pour une ressource donnée, sous la forme d’une paire nom-valeur.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="ff8c2-111">Vous pouvez utiliser des métadonnées pour stocker des valeurs supplémentaires avec une ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="ff8c2-112">Ces valeurs de métadonnées supplémentaires sont destinées à votre usage personnel et n’affectent pas le comportement de la ressource.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="ff8c2-113">La récupération des valeurs des propriétés et des métadonnées d’une ressource se déroule en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="ff8c2-114">Pour pouvoir lire ces valeurs, vous devez les récupérer explicitement en appelant la méthode **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="ff8c2-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff8c2-115">Les valeurs des propriétés et des métadonnées d’une ressource de stockage ne sont pas renseignées, sauf si vous appelez l’une des méthodes **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="ff8c2-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="ff8c2-116">Vous recevrez une erreur `400 Bad Request` si des paires nom/valeur contiennent des caractères non-ASCII.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="ff8c2-117">Les paires nom/valeur de métadonnées sont des en-têtes HTTP valides, et doivent donc respecter toutes les restrictions régissant les en-têtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="ff8c2-118">Par conséquent, il est recommandé d’utiliser l’encodage URL ou l’encodage Base64 pour les noms et valeurs contenant des caractères non-ASCII.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="ff8c2-119">Définition et récupération de propriétés</span><span class="sxs-lookup"><span data-stu-id="ff8c2-119">Setting and retrieving properties</span></span>
<span data-ttu-id="ff8c2-120">Pour récupérer des valeurs de propriétés, appelez la méthode **FetchAttributes** sur votre objet blob ou votre conteneur pour remplir les propriétés, puis lisez les valeurs.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="ff8c2-121">Pour configurer les propriétés d’un objet blob, indiquez la valeur de propriété, puis appelez la méthode **SetProperties** .</span><span class="sxs-lookup"><span data-stu-id="ff8c2-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="ff8c2-122">L’exemple de code suivant crée un conteneur, puis écrit certaines de ses valeurs de propriété dans une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="ff8c2-123">Définition et récupération de métadonnées</span><span class="sxs-lookup"><span data-stu-id="ff8c2-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="ff8c2-124">Vous pouvez indiquer des métadonnées sous la forme de paires nom-valeur sur une ressource d’objet blob ou de conteneur.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="ff8c2-125">Pour configurer des métadonnées, ajoutez des paires nom-valeur à la collection **Metadata** de la ressource, puis appelez la méthode **SetMetadata** pour enregistrer les valeurs sur le service.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="ff8c2-126">Le nom de vos métadonnées doit respecter la convention d’affectation de noms pour les identificateurs C#.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="ff8c2-127">L’exemple de code suivant définit les métadonnées d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="ff8c2-128">Une valeur est définie à l’aide de la méthode **Add** de la collection.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="ff8c2-129">L’autre valeur est définie à l’aide d’une syntaxe implicite clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="ff8c2-130">Les deux sont valides.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="ff8c2-131">Pour récupérer des métadonnées, appelez la méthode **FetchAttributes** sur votre objet blob ou votre conteneur pour remplir la collection **Metadata**, puis lisez les valeurs, comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ff8c2-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ff8c2-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff8c2-132">Next steps</span></span>
* [<span data-ttu-id="ff8c2-133">Référence de la bibliothèque cliente Stockage Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ff8c2-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="ff8c2-134">Package NuGet de la bibliothèque cliente Stockage Azure pour .NET</span><span class="sxs-lookup"><span data-stu-id="ff8c2-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
