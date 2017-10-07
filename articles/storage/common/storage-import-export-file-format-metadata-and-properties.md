---
title: "format de fichier des métadonnées et les propriétés d’aaaAzure Import/Export | Documents Microsoft"
description: "Découvrez comment toospecify métadonnées et propriétés d’un ou plusieurs objets BLOB qui font partie d’une importation ou de travail d’exportation."
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="385f0-103">Format de fichier de propriétés et de métadonnées du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="385f0-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="385f0-104">Vous pouvez spécifier les métadonnées et les propriétés d’un ou plusieurs objets blob dans le cadre d’un travail d’importation ou d’exportation.</span><span class="sxs-lookup"><span data-stu-id="385f0-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="385f0-105">tooset métadonnées ou des propriétés pour les objets BLOB en cours de création dans le cadre d’un travail d’importation, vous fournissez un fichier de métadonnées ou des propriétés sur un disque de hello contenant hello toobe de données importée.</span><span class="sxs-lookup"><span data-stu-id="385f0-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="385f0-106">Pour un travail d’exportation, les métadonnées et les propriétés sont écrites fichier de métadonnées ou des propriétés tooa qui est inclus sur le disque dur hello retourné tooyou.</span><span class="sxs-lookup"><span data-stu-id="385f0-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="385f0-107">Format du fichier de métadonnées</span><span class="sxs-lookup"><span data-stu-id="385f0-107">Metadata file format</span></span>  
<span data-ttu-id="385f0-108">format de Hello d’un fichier de métadonnées est la suivante :</span><span class="sxs-lookup"><span data-stu-id="385f0-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="385f0-109">Élément XML</span><span class="sxs-lookup"><span data-stu-id="385f0-109">XML Element</span></span>|<span data-ttu-id="385f0-110">Type</span><span class="sxs-lookup"><span data-stu-id="385f0-110">Type</span></span>|<span data-ttu-id="385f0-111">Description</span><span class="sxs-lookup"><span data-stu-id="385f0-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="385f0-112">Élément racine</span><span class="sxs-lookup"><span data-stu-id="385f0-112">Root element</span></span>|<span data-ttu-id="385f0-113">élément racine de Hello hello du fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="385f0-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="385f0-114">String</span><span class="sxs-lookup"><span data-stu-id="385f0-114">String</span></span>|<span data-ttu-id="385f0-115">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-115">Optional.</span></span> <span data-ttu-id="385f0-116">élément XML de Hello Spécifie le nom hello de hello métadonnées pour l’objet blob de hello et sa valeur spécifie la valeur hello du paramètre de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="385f0-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="385f0-117">Format du fichier de propriétés</span><span class="sxs-lookup"><span data-stu-id="385f0-117">Properties file format</span></span>  
<span data-ttu-id="385f0-118">format de Hello d’un fichier de propriétés est le suivant :</span><span class="sxs-lookup"><span data-stu-id="385f0-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="385f0-119">Élément XML</span><span class="sxs-lookup"><span data-stu-id="385f0-119">XML Element</span></span>|<span data-ttu-id="385f0-120">Type</span><span class="sxs-lookup"><span data-stu-id="385f0-120">Type</span></span>|<span data-ttu-id="385f0-121">Description</span><span class="sxs-lookup"><span data-stu-id="385f0-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="385f0-122">Élément racine</span><span class="sxs-lookup"><span data-stu-id="385f0-122">Root element</span></span>|<span data-ttu-id="385f0-123">élément racine de Hello du fichier de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="385f0-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="385f0-124">String</span><span class="sxs-lookup"><span data-stu-id="385f0-124">String</span></span>|<span data-ttu-id="385f0-125">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-125">Optional.</span></span> <span data-ttu-id="385f0-126">Hello heure de dernière modification de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="385f0-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="385f0-127">Travaux d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="385f0-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="385f0-128">String</span><span class="sxs-lookup"><span data-stu-id="385f0-128">String</span></span>|<span data-ttu-id="385f0-129">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-129">Optional.</span></span> <span data-ttu-id="385f0-130">Bonjour valeur ETag de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="385f0-130">hello blob's ETag value.</span></span> <span data-ttu-id="385f0-131">Travaux d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="385f0-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="385f0-132">String</span><span class="sxs-lookup"><span data-stu-id="385f0-132">String</span></span>|<span data-ttu-id="385f0-133">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-133">Optional.</span></span> <span data-ttu-id="385f0-134">taille de Hello du blob hello en octets.</span><span class="sxs-lookup"><span data-stu-id="385f0-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="385f0-135">Travaux d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="385f0-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="385f0-136">String</span><span class="sxs-lookup"><span data-stu-id="385f0-136">String</span></span>|<span data-ttu-id="385f0-137">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-137">Optional.</span></span> <span data-ttu-id="385f0-138">type de contenu Hello d’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="385f0-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="385f0-139">String</span><span class="sxs-lookup"><span data-stu-id="385f0-139">String</span></span>|<span data-ttu-id="385f0-140">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-140">Optional.</span></span> <span data-ttu-id="385f0-141">Bonjour hachage MD5 de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="385f0-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="385f0-142">String</span><span class="sxs-lookup"><span data-stu-id="385f0-142">String</span></span>|<span data-ttu-id="385f0-143">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-143">Optional.</span></span> <span data-ttu-id="385f0-144">le contenu de l’objet blob de Hello encodage.</span><span class="sxs-lookup"><span data-stu-id="385f0-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="385f0-145">String</span><span class="sxs-lookup"><span data-stu-id="385f0-145">String</span></span>|<span data-ttu-id="385f0-146">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-146">Optional.</span></span> <span data-ttu-id="385f0-147">Bonjour langue du contenu de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="385f0-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="385f0-148">String</span><span class="sxs-lookup"><span data-stu-id="385f0-148">String</span></span>|<span data-ttu-id="385f0-149">facultatif.</span><span class="sxs-lookup"><span data-stu-id="385f0-149">Optional.</span></span> <span data-ttu-id="385f0-150">chaîne de contrôle Hello du cache pour l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="385f0-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="385f0-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="385f0-151">Next steps</span></span>

<span data-ttu-id="385f0-152">Consultez les pages [Définir les propriétés d’objets blob](/rest/api/storageservices/set-blob-properties), [Définir les métadonnées d’objets blob](/rest/api/storageservices/set-blob-metadata) et [Définir et extraire les propriétés et métadonnées de ressources blob](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) pour obtenir des instructions détaillées sur la définition de propriétés et de métadonnées d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="385f0-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
