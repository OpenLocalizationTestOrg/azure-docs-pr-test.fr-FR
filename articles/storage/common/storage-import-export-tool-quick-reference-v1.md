---
title: "Aide-mémoire sur les commandes de travail d’importation pour l’outil Azure Import/Export - v1 | Microsoft Docs"
description: "Référence de l’outil Azure Import/Export pour les commandes de travail d’importation fréquemment utilisées. Cela s’applique à la version v1 de l’outil d’importation/exportation."
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 370cf6fae7ae106e8341f65086c8b8187d335746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="36b47-104">Aide-mémoire sur les commandes fréquemment utilisées pour les travaux d’importation</span><span class="sxs-lookup"><span data-stu-id="36b47-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="36b47-105">Cette section fournit un aide-mémoire pour certaines commandes fréquemment utilisées.</span><span class="sxs-lookup"><span data-stu-id="36b47-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="36b47-106">Pour une utilisation détaillée, consultez [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="36b47-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-to-the-hard-drive"></a><span data-ttu-id="36b47-107">Préparer un disque dur quand des données y ont déjà été copiées</span><span class="sxs-lookup"><span data-stu-id="36b47-107">Prepare a hard drive when data has already been copied to the hard drive</span></span>
 <span data-ttu-id="36b47-108">La commande suivante prépare un disque dur sur lequel des données ont déjà été copiées, mais pas encore chiffrées avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="36b47-108">The following command prepares a hard drive when data has already been copied to it, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="36b47-109">Copier un répertoire unique sur un disque dur</span><span class="sxs-lookup"><span data-stu-id="36b47-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="36b47-110">La commande suivante copie un répertoire source unique sur un disque dur qui n’a pas encore été chiffré avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="36b47-110">The following command copies a single source directory to a hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-to-a-hard-drive"></a><span data-ttu-id="36b47-111">Copier deux répertoires sur un disque dur</span><span class="sxs-lookup"><span data-stu-id="36b47-111">Copy two directories to a hard drive</span></span>  
 <span data-ttu-id="36b47-112">Pour copier deux répertoires sources sur un disque, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="36b47-112">To copy two source directories to a drive, use the following commands:</span></span>  
  
 <span data-ttu-id="36b47-113">La première commande spécifie le répertoire des journaux, la clé du compte de stockage, la lettre du lecteur cible, la configuration requise `format/encrypt` et des paramètres courants :</span><span class="sxs-lookup"><span data-stu-id="36b47-113">The first command specifies the log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="36b47-114">La deuxième commande spécifie le fichier journal, un nouvel ID de session, ainsi que les emplacements source et de destination :</span><span class="sxs-lookup"><span data-stu-id="36b47-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="36b47-115">Copier un fichier volumineux sur un disque dur dans une deuxième session de copie</span><span class="sxs-lookup"><span data-stu-id="36b47-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="36b47-116">La commande suivante copie un seul fichier volumineux sur un disque dur qui a été préparé au cours d’une session de copie précédente :</span><span class="sxs-lookup"><span data-stu-id="36b47-116">The following command copies a single large file to a hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="36b47-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36b47-117">Next steps</span></span>

* [<span data-ttu-id="36b47-118">Exemple de workflow pour préparer des disques durs à un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="36b47-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
