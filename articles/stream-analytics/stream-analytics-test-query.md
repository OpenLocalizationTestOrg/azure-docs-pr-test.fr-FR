---
title: "test de la requête de flux de données Analytique aaaAzure | Documents Microsoft"
description: "Comment tootest vos requêtes dans les tâches de flux de données Analytique."
keywords: "test des requêtes, dépannage des requêtes"
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="10db3-104">Tester les requêtes Azure Stream Analytique Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="10db3-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="10db3-105">Avec Azure Analytique de flux de données, vous pouvez tester les requêtes Bonjour portail Azure sans avoir besoin de toostart ou arrêter un travail.</span><span class="sxs-lookup"><span data-stu-id="10db3-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="10db3-106">Entrée de test hello</span><span class="sxs-lookup"><span data-stu-id="10db3-106">Test hello input</span></span>

1. <span data-ttu-id="10db3-107">tootest avec des exemples de données d’entrée, cliquez sur un de vos entrées, puis sélectionnez **télécharger des exemples de données à partir du fichier**.</span><span class="sxs-lookup"><span data-stu-id="10db3-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Test des requêtes dans l’éditeur de requête Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="10db3-109">Une fois le téléchargement de hello est terminé, cliquez sur **Test** tootest cette requête sur hello les exemples de données que vous avez fourni.</span><span class="sxs-lookup"><span data-stu-id="10db3-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![Exemple de données de test des requêtes dans l’éditeur de requête Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="10db3-111">sortie de Hello de votre requête s’affiche dans le navigateur hello, avec un lien de téléchargement de résultats si vous souhaitez que sortie de test toosave hello pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="10db3-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="10db3-112">Vous pouvez désormais facilement et de manière itérative modifiez votre requête et testez-le à plusieurs reprises toosee comment hello de sortie est modifiée.</span><span class="sxs-lookup"><span data-stu-id="10db3-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Exemple de sortie de l’éditeur de requête Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="10db3-114">Plusieurs sorties utilisé dans une requête, vous pouvez consulter les résultats hello pour les deux sorties séparément et basculer facilement entre eux.</span><span class="sxs-lookup"><span data-stu-id="10db3-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="10db3-115">Une fois que vous êtes satisfait des résultats hello indiquées dans le navigateur de hello, vous pouvez enregistrer votre requête, lancez votre tâche et laisser il traite les événements sans erreur.</span><span class="sxs-lookup"><span data-stu-id="10db3-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="10db3-116">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="10db3-116">Get help</span></span>

<span data-ttu-id="10db3-117">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="10db3-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10db3-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10db3-118">Next steps</span></span>

* [<span data-ttu-id="10db3-119">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="10db3-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="10db3-120">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10db3-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="10db3-121">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10db3-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="10db3-122">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10db3-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="10db3-123">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10db3-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
