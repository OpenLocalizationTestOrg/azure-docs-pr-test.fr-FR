---
title: "Didacticiel : Chiffrement et déchiffrement d’objets blob dans le service Stockage Azure à l’aide d’Azure Key Vault | Microsoft Docs"
description: "Comment tooencrypt et déchiffrer un objet blob à l’aide du chiffrement côté client pour le stockage Microsoft Azure avec Azure Key Vault."
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
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="fe302-103">Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l'aide d'Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="fe302-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="fe302-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="fe302-104">Introduction</span></span>
<span data-ttu-id="fe302-105">Ce didacticiel décrit comment utiliser des toomake de chiffrement de stockage côté client avec Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe302-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="fe302-106">Il vous guide dans la procédure tooencrypt et déchiffrer un objet blob dans une application console à l’aide de ces technologies.</span><span class="sxs-lookup"><span data-stu-id="fe302-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="fe302-107">**Estimation du temps toocomplete :** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="fe302-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="fe302-108">Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](../../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe302-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="fe302-109">Pour plus d’informations générales sur le chiffrement côté client du Stockage Azure, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe302-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe302-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fe302-110">Prerequisites</span></span>
<span data-ttu-id="fe302-111">toocomplete ce didacticiel, vous devez avoir hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fe302-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="fe302-112">Un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="fe302-112">An Azure Storage account</span></span>
* <span data-ttu-id="fe302-113">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="fe302-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="fe302-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe302-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="fe302-115">Vue d’ensemble du chiffrement côté client</span><span class="sxs-lookup"><span data-stu-id="fe302-115">Overview of client-side encryption</span></span>
<span data-ttu-id="fe302-116">Pour une vue d’ensemble du chiffrement côté client du Stockage Azure, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="fe302-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="fe302-117">Voici une brève description du fonctionnement du chiffrement côté client :</span><span class="sxs-lookup"><span data-stu-id="fe302-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="fe302-118">client de stockage Azure Hello SDK génère une clé de chiffrement de contenu (CEK), qui est une clé symétrique usage unique.</span><span class="sxs-lookup"><span data-stu-id="fe302-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="fe302-119">Les données du client sont chiffrées à l’aide de cette clé de chiffrement de contenu.</span><span class="sxs-lookup"><span data-stu-id="fe302-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="fe302-120">Hello CEK est ensuite encapsulée (chiffré) à l’aide de la clé de chiffrement à clé hello (KEK).</span><span class="sxs-lookup"><span data-stu-id="fe302-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="fe302-121">Hello veillent est identifié par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique et peut être géré localement ou stockée dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fe302-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="fe302-122">client de stockage Hello lui-même n’a jamais accès toohello de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="fe302-123">Il appelle simplement algorithme hello encapsulage de clé fourni par le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="fe302-124">Les clients peuvent choisir toouse des fournisseurs personnalisés pour la clé d’habillage/Désencapsulation s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="fe302-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="fe302-125">Hello données chiffrées seront ensuite téléchargé toohello le service Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fe302-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="fe302-126">Configurer votre coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="fe302-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="fe302-127">Dans l’ordre des tooproceed avec ce didacticiel, vous devez hello toodo comme suit, qui sont décrites dans le didacticiel de hello [prise en main d’Azure Key Vault](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="fe302-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="fe302-128">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="fe302-128">Create a key vault.</span></span>
* <span data-ttu-id="fe302-129">Ajouter une clé ou un coffre de clés secrètes toohello.</span><span class="sxs-lookup"><span data-stu-id="fe302-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="fe302-130">Inscription d’une application auprès d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe302-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="fe302-131">Autoriser hello application toouse hello clé ou le secret.</span><span class="sxs-lookup"><span data-stu-id="fe302-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="fe302-132">Vérifiez la note de hello ClientID et ClientSecret qui ont été générés lors de l’inscription d’une application avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe302-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="fe302-133">Créez les clés dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="fe302-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="fe302-134">Pour le reste de hello du didacticiel de hello, nous supposons que vous avez utilisé hello nom : ContosoKeyVault et TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="fe302-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="fe302-135">Création d’une application console avec les packages et AppSettings</span><span class="sxs-lookup"><span data-stu-id="fe302-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="fe302-136">Dans Visual Studio, créez une application console.</span><span class="sxs-lookup"><span data-stu-id="fe302-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="fe302-137">Ajouter les packages nuget nécessaires dans la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="fe302-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="fe302-138">Ajoutez AppSettings toohello App.Config.</span><span class="sxs-lookup"><span data-stu-id="fe302-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="fe302-139">Ajoutez hello suivant `using` tooadd que de créer une référence de projet de toohello tooSystem.Configuration et les instructions.</span><span class="sxs-lookup"><span data-stu-id="fe302-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="fe302-140">Ajouter un tooget méthode une application de console tooyour jeton</span><span class="sxs-lookup"><span data-stu-id="fe302-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="fe302-141">Hello méthode suivante est utilisée par les classes de coffre de clés qui doivent tooauthenticate pour coffre de clés tooyour accès.</span><span class="sxs-lookup"><span data-stu-id="fe302-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="fe302-142">Accéder à Storage et à Key Vault dans votre programme</span><span class="sxs-lookup"><span data-stu-id="fe302-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="fe302-143">Bonjour fonction Main, ajoutez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="fe302-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="fe302-144">Modèles d'objet Key Vault</span><span class="sxs-lookup"><span data-stu-id="fe302-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="fe302-145">Il est important qu’il n’y a en fait deux objets de coffre de clés de toounderstand modèles toobe prenant en charge de : une est basée sur hello l’API REST (espace de noms KeyVault) et hello autres est une extension pour le chiffrement côté client.</span><span class="sxs-lookup"><span data-stu-id="fe302-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="fe302-146">Hello clé de coffre Client interagit avec l’API REST de hello et comprend les clés Web JSON et les codes secrets pour hello deux types d’éléments contenus dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="fe302-147">Extensions de coffre de clé Hello sont des classes qui semblent spécifiquement créés pour le chiffrement côté client dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fe302-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="fe302-148">Elles contiennent une interface pour les clés (IKey) et les classes basées sur le concept de hello de clé d’un programme de résolution.</span><span class="sxs-lookup"><span data-stu-id="fe302-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="fe302-149">Il existe deux implémentations de IKey que vous avez besoin de tooknow : RSAKey et SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="fe302-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="fe302-150">Maintenant qu’ils se toocoincide avec les éléments hello qui sont contenus dans un coffre de clés, mais à ce stade sont des classes indépendantes (de sorte que hello clé et clé secrète récupérées par hello Client de coffre de clé n’implémentent pas IKey).</span><span class="sxs-lookup"><span data-stu-id="fe302-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="fe302-151">Chiffrement et téléchargement d’objets blob </span><span class="sxs-lookup"><span data-stu-id="fe302-151">Encrypt blob and upload</span></span>
<span data-ttu-id="fe302-152">Ajouter suivant de hello tooencrypt un objet blob de code et le télécharger compte de stockage Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="fe302-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="fe302-153">Hello **ResolveKeyAsync** méthode utilisé renvoie un IKey.</span><span class="sxs-lookup"><span data-stu-id="fe302-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="fe302-154">Voici une capture d’écran de hello [portail classique Azure](https://manage.windowsazure.com) pour un objet blob qui ont été chiffré à l’aide du chiffrement côté client avec une clé stockée dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="fe302-155">Hello **KeyId** propriété est hello URI de la clé de hello dans le coffre de clés qui agit en tant que hello de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="fe302-156">Hello **EncryptedKey** propriété contient une version chiffrée de la clé CEK de hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe302-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Capture d'écran présentant des métadonnées d'objets blob qui incluent des métadonnées de chiffrement](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="fe302-158">Si vous examinez le constructeur de BlobEncryptionPolicy hello, vous verrez qu’il peut accepter une clé et/ou un programme de résolution.</span><span class="sxs-lookup"><span data-stu-id="fe302-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="fe302-159">Rappelez-vous que vous ne pouvez pas utiliser un programme de résolution pour le chiffrement, car celui-ci ne prend pour l’instant pas en charge de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="fe302-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="fe302-160">Déchiffrement et téléchargement d’objets blob</span><span class="sxs-lookup"><span data-stu-id="fe302-160">Decrypt blob and download</span></span>
<span data-ttu-id="fe302-161">Le déchiffrement est réellement lorsque l’à l’aide de hello résolveur classes ont un sens.</span><span class="sxs-lookup"><span data-stu-id="fe302-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="fe302-162">ID de Hello de clé de chiffrement hello étant associée au blob hello dans ses métadonnées, il est inutile de clé hello tooretrieve et n’oubliez pas d’association hello entre la clé et les objets blob.</span><span class="sxs-lookup"><span data-stu-id="fe302-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="fe302-163">Il vous suffit de toomake que cette clé hello reste dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="fe302-164">clé privée Hello un reste de la clé RSA dans le coffre de clés, par conséquent, pour le déchiffrement toooccur, hello chiffrée de clé à partir des métadonnées d’objet blob hello qui contient la clé CEK est envoyé tooKey coffre pour le déchiffrement de hello.</span><span class="sxs-lookup"><span data-stu-id="fe302-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="fe302-165">Ajoutez hello suivant blob hello toodecrypt que vous venez de télécharger.</span><span class="sxs-lookup"><span data-stu-id="fe302-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="fe302-166">Il existe deux autres types de gestion de clés toomake programmes de résolution plus facile, y compris : AggregateKeyResolver et CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="fe302-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="fe302-167">Utiliser les secrets Key Vault</span><span class="sxs-lookup"><span data-stu-id="fe302-167">Use Key Vault secrets</span></span>
<span data-ttu-id="fe302-168">Hello moyen toouse un secret avec le chiffrement côté client est via hello SymmetricKey classe, car une clé secrète est essentiellement une clé symétrique.</span><span class="sxs-lookup"><span data-stu-id="fe302-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="fe302-169">Toutefois, comme indiqué ci-dessus, une clé secrète dans le coffre de clés ne mappe pas exactement tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="fe302-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="fe302-170">Il existe quelques éléments toounderstand :</span><span class="sxs-lookup"><span data-stu-id="fe302-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="fe302-171">clé Hello dans un SymmetricKey a toobe une longueur fixe : 128, 192, 256, 384 ou 512 bits.</span><span class="sxs-lookup"><span data-stu-id="fe302-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="fe302-172">clé de Hello dans un SymmetricKey doit être codé en Base64.</span><span class="sxs-lookup"><span data-stu-id="fe302-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="fe302-173">Un secret de coffre de clés qui sera utilisé comme un SymmetricKey doit toohave un Type de contenu de « application/octet-stream » dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="fe302-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="fe302-174">Voici un exemple de création de secret dans Key Vault, effectuée dans PowerShell, qui peut être utilisé comme une valeur SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="fe302-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="fe302-175">Notez que la valeur hello dur codé, $key, est uniquement à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="fe302-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="fe302-176">Dans votre propre code vous souhaiterez toogenerate cette clé.</span><span class="sxs-lookup"><span data-stu-id="fe302-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="fe302-177">Dans votre application console, vous pouvez utiliser hello même appeler comme avant tooretrieve ce secret principal en tant qu’un SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="fe302-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="fe302-178">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="fe302-178">That's it.</span></span> <span data-ttu-id="fe302-179">Vous n’avez plus qu’à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="fe302-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe302-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe302-180">Next steps</span></span>
<span data-ttu-id="fe302-181">Pour plus d’informations sur l’utilisation du Stockage Microsoft Azure avec C#, consultez [Bibliothèque cliente Stockage Microsoft Azure pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe302-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="fe302-182">Pour plus d’informations sur hello API REST d’objets Blob, consultez [API REST du Service Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe302-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="fe302-183">Hello dernières informations sur Microsoft Azure Storage, accédez à toohello [Blog de l’équipe Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="fe302-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
