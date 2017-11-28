---
title: "Définition des propriétés et des métadonnées avec Azure Import/Export - v1 | Microsoft Docs"
description: "Découvrez comment spécifier les propriétés et les métadonnées sur les objets blob de destination lors de l’exécution de l’outil Azure Import/Export pour préparer vos disques. Cela s’applique à la version v1 de l’outil d’importation/exportation."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 6455ce57572f9ec36d0ebae88c1ddd9f40f237bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="4e914-104">Définition des propriétés et métadonnées pendant le processus d’importation</span><span class="sxs-lookup"><span data-stu-id="4e914-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="4e914-105">Lorsque vous exécutez l’outil Microsoft Azure Import/Export pour préparer vos disques, vous pouvez spécifier des propriétés et des métadonnées à définir sur les objets blob de destination.</span><span class="sxs-lookup"><span data-stu-id="4e914-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="4e914-106">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e914-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="4e914-107">Pour définir les propriétés d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie la valeur et le nom des propriétés.</span><span class="sxs-lookup"><span data-stu-id="4e914-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="4e914-108">Pour définir les métadonnées d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="4e914-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="4e914-109">Transférez le chemin d’accès complet de l’un ou des deux fichiers à l’outil Azure Import/Export dans le cadre de l’opération `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="4e914-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="4e914-110">Lorsque vous spécifiez un fichier de propriétés ou de métadonnées dans le cadre d’une session de copie, ces propriétés ou métadonnées sont définies pour chaque objet blob importé dans le cadre de cette session de copie.</span><span class="sxs-lookup"><span data-stu-id="4e914-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="4e914-111">Si vous souhaitez spécifier un autre ensemble de propriétés ou de métadonnées pour certains des objets blob importés, vous devez créer une session de copie distincte avec des fichiers de propriétés ou de métadonnées différents.</span><span class="sxs-lookup"><span data-stu-id="4e914-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="4e914-112">Spécification des propriétés d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="4e914-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="4e914-113">Pour spécifier les propriétés d’objets blob, créez un fichier texte local et incluez un fichier XML qui spécifie les noms des propriétés en tant qu’éléments et les valeurs des propriétés en tant que valeurs.</span><span class="sxs-lookup"><span data-stu-id="4e914-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="4e914-114">Voici un exemple qui spécifie certaines valeurs de propriétés :</span><span class="sxs-lookup"><span data-stu-id="4e914-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="4e914-115">Enregistrez le fichier dans un emplacement local comme `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="4e914-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="4e914-116">Spécification des métadonnées d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="4e914-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="4e914-117">De même, pour spécifier les métadonnées d’objets blob, créez un fichier texte local qui spécifie les noms des métadonnées en tant qu’éléments et les valeurs des métadonnées en tant que valeurs.</span><span class="sxs-lookup"><span data-stu-id="4e914-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="4e914-118">Voici un exemple qui spécifie certaines valeurs de métadonnées :</span><span class="sxs-lookup"><span data-stu-id="4e914-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="4e914-119">Enregistrez le fichier dans un emplacement local comme `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="4e914-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="4e914-120">Créer une session de copie comprenant les fichiers de propriétés ou de métadonnées</span><span class="sxs-lookup"><span data-stu-id="4e914-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="4e914-121">Lorsque vous exécutez l’outil Azure Import/Export pour préparer le travail d’importation, spécifiez le fichier de propriétés en ligne de commande à l’aide du paramètre `PropertyFile`.</span><span class="sxs-lookup"><span data-stu-id="4e914-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="4e914-122">Spécifiez le fichier de métadonnées en ligne de commande à l’aide du paramètre`/MetadataFile`.</span><span class="sxs-lookup"><span data-stu-id="4e914-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="4e914-123">Voici un exemple qui spécifie les deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="4e914-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="4e914-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e914-124">Next steps</span></span>

* [<span data-ttu-id="4e914-125">Format de fichier de propriétés et de métadonnées du service d’importation / exportation</span><span class="sxs-lookup"><span data-stu-id="4e914-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
