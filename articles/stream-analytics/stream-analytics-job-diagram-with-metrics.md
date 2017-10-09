---
title: "AAA Analytique de flux de données Azure piloté par les données de débogage à l’aide du schéma de tâche hello | Documents Microsoft"
description: "Résoudre les problèmes de votre tâche de flux de données Analytique à l’aide de mesures et schéma de tâche hello."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="fde06-103">Débogage à l’aide du schéma de tâche hello piloté par les données</span><span class="sxs-lookup"><span data-stu-id="fde06-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="fde06-104">diagramme de travail Hello sur hello **analyse** panneau Bonjour portail Azure peut vous aider à visualiser le pipeline de votre travail.</span><span class="sxs-lookup"><span data-stu-id="fde06-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="fde06-105">Il montre les entrées, les sorties et les étapes de requête.</span><span class="sxs-lookup"><span data-stu-id="fde06-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="fde06-106">Vous pouvez utiliser des métriques de hello tooexamine hello travail diagramme pour chaque étape, toomore isoler rapidement source hello d’un problème pour résoudre des problèmes.</span><span class="sxs-lookup"><span data-stu-id="fde06-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="fde06-107">À l’aide du schéma de tâche hello</span><span class="sxs-lookup"><span data-stu-id="fde06-107">Using hello job diagram</span></span>

<span data-ttu-id="fde06-108">Bonjour portail Azure, alors que dans une tâche de flux de données Analytique sous **prise en charge + dépannage**, sélectionnez **diagramme de travail**:</span><span class="sxs-lookup"><span data-stu-id="fde06-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagramme de travail avec des mesures - emplacement](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="fde06-110">Sélectionnez chaque section requête étape toosee hello correspondant dans une volet de modification de la requête.</span><span class="sxs-lookup"><span data-stu-id="fde06-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="fde06-111">Un graphique de métrique de l’étape hello est affiché dans un volet inférieur de la page de hello.</span><span class="sxs-lookup"><span data-stu-id="fde06-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagramme de travail avec des mesures - travail de base](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="fde06-113">partitions de hello toosee d’entrée de concentrateurs d’événements Azure hello, sélectionnez **...**</span><span class="sxs-lookup"><span data-stu-id="fde06-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="fde06-114">Un menu contextuel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fde06-114">A context menu appears.</span></span> <span data-ttu-id="fde06-115">Vous pouvez également voir fusion d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="fde06-115">You also can see hello input merger.</span></span>

