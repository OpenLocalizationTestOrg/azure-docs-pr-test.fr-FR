---
title: "Surveiller et améliorer les performances - Azure SQL Database | Microsoft Docs"
description: "La base de données SQL Azure fournit des outils de performances pour vous aider à identifier les zones susceptibles d’améliorer les performances actuelles des requêtes."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 522b932ab055978c52f085dbaa36095bb6b77962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="82f19-103">Surveiller et améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="82f19-103">Monitor and improve performance</span></span>
<span data-ttu-id="82f19-104">Azure SQL Database identifie les problèmes potentiels de votre base de données et recommande les actions susceptibles d’améliorer les performances de votre charge de travail en fournissant des recommandations et des actions de réglage intelligent.</span><span class="sxs-lookup"><span data-stu-id="82f19-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="82f19-105">Pour vérifier les performances de votre base de données, utilisez la vignette **Performances** de la page Présentation ou accédez à la section « Support + dépannage » :</span><span class="sxs-lookup"><span data-stu-id="82f19-105">To review your database performance, use the **Performance** tile on the Overview page, or navigate down to "Support + troubleshooting" section:</span></span>

   ![Afficher les performances](./media/sql-database-performance/entries.png)

<span data-ttu-id="82f19-107">Dans la section « Support + dépannage », vous pouvez utiliser les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="82f19-107">In the "Support + troubleshooting" section, you can use the following pages:</span></span>


