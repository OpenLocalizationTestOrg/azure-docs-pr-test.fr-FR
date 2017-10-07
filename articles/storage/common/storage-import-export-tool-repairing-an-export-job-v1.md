---
title: "aaaRepairing un travail d’exportation Azure Import/Export - v1 | Documents Microsoft"
description: "Découvrez comment un travail d’exportation qui a été créé et exécuté à l’aide de toorepair hello Azure Import/Export service."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="e4273-103">Réparation d’un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="e4273-103">Repairing an export job</span></span>
<span data-ttu-id="e4273-104">Lorsqu’un travail d’exportation est terminé, vous pouvez exécuter hello outil de Microsoft Azure Import/Export localement pour :</span><span class="sxs-lookup"><span data-stu-id="e4273-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="e4273-105">Le téléchargement de fichiers que le service d’importation/exportation Azure hello a tooexport impossible.</span><span class="sxs-lookup"><span data-stu-id="e4273-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="e4273-106">Valider que les fichiers sur le lecteur de hello hello ont été correctement exportés.</span><span class="sxs-lookup"><span data-stu-id="e4273-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="e4273-107">Cette fonctionnalité, vous devez avoir toouse de stockage tooAzure de connectivité.</span><span class="sxs-lookup"><span data-stu-id="e4273-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="e4273-108">commande Hello pour réparer un travail d’importation est **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="e4273-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="e4273-109">Paramètres de RepairExport</span><span class="sxs-lookup"><span data-stu-id="e4273-109">RepairExport parameters</span></span>

