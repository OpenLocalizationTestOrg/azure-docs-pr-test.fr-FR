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
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Format de fichier de propriétés et de métadonnées du service Azure Import/Export
Vous pouvez spécifier les métadonnées et les propriétés d’un ou plusieurs objets blob dans le cadre d’un travail d’importation ou d’exportation. tooset métadonnées ou des propriétés pour les objets BLOB en cours de création dans le cadre d’un travail d’importation, vous fournissez un fichier de métadonnées ou des propriétés sur un disque de hello contenant hello toobe de données importée. Pour un travail d’exportation, les métadonnées et les propriétés sont écrites fichier de métadonnées ou des propriétés tooa qui est inclus sur le disque dur hello retourné tooyou.  
  
## <a name="metadata-file-format"></a>Format du fichier de métadonnées  
format de Hello d’un fichier de métadonnées est la suivante :  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|Élément XML|Type|Description|  
|-----------------|----------|-----------------|  
|`Metadata`|Élément racine|élément racine de Hello hello du fichier de métadonnées.|  
|`metadata-name`|String|facultatif. élément XML de Hello Spécifie le nom hello de hello métadonnées pour l’objet blob de hello et sa valeur spécifie la valeur hello du paramètre de métadonnées hello.|  
  
## <a name="properties-file-format"></a>Format du fichier de propriétés  
format de Hello d’un fichier de propriétés est le suivant :  
  
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
  
|Élément XML|Type|Description|  
|-----------------|----------|-----------------|  
|`Properties`|Élément racine|élément racine de Hello du fichier de propriétés hello.|  
|`Last-Modified`|String|facultatif. Hello heure de dernière modification de l’objet blob de hello. Travaux d’exportation uniquement.|  
|`Etag`|String|facultatif. Bonjour valeur ETag de l’objet blob. Travaux d’exportation uniquement.|  
|`Content-Length`|String|facultatif. taille de Hello du blob hello en octets. Travaux d’exportation uniquement.|  
|`Content-Type`|String|facultatif. type de contenu Hello d’objet blob de hello.|  
|`Content-MD5`|String|facultatif. Bonjour hachage MD5 de l’objet blob.|  
|`Content-Encoding`|String|facultatif. le contenu de l’objet blob de Hello encodage.|  
|`Content-Language`|String|facultatif. Bonjour langue du contenu de l’objet blob.|  
|`Cache-Control`|String|facultatif. chaîne de contrôle Hello du cache pour l’objet blob de hello.|  

## <a name="next-steps"></a>Étapes suivantes

Consultez les pages [Définir les propriétés d’objets blob](/rest/api/storageservices/set-blob-properties), [Définir les métadonnées d’objets blob](/rest/api/storageservices/set-blob-metadata) et [Définir et extraire les propriétés et métadonnées de ressources blob](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) pour obtenir des instructions détaillées sur la définition de propriétés et de métadonnées d’objets blob.
