---
title: format de fichier journal aaaAzure Import/Export | Documents Microsoft
description: "En savoir plus sur format hello de fichiers de journaux hello créé lors de l’exécution des étapes d’un travail de service d’importation/exportation."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="e23a0-103">Format de fichier journal du service Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="e23a0-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="e23a0-104">Lorsque hello service Microsoft Azure Import/Export exécute une action sur un lecteur dans le cadre d’un travail d’importation ou d’exportation, les journaux sont écrits tooblock BLOB hello compte de stockage associé à ce travail.</span><span class="sxs-lookup"><span data-stu-id="e23a0-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="e23a0-105">Il existe deux journaux pouvant être écrits par hello service d’importation/exportation :</span><span class="sxs-lookup"><span data-stu-id="e23a0-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="e23a0-106">journal des erreurs Hello est toujours générée dans le cas de hello d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e23a0-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="e23a0-107">Hello journal détaillé n’est pas activé par défaut, mais peut être activée en définissant les hello `EnableVerboseLog` propriété sur un [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) opération.</span><span class="sxs-lookup"><span data-stu-id="e23a0-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="e23a0-108">Emplacement du fichier journal</span><span class="sxs-lookup"><span data-stu-id="e23a0-108">Log file location</span></span>  
<span data-ttu-id="e23a0-109">Hello dans les journaux tooblock BLOB dans le conteneur de hello ou un répertoire virtuel spécifié par hello `ImportExportStatesPath` paramètre que vous pouvez définir sur une `Put Job` opération.</span><span class="sxs-lookup"><span data-stu-id="e23a0-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="e23a0-110">Hello emplacement toowhich hello dans les journaux dépend comment l’authentification est spécifiée pour la tâche hello, avec la valeur hello spécifiée pour `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="e23a0-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="e23a0-111">L’authentification pour le travail de hello peut être spécifiée via une clé de compte de stockage ou un conteneur de SAP (signature d’accès partagé).</span><span class="sxs-lookup"><span data-stu-id="e23a0-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="e23a0-112">nom de Hello du conteneur de hello ou un répertoire virtuel peut être le nom par défaut hello `waimportexport`, ou un autre conteneur ou nom de répertoire virtuel que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="e23a0-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="e23a0-113">tableau Hello ci-dessous montre les options possibles hello :</span><span class="sxs-lookup"><span data-stu-id="e23a0-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="e23a0-114">Méthode d'authentification</span><span class="sxs-lookup"><span data-stu-id="e23a0-114">Authentication Method</span></span>|<span data-ttu-id="e23a0-115">Valeur de l’élément `ImportExportStatesPath`</span><span class="sxs-lookup"><span data-stu-id="e23a0-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="e23a0-116">Emplacement des objets blob de journal</span><span class="sxs-lookup"><span data-stu-id="e23a0-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="e23a0-117">Clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e23a0-117">Storage account key</span></span>|<span data-ttu-id="e23a0-118">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="e23a0-118">Default value</span></span>|<span data-ttu-id="e23a0-119">Un conteneur nommé `waimportexport`, qui est le conteneur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="e23a0-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e23a0-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="e23a0-121">Clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e23a0-121">Storage account key</span></span>|<span data-ttu-id="e23a0-122">Valeur spécifiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e23a0-122">User-specified value</span></span>|<span data-ttu-id="e23a0-123">Un conteneur nommé par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-123">A container named by hello user.</span></span> <span data-ttu-id="e23a0-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e23a0-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="e23a0-125">SAP de conteneur</span><span class="sxs-lookup"><span data-stu-id="e23a0-125">Container SAS</span></span>|<span data-ttu-id="e23a0-126">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="e23a0-126">Default value</span></span>|<span data-ttu-id="e23a0-127">Un répertoire virtuel nommé `waimportexport`, qui est le nom par défaut de hello, sous le conteneur hello spécifié dans hello SAS.</span><span class="sxs-lookup"><span data-stu-id="e23a0-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="e23a0-128">Par exemple, si hello SAS spécifié pour le travail de hello est `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, puis de l’emplacement du journal hello serait`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="e23a0-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="e23a0-129">SAP de conteneur</span><span class="sxs-lookup"><span data-stu-id="e23a0-129">Container SAS</span></span>|<span data-ttu-id="e23a0-130">Valeur spécifiée par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e23a0-130">User-specified value</span></span>|<span data-ttu-id="e23a0-131">Un répertoire virtuel nommé par l’utilisateur hello, sous le conteneur hello spécifié dans hello SAS.</span><span class="sxs-lookup"><span data-stu-id="e23a0-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="e23a0-132">Par exemple, si hello SAS spécifié pour le travail de hello est `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, et hello spécifié le répertoire virtuel est appelé `mylogblobs`, puis de l’emplacement du journal hello serait `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="e23a0-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="e23a0-133">Vous pouvez récupérer des URL hello pour erreur de hello et les journaux détaillés en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération.</span><span class="sxs-lookup"><span data-stu-id="e23a0-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="e23a0-134">Hello journaux sont disponibles une fois le traitement du lecteur de hello est terminé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="e23a0-135">Format de fichier journal</span><span class="sxs-lookup"><span data-stu-id="e23a0-135">Log file format</span></span>  
<span data-ttu-id="e23a0-136">Hello format pour les journaux est hello même : un objet blob contenant des descriptions XML des événements hello qui s’est produite lors de la copie des objets BLOB entre le disque dur de hello et hello du compte client.</span><span class="sxs-lookup"><span data-stu-id="e23a0-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="e23a0-137">la journalisation documentée Hello contient des informations complètes sur l’état de hello d’opération de copie hello pour chaque objet blob (pour un travail d’importation) ou un fichier (pour un travail d’exportation), tandis que le journal des erreurs hello contient uniquement les informations de hello pour les objets BLOB ou des fichiers qui ont rencontré des erreurs pendant hello importer ou exporter des travaux.</span><span class="sxs-lookup"><span data-stu-id="e23a0-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="e23a0-138">format de journal détaillé Hello est indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e23a0-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="e23a0-139">journal des erreurs Hello a hello même structure, mais filtre les opérations réussies.</span><span class="sxs-lookup"><span data-stu-id="e23a0-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="e23a0-140">Hello tableau suivant décrit les éléments hello du fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="e23a0-141">Élément XML</span><span class="sxs-lookup"><span data-stu-id="e23a0-141">XML Element</span></span>|<span data-ttu-id="e23a0-142">Type</span><span class="sxs-lookup"><span data-stu-id="e23a0-142">Type</span></span>|<span data-ttu-id="e23a0-143">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="e23a0-144">Élément XML</span><span class="sxs-lookup"><span data-stu-id="e23a0-144">XML Element</span></span>|<span data-ttu-id="e23a0-145">Représente un journal de lecteur.</span><span class="sxs-lookup"><span data-stu-id="e23a0-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="e23a0-146">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-146">Attribute, String</span></span>|<span data-ttu-id="e23a0-147">version de Hello du format de journal hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="e23a0-148">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-148">String</span></span>|<span data-ttu-id="e23a0-149">Bonjour numéro de série du matériel du lecteur.</span><span class="sxs-lookup"><span data-stu-id="e23a0-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="e23a0-150">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-150">String</span></span>|<span data-ttu-id="e23a0-151">État de traitement du lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-151">Status of hello drive processing.</span></span> <span data-ttu-id="e23a0-152">Consultez hello `Drive Status Codes` tableau ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e23a0-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="e23a0-153">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="e23a0-153">Nested XML element</span></span>|<span data-ttu-id="e23a0-154">Représente un objet blob.</span><span class="sxs-lookup"><span data-stu-id="e23a0-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="e23a0-155">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-155">String</span></span>|<span data-ttu-id="e23a0-156">Hello URI d’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="e23a0-157">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-157">String</span></span>|<span data-ttu-id="e23a0-158">fichier de toohello Hello chemin d’accès relatif sur le lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="e23a0-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="e23a0-159">DateTime</span></span>|<span data-ttu-id="e23a0-160">version d’instantané Hello d’objet blob hello pour un travail d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="e23a0-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="e23a0-161">Entier </span><span class="sxs-lookup"><span data-stu-id="e23a0-161">Integer</span></span>|<span data-ttu-id="e23a0-162">longueur totale de Hello du blob hello en octets.</span><span class="sxs-lookup"><span data-stu-id="e23a0-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="e23a0-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="e23a0-163">DateTime</span></span>|<span data-ttu-id="e23a0-164">Hello date/heure dernière modification de cet objet blob hello pour un travail d’exportation uniquement.</span><span class="sxs-lookup"><span data-stu-id="e23a0-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="e23a0-165">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-165">String</span></span>|<span data-ttu-id="e23a0-166">disposition d’objet blob hello pour un travail d’importation d’importation Hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="e23a0-167">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-167">Attribute, String</span></span>|<span data-ttu-id="e23a0-168">état Hello Hello disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="e23a0-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="e23a0-169">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="e23a0-169">Nested XML element</span></span>|<span data-ttu-id="e23a0-170">Représente une liste de plages de pages pour un objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="e23a0-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="e23a0-171">Élément XML</span><span class="sxs-lookup"><span data-stu-id="e23a0-171">XML element</span></span>|<span data-ttu-id="e23a0-172">Représente une plage de pages.</span><span class="sxs-lookup"><span data-stu-id="e23a0-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="e23a0-173">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="e23a0-173">Attribute, Integer</span></span>|<span data-ttu-id="e23a0-174">Décalage de début de plage de pages hello dans l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="e23a0-175">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="e23a0-175">Attribute, Integer</span></span>|<span data-ttu-id="e23a0-176">Longueur en octets de la plage de pages hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="e23a0-177">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-177">Attribute, String</span></span>|<span data-ttu-id="e23a0-178">Hachage de MD5 encodé en Base16 hello de plage de pages.</span><span class="sxs-lookup"><span data-stu-id="e23a0-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="e23a0-179">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-179">Attribute, String</span></span>|<span data-ttu-id="e23a0-180">État de traitement de plage de pages hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="e23a0-181">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="e23a0-181">Nested XML element</span></span>|<span data-ttu-id="e23a0-182">Représente une liste de blocs pour un objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="e23a0-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="e23a0-183">Élément XML</span><span class="sxs-lookup"><span data-stu-id="e23a0-183">XML element</span></span>|<span data-ttu-id="e23a0-184">Représente un bloc.</span><span class="sxs-lookup"><span data-stu-id="e23a0-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="e23a0-185">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="e23a0-185">Attribute, Integer</span></span>|<span data-ttu-id="e23a0-186">Décalage de départ du bloc hello dans l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="e23a0-187">Attribut, Entier</span><span class="sxs-lookup"><span data-stu-id="e23a0-187">Attribute, Integer</span></span>|<span data-ttu-id="e23a0-188">Longueur en octets du bloc de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="e23a0-189">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-189">Attribute, String</span></span>|<span data-ttu-id="e23a0-190">ID de bloc de Hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="e23a0-191">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-191">Attribute, String</span></span>|<span data-ttu-id="e23a0-192">Hachage de MD5 encodé en Base16 du bloc de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="e23a0-193">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-193">Attribute, String</span></span>|<span data-ttu-id="e23a0-194">État de traitement hello bloc.</span><span class="sxs-lookup"><span data-stu-id="e23a0-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="e23a0-195">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="e23a0-195">Nested XML element</span></span>|<span data-ttu-id="e23a0-196">Représente les métadonnées de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="e23a0-197">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-197">Attribute, String</span></span>|<span data-ttu-id="e23a0-198">État de traitement des métadonnées d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="e23a0-199">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-199">String</span></span>|<span data-ttu-id="e23a0-200">Fichier de métadonnées global toohello chemin d’accès relatif.</span><span class="sxs-lookup"><span data-stu-id="e23a0-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="e23a0-201">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-201">Attribute, String</span></span>|<span data-ttu-id="e23a0-202">Encodé en Base16 hachage MD5 du fichier de métadonnées globales hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="e23a0-203">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-203">String</span></span>|<span data-ttu-id="e23a0-204">Fichier de métadonnées de toohello de chemin d’accès relatif.</span><span class="sxs-lookup"><span data-stu-id="e23a0-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="e23a0-205">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-205">Attribute, String</span></span>|<span data-ttu-id="e23a0-206">Hachage de MD5 encodé en Base16 du fichier de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="e23a0-207">Élément XML imbriqué</span><span class="sxs-lookup"><span data-stu-id="e23a0-207">Nested XML element</span></span>|<span data-ttu-id="e23a0-208">Représente les propriétés d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="e23a0-209">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-209">Attribute, String</span></span>|<span data-ttu-id="e23a0-210">État de traitement des propriétés d’objet blob hello, par exemple, fichier introuvable, s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="e23a0-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="e23a0-211">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-211">String</span></span>|<span data-ttu-id="e23a0-212">Fichier de propriétés globales de toohello de chemin d’accès relatif.</span><span class="sxs-lookup"><span data-stu-id="e23a0-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="e23a0-213">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-213">Attribute, String</span></span>|<span data-ttu-id="e23a0-214">Hachage de MD5 encodé en Base16 du fichier de propriétés globales hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="e23a0-215">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-215">String</span></span>|<span data-ttu-id="e23a0-216">Fichier de propriétés de toohello de chemin d’accès relatif.</span><span class="sxs-lookup"><span data-stu-id="e23a0-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="e23a0-217">Attribut, Chaîne</span><span class="sxs-lookup"><span data-stu-id="e23a0-217">Attribute, String</span></span>|<span data-ttu-id="e23a0-218">Hachage de MD5 encodé en Base16 du fichier de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="e23a0-219">String</span><span class="sxs-lookup"><span data-stu-id="e23a0-219">String</span></span>|<span data-ttu-id="e23a0-220">État de traitement des objets blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="e23a0-221">Codes d’état du lecteur</span><span class="sxs-lookup"><span data-stu-id="e23a0-221">Drive status codes</span></span>  
<span data-ttu-id="e23a0-222">Hello tableau suivant répertorie les codes d’état hello pour le traitement d’un lecteur.</span><span class="sxs-lookup"><span data-stu-id="e23a0-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="e23a0-223">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e23a0-223">Status code</span></span>|<span data-ttu-id="e23a0-224">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e23a0-225">lecteur de Hello a terminé le traitement sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="e23a0-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="e23a0-226">lecteur de Hello a terminé le traitement des avertissements dans un ou plusieurs des objets BLOB par dispositions d’importation hello spécifiées pour les objets BLOB de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="e23a0-227">lecteur de Hello a terminé avec des erreurs dans un ou plusieurs objets BLOB ou segments.</span><span class="sxs-lookup"><span data-stu-id="e23a0-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="e23a0-228">Aucun disque ne se trouve sur le lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="e23a0-229">Hello premier volume de données sur disque de hello n’est pas au format NTFS.</span><span class="sxs-lookup"><span data-stu-id="e23a0-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="e23a0-230">Une erreur inconnue s’est produite lors de l’exécution d’opérations sur le lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="e23a0-231">Aucun volume BitLocker chiffrable n’a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="e23a0-232">BitLocker n’est pas activé sur le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="e23a0-233">protecteur de clé de mot de passe numérique Hello n’existe pas sur le volume de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="e23a0-234">mot de passe numérique Hello fourni ne peut pas déverrouiller hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="e23a0-235">Erreur inconnue s’est produite lors de la tentative de volume de hello toounlock.</span><span class="sxs-lookup"><span data-stu-id="e23a0-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="e23a0-236">Une erreur inconnue s’est produite lors de l’exécution d’opérations BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e23a0-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="e23a0-237">nom du fichier manifeste Hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="e23a0-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="e23a0-238">nom du fichier manifeste Hello est trop long.</span><span class="sxs-lookup"><span data-stu-id="e23a0-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="e23a0-239">fichier de manifeste Hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="e23a0-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="e23a0-240">Fichier de manifeste toohello accès est refusé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="e23a0-241">Hello fichier manifeste est endommagé (hello contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="e23a0-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="e23a0-242">contenu du manifeste Hello ne respecte pas le format requis de toohello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="e23a0-243">lecteur Hello ID dans le fichier de manifeste hello ne correspond pas hello une lecture à partir du lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="e23a0-244">Un erreur d’e/s disque s’est produite lors de la lecture du manifeste de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="e23a0-245">Hello exportation blob liste d’objets blob ne respecte pas le format requis de toohello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="e23a0-246">Accéder aux objets BLOB de toohello dans le compte de stockage hello est interdite.</span><span class="sxs-lookup"><span data-stu-id="e23a0-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="e23a0-247">Cela est peut-être en raison de la clé de compte de stockage tooinvalid ou SAP de conteneur.</span><span class="sxs-lookup"><span data-stu-id="e23a0-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="e23a0-248">Et une erreur interne s’est produite lors du traitement du lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="e23a0-249">Codes d’état de l’objet blob</span><span class="sxs-lookup"><span data-stu-id="e23a0-249">Blob status codes</span></span>  
<span data-ttu-id="e23a0-250">Hello tableau suivant répertorie les codes d’état hello pour le traitement d’un objet blob.</span><span class="sxs-lookup"><span data-stu-id="e23a0-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="e23a0-251">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e23a0-251">Status code</span></span>|<span data-ttu-id="e23a0-252">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e23a0-253">objet blob de Hello a terminé le traitement sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="e23a0-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="e23a0-254">objet blob de Hello a terminé le traitement avec des erreurs dans une ou plusieurs plages de pages ou blocs, métadonnées ou propriétés.</span><span class="sxs-lookup"><span data-stu-id="e23a0-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="e23a0-255">nom de fichier Hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="e23a0-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="e23a0-256">nom de fichier Hello est trop long.</span><span class="sxs-lookup"><span data-stu-id="e23a0-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="e23a0-257">fichier de Hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="e23a0-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="e23a0-258">Fichier de toohello d’accès est refusé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e23a0-259">demande de service Blob Hello tooaccess hello blob a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="e23a0-260">demande de service Blob Hello tooaccess hello blob est interdite.</span><span class="sxs-lookup"><span data-stu-id="e23a0-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="e23a0-261">Cela est peut-être en raison de la clé de compte de stockage tooinvalid ou SAP de conteneur.</span><span class="sxs-lookup"><span data-stu-id="e23a0-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="e23a0-262">Échec de l’objet blob de hello toorename (pour un travail d’importation) ou un fichier hello (pour un travail d’exportation).</span><span class="sxs-lookup"><span data-stu-id="e23a0-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="e23a0-263">Une modification inattendue s’est produite avec l’objet blob de hello (pour un travail d’exportation).</span><span class="sxs-lookup"><span data-stu-id="e23a0-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="e23a0-264">Il existe un bail présent sur l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="e23a0-265">Un disque ou une erreur d’e/s de réseau s’est produite lors du traitement d’objets blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="e23a0-266">Une erreur inconnue s’est produite lors du traitement d’objets blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="e23a0-267">Codes d’état de disposition d’importation</span><span class="sxs-lookup"><span data-stu-id="e23a0-267">Import disposition status codes</span></span>  
<span data-ttu-id="e23a0-268">Hello tableau suivant répertorie les codes d’état hello pour résoudre une disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="e23a0-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="e23a0-269">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e23a0-269">Status code</span></span>|<span data-ttu-id="e23a0-270">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="e23a0-271">objet blob de Hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="e23a0-272">objet blob de Hello a été renommé par disposition d’importation de changement de nom.</span><span class="sxs-lookup"><span data-stu-id="e23a0-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="e23a0-273">Hello `Blob/BlobPath` élément contient hello URI pour l’objet blob de hello renommé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="e23a0-274">objet blob de Hello a été ignoré par `no-overwrite` disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="e23a0-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="e23a0-275">objet blob de Hello a remplacé un objet blob existant par `overwrite` disposition d’importation.</span><span class="sxs-lookup"><span data-stu-id="e23a0-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="e23a0-276">Une erreur précédente a arrêté le traitement de disposition d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="e23a0-277">Codes d’état de plage de pages/de bloc</span><span class="sxs-lookup"><span data-stu-id="e23a0-277">Page range/block status codes</span></span>  
<span data-ttu-id="e23a0-278">Hello tableau suivant répertorie les codes d’état hello pour le traitement d’une plage de pages ou un bloc.</span><span class="sxs-lookup"><span data-stu-id="e23a0-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="e23a0-279">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e23a0-279">Status code</span></span>|<span data-ttu-id="e23a0-280">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e23a0-281">plage de pages Hello ou un bloc a terminé le traitement sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="e23a0-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="e23a0-282">Hello bloc a été validé, mais pas dans hello liste complète de blocs, car les autres blocs ont a échoué, ou placez la liste complète de blocs a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="e23a0-283">bloc de Hello est téléchargé mais non validée.</span><span class="sxs-lookup"><span data-stu-id="e23a0-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="e23a0-284">plage de pages Hello ou un bloc est endommagé (hello contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="e23a0-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="e23a0-285">Une fin de fichier inattendue a été rencontrée.</span><span class="sxs-lookup"><span data-stu-id="e23a0-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="e23a0-286">Une fin d’objet blob inattendue a été rencontrée.</span><span class="sxs-lookup"><span data-stu-id="e23a0-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e23a0-287">Hello tooaccess hello plage de pages de la demande du service Blob ou bloc a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="e23a0-288">Un disque ou une erreur d’e/s de réseau s’est produite lors du traitement de la plage de pages hello ou un bloc.</span><span class="sxs-lookup"><span data-stu-id="e23a0-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="e23a0-289">Une erreur inconnue s’est produite lors du traitement de la plage de pages hello ou un bloc.</span><span class="sxs-lookup"><span data-stu-id="e23a0-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="e23a0-290">Une erreur précédente a arrêté le traitement de la plage de pages hello ou un bloc.</span><span class="sxs-lookup"><span data-stu-id="e23a0-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="e23a0-291">Codes d’état des métadonnées</span><span class="sxs-lookup"><span data-stu-id="e23a0-291">Metadata status codes</span></span>  
<span data-ttu-id="e23a0-292">Hello tableau suivant répertorie les codes d’état hello pour le traitement des métadonnées d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e23a0-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="e23a0-293">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e23a0-293">Status code</span></span>|<span data-ttu-id="e23a0-294">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e23a0-295">les métadonnées Hello a terminé le traitement sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="e23a0-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="e23a0-296">nom de fichier de métadonnées Hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="e23a0-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="e23a0-297">nom de fichier de métadonnées Hello est trop long.</span><span class="sxs-lookup"><span data-stu-id="e23a0-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="e23a0-298">fichier de métadonnées Hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="e23a0-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="e23a0-299">Fichier de métadonnées toohello accès est refusé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="e23a0-300">fichier de métadonnées Hello est endommagé (hello contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="e23a0-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="e23a0-301">contenu de métadonnées Hello ne respecte pas le format requis de toohello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="e23a0-302">Lors de l’écriture hello que XML a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e23a0-303">demande de service Blob Hello tooaccess hello métadonnées a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="e23a0-304">Une erreur d’e/s disque ou réseau s’est produite lors du traitement des métadonnées de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="e23a0-305">Une erreur inconnue s’est produite lors du traitement des métadonnées de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="e23a0-306">Une erreur précédente a arrêté le traitement des métadonnées de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="e23a0-307">Codes d’état des propriétés</span><span class="sxs-lookup"><span data-stu-id="e23a0-307">Properties status codes</span></span>  
<span data-ttu-id="e23a0-308">Hello tableau suivant répertorie les codes d’état hello pour le traitement des propriétés d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="e23a0-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="e23a0-309">Code d’état</span><span class="sxs-lookup"><span data-stu-id="e23a0-309">Status code</span></span>|<span data-ttu-id="e23a0-310">Description</span><span class="sxs-lookup"><span data-stu-id="e23a0-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="e23a0-311">les propriétés de Hello ont terminé le traitement sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="e23a0-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="e23a0-312">nom de fichier de propriétés Hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="e23a0-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="e23a0-313">nom de fichier de propriétés Hello est trop long.</span><span class="sxs-lookup"><span data-stu-id="e23a0-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="e23a0-314">fichier de propriétés Hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="e23a0-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="e23a0-315">Fichier de propriétés toohello accès est refusé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="e23a0-316">fichier de propriétés Hello est endommagé (hello contenu ne correspond pas à son hachage).</span><span class="sxs-lookup"><span data-stu-id="e23a0-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="e23a0-317">contenu des propriétés Hello ne respecte pas le format requis de toohello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="e23a0-318">L’écriture de propriétés hello que XML a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="e23a0-319">demande de service Blob Hello tooaccess hello propriétés a échoué.</span><span class="sxs-lookup"><span data-stu-id="e23a0-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="e23a0-320">Une erreur d’e/s disque ou réseau s’est produite lors du traitement des propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="e23a0-321">Une erreur inconnue s’est produite lors du traitement des propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="e23a0-322">Une erreur précédente a arrêté le traitement des propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="e23a0-323">Exemples de journaux</span><span class="sxs-lookup"><span data-stu-id="e23a0-323">Sample logs</span></span>  
<span data-ttu-id="e23a0-324">Hello Voici un exemple de journal détaillé.</span><span class="sxs-lookup"><span data-stu-id="e23a0-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="e23a0-325">journal des erreurs Hello correspondant est indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e23a0-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="e23a0-326">journal des erreurs Hello pour un travail d’importation contient une erreur sur un fichier introuvable sur le lecteur d’importation hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="e23a0-327">Notez qu’état hello des composants suivants est `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="e23a0-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="e23a0-328">Hello journal des erreurs pour un travail d’exportation indique que le contenu blob hello a été correctement écrit toohello lecteur, mais qu’une erreur s’est produite lors de l’exportation des propriétés de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="e23a0-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="e23a0-329">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e23a0-329">Next steps</span></span>
 
* [<span data-ttu-id="e23a0-330">API REST d’importation/exportation de stockage</span><span class="sxs-lookup"><span data-stu-id="e23a0-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
