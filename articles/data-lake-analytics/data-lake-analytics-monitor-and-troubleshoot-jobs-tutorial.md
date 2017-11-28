---
title: "Dépanner les travaux Azure Data Lake Analytics à l’aide du portail Azure | Microsoft Docs"
description: "Apprenez à utiliser le portail Azure afin de dépanner les travaux Data Lake Analytics. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="3a5cf-103">Dépanner les travaux Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3a5cf-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="3a5cf-104">Apprenez à utiliser le portail Azure afin de dépanner les travaux Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="3a5cf-105">Dans ce didacticiel, vous allez identifier un problème de fichier source manquant et utiliser le portail Azure pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="3a5cf-106">Envoyer le travail Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="3a5cf-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="3a5cf-107">Envoyer la tâche U-SQL suivante :</span><span class="sxs-lookup"><span data-stu-id="3a5cf-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="3a5cf-108">Le fichier source défini dans le script est **/Samples/Data/SearchLog.tsv1**, alors qu’il devrait s’agir de **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="3a5cf-109">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="3a5cf-109">Troubleshoot the job</span></span>

<span data-ttu-id="3a5cf-110">**Pour voir tous les travaux**</span><span class="sxs-lookup"><span data-stu-id="3a5cf-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="3a5cf-111">À partir du portail Azure, cliquez sur **Microsoft Azure** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="3a5cf-112">Cliquez sur la vignette indiquant le nom de votre compte Analytique Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="3a5cf-113">Le résumé du travail est affiché sur la vignette **Gestion des tâches** .</span><span class="sxs-lookup"><span data-stu-id="3a5cf-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Gestion du travail Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="3a5cf-115">La gestion des tâches vous offre un aperçu de l’état du travail.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="3a5cf-116">Notez qu’il s’agit d’une tâche ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="3a5cf-117">Cliquez sur la vignette **Gestion de la tâche** pour rechercher les travaux.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="3a5cf-118">Les travaux sont classés dans les catégories **En cours**, **En file d’attente** et **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="3a5cf-119">Vous devez voir le travail qui a échoué dans la section **Terminé** .</span><span class="sxs-lookup"><span data-stu-id="3a5cf-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="3a5cf-120">Il doit être le premier sur la liste.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-120">It shall be first one in the list.</span></span> <span data-ttu-id="3a5cf-121">Lorsque vous avez un grand nombre de travaux, vous pouvez cliquer sur **Filtrer** pour vous aider à localiser les travaux.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Travail de filtre d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="3a5cf-123">Cliquez sur le travail ayant échoué dans la liste pour ouvrir les détails du travail dans un nouveau panneau :</span><span class="sxs-lookup"><span data-stu-id="3a5cf-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Travail d’échec d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="3a5cf-125">Remarquez le bouton **Renvoyer** .</span><span class="sxs-lookup"><span data-stu-id="3a5cf-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="3a5cf-126">Après avoir résolu le problème, vous pouvez renvoyer le travail.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="3a5cf-127">Cliquez sur la partie mise en évidence de la capture d’écran précédente pour ouvrir les détails de l’erreur.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="3a5cf-128">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="3a5cf-128">You shall see something like:</span></span>

    ![Détails sur le travail d’échec d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="3a5cf-130">Elle vous indique que le dossier source est introuvable.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="3a5cf-131">Cliquez sur **Dupliquer le Script**.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="3a5cf-132">Mettez à jour le chemin d’accès **FROM** pour obtenir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="3a5cf-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="3a5cf-133">« Samples/Data/SearchLog.tsv »</span><span class="sxs-lookup"><span data-stu-id="3a5cf-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="3a5cf-134">Cliquez sur **Envoyer le travail**.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="3a5cf-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3a5cf-135">See also</span></span>
* [<span data-ttu-id="3a5cf-136">Présentation d’Analytique Data Lake Azure</span><span class="sxs-lookup"><span data-stu-id="3a5cf-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3a5cf-137">Prise en main d’Analytique Data Lake à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a5cf-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="3a5cf-138">Prise en main d’Analytique Data Lake Azure et U-SQL à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a5cf-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="3a5cf-139">Gestion d'Azure Data Lake Analytics à l'aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3a5cf-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
