---
title: "aaaRepairing un travail d’importation Azure Import/Export - v1 | Documents Microsoft"
description: "Découvrez comment un travail d’importation a été créé et exécuté à l’aide de toorepair hello Azure Import/Export service."
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
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Réparation d’un travail d’importation
Hello service Microsoft Azure Import/Export risque d’échouer toocopy certains de vos fichiers ou les parties d’un fichier de toohello service Blob Windows Azure. Voici quelques exemples de raisons de ces échecs :  
  
-   Fichiers endommagés  
  
-   Lecteurs endommagés  
  
-   clé de compte de stockage d’Hello changée pendant le transfert de fichier de hello.  
  
Vous pouvez exécuter hello outil d’importation/exportation de Microsoft Azure à l’importation de hello de fichiers journaux de copie du travail, et outil de hello téléchargera les fichiers manquants hello (ou les parties d’un fichier) travail d’importation toocomplete tooyour Windows Azure storage compte.  
  
## <a name="repairimport-parameters"></a>Paramètres de RepairImport

Hello paramètres suivants peuvent être spécifiés avec **RepairImport**: 
  
|||  
|-|-|  
|**/r:**&lt;RepairFile\>|**Obligatoire.** Chemin d’accès toohello fichier de réparation qui suit la progression de la réparation de hello hello et vous permet de tooresume une réparation interrompue. Chaque disque ne doit avoir qu’un fichier de réparation. Lorsque vous démarrez une réparation pour un lecteur donné, vous passez hello chemin d’accès tooa réparer un fichier qui n’existe pas. tooresume une réparation interrompue, vous devez passer dans le nom d’un fichier existant de la réparation de hello. lecteur cible correspondant toohello d’Hello réparation fichier doit toujours être spécifié.|  
|**/logdir:**&lt;LogDirectory\>|**Facultatif.** répertoire de journal Hello. Les fichiers journaux détaillés seront écrit toothis active. Si aucun répertoire de journal est spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello.|  
|**/d:**&lt;TargetDirectories\>|**Obligatoire.** Un ou plusieurs répertoires séparés par des points-virgules contenant hello des fichiers d’origine qui ont été importés. lecteur d’importation Hello peut-être également être utilisé, mais n’est pas nécessaire si d’autres emplacements de fichiers d’origine sont disponibles.|  
|**/bk:**&lt;BitLockerKey\>|**Facultatif.** Vous devez spécifier la clé de BitLocker hello si vous souhaitez hello outil toounlock un lecteur chiffré dans lequel les fichiers d’origine hello sont disponibles.|  
|**/sn:**&lt;StorageAccountName\>|**Obligatoire.** tâche d’importation nom Hello hello du compte de stockage pour hello.|  
|**/sk:**&lt;StorageAccountKey\>|**Obligatoire** si et seulement si une SAP de conteneur n’est pas spécifiée. tâche d’importation de clé de compte Hello hello compte de stockage pour hello.|  
|**/csas:**&lt;ContainerSas\>|**Requis** si et seulement si la clé de compte de stockage hello n’est pas spécifiée. Hello SAP de conteneur pour accéder aux objets BLOB de hello associé au travail d’importation hello.|  
|**/CopyLogFile:**&lt;DriveCopyLogFile\>|**Obligatoire.** Chemin d’accès toohello lecteur fichier journal de copie (journal détaillé ou journal des erreurs). fichier de Hello est généré par hello service Windows Azure Import/Export et peut être téléchargé à partir du stockage d’objets blob hello associé hello travail. fichier journal de copie Hello contient des informations sur les objets BLOB en échec ou les fichiers qui sont toobe réparé.|  
|**/PathMapFile:**&lt;DrivePathMapFile\>|**Facultatif.** Fichier texte tooa chemin d’accès peut être utilisé tooresolve ambiguïtés si vous avez plusieurs fichiers hello même nom que celui que vous importez dans hello même travail. outil hello première Hello est exécutée, elle peut remplir ce fichier avec tous les noms ambigus hello. Les exécutions suivantes de l’outil de hello utilisera cette ambiguïtés au niveau du fichier tooresolve hello.|  
  
