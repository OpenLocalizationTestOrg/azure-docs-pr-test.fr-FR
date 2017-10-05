---
title: "Résoudre les problèmes de performances et optimiser votre base de données | Microsoft Docs"
description: "Appliquer des recommandations en matière de performances à votre SQL Database et apprendre à obtenir des informations sur les performances des requêtes s’exécutant sur votre base de données"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: f9ae96cdc80c347593f229cb2fce3f2d4d8e7caf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="b8a1e-103">Résoudre les problèmes de performances et optimiser votre base de données</span><span class="sxs-lookup"><span data-stu-id="b8a1e-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="b8a1e-104">Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b8a1e-105">Ce didacticiel vous apprend à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8a1e-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b8a1e-106">Examiner, appliquer et annuler des recommandations en matière d’amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="b8a1e-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b8a1e-107">Rechercher les requêtes utilisant beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="b8a1e-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b8a1e-108">Rechercher les requêtes à exécution longue</span><span class="sxs-lookup"><span data-stu-id="b8a1e-108">Find long running queries</span></span>

> <span data-ttu-id="b8a1e-109">Vous avez besoin d’une charge de travail continue sur une base de données rencontrant des problèmes de performances (p. ex. index manquant) pour obtenir une recommandation.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-109">You need a continuous workload on a database with performance issues – missing an index for example to receive a recommendation.</span></span>
>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="b8a1e-110">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-110">Log in to the Azure portal</span></span>

<span data-ttu-id="b8a1e-111">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b8a1e-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="b8a1e-112">Examiner et appliquer une recommandation</span><span class="sxs-lookup"><span data-stu-id="b8a1e-112">Review and apply a recommendation</span></span>

<span data-ttu-id="b8a1e-113">Suivez les étapes ci-dessous pour appliquer une recommandation du système à votre base de données :</span><span class="sxs-lookup"><span data-stu-id="b8a1e-113">Follow these steps to apply a recommendation from the system for your database:</span></span>

1. <span data-ttu-id="b8a1e-114">Cliquez sur le menu **Recommandations sur les performances** dans le panneau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-114">Click the **Performance recommendations** menu in the database blade.</span></span>

    ![recommandation sur les performances](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="b8a1e-116">Sélectionnez une recommandation active dans la liste des recommandations.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-116">From the list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="b8a1e-117">Dans cet exemple, Créer un index.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-117">In this example, Create Index.</span></span>

    ![sélectionner une recommandation](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="b8a1e-119">Appliquez la recommandation en cliquant sur le bouton **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-119">Apply the recommendation by clicking the **Apply** button.</span></span> <span data-ttu-id="b8a1e-120">Si vous le souhaitez, examinez les détails de la recommandation et consultez le script T-SQL à exécuter en cliquant sur le bouton **Afficher le script**.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-120">Optionally, review the recommendation details and see the T-SQL script to  be executed by clicking on **View Script** button.</span></span>

    ![appliquer une recommandation](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="b8a1e-122">[Facultatif] Activez le réglage automatique pour appliquer automatiquement des recommandations.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-122">[Optional] Enable automatic tuning for recommendations to be applied automatically.</span></span>

    ![réglage automatique](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="b8a1e-124">Annuler une recommandation</span><span class="sxs-lookup"><span data-stu-id="b8a1e-124">Revert a recommendation</span></span>

<span data-ttu-id="b8a1e-125">Database Advisor surveille chaque recommandation implémentée.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-125">The Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="b8a1e-126">Si une recommandation n’améliore pas la charge de travail, elle est automatiquement annulée.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-126">If a recommendation doesn't improve the workload it will be automatically reverted.</span></span> <span data-ttu-id="b8a1e-127">Vous avez la possibilité d’annuler manuellement une recommandation, mais cela n’est pas nécessaire la plupart du temps.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="b8a1e-128">Pour annuler une recommandation :</span><span class="sxs-lookup"><span data-stu-id="b8a1e-128">To revert a recommendation:</span></span>

1. <span data-ttu-id="b8a1e-129">Accédez au menu des recommandations sur les performances et sélectionnez l’une des recommandations appliquées.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-129">Go to the performance recommendations menu and select one of the applied recommendations.</span></span>

    ![sélectionner une recommandation](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="b8a1e-131">Dans la vue Détails, cliquez sur **Revenir**.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-131">In the details view, click **Revert**.</span></span>

    ![annuler une recommandation](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-the-query-that-consumes-the-most-resources"></a><span data-ttu-id="b8a1e-133">Rechercher la requête qui consomme le plus de ressources</span><span class="sxs-lookup"><span data-stu-id="b8a1e-133">Find the query that consumes the most resources</span></span>

<span data-ttu-id="b8a1e-134">Suivez les étapes ci-dessous pour rechercher la requête qui consomme le plus de ressources :</span><span class="sxs-lookup"><span data-stu-id="b8a1e-134">Follow these steps to find the query consuming the most resources:</span></span>

1. <span data-ttu-id="b8a1e-135">Cliquez sur le menu **Query Performance Insight** dans le panneau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-135">Click on the **Query Performance Insight** menu in the database blade.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="b8a1e-137">Sélectionnez un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-137">Select a resource type.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="b8a1e-139">Sélectionnez la première requête dans la table.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-139">Select the first query in the table.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="b8a1e-141">Examinez les détails de la requête.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-141">Review the query details.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-the-longest-running-query"></a><span data-ttu-id="b8a1e-143">Rechercher la requête dont l’exécution est la plus longue</span><span class="sxs-lookup"><span data-stu-id="b8a1e-143">Find the longest running query</span></span>

1. <span data-ttu-id="b8a1e-144">Accédez à Query Performance Insight et sélectionnez l’onglet **Requêtes longues**.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-144">Go to Query Performance Insight and select the **Long running queries** tab.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="b8a1e-146">Sélectionnez la première requête dans la table.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-146">Select the first query in the table.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="b8a1e-148">Examinez les détails de la requête.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-148">Review the query details.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="b8a1e-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8a1e-150">Next steps</span></span> 
<span data-ttu-id="b8a1e-151">Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées.</span><span class="sxs-lookup"><span data-stu-id="b8a1e-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="b8a1e-152">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b8a1e-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b8a1e-153">Examiner, appliquer et annuler des recommandations en matière d’amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="b8a1e-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="b8a1e-154">Rechercher les requêtes utilisant beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="b8a1e-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="b8a1e-155">Rechercher les requêtes à exécution longue</span><span class="sxs-lookup"><span data-stu-id="b8a1e-155">Find long running queries</span></span>

[<span data-ttu-id="b8a1e-156">Conseils pour le réglage des performances de SQL Database</span><span class="sxs-lookup"><span data-stu-id="b8a1e-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
