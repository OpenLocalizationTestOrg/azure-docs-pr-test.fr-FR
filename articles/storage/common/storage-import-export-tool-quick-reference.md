---
title: "référence aaaQuick pour les commandes de travail d’importation outil d’importation/exportation Azure | Documents Microsoft"
description: "Référence de l’outil Azure Import/Export pour les commandes de travail d’importation fréquemment utilisées."
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
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="2aa15-103">Aide-mémoire sur les commandes fréquemment utilisées pour les travaux d’importation</span><span class="sxs-lookup"><span data-stu-id="2aa15-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="2aa15-104">Cet article fournit un aide-mémoire pour certaines commandes fréquemment utilisées.</span><span class="sxs-lookup"><span data-stu-id="2aa15-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="2aa15-105">Pour une utilisation détaillée, consultez [Préparation des disques durs pour un travail d’importation](../storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="2aa15-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="2aa15-106">Première session</span><span class="sxs-lookup"><span data-stu-id="2aa15-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="2aa15-107">Deuxième session</span><span class="sxs-lookup"><span data-stu-id="2aa15-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="2aa15-108">Annuler la dernière session</span><span class="sxs-lookup"><span data-stu-id="2aa15-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="2aa15-109">Reprise de la dernière session interrompue</span><span class="sxs-lookup"><span data-stu-id="2aa15-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="2aa15-110">Ajouter des lecteurs toolatest session</span><span class="sxs-lookup"><span data-stu-id="2aa15-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="2aa15-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2aa15-111">Next steps</span></span>

* [<span data-ttu-id="2aa15-112">Exemple workflow tooprepare les disques durs pour un travail d’importation</span><span class="sxs-lookup"><span data-stu-id="2aa15-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
