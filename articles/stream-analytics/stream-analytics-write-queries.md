---
title: "requêtes de toowrite aaaHow dans le flux de données Analytique | Documents Microsoft"
description: "Écrire des requêtes dans Stream Analytics et interroger des données | segment du parcours d’apprentissage."
keywords: "la façon dont les requêtes toowrite, interroger des données, écrivez une requête, l’écriture de requêtes"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="26858-104">Fonctionnement des requêtes dans le flux de données Analytique toowrite</span><span class="sxs-lookup"><span data-stu-id="26858-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="26858-105">L’écriture de requêtes pour le flux logique dans Azure flux Analytique de traitement est implémenté comme une « requête permanent » qui est définie avant un travail démarre et exécutés sur des données qu’il atteint le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="26858-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="26858-106">transformation des données Hello est exprimée dans un langage de requête de type SQL, qui est principalement un sous-ensemble T-SQL avec certaines ajouté comme des extensions de langage [fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx) utilisé tooexpress la sémantique temporel.</span><span class="sxs-lookup"><span data-stu-id="26858-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="26858-107">Écriture de requêtes :</span><span class="sxs-lookup"><span data-stu-id="26858-107">Writing Queries:</span></span>
1. <span data-ttu-id="26858-108">Dans votre tâche Analytique de flux de données dans le portail de gestion Azure hello, cliquez sur **requête**.</span><span class="sxs-lookup"><span data-stu-id="26858-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Sélection d'une requête](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="26858-110">Bonjour portail Azure, cliquez sur **requête**.</span><span class="sxs-lookup"><span data-stu-id="26858-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Sélection d’un aperçu de requête](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="26858-112">Nouvelles tâches ont une toohelp de modèle de requête vous aideront à démarrer.</span><span class="sxs-lookup"><span data-stu-id="26858-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="26858-113">requête Hello modèle effectue un « pass-through » de requête qui projette tous les champs à partir des événements d’entrée dans la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="26858-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="26858-114">Si vous avez défini au moins une entrée et sortie pour votre travail, vous pouvez remplacer hello espace réservé « [YourOutputAlias] » et « [YourInputAlias] » champs avec des alias hello Hello d’entrée et sortie que vous souhaitez utiliser tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="26858-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="26858-115">En outre, vous pouvez toujours créer et tester votre requête Bonjour portail classique Azure sans définir des entrées et sorties sur le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="26858-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="26858-116">Si vous le souhaitez tooperform davantage de traitement que direct simple, vous pouvez modifier la définition de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="26858-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="26858-117">tooget création de la requête, examinons certains des requêtes courantes de modèles sont capturés [ici](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="26858-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Fenêtre Données de requête](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="26858-119">données de requête toovalidate fonctionne :</span><span class="sxs-lookup"><span data-stu-id="26858-119">toovalidate query data is working:</span></span>
<span data-ttu-id="26858-120">Vous pouvez vérifier que votre requête se comporte comme prévu en l’exécutant dans le navigateur de hello sur un ou plusieurs fichiers JSON locales contenant des données de test.</span><span class="sxs-lookup"><span data-stu-id="26858-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="26858-121">Il ne sera pas démarrer le travail de hello ou avoir des conséquences de facturation.</span><span class="sxs-lookup"><span data-stu-id="26858-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="26858-122">Actuellement le test de la requête de dans le navigateur n’est pas pris en charge dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="26858-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="26858-123">Assurez-vous qu’il n’y a aucune erreur de requête hello (sinon hello Test bouton est désactivé) puis cliquez sur le bouton de Test hello.</span><span class="sxs-lookup"><span data-stu-id="26858-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Test des données de requête](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="26858-125">Vous serez fichiers toospecify demandées pour chacune des entrées hello référencées dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="26858-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="26858-126">Dans cet exemple, la requête de modèle hello est considérée comme-étant, boîte de dialogue hello demande pour une entrée nommée « yourinputalias ».</span><span class="sxs-lookup"><span data-stu-id="26858-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Tester les données de requête](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="26858-128">Rechercher le fichier de test tooa.</span><span class="sxs-lookup"><span data-stu-id="26858-128">Browse tooa test file.</span></span> <span data-ttu-id="26858-129">Plusieurs exemples de fichiers sont disponibles sur [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) et vous pouvez également récupérer des exemples de données à partir de vos propres entrées de flux de données via hello fonction d’exemples de données sur l’onglet d’entrées hello.</span><span class="sxs-lookup"><span data-stu-id="26858-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Entrée de requête](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="26858-131">Après avoir fermé la boîte de dialogue hello, votre requête sera exécutée sur les données de test hello et vous verrez des résultats hello bas hello de page de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="26858-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Résumé de la requête](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="26858-133">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="26858-133">Get help</span></span>
<span data-ttu-id="26858-134">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="26858-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="26858-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26858-135">Next steps</span></span>
* [<span data-ttu-id="26858-136">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="26858-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="26858-137">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26858-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="26858-138">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26858-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="26858-139">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26858-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="26858-140">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26858-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

