---
title: "travaux d’Analytique de LAC de données Azure aaaTroubleshoot à l’aide du portail Azure | Documents Microsoft"
description: "Découvrez comment toouse hello travaux de portail Azure tootroubleshoot Analytique lac de données. "
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="31471-103">Dépanner les travaux Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="31471-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="31471-104">Découvrez comment toouse hello travaux de portail Azure tootroubleshoot Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="31471-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="31471-105">Dans ce didacticiel, vous le programme d’installation d’un problème de fichier source manquant et utiliser hello Azure Portal tootroubleshoot hello problème.</span><span class="sxs-lookup"><span data-stu-id="31471-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="31471-106">Envoyer le travail Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="31471-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="31471-107">Soumettre hello suivant travail U-SQL :</span><span class="sxs-lookup"><span data-stu-id="31471-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="31471-108">Bonjour fichier source défini dans le script de hello est **/Samples/Data/SearchLog.tsv1**, où il doit être **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="31471-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="31471-109">Résoudre les problèmes des travaux de hello</span><span class="sxs-lookup"><span data-stu-id="31471-109">Troubleshoot hello job</span></span>

<span data-ttu-id="31471-110">**toosee tous hello travaux**</span><span class="sxs-lookup"><span data-stu-id="31471-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="31471-111">À partir de hello portail Azure, cliquez sur **Microsoft Azure** dans le coin supérieur gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="31471-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="31471-112">Cliquez sur mosaïque hello avec le nom de votre compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="31471-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="31471-113">Résumé des tâches Hello sont indiquée sur hello **gestion des travaux** vignette.</span><span class="sxs-lookup"><span data-stu-id="31471-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Gestion du travail Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="31471-115">le travail Hello gestion vous donne un aperçu de l’état de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="31471-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="31471-116">Notez qu’il s’agit d’une tâche ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="31471-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="31471-117">Cliquez sur hello **gestion des travaux** vignette des travaux de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="31471-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="31471-118">travaux de Hello est classées en **en cours d’exécution**, **en file d’attente**, et **terminé**.</span><span class="sxs-lookup"><span data-stu-id="31471-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="31471-119">Vous allez voir votre travail ayant échoué Bonjour **terminé** section.</span><span class="sxs-lookup"><span data-stu-id="31471-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="31471-120">Il doit être dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="31471-120">It shall be first one in hello list.</span></span> <span data-ttu-id="31471-121">Lorsque vous avez un grand nombre de travaux, vous pouvez cliquer sur **filtre** toohelp vous toolocate travaux.</span><span class="sxs-lookup"><span data-stu-id="31471-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Travail de filtre d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="31471-123">Cliquez sur hello le travail ayant échoué à partir de hello liste tooopen hello détails d’une tâche dans un nouveau panneau :</span><span class="sxs-lookup"><span data-stu-id="31471-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Travail d’échec d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="31471-125">Hello d’avis **renvoyer** bouton.</span><span class="sxs-lookup"><span data-stu-id="31471-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="31471-126">Après avoir corrigé le problème de hello, vous pouvez renvoyer le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="31471-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="31471-127">Cliquez sur la partie en surbrillance de hello précédente capture d’écran tooopen hello détails de l’erreur.</span><span class="sxs-lookup"><span data-stu-id="31471-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="31471-128">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="31471-128">You shall see something like:</span></span>

    ![Détails sur le travail d’échec d’Analytique Data Lake Azure](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="31471-130">Il indique le dossier source de hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="31471-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="31471-131">Cliquez sur **Dupliquer le Script**.</span><span class="sxs-lookup"><span data-stu-id="31471-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="31471-132">Hello de mise à jour **FROM** toohello chemin qui suit :</span><span class="sxs-lookup"><span data-stu-id="31471-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="31471-133">« Samples/Data/SearchLog.tsv »</span><span class="sxs-lookup"><span data-stu-id="31471-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="31471-134">Cliquez sur **Envoyer le travail**.</span><span class="sxs-lookup"><span data-stu-id="31471-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="31471-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="31471-135">See also</span></span>
* [<span data-ttu-id="31471-136">Présentation d’Analytique Data Lake Azure</span><span class="sxs-lookup"><span data-stu-id="31471-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="31471-137">Prise en main d’Analytique Data Lake à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="31471-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="31471-138">Prise en main d’Analytique Data Lake Azure et U-SQL à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31471-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="31471-139">Gestion d'Azure Data Lake Analytics à l'aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="31471-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
