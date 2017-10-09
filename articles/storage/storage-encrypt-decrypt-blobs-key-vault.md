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
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l'aide d'Azure Key Vault
## <a name="introduction"></a>Introduction
Ce didacticiel décrit comment utiliser des toomake de chiffrement de stockage côté client avec Azure Key Vault. Il vous guide dans la procédure tooencrypt et déchiffrer un objet blob dans une application console à l’aide de ces technologies.

**Estimation du temps toocomplete :** 20 minutes

Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](../key-vault/key-vault-whatis.md).

Pour plus d’informations générales sur le chiffrement côté client du Stockage Azure, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](storage-client-side-encryption.md).

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez avoir hello suivant :

* Un compte Azure Storage
* Visual Studio 2013 ou une version ultérieure
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Vue d’ensemble du chiffrement côté client
Pour une vue d’ensemble du chiffrement côté client du Stockage Azure, consultez [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](storage-client-side-encryption.md)

Voici une brève description du fonctionnement du chiffrement côté client :

1. client de stockage Azure Hello SDK génère une clé de chiffrement de contenu (CEK), qui est une clé symétrique usage unique.
2. Les données du client sont chiffrées à l’aide de cette clé de chiffrement de contenu.
3. Hello CEK est ensuite encapsulée (chiffré) à l’aide de la clé de chiffrement à clé hello (KEK). Hello veillent est identifié par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique et peut être géré localement ou stockée dans Azure Key Vault. client de stockage Hello lui-même n’a jamais accès toohello de clés. Il appelle simplement algorithme hello encapsulage de clé fourni par le coffre de clés. Les clients peuvent choisir toouse des fournisseurs personnalisés pour la clé d’habillage/Désencapsulation s’ils le souhaitent.
4. Hello données chiffrées seront ensuite téléchargé toohello le service Azure Storage.

## <a name="set-up-your-azure-key-vault"></a>Configurer votre coffre de clés Azure
Dans l’ordre des tooproceed avec ce didacticiel, vous devez hello toodo comme suit, qui sont décrites dans le didacticiel de hello [prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md):

* Création d’un coffre de clés
* Ajouter une clé ou un coffre de clés secrètes toohello.
* Inscription d’une application auprès d’Azure Active Directory
* Autoriser hello application toouse hello clé ou le secret.

Vérifiez la note de hello ClientID et ClientSecret qui ont été générés lors de l’inscription d’une application avec Azure Active Directory.

Créez les clés dans le coffre de clés hello. Pour le reste de hello du didacticiel de hello, nous supposons que vous avez utilisé hello nom : ContosoKeyVault et TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Création d’une application console avec les packages et AppSettings
Dans Visual Studio, créez une application console.

Ajouter les packages nuget nécessaires dans la Console du Gestionnaire de Package de hello.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Ajoutez AppSettings toohello App.Config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Ajoutez hello suivant `using` tooadd que de créer une référence de projet de toohello tooSystem.Configuration et les instructions.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Ajouter un tooget méthode une application de console tooyour jeton
Hello méthode suivante est utilisée par les classes de coffre de clés qui doivent tooauthenticate pour coffre de clés tooyour accès.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Accéder à Storage et à Key Vault dans votre programme
Bonjour fonction Main, ajoutez hello suivant de code.

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
> Modèles d'objet Key Vault
> 
> Il est important qu’il n’y a en fait deux objets de coffre de clés de toounderstand modèles toobe prenant en charge de : une est basée sur hello l’API REST (espace de noms KeyVault) et hello autres est une extension pour le chiffrement côté client.
> 
> Hello clé de coffre Client interagit avec l’API REST de hello et comprend les clés Web JSON et les codes secrets pour hello deux types d’éléments contenus dans le coffre de clés.
> 
> Extensions de coffre de clé Hello sont des classes qui semblent spécifiquement créés pour le chiffrement côté client dans le stockage Azure. Elles contiennent une interface pour les clés (IKey) et les classes basées sur le concept de hello de clé d’un programme de résolution. Il existe deux implémentations de IKey que vous avez besoin de tooknow : RSAKey et SymmetricKey. Maintenant qu’ils se toocoincide avec les éléments hello qui sont contenus dans un coffre de clés, mais à ce stade sont des classes indépendantes (de sorte que hello clé et clé secrète récupérées par hello Client de coffre de clé n’implémentent pas IKey).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Chiffrement et téléchargement d’objets blob 
Ajouter suivant de hello tooencrypt un objet blob de code et le télécharger compte de stockage Azure tooyour. Hello **ResolveKeyAsync** méthode utilisé renvoie un IKey.

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