1. <span data-ttu-id="82f19-108">[Vue d’ensemble des performances](#performance-overview) pour surveiller les performances de votre base de données ;</span><span class="sxs-lookup"><span data-stu-id="82f19-108">[Performance overview](#performance-overview) to monitor performance of your database.</span></span> 
2. <span data-ttu-id="82f19-109">[Recommandations sur les performances](#performance-recommendations) pour trouver des recommandations en termes de performances pouvant améliorer les performances de votre charge de travail ;</span><span class="sxs-lookup"><span data-stu-id="82f19-109">[Performance recommendations](#performance-recommendations) to find performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="82f19-110">[Analyse des performances des requêtes](#query-performance-insight) pour rechercher les principales requêtes consommatrices de ressources ;</span><span class="sxs-lookup"><span data-stu-id="82f19-110">[Query Performance Insight](#query-performance-insight) to find top resource consuming queries.</span></span>
4. <span data-ttu-id="82f19-111">[Paramétrage automatique](#automatic-tuning) pour permettre à Azure SQL Database d’optimiser automatiquement votre base de données.</span><span class="sxs-lookup"><span data-stu-id="82f19-111">[Automatic tuning](#automatic-tuning) to let Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="82f19-112">Vue d'ensemble des performances</span><span class="sxs-lookup"><span data-stu-id="82f19-112">Performance Overview</span></span>
<span data-ttu-id="82f19-113">Cette vue fournit un résumé des performances de votre base de données et vous aide à optimiser les performances et à résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="82f19-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Performances](./media/sql-database-performance/performance.png)

* <span data-ttu-id="82f19-115">La vignette **Recommandations** fournit une répartition des recommandations de paramétrage de votre base de données (les trois premières recommandations sont affichées s’il en existe plus).</span><span class="sxs-lookup"><span data-stu-id="82f19-115">The **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="82f19-116">La page **[Recommandations sur les performances](#performance-recommendations)** s’affiche si vous cliquez sur cette vignette.</span><span class="sxs-lookup"><span data-stu-id="82f19-116">Clicking this tile takes you to **[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="82f19-117">La vignette **Activité de paramétrage** fournit un résumé des actions de paramétrage en cours et terminées pour votre base de données, ce qui vous donne un aperçu rapide de l’historique des activités de paramétrage.</span><span class="sxs-lookup"><span data-stu-id="82f19-117">The **Tuning activity** tile provides a summary of the ongoing and completed tuning actions for your database, giving you a quick view into the history of tuning activity.</span></span> <span data-ttu-id="82f19-118">Cliquez sur cette vignette pour afficher l'historique de paramétrage complet de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="82f19-118">Clicking this tile takes you to the full tuning history view for your database.</span></span>
* <span data-ttu-id="82f19-119">La vignette **Paramétrage automatique** affiche la [configuration de paramétrage automatique](sql-database-automatic-tuning-enable.md) de votre base de données (options de paramétrage qui sont automatiquement appliquées à votre base de données).</span><span class="sxs-lookup"><span data-stu-id="82f19-119">The **Auto-tuning** tile shows the [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied to your database).</span></span> <span data-ttu-id="82f19-120">Cliquez sur cette vignette pour ouvrir la boîte de dialogue de configuration de l'automatisation.</span><span class="sxs-lookup"><span data-stu-id="82f19-120">Clicking this tile opens the automation configuration dialog.</span></span>
* <span data-ttu-id="82f19-121">La vignette **Requêtes de base de données** affiche le résumé des performances de requête de votre base de données (utilisation DTU globale et requêtes les plus consommatrices de ressources).</span><span class="sxs-lookup"><span data-stu-id="82f19-121">The **Database queries** tile shows the summary of the query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="82f19-122">La page **[Analyse des performances des requêtes](#query-performance-insight)** s’affiche si vous cliquez sur cette vignette.</span><span class="sxs-lookup"><span data-stu-id="82f19-122">Clicking this tile takes you to **[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="82f19-123">Recommandations en matière de performances</span><span class="sxs-lookup"><span data-stu-id="82f19-123">Performance recommendations</span></span>
<span data-ttu-id="82f19-124">Cette page fournit des [recommandations de réglage intelligent](sql-database-advisor.md) qui peuvent améliorer les performances de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="82f19-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="82f19-125">Les types de recommandations suivants sont affichés sur cette page :</span><span class="sxs-lookup"><span data-stu-id="82f19-125">The following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="82f19-126">Recommandations sur les index à créer ou à supprimer.</span><span class="sxs-lookup"><span data-stu-id="82f19-126">Recommendations on which indexes to create or drop.</span></span>
* <span data-ttu-id="82f19-127">Recommandations en cas de problèmes de schéma dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="82f19-127">Recommendations when schema issues are identified in the database.</span></span>
* <span data-ttu-id="82f19-128">Recommandations quand les requêtes peuvent tirer parti des requêtes paramétrables.</span><span class="sxs-lookup"><span data-stu-id="82f19-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Performances](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="82f19-130">Vous trouverez également un historique complet des actions de réglage qui ont été appliquées dans le passé.</span><span class="sxs-lookup"><span data-stu-id="82f19-130">You can also find complete history of tuning actions that were applied in the past.</span></span>

<span data-ttu-id="82f19-131">Découvrez comment rechercher et appliquer les recommandations relatives aux performances dans l’article [Rechercher et appliquer les recommandations en matière de performances](sql-database-advisor-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82f19-131">Learn how to find an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="82f19-132">Réglage automatique</span><span class="sxs-lookup"><span data-stu-id="82f19-132">Automatic tuning</span></span>
<span data-ttu-id="82f19-133">Azure SQL Database peut régler automatiquement les performances de base de données en appliquant les [recommandations relatives aux performances](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="82f19-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="82f19-134">Pour en savoir plus, voir l’article [Automatic tuning (Réglage automatique)](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="82f19-134">To learn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="82f19-135">Pour l’activer, lire [How to enable automatic tuning (Activation du réglage automatique)](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="82f19-135">To enable it, read [how to enable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="82f19-136">Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="82f19-136">Query Performance Insight</span></span>
<span data-ttu-id="82f19-137">[Query Performance Insight](sql-database-query-performance.md) vous permet de passer moins de temps à résoudre les problèmes de performances des bases de données en fournissant :</span><span class="sxs-lookup"><span data-stu-id="82f19-137">[Query Performance Insight](sql-database-query-performance.md) allows you to spend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="82f19-138">Une meilleure compréhension de la consommation des ressources des bases de données (DTU).</span><span class="sxs-lookup"><span data-stu-id="82f19-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="82f19-139">Les requêtes principales consommatrices d’UC peuvent être réglées pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="82f19-139">The top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="82f19-140">La possibilité d’examiner les détails d’une requête.</span><span class="sxs-lookup"><span data-stu-id="82f19-140">The ability to drill down into the details of a query.</span></span> 

  ![tableau de bord des performances](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="82f19-142">Pour plus d’informations sur cette page, voir l’article **[How to use Query Performance Insight (Utilisation de Query Performance Insight)](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="82f19-142">Find more information about this page in the article **[How to use Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82f19-143">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="82f19-143">Additional resources</span></span>
* [<span data-ttu-id="82f19-144">Guide des performances de base de données SQL Azure pour les bases de données uniques</span><span class="sxs-lookup"><span data-stu-id="82f19-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="82f19-145">Quand utiliser un pool élastique ?</span><span class="sxs-lookup"><span data-stu-id="82f19-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

