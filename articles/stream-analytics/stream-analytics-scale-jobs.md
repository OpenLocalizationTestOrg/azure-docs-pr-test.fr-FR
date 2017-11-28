---
title: "Mettre à l’échelle des travaux Stream Analytics pour augmenter le débit | Microsoft Docs"
description: "Découvrez comment mettre à l’échelle des travaux Stream Analytics en configurant des partitions d’entrée, en réglant la définition de requête et en configurant les unités de diffusion en continu d’un travail."
keywords: "diffusion en continu de données, traitement de données de diffusion en continu, régler l’analyse"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="d3b80-104">Mettre à l’échelle des tâches Azure Stream Analytics pour augmenter le débit de traitement des données de flux</span><span class="sxs-lookup"><span data-stu-id="d3b80-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="d3b80-105">Cet article vous indique comment régler une requête Stream Analytics pour augmenter le débit des travaux Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3b80-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="d3b80-106">Vous allez découvrir comment mettre à l’échelle des travaux Stream Analytics en configurant des partitions d’entrée, en réglant la définition de la requête d’analyse et en calculant et en configurant les *unités de diffusion en continu* d’un travail.</span><span class="sxs-lookup"><span data-stu-id="d3b80-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="d3b80-107">Quelles sont les parties d’un travail Stream Analytics ?</span><span class="sxs-lookup"><span data-stu-id="d3b80-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="d3b80-108">La définition d’une tâche Stream Analytics se compose d’entrées, d’une requête et d’une sortie.</span><span class="sxs-lookup"><span data-stu-id="d3b80-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="d3b80-109">Les entrées correspondent à l’emplacement où le travail lit le flux de données.</span><span class="sxs-lookup"><span data-stu-id="d3b80-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="d3b80-110">La requête permet de transformer le flux d’entrée de données, et la sortie correspond à l’emplacement où le travail envoie ses résultats.</span><span class="sxs-lookup"><span data-stu-id="d3b80-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="d3b80-111">Un travail nécessite au moins une source d’entrée pour la diffusion de données en continu.</span><span class="sxs-lookup"><span data-stu-id="d3b80-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="d3b80-112">La source d’entrée de flux de données peut être stockée dans un concentrateur Azure Event Hub ou dans un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b80-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="d3b80-113">Pour plus d’informations, consultez [Présentation d’Azure Stream Analytics](stream-analytics-introduction.md) et [Prise en main de l’utilisation d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="d3b80-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="d3b80-114">Partitions dans les concentrateurs d’événements et le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d3b80-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="d3b80-115">La mise à l’échelle d’un travail Stream Analytics tire parti des partitions dans l’entrée ou la sortie.</span><span class="sxs-lookup"><span data-stu-id="d3b80-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="d3b80-116">Le partitionnement vous permet de répartir les données en sous-ensembles basés sur une clé de partition.</span><span class="sxs-lookup"><span data-stu-id="d3b80-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="d3b80-117">Un processus qui consomme les données (par exemple, un travail Stream Analytics) peut consommer et écrire différentes partitions en parallèle, ce qui augmente le débit.</span><span class="sxs-lookup"><span data-stu-id="d3b80-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="d3b80-118">Lorsque vous utilisez Stream Analytics, vous pouvez tirer parti du partitionnement dans les concentrateurs d’événements et dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d3b80-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="d3b80-119">Pour plus d’informations sur les partitions, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d3b80-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="d3b80-120">Vue d’ensemble des fonctionnalités des concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="d3b80-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="d3b80-121">Partitionnement des données</span><span class="sxs-lookup"><span data-stu-id="d3b80-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="d3b80-122">Unités de diffusion en continu (SU)</span><span class="sxs-lookup"><span data-stu-id="d3b80-122">Streaming units (SUs)</span></span>
<span data-ttu-id="d3b80-123">Les unités de diffusion en continu représentent les ressources et la puissance de calcul requises pour exécuter un travail Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3b80-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="d3b80-124">Ces unités permettent de décrire la capacité relative de traitement des événements basée sur une mesure mixte du processeur, de la mémoire et des taux de lecture et d’écriture.</span><span class="sxs-lookup"><span data-stu-id="d3b80-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="d3b80-125">Chaque unité SU correspond à un débit d’environ 1 Mo/s.</span><span class="sxs-lookup"><span data-stu-id="d3b80-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="d3b80-126">Le choix du nombre d’unités SU requises pour un travail particulier dépend de la configuration de la partition pour les entrées et de la requête définie pour le travail.</span><span class="sxs-lookup"><span data-stu-id="d3b80-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="d3b80-127">Vous pouvez sélectionner votre quota en unités SU pour un travail.</span><span class="sxs-lookup"><span data-stu-id="d3b80-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="d3b80-128">Par défaut, chaque abonnement Azure dispose d’un quota de 50 unités SU pour tous les travaux d’analyse d’une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="d3b80-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="d3b80-129">Pour augmenter ce quota d’unités SU pour vos abonnements, contactez le [Support Microsoft](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d3b80-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="d3b80-130">Valeurs valides pour les unités SU par travail : 1, 3, 6 et au-dessus par incréments de 6.</span><span class="sxs-lookup"><span data-stu-id="d3b80-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="d3b80-131">Travaux massivement parallèles</span><span class="sxs-lookup"><span data-stu-id="d3b80-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="d3b80-132">Un travail *massivement parallèle* est le scénario le plus évolutif d’Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3b80-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="d3b80-133">Elle permet de connecter une partition de l’entrée à une instance de la requête, puis de connecter celle-ci à une partition de la sortie.</span><span class="sxs-lookup"><span data-stu-id="d3b80-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="d3b80-134">Ce parallélisme comporte les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3b80-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="d3b80-135">Si votre logique de requête dépend de la clé qui est actuellement traitée par la même instance de requête, vous devez vous assurer que les événements atteignent la même partition de votre entrée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="d3b80-136">Pour les concentrateurs d’événements, cela signifie que les données d’événement doivent posséder la valeur **PartitionKey** définie.</span><span class="sxs-lookup"><span data-stu-id="d3b80-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="d3b80-137">Par ailleurs, vous pouvez utiliser des expéditeurs partitionnés.</span><span class="sxs-lookup"><span data-stu-id="d3b80-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="d3b80-138">Pour le stockage d’objets blob, cela signifie que les événements sont envoyés vers le même dossier de partition.</span><span class="sxs-lookup"><span data-stu-id="d3b80-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="d3b80-139">Si votre logique de requête ne requiert pas la même clé pour être traitée par la même instance de requête, vous pouvez ignorer cette condition.</span><span class="sxs-lookup"><span data-stu-id="d3b80-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="d3b80-140">Un exemple de cette logique serait une requête simple du type select/project/filter.</span><span class="sxs-lookup"><span data-stu-id="d3b80-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="d3b80-141">Une fois les données disposées dans l’entrée, vous devez vérifier que votre requête est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="d3b80-142">Vous devez utiliser **Partition By** à toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="d3b80-143">Les étapes multiples sont autorisées, mais elles doivent être partitionnées à l’aide de la même clé.</span><span class="sxs-lookup"><span data-stu-id="d3b80-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="d3b80-144">Pour le moment, la clé de partitionnement doit être définie sur **PartitionId** afin que le travail soit entièrement parallèle.</span><span class="sxs-lookup"><span data-stu-id="d3b80-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="d3b80-145">Actuellement, seuls les concentrateurs d’événements et le stockage d’objets blob prennent en charge les sorties partitionnées.</span><span class="sxs-lookup"><span data-stu-id="d3b80-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="d3b80-146">Pour la sortie de concentrateur Event Hub, vous devez configurer la clé de partition et la définir sur **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="d3b80-147">Pour la sortie de stockage d’objets blob, aucune action n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d3b80-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="d3b80-148">Le nombre de partitions d’entrée doit être égal à celui des partitions de sortie.</span><span class="sxs-lookup"><span data-stu-id="d3b80-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="d3b80-149">Actuellement, la sortie du stockage d’objets blob ne prend pas en charge les partitions,</span><span class="sxs-lookup"><span data-stu-id="d3b80-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="d3b80-150">mais cela ne pose pas de problèmes, car elle hérite du schéma de partitionnement de la requête en amont.</span><span class="sxs-lookup"><span data-stu-id="d3b80-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="d3b80-151">Voici des exemples de valeurs de partition qui permettent la création d’un travail entièrement parallèle :</span><span class="sxs-lookup"><span data-stu-id="d3b80-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="d3b80-152">8 partitions d’entrée de concentrateur Event Hub et 8 partitions de sortie de concentrateur Event Hub</span><span class="sxs-lookup"><span data-stu-id="d3b80-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="d3b80-153">8 partitions d’entrée de concentrateur Event Hub et une sortie de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="d3b80-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="d3b80-154">8 partitions d’entrée de stockage d’objets blob et une sortie de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="d3b80-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="d3b80-155">8 partitions d’entrée de stockage d’objets blob et 8 partitions de sortie de concentrateur Event Hub</span><span class="sxs-lookup"><span data-stu-id="d3b80-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="d3b80-156">Les sections ci-après présentent quelques exemples de parallélisme massif.</span><span class="sxs-lookup"><span data-stu-id="d3b80-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="d3b80-157">Requête simple</span><span class="sxs-lookup"><span data-stu-id="d3b80-157">Simple query</span></span>

