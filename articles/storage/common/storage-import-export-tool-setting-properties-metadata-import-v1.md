---
title: "aaaSetting propriétés et des métadonnées à l’aide d’Azure Import/Export - v1 | Documents Microsoft"
description: "Déterminer comment toobe de métadonnées et propriétés toospecify définies sur les objets BLOB de destination hello lors de l’exécution tooprepare d’outil d’importation/exportation Azure hello vos lecteurs. Cela fait référence toov1 Hello outil d’importation/exportation."
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
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="a24fe-104">Définition des propriétés et métadonnées pendant hello processus d’importation</span><span class="sxs-lookup"><span data-stu-id="a24fe-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="a24fe-105">Lorsque vous exécutez hello Microsoft Azure Import/Export Tool tooprepare vos lecteurs, vous pouvez spécifier les propriétés et toobe de métadonnées définie sur les objets BLOB de destination hello.</span><span class="sxs-lookup"><span data-stu-id="a24fe-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="a24fe-106">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a24fe-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="a24fe-107">propriétés d’objet blob tooset, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms de propriété.</span><span class="sxs-lookup"><span data-stu-id="a24fe-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="a24fe-108">tooset métadonnées d’objets blob, créez un fichier texte sur votre ordinateur local qui spécifie les valeurs et les noms de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="a24fe-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="a24fe-109">Passer tooone de chemin d’accès complet hello ou les deux de ces toohello fichiers outil d’importation/exportation Azure dans le cadre de hello `PrepImport` opération.</span><span class="sxs-lookup"><span data-stu-id="a24fe-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="a24fe-110">Lorsque vous spécifiez un fichier de propriétés ou de métadonnées dans le cadre d’une session de copie, ces propriétés ou métadonnées sont définies pour chaque objet blob importé dans le cadre de cette session de copie.</span><span class="sxs-lookup"><span data-stu-id="a24fe-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="a24fe-111">Si vous souhaitez toospecify un ensemble différent de propriétés ou les métadonnées des objets BLOB de hello importés, vous devez toocreate distinct copier la session avec des propriétés différentes ou des fichiers de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="a24fe-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="a24fe-112">Spécification des propriétés d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="a24fe-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="a24fe-113">propriétés d’objet blob toospecify, créez un fichier texte local et inclure du XML qui spécifie les noms de propriétés comme éléments et les valeurs de propriété sous forme de valeurs.</span><span class="sxs-lookup"><span data-stu-id="a24fe-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="a24fe-114">Voici un exemple qui spécifie certaines valeurs de propriétés :</span><span class="sxs-lookup"><span data-stu-id="a24fe-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="a24fe-115">Enregistrez l’emplacement local de tooa fichier hello comme `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="a24fe-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="a24fe-116">Spécification des métadonnées d’objets blob dans un fichier texte</span><span class="sxs-lookup"><span data-stu-id="a24fe-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="a24fe-117">De même, toospecify métadonnées d’objets blob, créez un fichier texte local qui spécifie les noms de métadonnées comme éléments et les valeurs de métadonnées en tant que valeurs.</span><span class="sxs-lookup"><span data-stu-id="a24fe-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="a24fe-118">Voici un exemple qui spécifie certaines valeurs de métadonnées :</span><span class="sxs-lookup"><span data-stu-id="a24fe-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="a24fe-119">Enregistrez l’emplacement local de tooa fichier hello comme `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="a24fe-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="a24fe-120">Créer un hello notamment de Session de copie de fichiers de propriétés ou métadonnées</span><span class="sxs-lookup"><span data-stu-id="a24fe-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="a24fe-121">Lorsque vous exécutez la tâche d’importation hello outil d’importation/exportation Azure tooprepare hello, spécifiez le fichier des propriétés de ligne de commande hello à l’aide de hello hello `PropertyFile` paramètre.</span><span class="sxs-lookup"><span data-stu-id="a24fe-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="a24fe-122">Spécifiez le fichier de métadonnées hello sur la ligne de commande hello à l’aide de hello `/MetadataFile` paramètre.</span><span class="sxs-lookup"><span data-stu-id="a24fe-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="a24fe-123">Voici un exemple qui spécifie les deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="a24fe-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="a24fe-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a24fe-124">Next steps</span></span>

* [<span data-ttu-id="a24fe-125">Format de fichier de propriétés et de métadonnées du service d’importation / exportation</span><span class="sxs-lookup"><span data-stu-id="a24fe-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
