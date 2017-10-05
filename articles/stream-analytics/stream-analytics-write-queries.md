---
title: "Écrire des requêtes dans Stream Analytics | Microsoft Docs"
description: "Écrire des requêtes dans Stream Analytics et interroger des données | segment du parcours d’apprentissage."
keywords: "comment écrire des requêtes, données de requête, écrire une requête, écriture de requêtes"
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
ms.openlocfilehash: b44b0658a06761a805708e7fdeba9e3b2cf9d3ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-write-queries-in-stream-analytics"></a><span data-ttu-id="6602e-104">Écriture de requêtes dans Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6602e-104">How to write queries in Stream Analytics</span></span>
<span data-ttu-id="6602e-105">Une requête de logique de traitement de flux écrite dans Azure Stream Analytics est implémentée en tant que « requête active ». Celle-ci est définie avant que la tâche ne démarre et exécutée sur les données au moment où celles-ci atteignent la tâche.</span><span class="sxs-lookup"><span data-stu-id="6602e-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span></span> <span data-ttu-id="6602e-106">La transformation des données est exprimée dans un langage de requête semblable à SQL, qui est principalement un sous-ensemble de T-SQL avec certaines extensions de langage ajoutées, comme [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) qui est utilisé pour exprimer la sémantique temporelle.</span><span class="sxs-lookup"><span data-stu-id="6602e-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="6602e-107">Écriture de requêtes :</span><span class="sxs-lookup"><span data-stu-id="6602e-107">Writing Queries:</span></span>
1. <span data-ttu-id="6602e-108">Dans votre tâche Stream Analytics dans le portail de gestion Azure, cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="6602e-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span></span>
   
    ![Sélection d'une requête](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="6602e-110">Dans le portail Azure, cliquez sur **Requête**.</span><span class="sxs-lookup"><span data-stu-id="6602e-110">In the Azure Portal, click **Query**.</span></span>
   
    ![Sélection d’un aperçu de requête](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="6602e-112">Les nouvelles tâches disposent d'un modèle de requête pour vous aider à commencer.</span><span class="sxs-lookup"><span data-stu-id="6602e-112">New jobs have a query template to help get you started.</span></span> <span data-ttu-id="6602e-113">Le modèle de requête effectue une requête « pass-through » qui transfère tous les champs provenant d'événements d'entrée vers la sortie.</span><span class="sxs-lookup"><span data-stu-id="6602e-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span></span>  
   
   * <span data-ttu-id="6602e-114">Si vous avez défini au moins une entrée et une sortie pour votre tâche, vous pouvez remplacer les champs « [YourOutputAlias] » et « [YourInputAlias] » d'espace réservé par les alias de l'entrée et de la sortie que vous souhaitez utiliser en premier.</span><span class="sxs-lookup"><span data-stu-id="6602e-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span></span> <span data-ttu-id="6602e-115">En outre, vous pouvez toujours créer et tester votre requête dans le portail Azure Classic sans définir d'entrées et de sorties pour la tâche.</span><span class="sxs-lookup"><span data-stu-id="6602e-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span></span>
   * <span data-ttu-id="6602e-116">Si vous souhaitez effectuer un traitement supérieur à une simple opération « pass-through », vous pouvez modifier la définition de la requête.</span><span class="sxs-lookup"><span data-stu-id="6602e-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span></span> <span data-ttu-id="6602e-117">Pour vous familiariser avec la création de requêtes, examinez les modèles de requête courants illustrés [ici](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="6602e-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Fenêtre Données de requête](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a><span data-ttu-id="6602e-119">Pour vérifier le bon fonctionnement des données de requête :</span><span class="sxs-lookup"><span data-stu-id="6602e-119">To validate query data is working:</span></span>
<span data-ttu-id="6602e-120">Vous pouvez vérifier que votre requête se comporte comme prévu en l'exécutant dans le navigateur sur un ou plusieurs fichiers JSON locaux contenant des données de test.</span><span class="sxs-lookup"><span data-stu-id="6602e-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="6602e-121">Ceci ne démarre pas la tâche et n'a aucune incidence sur la facturation.</span><span class="sxs-lookup"><span data-stu-id="6602e-121">This will not start the job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="6602e-122">Actuellement, le portail Azure ne prend pas en charge le test d’une requête dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="6602e-122">Currently in-browser query testing is not supported in the Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="6602e-123">Assurez-vous que la requête ne contient pas d'erreur (sinon, le bouton Test sera désactivé), puis cliquez sur le bouton Test.</span><span class="sxs-lookup"><span data-stu-id="6602e-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span></span>  
   
   ![Test des données de requête](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="6602e-125">Vous devrez spécifier des fichiers pour chacune des entrées référencées dans la requête.</span><span class="sxs-lookup"><span data-stu-id="6602e-125">You will be prompted to specify files for each of the inputs referenced in the query.</span></span> <span data-ttu-id="6602e-126">Dans cet exemple, le modèle de requête est laissé tel quel, donc la boîte de dialogue demande une entrée nommée « yourinputalias ».</span><span class="sxs-lookup"><span data-stu-id="6602e-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Tester les données de requête](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="6602e-128">Accédez à un fichier de test.</span><span class="sxs-lookup"><span data-stu-id="6602e-128">Browse to a test file.</span></span> <span data-ttu-id="6602e-129">Plusieurs exemples de fichiers sont disponibles sur [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) et vous pouvez également récupérer des données d’exemple à partir de vos propres entrées de flux de données avec la fonction Exemples de données de l’onglet des entrées.</span><span class="sxs-lookup"><span data-stu-id="6602e-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span></span>  
   
   ![Entrée de requête](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="6602e-131">Après avoir fermé la boîte de dialogue, votre requête sera exécutée sur les données de test et les résultats s'afficheront au bas de la page de requête.</span><span class="sxs-lookup"><span data-stu-id="6602e-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span></span>  
   
   ![Résumé de la requête](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="6602e-133">Obtenir de l'aide</span><span class="sxs-lookup"><span data-stu-id="6602e-133">Get help</span></span>
<span data-ttu-id="6602e-134">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6602e-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6602e-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6602e-135">Next steps</span></span>
* [<span data-ttu-id="6602e-136">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6602e-136">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6602e-137">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6602e-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6602e-138">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6602e-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6602e-139">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6602e-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6602e-140">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6602e-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

