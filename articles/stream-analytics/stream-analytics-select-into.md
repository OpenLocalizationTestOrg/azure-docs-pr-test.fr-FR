---
title: "les requêtes à l’aide de SELECT INTO aaaDebug Analytique de flux de données Azure | Documents Microsoft"
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="72d9c-103">Déboguer des requêtes à l’aide des instructions SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="72d9c-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="72d9c-104">Dans le traitement des données en temps réel, savoir quelles données hello il semble que la requête peut être utile dans le milieu de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="72d9c-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="72d9c-105">Étant donné que les entrées ou les étapes d’un travail Azure Stream Analytics peuvent être lues plusieurs fois, vous pouvez écrire des instructions SELECT INTO supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="72d9c-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="72d9c-106">Cela génère des données intermédiaires dans le stockage et vous permet d’inspecter l’exactitude hello de données de hello, tout comme *variables espionnes* feriez lorsque vous déboguez un programme.</span><span class="sxs-lookup"><span data-stu-id="72d9c-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="72d9c-107">Utilisez SELECT INTO le flux de données hello toocheck</span><span class="sxs-lookup"><span data-stu-id="72d9c-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="72d9c-108">Hello exemple de requête suivant dans une tâche Analytique de flux de données Azure a un flux de données entrée, deux entrées de données de référence et une sortie de tooAzure le stockage de Table.</span><span class="sxs-lookup"><span data-stu-id="72d9c-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="72d9c-109">Hello jointure de données à partir de concentrateur d’événements hello et deux objets BLOB tooget hello nom et la catégorie des informations de référence :</span><span class="sxs-lookup"><span data-stu-id="72d9c-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Exemple de requête SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="72d9c-111">Notez que les travaux hello sont en cours d’exécution, mais aucun événement n’est produites dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="72d9c-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="72d9c-112">Sur hello **analyse** vignette, indiqué ici, vous pouvez voir que hello entrée qui produisent des données, mais vous ne savez pas quelle étape Hello **joindre** dû tous hello toobe événements supprimé.</span><span class="sxs-lookup"><span data-stu-id="72d9c-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![vignette de surveillance Hello](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="72d9c-114">Dans ce cas, vous pouvez ajouter quelques supplémentaire les instructions SELECT INTO trop « ouvrir une session « résultats de la jointure intermédiaires hello et données hello qui sont lu à partir de l’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="72d9c-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="72d9c-115">Dans cet exemple, nous avons ajouté deux nouvelles « sorties temporaires ».</span><span class="sxs-lookup"><span data-stu-id="72d9c-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="72d9c-116">Il peut s’agir du récepteur que vous voulez.</span><span class="sxs-lookup"><span data-stu-id="72d9c-116">They can be any sink you like.</span></span> <span data-ttu-id="72d9c-117">Ici, nous utilisons Stockage Azure comme exemple :</span><span class="sxs-lookup"><span data-stu-id="72d9c-117">Here we use Azure Storage as an example:</span></span>

![Ajout d’instructions SELECT INTO supplémentaires](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="72d9c-119">Vous pouvez ensuite réécrire requête hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="72d9c-119">You can then rewrite hello query like this:</span></span>

![Requête SELECT INTO réécrite](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="72d9c-121">Maintenant redémarrer les travaux hello et laisser s’exécuter pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="72d9c-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="72d9c-122">Requête puis temp1 et temp2 avec hello tooproduce de Visual Studio Cloud Explorer les tableaux suivants :</span><span class="sxs-lookup"><span data-stu-id="72d9c-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="72d9c-123">**table temp1**
![table temp1 SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="72d9c-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="72d9c-124">**table temp2**
![table temp2 SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="72d9c-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="72d9c-125">Comme vous pouvez le voir, temp1 et temp2 disposent de données et colonne de nom hello est rempli correctement dans temporaire-2.</span><span class="sxs-lookup"><span data-stu-id="72d9c-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="72d9c-126">Toutefois, étant donné qu’il n’y a toujours aucune donnée dans la sortie, quelque chose ne va pas :</span><span class="sxs-lookup"><span data-stu-id="72d9c-126">However, because there is still no data in output, something is wrong:</span></span>

![Table output1 SELECT INTO sans aucune donnée](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="72d9c-128">En échantillonnant les données de salutation, vous pouvez être pratiquement certain que le problème de hello a avec hello seconde jointure.</span><span class="sxs-lookup"><span data-stu-id="72d9c-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="72d9c-129">Vous pouvez télécharger des données de référence hello à partir de l’objet blob de hello et jeter un coup de œil :</span><span class="sxs-lookup"><span data-stu-id="72d9c-129">You can download hello reference data from hello blob and take a look:</span></span>

![Table de référence SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="72d9c-131">Comme vous pouvez le voir, format de hello Hello GUID dans ces données de référence est différent de format hello Hello [from] colonne temporaire-2.</span><span class="sxs-lookup"><span data-stu-id="72d9c-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="72d9c-132">C’est pourquoi les données de salutation n’est pas arrivé dans output1 comme prévu.</span><span class="sxs-lookup"><span data-stu-id="72d9c-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="72d9c-133">Vous pouvez corriger le format de données hello, téléchargez-le tooreference blob et réessayez :</span><span class="sxs-lookup"><span data-stu-id="72d9c-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![Table temp SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="72d9c-135">Cette fois-ci, données hello dans la sortie de hello sont mis en forme et remplies comme prévu.</span><span class="sxs-lookup"><span data-stu-id="72d9c-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![Table finale SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="72d9c-137">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="72d9c-137">Get help</span></span>

<span data-ttu-id="72d9c-138">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="72d9c-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72d9c-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72d9c-139">Next steps</span></span>

* [<span data-ttu-id="72d9c-140">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="72d9c-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="72d9c-141">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="72d9c-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="72d9c-142">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="72d9c-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="72d9c-143">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="72d9c-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="72d9c-144">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="72d9c-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