## <a name="using-hello-repairimport-command"></a>À l’aide de la commande RepairImport de hello  
toorepair d’importer des données par diffusion en continu des données de salutation réseau hello, vous devez spécifier les répertoires hello contenant les fichiers d’origine hello vous importez à l’aide de hello `/d` paramètre. Vous devez également spécifier le fichier journal de copie hello que vous avez téléchargé à partir de votre compte de stockage. Une ligne de commande classique de toorepair un travail d’importation avec des échecs partiels ressemble à ceci :  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
Hello Voici un exemple d’un fichier journal de copie. Dans ce cas, une partie de 64 Ko d’un fichier a été endommagé sur le lecteur hello qui a été expédié pour le travail d’importation hello. Dans la mesure où il s’agit de hello seule erreur indiquée, reste hello d’objets BLOB de hello dans la tâche de hello ont été correctement importés.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
Lorsque ce journal de copie est passé toohello outil d’importation/exportation Azure, outil de hello essaiera importation de hello toofinish pour ce fichier en copiant le contenu manquant de hello réseau hello. Selon l’exemple hello ci-dessus, outil de hello recherchera les fichiers d’origine hello `\animals\koala.jpg` dans les répertoires hello deux `C:\Users\bob\Pictures` et `X:\BobBackup\photos`. Si hello fichier `C:\Users\bob\Pictures\animals\koala.jpg` existe, hello outil d’importation/exportation Azure copie hello la plage manquante de l’objet blob de données toohello correspondant `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Résolution des conflits lors de l’utilisation de RepairImport  
Dans certaines situations, outil de hello peut-être pas toofind en mesure ou un fichier de nécessaires hello ouvert pour l’une des hello suivant raisons : Impossible de trouver le fichier de hello, fichier de hello n’est pas accessible, nom de fichier hello est ambigu ou le contenu du fichier de hello hello n’est plus approprié.  
  
Une erreur ambiguë peut se produire si l’outil de hello tente toolocate `\animals\koala.jpg` et qu’il existe un fichier portant ce nom dans les répertoires `C:\Users\bob\pictures` et `X:\BobBackup\photos`. Autrement dit, les deux `C:\Users\bob\pictures\animals\koala.jpg` et `X:\BobBackup\photos\animals\koala.jpg` existent sur des lecteurs de travail d’importation hello.  
  
Hello `/PathMapFile` option vous permettra de tooresolve ces erreurs. Vous pouvez spécifier le nom hello du fichier hello qui contiendra la liste hello des fichiers hello outil n’a pas pu identifier de toocorrectly. Hello Voici un exemple de ligne de commande qui remplirait `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Hello outil écrira ensuite hello problématique chemins d’accès trop`9WM35C2V_pathmap.txt`, une sur chaque ligne. Par exemple, fichier de hello peut contenir des hello suivant entrées après avoir exécuté la commande hello :  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Pour chaque fichier dans la liste de hello, vous devez tenter de toolocate et ouvrez hello tooensure de fichier toohello disponible outil. Si vous le souhaitez outil de hello tootell explicitement toofind un fichier, vous pouvez modifier le chemin d’accès de hello mapper le fichier et ajouter le fichier de tooeach de chemin d’accès hello sur hello même ligne, séparé par un caractère de tabulation :  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
Après avoir outil toohello disponible de fichiers nécessaires en hello, ou fichier de mappage de chemin d’accès hello mise à jour, vous pouvez réexécuter le processus d’importation hello outil toocomplete hello.  
  
## <a name="next-steps"></a>Étapes suivantes
 
* [Configuration des hello, outil d’importation/exportation Azure](storage-import-export-tool-setup-v1.md)   
* [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Consultation de l’état du travail avec les fichiers journaux de copie](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Réparation d’un travail d’exportation](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Résolution des problèmes de hello outil d’importation/exportation Azure](storage-import-export-tool-troubleshooting-v1.md)