* <span data-ttu-id="d3b80-158">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="d3b80-159">Sortie : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="d3b80-160">Requête :</span><span class="sxs-lookup"><span data-stu-id="d3b80-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="d3b80-161">Cette requête est un filtre simple.</span><span class="sxs-lookup"><span data-stu-id="d3b80-161">This query is a simple filter.</span></span> <span data-ttu-id="d3b80-162">Par conséquent, nous n’avons pas à nous préoccuper du partitionnement de l’entrée qui est envoyée au concentrateur Event Hub.</span><span class="sxs-lookup"><span data-stu-id="d3b80-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="d3b80-163">Notez que la requête inclut **Partition By PartitionId**. Elle répond donc à l’exigence n°2 indiquée précédemment.</span><span class="sxs-lookup"><span data-stu-id="d3b80-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="d3b80-164">Pour la sortie, nous devons configurer la sortie de concentrateur Event Hub dans le travail afin que la clé de partition soit définie sur **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="d3b80-165">La dernière vérification consiste à s’assurer que le nombre de partitions d’entrée est égal au nombre de partitions de sortie.</span><span class="sxs-lookup"><span data-stu-id="d3b80-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="d3b80-166">Requête avec clé de regroupement</span><span class="sxs-lookup"><span data-stu-id="d3b80-166">Query with a grouping key</span></span>

