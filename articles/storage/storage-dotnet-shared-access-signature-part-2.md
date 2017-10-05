---
title: "Créer et utiliser une signature d’accès partagé (SAP) avec le Stockage Blob Azure | Documents Microsoft"
description: "Ce didacticiel vous montre comment créer des signatures d’accès partagé en vue d’une utilisation avec Stockage Blob et comment les utiliser dans vos applications clientes."
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
ms.openlocfilehash: ba78dd2bbcc68ffffeba59b1623891126baf656f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="c9b67-103">Signatures d’accès partagé, partie 2 : créer et utiliser une signature d’accès partagé avec Blob Storage</span><span class="sxs-lookup"><span data-stu-id="c9b67-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="c9b67-104">[partie 1](storage-dotnet-shared-access-signature-part-1.md) de ce didacticiel traitait des signatures d'accès partagé et indiquait les meilleures pratiques les concernant.</span><span class="sxs-lookup"><span data-stu-id="c9b67-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="c9b67-105">La partie 2 indique comment générer et utiliser les signatures d’accès partagé avec Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c9b67-105">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="c9b67-106">Les exemples ont été écrits en C# et utilisent la bibliothèque du client Azure Storage pour .NET.</span><span class="sxs-lookup"><span data-stu-id="c9b67-106">The examples are written in C# and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="c9b67-107">Le didacticiel traite des points suivants :</span><span class="sxs-lookup"><span data-stu-id="c9b67-107">The examples in this tutorial:</span></span>

* <span data-ttu-id="c9b67-108">Générer une signature d'accès partagé sur un conteneur</span><span class="sxs-lookup"><span data-stu-id="c9b67-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="c9b67-109">Générer une signature d'accès partagé sur un blob</span><span class="sxs-lookup"><span data-stu-id="c9b67-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="c9b67-110">Créer une stratégie d’accès afin de gérer les signatures sur les ressources d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="c9b67-110">Create a stored access policy to manage signatures on a container's resources</span></span>
* <span data-ttu-id="c9b67-111">Tester les signatures d’accès partagé dans une application cliente</span><span class="sxs-lookup"><span data-stu-id="c9b67-111">Test the shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="c9b67-112">À propos de ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="c9b67-112">About this tutorial</span></span>
<span data-ttu-id="c9b67-113">Au cours de ce didacticiel, nous allons créer deux consoles d’application qui présentent la création et l’utilisation des signatures d’accès partagé pour les conteneurs et les blobs :</span><span class="sxs-lookup"><span data-stu-id="c9b67-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="c9b67-114">**Application n°1** : l’application de gestion.</span><span class="sxs-lookup"><span data-stu-id="c9b67-114">**Application 1**: The management application.</span></span> <span data-ttu-id="c9b67-115">Elle génère une signature d’accès partagé pour un conteneur et un blob.</span><span class="sxs-lookup"><span data-stu-id="c9b67-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="c9b67-116">Elle inclut la clé d’accès au compte de stockage dans le code source.</span><span class="sxs-lookup"><span data-stu-id="c9b67-116">Includes the storage account access key in source code.</span></span>

<span data-ttu-id="c9b67-117">**Application n°2** : l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="c9b67-117">**Application 2**: The client application.</span></span> <span data-ttu-id="c9b67-118">Elle accède aux ressources du conteneur et du blob à l’aide des signatures d’accès partagé, créées grâce à la première application.</span><span class="sxs-lookup"><span data-stu-id="c9b67-118">Accesses container and blob resources using the shared access signatures created with the first application.</span></span> <span data-ttu-id="c9b67-119">Elle utilise uniquement les signatures d’accès partagé pour accéder aux ressources du conteneur et du blob. La clé d’accès au compte de stockage *n’est pas* incluse.</span><span class="sxs-lookup"><span data-stu-id="c9b67-119">Uses only the shared access signatures to access container and blob resources--it does *not* include the storage account access key.</span></span>

