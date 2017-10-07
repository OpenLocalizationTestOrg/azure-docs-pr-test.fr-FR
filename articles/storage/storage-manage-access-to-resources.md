---
title: "accès en lecture aaaEnable public pour les conteneurs et objets BLOB dans le stockage Blob Azure | Documents Microsoft"
description: "Découvrez comment toomake conteneurs et objets BLOB disponibles pour l’accès anonyme et comment tooaccess les par programme."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Gérer les objets BLOB et l’accès en lecture anonyme toocontainers
Vous pouvez activer un accès en lecture public anonyme tooa conteneur et ses objets BLOB dans le stockage d’objets Blob Azure. En procédant ainsi, vous pouvez accorder des ressources de toothese accès en lecture seule sans partager votre clé de compte et sans nécessiter une signature d’accès partagé (SAS).

Accès en lecture public est idéal pour les scénarios où vous souhaitez que certains objets BLOB tooalways être disponibles pour l’accès en lecture anonyme. Pour un contrôle plus précis, vous pouvez créer une signature d’accès partagé. Signatures d’accès partagé activer tooprovide restreint l’accès à l’aide des autorisations différentes pour une période spécifique. Pour plus d’informations sur la création de signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP) dans le Stockage Azure](storage-dotnet-shared-access-signature-part-1.md).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Accorder aux utilisateurs anonymes des autorisations toocontainers et les objets BLOB
Par défaut, un conteneur et tous les objets BLOB qu’il contient sont accessibles uniquement par le propriétaire de hello hello du compte de stockage. conteneur de tooa toogive les utilisateurs anonymes des autorisations lecture et ses objets BLOB, vous pouvez définir des autorisations hello conteneur tooallow un accès public. Utilisateurs anonymes peuvent lire des objets BLOB dans un conteneur accessible publiquement sans authentifier la demande de hello.

Vous pouvez configurer un conteneur avec hello les autorisations suivantes :

* **Accès en lecture sans public :** conteneur de hello et ses objets BLOB sont accessibles uniquement par le propriétaire du compte de stockage hello. Il s’agit par défaut de hello pour tous les conteneurs de nouveau.
* **Pour les objets BLOB uniquement l’accès en lecture public :** BLOB conteneur hello peuvent être lus par une demande anonyme, mais les données de conteneur ne seront pas disponibles. Les clients anonymes ne peuvent pas énumérer les objets BLOB hello conteneur de hello.
* **Accès en lecture public total :** toutes les données du conteneur et des objets blob peuvent être lues par une demande anonyme. Les clients peuvent énumérer les objets BLOB dans le conteneur de hello par une demande anonyme, mais ne peut pas énumérer des conteneurs dans le compte de stockage hello.

Vous pouvez utiliser hello tooset conteneur autorisations suivantes :

