---
title: "aaaReviewing v1 - état du travail Azure Import/Export | Documents Microsoft"
description: "Découvrez comment les fichiers de journaux de hello toouse créés lorsque hello importation ou travail d’exportation a été exécutée état de hello toosee de tâche d’importation/exportation hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Vérification de l’état des travaux Azure Import/Export avec les copies des fichiers journaux
En cas de hello service Microsoft Azure Import/Export traite les lecteurs associés à un travail d’importation ou d’exportation, il écrit copie journal fichiers toohello stockage compte tooor à partir de laquelle vous importez ou exportez des objets BLOB. fichier journal de Hello contient l’état détaillé de chaque fichier qui a été importé ou exporté. fichier journal de copie Hello URL tooeach est retourné lorsque vous interrogez l’état hello d’un travail effectué ; consultez [Get Job](/rest/api/storageservices/Get-Job3) pour plus d’informations.  

## <a name="example-urls"></a>Exemples d’URL

Hello Voici des exemples d’URL pour les fichiers journaux de copie pour un travail d’importation avec deux lecteurs :  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Consultez [service d’importation/exportation Format de fichier journal](storage-import-export-file-format-log.md) pour le format des journaux de copie et de la liste complète des codes d’état hello hello.  
  
## <a name="next-steps"></a>Étapes suivantes
 
 * [Configuration des hello, outil d’importation/exportation Azure](storage-import-export-tool-setup-v1.md)   
 * [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Réparation d’un travail d’importation](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Réparation d’un travail d’exportation](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Résolution des problèmes de hello outil d’importation/exportation Azure](storage-import-export-tool-troubleshooting-v1.md)
