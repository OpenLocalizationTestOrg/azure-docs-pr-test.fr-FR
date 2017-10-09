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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Aide-mémoire sur les commandes fréquemment utilisées pour les travaux d’importation
Cette section fournit des références rapides pour certaines commandes fréquemment utilisées. Pour une utilisation détaillée, consultez [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>Préparer les disques de hello lorsque les données copiées déjà toohello disques
 Voici un tooprepare de commande exemple un disque lorsque les données copiées déjà disque toohello qui n’a pas été encore été chiffré avec BitLocker :  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Copier un disque dur tooa de répertoire unique  
 Voici un toocopy de commande exemple une seule source directory tooa disque qui n’a pas été encore été chiffré avec BitLocker :  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>Copiez le disque dur de wwo répertoires tooa  
 toocopy deux répertoires tooa lecteur source, vous aurez besoin des deux commandes.  
  
 Hello première commande Spécifie répertoire du journal hello, clé de compte de stockage, lettre de lecteur cible et `format/encrypt` exigences, dans Paramètres communs d’addition toohello :  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 Hello deuxième commande spécifie hello journal fichier, un nouvel ID de session et les emplacements source et destination hello :  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Copier un disque dur tooa de fichiers volumineux dans une deuxième session de copie  
 Voici un exemple de commande qui copie un lecteur tooa seul fichier volumineux qui a été préparé dans une session de copie précédente :  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Étapes suivantes

* [Exemple workflow tooprepare les disques durs pour un travail d’importation](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
