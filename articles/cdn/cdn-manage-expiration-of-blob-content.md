---
title: "expiration aaaManage d’objets BLOB de stockage Azure dans Azure CDN | Documents Microsoft"
description: "En savoir plus sur les options de hello pour contrôler la durée de vie des objets BLOB dans la mise en cache du CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Gérer l’expiration des objets blob d’Azure Storage dans Azure CDN
> [!div class="op_single_selector"]
> * [Azure Web Apps/Cloud Services, ASP.NET ou IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Service Azure Storage Blob](cdn-manage-expiration-of-blob-content.md)
> 
> 

Hello [service blob](../storage/common/storage-introduction.md#blob-storage) dans [Azure Storage](../storage/common/storage-introduction.md) parmi plusieurs origines basé sur Azure est intégré avec Azure CDN.  Tout contenu d’objet BLOB publiquement accessible peut être mis en cache dans Azure CDN jusqu’à l’expiration de sa durée de vie.  durée de vie Hello est déterminée par hello [ *Cache-Control* en-tête](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en réponse hello HTTP depuis le stockage Azure.

> [!TIP]
> Vous ne pouvez choisir tooset aucune durée de vie d’un objet blob.  Dans ce cas, Azure CDN applique automatiquement une durée de vie de sept jours par défaut.
> 
> Pour plus d’informations sur le fonctionnement de Azure CDN toospeed tooblobs d’accès et d’autres fichiers, consultez hello [vue d’ensemble du CDN Azure](cdn-overview.md).
> 
> Pour plus d’informations sur hello service d’objets blob Azure Storage, consultez [Concepts du Service Blob](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

Ce didacticiel illustre plusieurs méthodes que vous pouvez définir la durée de vie de hello sur un objet blob dans le stockage Azure.  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) est un des tooadminister de façons plus rapide et la plus puissante hello vos services Azure.  Hello d’utilisation `Get-AzureStorageBlob` tooget de l’applet de commande un objet blob de référence toohello, puis définissez hello `.ICloudBlob.Properties.CacheControl` propriété. 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> Vous pouvez également utiliser PowerShell trop[gérer vos points de terminaison et les profils CDN](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Bibliothèque cliente Azure Storage pour .NET
tooset un objet blob de durée de vie à l’aide de .NET, utilisez hello [bibliothèque cliente de stockage Azure pour .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) propriété.

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> Nombre d’autres exemples de code .NET sont disponibles dans hello [exemples de stockage d’objets Blob Azure pour .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Autres méthodes
* [Interface de ligne de commande Azure](../cli-install-nodejs.md)
  
    Lors du téléchargement d’objet blob de hello, définissez hello *cacheControl* propriété à l’aide de hello `-p` basculer.  Cet exemple définit l’heure tooone de durée de vie hello (3600 secondes).
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [API REST des services d’Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Explicitement ensemble hello *x-ms-objet blob-cache-control* propriété sur un [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [placer la liste de blocs](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), ou [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) demande.
* Outils de gestion du stockage tiers
  
    Certains outils de gestion du stockage Azure tiers vous autoriser tooset hello *CacheControl* propriété sur les objets BLOB. 

## <a name="testing-hello-cache-control-header"></a>Test hello *Cache-Control* en-tête
Vous pouvez facilement vérifier hello durée de vie de vos objets BLOB.  À l’aide de votre navigateur [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), tester que votre objet blob est notamment hello *Cache-Control* en-tête de réponse.  Vous pouvez également utiliser un outil tel que **wget**, [Postman](https://www.getpostman.com/), ou [Fiddler](http://www.telerik.com/fiddler) tooexamine les en-têtes de réponse hello.

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello *Cache-Control* en-tête](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Découvrez comment toomanage l’expiration des contenus de Service Cloud dans Azure CDN](cdn-manage-expiration-of-cloud-service-content.md)

