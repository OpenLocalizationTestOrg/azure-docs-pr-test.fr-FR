---
title: "Aperçu de l’utilisation d’un lecteur pour un travail d’exportation Azure Import/Export - v1 | Microsoft Docs"
description: "Découvrez comment afficher un aperçu de la liste d’objets blob que vous avez sélectionnés pour un travail d’exportation dans le service Azure Import-Export."
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
ms.openlocfilehash: 6ec74ae0b0931f3fed99a43f4f7e58f9d425b138
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="0d6c9-103">Aperçu de l’utilisation des lecteurs pour un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="0d6c9-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="0d6c9-104">Avant de créer un travail d’exportation, vous devez choisir un ensemble d’objets blob à exporter.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="0d6c9-105">Le service Microsoft Azure Import/Export vous permet d’utiliser une liste de chemins d’accès ou de préfixes d’objets blob pour représenter les objets blob que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="0d6c9-106">Ensuite, vous devez déterminer le nombre de lecteurs à envoyer.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="0d6c9-107">L’outil Import/Export offre la commande `PreviewExport` permettant d’afficher un aperçu de l’utilisation du disque pour les objets blob que vous avez sélectionnés, en fonction de la taille des disques que vous voulez utiliser.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="0d6c9-108">Paramètres de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="0d6c9-108">Command-line parameters</span></span>

<span data-ttu-id="0d6c9-109">Vous pouvez utiliser les paramètres suivants lorsque vous utilisez la commande `PreviewExport` de l’outil Import/Export.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="0d6c9-110">Paramètre de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="0d6c9-110">Command-line parameter</span></span>|<span data-ttu-id="0d6c9-111">Description</span><span class="sxs-lookup"><span data-stu-id="0d6c9-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="0d6c9-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="0d6c9-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="0d6c9-113">facultatif.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-113">Optional.</span></span> <span data-ttu-id="0d6c9-114">Répertoire contenant les journaux.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-114">The log directory.</span></span> <span data-ttu-id="0d6c9-115">Les fichiers journaux détaillés seront écrits dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="0d6c9-116">Si aucun répertoire de journaux n’est spécifié, le répertoire courant est utilisé comme répertoire de journaux.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="0d6c9-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="0d6c9-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="0d6c9-118">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-118">Required.</span></span> <span data-ttu-id="0d6c9-119">Nom du compte de stockage du travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="0d6c9-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="0d6c9-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="0d6c9-121">Obligatoire si et seulement si aucune SAP de conteneur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="0d6c9-122">Clé du compte de stockage du travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="0d6c9-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="0d6c9-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="0d6c9-124">Obligatoire si et seulement si aucune clé du compte de stockage n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="0d6c9-125">SAP du conteneur pour lister les objets blob à exporter dans le travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="0d6c9-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="0d6c9-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="0d6c9-127">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-127">Required.</span></span> <span data-ttu-id="0d6c9-128">Chemin d’accès au fichier XML contenant la liste des chemins d’accès ou des préfixes de chemin d’accès aux objets blob à exporter.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="0d6c9-129">Format du fichier utilisé dans l’élément `BlobListBlobPath` dans l’opération [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) de l’API REST du service Import/Export.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="0d6c9-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="0d6c9-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="0d6c9-131">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-131">Required.</span></span> <span data-ttu-id="0d6c9-132">Taille des disques à utiliser pour un travail d’exportation, *par exemple* 500 Go ou 1,5 To.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="0d6c9-133">Exemple de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="0d6c9-133">Command-line example</span></span>

<span data-ttu-id="0d6c9-134">L’exemple suivant illustre la commande `PreviewExport` :</span><span class="sxs-lookup"><span data-stu-id="0d6c9-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="0d6c9-135">Le fichier de liste d’objets blob à exporter peut contenir des noms et des préfixes d’objets blob, comme l’illustre ce code :</span><span class="sxs-lookup"><span data-stu-id="0d6c9-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="0d6c9-136">L’outil Azure Import/Export liste tous les objets blob à exporter et calcule leur répartition sur des lecteurs de la taille spécifiée, en prenant en compte les éventuelles surcharges nécessaires, puis évalue le nombre de disques requis pour contenir les objets blob et les informations sur l’utilisation des lecteurs.</span><span class="sxs-lookup"><span data-stu-id="0d6c9-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="0d6c9-137">Voici un exemple de sortie, les journaux d’information étant omis :</span><span class="sxs-lookup"><span data-stu-id="0d6c9-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="0d6c9-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d6c9-138">Next steps</span></span>

* [<span data-ttu-id="0d6c9-139">Référence sur l’outil Azure Import-Export</span><span class="sxs-lookup"><span data-stu-id="0d6c9-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
