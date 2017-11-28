---
title: "aaaMonitor et améliorer les performances - base de données SQL Azure | Documents Microsoft"
description: "Hello, que base de données SQL Azure offre des performances des outils toohelp vous identifiez les zones qui peuvent améliorer les performances des requêtes en cours."
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
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="4d227-103">Surveiller et améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="4d227-103">Monitor and improve performance</span></span>
<span data-ttu-id="4d227-104">Azure SQL Database identifie les problèmes potentiels de votre base de données et recommande les actions susceptibles d’améliorer les performances de votre charge de travail en fournissant des recommandations et des actions de réglage intelligent.</span><span class="sxs-lookup"><span data-stu-id="4d227-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="4d227-105">tooreview vos performances de la base de données, les utilisez hello **performances** vignette sur la page de vue d’ensemble de hello ou naviguez vers le bas trop « Prise en charge + dépannage » section :</span><span class="sxs-lookup"><span data-stu-id="4d227-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Afficher les performances](./media/sql-database-performance/entries.png)

<span data-ttu-id="4d227-107">Dans la section de hello « Prise en charge + dépannage », vous pouvez utiliser hello suivant pages :</span><span class="sxs-lookup"><span data-stu-id="4d227-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="4d227-108">[Vue d’ensemble des performances](#performance-overview) toomonitor les performances de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4d227-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="4d227-109">[Recommandations relatives aux performances](#performance-recommendations) recommandations relatives aux performances toofind qui peut améliorer les performances de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="4d227-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="4d227-110">[Query Performance Insight](#query-performance-insight) principales requêtes consommatrices de ressources toofind.</span><span class="sxs-lookup"><span data-stu-id="4d227-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="4d227-111">[Le paramétrage automatique](#automatic-tuning) toolet base de données SQL Azure optimiser automatiquement votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4d227-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="4d227-112">Vue d'ensemble des performances</span><span class="sxs-lookup"><span data-stu-id="4d227-112">Performance Overview</span></span>
<span data-ttu-id="4d227-113">Cette vue fournit un résumé des performances de votre base de données et vous aide à optimiser les performances et à résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="4d227-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Performances](./media/sql-database-performance/performance.png)

* <span data-ttu-id="4d227-115">Hello **recommandations** vignette fournit une décomposition des recommandations pour votre base de données de paramétrage (recommandations les trois premières sont affichées s’il existe plusieurs).</span><span class="sxs-lookup"><span data-stu-id="4d227-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="4d227-116">Cliquez sur cette vignette pour accéder trop**[recommandations relatives aux performances](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="4d227-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="4d227-117">Hello **paramétrage activité** vignette fournit un résumé de hello en cours et terminée de réglage des actions pour votre base de données, ce qui vous donne un aperçu rapide de l’historique de hello du paramétrage d’activité.</span><span class="sxs-lookup"><span data-stu-id="4d227-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="4d227-118">Cliquez sur cette vignette pour accéder toohello complète réglage d’affichage de l’historique de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4d227-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="4d227-119">Hello **réglage automatique** vignette affiche hello [réglage automatique de la configuration](sql-database-automatic-tuning-enable.md) pour votre base de données (options d’analyse qui sont automatiquement appliqués tooyour de base de données).</span><span class="sxs-lookup"><span data-stu-id="4d227-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="4d227-120">En cliquant sur cette vignette ouvre la boîte de dialogue de configuration hello automation.</span><span class="sxs-lookup"><span data-stu-id="4d227-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="4d227-121">Hello **les requêtes de base de données** vignette affiche hello résumé des performances des requêtes hello pour votre base de données (globale DTU d’utilisation et haut requêtes consommatrices de ressources).</span><span class="sxs-lookup"><span data-stu-id="4d227-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="4d227-122">Cliquez sur cette vignette pour accéder trop**[Query Performance Insight](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="4d227-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="4d227-123">Recommandations en matière de performances</span><span class="sxs-lookup"><span data-stu-id="4d227-123">Performance recommendations</span></span>
<span data-ttu-id="4d227-124">Cette page fournit des [recommandations de réglage intelligent](sql-database-advisor.md) qui peuvent améliorer les performances de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4d227-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="4d227-125">Hello les types de recommandations suivants s’affichent sur cette page :</span><span class="sxs-lookup"><span data-stu-id="4d227-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="4d227-126">Recommandations sur les index toocreate ou les déplacer.</span><span class="sxs-lookup"><span data-stu-id="4d227-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="4d227-127">Recommandations de problèmes de schéma sont identifiées dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4d227-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="4d227-128">Recommandations quand les requêtes peuvent tirer parti des requêtes paramétrables.</span><span class="sxs-lookup"><span data-stu-id="4d227-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Performances](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="4d227-130">Vous trouverez également un historique complet des actions qui ont été appliquées dans hello en cours de paramétrage.</span><span class="sxs-lookup"><span data-stu-id="4d227-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="4d227-131">En savoir comment toofind un appliquer les recommandations relatives aux performances dans [trouver et appliquer les recommandations relatives aux performances](sql-database-advisor-portal.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4d227-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="4d227-132">Réglage automatique</span><span class="sxs-lookup"><span data-stu-id="4d227-132">Automatic tuning</span></span>
<span data-ttu-id="4d227-133">Azure SQL Database peut régler automatiquement les performances de base de données en appliquant les [recommandations relatives aux performances](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="4d227-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="4d227-134">toolearn plus, lisez [article Paramétrage automatique](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="4d227-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="4d227-135">tooenable, lecture [comment le paramétrage automatique tooenable](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="4d227-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="4d227-136">Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="4d227-136">Query Performance Insight</span></span>
<span data-ttu-id="4d227-137">[Query Performance Insight](sql-database-query-performance.md) permet toospend moins de temps résolution des problèmes de performances de la base de données en fournissant :</span><span class="sxs-lookup"><span data-stu-id="4d227-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="4d227-138">Une meilleure compréhension de la consommation des ressources des bases de données (DTU).</span><span class="sxs-lookup"><span data-stu-id="4d227-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="4d227-139">Hello processeur supérieure consomme des requêtes, qui peuvent potentiellement être paramétrées pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="4d227-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="4d227-140">Bonjour capacité toodrill vers le bas dans les détails de hello d’une requête.</span><span class="sxs-lookup"><span data-stu-id="4d227-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![tableau de bord des performances](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="4d227-142">Trouver plus d’informations sur cette page dans l’article de hello  **[comment toouse Query Performance Insight](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="4d227-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4d227-143">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4d227-143">Additional resources</span></span>
* [<span data-ttu-id="4d227-144">Guide des performances de base de données SQL Azure pour les bases de données uniques</span><span class="sxs-lookup"><span data-stu-id="4d227-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="4d227-145">Quand utiliser un pool élastique ?</span><span class="sxs-lookup"><span data-stu-id="4d227-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