![Diagramme de travail avec des mesures - étendre une partition](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="fde06-117">graphique de métrique hello toosee pour une seule partition, nœud de partition hello select.</span><span class="sxs-lookup"><span data-stu-id="fde06-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="fde06-118">métriques de Hello sont affichés en bas de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="fde06-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagramme de travail avec des mesures - mesures supplémentaires](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="fde06-120">graphique des métriques toosee hello pour une fusion, le nœud de fusion hello select.</span><span class="sxs-lookup"><span data-stu-id="fde06-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="fde06-121">Hello suivant le graphique indique qu’aucun événement ont été supprimés ou ajustée.</span><span class="sxs-lookup"><span data-stu-id="fde06-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagramme de travail avec des mesures - grille](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="fde06-123">Détails de hello toosee de valeur de métrique hello et l’heure, point toohello graphique.</span><span class="sxs-lookup"><span data-stu-id="fde06-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diagramme de travail avec des mesures - pointer](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="fde06-125">Résoudre les problèmes à l’aide de mesures</span><span class="sxs-lookup"><span data-stu-id="fde06-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="fde06-126">Hello **QueryLastProcessedTime** métrique indique quand une étape spécifique a reçu des données.</span><span class="sxs-lookup"><span data-stu-id="fde06-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="fde06-127">En examinant la topologie de hello, vous pouvez travailler à partir de hello sortie processeur toosee étape qui ne reçoit pas de données.</span><span class="sxs-lookup"><span data-stu-id="fde06-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="fde06-128">Si une étape ne reçoit pas de données, passez à étape de requête toohello juste avant qu’il.</span><span class="sxs-lookup"><span data-stu-id="fde06-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="fde06-129">Vérifiez si une fenêtre de temps a hello précédente étape de requête, et si suffisamment longtemps pour qu’il toooutput données.</span><span class="sxs-lookup"><span data-stu-id="fde06-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="fde06-130">(Notez que temporelles windows sont alignés toohello heure).</span><span class="sxs-lookup"><span data-stu-id="fde06-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="fde06-131">Si hello étape de requête précédente est un processeur d’entrée, les éléments suivants utilisez hello métriques d’entrée toohelp réponses hello ciblé questions.</span><span class="sxs-lookup"><span data-stu-id="fde06-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="fde06-132">Elles peuvent vous aider à déterminer si un travail récupère des données à partir de ses sources d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fde06-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="fde06-133">Si la requête de hello est partitionnée, examinez chaque partition.</span><span class="sxs-lookup"><span data-stu-id="fde06-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="fde06-134">Quelle est la quantité de données lue ?</span><span class="sxs-lookup"><span data-stu-id="fde06-134">How much data is being read?</span></span>

*   <span data-ttu-id="fde06-135">**InputEventsSourcesTotal** est le nombre de hello d’unités de données en lecture.</span><span class="sxs-lookup"><span data-stu-id="fde06-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="fde06-136">Par exemple, hello nombre d’objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="fde06-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="fde06-137">**InputEventsTotal** nombre de hello d’événements de lecture.</span><span class="sxs-lookup"><span data-stu-id="fde06-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="fde06-138">Cette mesure est disponible par partition.</span><span class="sxs-lookup"><span data-stu-id="fde06-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="fde06-139">**InputEventsInBytesTotal** est le nombre de hello d’octets lus.</span><span class="sxs-lookup"><span data-stu-id="fde06-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="fde06-140">**InputEventsLastArrivalTime** est mis à jour avec chaque durée de file d’attente des événements reçus.</span><span class="sxs-lookup"><span data-stu-id="fde06-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="fde06-141">La chronologie progresse-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="fde06-141">Is time moving forward?</span></span> <span data-ttu-id="fde06-142">Si des événements réels sont lus, il est possible qu’aucune ponctuation ne soit émise.</span><span class="sxs-lookup"><span data-stu-id="fde06-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="fde06-143">**InputEventsLastPunctuationTime** indique quand un signe de ponctuation a été émis tookeep temps à transférer vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="fde06-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="fde06-144">Si la ponctuation n’est pas émise, le flux de données peut être bloqué.</span><span class="sxs-lookup"><span data-stu-id="fde06-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="fde06-145">Existe-t-il des erreurs dans l’entrée de hello ?</span><span class="sxs-lookup"><span data-stu-id="fde06-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="fde06-146">**InputEventsEventDataNullTotal** correspond au nombre d’événements présentant des données nulles.</span><span class="sxs-lookup"><span data-stu-id="fde06-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="fde06-147">**InputEventsSerializerErrorsTotal** correspond au nombre d’événements qui n’ont pas pu être désérialisés correctement.</span><span class="sxs-lookup"><span data-stu-id="fde06-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="fde06-148">**InputEventsDegradedTotal** correspond au nombre d’événements présentant un problème autre que la désérialisation.</span><span class="sxs-lookup"><span data-stu-id="fde06-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="fde06-149">Les événements sont-ils supprimés ou modifiés ?</span><span class="sxs-lookup"><span data-stu-id="fde06-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="fde06-150">**InputEventsEarlyTotal** nombre de hello d’événements qui ont un horodateur de l’application avant la limite supérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="fde06-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="fde06-151">**InputEventsLateTotal** est nombre hello d’événements qui ont un horodateur de l’application après la limite supérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="fde06-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="fde06-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** est le nombre d’événements hello supprimé avant l’heure de début du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="fde06-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="fde06-153">Sommes-nous en retard en matière de lecture des données ?</span><span class="sxs-lookup"><span data-stu-id="fde06-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="fde06-154">**InputEventsSourcesBackloggedTotal** vous indique de combien de messages plus besoin toobe lire pour les entrées de concentrateurs d’événements et Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fde06-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="fde06-155">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="fde06-155">Get help</span></span>
<span data-ttu-id="fde06-156">Pour une assistance supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="fde06-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fde06-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fde06-157">Next steps</span></span>
* [<span data-ttu-id="fde06-158">Introduction tooStream Analytique</span><span class="sxs-lookup"><span data-stu-id="fde06-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fde06-159">Prise en main de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fde06-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fde06-160">Mise à l’échelle des travaux Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fde06-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fde06-161">Informations de référence sur le langage de requête Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fde06-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fde06-162">Références sur l’API REST de gestion de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fde06-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