Voici une capture d’écran de hello [portail classique Azure](https://manage.windowsazure.com) pour un objet blob qui ont été chiffré à l’aide du chiffrement côté client avec une clé stockée dans le coffre de clés. Hello **KeyId** propriété est hello URI de la clé de hello dans le coffre de clés qui agit en tant que hello de clés. Hello **EncryptedKey** propriété contient une version chiffrée de la clé CEK de hello hello.

![Capture d'écran présentant des métadonnées d'objets blob qui incluent des métadonnées de chiffrement](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Si vous examinez le constructeur de BlobEncryptionPolicy hello, vous verrez qu’il peut accepter une clé et/ou un programme de résolution. Rappelez-vous que vous ne pouvez pas utiliser un programme de résolution pour le chiffrement, car celui-ci ne prend pour l’instant pas en charge de clé par défaut.
> 
> 

## <a name="decrypt-blob-and-download"></a>Déchiffrement et téléchargement d’objets blob
Le déchiffrement est réellement lorsque l’à l’aide de hello résolveur classes ont un sens. ID de Hello de clé de chiffrement hello étant associée au blob hello dans ses métadonnées, il est inutile de clé hello tooretrieve et n’oubliez pas d’association hello entre la clé et les objets blob. Il vous suffit de toomake que cette clé hello reste dans le coffre de clés.   

clé privée Hello un reste de la clé RSA dans le coffre de clés, par conséquent, pour le déchiffrement toooccur, hello chiffrée de clé à partir des métadonnées d’objet blob hello qui contient la clé CEK est envoyé tooKey coffre pour le déchiffrement de hello.

Ajoutez hello suivant blob hello toodecrypt que vous venez de télécharger.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Il existe deux autres types de gestion de clés toomake programmes de résolution plus facile, y compris : AggregateKeyResolver et CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Utiliser les secrets Key Vault
Hello moyen toouse un secret avec le chiffrement côté client est via hello SymmetricKey classe, car une clé secrète est essentiellement une clé symétrique. Toutefois, comme indiqué ci-dessus, une clé secrète dans le coffre de clés ne mappe pas exactement tooa SymmetricKey. Il existe quelques éléments toounderstand :

* clé Hello dans un SymmetricKey a toobe une longueur fixe : 128, 192, 256, 384 ou 512 bits.
* clé de Hello dans un SymmetricKey doit être codé en Base64.
* Un secret de coffre de clés qui sera utilisé comme un SymmetricKey doit toohave un Type de contenu de « application/octet-stream » dans le coffre de clés.

Voici un exemple de création de secret dans Key Vault, effectuée dans PowerShell, qui peut être utilisé comme une valeur SymmetricKey.
Notez que la valeur hello dur codé, $key, est uniquement à des fins de démonstration. Dans votre propre code vous souhaiterez toogenerate cette clé.

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

Dans votre application console, vous pouvez utiliser hello même appeler comme avant tooretrieve ce secret principal en tant qu’un SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
Vous avez terminé. Vous n’avez plus qu’à l’utiliser !

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation du Stockage Microsoft Azure avec C#, consultez [Bibliothèque cliente Stockage Microsoft Azure pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Pour plus d’informations sur hello API REST d’objets Blob, consultez [API REST du Service Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Hello dernières informations sur Microsoft Azure Storage, accédez à toohello [Blog de l’équipe Microsoft Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/).
