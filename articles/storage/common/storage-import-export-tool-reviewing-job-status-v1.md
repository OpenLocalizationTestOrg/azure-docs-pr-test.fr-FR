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
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="b46c9-103">Vérification de l’état des travaux Azure Import/Export avec les copies des fichiers journaux</span><span class="sxs-lookup"><span data-stu-id="b46c9-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="b46c9-104">En cas de hello service Microsoft Azure Import/Export traite les lecteurs associés à un travail d’importation ou d’exportation, il écrit copie journal fichiers toohello stockage compte tooor à partir de laquelle vous importez ou exportez des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="b46c9-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="b46c9-105">fichier journal de Hello contient l’état détaillé de chaque fichier qui a été importé ou exporté.</span><span class="sxs-lookup"><span data-stu-id="b46c9-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="b46c9-106">fichier journal de copie Hello URL tooeach est retourné lorsque vous interrogez l’état hello d’un travail effectué ; consultez [Get Job](/rest/api/storageservices/Get-Job3) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b46c9-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="b46c9-107">Exemples d’URL</span><span class="sxs-lookup"><span data-stu-id="b46c9-107">Example URLs</span></span>

<span data-ttu-id="b46c9-108">Hello Voici des exemples d’URL pour les fichiers journaux de copie pour un travail d’importation avec deux lecteurs :</span><span class="sxs-lookup"><span data-stu-id="b46c9-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="b46c9-109">Consultez [service d’importation/exportation Format de fichier journal](../storage-import-export-file-format-log.md) pour le format des journaux de copie et de la liste complète des codes d’état hello hello.</span><span class="sxs-lookup"><span data-stu-id="b46c9-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b46c9-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b46c9-110">Next steps</span></span>
 
 * [<span data-ttu-id="b46c9-111">Configuration des hello, outil d’importation/exportation Azure</span><span class="sxs-lookup"><span data-stu-id="b46c9-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="b46c9-112">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="b46c9-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="b46c9-113">Réparation d’un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="b46c9-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="b46c9-114">Réparation d’un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="b46c9-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="b46c9-115">Résolution des problèmes de hello outil d’importation/exportation Azure</span><span class="sxs-lookup"><span data-stu-id="b46c9-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