* <span data-ttu-id="d3b80-167">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="d3b80-168">Sortie : stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="d3b80-168">Output: Blob storage</span></span>

<span data-ttu-id="d3b80-169">Requête :</span><span class="sxs-lookup"><span data-stu-id="d3b80-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="d3b80-170">Cette requête comporte une clé de regroupement.</span><span class="sxs-lookup"><span data-stu-id="d3b80-170">This query has a grouping key.</span></span> <span data-ttu-id="d3b80-171">Par conséquent, la même clé doit être traitée par la même instance de la requête, ce qui signifie que les événements doivent être envoyés au concentrateur Event Hub de manière partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="d3b80-172">Mais quelle clé convient-il d’utiliser ?</span><span class="sxs-lookup"><span data-stu-id="d3b80-172">But which key should be used?</span></span> <span data-ttu-id="d3b80-173">**PartitionId** est un concept de logique de travail.</span><span class="sxs-lookup"><span data-stu-id="d3b80-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="d3b80-174">Comme la clé qui nous importe réellement est **TollBoothId**, la valeur **PartitionKey** des données d’événement doit être **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="d3b80-175">Pour ce faire, nous définissons **Partition By** sur **PartitionId** dans la requête.</span><span class="sxs-lookup"><span data-stu-id="d3b80-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="d3b80-176">Étant donné que la sortie est un stockage d’objets blob, nous n’avons pas à nous soucier de la configuration d’une valeur de clé de partition, conformément à l’exigence n°4.</span><span class="sxs-lookup"><span data-stu-id="d3b80-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="d3b80-177">Requête à plusieurs étapes avec clé de regroupement</span><span class="sxs-lookup"><span data-stu-id="d3b80-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="d3b80-178">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="d3b80-179">Sortie : instance de concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="d3b80-180">Requête :</span><span class="sxs-lookup"><span data-stu-id="d3b80-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="d3b80-181">Cette requête contient une clé de regroupement. La même clé doit donc être traitée par la même instance de la requête.</span><span class="sxs-lookup"><span data-stu-id="d3b80-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="d3b80-182">Nous pouvons utiliser la même stratégie que dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="d3b80-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="d3b80-183">Dans ce cas, la requête comporte plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="d3b80-184">Chaque étape inclut-elle **Partition By PartitionId** ?</span><span class="sxs-lookup"><span data-stu-id="d3b80-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="d3b80-185">Oui, la requête répond à l’exigence n°3.</span><span class="sxs-lookup"><span data-stu-id="d3b80-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="d3b80-186">Pour la sortie, nous devons définir la clé de partition sur **PartitionId**, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="d3b80-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="d3b80-187">Nous pouvons également observer que la sortie dispose du même nombre de partitions que l’entrée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="d3b80-188">Exemples de scénarios qui n’impliquent *pas* un parallélisme massif</span><span class="sxs-lookup"><span data-stu-id="d3b80-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="d3b80-189">Dans la section précédente, nous vous avons présenté certains scénarios impliquant un parallélisme massif.</span><span class="sxs-lookup"><span data-stu-id="d3b80-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="d3b80-190">Dans cette section, nous étudions des cas dans lesquels toutes les exigences ne sont pas remplies pour un parallélisme massif.</span><span class="sxs-lookup"><span data-stu-id="d3b80-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="d3b80-191">Nombre de partitions d’entrée et de sortie différent</span><span class="sxs-lookup"><span data-stu-id="d3b80-191">Mismatched partition count</span></span>
* <span data-ttu-id="d3b80-192">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="d3b80-193">Sortie : concentrateur Event Hub avec 32 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="d3b80-194">Dans ce cas, le type de requête importe peu.</span><span class="sxs-lookup"><span data-stu-id="d3b80-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="d3b80-195">Si le nombre de partitions d’entrée ne correspond pas au nombre de partitions de sortie, la topologie n’est pas massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="d3b80-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="d3b80-196">Sortie ne correspondant pas à un concentrateur Event Hub ni à un stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="d3b80-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="d3b80-197">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="d3b80-198">Sortie : Power BI</span><span class="sxs-lookup"><span data-stu-id="d3b80-198">Output: PowerBI</span></span>

