---
title: "Gérer l’expiration des objets blob d’Azure Storage dans Azure CDN | Microsoft Docs"
description: "Découvrez les options de contrôle de la durée de vie des objets blob dans la mise en cache Azure CDN."
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
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="57b9d-103">Gérer l’expiration des objets blob d’Azure Storage dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="57b9d-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57b9d-104">Azure Web Apps/Cloud Services, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="57b9d-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="57b9d-105">Service Azure Storage Blob</span><span class="sxs-lookup"><span data-stu-id="57b9d-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="57b9d-106">Le [service BLOB](../storage/common/storage-introduction.md#blob-storage) dans [Stockage Azure](../storage/common/storage-introduction.md) fait partie des différentes origines Azure intégrées à Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="57b9d-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="57b9d-107">Tout contenu d’objet BLOB publiquement accessible peut être mis en cache dans Azure CDN jusqu’à l’expiration de sa durée de vie.</span><span class="sxs-lookup"><span data-stu-id="57b9d-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="57b9d-108">La durée de vie est déterminée par l’ [*Cache-Control* ](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) dans la réponse HTTP d’Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="57b9d-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="57b9d-109">Vous pouvez choisir de ne pas définir la durée de vie d’un objet BLOB.</span><span class="sxs-lookup"><span data-stu-id="57b9d-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="57b9d-110">Dans ce cas, Azure CDN applique automatiquement une durée de vie de sept jours par défaut.</span><span class="sxs-lookup"><span data-stu-id="57b9d-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="57b9d-111">Pour découvrir comment Azure CDN accélère l’accès aux objets blob et à d’autres fichiers, consultez la [Vue d’ensemble d’Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57b9d-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="57b9d-112">Pour plus d’informations sur le service BLOB Azure Storage, consultez la page [Concepts du service BLOB](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="57b9d-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="57b9d-113">Ce didacticiel présente plusieurs façons de définir la durée de vie d’un objet BLOB dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="57b9d-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="57b9d-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="57b9d-114">Azure PowerShell</span></span>
<span data-ttu-id="57b9d-115">[Azure PowerShell](/powershell/azure/overview) est l’un des moyens les plus rapides et puissants de gérer vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="57b9d-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="57b9d-116">Utilisez l’applet de commande `Get-AzureStorageBlob` pour obtenir une référence à l’objet BLOB, puis définissez la propriété `.ICloudBlob.Properties.CacheControl`.</span><span class="sxs-lookup"><span data-stu-id="57b9d-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="57b9d-117">Vous pouvez également utiliser PowerShell pour [gérer vos profils et points de terminaison CDN](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="57b9d-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="57b9d-118">Bibliothèque cliente Azure Storage pour .NET</span><span class="sxs-lookup"><span data-stu-id="57b9d-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="57b9d-119">Pour définir la durée de vie d’un objet blob à l’aide de .NET, utilisez la [bibliothèque cliente Stockage Azure pour .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) pour définir la propriété [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx).</span><span class="sxs-lookup"><span data-stu-id="57b9d-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="57b9d-120">De nombreux autres exemples de code .NET sont disponibles dans les [exemples de stockage d’objets BLOB Azure pour .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="57b9d-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="57b9d-121">Autres méthodes</span><span class="sxs-lookup"><span data-stu-id="57b9d-121">Other methods</span></span>
* [<span data-ttu-id="57b9d-122">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="57b9d-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="57b9d-123">Lors du chargement de l’objet blob, définissez la propriété *cacheControl* à l’aide du switch `-p`.</span><span class="sxs-lookup"><span data-stu-id="57b9d-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="57b9d-124">Cet exemple définit la durée de vie sur une heure (3 600 secondes).</span><span class="sxs-lookup"><span data-stu-id="57b9d-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="57b9d-125">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="57b9d-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="57b9d-126">Définissez explicitement la propriété *x-ms-blob-cache-control* sur une demande [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx) ou [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx).</span><span class="sxs-lookup"><span data-stu-id="57b9d-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="57b9d-127">Outils de gestion du stockage tiers</span><span class="sxs-lookup"><span data-stu-id="57b9d-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="57b9d-128">Certains outils de gestion Azure Storage tiers vous permettent de définir la propriété *CacheControl* sur les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="57b9d-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="57b9d-129">Test de l’en-tête *Cache-Control*</span><span class="sxs-lookup"><span data-stu-id="57b9d-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="57b9d-130">Vous pouvez facilement vérifier la durée de vie de vos objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="57b9d-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="57b9d-131">À l’aide des [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)de votre navigateur, vérifiez que votre objet BLOB comprend l’en-tête de réponse *Cache-Control* .</span><span class="sxs-lookup"><span data-stu-id="57b9d-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="57b9d-132">Vous pouvez également utiliser un outil tel que **wget**, [Postman](https://www.getpostman.com/) ou [Fiddler](http://www.telerik.com/fiddler) pour examiner les en-têtes de réponse.</span><span class="sxs-lookup"><span data-stu-id="57b9d-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57b9d-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57b9d-133">Next Steps</span></span>
* [<span data-ttu-id="57b9d-134">En savoir plus sur les en-têtes *Cache-Control*</span><span class="sxs-lookup"><span data-stu-id="57b9d-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="57b9d-135">Comment gérer l’expiration des contenus de service cloud dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="57b9d-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

