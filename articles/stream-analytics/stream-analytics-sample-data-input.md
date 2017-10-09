---
title: "entrées d’échantillonnage aaa Analytique de flux de données Azure | Documents Microsoft"
description: "Identifiez les problèmes lors du dépannage des travaux Stream Analytics."
keywords: "résoudre les problèmes d’entrée, échantillonnage des entrées"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="70b9b-104">Échantillonnage de flux d’entrée Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="70b9b-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="70b9b-105">À l’aide d’Analytique de flux de données Azure, vous pouvez échantillonner des événements d’entrée qui proviennent d’un fichier et de tester les requêtes dans le portail de hello sans avoir besoin de toostart ou d’arrêter un travail.</span><span class="sxs-lookup"><span data-stu-id="70b9b-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="70b9b-106">Test de votre requête</span><span class="sxs-lookup"><span data-stu-id="70b9b-106">Testing your query</span></span>

<span data-ttu-id="70b9b-107">Dans le volet d’informations travail hello Analytique de flux de données, ouvrez hello **l’éditeur de requête** panneau en cliquant sur le nom de la requête hello sous **requête**.</span><span class="sxs-lookup"><span data-stu-id="70b9b-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="70b9b-108">(Dans notre exemple de scénario, car aucune requête n’a encore été créé, cliquez sur hello **< >** espace réservé.)</span><span class="sxs-lookup"><span data-stu-id="70b9b-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![éditeur de requête de flux de données Analytique Hello](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="70b9b-110">panneau d’éditeur enrichi Hello pour la création de votre requête s’affiche telle qu’elle était dans la version précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="70b9b-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="70b9b-111">Maintenant le panneau de hello a été mis à jour avec un nouveau volet gauche qui affiche hello entrées et les sorties qui sont utilisées par la requête de hello et définis pour cette tâche.</span><span class="sxs-lookup"><span data-stu-id="70b9b-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![éditeur de requête de flux de données Analytique Hello les entrées et sorties des listes](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="70b9b-113">Sont également affichées une entrée et une sortie supplémentaires, qui ne sont pas définies.</span><span class="sxs-lookup"><span data-stu-id="70b9b-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="70b9b-114">Elles proviennent de hello modèle de requête avec laquelle vous démarrez.</span><span class="sxs-lookup"><span data-stu-id="70b9b-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="70b9b-115">Ils modifient ou disparaissent complètement, lorsque vous modifiez la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="70b9b-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="70b9b-116">Vous pouvez ignorer ces erreurs pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="70b9b-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="70b9b-117">tootest avec des exemples de données d’entrée, cliquez sur un de vos entrées, puis sélectionnez **télécharger des exemples de données à partir du fichier**.</span><span class="sxs-lookup"><span data-stu-id="70b9b-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Hello flux Analytique éditeur téléchargement exemple interroge les données de fichier (commande)](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="70b9b-119">Une fois le téléchargement de hello est terminé, cliquez sur **Test** tootest cette requête sur hello exemples de données que vous avez fournies.</span><span class="sxs-lookup"><span data-stu-id="70b9b-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![bouton Test éditeur Hello Analytique de flux de requête](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="70b9b-121">Si vous souhaitez que les résultats des tests toosave hello pour une utilisation ultérieure, sortie hello de votre requête s’affiche dans le navigateur hello avec un résultats du téléchargement toohello lien.</span><span class="sxs-lookup"><span data-stu-id="70b9b-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="70b9b-122">Vous pouvez désormais facilement et de manière itérative modifiez votre requête et testez-le à plusieurs reprises toosee comment hello de sortie est modifiée.</span><span class="sxs-lookup"><span data-stu-id="70b9b-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Exemple de sortie de l’éditeur de requête Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="70b9b-124">Bonjour précédant l’image, une deuxième sortie a été ajoutée, appelée **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="70b9b-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="70b9b-125">Lorsque vous utilisez plusieurs sorties dans une requête, vous pouvez voir les résultats de hello pour chaque sortie séparément et basculer facilement entre eux.</span><span class="sxs-lookup"><span data-stu-id="70b9b-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="70b9b-126">Une fois que vous êtes satisfait des résultats de hello, vous pouvez enregistrer votre requête, lancez votre tâche, confortablement et regardez magic hello de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="70b9b-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="70b9b-127">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="70b9b-127">Get help</span></span>

<span data-ttu-id="70b9b-128">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="70b9b-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70b9b-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70b9b-129">Next steps</span></span>
* [<span data-ttu-id="70b9b-130">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="70b9b-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="70b9b-131">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="70b9b-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="70b9b-132">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="70b9b-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="70b9b-133">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="70b9b-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="70b9b-134">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="70b9b-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
