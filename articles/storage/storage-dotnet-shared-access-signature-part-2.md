---
title: "aaaCreate et utiliser une signature d’accès partagé (SAS) avec le stockage d’objets Blob Azure | Documents Microsoft"
description: "Ce didacticiel vous montre comment toocreate partagé des signatures d’accès pour une utilisation avec le stockage d’objets Blob et tooconsume dans vos applications clientes."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="bad31-103">Signatures d’accès partagé, partie 2 : créer et utiliser une signature d’accès partagé avec Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bad31-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="bad31-104">[partie 1](storage-dotnet-shared-access-signature-part-1.md) de ce didacticiel traitait des signatures d'accès partagé et indiquait les meilleures pratiques les concernant.</span><span class="sxs-lookup"><span data-stu-id="bad31-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="bad31-105">Partie 2 vous montre comment toogenerate, puis utiliser un accès partagé les signatures avec un stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="bad31-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="bad31-106">exemples de Hello sont écrites en c# et utilisent hello bibliothèque cliente de stockage Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="bad31-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="bad31-107">exemples de Hello dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="bad31-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="bad31-108">Générer une signature d'accès partagé sur un conteneur</span><span class="sxs-lookup"><span data-stu-id="bad31-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="bad31-109">Générer une signature d'accès partagé sur un blob</span><span class="sxs-lookup"><span data-stu-id="bad31-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="bad31-110">Créer des signatures de toomanage stratégie un accès stockée sur les ressources d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="bad31-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="bad31-111">Test des signatures d’accès hello partagé dans une application cliente</span><span class="sxs-lookup"><span data-stu-id="bad31-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="bad31-112">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="bad31-112">About this tutorial</span></span>
<span data-ttu-id="bad31-113">Au cours de ce didacticiel, nous allons créer deux consoles d’application qui présentent la création et l’utilisation des signatures d’accès partagé pour les conteneurs et les blobs :</span><span class="sxs-lookup"><span data-stu-id="bad31-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="bad31-114">**Application 1**: hello application de gestion.</span><span class="sxs-lookup"><span data-stu-id="bad31-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="bad31-115">Elle génère une signature d’accès partagé pour un conteneur et un blob.</span><span class="sxs-lookup"><span data-stu-id="bad31-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="bad31-116">Inclut la clé de l’accès du compte de stockage hello dans le code source.</span><span class="sxs-lookup"><span data-stu-id="bad31-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="bad31-117">**L’application 2**: hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="bad31-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="bad31-118">Accède aux objets blob ressources de conteneur et à l’aide de signatures d’accès hello partagé créés avec la première application de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="bad31-119">Signatures tooaccess conteneur utilise uniquement hello accès partagé et des ressources d’objet blob--il exécute *pas* incluent la clé de l’accès du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="bad31-120">Partie 1 : Créer un accès à la console application toogenerate partagé des signatures</span><span class="sxs-lookup"><span data-stu-id="bad31-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="bad31-121">Tout d’abord, assurez-vous que vous avez hello bibliothèque cliente de stockage Azure pour .NET est installé.</span><span class="sxs-lookup"><span data-stu-id="bad31-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="bad31-122">Vous pouvez installer hello [package NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "package NuGet") contenant des assemblys plus récentes de hello pour la bibliothèque cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="bad31-123">Il s’agit de hello méthode pour vous assurer que vous disposez correctifs les plus récentes de hello recommandée.</span><span class="sxs-lookup"><span data-stu-id="bad31-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="bad31-124">Vous pouvez également télécharger la bibliothèque cliente de hello dans le cadre de la version la plus récente de hello hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bad31-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="bad31-125">Dans Visual Studio, créez une application console Windows et nommez-la **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="bad31-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="bad31-126">Ajouter des références trop[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) et [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="bad31-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="bad31-127">Hello d’utilisation [Gestionnaire de package NuGet](https://docs.nuget.org/consume/installing-nuget) dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bad31-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="bad31-128">Sélectionnez **Projet** > **Gérer les packages NuGet**, puis effectuez une recherche en ligne pour chaque package (Microsoft.WindowsAzure.ConfigurationManager et WindowsAzure.Storage), et installez-les.</span><span class="sxs-lookup"><span data-stu-id="bad31-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="bad31-129">Vous pouvez également rechercher ces assemblys dans votre installation de hello Azure SDK et ajouter des références toothem :</span><span class="sxs-lookup"><span data-stu-id="bad31-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="bad31-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="bad31-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="bad31-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="bad31-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="bad31-132">Au haut hello du fichier de hello Program.cs, ajoutez hello **à l’aide de** directives :</span><span class="sxs-lookup"><span data-stu-id="bad31-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="bad31-133">Modifier le fichier app.config de hello pour qu’il contienne un paramètre de configuration avec une chaîne de connexion qui pointe de compte de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="bad31-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="bad31-134">Votre fichier app.config doit ressembler similaire toothis une :</span><span class="sxs-lookup"><span data-stu-id="bad31-134">Your app.config file should look similar toothis one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="bad31-135">Générer une URI de signature d’accès partagé pour un conteneur</span><span class="sxs-lookup"><span data-stu-id="bad31-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="bad31-136">toobegin avec, nous ajoutons une méthode de toogenerate une signature d’accès partagé sur un nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="bad31-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="bad31-137">Dans ce cas, la signature de hello n’est pas associé à une stratégie d’accès stockée, afin qu’elle exerce hello d’informations URI hello indiquant ses autorisations d’expiration de temps et hello il accorde un accès.</span><span class="sxs-lookup"><span data-stu-id="bad31-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="bad31-138">D’abord, ajoutez le code toohello **Main()** méthode tooauthenticate accéder au compte de stockage tooyour et créer un nouveau conteneur :</span><span class="sxs-lookup"><span data-stu-id="bad31-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

<span data-ttu-id="bad31-139">Ensuite, ajoutez une méthode qui génère la signature d’accès partagé hello pour le conteneur de hello et retourne l’URI de signature hello :</span><span class="sxs-lookup"><span data-stu-id="bad31-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="bad31-140">Ajouter hello lignes bas hello hello suivantes **Main()** (méthode), avant l’appel hello**console.ReadLine**, toocall **GetContainerSasUri()** et d’écriture hello fenêtre de console URI toohello signature :</span><span class="sxs-lookup"><span data-stu-id="bad31-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="bad31-141">Compilez et exécutez la signature d’accès partagé toooutput hello URI pour le nouveau conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="bad31-142">Hello URI sera similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="bad31-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="bad31-143">Une fois que vous avez exécuté le code de hello, signature d’accès partagé hello que vous avez créé pour le conteneur de hello sera valide pour hello pendant les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="bad31-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="bad31-144">signature de Hello accorde à un client autorisation toolist des objets BLOB hello conteneurs et toowrite nouveaux objets BLOB toohello.</span><span class="sxs-lookup"><span data-stu-id="bad31-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="bad31-145">Générer une URI de signature d’accès partagé pour un blob</span><span class="sxs-lookup"><span data-stu-id="bad31-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="bad31-146">Ensuite, nous écrire toocreate de code similaire à un nouvel objet blob dans le conteneur de hello et générer une signature d’accès partagé pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="bad31-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="bad31-147">Cette signature d’accès partagé n’est pas associée à une stratégie d’accès stockée pour qu’elle comporte hello heure de début, heure d’expiration et les informations d’autorisation Bonjour URI.</span><span class="sxs-lookup"><span data-stu-id="bad31-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="bad31-148">Ajoutez une nouvelle méthode qui crée un nouvel objet blob et écrit certains tooit de texte, puis génère une signature d’accès partagé et retourne l’URI de signature hello :</span><span class="sxs-lookup"><span data-stu-id="bad31-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="bad31-149">Bas hello hello **Main()** (méthode), ajouter hello suivant lignes toocall **GetBlobSasUri()**, avant d’appeler de hello trop**console.ReadLine ()**et d’écriture hello partagé fenêtre de console accès signature URI toohello :</span><span class="sxs-lookup"><span data-stu-id="bad31-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="bad31-150">Compilez et exécutez la signature d’accès partagé toooutput hello URI pour le nouvel objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="bad31-151">Hello URI sera similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="bad31-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="bad31-152">Créer une stratégie d’accès stockée sur le conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="bad31-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="bad31-153">Maintenant nous allons créer une stratégie d’accès stockée sur le conteneur de hello, qui définit les contraintes hello pour les signatures d’accès partagé qui lui sont associés.</span><span class="sxs-lookup"><span data-stu-id="bad31-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="bad31-154">Dans les exemples précédents hello, que nous avons spécifié l’heure de début hello (implicitement ou explicitement), heure d’expiration hello et autorisations hello sur hello signature d’accès partagé URI lui-même.</span><span class="sxs-lookup"><span data-stu-id="bad31-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="bad31-155">Bonjour exemple suivant, nous spécifions ces sur la stratégie d’accès stockée hello, et non sur la signature d’accès partagé hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="bad31-156">Cela permet de nous toochange ces contraintes sans réémettre hello partagés signature d’accès.</span><span class="sxs-lookup"><span data-stu-id="bad31-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="bad31-157">Il est possible de toohave un ou plusieurs des contraintes de hello sur la signature d’accès partagé hello et reste hello sur la stratégie d’accès stockée hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="bad31-158">Toutefois, vous pouvez spécifier uniquement l’heure de début hello, délai d’expiration et les autorisations dans un lieu ou hello autres.</span><span class="sxs-lookup"><span data-stu-id="bad31-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="bad31-159">Par exemple, vous ne peut pas spécifier des autorisations sur la signature d’accès partagé hello et également de les spécifier dans la stratégie d’accès stockée hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="bad31-160">Lorsque vous ajoutez un conteneur de tooa de stratégie d’accès stockée, vous devez obtenir les autorisations existantes du conteneur hello, ajoutez la nouvelle stratégie d’accès hello et puis définissez les autorisations du conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="bad31-161">Ajoutez une nouvelle méthode qui crée une nouvelle stratégie d’accès stockée sur un conteneur et retourne le nom hello de stratégie de hello :</span><span class="sxs-lookup"><span data-stu-id="bad31-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="bad31-162">En bas de hello Hello **Main()** (méthode), avant l’appel hello**console.ReadLine**, ajouter hello suivant lignes toofirst effacer les stratégies d’accès, puis appelez hello  **CreateSharedAccessPolicy()** méthode :</span><span class="sxs-lookup"><span data-stu-id="bad31-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="bad31-163">Lorsque vous désactivez les stratégies d’accès hello sur un conteneur, vous devez tout d’abord obtenir les autorisations existantes du conteneur hello, puis les autorisations hello clair, puis définir les autorisations de hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="bad31-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="bad31-164">Générer une signature d’accès partagé URI sur conteneur hello qui utilise une stratégie d’accès</span><span class="sxs-lookup"><span data-stu-id="bad31-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="bad31-165">Ensuite, nous créons une autre signature d’accès partagé pour le conteneur hello que nous avons créés précédemment, mais cette fois nous associons signature de hello avec la stratégie d’accès stockée hello que nous avons créé dans l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="bad31-166">Ajouter un nouveau toogenerate de méthode autre signature d’accès partagé pour le conteneur de hello :</span><span class="sxs-lookup"><span data-stu-id="bad31-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="bad31-167">Bas hello hello **Main()** (méthode), avant l’appel hello**console.ReadLine**, ajouter hello suivant hello toocall de lignes **GetContainerSasUriWithPolicy** (méthode) :</span><span class="sxs-lookup"><span data-stu-id="bad31-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="bad31-168">Générer un URI de Signature d’accès partagé sur hello Blob qu’utilise une stratégie d’accès</span><span class="sxs-lookup"><span data-stu-id="bad31-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="bad31-169">Enfin, nous ajouter un toocreate méthode similaire à un autre objet blob et générer une signature d’accès partagé qui est associé à une stratégie d’accès stockée.</span><span class="sxs-lookup"><span data-stu-id="bad31-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="bad31-170">Ajouter un nouveau toocreate de la méthode un objet blob et générer une signature d’accès partagé :</span><span class="sxs-lookup"><span data-stu-id="bad31-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="bad31-171">Bas hello hello **Main()** (méthode), avant l’appel hello**console.ReadLine**, ajouter hello suivant hello toocall de lignes **GetBlobSasUriWithPolicy** méthode :</span><span class="sxs-lookup"><span data-stu-id="bad31-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="bad31-172">Hello **Main()** méthode doit maintenant ressembler à ceci dans son intégralité.</span><span class="sxs-lookup"><span data-stu-id="bad31-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="bad31-173">Exécuter la signature d’accès partagé hello toowrite fenêtre de console toohello URI, puis copiez et collez-les dans un fichier texte pour une utilisation dans hello deuxième partie de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bad31-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="bad31-174">Lorsque vous exécutez des applications de console hello GenerateSharedAccessSignatures, vous verrez suivant toohello similaire de sortie.</span><span class="sxs-lookup"><span data-stu-id="bad31-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="bad31-175">Il s’agit des signatures d’accès partagé de hello que vous utilisez dans la partie 2 du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="bad31-176">Partie 2 : Créer un accès à la console application tootest hello partagé des signatures</span><span class="sxs-lookup"><span data-stu-id="bad31-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="bad31-177">tootest hello partagé créés dans les exemples précédents hello des signatures d’accès, nous créons une deuxième application console qui utilise des opérations de tooperform hello signatures sur le conteneur de hello et sur un objet blob.</span><span class="sxs-lookup"><span data-stu-id="bad31-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="bad31-178">Si plus de 24 heures se sont écoulés depuis la fin de hello première partie du didacticiel de hello, vous avez généré des signatures hello ne seront plus valides.</span><span class="sxs-lookup"><span data-stu-id="bad31-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="bad31-179">Dans ce cas, vous devez exécuter les code hello dans hello première console application toogenerate signatures d’accès partagé actualisée pour une utilisation dans la deuxième partie de hello du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="bad31-180">Dans Visual Studio, créez une application console Windows et nommez-la **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="bad31-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="bad31-181">Ajouter des références trop[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) et [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), comme vous l’avez fait précédemment.</span><span class="sxs-lookup"><span data-stu-id="bad31-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="bad31-182">Au haut hello du fichier de hello Program.cs, ajoutez hello **à l’aide de** directives :</span><span class="sxs-lookup"><span data-stu-id="bad31-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="bad31-183">Dans le corps hello Hello **Main()** (méthode), ajouter hello suivant des constantes de chaîne, la modification de leurs valeurs toohello partagé des signatures d’accès vous avez généré dans la partie 1 du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="bad31-184">Ajouter une méthode tootry conteneur les opérations à l’aide d’une signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="bad31-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="bad31-185">Ensuite, nous ajouter une méthode qui vérifie certaines opérations de conteneur à l’aide d’une signature d’accès partagé pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="bad31-186">signature d’accès partagé Hello est tooreturn utilisé un conteneur de toohello de référence, l’authentification du conteneur de toohello d’accès basé sur la signature hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="bad31-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="bad31-187">Ajoutez hello suivant tooProgram.cs de méthode :</span><span class="sxs-lookup"><span data-stu-id="bad31-187">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="bad31-188">Hello de mise à jour **Main()** méthode toocall **UseContainerSAS()** avec deux hello de signatures d’accès vous avez créé sur le conteneur de hello partagé :</span><span class="sxs-lookup"><span data-stu-id="bad31-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="bad31-189">Ajouter une méthode tootry blob les opérations à l’aide d’une signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="bad31-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="bad31-190">Enfin, nous ajouter une méthode qui vérifie certaines opérations de l’objet blob à l’aide d’une signature d’accès partagé sur un objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="bad31-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="bad31-191">Dans ce cas, nous utilisons le constructeur de hello **CloudBlockBlob(String)**, en passant la signature d’accès partagé hello, tooreturn un objet blob toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="bad31-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="bad31-192">Aucune authentification n’est requise ; Il est basé sur la signature hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="bad31-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="bad31-193">Ajoutez hello suivant tooProgram.cs de méthode :</span><span class="sxs-lookup"><span data-stu-id="bad31-193">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="bad31-194">Hello de mise à jour **Main()** méthode toocall **UseBlobSAS()** avec deux hello partagé des signatures d’accès que vous avez créé sur l’objet blob de hello :</span><span class="sxs-lookup"><span data-stu-id="bad31-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="bad31-195">Exécutez l’application de console hello et observez les toosee de sortie hello quelles opérations sont autorisées pour les signatures.</span><span class="sxs-lookup"><span data-stu-id="bad31-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="bad31-196">sortie Hello dans la fenêtre de console hello ressemblera similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="bad31-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="bad31-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bad31-197">Next Steps</span></span>

* [<span data-ttu-id="bad31-198">Signatures d’accès partagé, partie 1 : Hello de présentation modèle SAP</span><span class="sxs-lookup"><span data-stu-id="bad31-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="bad31-199">Gérer les objets BLOB et l’accès en lecture anonyme toocontainers</span><span class="sxs-lookup"><span data-stu-id="bad31-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="bad31-200">Délégation de l’accès avec une signature d’accès partagé (API REST)</span><span class="sxs-lookup"><span data-stu-id="bad31-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="bad31-201">Présentation des signatures d’accès partagé de table et de file d’attente</span><span class="sxs-lookup"><span data-stu-id="bad31-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
