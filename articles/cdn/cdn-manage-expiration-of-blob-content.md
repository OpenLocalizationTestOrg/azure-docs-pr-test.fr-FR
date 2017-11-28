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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="9cac7-103">Gérer l’expiration des objets blob d’Azure Storage dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9cac7-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cac7-104">Azure Web Apps/Cloud Services, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="9cac7-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="9cac7-105">Service Azure Storage Blob</span><span class="sxs-lookup"><span data-stu-id="9cac7-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="9cac7-106">Hello [service blob](../storage/common/storage-introduction.md#blob-storage) dans [Azure Storage](../storage/common/storage-introduction.md) parmi plusieurs origines basé sur Azure est intégré avec Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="9cac7-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="9cac7-107">Tout contenu d’objet BLOB publiquement accessible peut être mis en cache dans Azure CDN jusqu’à l’expiration de sa durée de vie.</span><span class="sxs-lookup"><span data-stu-id="9cac7-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="9cac7-108">durée de vie Hello est déterminée par hello [ *Cache-Control* en-tête](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en réponse hello HTTP depuis le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9cac7-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="9cac7-109">Vous ne pouvez choisir tooset aucune durée de vie d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="9cac7-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="9cac7-110">Dans ce cas, Azure CDN applique automatiquement une durée de vie de sept jours par défaut.</span><span class="sxs-lookup"><span data-stu-id="9cac7-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="9cac7-111">Pour plus d’informations sur le fonctionnement de Azure CDN toospeed tooblobs d’accès et d’autres fichiers, consultez hello [vue d’ensemble du CDN Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cac7-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="9cac7-112">Pour plus d’informations sur hello service d’objets blob Azure Storage, consultez [Concepts du Service Blob](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cac7-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="9cac7-113">Ce didacticiel illustre plusieurs méthodes que vous pouvez définir la durée de vie de hello sur un objet blob dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9cac7-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="9cac7-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cac7-114">Azure PowerShell</span></span>
<span data-ttu-id="9cac7-115">[Azure PowerShell](/powershell/azure/overview) est un des tooadminister de façons plus rapide et la plus puissante hello vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="9cac7-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="9cac7-116">Hello d’utilisation `Get-AzureStorageBlob` tooget de l’applet de commande un objet blob de référence toohello, puis définissez hello `.ICloudBlob.Properties.CacheControl` propriété.</span><span class="sxs-lookup"><span data-stu-id="9cac7-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

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
> <span data-ttu-id="9cac7-117">Vous pouvez également utiliser PowerShell trop[gérer vos points de terminaison et les profils CDN](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9cac7-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="9cac7-118">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="9cac7-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="9cac7-119">tooset un objet blob de durée de vie à l’aide de .NET, utilisez hello [bibliothèque cliente de stockage Azure pour .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) propriété.</span><span class="sxs-lookup"><span data-stu-id="9cac7-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

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
> <span data-ttu-id="9cac7-120">Nombre d’autres exemples de code .NET sont disponibles dans hello [exemples de stockage d’objets Blob Azure pour .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="9cac7-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="9cac7-121">Autres méthodes</span><span class="sxs-lookup"><span data-stu-id="9cac7-121">Other methods</span></span>
* [<span data-ttu-id="9cac7-122">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="9cac7-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="9cac7-123">Lors du téléchargement d’objet blob de hello, définissez hello *cacheControl* propriété à l’aide de hello `-p` basculer.</span><span class="sxs-lookup"><span data-stu-id="9cac7-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="9cac7-124">Cet exemple définit l’heure tooone de durée de vie hello (3600 secondes).</span><span class="sxs-lookup"><span data-stu-id="9cac7-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="9cac7-125">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9cac7-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="9cac7-126">Explicitement ensemble hello *x-ms-objet blob-cache-control* propriété sur un [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [placer la liste de blocs](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), ou [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) demande.</span><span class="sxs-lookup"><span data-stu-id="9cac7-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="9cac7-127">Outils de gestion du stockage tiers</span><span class="sxs-lookup"><span data-stu-id="9cac7-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="9cac7-128">Certains outils de gestion du stockage Azure tiers vous autoriser tooset hello *CacheControl* propriété sur les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="9cac7-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="9cac7-129">Test hello *Cache-Control* en-tête</span><span class="sxs-lookup"><span data-stu-id="9cac7-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="9cac7-130">Vous pouvez facilement vérifier hello durée de vie de vos objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="9cac7-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="9cac7-131">À l’aide de votre navigateur [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), tester que votre objet blob est notamment hello *Cache-Control* en-tête de réponse.</span><span class="sxs-lookup"><span data-stu-id="9cac7-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="9cac7-132">Vous pouvez également utiliser un outil tel que **wget**, [Postman](https://www.getpostman.com/), ou [Fiddler](http://www.telerik.com/fiddler) tooexamine les en-têtes de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="9cac7-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cac7-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9cac7-133">Next Steps</span></span>
* [<span data-ttu-id="9cac7-134">En savoir plus sur hello *Cache-Control* en-tête</span><span class="sxs-lookup"><span data-stu-id="9cac7-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="9cac7-135">Découvrez comment toomanage l’expiration des contenus de Service Cloud dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9cac7-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

