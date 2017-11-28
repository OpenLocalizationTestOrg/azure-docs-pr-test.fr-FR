---
title: "Didacticiel : Chiffrement et déchiffrement d’objets blob dans le service Stockage Azure à l’aide d’Azure Key Vault | Microsoft Docs"
description: "Comment chiffrer et déchiffrer un objet blob en utilisant le chiffrement côté client pour le service Stockage Microsoft Azure avec Azure Key Vault."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: 0c33742a0212e670072a947a2d2ab8304c77b973
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="8f349-103">Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l'aide d'Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f349-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="8f349-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="8f349-104">Introduction</span></span>
<span data-ttu-id="8f349-105">Ce didacticiel décrit comment utiliser le chiffrement de stockage côté client avec Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="8f349-106">Il vous explique comment chiffrer et déchiffrer un objet blob dans une application console à l'aide de ces technologies.</span><span class="sxs-lookup"><span data-stu-id="8f349-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="8f349-107">**Durée estimée :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="8f349-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="8f349-108">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f349-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="8f349-109">Pour plus d’informations générales sur le chiffrement côté client du Stockage Azure, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="8f349-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f349-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8f349-110">Prerequisites</span></span>
<span data-ttu-id="8f349-111">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8f349-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="8f349-112">Un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8f349-112">An Azure Storage account</span></span>
* <span data-ttu-id="8f349-113">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="8f349-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="8f349-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f349-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="8f349-115">Vue d’ensemble du chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="8f349-115">Overview of client-side encryption</span></span>
<span data-ttu-id="8f349-116">Pour une vue d’ensemble du chiffrement côté client du Stockage Azure, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="8f349-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="8f349-117">Voici une brève description du fonctionnement du chiffrement côté client :</span><span class="sxs-lookup"><span data-stu-id="8f349-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="8f349-118">Le Kit de développement logiciel (SDK) client d’Azure Storage génère une clé de chiffrement de contenu (CEK) qui est une clé symétrique à usage unique.</span><span class="sxs-lookup"><span data-stu-id="8f349-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="8f349-119">Les données du client sont chiffrées à l’aide de cette clé de chiffrement de contenu.</span><span class="sxs-lookup"><span data-stu-id="8f349-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="8f349-120">La clé de chiffrement de contenu est ensuite encapsulée (chiffrée) à l’aide de la clé de chiffrement de clés (KEK).</span><span class="sxs-lookup"><span data-stu-id="8f349-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="8f349-121">La clé de chiffrement de clés est identifiée par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique pouvant être gérée localement ou stockée dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="8f349-122">Le client Storage n’a jamais accès à la clé de chiffrement de clés.</span><span class="sxs-lookup"><span data-stu-id="8f349-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="8f349-123">Il appelle simplement l'algorithme d’encapsulage de clés fourni par Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="8f349-124">Si besoin est, les clients peuvent choisir d’utiliser des fournisseurs personnalisés pour l’encapsulage/le désencapsulage de clés.</span><span class="sxs-lookup"><span data-stu-id="8f349-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="8f349-125">Les données chiffrées sont ensuite téléchargées sur le service Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8f349-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="8f349-126">Configurer votre coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="8f349-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="8f349-127">Pour continuer avec ce didacticiel, vous devez effectuer les étapes suivantes qui sont décrites dans le didacticiel [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md) :</span><span class="sxs-lookup"><span data-stu-id="8f349-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="8f349-128">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="8f349-128">Create a key vault.</span></span>
* <span data-ttu-id="8f349-129">Ajout d’une clé ou d’un secret au coffre de clés</span><span class="sxs-lookup"><span data-stu-id="8f349-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="8f349-130">Inscription d’une application auprès d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f349-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="8f349-131">Autorisation de l’application à utiliser la clé ou le secret</span><span class="sxs-lookup"><span data-stu-id="8f349-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="8f349-132">Notez les valeurs ClientID et ClientSecret qui ont été générées lors de l'inscription d'une application avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f349-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="8f349-133">Créez les deux clés dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="8f349-133">Create both keys in the key vault.</span></span> <span data-ttu-id="8f349-134">Pour la suite du didacticiel, nous partons du principe que vous avez utilisé les noms suivants : ContosoKeyVault et TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="8f349-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="8f349-135">Création d’une application console avec les packages et AppSettings</span><span class="sxs-lookup"><span data-stu-id="8f349-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="8f349-136">Dans Visual Studio, créez une application console.</span><span class="sxs-lookup"><span data-stu-id="8f349-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="8f349-137">Ajoutez les packages nuget nécessaires dans la Console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="8f349-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="8f349-138">Ajoutez la section AppSettings au fichier App.Config.</span><span class="sxs-lookup"><span data-stu-id="8f349-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="8f349-139">Ajoutez les instructions `using` suivantes et assurez-vous d’ajouter une référence à l’assembly System.Configuration du projet.</span><span class="sxs-lookup"><span data-stu-id="8f349-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="8f349-140">Ajouter une méthode pour obtenir un jeton pour votre application console</span><span class="sxs-lookup"><span data-stu-id="8f349-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="8f349-141">La méthode suivante est utilisée par les classes Key Vault qui doivent s’authentifier pour accéder à votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="8f349-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="8f349-142">Accéder à Storage et à Key Vault dans votre programme</span><span class="sxs-lookup"><span data-stu-id="8f349-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="8f349-143">Dans la fonction Main, ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="8f349-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="8f349-144">Modèles d'objet Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f349-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="8f349-145">Il est important de comprendre qu'il n'y a que deux modèles d'objet Key Vault à connaître : l’un est basé sur l'API REST (espace de noms KeyVault) et l'autre est une extension pour le chiffrement côté client.</span><span class="sxs-lookup"><span data-stu-id="8f349-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="8f349-146">Le client Key Vault interagit avec l’API REST et comprend les secrets et les clés web JSON pour les deux genres d’éléments qui sont contenus dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="8f349-147">Les extensions Key Vault sont des classes qui semblent avoir été créées spécifiquement pour le chiffrement côté client dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8f349-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="8f349-148">Elles contiennent une interface pour les clés (IKey) et des classes basées sur le concept d’un programme de résolution de clés.</span><span class="sxs-lookup"><span data-stu-id="8f349-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="8f349-149">Il existe deux implémentations d’IKey à connaître : RSAKey et SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="8f349-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="8f349-150">Elles coïncident désormais avec les éléments contenus dans un coffre de clés, mais à ce stade, ce sont des classes indépendantes (la clé et le secret récupérés par le client Key Vault n'implémentent donc pas IKey).</span><span class="sxs-lookup"><span data-stu-id="8f349-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="8f349-151">Chiffrement et téléchargement d’objets blob </span><span class="sxs-lookup"><span data-stu-id="8f349-151">Encrypt blob and upload</span></span>
<span data-ttu-id="8f349-152">Ajoutez le code suivant pour chiffrer un objet blob et le télécharger sur votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8f349-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="8f349-153">La méthode **ResolveKeyAsync** utilisée renvoie un IKey.</span><span class="sxs-lookup"><span data-stu-id="8f349-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="8f349-154">Voici une capture d’écran du [portail Azure Classic](https://manage.windowsazure.com) pour un objet blob qui a été chiffré à l’aide du chiffrement côté client avec une clé stockée dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="8f349-155">La propriété **KeyId** est l’URI de la clé dans Key Vault qui fait office de clé de chiffrement de clés (KEK).</span><span class="sxs-lookup"><span data-stu-id="8f349-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="8f349-156">La propriété **EncryptedKey** contient la version chiffrée de la clé de chiffrement de contenu (CEK).</span><span class="sxs-lookup"><span data-stu-id="8f349-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Capture d'écran présentant des métadonnées d'objets blob qui incluent des métadonnées de chiffrement](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="8f349-158">Si vous examinez le constructeur BlobEncryptionPolicy, vous remarquerez qu'il peut accepter une clé et/ou un programme de résolution.</span><span class="sxs-lookup"><span data-stu-id="8f349-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="8f349-159">Rappelez-vous que vous ne pouvez pas utiliser un programme de résolution pour le chiffrement, car celui-ci ne prend pour l’instant pas en charge de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="8f349-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="8f349-160">Déchiffrement et téléchargement d’objets blob</span><span class="sxs-lookup"><span data-stu-id="8f349-160">Decrypt blob and download</span></span>
<span data-ttu-id="8f349-161">Le déchiffrement s’effectue réellement quand les classes du programme de résolution sont pertinentes.</span><span class="sxs-lookup"><span data-stu-id="8f349-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="8f349-162">L’ID de la clé utilisée pour le chiffrement est associé à l’objet blob dans ses métadonnées. Il est donc inutile de récupérer la clé et de mémoriser l’association entre la clé et les objets blob.</span><span class="sxs-lookup"><span data-stu-id="8f349-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="8f349-163">Il vous suffit de vous assurer que la clé reste bien dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="8f349-164">La clé privée d’une clé RSA reste dans Key Vault. Ainsi, la clé chiffrée des métadonnées d’objets blob qui contient la clé de chiffrement de contenu (CEK) est envoyée à Key Vault pour que le déchiffrement puisse avoir lieu.</span><span class="sxs-lookup"><span data-stu-id="8f349-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="8f349-165">Ajoutez le code suivant pour déchiffrer l’objet blob que vous venez de télécharger.</span><span class="sxs-lookup"><span data-stu-id="8f349-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="8f349-166">Il existe deux autres genres de programmes de résolution vous permettant de gérer plus facilement vos clés, à savoir : AggregateKeyResolver et CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="8f349-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="8f349-167">Utiliser les secrets Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f349-167">Use Key Vault secrets</span></span>
<span data-ttu-id="8f349-168">L’utilisation d’un secret avec le chiffrement côté client s’effectue via la classe SymmetricKey, car un secret est essentiellement une clé symétrique.</span><span class="sxs-lookup"><span data-stu-id="8f349-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="8f349-169">Mais, comme indiqué ci-dessus, un secret dans Key Vault ne correspond pas exactement à une valeur SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="8f349-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="8f349-170">Plusieurs choses sont à savoir ici :</span><span class="sxs-lookup"><span data-stu-id="8f349-170">There are a few things to understand:</span></span>