<span data-ttu-id="d3b80-199">Pour le moment, la sortie Power BI ne prend pas en charge le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="d3b80-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="d3b80-200">Par conséquent, ce scénario n’est pas de type massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="d3b80-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="d3b80-201">Requête à plusieurs étapes avec différentes valeurs Partition By</span><span class="sxs-lookup"><span data-stu-id="d3b80-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="d3b80-202">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="d3b80-203">Sortie : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="d3b80-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="d3b80-204">Requête :</span><span class="sxs-lookup"><span data-stu-id="d3b80-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="d3b80-205">Comme vous pouvez le voir, la deuxième étape utilise **TollBoothId** comme clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="d3b80-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="d3b80-206">Cette étape n’est pas la même que la première. Nous devons donc apporter quelques modifications.</span><span class="sxs-lookup"><span data-stu-id="d3b80-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="d3b80-207">Les exemples précédents décrivent des travaux Stream Analytics qui respectent (ou pas) une topologie de type massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="d3b80-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="d3b80-208">S’ils la respectent, ils présentent alors le potentiel pour une mise à l’échelle maximale.</span><span class="sxs-lookup"><span data-stu-id="d3b80-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="d3b80-209">Pour les travaux qui ne correspondent pas à l’un de ces profils, des conseils de mise à l’échelle seront disponibles dans les futures mises à jour.</span><span class="sxs-lookup"><span data-stu-id="d3b80-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="d3b80-210">Pour le moment, suivez les instructions générales indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="d3b80-211">Calcul du nombre maximum d'unités de diffusion en continu pour un travail</span><span class="sxs-lookup"><span data-stu-id="d3b80-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="d3b80-212">Le nombre total d'unités de diffusion en continu qui peut être utilisé par un travail Stream Analytics varie selon le nombre d'étapes de la requête définie pour le travail et le nombre de partitions pour chaque étape.</span><span class="sxs-lookup"><span data-stu-id="d3b80-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="d3b80-213">Étapes dans une requête</span><span class="sxs-lookup"><span data-stu-id="d3b80-213">Steps in a query</span></span>
<span data-ttu-id="d3b80-214">Une requête peut avoir une ou plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-214">A query can have one or many steps.</span></span> <span data-ttu-id="d3b80-215">Chaque étape est une sous-requête définie par le mot-clé **WITH**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="d3b80-216">La requête qui se trouve en dehors du mot-clé **WITH** (une seule requête) est également comptabilisée comme une étape, par exemple, l’instruction **SELECT** dans la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="d3b80-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="d3b80-217">Cette requête compte deux étapes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="d3b80-218">Cette requête est approfondie plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d3b80-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="d3b80-219">Partitionnement d'une étape</span><span class="sxs-lookup"><span data-stu-id="d3b80-219">Partition a step</span></span>
<span data-ttu-id="d3b80-220">Les conditions suivantes doivent être respectées pour procéder au partitionnement d'une étape :</span><span class="sxs-lookup"><span data-stu-id="d3b80-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="d3b80-221">La source d'entrée doit être partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="d3b80-222">L’instruction **SELECT** de la requête doit lire à partir d’une source d’entrée partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="d3b80-223">La requête de l’étape doit contenir le mot-clé **Partition By**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="d3b80-224">Lorsqu’une requête est partitionnée, les événements d’entrée sont traités et agrégés dans des groupes de partition distincts, et les événements de sortie sont générés pour chacun des groupes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="d3b80-225">Si vous souhaitez procéder à un agrégat combiné, vous devez créer une deuxième étape non partitionnée à agréger.</span><span class="sxs-lookup"><span data-stu-id="d3b80-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="d3b80-226">Calcul des unités de diffusion en continu maximum pour un travail</span><span class="sxs-lookup"><span data-stu-id="d3b80-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="d3b80-227">Toutes les étapes non partitionnées ensemble peuvent être mises à l’échelle jusqu’à atteindre six unités SU par travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3b80-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="d3b80-228">Pour ajouter des unités SU, une étape doit être partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="d3b80-229">Chaque partition peut comporter six unités SU.</span><span class="sxs-lookup"><span data-stu-id="d3b80-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="d3b80-230">Requête</span><span class="sxs-lookup"><span data-stu-id="d3b80-230">Query</span></span></th><th><span data-ttu-id="d3b80-231">Nombre d’unités SU maximal pour le travail</span><span class="sxs-lookup"><span data-stu-id="d3b80-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="d3b80-232">La requête contient une étape.</span><span class="sxs-lookup"><span data-stu-id="d3b80-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="d3b80-233">L'étape n'est pas partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="d3b80-234">6</span><span class="sxs-lookup"><span data-stu-id="d3b80-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="d3b80-235">Le flux de données d'entrée est partitionné par 3.</span><span class="sxs-lookup"><span data-stu-id="d3b80-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="d3b80-236">La requête contient une étape.</span><span class="sxs-lookup"><span data-stu-id="d3b80-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="d3b80-237">L'étape est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="d3b80-238">18</span><span class="sxs-lookup"><span data-stu-id="d3b80-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="d3b80-239">La requête contient 2 étapes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="d3b80-240">Aucune des étapes n'est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="d3b80-241">6</span><span class="sxs-lookup"><span data-stu-id="d3b80-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="d3b80-242">Le flux de données d'entrée est partitionné par 3.</span><span class="sxs-lookup"><span data-stu-id="d3b80-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="d3b80-243">La requête contient 2 étapes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-243">The query contains two steps.</span></span> <span data-ttu-id="d3b80-244">L'étape d'entrée est partitionnée et la deuxième étape ne l'est pas.</span><span class="sxs-lookup"><span data-stu-id="d3b80-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="d3b80-245">L’instruction <strong>SELECT</strong> lit dans l’entrée partitionnée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="d3b80-246">24 (18 pour les étapes partitionnées + 6 pour les étapes non partitionnées)</span><span class="sxs-lookup"><span data-stu-id="d3b80-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="d3b80-247">Exemples de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="d3b80-247">Examples of scaling</span></span>

