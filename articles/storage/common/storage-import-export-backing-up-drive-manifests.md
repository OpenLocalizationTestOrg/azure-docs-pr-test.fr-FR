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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="42620-103">Sauvegarde de manifestes de lecteur pour les travaux Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="42620-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="42620-104">Manifestes de lecteur peuvent être automatiquement sauvegardés tooblobs en définissant un hello `BackupDriveManifest` propriété trop`true` Bonjour [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) opérations d’API REST.</span><span class="sxs-lookup"><span data-stu-id="42620-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="42620-105">Par défaut, les manifestes de lecteur hello ne sont pas sauvegardés.</span><span class="sxs-lookup"><span data-stu-id="42620-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="42620-106">sauvegardes de manifeste de lecteur Hello sont stockées en tant qu’objets BLOB de blocs dans un conteneur avec un compte de stockage hello associé hello travail.</span><span class="sxs-lookup"><span data-stu-id="42620-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="42620-107">Par défaut, le nom du conteneur hello est `waimportexport`, mais vous pouvez spécifier un autre nom Bonjour `DiagnosticsPath` propriété lors de l’appel hello `Put Job` ou `Update Job Properties` operations.</span><span class="sxs-lookup"><span data-stu-id="42620-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="42620-108">Hello manifeste sauvegarde d’objet blob sont nommés hello suivant le format : `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="42620-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="42620-109">Vous pouvez récupérer hello URI de disque de sauvegarde hello manifestes pour un travail en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération.</span><span class="sxs-lookup"><span data-stu-id="42620-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="42620-110">blob Hello URI est retourné dans hello `ManifestUri` propriété pour chaque lecteur.</span><span class="sxs-lookup"><span data-stu-id="42620-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42620-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42620-111">Next steps</span></span>

* [<span data-ttu-id="42620-112">À l’aide des API REST du service importation/exportation hello</span><span class="sxs-lookup"><span data-stu-id="42620-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
