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
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a>Résoudre les problèmes de performances et optimiser votre base de données

Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées. Ce didacticiel vous apprend à effectuer les opérations suivantes :
> [!div class="checklist"]
> * Examiner, appliquer et annuler des recommandations en matière d’amélioration des performances
> * Rechercher les requêtes utilisant beaucoup de ressources
> * Rechercher les requêtes à exécution longue

> Vous avez besoin d’une charge de travail continue sur une base de données avec les problèmes de performances – manque un index, par exemple tooreceive une recommandation.
>

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

## <a name="review-and-apply-a-recommendation"></a>Examiner et appliquer une recommandation

Suivez ces étapes de tooapply une recommandation système hello pour votre base de données :

1. Cliquez sur hello **recommandations relatives aux performances** menu dans le panneau de base de données hello.

    ![recommandation sur les performances](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. Dans la liste hello des recommandations, sélectionnez une recommandation active. Dans cet exemple, Créer un index.

    ![sélectionner une recommandation](./media/sql-database-performance-tutorial/create_index.png)

3. Appliquer la recommandation de hello en cliquant sur hello **appliquer** bouton. Si vous le souhaitez, passez en revue les détails de la recommandation hello et consultez les script T-SQL de hello trop d’être exécuté en cliquant sur **afficher le Script** bouton.

    ![appliquer une recommandation](./media/sql-database-performance-tutorial/apply.png)

4. [Facultatif] Activer le réglage automatique pour toobe recommandations appliquée automatiquement.

    ![réglage automatique](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a>Annuler une recommandation

Hello Database Advisor analyse chaque recommandation implémentée. Si une recommandation n’améliore pas la charge de travail hello que vont être annulée automatiquement. Vous avez la possibilité d’annuler manuellement une recommandation, mais cela n’est pas nécessaire la plupart du temps. toorevert une recommandation :

1. Toohello performances recommandations menu Aller et sélectionnez une des recommandations de hello appliqué.

    ![sélectionner une recommandation](./media/sql-database-performance-tutorial/select.png)

2. Dans la vue des détails hello, cliquez sur **Revert**.

    ![annuler une recommandation](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a>Rechercher les requête hello qui consomme hello plus de ressources

Suivez ces requêtes de hello toofind étapes consommation hello plus de ressources :

1. Cliquez sur hello **Query Performance Insight** menu dans le panneau de base de données hello.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. Sélectionnez un type de ressource.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_resource_type.png)

3. Sélectionnez la première requête de hello dans la table de hello.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_query.png)

4. Passez en revue les détails de la requête hello.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a>Trouver la requête en cours d’exécution plus longue de hello

1. TooQuery Performance Insight, sélectionnez hello **longues requêtes** onglet.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/long_running.png)

3. Sélectionnez la première requête de hello dans la table de hello.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/select_first_query.png)

4. Passez en revue les détails de la requête hello.

    ![analyse des requêtes](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a>Étapes suivantes 
Des index manquants et des requêtes incorrectement optimisées sont souvent à l’origine de performances de base de données limitées. Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :
> [!div class="checklist"]
> * Examiner, appliquer et annuler des recommandations en matière d’amélioration des performances
> * Rechercher les requêtes utilisant beaucoup de ressources
> * Rechercher les requêtes à exécution longue

[Conseils pour le réglage des performances de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