<span data-ttu-id="d3b80-248">La requête suivante calcule le nombre de voitures, dans une fenêtre de trois minutes, qui traversent un poste de péage pourvu de trois cabines de péage.</span><span class="sxs-lookup"><span data-stu-id="d3b80-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="d3b80-249">Cette requête peut être mise à l’échelle jusqu’à six unités SU.</span><span class="sxs-lookup"><span data-stu-id="d3b80-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="d3b80-250">Pour utiliser plus d’unités SU pour la requête, le flux de données d’entrée et la requête doivent être partitionnés.</span><span class="sxs-lookup"><span data-stu-id="d3b80-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="d3b80-251">Comme la partition de flux de données est définie sur 3, la requête modifiée suivante peut être mise à l’échelle jusqu’à compter 18 unités SU :</span><span class="sxs-lookup"><span data-stu-id="d3b80-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="d3b80-252">Lorsqu'une requête est partitionnée, les événements d'entrée sont traités et agrégées dans des groupes de partition distincts.</span><span class="sxs-lookup"><span data-stu-id="d3b80-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="d3b80-253">Les événements de sortie sont également générés pour chacun des groupes.</span><span class="sxs-lookup"><span data-stu-id="d3b80-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="d3b80-254">Le partitionnement peut provoquer des résultats inattendus si le champ **GROUP BY** n’est pas la clé de partition dans le flux de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="d3b80-255">Par exemple, dans la requête précédente, le champ **TollBoothId** n’est pas la clé de partition **d’Input1**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="d3b80-256">Le résultat est le suivant : les données de la cabine de péage « TollBooth 1 » peuvent être réparties dans plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="d3b80-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="d3b80-257">Chaque partition **Input1** est traitée séparément par Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d3b80-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="d3b80-258">En conséquence, plusieurs enregistrements du nombre de voitures pour la même cabine de péage sont créés dans la même fenêtre bascule.</span><span class="sxs-lookup"><span data-stu-id="d3b80-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="d3b80-259">Si la clé de partition d’entrée ne peut pas être modifiée, ce problème peut être résolu en ajoutant une étape non partitionnée, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d3b80-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="d3b80-260">Cette requête peut être mise à l’échelle jusqu’à comporter 24 unités SU.</span><span class="sxs-lookup"><span data-stu-id="d3b80-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="d3b80-261">Si vous joignez deux flux de données, assurez-vous qu’ils sont partitionnés par la clé de partition de la colonne que vous utilisez pour créer les jointures.</span><span class="sxs-lookup"><span data-stu-id="d3b80-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="d3b80-262">Assurez-vous également d’avoir le même nombre de partitions dans les deux flux de données.</span><span class="sxs-lookup"><span data-stu-id="d3b80-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="d3b80-263">Configurer des unités de diffusion en continu Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3b80-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="d3b80-264">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3b80-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d3b80-265">Dans la liste des ressources, recherchez le travail Stream Analytics que vous souhaitez mettre à l’échelle, puis ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="d3b80-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="d3b80-266">Dans le panneau du travail, sous **Configurer**, cliquez sur **Échelle**.</span><span class="sxs-lookup"><span data-stu-id="d3b80-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Configuration d’un travail Stream Analytics sur le portail Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="d3b80-268">Définissez les unités SU pour le travail à l’aide du curseur.</span><span class="sxs-lookup"><span data-stu-id="d3b80-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="d3b80-269">Notez que vous êtes limité à des paramètres d’unité SU spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d3b80-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="d3b80-270">Surveillance des performances du travail</span><span class="sxs-lookup"><span data-stu-id="d3b80-270">Monitor job performance</span></span>
<span data-ttu-id="d3b80-271">À l’aide du portail Azure, vous pouvez suivre le débit d’un travail :</span><span class="sxs-lookup"><span data-stu-id="d3b80-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Surveillance des travaux Azure Stream Analytics][img.stream.analytics.monitor.job]

