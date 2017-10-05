---
title: "Déboguer les requêtes Azure Stream Analytics à l’aide de SELECT INTO | Microsoft Docs"
description: "Exemple de requête intermédiaire des données utilisant des instructions SELECT INTO dans Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="b71cb-103">Déboguer des requêtes à l’aide des instructions SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="b71cb-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="b71cb-104">Lors du traitement de données en temps réel, savoir à quoi ressemblent les données au milieu de la requête peut être utile.</span><span class="sxs-lookup"><span data-stu-id="b71cb-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="b71cb-105">Étant donné que les entrées ou les étapes d’un travail Azure Stream Analytics peuvent être lues plusieurs fois, vous pouvez écrire des instructions SELECT INTO supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b71cb-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="b71cb-106">Cela génère des données intermédiaires dans le stockage et vous permet d’inspecter l’exactitude des données, tout comme le font les *variables espionnes* lorsque vous déboguez un programme.</span><span class="sxs-lookup"><span data-stu-id="b71cb-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="b71cb-107">Utiliser SELECT INTO pour vérifier le flux de données</span><span class="sxs-lookup"><span data-stu-id="b71cb-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="b71cb-108">L’exemple de requête suivant dans un travail Azure Stream Analytics a un flux d’entrée, deux entrées de données de référence et une sortie pour Stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="b71cb-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="b71cb-109">La requête joint les données du Event Hub et deux objets blob de référence pour obtenir les informations de nom et de catégorie :</span><span class="sxs-lookup"><span data-stu-id="b71cb-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![Exemple de requête SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="b71cb-111">Notez que le travail est en cours d’exécution, mais aucun événement n’est produit dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="b71cb-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="b71cb-112">Dans la vignette **Surveillance**, illustrée ici, vous pouvez voir que l’entrée génère des données, mais vous ne savez pas quelle étape de **JOIN** a causé la suppression de tous les événements.</span><span class="sxs-lookup"><span data-stu-id="b71cb-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![Vignette Surveillance](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="b71cb-114">Dans ce cas, vous pouvez ajouter quelques instructions SELECT INTO supplémentaires pour « journaliser » les résultats JOIN intermédiaires et les données lues à partir de l’entrée.</span><span class="sxs-lookup"><span data-stu-id="b71cb-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="b71cb-115">Dans cet exemple, nous avons ajouté deux nouvelles « sorties temporaires ».</span><span class="sxs-lookup"><span data-stu-id="b71cb-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="b71cb-116">Il peut s’agir du récepteur que vous voulez.</span><span class="sxs-lookup"><span data-stu-id="b71cb-116">They can be any sink you like.</span></span> <span data-ttu-id="b71cb-117">Ici, nous utilisons Stockage Azure comme exemple :</span><span class="sxs-lookup"><span data-stu-id="b71cb-117">Here we use Azure Storage as an example:</span></span>

![Ajout d’instructions SELECT INTO supplémentaires](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="b71cb-119">Vous pouvez ensuite réécrire la requête comme suit :</span><span class="sxs-lookup"><span data-stu-id="b71cb-119">You can then rewrite the query like this:</span></span>

![Requête SELECT INTO réécrite](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="b71cb-121">À présent, relancez le travail et laissez-le s’exécuter pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="b71cb-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="b71cb-122">Ensuite, interrogez temp1 et temp2 avec Visual Studio Cloud Explorer pour produire les tables suivantes :</span><span class="sxs-lookup"><span data-stu-id="b71cb-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="b71cb-123">**table temp1**
![table temp1 SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="b71cb-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="b71cb-124">**table temp2**
![table temp2 SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="b71cb-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="b71cb-125">Comme vous pouvez le voir, temp1 et temp2 présentent tous deux des données, et la colonne de nom est remplie correctement dans temp2.</span><span class="sxs-lookup"><span data-stu-id="b71cb-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="b71cb-126">Toutefois, étant donné qu’il n’y a toujours aucune donnée dans la sortie, quelque chose ne va pas :</span><span class="sxs-lookup"><span data-stu-id="b71cb-126">However, because there is still no data in output, something is wrong:</span></span>

![Table output1 SELECT INTO sans aucune donnée](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="b71cb-128">En échantillonnant les données, vous pouvez être presque certain que le problème concerne le deuxième JOIN.</span><span class="sxs-lookup"><span data-stu-id="b71cb-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="b71cb-129">Vous pouvez télécharger les données de référence à partir de l’objet blob et jeter un coup de œil :</span><span class="sxs-lookup"><span data-stu-id="b71cb-129">You can download the reference data from the blob and take a look:</span></span>

![Table de référence SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="b71cb-131">Comme vous pouvez le voir, le format du GUID dans ces données de référence est différent du format de la colonne [from] dans temp2.</span><span class="sxs-lookup"><span data-stu-id="b71cb-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="b71cb-132">C’est pourquoi les données ne sont pas arrivées dans output1 comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b71cb-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="b71cb-133">Vous pouvez corriger le format de données, les télécharger pour référencer des objets blob, puis réessayer :</span><span class="sxs-lookup"><span data-stu-id="b71cb-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![Table temp SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="b71cb-135">Cette fois, les données dans la sortie sont mises en forme et remplies comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b71cb-135">This time, the data in the output is formatted and populated as expected.</span></span>

![Table finale SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="b71cb-137">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="b71cb-137">Get help</span></span>

<span data-ttu-id="b71cb-138">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b71cb-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b71cb-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b71cb-139">Next steps</span></span>

* [<span data-ttu-id="b71cb-140">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b71cb-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b71cb-141">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b71cb-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b71cb-142">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b71cb-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b71cb-143">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b71cb-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b71cb-144">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b71cb-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

