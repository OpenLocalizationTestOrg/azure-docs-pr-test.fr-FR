---
title: "Format de fichier journal d’Azure Import/Export | Microsoft Docs"
description: "Découvrez-en davantage sur le format des fichiers journaux créés lors de l’exécution des étapes d’un travail du service d’importation/exportation."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="6d45d-103">Format de fichier journal du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="6d45d-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="6d45d-104">Lorsque le service Microsoft Azure Import/Export exécute une action sur un lecteur dans le cadre d’un travail d’importation ou d’exportation, les journaux sont écrits pour bloquer des objets blob dans le compte de stockage associé à ce travail.</span><span class="sxs-lookup"><span data-stu-id="6d45d-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="6d45d-105">Il existe deux journaux pouvant être écrits par le service d’importation/exportation :</span><span class="sxs-lookup"><span data-stu-id="6d45d-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="6d45d-106">Le journal d’erreurs est toujours généré en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="6d45d-107">Le journal détaillé n’est pas activé par défaut, mais il peut être activé en définissant la propriété `EnableVerboseLog` sur une opération [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="6d45d-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="6d45d-108">Emplacement du fichier journal</span><span class="sxs-lookup"><span data-stu-id="6d45d-108">Log file location</span></span>  
<span data-ttu-id="6d45d-109">Les journaux sont écrits pour bloquer des objets blob dans le conteneur ou le répertoire virtuel spécifié par le paramètre `ImportExportStatesPath`, que vous pouvez définir sur une opération `Put Job`.</span><span class="sxs-lookup"><span data-stu-id="6d45d-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="6d45d-110">L’emplacement dans lequel les journaux sont écrits dépend de la façon dont l’authentification est spécifiée pour le travail, ainsi que de la valeur spécifiée pour `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="6d45d-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="6d45d-111">L’authentification du travail peut être spécifiée via une clé de compte de stockage ou une SAP (signature d’accès partagé) de conteneur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="6d45d-112">Le nom du conteneur ou du répertoire virtuel peut être le nom par défaut `waimportexport` ou le nom d’un autre conteneur ou répertoire virtuel que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="6d45d-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="6d45d-113">Le tableau ci-dessous présente les options possibles :</span><span class="sxs-lookup"><span data-stu-id="6d45d-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="6d45d-114">Méthode d’authentification</span><span class="sxs-lookup"><span data-stu-id="6d45d-114">Authentication Method</span></span>|<span data-ttu-id="6d45d-115">Valeur de l’élément `ImportExportStatesPath`</span><span class="sxs-lookup"><span data-stu-id="6d45d-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="6d45d-116">Emplacement des objets blob de journal</span><span class="sxs-lookup"><span data-stu-id="6d45d-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="6d45d-117">Clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="6d45d-117">Storage account key</span></span>|<span data-ttu-id="6d45d-118">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="6d45d-118">Default value</span></span>|<span data-ttu-id="6d45d-119">Un conteneur nommé `waimportexport`, qui est le conteneur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6d45d-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="6d45d-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6d45d-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="6d45d-121">Clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="6d45d-121">Storage account key</span></span>|<span data-ttu-id="6d45d-122">Valeur spécifiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6d45d-122">User-specified value</span></span>|<span data-ttu-id="6d45d-123">Un conteneur nommé par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-123">A container named by the user.</span></span> <span data-ttu-id="6d45d-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6d45d-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="6d45d-125">SAP de conteneur</span><span class="sxs-lookup"><span data-stu-id="6d45d-125">Container SAS</span></span>|<span data-ttu-id="6d45d-126">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="6d45d-126">Default value</span></span>|<span data-ttu-id="6d45d-127">Un répertoire virtuel nommé `waimportexport`, qui est le nom par défaut, sous le conteneur spécifié dans la SAP.</span><span class="sxs-lookup"><span data-stu-id="6d45d-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="6d45d-128">Par exemple, si la SAP spécifiée pour le travail est `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, l’emplacement du journal serait alors `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="6d45d-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="6d45d-129">SAP de conteneur</span><span class="sxs-lookup"><span data-stu-id="6d45d-129">Container SAS</span></span>|<span data-ttu-id="6d45d-130">Valeur spécifiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6d45d-130">User-specified value</span></span>|<span data-ttu-id="6d45d-131">Un répertoire virtuel nommé par l’utilisateur, sous le conteneur spécifié dans la SAP.</span><span class="sxs-lookup"><span data-stu-id="6d45d-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="6d45d-132">Par exemple, si la SAP spécifiée pour le travail est `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue` et le répertoire virtuel spécifié est nommé `mylogblobs`, l’emplacement du journal serait `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="6d45d-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="6d45d-133">Vous pouvez récupérer l’URL de l’erreur et les journaux détaillés en appelant l’opération [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="6d45d-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="6d45d-134">Les journaux sont disponibles dès que le traitement du lecteur est terminé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="6d45d-135">Format de fichier journal</span><span class="sxs-lookup"><span data-stu-id="6d45d-135">Log file format</span></span>  
<span data-ttu-id="6d45d-136">Le format de ces deux journaux est le même : un objet blob contenant des descriptions XML des événements qui se sont produits lors de la copie des objets blob entre le disque dur et le compte du client.</span><span class="sxs-lookup"><span data-stu-id="6d45d-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="6d45d-137">Le journal détaillé contient des informations complètes sur l’état de l’opération de copie pour chaque objet blob (pour un travail d’importation) ou un fichier (pour un travail d’exportation), alors que le journal d’erreurs contient uniquement les informations des objets blob ou fichiers qui ont rencontré des erreurs lors du travail d’importation ou d’exportation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="6d45d-138">Le format du journal détaillé est illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6d45d-138">The verbose log format is shown below.</span></span> <span data-ttu-id="6d45d-139">Le journal d’erreurs a la même structure mais il exclut les opérations réussies.</span><span class="sxs-lookup"><span data-stu-id="6d45d-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="6d45d-140">Le tableau suivant décrit les éléments du fichier journal.</span><span class="sxs-lookup"><span data-stu-id="6d45d-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="6d45d-141">Élément XML</span><span class="sxs-lookup"><span data-stu-id="6d45d-141">XML Element</span></span>|<span data-ttu-id="6d45d-142">Type</span><span class="sxs-lookup"><span data-stu-id="6d45d-142">Type</span></span>|<span data-ttu-id="6d45d-143">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="6d45d-144">Élément XML</span><span class="sxs-lookup"><span data-stu-id="6d45d-144">XML Element</span></span>|<span data-ttu-id="6d45d-145">Représente un journal de lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="6d45d-146">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-146">Attribute, String</span></span>|<span data-ttu-id="6d45d-147">Version du format du journal.</span><span class="sxs-lookup"><span data-stu-id="6d45d-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="6d45d-148">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-148">String</span></span>|<span data-ttu-id="6d45d-149">Numéro de série du matériel du lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="6d45d-150">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-150">String</span></span>|<span data-ttu-id="6d45d-151">État de traitement du lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-151">Status of the drive processing.</span></span> <span data-ttu-id="6d45d-152">Pour plus d’informations, consultez le tableau `Drive Status Codes` ci-après.</span><span class="sxs-lookup"><span data-stu-id="6d45d-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="6d45d-153">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="6d45d-153">Nested XML element</span></span>|<span data-ttu-id="6d45d-154">Représente un objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="6d45d-155">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-155">String</span></span>|<span data-ttu-id="6d45d-156">URI de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="6d45d-157">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-157">String</span></span>|<span data-ttu-id="6d45d-158">Chemin relatif d’accès au fichier sur le lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="6d45d-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="6d45d-159">DateTime</span></span>|<span data-ttu-id="6d45d-160">Version de l’instantané de l’objet blob, pour un travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="6d45d-161">Entier </span><span class="sxs-lookup"><span data-stu-id="6d45d-161">Integer</span></span>|<span data-ttu-id="6d45d-162">Longueur totale de l’objet blob en octets.</span><span class="sxs-lookup"><span data-stu-id="6d45d-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="6d45d-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="6d45d-163">DateTime</span></span>|<span data-ttu-id="6d45d-164">Date/heure de dernière modification de l’objet blob, pour un travail d’exportation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="6d45d-165">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-165">String</span></span>|<span data-ttu-id="6d45d-166">Disposition d’importation de l’objet blob, pour un travail d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="6d45d-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="6d45d-167">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-167">Attribute, String</span></span>|<span data-ttu-id="6d45d-168">État de la disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="6d45d-169">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="6d45d-169">Nested XML element</span></span>|<span data-ttu-id="6d45d-170">Représente une liste de plages de pages pour un objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="6d45d-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="6d45d-171">Élément XML</span><span class="sxs-lookup"><span data-stu-id="6d45d-171">XML element</span></span>|<span data-ttu-id="6d45d-172">Représente une plage de pages.</span><span class="sxs-lookup"><span data-stu-id="6d45d-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="6d45d-173">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="6d45d-173">Attribute, Integer</span></span>|<span data-ttu-id="6d45d-174">Décalage de début de la plage de pages dans l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="6d45d-175">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="6d45d-175">Attribute, Integer</span></span>|<span data-ttu-id="6d45d-176">Longueur en octets de la plage de pages.</span><span class="sxs-lookup"><span data-stu-id="6d45d-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="6d45d-177">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-177">Attribute, String</span></span>|<span data-ttu-id="6d45d-178">Hachage MD5 encodé en Base16 de la plage de pages.</span><span class="sxs-lookup"><span data-stu-id="6d45d-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="6d45d-179">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-179">Attribute, String</span></span>|<span data-ttu-id="6d45d-180">État du traitement de la plage de pages.</span><span class="sxs-lookup"><span data-stu-id="6d45d-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="6d45d-181">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="6d45d-181">Nested XML element</span></span>|<span data-ttu-id="6d45d-182">Représente une liste de blocs pour un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="6d45d-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="6d45d-183">Élément XML</span><span class="sxs-lookup"><span data-stu-id="6d45d-183">XML element</span></span>|<span data-ttu-id="6d45d-184">Représente un bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="6d45d-185">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="6d45d-185">Attribute, Integer</span></span>|<span data-ttu-id="6d45d-186">Décalage de début du bloc dans l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="6d45d-187">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="6d45d-187">Attribute, Integer</span></span>|<span data-ttu-id="6d45d-188">Longueur du bloc en octets.</span><span class="sxs-lookup"><span data-stu-id="6d45d-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="6d45d-189">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-189">Attribute, String</span></span>|<span data-ttu-id="6d45d-190">ID du bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="6d45d-191">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-191">Attribute, String</span></span>|<span data-ttu-id="6d45d-192">Hachage MD5 encodé en Base16 du bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="6d45d-193">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-193">Attribute, String</span></span>|<span data-ttu-id="6d45d-194">État du traitement du bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="6d45d-195">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="6d45d-195">Nested XML element</span></span>|<span data-ttu-id="6d45d-196">Représente les métadonnées de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="6d45d-197">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-197">Attribute, String</span></span>|<span data-ttu-id="6d45d-198">État de traitement des métadonnées de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="6d45d-199">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-199">String</span></span>|<span data-ttu-id="6d45d-200">Chemin relatif d’accès au fichier de métadonnées global.</span><span class="sxs-lookup"><span data-stu-id="6d45d-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="6d45d-201">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-201">Attribute, String</span></span>|<span data-ttu-id="6d45d-202">Hachage MD5 encodé en Base16 du fichier de métadonnées global.</span><span class="sxs-lookup"><span data-stu-id="6d45d-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="6d45d-203">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-203">String</span></span>|<span data-ttu-id="6d45d-204">Chemin relatif d’accès au fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="6d45d-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="6d45d-205">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-205">Attribute, String</span></span>|<span data-ttu-id="6d45d-206">Hachage MD5 encodé en Base16 du fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="6d45d-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="6d45d-207">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="6d45d-207">Nested XML element</span></span>|<span data-ttu-id="6d45d-208">Représente les propriétés de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="6d45d-209">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-209">Attribute, String</span></span>|<span data-ttu-id="6d45d-210">État de traitement des propriétés de l’objet blob, par exemple, fichier introuvable, terminé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="6d45d-211">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-211">String</span></span>|<span data-ttu-id="6d45d-212">Chemin relatif d’accès au fichier de propriétés global.</span><span class="sxs-lookup"><span data-stu-id="6d45d-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="6d45d-213">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-213">Attribute, String</span></span>|<span data-ttu-id="6d45d-214">Hachage MD5 encodé en Base16 du fichier de propriétés global.</span><span class="sxs-lookup"><span data-stu-id="6d45d-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="6d45d-215">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-215">String</span></span>|<span data-ttu-id="6d45d-216">Chemin relatif d’accès au fichier de propriétés.</span><span class="sxs-lookup"><span data-stu-id="6d45d-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="6d45d-217">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="6d45d-217">Attribute, String</span></span>|<span data-ttu-id="6d45d-218">Hachage MD5 encodé en Base16 du fichier de propriétés.</span><span class="sxs-lookup"><span data-stu-id="6d45d-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="6d45d-219">String</span><span class="sxs-lookup"><span data-stu-id="6d45d-219">String</span></span>|<span data-ttu-id="6d45d-220">État du traitement de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="6d45d-221">Codes d’état du lecteur</span><span class="sxs-lookup"><span data-stu-id="6d45d-221">Drive status codes</span></span>  
<span data-ttu-id="6d45d-222">Le tableau suivant répertorie les codes d’état pour le traitement d’un lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="6d45d-223">Code d’état</span><span class="sxs-lookup"><span data-stu-id="6d45d-223">Status code</span></span>|<span data-ttu-id="6d45d-224">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="6d45d-225">Le traitement du lecteur s’est terminé sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="6d45d-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="6d45d-226">Le lecteur a terminé le traitement avec des avertissements dans un ou plusieurs objets blob selon les dispositions d’importation spécifiées pour les objets blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="6d45d-227">Le lecteur a terminé avec des erreurs dans un ou plusieurs objets blob ou segments.</span><span class="sxs-lookup"><span data-stu-id="6d45d-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="6d45d-228">Aucun disque ne se trouve sur le lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="6d45d-229">Le premier volume de données sur le disque n’est pas au format NTFS.</span><span class="sxs-lookup"><span data-stu-id="6d45d-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="6d45d-230">Une erreur inconnue s’est produite lors de l’exécution d’opérations sur le lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="6d45d-231">Aucun volume BitLocker chiffrable n’a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="6d45d-232">BitLocker n’est pas activé sur le volume.</span><span class="sxs-lookup"><span data-stu-id="6d45d-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="6d45d-233">Le protecteur de clé de mot de passe numérique n’existe pas sur le volume.</span><span class="sxs-lookup"><span data-stu-id="6d45d-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="6d45d-234">Le mot de passe numérique fourni ne peut pas déverrouiller le volume.</span><span class="sxs-lookup"><span data-stu-id="6d45d-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="6d45d-235">Une erreur inconnue s’est produite lors de la tentative de déverrouillage du volume.</span><span class="sxs-lookup"><span data-stu-id="6d45d-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="6d45d-236">Une erreur inconnue s’est produite lors de l’exécution d’opérations BitLocker.</span><span class="sxs-lookup"><span data-stu-id="6d45d-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="6d45d-237">Le nom du fichier manifeste n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="6d45d-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="6d45d-238">Le nom du fichier manifeste est trop long.</span><span class="sxs-lookup"><span data-stu-id="6d45d-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="6d45d-239">Le fichier manifeste est introuvable.</span><span class="sxs-lookup"><span data-stu-id="6d45d-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="6d45d-240">L’accès au fichier manifeste est refusé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="6d45d-241">Le fichier manifeste est endommagé (le contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="6d45d-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="6d45d-242">Le contenu du manifeste n’est pas conforme au format requis.</span><span class="sxs-lookup"><span data-stu-id="6d45d-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="6d45d-243">L’ID du lecteur dans le fichier manifeste ne correspond pas à celui lu à partir du lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="6d45d-244">Un erreur d’E/S du disque s’est produite lors de la lecture à partir du manifeste.</span><span class="sxs-lookup"><span data-stu-id="6d45d-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="6d45d-245">L’objet blob de la liste d’objets blob d’exportation n’est pas conforme au format requis.</span><span class="sxs-lookup"><span data-stu-id="6d45d-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="6d45d-246">L’accès aux objets blob dans le compte de stockage est interdit.</span><span class="sxs-lookup"><span data-stu-id="6d45d-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="6d45d-247">Cela peut être dû à une clé de compte de stockage ou une SAP de conteneur non valide.</span><span class="sxs-lookup"><span data-stu-id="6d45d-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="6d45d-248">Une erreur interne s'est produite lors du traitement du lecteur.</span><span class="sxs-lookup"><span data-stu-id="6d45d-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="6d45d-249">Codes d’état de l’objet blob</span><span class="sxs-lookup"><span data-stu-id="6d45d-249">Blob status codes</span></span>  
<span data-ttu-id="6d45d-250">Le tableau suivant répertorie les codes d’état pour le traitement d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="6d45d-251">Code d’état</span><span class="sxs-lookup"><span data-stu-id="6d45d-251">Status code</span></span>|<span data-ttu-id="6d45d-252">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="6d45d-253">Le traitement de l’objet blob s’est terminé sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="6d45d-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="6d45d-254">Le traitement de l’objet blob s’est terminé avec des erreurs dans une ou plusieurs plages de pages ou blocs, métadonnées ou propriétés.</span><span class="sxs-lookup"><span data-stu-id="6d45d-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="6d45d-255">Le nom du fichier n'est pas valide.</span><span class="sxs-lookup"><span data-stu-id="6d45d-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="6d45d-256">Le nom du fichier est trop long.</span><span class="sxs-lookup"><span data-stu-id="6d45d-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="6d45d-257">Le fichier est introuvable.</span><span class="sxs-lookup"><span data-stu-id="6d45d-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="6d45d-258">L’accès au fichier est refusé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="6d45d-259">La demande de service Blob pour accéder à l’objet blob a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="6d45d-260">La demande de service Blob pour accéder à l’objet blob est interdite.</span><span class="sxs-lookup"><span data-stu-id="6d45d-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="6d45d-261">Cela peut être dû à une clé de compte de stockage ou une SAP de conteneur non valide.</span><span class="sxs-lookup"><span data-stu-id="6d45d-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="6d45d-262">Impossible de renommer l’objet blob (pour un travail d’importation) ou le fichier (pour un travail d’exportation).</span><span class="sxs-lookup"><span data-stu-id="6d45d-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="6d45d-263">Une modification inattendue s’est produite avec l’objet blob (pour un travail d’exportation).</span><span class="sxs-lookup"><span data-stu-id="6d45d-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="6d45d-264">Il existe un bail sur l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="6d45d-265">Une erreur d’E/S du disque ou réseau s’est produite lors du traitement de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="6d45d-266">Une erreur inconnue s’est produite lors du traitement de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="6d45d-267">Codes d’état de disposition d’importation</span><span class="sxs-lookup"><span data-stu-id="6d45d-267">Import disposition status codes</span></span>  
<span data-ttu-id="6d45d-268">Le tableau suivant répertorie les codes d’état de résolution d’une disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="6d45d-269">Code d’état</span><span class="sxs-lookup"><span data-stu-id="6d45d-269">Status code</span></span>|<span data-ttu-id="6d45d-270">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="6d45d-271">L’objet blob a été créé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="6d45d-272">L’objet blob a été renommé en fonction de la disposition d’importation de changement de nom.</span><span class="sxs-lookup"><span data-stu-id="6d45d-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="6d45d-273">L’élément `Blob/BlobPath` contient l’URI de l’objet blob renommé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="6d45d-274">L’objet blob a été ignoré en fonction de la disposition d’importation `no-overwrite`.</span><span class="sxs-lookup"><span data-stu-id="6d45d-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="6d45d-275">L’objet blob a remplacé un objet blob existant en fonction de la disposition d’importation `overwrite`.</span><span class="sxs-lookup"><span data-stu-id="6d45d-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="6d45d-276">Une erreur précédente a arrêté le traitement de la disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="6d45d-277">Codes d’état de plage de pages/de bloc</span><span class="sxs-lookup"><span data-stu-id="6d45d-277">Page range/block status codes</span></span>  
<span data-ttu-id="6d45d-278">Le tableau suivant répertorie les codes d’état pour le traitement d’une plage de pages ou d’un bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="6d45d-279">Code d’état</span><span class="sxs-lookup"><span data-stu-id="6d45d-279">Status code</span></span>|<span data-ttu-id="6d45d-280">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="6d45d-281">Le traitement de la plage de pages ou du bloc s’est terminé sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="6d45d-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="6d45d-282">Le bloc a été validé, mais pas dans la liste de blocs complète car d’autres blocs ont échoué, ou la liste de blocs complète elle-même a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="6d45d-283">Le bloc est téléchargé mais non validé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="6d45d-284">La plage de pages ou le bloc est endommagé (le contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="6d45d-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="6d45d-285">Une fin de fichier inattendue a été rencontrée.</span><span class="sxs-lookup"><span data-stu-id="6d45d-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="6d45d-286">Une fin d’objet blob inattendue a été rencontrée.</span><span class="sxs-lookup"><span data-stu-id="6d45d-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="6d45d-287">La demande de service Blob pour accéder à la plage de pages ou au bloc a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="6d45d-288">Une erreur d’E/S du disque ou réseau s’est produite lors du traitement de la plage de pages ou du bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="6d45d-289">Une erreur inconnue s’est produite lors du traitement de la plage de pages ou du bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="6d45d-290">Une erreur précédente a arrêté le traitement de la plage de pages ou du bloc.</span><span class="sxs-lookup"><span data-stu-id="6d45d-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="6d45d-291">Codes d’état des métadonnées</span><span class="sxs-lookup"><span data-stu-id="6d45d-291">Metadata status codes</span></span>  
<span data-ttu-id="6d45d-292">Le tableau suivant répertorie les codes d’état pour le traitement des métadonnées d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="6d45d-293">Code d’état</span><span class="sxs-lookup"><span data-stu-id="6d45d-293">Status code</span></span>|<span data-ttu-id="6d45d-294">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="6d45d-295">Le traitement des métadonnées s’est terminé sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="6d45d-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="6d45d-296">Le nom du fichier de métadonnées n'est pas valide.</span><span class="sxs-lookup"><span data-stu-id="6d45d-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="6d45d-297">Le nom du fichier de métadonnées est trop long.</span><span class="sxs-lookup"><span data-stu-id="6d45d-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="6d45d-298">Le fichier de métadonnées est introuvable.</span><span class="sxs-lookup"><span data-stu-id="6d45d-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="6d45d-299">L’accès au fichier de métadonnées est refusé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="6d45d-300">Le fichier de métadonnées est endommagé (le contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="6d45d-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="6d45d-301">Le contenu des métadonnées n’est pas conforme au format requis.</span><span class="sxs-lookup"><span data-stu-id="6d45d-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="6d45d-302">L’écriture des métadonnées XML a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="6d45d-303">La demande de service Blob pour accéder aux métadonnées a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="6d45d-304">Une erreur d’E/S du disque ou réseau s’est produite lors du traitement des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="6d45d-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="6d45d-305">Une erreur inconnue s’est produite lors du traitement des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="6d45d-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="6d45d-306">Une erreur précédente a arrêté le traitement des métadonnées.</span><span class="sxs-lookup"><span data-stu-id="6d45d-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="6d45d-307">Codes d’état des propriétés</span><span class="sxs-lookup"><span data-stu-id="6d45d-307">Properties status codes</span></span>  
<span data-ttu-id="6d45d-308">Le tableau suivant répertorie les codes d’état pour le traitement des propriétés d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="6d45d-309">Code d’état</span><span class="sxs-lookup"><span data-stu-id="6d45d-309">Status code</span></span>|<span data-ttu-id="6d45d-310">Description</span><span class="sxs-lookup"><span data-stu-id="6d45d-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="6d45d-311">Le traitement des propriétés s’est terminé sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="6d45d-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="6d45d-312">Le nom du fichier de propriétés n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="6d45d-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="6d45d-313">Le nom du fichier de propriétés est trop long.</span><span class="sxs-lookup"><span data-stu-id="6d45d-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="6d45d-314">Le fichier de propriétés est introuvable.</span><span class="sxs-lookup"><span data-stu-id="6d45d-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="6d45d-315">L’accès au fichier de propriétés est refusé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="6d45d-316">Le fichier de propriétés est endommagé (le contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="6d45d-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="6d45d-317">Le contenu des propriétés n’est pas conforme au format requis.</span><span class="sxs-lookup"><span data-stu-id="6d45d-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="6d45d-318">L’écriture des propriétés XML a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="6d45d-319">La demande de service Blob pour accéder aux propriétés a échoué.</span><span class="sxs-lookup"><span data-stu-id="6d45d-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="6d45d-320">Une erreur d’E/S du disque ou réseau s’est produite lors du traitement des propriétés.</span><span class="sxs-lookup"><span data-stu-id="6d45d-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="6d45d-321">Une erreur inconnue s’est produite lors du traitement des propriétés.</span><span class="sxs-lookup"><span data-stu-id="6d45d-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="6d45d-322">Une erreur précédente a arrêté le traitement des propriétés.</span><span class="sxs-lookup"><span data-stu-id="6d45d-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="6d45d-323">Exemples de journaux</span><span class="sxs-lookup"><span data-stu-id="6d45d-323">Sample logs</span></span>  
<span data-ttu-id="6d45d-324">Vous trouverez ci-dessous un exemple de journal détaillé.</span><span class="sxs-lookup"><span data-stu-id="6d45d-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="6d45d-325">Le journal d’erreurs correspondant est illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6d45d-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="6d45d-326">Le journal d’erreurs suivant pour un travail d’importation contient une erreur sur un fichier introuvable sur le lecteur d’importation.</span><span class="sxs-lookup"><span data-stu-id="6d45d-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="6d45d-327">Notez que l’état des composants suivants est `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="6d45d-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="6d45d-328">Le journal d’erreurs suivant pour un travail d’exportation indique que le contenu de l’objet blob a été correctement écrit sur le lecteur, mais qu’une erreur s’est produite lors de l’exportation des propriétés de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="6d45d-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="6d45d-329">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d45d-329">Next steps</span></span>
 
* [<span data-ttu-id="6d45d-330">API REST d’importation/exportation de stockage</span><span class="sxs-lookup"><span data-stu-id="6d45d-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
