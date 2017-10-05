---
title: "Format de fichier de propriétés et de métadonnées d’Azure Import/Export | Microsoft Docs"
description: "Découvrez comment spécifier les métadonnées et les propriétés d’un ou plusieurs objets blob qui font partie d’un travail d’importation ou d’exportation."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="fc044-103">Format de fichier de propriétés et de métadonnées du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="fc044-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="fc044-104">Vous pouvez spécifier les métadonnées et les propriétés d’un ou plusieurs objets blob dans le cadre d’un travail d’importation ou d’exportation.</span><span class="sxs-lookup"><span data-stu-id="fc044-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="fc044-105">Pour définir les métadonnées ou les propriétés d’objets blob créés dans le cadre d’un travail d’importation, vous devez fournir un fichier de métadonnées ou de propriétés sur le disque dur contenant les données à importer.</span><span class="sxs-lookup"><span data-stu-id="fc044-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="fc044-106">Pour un travail d’exportation, les métadonnées et les propriétés sont écrites dans un fichier de métadonnées ou de propriétés inclus sur le disque dur retourné.</span><span class="sxs-lookup"><span data-stu-id="fc044-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="fc044-107">Format du fichier de métadonnées</span><span class="sxs-lookup"><span data-stu-id="fc044-107">Metadata file format</span></span>  
<span data-ttu-id="fc044-108">Le format d’un fichier de métadonnées est le suivant :</span><span class="sxs-lookup"><span data-stu-id="fc044-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="fc044-109">Élément XML</span><span class="sxs-lookup"><span data-stu-id="fc044-109">XML Element</span></span>|<span data-ttu-id="fc044-110">Type</span><span class="sxs-lookup"><span data-stu-id="fc044-110">Type</span></span>|<span data-ttu-id="fc044-111">Description</span><span class="sxs-lookup"><span data-stu-id="fc044-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="fc044-112">Élément racine</span><span class="sxs-lookup"><span data-stu-id="fc044-112">Root element</span></span>|<span data-ttu-id="fc044-113">Élément racine du fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="fc044-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="fc044-114">String</span><span class="sxs-lookup"><span data-stu-id="fc044-114">String</span></span>|<span data-ttu-id="fc044-115">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-115">Optional.</span></span> <span data-ttu-id="fc044-116">L’élément XML spécifie le nom des métadonnées de l’objet blob, et sa valeur spécifie la valeur du paramètre des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="fc044-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="fc044-117">Format du fichier de propriétés</span><span class="sxs-lookup"><span data-stu-id="fc044-117">Properties file format</span></span>  
<span data-ttu-id="fc044-118">Le format d’un fichier de propriétés est le suivant :</span><span class="sxs-lookup"><span data-stu-id="fc044-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="fc044-119">Élément XML</span><span class="sxs-lookup"><span data-stu-id="fc044-119">XML Element</span></span>|<span data-ttu-id="fc044-120">Type</span><span class="sxs-lookup"><span data-stu-id="fc044-120">Type</span></span>|<span data-ttu-id="fc044-121">Description</span><span class="sxs-lookup"><span data-stu-id="fc044-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="fc044-122">Élément racine</span><span class="sxs-lookup"><span data-stu-id="fc044-122">Root element</span></span>|<span data-ttu-id="fc044-123">Élément racine du fichier de propriétés.</span><span class="sxs-lookup"><span data-stu-id="fc044-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="fc044-124">String</span><span class="sxs-lookup"><span data-stu-id="fc044-124">String</span></span>|<span data-ttu-id="fc044-125">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-125">Optional.</span></span> <span data-ttu-id="fc044-126">Heure de dernière modification de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-126">The last-modified time for the blob.</span></span> <span data-ttu-id="fc044-127">Travaux d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="fc044-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="fc044-128">String</span><span class="sxs-lookup"><span data-stu-id="fc044-128">String</span></span>|<span data-ttu-id="fc044-129">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-129">Optional.</span></span> <span data-ttu-id="fc044-130">Valeur ETag de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-130">The blob's ETag value.</span></span> <span data-ttu-id="fc044-131">Travaux d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="fc044-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="fc044-132">String</span><span class="sxs-lookup"><span data-stu-id="fc044-132">String</span></span>|<span data-ttu-id="fc044-133">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-133">Optional.</span></span> <span data-ttu-id="fc044-134">Taille de l’objet blob en octets.</span><span class="sxs-lookup"><span data-stu-id="fc044-134">The size of the blob in bytes.</span></span> <span data-ttu-id="fc044-135">Travaux d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="fc044-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="fc044-136">String</span><span class="sxs-lookup"><span data-stu-id="fc044-136">String</span></span>|<span data-ttu-id="fc044-137">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-137">Optional.</span></span> <span data-ttu-id="fc044-138">Type de contenu de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="fc044-139">String</span><span class="sxs-lookup"><span data-stu-id="fc044-139">String</span></span>|<span data-ttu-id="fc044-140">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-140">Optional.</span></span> <span data-ttu-id="fc044-141">Hash MD5 de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="fc044-142">String</span><span class="sxs-lookup"><span data-stu-id="fc044-142">String</span></span>|<span data-ttu-id="fc044-143">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-143">Optional.</span></span> <span data-ttu-id="fc044-144">Codage du contenu de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="fc044-145">String</span><span class="sxs-lookup"><span data-stu-id="fc044-145">String</span></span>|<span data-ttu-id="fc044-146">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-146">Optional.</span></span> <span data-ttu-id="fc044-147">Langage du contenu de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="fc044-148">String</span><span class="sxs-lookup"><span data-stu-id="fc044-148">String</span></span>|<span data-ttu-id="fc044-149">facultatif.</span><span class="sxs-lookup"><span data-stu-id="fc044-149">Optional.</span></span> <span data-ttu-id="fc044-150">Chaîne de contrôle du cache de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="fc044-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc044-151">Next steps</span></span>

<span data-ttu-id="fc044-152">Consultez les pages [Définir les propriétés d’objets blob](/rest/api/storageservices/set-blob-properties), [Définir les métadonnées d’objets blob](/rest/api/storageservices/set-blob-metadata) et [Définir et extraire les propriétés et métadonnées de ressources blob](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) pour obtenir des instructions détaillées sur la définition de propriétés et de métadonnées d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="fc044-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
