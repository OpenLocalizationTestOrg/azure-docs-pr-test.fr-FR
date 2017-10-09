---
title: "aaaTroubleshoot performances problèmes et optimiser votre base de données | Documents Microsoft"
description: "Appliquer tooyour de recommandations de performances de la base de données SQL ainsi effacer comment insights toogain sur hello les performances des requêtes hello sur votre base de données"
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
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="537f0-103">Résoudre les problèmes de performances et optimiser votre base de données</span><span class="sxs-lookup"><span data-stu-id="537f0-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="537f0-104">Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées.</span><span class="sxs-lookup"><span data-stu-id="537f0-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="537f0-105">Ce didacticiel vous apprend à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="537f0-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="537f0-106">Examiner, appliquer et annuler des recommandations en matière d’amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="537f0-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="537f0-107">Rechercher les requêtes utilisant beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="537f0-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="537f0-108">Rechercher les requêtes à exécution longue</span><span class="sxs-lookup"><span data-stu-id="537f0-108">Find long running queries</span></span>

> <span data-ttu-id="537f0-109">Vous avez besoin d’une charge de travail continue sur une base de données avec les problèmes de performances – manque un index, par exemple tooreceive une recommandation.</span><span class="sxs-lookup"><span data-stu-id="537f0-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="537f0-110">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="537f0-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="537f0-111">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="537f0-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="537f0-112">Examiner et appliquer une recommandation</span><span class="sxs-lookup"><span data-stu-id="537f0-112">Review and apply a recommendation</span></span>

<span data-ttu-id="537f0-113">Suivez ces étapes de tooapply une recommandation système hello pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="537f0-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="537f0-114">Cliquez sur hello **recommandations relatives aux performances** menu dans le panneau de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="537f0-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![recommandation sur les performances](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="537f0-116">Dans la liste hello des recommandations, sélectionnez une recommandation active.</span><span class="sxs-lookup"><span data-stu-id="537f0-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="537f0-117">Dans cet exemple, Créer un index.</span><span class="sxs-lookup"><span data-stu-id="537f0-117">In this example, Create Index.</span></span>

    ![sélectionner une recommandation](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="537f0-119">Appliquer la recommandation de hello en cliquant sur hello **appliquer** bouton.</span><span class="sxs-lookup"><span data-stu-id="537f0-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="537f0-120">Si vous le souhaitez, passez en revue les détails de la recommandation hello et consultez les script T-SQL de hello trop d’être exécuté en cliquant sur **afficher le Script** bouton.</span><span class="sxs-lookup"><span data-stu-id="537f0-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![appliquer une recommandation](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="537f0-122">[Facultatif] Activer le réglage automatique pour toobe recommandations appliquée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="537f0-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![réglage automatique](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="537f0-124">Annuler une recommandation</span><span class="sxs-lookup"><span data-stu-id="537f0-124">Revert a recommendation</span></span>

<span data-ttu-id="537f0-125">Hello Database Advisor analyse chaque recommandation implémentée.</span><span class="sxs-lookup"><span data-stu-id="537f0-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="537f0-126">Si une recommandation n’améliore pas la charge de travail hello que vont être annulée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="537f0-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="537f0-127">Vous avez la possibilité d’annuler manuellement une recommandation, mais cela n’est pas nécessaire la plupart du temps.</span><span class="sxs-lookup"><span data-stu-id="537f0-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="537f0-128">toorevert une recommandation :</span><span class="sxs-lookup"><span data-stu-id="537f0-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="537f0-129">Toohello performances recommandations menu Aller et sélectionnez une des recommandations de hello appliqué.</span><span class="sxs-lookup"><span data-stu-id="537f0-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![sélectionner une recommandation](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="537f0-131">Dans la vue des détails hello, cliquez sur **Revert**.</span><span class="sxs-lookup"><span data-stu-id="537f0-131">In hello details view, click **Revert**.</span></span>

    ![annuler une recommandation](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="537f0-133">Rechercher les requête hello qui consomme hello plus de ressources</span><span class="sxs-lookup"><span data-stu-id="537f0-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="537f0-134">Suivez ces requêtes de hello toofind étapes consommation hello plus de ressources :</span><span class="sxs-lookup"><span data-stu-id="537f0-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="537f0-135">Cliquez sur hello **Query Performance Insight** menu dans le panneau de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="537f0-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="537f0-137">Sélectionnez un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="537f0-137">Select a resource type.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="537f0-139">Sélectionnez la première requête de hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="537f0-139">Select hello first query in hello table.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="537f0-141">Passez en revue les détails de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="537f0-141">Review hello query details.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="537f0-143">Trouver la requête en cours d’exécution plus longue de hello</span><span class="sxs-lookup"><span data-stu-id="537f0-143">Find hello longest running query</span></span>

1. <span data-ttu-id="537f0-144">TooQuery Performance Insight, sélectionnez hello **longues requêtes** onglet.</span><span class="sxs-lookup"><span data-stu-id="537f0-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="537f0-146">Sélectionnez la première requête de hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="537f0-146">Select hello first query in hello table.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="537f0-148">Passez en revue les détails de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="537f0-148">Review hello query details.</span></span>

    ![analyse des requêtes](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="537f0-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="537f0-150">Next steps</span></span> 
<span data-ttu-id="537f0-151">Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées.</span><span class="sxs-lookup"><span data-stu-id="537f0-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="537f0-152">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="537f0-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="537f0-153">Examiner, appliquer et annuler des recommandations en matière d’amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="537f0-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="537f0-154">Rechercher les requêtes utilisant beaucoup de ressources</span><span class="sxs-lookup"><span data-stu-id="537f0-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="537f0-155">Rechercher les requêtes à exécution longue</span><span class="sxs-lookup"><span data-stu-id="537f0-155">Find long running queries</span></span>

[<span data-ttu-id="537f0-156">Conseils pour le réglage des performances de SQL Database</span><span class="sxs-lookup"><span data-stu-id="537f0-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
