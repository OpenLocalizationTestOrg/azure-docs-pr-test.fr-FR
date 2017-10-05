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
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="a585a-104">Aide-mémoire sur les commandes fréquemment utilisées pour les travaux d’importation</span><span class="sxs-lookup"><span data-stu-id="a585a-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="a585a-105">Cette section fournit des références rapides pour certaines commandes fréquemment utilisées.</span><span class="sxs-lookup"><span data-stu-id="a585a-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="a585a-106">Pour une utilisation détaillée, consultez [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="a585a-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="a585a-107">Préparer les disques lorsque des données sont déjà copiées sur les disques</span><span class="sxs-lookup"><span data-stu-id="a585a-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="a585a-108">Voici un exemple de commande pour préparer un disque quand les données déjà copiées sur le disque dur n’ont pas encore été chiffrées avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="a585a-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="a585a-109">Copier un répertoire unique sur un disque dur</span><span class="sxs-lookup"><span data-stu-id="a585a-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="a585a-110">Voici un exemple de commande pour copier un répertoire source unique sur un disque dur qui n’a pas encore été chiffré avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="a585a-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="a585a-111">Copier deux répertoires sur un disque dur</span><span class="sxs-lookup"><span data-stu-id="a585a-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="a585a-112">Pour copier deux répertoires sources sur un disque, vous devez utiliser deux commandes.</span><span class="sxs-lookup"><span data-stu-id="a585a-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="a585a-113">La première commande spécifie le répertoire des journaux, la clé du compte de stockage, la lettre du lecteur cible et la configuration requise `format/encrypt`, outre les paramètres communs :</span><span class="sxs-lookup"><span data-stu-id="a585a-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="a585a-114">La deuxième commande spécifie le fichier journal, un nouvel ID de session, ainsi que les emplacements source et de destination :</span><span class="sxs-lookup"><span data-stu-id="a585a-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="a585a-115">Copier un fichier volumineux sur un disque dur dans une deuxième session de copie</span><span class="sxs-lookup"><span data-stu-id="a585a-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="a585a-116">Voici un exemple de commande qui copie un seul fichier volumineux sur un disque qui a été préparé dans une session de copie précédente :</span><span class="sxs-lookup"><span data-stu-id="a585a-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="a585a-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a585a-117">Next steps</span></span>

* [<span data-ttu-id="a585a-118">Exemple de workflow pour préparer des disques durs à un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="a585a-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
