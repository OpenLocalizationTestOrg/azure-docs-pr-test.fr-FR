---
title: "Présentation de la surveillance des travaux Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 13d96807a5591ec88deda19ea73cfedc07078433
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="0ed1e-104">Présentation de la surveillance des tâches Stream Analytics et des requêtes</span><span class="sxs-lookup"><span data-stu-id="0ed1e-104">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="0ed1e-105">Introduction : page de surveillance</span><span class="sxs-lookup"><span data-stu-id="0ed1e-105">Introduction: The monitor page</span></span>
<span data-ttu-id="0ed1e-106">Le portail Azure affiche les mesures de performances clés qui peuvent servir à surveiller et résoudre les problèmes affectant les performances de vos requêtes et de vos travaux.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="0ed1e-107">Pour voir ces métriques, accédez au travail Stream Analytics dont vous souhaitez consulter les métriques et affichez la section **Surveillance** dans la page Vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![Lien Surveillance](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="0ed1e-109">Une fenêtre s’affiche comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ed1e-109">The window will appear as shown:</span></span>

![Tableau de bord de surveillance des tâches](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="0ed1e-111">Mesures disponibles pour Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ed1e-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="0ed1e-112">Mesure</span><span class="sxs-lookup"><span data-stu-id="0ed1e-112">Metric</span></span>                 | <span data-ttu-id="0ed1e-113">Définition</span><span class="sxs-lookup"><span data-stu-id="0ed1e-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="0ed1e-114">Utilisation de % d’unités de diffusion</span><span class="sxs-lookup"><span data-stu-id="0ed1e-114">SU % Utilization</span></span>       | <span data-ttu-id="0ed1e-115">Utilisation des unités de diffusion affectées à une tâche à partir de l’onglet Mettre à l’échelle de la tâche.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="0ed1e-116">Si cet indicateur atteint 80 % ou plus, il est fort probable que le traitement des événements soit retardé ou arrêté.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="0ed1e-117">Événements d’entrée</span><span class="sxs-lookup"><span data-stu-id="0ed1e-117">Input Events</span></span>           | <span data-ttu-id="0ed1e-118">Quantité de données reçues par le travail Stream Analytics, en nombre d’événements.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-118">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="0ed1e-119">Cela permet de valider que les événements sont envoyés à la source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-119">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="0ed1e-120">Événements de sortie</span><span class="sxs-lookup"><span data-stu-id="0ed1e-120">Output Events</span></span>          | <span data-ttu-id="0ed1e-121">Quantité de données envoyées par le travail Stream Analytics à la cible de sortie, en nombre d’événements.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="0ed1e-122">Événements non ordonnés</span><span class="sxs-lookup"><span data-stu-id="0ed1e-122">Out-of-Order Events</span></span>    | <span data-ttu-id="0ed1e-123">Nombre d’événements reçus dans le désordre qui ont été supprimés ou dont l’horodatage a été réglé, en fonction de la stratégie de classement des événements.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="0ed1e-124">Cela peut être affecté par la configuration du paramètre de la plage de tolérance pour les événements en désordre.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="0ed1e-125">Erreurs de conversion de données</span><span class="sxs-lookup"><span data-stu-id="0ed1e-125">Data Conversion Errors</span></span> | <span data-ttu-id="0ed1e-126">Nombre d’erreurs de conversion de données générées par une tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="0ed1e-127">Erreurs d’exécution</span><span class="sxs-lookup"><span data-stu-id="0ed1e-127">Runtime Errors</span></span>         | <span data-ttu-id="0ed1e-128">Nombre total d’erreurs qui se produisent pendant l’exécution d’un travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-128">The total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="0ed1e-129">Événements d’entrée tardifs</span><span class="sxs-lookup"><span data-stu-id="0ed1e-129">Late Input Events</span></span>      | <span data-ttu-id="0ed1e-130">Nombre d’événements qui arrivent en retard de la source qui ont été supprimés ou dont l’horodatage a été réglé, en fonction de la configuration de la stratégie de classement des événements du paramètre de la plage de tolérance d’arrivée tardive.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="0ed1e-131">Requêtes de fonction</span><span class="sxs-lookup"><span data-stu-id="0ed1e-131">Function Requests</span></span>      | <span data-ttu-id="0ed1e-132">Nombre d’appels à la fonction Azure Machine Learning (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="0ed1e-132">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="0ed1e-133">Requêtes de fonction ayant échoué</span><span class="sxs-lookup"><span data-stu-id="0ed1e-133">Failed Function Requests</span></span> | <span data-ttu-id="0ed1e-134">Nombre d’appels à la fonction Azure Machine Learning ayant échoué (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="0ed1e-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="0ed1e-135">Événements de fonction</span><span class="sxs-lookup"><span data-stu-id="0ed1e-135">Function Events</span></span>        | <span data-ttu-id="0ed1e-136">Nombre d’événements envoyés à la fonction Azure Machine Learning (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="0ed1e-136">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="0ed1e-137">Octets des événements d’entrée</span><span class="sxs-lookup"><span data-stu-id="0ed1e-137">Input Event Bytes</span></span>      | <span data-ttu-id="0ed1e-138">Quantité de données reçues par le travail Stream Analytics, en octets.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-138">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="0ed1e-139">Cela permet de valider que les événements sont envoyés à la source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-139">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="0ed1e-140">Personnalisation de la surveillance dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0ed1e-140">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="0ed1e-141">Vous pouvez régler le type de graphique, les mesures affichées et la période dans les paramètres Modifier le graphique.</span><span class="sxs-lookup"><span data-stu-id="0ed1e-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="0ed1e-142">Pour plus d’informations, consultez [Personnalisation de la surveillance](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="0ed1e-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Graphique représentant le temps de surveillance des requêtes](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="0ed1e-144">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="0ed1e-144">Get help</span></span>
<span data-ttu-id="0ed1e-145">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0ed1e-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ed1e-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ed1e-146">Next steps</span></span>
* [<span data-ttu-id="0ed1e-147">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ed1e-147">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0ed1e-148">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ed1e-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0ed1e-149">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ed1e-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0ed1e-150">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ed1e-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0ed1e-151">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0ed1e-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