<span data-ttu-id="e4273-110">Hello paramètres suivants peuvent être spécifiés avec **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="e4273-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="e4273-111">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e4273-111">Parameter</span></span>|<span data-ttu-id="e4273-112">Description</span><span class="sxs-lookup"><span data-stu-id="e4273-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="e4273-113">**/r:&lt;RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="e4273-114">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e4273-114">Required.</span></span> <span data-ttu-id="e4273-115">Chemin d’accès toohello fichier de réparation qui suit la progression de la réparation de hello hello et vous permet de tooresume une réparation interrompue.</span><span class="sxs-lookup"><span data-stu-id="e4273-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="e4273-116">Chaque disque ne doit avoir qu’un fichier de réparation.</span><span class="sxs-lookup"><span data-stu-id="e4273-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="e4273-117">Lorsque vous démarrez une réparation pour un lecteur donné, vous passez hello chemin d’accès tooa réparer un fichier qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="e4273-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="e4273-118">tooresume une réparation interrompue, vous devez passer dans le nom d’un fichier existant de la réparation de hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="e4273-119">lecteur cible correspondant toohello d’Hello réparation fichier doit toujours être spécifié.</span><span class="sxs-lookup"><span data-stu-id="e4273-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="e4273-120">**/logdir:&lt;LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="e4273-121">facultatif.</span><span class="sxs-lookup"><span data-stu-id="e4273-121">Optional.</span></span> <span data-ttu-id="e4273-122">répertoire de journal Hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-122">hello log directory.</span></span> <span data-ttu-id="e4273-123">Les fichiers journaux détaillés seront écrit toothis active.</span><span class="sxs-lookup"><span data-stu-id="e4273-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="e4273-124">Si aucun répertoire de journal est spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="e4273-125">**/d:&lt;TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="e4273-126">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e4273-126">Required.</span></span> <span data-ttu-id="e4273-127">Hello Active toovalidate et la réparation.</span><span class="sxs-lookup"><span data-stu-id="e4273-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="e4273-128">Cela est généralement hello répertoire racine du lecteur d’exportation hello, mais peut également être un partage de fichiers réseau qui contient une copie des fichiers de hello exportée.</span><span class="sxs-lookup"><span data-stu-id="e4273-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="e4273-129">**/bk:&lt;BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="e4273-130">facultatif.</span><span class="sxs-lookup"><span data-stu-id="e4273-130">Optional.</span></span> <span data-ttu-id="e4273-131">Vous devez spécifier la clé de BitLocker hello si vous souhaitez toounlock d’outil hello chiffré hello où les fichiers exportés sont stockés.</span><span class="sxs-lookup"><span data-stu-id="e4273-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="e4273-132">**/sn:&lt;StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="e4273-133">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e4273-133">Required.</span></span> <span data-ttu-id="e4273-134">tâche d’exportation de nom Hello hello du compte de stockage pour hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="e4273-135">**/sk:&lt;StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="e4273-136">**Obligatoire** si et seulement si une SAP de conteneur n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e4273-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="e4273-137">tâche d’exportation de clé de compte Hello hello compte de stockage pour hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="e4273-138">**/csas:&lt;ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="e4273-139">**Requis** si et seulement si la clé de compte de stockage hello n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e4273-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="e4273-140">Hello SAP de conteneur pour accéder aux objets BLOB de hello associé au travail d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="e4273-141">**/CopyLogFile:&lt;DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="e4273-142">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e4273-142">Required.</span></span> <span data-ttu-id="e4273-143">Hello chemin d’accès toohello lecteur fichier journal de copie.</span><span class="sxs-lookup"><span data-stu-id="e4273-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="e4273-144">fichier de Hello est généré par hello service Windows Azure Import/Export et peut être téléchargé à partir du stockage d’objets blob hello associé hello travail.</span><span class="sxs-lookup"><span data-stu-id="e4273-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="e4273-145">fichier journal de copie Hello contient des informations sur les objets BLOB en échec ou les fichiers qui sont toobe réparé.</span><span class="sxs-lookup"><span data-stu-id="e4273-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="e4273-146">**/ManifestFile:&lt;DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="e4273-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="e4273-147">facultatif.</span><span class="sxs-lookup"><span data-stu-id="e4273-147">Optional.</span></span> <span data-ttu-id="e4273-148">fichier manifeste de lecteur exportation Hello chemin d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="e4273-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="e4273-149">Ce fichier est généré par le service de Windows Azure Import/Export hello et stocké sur le lecteur d’exportation hello et, éventuellement dans un objet blob dans le compte de stockage hello associé hello travail.</span><span class="sxs-lookup"><span data-stu-id="e4273-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="e4273-150">Hello contenu des fichiers hello sur le lecteur d’exportation hello sera vérifié avec hello les hachages MD5 contenus dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e4273-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="e4273-151">Les fichiers qui sont déterminé toobe endommagé seront téléchargés et réécrits toohello cible répertoires.</span><span class="sxs-lookup"><span data-stu-id="e4273-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="e4273-152">Utilisation de RepairExport mode toocorrect les échecs d’exportation</span><span class="sxs-lookup"><span data-stu-id="e4273-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="e4273-153">Vous pouvez utiliser les fichiers toodownload hello outil d’importation/exportation Azure qui a échoué tooexport.</span><span class="sxs-lookup"><span data-stu-id="e4273-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="e4273-154">fichier journal de copie Hello contient une liste de fichiers qui ont échoué tooexport.</span><span class="sxs-lookup"><span data-stu-id="e4273-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="e4273-155">Hello causes des échecs d’exportation hello suivant les possibilités suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4273-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="e4273-156">Lecteurs endommagés</span><span class="sxs-lookup"><span data-stu-id="e4273-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="e4273-157">clé de compte de stockage Hello modifiée pendant le processus de transfert hello</span><span class="sxs-lookup"><span data-stu-id="e4273-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="e4273-158">outil de hello toorun dans **RepairExport** mode, vous devez tout d’abord lecteur de hello tooconnect contenant l’ordinateur de tooyour hello fichiers exportés.</span><span class="sxs-lookup"><span data-stu-id="e4273-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="e4273-159">Ensuite, exécutez hello outil d’importation/exportation Azure, spécifiant hello chemin toothat lecteur avec hello `/d` paramètre.</span><span class="sxs-lookup"><span data-stu-id="e4273-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="e4273-160">Vous devez également le fichier journal de copie du lecteur toohello toospecify hello chemin d’accès que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="e4273-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="e4273-161">Hello exemple de ligne de commande suivante exécute hello outil toorepair tous les fichiers qui ont échoué tooexport :</span><span class="sxs-lookup"><span data-stu-id="e4273-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="e4273-162">Hello Voici un exemple d’un fichier journal de copie qui montre un bloc dans hello blob échoué tooexport :</span><span class="sxs-lookup"><span data-stu-id="e4273-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="e4273-163">fichier journal de copie Hello indique qu’une défaillance s’est produite pendant que hello service Windows Azure Import/Export téléchargeait un du fichier de toohello de l’objet blob de hello blocs sur le lecteur d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="e4273-164">Hello d’autres composants du fichier de hello téléchargé avec succès et longueur du fichier hello a été correctement définie.</span><span class="sxs-lookup"><span data-stu-id="e4273-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="e4273-165">Dans ce cas, outil de hello sera ouvrir le fichier hello sur le lecteur de hello, téléchargez le bloc de hello hello compte de stockage et écrire toohello plage de fichiers à partir de décalage 65536 avec la longueur 65536.</span><span class="sxs-lookup"><span data-stu-id="e4273-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="e4273-166">À l’aide du contenu du lecteur RepairExport toovalidate</span><span class="sxs-lookup"><span data-stu-id="e4273-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="e4273-167">Vous pouvez également utiliser Azure Import/Export avec hello **RepairExport** option toovalidate hello contenu sur le lecteur de hello est correct.</span><span class="sxs-lookup"><span data-stu-id="e4273-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="e4273-168">fichier de manifeste Hello sur chaque lecteur d’exportation contient MD5s pour contenu hello du lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="e4273-169">Hello service Azure Import/Export peut également enregistrer les fichiers manifeste hello compte de stockage tooa pendant le processus d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="e4273-170">Hello emplacement des fichiers de manifeste hello est disponible via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération lorsque hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="e4273-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="e4273-171">Consultez [service d’importation/exportation Format de fichier manifeste](storage-import-export-file-format-metadata-and-properties.md) pour plus d’informations sur le format de hello d’un fichier de manifeste de lecteur.</span><span class="sxs-lookup"><span data-stu-id="e4273-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="e4273-172">Hello suivant montre comment toorun hello outil d’importation/exportation Azure avec hello **MANIFESTFILE** et **/CopyLogFile** paramètres :</span><span class="sxs-lookup"><span data-stu-id="e4273-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="e4273-173">Hello Voici un exemple d’un fichier manifeste :</span><span class="sxs-lookup"><span data-stu-id="e4273-173">hello following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="e4273-174">Après le processus de réparation en terminant hello, outil de hello parcourt chaque fichier référencé dans le fichier de manifeste hello et vérifier l’intégrité du fichier hello d’avec des hachages de hello MD5.</span><span class="sxs-lookup"><span data-stu-id="e4273-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="e4273-175">Pour le manifeste hello ci-dessus, il parcourt hello suivant des composants.</span><span class="sxs-lookup"><span data-stu-id="e4273-175">For hello manifest above, it will go through hello following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="e4273-176">N’importe quel composant échecs hello sera téléchargé par hello outil et réécrit toohello même fichier sur le lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="e4273-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="e4273-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e4273-177">Next steps</span></span>
 
* [<span data-ttu-id="e4273-178">Configuration des hello, outil d’importation/exportation Azure</span><span class="sxs-lookup"><span data-stu-id="e4273-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="e4273-179">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="e4273-179">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="e4273-180">Consultation de l’état du travail avec les fichiers journaux de copie</span><span class="sxs-lookup"><span data-stu-id="e4273-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="e4273-181">Réparation d’un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="e4273-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="e4273-182">Résolution des problèmes de hello outil d’importation/exportation Azure</span><span class="sxs-lookup"><span data-stu-id="e4273-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
