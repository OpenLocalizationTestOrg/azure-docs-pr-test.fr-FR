---
title: aaaBacking des manifestes de lecteur Azure Import/Export | Documents Microsoft
description: "Découvrez comment toohave votre lecteur de manifestes pour le service de Microsoft Azure Import/Export hello sauvegardée automatiquement."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Sauvegarde de manifestes de lecteur pour les travaux Azure Import/Export

Manifestes de lecteur peuvent être automatiquement sauvegardés tooblobs en définissant un hello `BackupDriveManifest` propriété trop`true` Bonjour [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) opérations d’API REST. Par défaut, les manifestes de lecteur hello ne sont pas sauvegardés. sauvegardes de manifeste de lecteur Hello sont stockées en tant qu’objets BLOB de blocs dans un conteneur avec un compte de stockage hello associé hello travail. Par défaut, le nom du conteneur hello est `waimportexport`, mais vous pouvez spécifier un autre nom Bonjour `DiagnosticsPath` propriété lors de l’appel hello `Put Job` ou `Update Job Properties` operations. Hello manifeste sauvegarde d’objet blob sont nommés hello suivant le format : `waies/jobname_driveid_timestamp_manifest.xml`.

 Vous pouvez récupérer hello URI de disque de sauvegarde hello manifestes pour un travail en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération. blob Hello URI est retourné dans hello `ManifestUri` propriété pour chaque lecteur.

## <a name="next-steps"></a>Étapes suivantes

* [À l’aide des API REST du service importation/exportation hello](storage-import-export-using-the-rest-api.md)