* <span data-ttu-id="8f349-171">La clé d’une valeur SymmetricKey doit avoir une longueur fixe : 128, 192, 256, 384 ou 512 bits.</span><span class="sxs-lookup"><span data-stu-id="8f349-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="8f349-172">La clé d’une valeur SymmetricKey doit être codée en Base64.</span><span class="sxs-lookup"><span data-stu-id="8f349-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="8f349-173">Un secret Key Vault qui est utilisé comme une valeur SymmetricKey doit avoir un type de contenu « application/octet-stream » dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f349-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="8f349-174">Voici un exemple de création de secret dans Key Vault, effectuée dans PowerShell, qui peut être utilisé comme une valeur SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="8f349-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="8f349-175">Veuillez noter que la valeur codée en dur, $key, est fournie uniquement à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="8f349-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="8f349-176">Dans votre propre code, vous devez générer cette clé.</span><span class="sxs-lookup"><span data-stu-id="8f349-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="8f349-177">Dans votre application console, vous pouvez utiliser le même appel qu’auparavant pour récupérer ce secret comme une valeur SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="8f349-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="8f349-178">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="8f349-178">That's it.</span></span> <span data-ttu-id="8f349-179">Vous n’avez plus qu’à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="8f349-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f349-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f349-180">Next steps</span></span>
<span data-ttu-id="8f349-181">Pour plus d’informations sur l’utilisation du Stockage Microsoft Azure avec C#, consultez [Bibliothèque cliente Stockage Microsoft Azure pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f349-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="8f349-182">Pour plus d’informations sur l’API REST Blob, consultez [API REST du service BLOB](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f349-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="8f349-183">Pour obtenir les dernières informations sur Stockage Microsoft Azure, consultez le [Blog de l’équipe Stockage Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="8f349-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
