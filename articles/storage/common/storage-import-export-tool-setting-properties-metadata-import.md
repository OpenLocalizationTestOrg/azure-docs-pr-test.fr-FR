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
ms.openlocfilehash: c763237160f0e4b72ce88fd31e2958994bfe8e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="82d93-103">Définition des propriétés et métadonnées pendant hello processus d’importation</span><span class="sxs-lookup"><span data-stu-id="82d93-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="82d93-104">Lorsque vous exécutez hello Microsoft Azure Import/Export Tool tooprepare vos lecteurs, vous pouvez spécifier les propriétés et toobe de métadonnées définie sur les objets BLOB de destination hello.</span><span class="sxs-lookup"><span data-stu-id="82d93-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="82d93-105">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="82d93-105">Follow these steps:</span></span>

1.  <span data-ttu-id="82d93-106">propriétés d’objet blob tooset, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms de propriété.</span><span class="sxs-lookup"><span data-stu-id="82d93-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="82d93-107">tooset métadonnées d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="82d93-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="82d93-108">Passer tooone de chemin d’accès complet hello ou les deux de ces toohello fichiers outil d’importation/exportation Azure dans le cadre de hello `PrepImport` opération.</span><span class="sxs-lookup"><span data-stu-id="82d93-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="82d93-109">Lorsque vous spécifiez un fichier de propriétés ou de métadonnées dans le cadre d’une session de copie, ces propriétés ou métadonnées sont définies pour chaque objet blob importé dans le cadre de cette session de copie.</span><span class="sxs-lookup"><span data-stu-id="82d93-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="82d93-110">Si vous souhaitez toospecify un ensemble différent de propriétés ou les métadonnées des objets BLOB de hello importés, vous devez toocreate distinct copier la session avec des propriétés différentes ou des fichiers de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="82d93-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="82d93-111">Spécification des propriétés d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="82d93-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="82d93-112">propriétés d’objet blob toospecify, créez un fichier texte local et inclure du XML qui spécifie les noms de propriétés comme éléments et les valeurs de propriété sous forme de valeurs.</span><span class="sxs-lookup"><span data-stu-id="82d93-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="82d93-113">Voici un exemple qui spécifie certaines valeurs de propriétés :</span><span class="sxs-lookup"><span data-stu-id="82d93-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="82d93-114">Enregistrez l’emplacement local de tooa fichier hello comme `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="82d93-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="82d93-115">Spécification des métadonnées d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="82d93-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="82d93-116">De même, toospecify métadonnées d’objets blob, créez un fichier texte local qui spécifie les noms de métadonnées comme éléments et les valeurs de métadonnées en tant que valeurs.</span><span class="sxs-lookup"><span data-stu-id="82d93-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="82d93-117">Voici un exemple qui spécifie certaines valeurs de métadonnées :</span><span class="sxs-lookup"><span data-stu-id="82d93-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="82d93-118">Enregistrez l’emplacement local de tooa fichier hello comme `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="82d93-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="82d93-119">Ajouter des fichiers tooproperties et les métadonnées du chemin d’accès hello dans dataset.csv</span><span class="sxs-lookup"><span data-stu-id="82d93-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="82d93-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82d93-120">Next steps</span></span>

* [<span data-ttu-id="82d93-121">Format de fichier de propriétés et de métadonnées du service d’importation / exportation</span><span class="sxs-lookup"><span data-stu-id="82d93-121">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
