---
title: "débit de tooincrease travaux aaaScale flux Analytique | Documents Microsoft"
description: "Découvrez comment tooscale les travaux de flux de données Analytique par la configuration de partitions d’entrée, le paramétrage de la définition de requête hello et définition de la tâche unités de diffusion en continu."
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
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="4b888-104">Débit en échelle Analytique de flux de données Azure travaux tooincrease flux le traitement des données</span><span class="sxs-lookup"><span data-stu-id="4b888-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="4b888-105">Cet article vous explique comment tootune un Analytique de flux de requête tooincrease le débit pour les travaux de l’Analytique de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="4b888-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="4b888-106">Vous apprendrez comment tooscale Analytique de flux de travaux en configurant les partitions d’entrée, définition de la requête analytique de hello paramétrage et du calcul et la définition de la tâche *unités de diffusion en continu* (SUs).</span><span class="sxs-lookup"><span data-stu-id="4b888-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="4b888-107">Quelles sont les parties hello d’une tâche de flux de données Analytique ?</span><span class="sxs-lookup"><span data-stu-id="4b888-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="4b888-108">La définition d’une tâche Stream Analytics se compose d’entrées, d’une requête et d’une sortie.</span><span class="sxs-lookup"><span data-stu-id="4b888-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="4b888-109">Les entrées sont où le travail de hello lit les flux de données de hello à partir de.</span><span class="sxs-lookup"><span data-stu-id="4b888-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="4b888-110">flux d’entrée des données hello tootransform utilisé est Hello requête et sortie de la hello est où le travail de hello envoie les résultats de la tâche hello pour.</span><span class="sxs-lookup"><span data-stu-id="4b888-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="4b888-111">Un travail nécessite au moins une source d’entrée pour la diffusion de données en continu.</span><span class="sxs-lookup"><span data-stu-id="4b888-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="4b888-112">Hello source d’entrée de flux de données peut être stockée dans un concentrateur d’événements Azure ou dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4b888-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="4b888-113">Pour plus d’informations, consultez [tooAzure de présentation des flux de données Analytique](stream-analytics-introduction.md) et [prise en main Azure flux Analytique](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="4b888-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="4b888-114">Partitions dans les concentrateurs d’événements et le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4b888-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="4b888-115">Mise à l’échelle d’une tâche de flux de données Analytique bénéficie de partitions Bonjour d’entrée ou sortie.</span><span class="sxs-lookup"><span data-stu-id="4b888-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="4b888-116">Le partitionnement vous permet de répartir les données en sous-ensembles basés sur une clé de partition.</span><span class="sxs-lookup"><span data-stu-id="4b888-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="4b888-117">Un processus qui consomme des données hello (par exemple, une tâche Analytique de diffusion en continu) peut consommer et écrire des différentes partitions en parallèle, ce qui augmente le débit.</span><span class="sxs-lookup"><span data-stu-id="4b888-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="4b888-118">Lorsque vous utilisez Stream Analytics, vous pouvez tirer parti du partitionnement dans les concentrateurs d’événements et dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="4b888-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="4b888-119">Pour plus d’informations sur les partitions, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="4b888-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="4b888-120">Vue d’ensemble des fonctionnalités des concentrateurs d’événements</span><span class="sxs-lookup"><span data-stu-id="4b888-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="4b888-121">Partitionnement des données</span><span class="sxs-lookup"><span data-stu-id="4b888-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="4b888-122">Unités de diffusion en continu (SU)</span><span class="sxs-lookup"><span data-stu-id="4b888-122">Streaming units (SUs)</span></span>
<span data-ttu-id="4b888-123">Diffusion en continu des ressources de hello représentent des unités (SUs) et calcul d’alimentation qui sont requis dans l’ordre de tooexecute un travail Azure Stream Analytique.</span><span class="sxs-lookup"><span data-stu-id="4b888-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="4b888-124">SUs fournissent un événement relatif hello toodescribe moyen en fonction de la mesure du processeur, mémoire, la capacité de traitement et lire et écrire des taux.</span><span class="sxs-lookup"><span data-stu-id="4b888-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="4b888-125">Chaque appel à SU correspond tooroughly débit de 1 Mo par seconde.</span><span class="sxs-lookup"><span data-stu-id="4b888-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="4b888-126">En choisissant SUs combien sont requis pour une tâche particulière dépend de la configuration de partitions hello pour les entrées de hello et de requête hello définis pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="4b888-127">Vous pouvez sélectionner des quotas tooyour SUS d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="4b888-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="4b888-128">Par défaut, chaque abonnement Azure a un quota de configuration SUs too50 pour tous les travaux d’analytique hello dans une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="4b888-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="4b888-129">tooincrease SUs pour vos abonnements au-delà de ce quota, contactez [Support technique de Microsoft](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4b888-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="4b888-130">Valeurs valides pour les unités SU par travail : 1, 3, 6 et au-dessus par incréments de 6.</span><span class="sxs-lookup"><span data-stu-id="4b888-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="4b888-131">Travaux massivement parallèles</span><span class="sxs-lookup"><span data-stu-id="4b888-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="4b888-132">Un *embarrassingly parallel* travail est scénario plus évolutive de hello, nous disposons d’Analytique de flux de données Azure.</span><span class="sxs-lookup"><span data-stu-id="4b888-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="4b888-133">Il connecte une partition d’instance d’entrée tooone de hello de partition de tooone hello requête de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="4b888-134">Ce parallélisme a hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="4b888-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="4b888-135">Si votre logique de requête dépend hello même clé en cours de traitement par hello même instance de requête, vous devez vous assurer que les événements hello accédez toohello même partition de votre entrée.</span><span class="sxs-lookup"><span data-stu-id="4b888-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="4b888-136">Pour les concentrateurs d’événements, cela signifie que les données d’événement hello doivent avoir hello **PartitionKey** ensemble de valeurs.</span><span class="sxs-lookup"><span data-stu-id="4b888-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="4b888-137">Par ailleurs, vous pouvez utiliser des expéditeurs partitionnés.</span><span class="sxs-lookup"><span data-stu-id="4b888-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="4b888-138">Pour le stockage d’objets blob, cela signifie que les événements de hello sont envoyés toohello même dossier de la partition.</span><span class="sxs-lookup"><span data-stu-id="4b888-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="4b888-139">Si votre logique de requête ne nécessite pas de hello même clé toobe traité par hello même instance de requête, vous pouvez ignorer cette exigence.</span><span class="sxs-lookup"><span data-stu-id="4b888-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="4b888-140">Un exemple de cette logique serait une requête simple du type select/project/filter.</span><span class="sxs-lookup"><span data-stu-id="4b888-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="4b888-141">Une fois que les données de salutation sont disposées côté hello d’entrée, il se peut que vous devez vous assurer que votre requête est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="4b888-142">Vous devez toouse **Partition By** dans toutes les étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="4b888-143">Plusieurs étapes sont autorisés, mais ils doivent être partitionnées par hello même clé.</span><span class="sxs-lookup"><span data-stu-id="4b888-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="4b888-144">Actuellement, hello clé de partitionnement doit être défini trop**PartitionId** par ordre de hello toobe de travail entièrement parallèle.</span><span class="sxs-lookup"><span data-stu-id="4b888-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="4b888-145">Actuellement, seuls les concentrateurs d’événements et le stockage d’objets blob prennent en charge les sorties partitionnées.</span><span class="sxs-lookup"><span data-stu-id="4b888-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="4b888-146">Pour la sortie de concentrateur d’événements, vous devez configurer toobe clé de partition hello **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="4b888-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="4b888-147">Pour la sortie de stockage d’objets blob, vous n’avez toodo quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="4b888-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="4b888-148">nombre de Hello de partitions d’entrée doit être égal nombre hello de partitions de sortie.</span><span class="sxs-lookup"><span data-stu-id="4b888-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="4b888-149">Actuellement, la sortie du stockage d’objets blob ne prend pas en charge les partitions,</span><span class="sxs-lookup"><span data-stu-id="4b888-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="4b888-150">Mais c’est OK, parce qu’elle hérite hello schéma de requête en amont de hello de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="4b888-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="4b888-151">Voici des exemples de valeurs de partition qui permettent la création d’un travail entièrement parallèle :</span><span class="sxs-lookup"><span data-stu-id="4b888-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="4b888-152">8 partitions d’entrée de concentrateur Event Hub et 8 partitions de sortie de concentrateur Event Hub</span><span class="sxs-lookup"><span data-stu-id="4b888-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="4b888-153">8 partitions d’entrée de concentrateur Event Hub et une sortie de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="4b888-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="4b888-154">8 partitions d’entrée de stockage d’objets blob et une sortie de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="4b888-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="4b888-155">8 partitions d’entrée de stockage d’objets blob et 8 partitions de sortie de concentrateur Event Hub</span><span class="sxs-lookup"><span data-stu-id="4b888-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="4b888-156">Hello sections suivantes présentent des exemples de scénarios qui sont excessivement parallèles.</span><span class="sxs-lookup"><span data-stu-id="4b888-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="4b888-157">Requête simple</span><span class="sxs-lookup"><span data-stu-id="4b888-157">Simple query</span></span>

* <span data-ttu-id="4b888-158">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="4b888-159">Sortie : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="4b888-160">Requête :</span><span class="sxs-lookup"><span data-stu-id="4b888-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="4b888-161">Cette requête est un filtre simple.</span><span class="sxs-lookup"><span data-stu-id="4b888-161">This query is a simple filter.</span></span> <span data-ttu-id="4b888-162">Par conséquent, nous n’avez pas besoin tooworry sur le partitionnement d’entrée de hello est envoyée toohello concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="4b888-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="4b888-163">Notez cette requête hello inclut **Partition par PartitionId**, donc il répond à un besoin #2 précédemment.</span><span class="sxs-lookup"><span data-stu-id="4b888-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="4b888-164">Pour une sortie hello, nous avons besoin de sortie du hub d’événements tooconfigure hello dans hello travail toohave hello partition jeu de clés trop**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="4b888-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="4b888-165">Une dernière vérification est toomake assurer que le nombre hello de partitions d’entrée est nombre égal toohello de partitions de sortie.</span><span class="sxs-lookup"><span data-stu-id="4b888-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="4b888-166">Requête avec clé de regroupement</span><span class="sxs-lookup"><span data-stu-id="4b888-166">Query with a grouping key</span></span>

* <span data-ttu-id="4b888-167">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="4b888-168">Sortie : stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="4b888-168">Output: Blob storage</span></span>

<span data-ttu-id="4b888-169">Requête :</span><span class="sxs-lookup"><span data-stu-id="4b888-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="4b888-170">Cette requête comporte une clé de regroupement.</span><span class="sxs-lookup"><span data-stu-id="4b888-170">This query has a grouping key.</span></span> <span data-ttu-id="4b888-171">Par conséquent, hello même clé besoins toobe traité par hello même requête d’instance, ce qui signifie que les événements doivent être envoyés toohello concentrateur d’événements de manière partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="4b888-172">Mais quelle clé convient-il d’utiliser ?</span><span class="sxs-lookup"><span data-stu-id="4b888-172">But which key should be used?</span></span> <span data-ttu-id="4b888-173">**PartitionId** est un concept de logique de travail.</span><span class="sxs-lookup"><span data-stu-id="4b888-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="4b888-174">clé Hello nous intéressent réellement est **TollBoothId**, donc hello **PartitionKey** valeur hello des données d’événement doit être **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="4b888-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="4b888-175">Cela, nous dans les requêtes hello en définissant **Partition By** trop**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="4b888-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="4b888-176">Étant donné que la sortie de hello est le stockage d’objets blob, nous n’avez pas besoin tooworry sur la configuration d’une valeur de clé de partition, conformément à la spécification #4.</span><span class="sxs-lookup"><span data-stu-id="4b888-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="4b888-177">Requête à plusieurs étapes avec clé de regroupement</span><span class="sxs-lookup"><span data-stu-id="4b888-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="4b888-178">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="4b888-179">Sortie : instance de concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="4b888-180">Requête :</span><span class="sxs-lookup"><span data-stu-id="4b888-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="4b888-181">Cette requête comporte une clé de regroupement, par conséquent, hello même clé besoins toobe traité par hello même instance de requête.</span><span class="sxs-lookup"><span data-stu-id="4b888-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="4b888-182">Nous pouvons utiliser hello même stratégie dans l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="4b888-183">Dans ce cas, la requête de hello comprend plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="4b888-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="4b888-184">Chaque étape inclut-elle **Partition By PartitionId** ?</span><span class="sxs-lookup"><span data-stu-id="4b888-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="4b888-185">Oui, afin de la requête de hello répond à un besoin #3.</span><span class="sxs-lookup"><span data-stu-id="4b888-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="4b888-186">Pour une sortie hello, nous devons trop clé de partition hello tooset**PartitionId**, comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="4b888-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="4b888-187">Nous pouvons également voir qu’il a hello même nombre de partitions en tant qu’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="4b888-188">Exemples de scénarios qui n’impliquent *pas* un parallélisme massif</span><span class="sxs-lookup"><span data-stu-id="4b888-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="4b888-189">Dans la section précédente de hello, nous vous avons montré certains scénarios excessivement parallèles.</span><span class="sxs-lookup"><span data-stu-id="4b888-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="4b888-190">Dans cette section, nous traitent de scénarios qui ne répondent pas aux hello toutes les exigences toobe embarrassingly parallel.</span><span class="sxs-lookup"><span data-stu-id="4b888-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="4b888-191">Nombre de partitions d’entrée et de sortie différent</span><span class="sxs-lookup"><span data-stu-id="4b888-191">Mismatched partition count</span></span>
* <span data-ttu-id="4b888-192">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="4b888-193">Sortie : concentrateur Event Hub avec 32 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="4b888-194">Dans ce cas, il n’importe quelle requête hello est.</span><span class="sxs-lookup"><span data-stu-id="4b888-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="4b888-195">Si le nombre de partitions d’entrée de hello ne correspond pas à nombre de partitions de sortie hello, topologie de hello n’est pas excessivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="4b888-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="4b888-196">Sortie ne correspondant pas à un concentrateur Event Hub ni à un stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="4b888-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="4b888-197">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="4b888-198">Sortie : Power BI</span><span class="sxs-lookup"><span data-stu-id="4b888-198">Output: PowerBI</span></span>

<span data-ttu-id="4b888-199">Pour le moment, la sortie Power BI ne prend pas en charge le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="4b888-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="4b888-200">Par conséquent, ce scénario n’est pas de type massivement parallèle.</span><span class="sxs-lookup"><span data-stu-id="4b888-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="4b888-201">Requête à plusieurs étapes avec différentes valeurs Partition By</span><span class="sxs-lookup"><span data-stu-id="4b888-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="4b888-202">Entrée : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="4b888-203">Sortie : concentrateur Event Hub avec 8 partitions</span><span class="sxs-lookup"><span data-stu-id="4b888-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="4b888-204">Requête :</span><span class="sxs-lookup"><span data-stu-id="4b888-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="4b888-205">Comme vous pouvez le voir, hello deuxième étape utilise **TollBoothId** en tant que clé de partitionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="4b888-206">Cette étape est même hello pas en tant que première étape de hello, et elle nécessite par conséquent nous toodo une lecture aléatoire.</span><span class="sxs-lookup"><span data-stu-id="4b888-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="4b888-207">Hello exemples précédents décrivent certains travaux Analytique de flux de données qui sont conformes trop (ou ne) une topologie de ces.</span><span class="sxs-lookup"><span data-stu-id="4b888-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="4b888-208">Si elles sont conformes, ils ont potentiel hello pour l’échelle maximale.</span><span class="sxs-lookup"><span data-stu-id="4b888-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="4b888-209">Pour les travaux qui ne correspondent pas à l’un de ces profils, des conseils de mise à l’échelle seront disponibles dans les futures mises à jour.</span><span class="sxs-lookup"><span data-stu-id="4b888-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="4b888-210">Pour l’instant, utilisez les conseils généraux hello Bonjour les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="4b888-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="4b888-211">Calculer les unités de diffusion en continu maximale hello d’un travail</span><span class="sxs-lookup"><span data-stu-id="4b888-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="4b888-212">Nombre total de Hello d’unités de diffusion en continu qui peut être utilisé par une tâche de flux de données Analytique dépend du nombre hello des étapes de requête de hello définie pour les travaux de hello et nombre de hello de partitions pour chaque étape.</span><span class="sxs-lookup"><span data-stu-id="4b888-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="4b888-213">Étapes dans une requête</span><span class="sxs-lookup"><span data-stu-id="4b888-213">Steps in a query</span></span>
<span data-ttu-id="4b888-214">Une requête peut avoir une ou plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="4b888-214">A query can have one or many steps.</span></span> <span data-ttu-id="4b888-215">Chaque étape est une sous-requête définie par hello **WITH** (mot clé).</span><span class="sxs-lookup"><span data-stu-id="4b888-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="4b888-216">requête Hello qui se trouve en dehors de hello **WITH** (mot clé) (une requête uniquement) est également comptabilisée comme une étape, par exemple hello **sélectionnez** instruction Bonjour suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="4b888-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="4b888-217">Cette requête compte deux étapes.</span><span class="sxs-lookup"><span data-stu-id="4b888-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="4b888-218">Cette requête est décrite plus en détail plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="4b888-219">Partitionnement d'une étape</span><span class="sxs-lookup"><span data-stu-id="4b888-219">Partition a step</span></span>
<span data-ttu-id="4b888-220">Une étape de partitionnement nécessite hello conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b888-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="4b888-221">source d’entrée de Hello doit être partitionné.</span><span class="sxs-lookup"><span data-stu-id="4b888-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="4b888-222">Hello **sélectionnez** instruction de requête de hello doit lire à partir d’une source d’entrée partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="4b888-223">requête Hello au sein de l’étape de hello doit avoir hello **Partition By** (mot clé).</span><span class="sxs-lookup"><span data-stu-id="4b888-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="4b888-224">Lorsqu’une requête est partitionnée, les événements d’entrée hello sont des groupes de traité et agrégées dans partition distincte, et les événements de sorties sont générés pour chaque groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="4b888-225">Si vous souhaitez un agrégat combiné, vous devez créer un deuxième tooaggregate de non partitionné une étape.</span><span class="sxs-lookup"><span data-stu-id="4b888-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="4b888-226">Calculer max hello unités pour un travail de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="4b888-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="4b888-227">Toutes les étapes non partitionnées ensemble peuvent évoluer toosix unités (SUs) pour une tâche de flux de données Analytique de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="4b888-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="4b888-228">SUs tooadd, une étape doivent être partitionnées.</span><span class="sxs-lookup"><span data-stu-id="4b888-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="4b888-229">Chaque partition peut comporter six unités SU.</span><span class="sxs-lookup"><span data-stu-id="4b888-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="4b888-230">Interroger</span><span class="sxs-lookup"><span data-stu-id="4b888-230">Query</span></span></th><th><span data-ttu-id="4b888-231">SUs max pour le travail de hello</span><span class="sxs-lookup"><span data-stu-id="4b888-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="4b888-232">requête de Hello contient une seule étape.</span><span class="sxs-lookup"><span data-stu-id="4b888-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="4b888-233">étape de Hello n’est pas partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="4b888-234">6</span><span class="sxs-lookup"><span data-stu-id="4b888-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="4b888-235">flux de données d’entrée Hello est partitionné par 3.</span><span class="sxs-lookup"><span data-stu-id="4b888-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="4b888-236">requête de Hello contient une seule étape.</span><span class="sxs-lookup"><span data-stu-id="4b888-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="4b888-237">étape de Hello est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="4b888-238">18</span><span class="sxs-lookup"><span data-stu-id="4b888-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="4b888-239">requête de Hello contient deux étapes.</span><span class="sxs-lookup"><span data-stu-id="4b888-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="4b888-240">Aucun des étapes de hello est partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="4b888-241">6</span><span class="sxs-lookup"><span data-stu-id="4b888-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="4b888-242">flux de données d’entrée Hello est partitionné par 3.</span><span class="sxs-lookup"><span data-stu-id="4b888-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="4b888-243">requête de Hello contient deux étapes.</span><span class="sxs-lookup"><span data-stu-id="4b888-243">hello query contains two steps.</span></span> <span data-ttu-id="4b888-244">étape d’entrée de Hello est partitionné et la deuxième étape de hello n’est pas.</span><span class="sxs-lookup"><span data-stu-id="4b888-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="4b888-245">Hello <strong>sélectionnez</strong> instruction lit à partir de l’entrée de hello partitionnée.</span><span class="sxs-lookup"><span data-stu-id="4b888-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="4b888-246">24 (18 pour les étapes partitionnées + 6 pour les étapes non partitionnées)</span><span class="sxs-lookup"><span data-stu-id="4b888-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="4b888-247">Exemples de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="4b888-247">Examples of scaling</span></span>

<span data-ttu-id="4b888-248">Hello requête suivante calcule nombre hello de voitures dans une fenêtre de trois minutes traverser une station de péage qui a trois péages.</span><span class="sxs-lookup"><span data-stu-id="4b888-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="4b888-249">Cette requête peut être augmentée toosix SUs.</span><span class="sxs-lookup"><span data-stu-id="4b888-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="4b888-250">toouse plus SUs pour hello requête, les deux hello des flux de données d’entrée et les requêtes hello doivent être partitionnées.</span><span class="sxs-lookup"><span data-stu-id="4b888-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="4b888-251">Étant donné que la partition de flux de données hello a la valeur too3, hello requête modifiée suivante peut être mis à l’échelle too18 SUs :</span><span class="sxs-lookup"><span data-stu-id="4b888-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="4b888-252">Lorsqu’une requête est partitionnée, les événements d’entrée hello sont traités et agrégées dans des groupes de partition distincte.</span><span class="sxs-lookup"><span data-stu-id="4b888-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="4b888-253">Événements de sortie sont également générés pour chaque groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="4b888-254">Le partitionnement peut entraîner des résultats inattendus lorsque hello **GROUP BY** champ n’est pas clé de partition hello dans le flux de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="4b888-255">Par exemple, hello **TollBoothId** clé de partition hello de champ dans la requête précédente de hello n’est pas **entrée1**.</span><span class="sxs-lookup"><span data-stu-id="4b888-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="4b888-256">résultat de Hello est que hello données à partir de péage #1 peuvent être réparties dans plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="4b888-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="4b888-257">Chacun des hello **entrée1** partitions seront traitées séparément par flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="4b888-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="4b888-258">Par conséquent, plusieurs enregistrements de nombre de voitures hello pour hello même péage Bonjour même fenêtre bascule sera créée.</span><span class="sxs-lookup"><span data-stu-id="4b888-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="4b888-259">Si la clé de partition d’entrée hello ne peut pas être modifié, ce problème peut être résolu en ajoutant une étape d’une partition, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4b888-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="4b888-260">Cette requête peut être mis à l’échelle too24 SUs.</span><span class="sxs-lookup"><span data-stu-id="4b888-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="4b888-261">Si vous joignez deux flux de données, assurez-vous que les flux de hello sont partitionnées par clé de partition hello de colonne de hello que vous utilisez des jointures de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4b888-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="4b888-262">Assurez-vous également que vous avez hello même nombre de partitions dans les deux flux de données.</span><span class="sxs-lookup"><span data-stu-id="4b888-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="4b888-263">Configurer des unités de diffusion en continu Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4b888-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="4b888-264">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b888-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4b888-265">Dans la liste de hello des ressources, recherchez les tâches de flux Analytique hello que vous souhaitez tooscale, puis ouvrez.</span><span class="sxs-lookup"><span data-stu-id="4b888-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="4b888-266">Bonjour travail panneau, sous **configurer**, cliquez sur **échelle**.</span><span class="sxs-lookup"><span data-stu-id="4b888-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Configuration d’un travail Stream Analytics sur le portail Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="4b888-268">Utilisez hello curseur tooset hello SUs pour le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="4b888-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="4b888-269">Notez que vous les paramètres SU toospecific limité.</span><span class="sxs-lookup"><span data-stu-id="4b888-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="4b888-270">Surveillance des performances du travail</span><span class="sxs-lookup"><span data-stu-id="4b888-270">Monitor job performance</span></span>
<span data-ttu-id="4b888-271">À l’aide de hello portail Azure, vous pouvez suivre le débit d’une tâche hello :</span><span class="sxs-lookup"><span data-stu-id="4b888-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Surveillance des travaux Azure Stream Analytics][img.stream.analytics.monitor.job]

<span data-ttu-id="4b888-273">Calculer le débit de charge de travail hello hello attendu.</span><span class="sxs-lookup"><span data-stu-id="4b888-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="4b888-274">Si le débit de hello est inférieur au nombre attendu, régler la partition d’entrée de hello, paramétrez hello requête et ajouter SUs tooyour travail.</span><span class="sxs-lookup"><span data-stu-id="4b888-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="4b888-275">Visualiser le débit de flux de données Analytique à l’échelle : scénario de framboises Pi hello</span><span class="sxs-lookup"><span data-stu-id="4b888-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="4b888-276">toohelp que vous comprenez comment les tâches de flux de données Analytique l’échelle, nous avons effectué une expérience en fonction de l’entrée à partir d’un appareil framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="4b888-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="4b888-277">Cette expérience nous permettre de voir l’effet hello sur le débit de plusieurs unités de diffusion en continu et partitions.</span><span class="sxs-lookup"><span data-stu-id="4b888-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="4b888-278">Dans ce scénario, les appareils hello envoie concentrateur d’événements tooan capteur données (clients).</span><span class="sxs-lookup"><span data-stu-id="4b888-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="4b888-279">Analytique de diffusion en continu traite les données de hello et envoie une alerte ou les statistiques sous la forme d’un concentrateur d’événements de sortie tooanother.</span><span class="sxs-lookup"><span data-stu-id="4b888-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="4b888-280">client de Hello envoie des données de capteur au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4b888-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="4b888-281">sortie des données Hello est également au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4b888-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="4b888-282">les données de salutation ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="4b888-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="4b888-283">Hello suivant la requête est toosend utilisé une alerte lorsqu’une lumière est mises hors tension :</span><span class="sxs-lookup"><span data-stu-id="4b888-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="4b888-284">Mesurer le débit</span><span class="sxs-lookup"><span data-stu-id="4b888-284">Measure throughput</span></span>

<span data-ttu-id="4b888-285">Dans ce contexte, le débit est Montant hello des données d’entrée traitées par les flux de données Analytique une quantité fixe de temps.</span><span class="sxs-lookup"><span data-stu-id="4b888-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="4b888-286">(Nous mesuré pendant 10 minutes). tooachieve hello meilleur débit de traitement pour hello les données d’entrée, les fichiers de données hello de flux d’entrée et les requêtes hello ont été partitionnées.</span><span class="sxs-lookup"><span data-stu-id="4b888-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="4b888-287">Nous avons inclus **COUNT()** dans hello requête toomeasure combien d’événements d’entrée ont été traitées.</span><span class="sxs-lookup"><span data-stu-id="4b888-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="4b888-288">travail de hello que toomake pas simplement attendait toocome des événements d’entrée, chaque partition du concentrateur d’événements d’entrée hello a été préchargée environ 300 Mo de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4b888-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="4b888-289">Hello tableau suivant montre les résultats hello que nous avons vu lorsque nous avons augmenté nombre hello d’unités de diffusion en continu et du nombre de partition correspondante de hello dans les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="4b888-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="4b888-290">Partitions d'entrée</span><span class="sxs-lookup"><span data-stu-id="4b888-290">Input Partitions</span></span></th><th><span data-ttu-id="4b888-291">Partitions de sortie</span><span class="sxs-lookup"><span data-stu-id="4b888-291">Output Partitions</span></span></th><th><span data-ttu-id="4b888-292">Unités de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="4b888-292">Streaming Units</span></span></th><th><span data-ttu-id="4b888-293">Débit soutenu</span><span class="sxs-lookup"><span data-stu-id="4b888-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="4b888-294">12</span><span class="sxs-lookup"><span data-stu-id="4b888-294">12</span></span></td>
<td><span data-ttu-id="4b888-295">12</span><span class="sxs-lookup"><span data-stu-id="4b888-295">12</span></span></td>
<td><span data-ttu-id="4b888-296">6</span><span class="sxs-lookup"><span data-stu-id="4b888-296">6</span></span></td>
<td><span data-ttu-id="4b888-297">4,06 Mo/s</span><span class="sxs-lookup"><span data-stu-id="4b888-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="4b888-298">12</span><span class="sxs-lookup"><span data-stu-id="4b888-298">12</span></span></td>
<td><span data-ttu-id="4b888-299">12</span><span class="sxs-lookup"><span data-stu-id="4b888-299">12</span></span></td>
<td><span data-ttu-id="4b888-300">12</span><span class="sxs-lookup"><span data-stu-id="4b888-300">12</span></span></td>
<td><span data-ttu-id="4b888-301">8,06 Mo/s</span><span class="sxs-lookup"><span data-stu-id="4b888-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="4b888-302">48</span><span class="sxs-lookup"><span data-stu-id="4b888-302">48</span></span></td>
<td><span data-ttu-id="4b888-303">48</span><span class="sxs-lookup"><span data-stu-id="4b888-303">48</span></span></td>
<td><span data-ttu-id="4b888-304">48</span><span class="sxs-lookup"><span data-stu-id="4b888-304">48</span></span></td>
<td><span data-ttu-id="4b888-305">38,32 Mo/s</span><span class="sxs-lookup"><span data-stu-id="4b888-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="4b888-306">192</span><span class="sxs-lookup"><span data-stu-id="4b888-306">192</span></span></td>
<td><span data-ttu-id="4b888-307">192</span><span class="sxs-lookup"><span data-stu-id="4b888-307">192</span></span></td>
<td><span data-ttu-id="4b888-308">192</span><span class="sxs-lookup"><span data-stu-id="4b888-308">192</span></span></td>
<td><span data-ttu-id="4b888-309">172,67 Mo/s</span><span class="sxs-lookup"><span data-stu-id="4b888-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="4b888-310">480</span><span class="sxs-lookup"><span data-stu-id="4b888-310">480</span></span></td>
<td><span data-ttu-id="4b888-311">480</span><span class="sxs-lookup"><span data-stu-id="4b888-311">480</span></span></td>
<td><span data-ttu-id="4b888-312">480</span><span class="sxs-lookup"><span data-stu-id="4b888-312">480</span></span></td>
<td><span data-ttu-id="4b888-313">454,27 Mo/s</span><span class="sxs-lookup"><span data-stu-id="4b888-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="4b888-314">720</span><span class="sxs-lookup"><span data-stu-id="4b888-314">720</span></span></td>
<td><span data-ttu-id="4b888-315">720</span><span class="sxs-lookup"><span data-stu-id="4b888-315">720</span></span></td>
<td><span data-ttu-id="4b888-316">720</span><span class="sxs-lookup"><span data-stu-id="4b888-316">720</span></span></td>
<td><span data-ttu-id="4b888-317">609,69 Mo/s</span><span class="sxs-lookup"><span data-stu-id="4b888-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="4b888-318">Et hello graphique suivant montre une visualisation de relation hello entre SUs et le débit.</span><span class="sxs-lookup"><span data-stu-id="4b888-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="4b888-320">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="4b888-320">Get help</span></span>
<span data-ttu-id="4b888-321">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="4b888-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b888-322">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b888-322">Next steps</span></span>
* [<span data-ttu-id="4b888-323">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="4b888-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4b888-324">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4b888-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4b888-325">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4b888-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4b888-326">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="4b888-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

