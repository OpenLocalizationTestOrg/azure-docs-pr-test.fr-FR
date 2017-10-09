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
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Signatures d’accès partagé, partie 2 : créer et utiliser une signature d’accès partagé avec Blob Storage

[partie 1](storage-dotnet-shared-access-signature-part-1.md) de ce didacticiel traitait des signatures d'accès partagé et indiquait les meilleures pratiques les concernant. Partie 2 vous montre comment toogenerate, puis utiliser un accès partagé les signatures avec un stockage d’objets Blob. exemples de Hello sont écrites en c# et utilisent hello bibliothèque cliente de stockage Azure pour .NET. exemples de Hello dans ce didacticiel :

* Générer une signature d'accès partagé sur un conteneur
* Générer une signature d'accès partagé sur un blob
* Créer des signatures de toomanage stratégie un accès stockée sur les ressources d’un conteneur
* Test des signatures d’accès hello partagé dans une application cliente

## <a name="about-this-tutorial"></a>À propos de ce didacticiel
Au cours de ce didacticiel, nous allons créer deux consoles d’application qui présentent la création et l’utilisation des signatures d’accès partagé pour les conteneurs et les blobs :

**Application 1**: hello application de gestion. Elle génère une signature d’accès partagé pour un conteneur et un blob. Inclut la clé de l’accès du compte de stockage hello dans le code source.

**L’application 2**: hello application cliente. Accède aux objets blob ressources de conteneur et à l’aide de signatures d’accès hello partagé créés avec la première application de hello. Signatures tooaccess conteneur utilise uniquement hello accès partagé et des ressources d’objet blob--il exécute *pas* incluent la clé de l’accès du compte de stockage hello.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Partie 1 : Créer un accès à la console application toogenerate partagé des signatures
Tout d’abord, assurez-vous que vous avez hello bibliothèque cliente de stockage Azure pour .NET est installé. Vous pouvez installer hello [package NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "package NuGet") contenant des assemblys plus récentes de hello pour la bibliothèque cliente de hello. Il s’agit de hello méthode pour vous assurer que vous disposez correctifs les plus récentes de hello recommandée. Vous pouvez également télécharger la bibliothèque cliente de hello dans le cadre de la version la plus récente de hello hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/).

Dans Visual Studio, créez une application console Windows et nommez-la **GenerateSharedAccessSignatures**. Ajouter des références trop[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) et [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) à l’aide d’une des méthodes suivantes de hello :

