---
title: "Définition des propriétés et des métadonnées avec Azure Import/Export | Microsoft Docs |"
description: "Découvrez comment spécifier les propriétés et les métadonnées sur les objets blob de destination lors de l’exécution de l’outil Azure Import/Export pour préparer vos disques."
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
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="c8d10-103">Définition des propriétés et métadonnées pendant le processus d’importation</span><span class="sxs-lookup"><span data-stu-id="c8d10-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="c8d10-104">Lorsque vous exécutez l’outil Microsoft Azure Import/Export pour préparer vos disques, vous pouvez spécifier des propriétés et des métadonnées à définir sur les objets blob de destination.</span><span class="sxs-lookup"><span data-stu-id="c8d10-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="c8d10-105">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8d10-105">Follow these steps:</span></span>

1.  <span data-ttu-id="c8d10-106">Pour définir les propriétés d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie la valeur et le nom des propriétés.</span><span class="sxs-lookup"><span data-stu-id="c8d10-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="c8d10-107">Pour définir les métadonnées d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="c8d10-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="c8d10-108">Transférez le chemin d’accès complet de l’un ou des deux fichiers à l’outil Azure Import/Export dans le cadre de l’opération `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="c8d10-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="c8d10-109">Lorsque vous spécifiez un fichier de propriétés ou de métadonnées dans le cadre d’une session de copie, ces propriétés ou métadonnées sont définies pour chaque objet blob importé dans le cadre de cette session de copie.</span><span class="sxs-lookup"><span data-stu-id="c8d10-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="c8d10-110">Si vous souhaitez spécifier un autre ensemble de propriétés ou de métadonnées pour certains des objets blob importés, vous devez créer une session de copie distincte avec des fichiers de propriétés ou de métadonnées différents.</span><span class="sxs-lookup"><span data-stu-id="c8d10-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="c8d10-111">Spécification des propriétés d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="c8d10-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="c8d10-112">Pour spécifier les propriétés d’objets blob, créez un fichier texte local et incluez un fichier XML qui spécifie les noms de propriétés en tant qu’éléments et les valeurs des propriétés en tant que valeurs.</span><span class="sxs-lookup"><span data-stu-id="c8d10-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="c8d10-113">Voici un exemple qui spécifie certaines valeurs de propriétés :</span><span class="sxs-lookup"><span data-stu-id="c8d10-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="c8d10-114">Enregistrez le fichier dans un emplacement local comme `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="c8d10-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="c8d10-115">Spécification des métadonnées d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="c8d10-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="c8d10-116">De même, pour spécifier les métadonnées d’objets blob, créez un fichier texte local qui spécifie les noms des métadonnées en tant qu’éléments et les valeurs des métadonnées en tant que valeurs.</span><span class="sxs-lookup"><span data-stu-id="c8d10-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="c8d10-117">Voici un exemple qui spécifie certaines valeurs de métadonnées :</span><span class="sxs-lookup"><span data-stu-id="c8d10-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="c8d10-118">Enregistrez le fichier dans un emplacement local comme `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="c8d10-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="c8d10-119">Ajoutez le chemin d’accès aux fichiers de propriétés et de métadonnées dans dataset.csv</span><span class="sxs-lookup"><span data-stu-id="c8d10-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="c8d10-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8d10-120">Next steps</span></span>

* [<span data-ttu-id="c8d10-121">Format de fichier de propriétés et de métadonnées du service d’importation / exportation</span><span class="sxs-lookup"><span data-stu-id="c8d10-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
