---
title: "l’utilisation des lecteurs pour un travail d’exportation Azure Import/Export - v1 aaaPreviewing | Documents Microsoft"
description: "Découvrez la liste de hello toopreview d’objets BLOB que vous avez sélectionné pour un travail d’exportation dans le service d’importation/exportation Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="8f32f-103">Aperçu de l’utilisation des lecteurs pour un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="8f32f-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="8f32f-104">Avant de créer un travail d’exportation, vous devez toochoose un ensemble d’objets BLOB toobe exporté.</span><span class="sxs-lookup"><span data-stu-id="8f32f-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="8f32f-105">Hello service Microsoft Azure Import/Export vous permet de toouse une liste de chemins d’accès de l’objet blob ou objet blob de préfixes d’objets BLOB de hello toorepresent que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="8f32f-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="8f32f-106">Ensuite, vous devez toodetermine, nombre de disques dont vous avez besoin de toosend.</span><span class="sxs-lookup"><span data-stu-id="8f32f-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="8f32f-107">Hello outil Import/Export fournit hello `PreviewExport` l’utilisation des lecteurs toopreview commande pour les objets BLOB de hello que vous avez sélectionné, en fonction de taille hello hello lecteurs que vous vous apprêtez toouse.</span><span class="sxs-lookup"><span data-stu-id="8f32f-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="8f32f-108">Paramètres de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="8f32f-108">Command-line parameters</span></span>

<span data-ttu-id="8f32f-109">Vous pouvez utiliser hello paramètres suivants lors de l’utilisation de hello `PreviewExport` commande Hello outil d’importation/exportation.</span><span class="sxs-lookup"><span data-stu-id="8f32f-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="8f32f-110">Paramètre de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="8f32f-110">Command-line parameter</span></span>|<span data-ttu-id="8f32f-111">Description</span><span class="sxs-lookup"><span data-stu-id="8f32f-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="8f32f-112">**/logdir:**&lt;LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="8f32f-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="8f32f-113">facultatif.</span><span class="sxs-lookup"><span data-stu-id="8f32f-113">Optional.</span></span> <span data-ttu-id="8f32f-114">répertoire de journal Hello.</span><span class="sxs-lookup"><span data-stu-id="8f32f-114">hello log directory.</span></span> <span data-ttu-id="8f32f-115">Les fichiers journaux détaillés seront écrit toothis active.</span><span class="sxs-lookup"><span data-stu-id="8f32f-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="8f32f-116">Si aucun répertoire de journal est spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello.</span><span class="sxs-lookup"><span data-stu-id="8f32f-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="8f32f-117">**/sn:**&lt;StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="8f32f-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="8f32f-118">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="8f32f-118">Required.</span></span> <span data-ttu-id="8f32f-119">tâche d’exportation de nom Hello hello du compte de stockage pour hello.</span><span class="sxs-lookup"><span data-stu-id="8f32f-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="8f32f-120">**/sk:**&lt;StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="8f32f-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="8f32f-121">Obligatoire si et seulement si aucune SAP de conteneur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8f32f-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="8f32f-122">tâche d’exportation de clé de compte Hello hello compte de stockage pour hello.</span><span class="sxs-lookup"><span data-stu-id="8f32f-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="8f32f-123">**/csas:**&lt;ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="8f32f-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="8f32f-124">Obligatoire si et seulement si aucune clé du compte de stockage n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8f32f-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="8f32f-125">SAP de conteneur Hello pour toobe d’objets BLOB annonce hello exportée dans le travail d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="8f32f-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="8f32f-126">**/ExportBlobListFile:**&lt;ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="8f32f-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="8f32f-127">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="8f32f-127">Required.</span></span> <span data-ttu-id="8f32f-128">Chemin d’accès toohello XML du fichier contenant la liste des chemins d’accès de l’objet blob ou préfixes de chemin d’accès pour toobe d’objets BLOB hello exportée d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="8f32f-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="8f32f-129">format de fichier Hello utilisé Bonjour `BlobListBlobPath` élément Bonjour [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération Hello API REST du service importation/exportation.</span><span class="sxs-lookup"><span data-stu-id="8f32f-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="8f32f-130">**/DriveSize:**&lt;DriveSize\></span><span class="sxs-lookup"><span data-stu-id="8f32f-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="8f32f-131">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="8f32f-131">Required.</span></span> <span data-ttu-id="8f32f-132">taille de toouse de lecteurs pour un travail d’exportation, de Hello *, par exemple*, 500 Go, 1,5 To.</span><span class="sxs-lookup"><span data-stu-id="8f32f-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="8f32f-133">Exemple de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="8f32f-133">Command-line example</span></span>

<span data-ttu-id="8f32f-134">exemple Hello illustre hello `PreviewExport` commande :</span><span class="sxs-lookup"><span data-stu-id="8f32f-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="8f32f-135">Hello blob liste et fichier d’exportation peut contenir des noms d’objet blob d’objets blob préfixes, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="8f32f-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="8f32f-136">Hello, outil d’importation/exportation Azure répertorie tous les objets BLOB toobe exporté et calcule comment toopack les lecteurs de hello spécifié la taille, en prenant en compte toute surcharge nécessaire, évalue ensuite le nombre de hello de lecteurs nécessaires blobs de hello toohold et l’utilisation des lecteurs plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8f32f-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="8f32f-137">Voici un exemple de sortie de hello, avec des journaux d’information omis :</span><span class="sxs-lookup"><span data-stu-id="8f32f-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="8f32f-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f32f-138">Next steps</span></span>

* [<span data-ttu-id="8f32f-139">Référence sur l’outil Azure Import-Export</span><span class="sxs-lookup"><span data-stu-id="8f32f-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
