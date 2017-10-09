---
title: "aaaUnderstanding analyse de flux de données Analytique travail | Documents Microsoft"
description: "Présentation de la surveillance des tâches Stream Analytics"
keywords: "surveillance des requêtes"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="24af1-104">Comprendre l’analyse de travail Analytique des flux de données et la manière dont les requêtes toomonitor</span><span class="sxs-lookup"><span data-stu-id="24af1-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="24af1-105">Introduction : la page hello moniteur</span><span class="sxs-lookup"><span data-stu-id="24af1-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="24af1-106">Hello portail Azure, les deux mesures de performances clés qui peuvent être utilisé toomonitor et résoudre les problèmes de performances de vos requêtes et de travail de surface.</span><span class="sxs-lookup"><span data-stu-id="24af1-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="24af1-107">toosee ces métriques, parcourir la tâche de flux de données Analytique toohello vous ne souhaitez afficher hello de vue et les métriques pour **analyse** section sur la page de vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="24af1-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Lien Surveillance](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="24af1-109">fenêtre Hello s’affichent comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="24af1-109">hello window will appear as shown:</span></span>

![Tableau de bord de surveillance des tâches](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="24af1-111">Mesures disponibles pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24af1-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="24af1-112">Mesure</span><span class="sxs-lookup"><span data-stu-id="24af1-112">Metric</span></span>                 | <span data-ttu-id="24af1-113">Définition</span><span class="sxs-lookup"><span data-stu-id="24af1-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="24af1-114">Utilisation de % d’unités de diffusion</span><span class="sxs-lookup"><span data-stu-id="24af1-114">SU % Utilization</span></span>       | <span data-ttu-id="24af1-115">utilisation de Hello de hello ou les unités de diffusion en continu affecté tooa travail à partir de l’onglet échelle hello du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="24af1-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="24af1-116">Si cet indicateur atteint 80 % ou plus, il est fort probable que le traitement des événements soit retardé ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="24af1-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="24af1-117">Événements d’entrée</span><span class="sxs-lookup"><span data-stu-id="24af1-117">Input Events</span></span>           | <span data-ttu-id="24af1-118">Quantité de données reçues par tâche de flux de données Analytique hello, dans le nombre d’événements.</span><span class="sxs-lookup"><span data-stu-id="24af1-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="24af1-119">Cela peut être utilisé toovalidate que les événements sont envoyés toohello des sources d’entrée.</span><span class="sxs-lookup"><span data-stu-id="24af1-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="24af1-120">Événements de sortie</span><span class="sxs-lookup"><span data-stu-id="24af1-120">Output Events</span></span>          | <span data-ttu-id="24af1-121">Quantité de données envoyées par hello flux Analytique toohello sortie cible du travail, dans le nombre d’événements.</span><span class="sxs-lookup"><span data-stu-id="24af1-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="24af1-122">Événements non ordonnés</span><span class="sxs-lookup"><span data-stu-id="24af1-122">Out-of-Order Events</span></span>    | <span data-ttu-id="24af1-123">Nombre d’événements reçus dans le désordre qui ont été supprimés ou dont un horodatage ajusté, en fonction de hello stratégie de classement des événements.</span><span class="sxs-lookup"><span data-stu-id="24af1-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="24af1-124">Cela peut être touché par configuration hello du paramètre de la fenêtre de tolérance de panne de hello.</span><span class="sxs-lookup"><span data-stu-id="24af1-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="24af1-125">Erreurs de conversion de données</span><span class="sxs-lookup"><span data-stu-id="24af1-125">Data Conversion Errors</span></span> | <span data-ttu-id="24af1-126">Nombre d’erreurs de conversion de données générées par une tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="24af1-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="24af1-127">Erreurs d’exécution</span><span class="sxs-lookup"><span data-stu-id="24af1-127">Runtime Errors</span></span>         | <span data-ttu-id="24af1-128">Nombre total de Hello d’erreurs qui se produisent pendant l’exécution d’une tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="24af1-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="24af1-129">Événements d’entrée tardifs</span><span class="sxs-lookup"><span data-stu-id="24af1-129">Late Input Events</span></span>      | <span data-ttu-id="24af1-130">Nombre d’événements entrants au plus tard à partir de la source de hello qui soit ont été abandonnés ou leur horodatage a été ajusté, selon la configuration de stratégie de classement des événements hello du paramètre de fenêtre de tolérance d’arrivée tardive hello.</span><span class="sxs-lookup"><span data-stu-id="24af1-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="24af1-131">Requêtes de fonction</span><span class="sxs-lookup"><span data-stu-id="24af1-131">Function Requests</span></span>      | <span data-ttu-id="24af1-132">Nombre d’appels toohello fonction Azure Machine Learning (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="24af1-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="24af1-133">Requêtes de fonction ayant échoué</span><span class="sxs-lookup"><span data-stu-id="24af1-133">Failed Function Requests</span></span> | <span data-ttu-id="24af1-134">Nombre d’appels à la fonction Azure Machine Learning ayant échoué (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="24af1-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="24af1-135">Événements de fonction</span><span class="sxs-lookup"><span data-stu-id="24af1-135">Function Events</span></span>        | <span data-ttu-id="24af1-136">Nombre d’événements envoyés fonction d’Azure Machine Learning toohello (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="24af1-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="24af1-137">Octets des événements d’entrée</span><span class="sxs-lookup"><span data-stu-id="24af1-137">Input Event Bytes</span></span>      | <span data-ttu-id="24af1-138">Quantité de données reçues par la tâche de flux de données Analytique hello, en octets.</span><span class="sxs-lookup"><span data-stu-id="24af1-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="24af1-139">Cela peut être utilisé toovalidate que les événements sont envoyés toohello des sources d’entrée.</span><span class="sxs-lookup"><span data-stu-id="24af1-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="24af1-140">Personnalisation de surveillance Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="24af1-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="24af1-141">Vous pouvez ajuster le type hello du graphique, les métriques affichées et la période dans les paramètres de modifier le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="24af1-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="24af1-142">Pour plus d’informations, consultez [comment tooCustomize analyse](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="24af1-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Graphique représentant le temps de surveillance des requêtes](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="24af1-144">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="24af1-144">Get help</span></span>
<span data-ttu-id="24af1-145">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="24af1-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="24af1-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24af1-146">Next steps</span></span>
* [<span data-ttu-id="24af1-147">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="24af1-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="24af1-148">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24af1-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="24af1-149">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24af1-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="24af1-150">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24af1-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="24af1-151">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24af1-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

