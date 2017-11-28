---
title: "Vérification de l’état des travaux Azure Import/Export - v1 | Microsoft Docs"
description: "Découvrez comment utiliser les fichiers journaux créés lors de l’exécution du travail d’importation ou d’exportation pour connaître l’état du travail Import/Export."
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
ms.openlocfilehash: 621e41df127fded6ec6fe1f71e86cb8630965a70
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="5a8f2-103">Vérification de l’état des travaux Azure Import/Export avec les copies des fichiers journaux</span><span class="sxs-lookup"><span data-stu-id="5a8f2-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="5a8f2-104">Lorsque le service Microsoft Azure Import/Export traite des lecteurs associés à un travail d’importation ou d’exportation, il écrit les fichiers journaux de copie dans le compte de stockage dans ou à partir duquel vous importez ou exportez des objets blob.</span><span class="sxs-lookup"><span data-stu-id="5a8f2-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="5a8f2-105">Le fichier journal contient l’état détaillé de chaque fichier importé ou exporté.</span><span class="sxs-lookup"><span data-stu-id="5a8f2-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="5a8f2-106">L’URL de chaque fichier journal de copie est renvoyée lorsque vous interrogez l’état d’un travail effectué ; consultez la page [Get Job](/rest/api/storageservices/Get-Job3) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5a8f2-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="5a8f2-107">Exemples d’URL</span><span class="sxs-lookup"><span data-stu-id="5a8f2-107">Example URLs</span></span>

<span data-ttu-id="5a8f2-108">Voici des exemples d’URL de fichiers journaux de copie pour un travail d’importation avec deux lecteurs :</span><span class="sxs-lookup"><span data-stu-id="5a8f2-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="5a8f2-109">Consultez la page [Format des fichiers journaux du Service Import-Export](storage-import-export-file-format-log.md) pour connaître le format des journaux de copie et la liste complète des codes d’état.</span><span class="sxs-lookup"><span data-stu-id="5a8f2-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="5a8f2-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a8f2-110">Next steps</span></span>
 
 * [<span data-ttu-id="5a8f2-111">Configuration de l’outil Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="5a8f2-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="5a8f2-112">Préparation des disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="5a8f2-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="5a8f2-113">Réparation d’un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="5a8f2-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="5a8f2-114">Réparation d’un travail d’exportation</span><span class="sxs-lookup"><span data-stu-id="5a8f2-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="5a8f2-115">Résolution des problèmes associés à l’outil Azure Import-Export</span><span class="sxs-lookup"><span data-stu-id="5a8f2-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