* Hello d’utilisation [Gestionnaire de package NuGet](https://docs.nuget.org/consume/installing-nuget) dans Visual Studio. Sélectionnez **Projet** > **Gérer les packages NuGet**, puis effectuez une recherche en ligne pour chaque package (Microsoft.WindowsAzure.ConfigurationManager et WindowsAzure.Storage), et installez-les.
* Vous pouvez également rechercher ces assemblys dans votre installation de hello Azure SDK et ajouter des références toothem :
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Au haut hello du fichier de hello Program.cs, ajoutez hello **à l’aide de** directives :

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Modifier le fichier app.config de hello pour qu’il contienne un paramètre de configuration avec une chaîne de connexion qui pointe de compte de stockage tooyour. Votre fichier app.config doit ressembler similaire toothis une :

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Générer une URI de signature d’accès partagé pour un conteneur
toobegin avec, nous ajoutons une méthode de toogenerate une signature d’accès partagé sur un nouveau conteneur. Dans ce cas, la signature de hello n’est pas associé à une stratégie d’accès stockée, afin qu’elle exerce hello d’informations URI hello indiquant ses autorisations d’expiration de temps et hello il accorde un accès.

D’abord, ajoutez le code toohello **Main()** méthode tooauthenticate accéder au compte de stockage tooyour et créer un nouveau conteneur :

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

Ensuite, ajoutez une méthode qui génère la signature d’accès partagé hello pour le conteneur de hello et retourne l’URI de signature hello :

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

Ajouter hello lignes bas hello hello suivantes **Main()** (méthode), avant l’appel hello**console.ReadLine**, toocall **GetContainerSasUri()** et d’écriture hello fenêtre de console URI toohello signature :

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Compilez et exécutez la signature d’accès partagé toooutput hello URI pour le nouveau conteneur de hello. Hello URI sera similaire toohello suivantes :

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Une fois que vous avez exécuté le code de hello, signature d’accès partagé hello que vous avez créé pour le conteneur de hello sera valide pour hello pendant les 24 heures. signature de Hello accorde à un client autorisation toolist des objets BLOB hello conteneurs et toowrite nouveaux objets BLOB toohello.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Générer une URI de signature d’accès partagé pour un blob
Ensuite, nous écrire toocreate de code similaire à un nouvel objet blob dans le conteneur de hello et générer une signature d’accès partagé pour celle-ci. Cette signature d’accès partagé n’est pas associée à une stratégie d’accès stockée pour qu’elle comporte hello heure de début, heure d’expiration et les informations d’autorisation Bonjour URI.

Ajoutez une nouvelle méthode qui crée un nouvel objet blob et écrit certains tooit de texte, puis génère une signature d’accès partagé et retourne l’URI de signature hello :

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

Bas hello hello **Main()** (méthode), ajouter hello suivant lignes toocall **GetBlobSasUri()**, avant d’appeler de hello trop**console.ReadLine ()**et d’écriture hello partagé fenêtre de console accès signature URI toohello :

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Compilez et exécutez la signature d’accès partagé toooutput hello URI pour le nouvel objet blob de hello. Hello URI sera similaire toohello suivantes :

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Créer une stratégie d’accès stockée sur le conteneur de hello
Maintenant nous allons créer une stratégie d’accès stockée sur le conteneur de hello, qui définit les contraintes hello pour les signatures d’accès partagé qui lui sont associés.

Dans les exemples précédents hello, que nous avons spécifié l’heure de début hello (implicitement ou explicitement), heure d’expiration hello et autorisations hello sur hello signature d’accès partagé URI lui-même. Bonjour exemple suivant, nous spécifions ces sur la stratégie d’accès stockée hello, et non sur la signature d’accès partagé hello. Cela permet de nous toochange ces contraintes sans réémettre hello partagés signature d’accès.

Il est possible de toohave un ou plusieurs des contraintes de hello sur la signature d’accès partagé hello et reste hello sur la stratégie d’accès stockée hello. Toutefois, vous pouvez spécifier uniquement l’heure de début hello, délai d’expiration et les autorisations dans un lieu ou hello autres. Par exemple, vous ne peut pas spécifier des autorisations sur la signature d’accès partagé hello et également de les spécifier dans la stratégie d’accès stockée hello.

Lorsque vous ajoutez un conteneur de tooa de stratégie d’accès stockée, vous devez obtenir les autorisations existantes du conteneur hello, ajoutez la nouvelle stratégie d’accès hello et puis définissez les autorisations du conteneur hello.

Ajoutez une nouvelle méthode qui crée une nouvelle stratégie d’accès stockée sur un conteneur et retourne le nom hello de stratégie de hello :

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

En bas de hello Hello **Main()** (méthode), avant l’appel hello**console.ReadLine**, ajouter hello suivant lignes toofirst effacer les stratégies d’accès, puis appelez hello  **CreateSharedAccessPolicy()** méthode :

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

Lorsque vous désactivez les stratégies d’accès hello sur un conteneur, vous devez tout d’abord obtenir les autorisations existantes du conteneur hello, puis les autorisations hello clair, puis définir les autorisations de hello à nouveau.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Générer une signature d’accès partagé URI sur conteneur hello qui utilise une stratégie d’accès
Ensuite, nous créons une autre signature d’accès partagé pour le conteneur hello que nous avons créés précédemment, mais cette fois nous associons signature de hello avec la stratégie d’accès stockée hello que nous avons créé dans l’exemple précédent de hello.

Ajouter un nouveau toogenerate de méthode autre signature d’accès partagé pour le conteneur de hello :

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

Bas hello hello **Main()** (méthode), avant l’appel hello**console.ReadLine**, ajouter hello suivant hello toocall de lignes **GetContainerSasUriWithPolicy** (méthode) :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Générer un URI de Signature d’accès partagé sur hello Blob qu’utilise une stratégie d’accès
Enfin, nous ajouter un toocreate méthode similaire à un autre objet blob et générer une signature d’accès partagé qui est associé à une stratégie d’accès stockée.

Ajouter un nouveau toocreate de la méthode un objet blob et générer une signature d’accès partagé :

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

Bas hello hello **Main()** (méthode), avant l’appel hello**console.ReadLine**, ajouter hello suivant hello toocall de lignes **GetBlobSasUriWithPolicy** méthode :

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Hello **Main()** méthode doit maintenant ressembler à ceci dans son intégralité. Exécuter la signature d’accès partagé hello toowrite fenêtre de console toohello URI, puis copiez et collez-les dans un fichier texte pour une utilisation dans hello deuxième partie de ce didacticiel.

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

Lorsque vous exécutez des applications de console hello GenerateSharedAccessSignatures, vous verrez suivant toohello similaire de sortie. Il s’agit des signatures d’accès partagé de hello que vous utilisez dans la partie 2 du didacticiel de hello.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Partie 2 : Créer un accès à la console application tootest hello partagé des signatures
tootest hello partagé créés dans les exemples précédents hello des signatures d’accès, nous créons une deuxième application console qui utilise des opérations de tooperform hello signatures sur le conteneur de hello et sur un objet blob.

> [!NOTE]
> Si plus de 24 heures se sont écoulés depuis la fin de hello première partie du didacticiel de hello, vous avez généré des signatures hello ne seront plus valides. Dans ce cas, vous devez exécuter les code hello dans hello première console application toogenerate signatures d’accès partagé actualisée pour une utilisation dans la deuxième partie de hello du didacticiel de hello.
>

Dans Visual Studio, créez une application console Windows et nommez-la **ConsumeSharedAccessSignatures**. Ajouter des références trop[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) et [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), comme vous l’avez fait précédemment.

Au haut hello du fichier de hello Program.cs, ajoutez hello **à l’aide de** directives :

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Dans le corps hello Hello **Main()** (méthode), ajouter hello suivant des constantes de chaîne, la modification de leurs valeurs toohello partagé des signatures d’accès vous avez généré dans la partie 1 du didacticiel de hello.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Ajouter une méthode tootry conteneur les opérations à l’aide d’une signature d’accès partagé
Ensuite, nous ajouter une méthode qui vérifie certaines opérations de conteneur à l’aide d’une signature d’accès partagé pour le conteneur de hello. signature d’accès partagé Hello est tooreturn utilisé un conteneur de toohello de référence, l’authentification du conteneur de toohello d’accès basé sur la signature hello uniquement.

Ajoutez hello suivant tooProgram.cs de méthode :

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

Hello de mise à jour **Main()** méthode toocall **UseContainerSAS()** avec deux hello de signatures d’accès vous avez créé sur le conteneur de hello partagé :

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Ajouter une méthode tootry blob les opérations à l’aide d’une signature d’accès partagé
Enfin, nous ajouter une méthode qui vérifie certaines opérations de l’objet blob à l’aide d’une signature d’accès partagé sur un objet blob de hello. Dans ce cas, nous utilisons le constructeur de hello **CloudBlockBlob(String)**, en passant la signature d’accès partagé hello, tooreturn un objet blob toohello de référence. Aucune authentification n’est requise ; Il est basé sur la signature hello uniquement.

Ajoutez hello suivant tooProgram.cs de méthode :

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

Hello de mise à jour **Main()** méthode toocall **UseBlobSAS()** avec deux hello partagé des signatures d’accès que vous avez créé sur l’objet blob de hello :

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

Exécutez l’application de console hello et observez les toosee de sortie hello quelles opérations sont autorisées pour les signatures. sortie Hello dans la fenêtre de console hello ressemblera similaire toohello suivantes :

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Étapes suivantes

* [Signatures d’accès partagé, partie 1 : Hello de présentation modèle SAP](storage-dotnet-shared-access-signature-part-1.md)
* [Gérer les objets BLOB et l’accès en lecture anonyme toocontainers](storage-manage-access-to-resources.md)
* [Délégation de l’accès avec une signature d’accès partagé (API REST)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Présentation des signatures d’accès partagé de table et de file d’attente](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