## <a name="part-1-create-a-console-application-to-generate-shared-access-signatures"></a><span data-ttu-id="c9b67-120">Première partie : créer une application console pour générer des signatures d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="c9b67-120">Part 1: Create a console application to generate shared access signatures</span></span>
<span data-ttu-id="c9b67-121">Commencez par vérifier que la bibliothèque cliente Azure Storage pour .NET est installée.</span><span class="sxs-lookup"><span data-stu-id="c9b67-121">First, ensure that you have the Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="c9b67-122">Vous pouvez installer le [package NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "package NuGet") qui contient les assemblies les plus récentes pour la bibliothèque cliente.</span><span class="sxs-lookup"><span data-stu-id="c9b67-122">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library.</span></span> <span data-ttu-id="c9b67-123">Il s’agit de la méthode recommandée pour vérifier que vous disposez des correctifs les plus récents.</span><span class="sxs-lookup"><span data-stu-id="c9b67-123">This is the recommended method for ensuring that you have the most recent fixes.</span></span> <span data-ttu-id="c9b67-124">Vous pouvez également télécharger la bibliothèque cliente avec la version la plus récente du [Kit de développement logiciel (SDK) Azure pour .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c9b67-124">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="c9b67-125">Dans Visual Studio, créez une application console Windows et nommez-la **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="c9b67-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="c9b67-126">Ajoutez des références à [Microsoft.WindowsAzure.Configuration.dll](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) et [Microsoft.WindowsAzure.Storage.dll](https://www.nuget.org/packages/WindowsAzure.Storage/) en utilisant l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9b67-126">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of the following approaches:</span></span>

* <span data-ttu-id="c9b67-127">Utilisez le [gestionnaire des packages NuGet](https://docs.nuget.org/consume/installing-nuget) dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9b67-127">Use the [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="c9b67-128">Sélectionnez **Projet** > **Gérer les packages NuGet**, puis effectuez une recherche en ligne pour chaque package (Microsoft.WindowsAzure.ConfigurationManager et WindowsAzure.Storage), et installez-les.</span><span class="sxs-lookup"><span data-stu-id="c9b67-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="c9b67-129">Vous pouvez également rechercher ces assemblies dans l’installation de votre Kit de développement logiciel Azure SDK et y ajouter des références :</span><span class="sxs-lookup"><span data-stu-id="c9b67-129">Alternatively, locate these assemblies in your installation of the Azure SDK and add references to them:</span></span>
  * <span data-ttu-id="c9b67-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="c9b67-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="c9b67-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="c9b67-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="c9b67-132">Au tout début du fichier Program.cs, ajoutez les directives **d’utilisation** suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9b67-132">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="c9b67-133">Modifiez le fichier app.config pour qu'il contienne un paramètre de configuration avec une chaîne de connexion qui pointe vers votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c9b67-133">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span></span> <span data-ttu-id="c9b67-134">Votre fichier app.config ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="c9b67-134">Your app.config file should look similar to this one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="c9b67-135">Générer une URI de signature d’accès partagé pour un conteneur</span><span class="sxs-lookup"><span data-stu-id="c9b67-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="c9b67-136">Pour commencer, nous allons ajouter une méthode pour générer une signature d'accès partagé sur un nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="c9b67-136">To begin with, we add a method to generate a shared access signature on a new container.</span></span> <span data-ttu-id="c9b67-137">Ici, la signature n'est pas associée à une stratégie d'accès stocké. C’est pourquoi elle reporte sur l’URI les informations concernant son heure d’expiration et les autorisations qu’elle accorde.</span><span class="sxs-lookup"><span data-stu-id="c9b67-137">In this case, the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions it grants.</span></span>

<span data-ttu-id="c9b67-138">Ajoutons du code à la méthode **Main()** pour authentifier l'accès à votre compte de stockage et créer un conteneur :</span><span class="sxs-lookup"><span data-stu-id="c9b67-138">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls to the methods created below here...

    //Require user input before closing the console window.
    Console.ReadLine();
}
```

<span data-ttu-id="c9b67-139">Ensuite, ajoutez une nouvelle méthode qui génère la signature d'accès partagé pour le conteneur et renvoie l'URI de signature :</span><span class="sxs-lookup"><span data-stu-id="c9b67-139">Next, add a method that generates the shared access signature for the container and returns the signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set the expiry time and permissions for the container.
    //In this case no start time is specified, so the shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="c9b67-140">Ajoutez les lignes suivantes à la fin de la méthode **Main()** avant d’appeler **Console.ReadLine()** pour appeler **GetContainerSasUri()** et écrire l’URI de la signature dans la fenêtre de la console :</span><span class="sxs-lookup"><span data-stu-id="c9b67-140">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for the container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="c9b67-141">Compilez et exécutez pour renvoyer l'URI de la signature d'accès partagé pour le nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="c9b67-141">Compile and run to output the shared access signature URI for the new container.</span></span> <span data-ttu-id="c9b67-142">L’URI ressemblera à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c9b67-142">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="c9b67-143">Dès lors que le code est exécuté, la signature d’accès partagé que vous avez créée pour le conteneur sera valide durant les prochaines 24 heures.</span><span class="sxs-lookup"><span data-stu-id="c9b67-143">Once you have run the code, the shared access signature you created for the container will be valid for the next 24 hours.</span></span> <span data-ttu-id="c9b67-144">La signature accorde une autorisation client pour lister des blobs dans le conteneur et pour écrire de nouveaux blobs dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="c9b67-144">The signature grants a client permission to list blobs in the container and to write new blobs to the container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="c9b67-145">Générer une URI de signature d’accès partagé pour un blob</span><span class="sxs-lookup"><span data-stu-id="c9b67-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="c9b67-146">Nous allons ensuite écrire un code similaire afin de créer un blob au sein du conteneur et lui générer une signature d'accès partagé.</span><span class="sxs-lookup"><span data-stu-id="c9b67-146">Next, we write similar code to create a new blob within the container and generate a shared access signature for it.</span></span> <span data-ttu-id="c9b67-147">Cette signature d'accès partagé n'est pas associée à une stratégie d'accès stocké. C’est pourquoi elle inclut dans l’URI l’heure de début, l’heure d’expiration et les informations concernant l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c9b67-147">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information in the URI.</span></span>

<span data-ttu-id="c9b67-148">Ajoutez une nouvelle méthode qui crée un blob et y écrit quelques textes, puis génère une signature d’accès partagé et renvoie l’URI de signature :</span><span class="sxs-lookup"><span data-stu-id="c9b67-148">Add a new method that creates a new blob and writes some text to it, then generates a shared access signature and returns the signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set the expiry time and permissions for the blob.
    //In this case, the start time is specified as a few minutes in the past, to mitigate clock skew.
    //The shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the blob, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="c9b67-149">Ajoutez les lignes suivantes à la fin de la méthode **Main()** avant d’appeler **Console.ReadLine()** pour appeler **GetBlobSasUri()** et écrire l’URI de la signature d’accès partagé dans la fenêtre de la console :</span><span class="sxs-lookup"><span data-stu-id="c9b67-149">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="c9b67-150">Compilez et exécutez pour renvoyer l'URI de la signature d'accès partagé pour le nouvel objet blob.</span><span class="sxs-lookup"><span data-stu-id="c9b67-150">Compile and run to output the shared access signature URI for the new blob.</span></span> <span data-ttu-id="c9b67-151">L’URI ressemblera à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c9b67-151">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-the-container"></a><span data-ttu-id="c9b67-152">Créer une stratégie d’accès stocké sur le conteneur</span><span class="sxs-lookup"><span data-stu-id="c9b67-152">Create a stored access policy on the container</span></span>
<span data-ttu-id="c9b67-153">Créons une stratégie d'accès stockée sur le conteneur pour définir les contraintes des signatures d'accès partagé qui y sont associées.</span><span class="sxs-lookup"><span data-stu-id="c9b67-153">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="c9b67-154">Dans les exemples précédents, nous avons spécifié l'heure de début (implicitement ou explicitement), l'heure d'expiration et les autorisations sur l'URI de la signature d'accès partagé lui-même.</span><span class="sxs-lookup"><span data-stu-id="c9b67-154">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span></span> <span data-ttu-id="c9b67-155">Dans les exemples suivants, nous allons les spécifier sur la stratégie d'accès stocké, et non sur la signature d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="c9b67-155">In the following examples, we specify these on the stored access policy, not on the shared access signature.</span></span> <span data-ttu-id="c9b67-156">Cela nous permettra de modifier ces contraintes sans devoir émettre de nouveau la signature d'accès partagé.</span><span class="sxs-lookup"><span data-stu-id="c9b67-156">Doing so enables us to change these constraints without reissuing the shared access signature.</span></span>

<span data-ttu-id="c9b67-157">Il est possible de définir sur la signature d’accès partagé un certain nombre de contraintes et de définir le reste sur la stratégie d’accès stocké.</span><span class="sxs-lookup"><span data-stu-id="c9b67-157">It's possible to have one or more of the constraints on the shared access signature, and the remainder on the stored access policy.</span></span> <span data-ttu-id="c9b67-158">Toutefois, vous ne pouvez spécifier que l’heure de début, l’heure d’expiration et les autorisations dans un emplacement ou un autre.</span><span class="sxs-lookup"><span data-stu-id="c9b67-158">However, you can only specify the start time, expiry time, and permissions in one place or the other.</span></span> <span data-ttu-id="c9b67-159">Par exemple, vous ne pouvez pas spécifier d’autorisations sur la signature d’accès partagé et dans le même temps, les spécifier sur une stratégie d’accès stocké.</span><span class="sxs-lookup"><span data-stu-id="c9b67-159">For example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span></span>

<span data-ttu-id="c9b67-160">Lorsque vous ajoutez une stratégie d’accès stocké à un conteneur, vous devez obtenir les autorisations existantes du conteneur, ajouter la nouvelle stratégie d’accès et ensuite configurer les autorisations du conteneur.</span><span class="sxs-lookup"><span data-stu-id="c9b67-160">When you add a stored access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span></span>

<span data-ttu-id="c9b67-161">Ajoutez une nouvelle méthode qui crée une stratégie d’accès stockée sur un conteneur et renvoie le nom de la stratégie :</span><span class="sxs-lookup"><span data-stu-id="c9b67-161">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get the container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="c9b67-162">À la fin de la méthode **Main()**, avant d’appeler **Console.ReadLine()**, ajoutez les lignes suivantes pour supprimer dans un premier temps toute stratégie d’accès existante, puis appeler la méthode **CreateSharedAccessPolicy()** :</span><span class="sxs-lookup"><span data-stu-id="c9b67-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies, and then call the **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on the container, which may be optionally used to provide constraints for
//shared access signatures on the container and the blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="c9b67-163">Avant de désactiver les stratégies d’accès sur un conteneur, vous devez obtenir les autorisations existantes du conteneur. Vous pouvez par la suite désactiver les autorisations et en configurer de nouvelles.</span><span class="sxs-lookup"><span data-stu-id="c9b67-163">When you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-the-container-that-uses-an-access-policy"></a><span data-ttu-id="c9b67-164">Générer une URI de signature d’accès partagé sur un conteneur qui utilise une stratégie d’accès</span><span class="sxs-lookup"><span data-stu-id="c9b67-164">Generate a shared access signature URI on the container that uses an access policy</span></span>
<span data-ttu-id="c9b67-165">Nous allons dès à présent créer une nouvelle fois une signature d’accès partagé pour le conteneur créé précédemment. Cette fois-ci, nous allons associer la signature à la stratégie d’accès stocké de l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="c9b67-165">Next, we create another shared access signature for the container that we created earlier, but this time we associate the signature with the stored access policy we created in the previous example.</span></span>

<span data-ttu-id="c9b67-166">Ajouter une nouvelle méthode afin de générer une autre signature d’accès partagé pour le conteneur :</span><span class="sxs-lookup"><span data-stu-id="c9b67-166">Add a new method to generate another shared access signature for the container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate the shared access signature on the container. In this case, all of the constraints for the
    //shared access signature are specified on the stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="c9b67-167">Ajoutez les lignes suivantes à la fin de la méthode **Main()** avant d’appeler **Console.ReadLine()** pour appeler la méthode **GetContainerSasUriWithPolicy** :</span><span class="sxs-lookup"><span data-stu-id="c9b67-167">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-the-blob-that-uses-an-access-policy"></a><span data-ttu-id="c9b67-168">Génération d'un URI de signature d'accès partagé sur l'objet blob qui utilise une stratégie d'accès</span><span class="sxs-lookup"><span data-stu-id="c9b67-168">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span></span>
<span data-ttu-id="c9b67-169">Pour finir, nous allons ajouter une méthode similaire afin de créer un autre blob et générer une signature d’accès partagé, associée à une stratégie d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="c9b67-169">Finally, we add a similar method to create another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="c9b67-170">Ajoutez une nouvelle méthode pour créer un objet blob et générer une signature d'accès partagé :</span><span class="sxs-lookup"><span data-stu-id="c9b67-170">Add a new method to create a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature. " +
    "A stored access policy defines the constraints for the signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate the shared access signature on the blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="c9b67-171">Ajoutez les lignes suivantes à la fin de la méthode **Main()** avant d’appeler **Console.ReadLine()** pour appeler la méthode **GetBlobSasUriWithPolicy** :</span><span class="sxs-lookup"><span data-stu-id="c9b67-171">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="c9b67-172">La méthode **Main()** doit maintenant ressembler à ceci.</span><span class="sxs-lookup"><span data-stu-id="c9b67-172">The **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="c9b67-173">Lancez-la pour écrire les URI de signature d'accès partagé sur la fenêtre de la console, puis copiez et collez-les dans un fichier texte pour les utiliser dans la deuxième partie de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c9b67-173">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for the container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on the container, which may be optionally used to provide constraints for
    //shared access signatures on the container and the blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="c9b67-174">Lorsque vous exécutez l'application console GenerateSharedAccessSignatures, vous verrez une sortie semblable à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c9b67-174">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following.</span></span> <span data-ttu-id="c9b67-175">Il s'agit des signatures d'accès partagé que vous utilisez dans la deuxième partie du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c9b67-175">These are the shared access signatures you use in Part 2 of the tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-to-test-the-shared-access-signatures"></a><span data-ttu-id="c9b67-176">Deuxième partie : créer une application console afin de tester les signatures d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="c9b67-176">Part 2: Create a console application to test the shared access signatures</span></span>
<span data-ttu-id="c9b67-177">Afin de tester les signatures d’accès partagé créées dans les exemples précédents, nous allons créer une deuxième application console qui utilise les signatures pour exécuter les opérations sur le conteneur et sur un blob.</span><span class="sxs-lookup"><span data-stu-id="c9b67-177">To test the shared access signatures created in the previous examples, we create a second console application that uses the signatures to perform operations on the container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="c9b67-178">Si plus de 24 heures se sont écoulées depuis la fin de la première partie de ce didacticiel, les signatures que vous avez générées ne sont plus valides.</span><span class="sxs-lookup"><span data-stu-id="c9b67-178">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span></span> <span data-ttu-id="c9b67-179">Dans ce cas, exécutez le code dans la première application console pour générer de nouvelles signatures d’accès partagé pour la seconde partie du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c9b67-179">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span></span>
>

<span data-ttu-id="c9b67-180">Dans Visual Studio, créez une application console Windows et nommez-la **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="c9b67-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="c9b67-181">Ajoutez des références à [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) et [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), comme précédemment.</span><span class="sxs-lookup"><span data-stu-id="c9b67-181">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="c9b67-182">Au tout début du fichier Program.cs, ajoutez les directives **d’utilisation** suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9b67-182">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="c9b67-183">Dans le corps de la méthode **Main()**, ajoutez les constantes de chaîne suivantes. Cela entraîne une modification des valeurs par les signatures d’accès partagé générées dans la première partie de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c9b67-183">In the body of the **Main()** method, add the following string constants, changing their values to the shared access signatures you generated in part 1 of the tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-to-try-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="c9b67-184">Ajouter une méthode afin de tester les opérations sur un conteneur à l’aide d’une signature d’accès partagé</span><span class="sxs-lookup"><span data-stu-id="c9b67-184">Add a method to try container operations using a shared access signature</span></span>
<span data-ttu-id="c9b67-185">Par la suite, nous allons ajouter une méthode qui teste quelques opérations sur un conteneur à l’aide d’une signature d’accès partagé pour le conteneur.</span><span class="sxs-lookup"><span data-stu-id="c9b67-185">Next, we add a method that tests some container operations using a shared access signature for the container.</span></span> <span data-ttu-id="c9b67-186">La signature d'accès partagé permet de renvoyer une référence au conteneur, authentifiant l'accès au conteneur uniquement sur la base de la signature.</span><span class="sxs-lookup"><span data-stu-id="c9b67-186">The shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span></span>

<span data-ttu-id="c9b67-187">Ajoutez la méthode suivante au fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="c9b67-187">Add the following method to Program.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with the SAS provided.

    //Return a reference to the container using the SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list to store blob URIs returned by a listing operation on the container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob to the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions to the container. ";
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

    //List operation: List the blobs in the container.
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

    //Read operation: Get a reference to one of the blobs in the container and read it.
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

    //Delete operation: Delete a blob in the container.
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

<span data-ttu-id="c9b67-188">Mettez à jour la méthode **Main()** afin d’appeler **UseContainerSAS()** grâce aux deux signatures d’accès partagé créées sur le conteneur :</span><span class="sxs-lookup"><span data-stu-id="c9b67-188">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures you created on the container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-to-try-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="c9b67-189">Ajoutez une méthode pour tester les opérations sur un blob à l’aide d’une signature d'accès partagé</span><span class="sxs-lookup"><span data-stu-id="c9b67-189">Add a method to try blob operations using a shared access signature</span></span>
<span data-ttu-id="c9b67-190">Pour terminer, nous allons ajouter une méthode qui teste quelques opérations sur un blob à l’aide d’une signature d’accès partagé sur le blob.</span><span class="sxs-lookup"><span data-stu-id="c9b67-190">Finally, we add a method that tests some blob operations using a shared access signature on the blob.</span></span> <span data-ttu-id="c9b67-191">Ici, nous utilisons le constructeur **CloudBlockBlob(String)**, en passant dans la signature d'accès partagé, pour renvoyer une référence vers le blob.</span><span class="sxs-lookup"><span data-stu-id="c9b67-191">In this case, we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span></span> <span data-ttu-id="c9b67-192">Aucune autre authentification n'est nécessaire, car l'opération est basée uniquement sur la signature.</span><span class="sxs-lookup"><span data-stu-id="c9b67-192">No other authentication is required; it's based on the signature alone.</span></span>

<span data-ttu-id="c9b67-193">Ajoutez la méthode suivante au fichier Program.cs :</span><span class="sxs-lookup"><span data-stu-id="c9b67-193">Add the following method to Program.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using the SAS provided.

    //Return a reference to the blob using the SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob to the container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions to the blob. ";
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

    //Read operation: Read the contents of the blob.
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

    //Delete operation: Delete the blob.
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

<span data-ttu-id="c9b67-194">Mettez à jour la méthode **Main()** pour appeler **UseBlobSAS()** avec les deux signatures d’accès partagé que vous avez créées sur l’objet blob :</span><span class="sxs-lookup"><span data-stu-id="c9b67-194">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call the test methods with the shared access signatures created on the blob, with and without the access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="c9b67-195">Exécutez l'application console et observez la sortie pour connaître les opérations autorisées en fonction des signatures.</span><span class="sxs-lookup"><span data-stu-id="c9b67-195">Run the console application and observe the output to see which operations are permitted for which signatures.</span></span> <span data-ttu-id="c9b67-196">La sortie dans la fenêtre de la console ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="c9b67-196">The output in the console window will look similar to the following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="c9b67-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9b67-197">Next Steps</span></span>

* [<span data-ttu-id="c9b67-198">Signatures d'accès partagé, partie 1 : présentation du modèle SAP</span><span class="sxs-lookup"><span data-stu-id="c9b67-198">Shared Access Signatures, Part 1: Understanding the SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="c9b67-199">Gestion de l’accès en lecture anonyme aux conteneurs et aux objets blob</span><span class="sxs-lookup"><span data-stu-id="c9b67-199">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="c9b67-200">Délégation de l’accès avec une signature d’accès partagé (API REST)</span><span class="sxs-lookup"><span data-stu-id="c9b67-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="c9b67-201">Présentation des signatures d’accès partagé de table et de file d’attente</span><span class="sxs-lookup"><span data-stu-id="c9b67-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
