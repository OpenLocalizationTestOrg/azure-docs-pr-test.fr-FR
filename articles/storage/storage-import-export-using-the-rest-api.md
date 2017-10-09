---
title: aaaUsing hello API REST du service Azure Import/Export | Documents Microsoft
description: "Découvrez où toofind des ressources pour l’utilisation de hello Azure Import/Export service API REST, y compris les deux documents de référence tooand de procédure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>À l’aide des API REST du service Azure Import/Export hello

Hello service Microsoft Azure Import/Export expose un contrôle par programmation de tooenable d’API REST de travaux d’importation/exportation. Vous pouvez utiliser les API REST de hello tooperform hello toutes les opérations que vous pouvez effectuer avec hello importation/exportation [portail Azure](https://portal.azure.com/). En outre, vous pouvez utiliser hello API REST tooperform certaines opérations granulaires, comme l’interrogation de hello Pourcentage achèvement d’une tâche, qui ne sont pas actuellement disponibles dans le portail classique de hello.

Consultez [à l’aide du service d’importation/exportation de Microsoft Azure hello données tooTransfer tooBlob stockage](storage-import-export-service.md) pour une vue d’ensemble du service d’importation/exportation hello et un didacticiel qui montre comment toouse hello toocreate portail classique et gérer l’importation travaux et d’exportation.

## <a name="service-endpoints"></a>Points de terminaison de service

Hello service Azure Import/Export est un fournisseur de ressources pour le Gestionnaire de ressources Azure et fournit un ensemble d’API REST à hello après le point de terminaison HTTPS pour la gestion des travaux d’importation/exportation :

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Contrôle de version

Demandes de toohello service d’importation/exportation doit spécifier hello `api-version` paramètre et définissez sa valeur trop`2016-11-01`.

## <a name="importexport-service-operations"></a>Opérations du service Import/Export

[Création d’un travail d’importation](storage-import-export-creating-an-import-job.md)

[Création d’un travail d’exportation](storage-import-export-creating-an-export-job.md)

[Récupération des informations d’état d’un travail](storage-import-export-retrieving-state-info-for-a-job.md)

[Énumération des travaux](storage-import-export-enumerating-jobs.md)

[Annulation et suppression de travaux](storage-import-export-cancelling-and-deleting-jobs.md)

[Sauvegarde de manifestes de lecteur](storage-import-export-backing-up-drive-manifests.md)

[Diagnostic et récupération d’erreur pour les travaux d’importation / exportation](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Étapes suivantes

* [API REST d’importation/exportation de stockage](/rest/api/storageimportexport)