* [Portail Azure](https://portal.azure.com)
* [Azure PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [Azure CLI 2.0](storage-azure-cli.md#create-and-manage-blobs)
* Par programme, en utilisant l’une des bibliothèques clientes de stockage hello ou hello API REST

### <a name="set-container-permissions-in-hello-azure-portal"></a>Définir les autorisations du conteneur dans hello portail Azure
autorisations du conteneur tooset Bonjour [portail Azure](https://portal.azure.com), procédez comme suit :

1. Ouvrez votre **compte de stockage** panneau dans le portail de hello. Vous pouvez trouver votre compte de stockage en sélectionnant **comptes de stockage** dans le panneau de menus du portail principal hello.
1. Sous **SERVICE BLOB** dans le panneau de menu hello, sélectionnez **conteneurs**.
1. Avec le bouton droit sur la ligne du conteneur hello ou du conteneur hello hello Sélectionnez points de suspension tooopen **menu contextuel**.
1. Sélectionnez **stratégie d’accès** dans le menu contextuel de hello.
1. Sélectionnez un **type d’accès** de hello menu déroulant.

    ![Boîte de dialogue Modifier les métadonnées du conteneur](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Définir des autorisations de conteneur avec .NET
autorisations tooset pour un conteneur à l’aide de c# et hello bibliothèque cliente de stockage pour .NET, tout d’abord extraire les autorisations existantes du conteneur hello en appelant hello **GetPermissions** (méthode). Puis ensemble hello **PublicAccess** propriété hello **BlobContainerPermissions** objet qui est retourné par hello **GetPermissions** (méthode). Enfin, appelez hello **SetPermissions** méthode avec hello mis à jour les autorisations.

Hello, l’exemple suivant définit les autorisations du conteneur hello toofull un accès en lecture public. tooset autorisations toopublic l’accès en lecture pour les objets BLOB uniquement, définissez hello **PublicAccess** propriété trop**BlobContainerPublicAccessType.Blob**. valeur de toutes les autorisations pour les utilisateurs anonymes, tooremove hello propriété trop**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Accéder anonymement aux conteneurs et aux objets Blob
Un client ayant un accès anonyme aux conteneurs et aux objets Blob peut utiliser des constructeurs qui ne nécessitent pas d’informations d’identification. Hello suivant exemples montrent différentes manières de ressources du service Blob tooreference anonymement.

### <a name="create-an-anonymous-client-object"></a>Créer un objet de client anonyme
Vous pouvez créer un nouvel objet de service client pour l’accès anonyme en fournissant un point de terminaison de service hello Blob pour le compte de hello. Toutefois, vous devez également connaître nom hello d’un conteneur dans ce compte n’est disponible pour l’accès anonyme.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Référencer un conteneur de manière anonyme
Si vous avez hello URL tooa conteneur qui est disponible de manière anonyme, vous pouvez utiliser il tooreference hello conteneur directement.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Référencer un objet Blob de façon anonyme
Si vous avez hello URL tooa blob qui est disponible pour l’accès anonyme, vous pouvez référencer des blob hello directement à l’aide de cette URL :

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Utilisateurs de fonctionnalités disponible tooanonymous
Hello tableau suivant montre les opérations pouvant être appelées par des utilisateurs anonymes lorsque les ACL d’un conteneur a tooallow un accès public.

| Opération REST | Autorisation avec accès en lecture public complet | Autorisation avec accès en lecture public pour les objets blob uniquement |
| --- | --- | --- |
| List Containers |Propriétaire uniquement |Propriétaire uniquement |
| Create Container |Propriétaire uniquement |Propriétaire uniquement |
| Get Container Properties |Tout |Propriétaire uniquement |
| Get Container Metadata |Tout |Propriétaire uniquement |
| Set Container Metadata |Propriétaire uniquement |Propriétaire uniquement |
| Get Container ACL |Propriétaire uniquement |Propriétaire uniquement |
| Set Container ACL |Propriétaire uniquement |Propriétaire uniquement |
| Delete Container |Propriétaire uniquement |Propriétaire uniquement |
| List Blobs |Tout |Propriétaire uniquement |
| Put Blob |Propriétaire uniquement |Propriétaire uniquement |
| Get Blob |Tout |Tout |
| Get Blob Properties |Tout |Tout |
| Set Blob Properties |Propriétaire uniquement |Propriétaire uniquement |
| Get Blob Metadata |Tout |Tout |
| Set Blob Metadata |Propriétaire uniquement |Propriétaire uniquement |
| Put Block |Propriétaire uniquement |Propriétaire uniquement |
| Get Block List (blocs validés uniquement) |Tout |Tout |
| Get Block List (blocs non validés uniquement ou tous les blocs) |Propriétaire uniquement |Propriétaire uniquement |
| Put Block List |Propriétaire uniquement |Propriétaire uniquement |
| Delete Blob |Propriétaire uniquement |Propriétaire uniquement |
| Copie d'un objet blob |Propriétaire uniquement |Propriétaire uniquement |
| Snapshot Blob |Propriétaire uniquement |Propriétaire uniquement |
| Lease Blob |Propriétaire uniquement |Propriétaire uniquement |
| Put Page |Propriétaire uniquement |Propriétaire uniquement |
| Get Page Ranges |Tout |Tout |
| Append Blob |Propriétaire uniquement |Propriétaire uniquement |

## <a name="next-steps"></a>Étapes suivantes

* [Authentification pour hello Services de stockage Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md)
* [Délégation de l'accès avec une signature d'accès partagé](https://msdn.microsoft.com/library/azure/ee395415.aspx)
