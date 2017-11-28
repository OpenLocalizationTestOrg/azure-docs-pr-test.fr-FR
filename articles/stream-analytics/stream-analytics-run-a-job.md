---
title: "toostart aaaHow travaux dans le flux de données Analytique de diffusion en continu | Documents Microsoft"
description: "Comment exécuter une tâche de diffusion en continu dans Azure Stream Analytics | segment du parcours d’apprentissage."
keywords: "diffusion en continu de tâches"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="11a0a-104">Comment toorun une diffusion en continu de la tâche dans Azure flux Analytique</span><span class="sxs-lookup"><span data-stu-id="11a0a-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="11a0a-105">Lorsqu’une tâche d’entrée, de requêtes et de sortie ont tous été spécifiés que vous pouvez démarrer la tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="11a0a-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="11a0a-106">toostart votre travail :</span><span class="sxs-lookup"><span data-stu-id="11a0a-106">toostart your job:</span></span>

1. <span data-ttu-id="11a0a-107">Dans le portail Azure Classic hello, à partir du tableau de bord projet hello, cliquez sur **Démarrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="11a0a-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Bouton Démarrer la tâche](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="11a0a-109">Bonjour portail Azure, cliquez sur **Démarrer** haut hello de votre page de travail.</span><span class="sxs-lookup"><span data-stu-id="11a0a-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Bouton Démarrer le travail du portail Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="11a0a-111">Spécifiez un **démarrer une sortie** toodetermine valeur lors de la tâche commencera à générer une sortie.</span><span class="sxs-lookup"><span data-stu-id="11a0a-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="11a0a-112">Hello paramètre par défaut pour les travaux qui n’ont pas déjà été démarré est **heure de début de tâche**, ce qui signifie que le travail hello démarre immédiatement le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="11a0a-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="11a0a-113">Vous pouvez également spécifier un **personnalisé** temps Bonjour passé (pour consommer des données d’historique) ou hello future (toodelay traitement jusqu'à une date future).</span><span class="sxs-lookup"><span data-stu-id="11a0a-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="11a0a-114">Pour les cas où un travail a été démarré et arrêté, précédemment hello option **heure du dernier arrêt** est disponible dans la tâche de hello tooresume ordre à partir de hello dernière heure de sortie et d’éviter la perte de données.</span><span class="sxs-lookup"><span data-stu-id="11a0a-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Heure de démarrage de la tâche de diffusion en continu](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Heure de démarrage du travail de streaming dans le portail Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="11a0a-117">Confirmez votre sélection.</span><span class="sxs-lookup"><span data-stu-id="11a0a-117">Confirm your selection.</span></span> <span data-ttu-id="11a0a-118">état de la tâche Hello modifiera trop*départ* et déplacera peu trop*en cours d’exécution* une fois que le travail hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="11a0a-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="11a0a-119">Vous pouvez surveiller la progression hello Hello **Démarrer** opération Bonjour **Hub de Notification**:</span><span class="sxs-lookup"><span data-stu-id="11a0a-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![progression de la tâche de diffusion en continu](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Progression du travail de streaming dans le portail Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="11a0a-122">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="11a0a-122">Get help</span></span>
<span data-ttu-id="11a0a-123">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="11a0a-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="11a0a-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11a0a-124">Next steps</span></span>
* [<span data-ttu-id="11a0a-125">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="11a0a-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="11a0a-126">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11a0a-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="11a0a-127">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11a0a-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="11a0a-128">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11a0a-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="11a0a-129">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11a0a-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