<span data-ttu-id="d3b80-273">Calculez le débit prévu pour la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="d3b80-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="d3b80-274">Si le débit est plus faible que prévu, paramétrez la partition d’entrée ainsi que la requête, puis ajoutez des unités SU à votre travail.</span><span class="sxs-lookup"><span data-stu-id="d3b80-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="d3b80-275">Visualiser le débit Stream Analytics à l’échelle : scénario Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="d3b80-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="d3b80-276">Pour vous aider à comprendre comment les travaux Stream Analytics sont mis à l’échelle, nous avons effectué une expérience basée sur l’entrée d’un appareil Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d3b80-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="d3b80-277">Cette expérience nous permet d’observer l’effet de plusieurs unités SU et partitions sur le débit.</span><span class="sxs-lookup"><span data-stu-id="d3b80-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="d3b80-278">Dans ce scénario, l’appareil envoie des données de capteur (clients) à un concentrateur Event Hub.</span><span class="sxs-lookup"><span data-stu-id="d3b80-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="d3b80-279">Stream Analytics traite les données et envoie une alerte ou des statistiques en tant que sortie à un autre concentrateur Event Hub.</span><span class="sxs-lookup"><span data-stu-id="d3b80-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="d3b80-280">Le client envoie des données de capteur au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d3b80-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="d3b80-281">La sortie des données est également au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d3b80-281">The data output is also in JSON format.</span></span> <span data-ttu-id="d3b80-282">Voici à quoi ressemblent les données :</span><span class="sxs-lookup"><span data-stu-id="d3b80-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="d3b80-283">La requête suivante permet d’envoyer une alerte quand lorsqu’une lumière est éteinte :</span><span class="sxs-lookup"><span data-stu-id="d3b80-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="d3b80-284">Mesurer le débit</span><span class="sxs-lookup"><span data-stu-id="d3b80-284">Measure throughput</span></span>

