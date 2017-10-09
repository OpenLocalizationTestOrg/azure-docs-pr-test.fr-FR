---
title: "l’utilisation des lecteurs pour un travail d’exportation Azure Import/Export - v1 aaaPreviewing | Documents Microsoft"
description: "Découvrez la liste de hello toopreview d’objets BLOB que vous avez sélectionné pour un travail d’exportation dans le service d’importation/exportation Azure hello."
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
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>Aperçu de l’utilisation des lecteurs pour un travail d’exportation
Avant de créer un travail d’exportation, vous devez toochoose un ensemble d’objets BLOB toobe exporté. Hello service Microsoft Azure Import/Export vous permet de toouse une liste de chemins d’accès de l’objet blob ou objet blob de préfixes d’objets BLOB de hello toorepresent que vous avez sélectionné.  
  
Ensuite, vous devez toodetermine, nombre de disques dont vous avez besoin de toosend. Hello outil Import/Export fournit hello `PreviewExport` l’utilisation des lecteurs toopreview commande pour les objets BLOB de hello que vous avez sélectionné, en fonction de taille hello hello lecteurs que vous vous apprêtez toouse.

## <a name="command-line-parameters"></a>Paramètres de ligne de commande

Vous pouvez utiliser hello paramètres suivants lors de l’utilisation de hello `PreviewExport` commande Hello outil d’importation/exportation.

|Paramètre de ligne de commande|Description|  
|--------------------------|-----------------|  
|**/logdir:**&lt;LogDirectory\>|facultatif. répertoire de journal Hello. Les fichiers journaux détaillés seront écrit toothis active. Si aucun répertoire de journal est spécifié, répertoire actuel de hello sera utilisé comme répertoire de journal hello.|  
|**/sn:**&lt;StorageAccountName\>|Obligatoire. tâche d’exportation de nom Hello hello du compte de stockage pour hello.|  
|**/sk:**&lt;StorageAccountKey\>|Obligatoire si et seulement si aucune SAP de conteneur n’est spécifiée. tâche d’exportation de clé de compte Hello hello compte de stockage pour hello.|  
|**/csas:**&lt;ContainerSas\>|Obligatoire si et seulement si aucune clé du compte de stockage n’est spécifiée. SAP de conteneur Hello pour toobe d’objets BLOB annonce hello exportée dans le travail d’exportation hello.|  
|**/ExportBlobListFile:**&lt;ExportBlobListFile\>|Obligatoire. Chemin d’accès toohello XML du fichier contenant la liste des chemins d’accès de l’objet blob ou préfixes de chemin d’accès pour toobe d’objets BLOB hello exportée d’objets blob. format de fichier Hello utilisé Bonjour `BlobListBlobPath` élément Bonjour [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération Hello API REST du service importation/exportation.|  
|**/DriveSize:**&lt;DriveSize\>|Obligatoire. taille de toouse de lecteurs pour un travail d’exportation, de Hello *, par exemple*, 500 Go, 1,5 To.|  

## <a name="command-line-example"></a>Exemple de ligne de commande

exemple Hello illustre hello `PreviewExport` commande :  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Hello blob liste et fichier d’exportation peut contenir des noms d’objet blob d’objets blob préfixes, comme illustré ici :  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Hello, outil d’importation/exportation Azure répertorie tous les objets BLOB toobe exporté et calcule comment toopack les lecteurs de hello spécifié la taille, en prenant en compte toute surcharge nécessaire, évalue ensuite le nombre de hello de lecteurs nécessaires blobs de hello toohold et l’utilisation des lecteurs plus d’informations.  
  
Voici un exemple de sortie de hello, avec des journaux d’information omis :  
  
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
  
## <a name="next-steps"></a>Étapes suivantes

* [Référence sur l’outil Azure Import-Export](storage-import-export-tool-how-to-v1.md)
