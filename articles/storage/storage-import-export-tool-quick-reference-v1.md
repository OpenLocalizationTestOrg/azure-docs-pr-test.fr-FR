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
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="42885-104">Aide-mémoire sur les commandes fréquemment utilisées pour les travaux d’importation</span><span class="sxs-lookup"><span data-stu-id="42885-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="42885-105">Cette section fournit des références rapides pour certaines commandes fréquemment utilisées.</span><span class="sxs-lookup"><span data-stu-id="42885-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="42885-106">Pour une utilisation détaillée, consultez [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="42885-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="42885-107">Préparer les disques de hello lorsque les données copiées déjà toohello disques</span><span class="sxs-lookup"><span data-stu-id="42885-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="42885-108">Voici un tooprepare de commande exemple un disque lorsque les données copiées déjà disque toohello qui n’a pas été encore été chiffré avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="42885-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="42885-109">Copier un disque dur tooa de répertoire unique</span><span class="sxs-lookup"><span data-stu-id="42885-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="42885-110">Voici un toocopy de commande exemple une seule source directory tooa disque qui n’a pas été encore été chiffré avec BitLocker :</span><span class="sxs-lookup"><span data-stu-id="42885-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="42885-111">Copiez le disque dur de wwo répertoires tooa</span><span class="sxs-lookup"><span data-stu-id="42885-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="42885-112">toocopy deux répertoires tooa lecteur source, vous aurez besoin des deux commandes.</span><span class="sxs-lookup"><span data-stu-id="42885-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="42885-113">Hello première commande Spécifie répertoire du journal hello, clé de compte de stockage, lettre de lecteur cible et `format/encrypt` exigences, dans Paramètres communs d’addition toohello :</span><span class="sxs-lookup"><span data-stu-id="42885-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="42885-114">Hello deuxième commande spécifie hello journal fichier, un nouvel ID de session et les emplacements source et destination hello :</span><span class="sxs-lookup"><span data-stu-id="42885-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="42885-115">Copier un disque dur tooa de fichiers volumineux dans une deuxième session de copie</span><span class="sxs-lookup"><span data-stu-id="42885-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="42885-116">Voici un exemple de commande qui copie un lecteur tooa seul fichier volumineux qui a été préparé dans une session de copie précédente :</span><span class="sxs-lookup"><span data-stu-id="42885-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="42885-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42885-117">Next steps</span></span>

* [<span data-ttu-id="42885-118">Exemple workflow tooprepare les disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="42885-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