<span data-ttu-id="d3b80-285">Dans ce contexte, le débit correspond à la quantité de données d’entrée traitées par Stream Analytics au cours d’une durée fixe.</span><span class="sxs-lookup"><span data-stu-id="d3b80-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="d3b80-286">(Nous avons mesuré le débit pendant 10 minutes.) Pour obtenir le meilleur débit de traitement pour les données d’entrée, l’entrée de flux de données et la requête ont été partitionnées.</span><span class="sxs-lookup"><span data-stu-id="d3b80-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="d3b80-287">Nous avons inclus **COUNT()** dans la requête pour mesurer le nombre d’événements d’entrée traités.</span><span class="sxs-lookup"><span data-stu-id="d3b80-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="d3b80-288">Pour vous assurer que le travail n’attende pas simplement les événements d’entrée, chaque partition du concentrateur Event Hub d’entrée a été préchargée avec environ 300 Mo de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d3b80-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="d3b80-289">Le tableau suivant montre les résultats que nous avons observés lorsque nous avons augmenté le nombre d’unités SU et le nombre de partitions correspondant dans les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="d3b80-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="d3b80-290">Partitions d'entrée</span><span class="sxs-lookup"><span data-stu-id="d3b80-290">Input Partitions</span></span></th><th><span data-ttu-id="d3b80-291">Partitions de sortie</span><span class="sxs-lookup"><span data-stu-id="d3b80-291">Output Partitions</span></span></th><th><span data-ttu-id="d3b80-292">Unités de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="d3b80-292">Streaming Units</span></span></th><th><span data-ttu-id="d3b80-293">Débit soutenu</span><span class="sxs-lookup"><span data-stu-id="d3b80-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="d3b80-294">12</span><span class="sxs-lookup"><span data-stu-id="d3b80-294">12</span></span></td>
<td><span data-ttu-id="d3b80-295">12</span><span class="sxs-lookup"><span data-stu-id="d3b80-295">12</span></span></td>
<td><span data-ttu-id="d3b80-296">6</span><span class="sxs-lookup"><span data-stu-id="d3b80-296">6</span></span></td>
<td><span data-ttu-id="d3b80-297">4,06 Mo/s</span><span class="sxs-lookup"><span data-stu-id="d3b80-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="d3b80-298">12</span><span class="sxs-lookup"><span data-stu-id="d3b80-298">12</span></span></td>
<td><span data-ttu-id="d3b80-299">12</span><span class="sxs-lookup"><span data-stu-id="d3b80-299">12</span></span></td>
<td><span data-ttu-id="d3b80-300">12</span><span class="sxs-lookup"><span data-stu-id="d3b80-300">12</span></span></td>
<td><span data-ttu-id="d3b80-301">8,06 Mo/s</span><span class="sxs-lookup"><span data-stu-id="d3b80-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="d3b80-302">48</span><span class="sxs-lookup"><span data-stu-id="d3b80-302">48</span></span></td>
<td><span data-ttu-id="d3b80-303">48</span><span class="sxs-lookup"><span data-stu-id="d3b80-303">48</span></span></td>
<td><span data-ttu-id="d3b80-304">48</span><span class="sxs-lookup"><span data-stu-id="d3b80-304">48</span></span></td>
<td><span data-ttu-id="d3b80-305">38,32 Mo/s</span><span class="sxs-lookup"><span data-stu-id="d3b80-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="d3b80-306">192</span><span class="sxs-lookup"><span data-stu-id="d3b80-306">192</span></span></td>
<td><span data-ttu-id="d3b80-307">192</span><span class="sxs-lookup"><span data-stu-id="d3b80-307">192</span></span></td>
<td><span data-ttu-id="d3b80-308">192</span><span class="sxs-lookup"><span data-stu-id="d3b80-308">192</span></span></td>
<td><span data-ttu-id="d3b80-309">172,67 Mo/s</span><span class="sxs-lookup"><span data-stu-id="d3b80-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="d3b80-310">480</span><span class="sxs-lookup"><span data-stu-id="d3b80-310">480</span></span></td>
<td><span data-ttu-id="d3b80-311">480</span><span class="sxs-lookup"><span data-stu-id="d3b80-311">480</span></span></td>
<td><span data-ttu-id="d3b80-312">480</span><span class="sxs-lookup"><span data-stu-id="d3b80-312">480</span></span></td>
<td><span data-ttu-id="d3b80-313">454,27 Mo/s</span><span class="sxs-lookup"><span data-stu-id="d3b80-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="d3b80-314">720</span><span class="sxs-lookup"><span data-stu-id="d3b80-314">720</span></span></td>
<td><span data-ttu-id="d3b80-315">720</span><span class="sxs-lookup"><span data-stu-id="d3b80-315">720</span></span></td>
<td><span data-ttu-id="d3b80-316">720</span><span class="sxs-lookup"><span data-stu-id="d3b80-316">720</span></span></td>
<td><span data-ttu-id="d3b80-317">609,69 Mo/s</span><span class="sxs-lookup"><span data-stu-id="d3b80-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="d3b80-318">Et le graphique suivant présente une visualisation de la relation entre les unités SU et le débit.</span><span class="sxs-lookup"><span data-stu-id="d3b80-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="d3b80-320">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="d3b80-320">Get help</span></span>
<span data-ttu-id="d3b80-321">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="d3b80-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3b80-322">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3b80-322">Next steps</span></span>
* [<span data-ttu-id="d3b80-323">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3b80-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d3b80-324">Prise en main d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3b80-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d3b80-325">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3b80-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d3b80-326">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3b80-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

