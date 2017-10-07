---
title: "aaaSetting propriétés et des métadonnées à l’aide d’Azure Import/Export | Documents Microsoft"
description: "Déterminer comment toobe de métadonnées et propriétés toospecify définies sur les objets BLOB de destination hello lors de l’exécution tooprepare d’outil d’importation/exportation Azure hello vos lecteurs."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 05c2b13bead793c8ab5aac6ce25816be97fffb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Définition des propriétés et métadonnées pendant hello processus d’importation

Lorsque vous exécutez hello Microsoft Azure Import/Export Tool tooprepare vos lecteurs, vous pouvez spécifier les propriétés et toobe de métadonnées définie sur les objets BLOB de destination hello. Procédez comme suit :

1.  propriétés d’objet blob tooset, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms de propriété.
2.  tooset métadonnées d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms de métadonnées.
3.  Passer tooone de chemin d’accès complet hello ou les deux de ces toohello fichiers outil d’importation/exportation Azure dans le cadre de hello `PrepImport` opération.

> [!NOTE]
>  Lorsque vous spécifiez un fichier de propriétés ou de métadonnées dans le cadre d’une session de copie, ces propriétés ou métadonnées sont définies pour chaque objet blob importé dans le cadre de cette session de copie. Si vous souhaitez toospecify un ensemble différent de propriétés ou les métadonnées des objets BLOB de hello importés, vous devez toocreate distinct copier la session avec des propriétés différentes ou des fichiers de métadonnées.

## <a name="specify-blob-properties-in-a-text-file"></a>Spécification des propriétés d’objets blob dans un fichier texte

propriétés d’objet blob toospecify, créez un fichier texte local et inclure du XML qui spécifie les noms de propriétés comme éléments et les valeurs de propriété sous forme de valeurs. Voici un exemple qui spécifie certaines valeurs de propriétés :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

Enregistrez l’emplacement local de tooa fichier hello comme `C:\WAImportExport\ImportProperties.txt`.

## <a name="specify-blob-metadata-in-a-text-file"></a>Spécification des métadonnées d’objets blob dans un fichier texte

De même, toospecify métadonnées d’objets blob, créez un fichier texte local qui spécifie les noms de métadonnées comme éléments et les valeurs de métadonnées en tant que valeurs. Voici un exemple qui spécifie certaines valeurs de métadonnées :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Enregistrez l’emplacement local de tooa fichier hello comme `C:\WAImportExport\ImportMetadata.txt`.

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a>Ajouter des fichiers tooproperties et les métadonnées du chemin d’accès hello dans dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a>Étapes suivantes

* [Format de fichier de propriétés et de métadonnées du service d’importation / exportation](storage-import-export-file-format-metadata-and-properties.md)
