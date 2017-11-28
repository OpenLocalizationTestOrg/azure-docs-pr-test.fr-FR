---
title: "référence aaaQuick pour les commandes de travail outil d’importation/exportation Azure import - v1 | Documents Microsoft"
description: "Référence de l’outil Azure Import/Export pour les commandes de travail d’importation fréquemment utilisées. Cela fait référence toov1 Hello outil d’importation/exportation."
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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="10646-104">Aide-mémoire sur les commandes fréquemment utilisées pour les travaux d’importation</span><span class="sxs-lookup"><span data-stu-id="10646-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="10646-105">Cette section fournit un aide-mémoire pour certaines commandes fréquemment utilisées.</span><span class="sxs-lookup"><span data-stu-id="10646-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="10646-106">Pour une utilisation détaillée, consultez [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="10646-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="10646-107">Préparer un disque dur lorsque les données ont déjà été copié le disque dur de toohello</span><span class="sxs-lookup"><span data-stu-id="10646-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="10646-108">Hello suivant commande prépare un disque dur lorsque des données a déjà été copié tooit, mais n’a pas encore été chiffrées avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="10646-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="10646-109">Copier un disque dur tooa de répertoire unique</span><span class="sxs-lookup"><span data-stu-id="10646-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="10646-110">Hello commande suivante copie un seul répertoire tooa disque source qui n’a pas encore été chiffré avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="10646-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="10646-111">Copier deux répertoires tooa disque</span><span class="sxs-lookup"><span data-stu-id="10646-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="10646-112">toocopy deux source répertoires tooa lecteur hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="10646-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="10646-113">Hello première commande Spécifie répertoire du journal hello, clé de compte de stockage, lettre du lecteur cible `format/encrypt` configuration requise et les paramètres communs :</span><span class="sxs-lookup"><span data-stu-id="10646-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="10646-114">Hello deuxième commande spécifie hello journal fichier, un nouvel ID de session et les emplacements source et destination hello :</span><span class="sxs-lookup"><span data-stu-id="10646-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="10646-115">Copier un disque dur tooa de fichiers volumineux dans une deuxième session de copie</span><span class="sxs-lookup"><span data-stu-id="10646-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="10646-116">Hello commande suivante copie un seul fichier volumineux tooa disque qui a été préparé dans une session de copie précédente :</span><span class="sxs-lookup"><span data-stu-id="10646-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="10646-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10646-117">Next steps</span></span>

* [<span data-ttu-id="10646-118">Exemple workflow tooprepare les disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="10646-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
