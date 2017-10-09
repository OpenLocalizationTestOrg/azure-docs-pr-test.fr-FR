---
title: "analyse des performances pour la base de données SQL Azure aaaQuery | Documents Microsoft"
description: "Analyse des performances des requêtes identifie hello consommation d’UC de la plupart des requêtes pour une base de données SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="45ea5-103">Query Performance Insight pour base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="45ea5-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="45ea5-104">La gestion et de réglage des performances de hello de bases de données relationnelles sont une tâche complexe qui nécessite des compétences importantes et nécessite beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="45ea5-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="45ea5-105">Query Performance Insight vous permet de toospend moins de temps résolution des problèmes de performances de la base de données en fournissant les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="45ea5-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="45ea5-106">Une meilleure compréhension de la consommation des ressources des bases de données (DTU).</span><span class="sxs-lookup"><span data-stu-id="45ea5-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="45ea5-107">Hello premières requêtes par le nombre d’UC ou durée/de l’exécution, qui peuvent potentiellement être paramétrées pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="45ea5-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="45ea5-108">Hello capacité toodrill vers le bas dans les détails de hello d’une requête, afficher son texte et son historique d’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="45ea5-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="45ea5-109">Des annotations de réglage des performances qui indiquent les actions effectuées par [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="45ea5-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="45ea5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="45ea5-110">Prerequisites</span></span>
* <span data-ttu-id="45ea5-111">Query Performance Insight nécessite que le [magasin de requêtes](https://msdn.microsoft.com/library/dn817826.aspx) soit actif sur votre base de données.</span><span class="sxs-lookup"><span data-stu-id="45ea5-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="45ea5-112">Si le magasin de requêtes n’est pas en cours d’exécution, le portail de hello vous invite tooturn sur.</span><span class="sxs-lookup"><span data-stu-id="45ea5-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="45ea5-113">Autorisations</span><span class="sxs-lookup"><span data-stu-id="45ea5-113">Permissions</span></span>
<span data-ttu-id="45ea5-114">suivant de Hello [contrôle d’accès basé sur le rôle](../active-directory/role-based-access-control-what-is.md) autorisations sont requise toouse Query Performance Insight :</span><span class="sxs-lookup"><span data-stu-id="45ea5-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="45ea5-115">**Lecteur**, **propriétaire**, **collaborateur**, **collaborateur de base de données SQL**, ou **SQL Server collaborateur** sont des autorisations tooview requis hello principales consommatrices de ressources des requêtes et des graphiques.</span><span class="sxs-lookup"><span data-stu-id="45ea5-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="45ea5-116">**Propriétaire**, **collaborateur**, **collaborateur de base de données SQL**, ou **SQL Server collaborateur** autorisations sont requises tooview texte de la requête.</span><span class="sxs-lookup"><span data-stu-id="45ea5-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="45ea5-117">Utilisation de Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="45ea5-117">Using Query Performance Insight</span></span>
<span data-ttu-id="45ea5-118">Query Performance Insight est facile toouse :</span><span class="sxs-lookup"><span data-stu-id="45ea5-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="45ea5-119">Ouvrez [portail Azure](https://portal.azure.com/) et base de données de recherche que vous souhaitez tooexamine.</span><span class="sxs-lookup"><span data-stu-id="45ea5-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="45ea5-120">Dans le menu de gauche, sous Support et dépannage, sélectionnez « Query Performance Insight ».</span><span class="sxs-lookup"><span data-stu-id="45ea5-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="45ea5-121">Sur le premier onglet de hello, examinez la liste hello des principales requêtes consommatrices de ressources.</span><span class="sxs-lookup"><span data-stu-id="45ea5-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="45ea5-122">Sélectionnez une requête individuelle de tooview ses détails.</span><span class="sxs-lookup"><span data-stu-id="45ea5-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="45ea5-123">Ouvrez [SQL Azure Database Advisor](sql-database-advisor.md) , puis regardez si des recommandations sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="45ea5-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="45ea5-124">Utiliser des curseurs ou zoom toochange icônes observé intervalle.</span><span class="sxs-lookup"><span data-stu-id="45ea5-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![tableau de bord des performances](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="45ea5-126">Quelques heures de données doit toobe capturée par le magasin de requêtes pour l’analyse des performances des requêtes de base de données SQL tooprovide.</span><span class="sxs-lookup"><span data-stu-id="45ea5-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="45ea5-127">Si la base de données hello ne comporte aucune activité ou magasin de requêtes n’était pas actif pendant une période donnée, les graphiques de hello sera vides lors de l’affichage de cette période.</span><span class="sxs-lookup"><span data-stu-id="45ea5-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="45ea5-128">Vous pouvez activer Query Store à tout moment s’il n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="45ea5-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="45ea5-129">Consultez les requêtes principales consommatrices d’UC</span><span class="sxs-lookup"><span data-stu-id="45ea5-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="45ea5-130">Bonjour [portal](http://portal.azure.com) hello suivant :</span><span class="sxs-lookup"><span data-stu-id="45ea5-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="45ea5-131">Parcourir la base de données SQL tooa et cliquez sur **tous les paramètres** > **prise en charge + dépannage** > **analyse des performances de requête**.</span><span class="sxs-lookup"><span data-stu-id="45ea5-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Query Performance Insight][1]
   
    <span data-ttu-id="45ea5-133">affichage des requêtes principales Hello s’ouvre et premières requêtes de consommation UC hello sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="45ea5-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="45ea5-134">Cliquez sur le graphique hello pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="45ea5-134">Click around hello chart for details.</span></span><br><span data-ttu-id="45ea5-135">Hello ligne supérieure affiche % DTU global pour la base de données hello, tandis que les barres de hello affichent % processeur utilisé par les requêtes hello sélectionné pendant l’intervalle sélectionné de hello (par exemple, si **semaine** est sélectionné chaque barre représente un jour).</span><span class="sxs-lookup"><span data-stu-id="45ea5-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![principales requêtes][2]
   
    <span data-ttu-id="45ea5-137">grille de bas Hello représente des informations agrégées pour les requêtes visible hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="45ea5-138">ID de requête : identificateur unique de la requête dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="45ea5-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="45ea5-139">UC par requête pendant l’intervalle observable (dépend de la fonction d’agrégation).</span><span class="sxs-lookup"><span data-stu-id="45ea5-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="45ea5-140">Durée par requête (dépend de la fonction d’agrégation).</span><span class="sxs-lookup"><span data-stu-id="45ea5-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="45ea5-141">Nombre total d’exécutions pour une requête particulière.</span><span class="sxs-lookup"><span data-stu-id="45ea5-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="45ea5-142">Activez ou désactivez des requêtes individuelles tooinclude ou les exclure de graphique de hello à l’aide de cases à cocher.</span><span class="sxs-lookup"><span data-stu-id="45ea5-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="45ea5-143">Si vos données devient obsolètes, cliquez sur hello **Actualiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="45ea5-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="45ea5-144">Vous pouvez utiliser des curseurs et l’intervalle d’observation de zoom boutons toochange et examiner les pics : ![paramètres](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="45ea5-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="45ea5-145">Si vous souhaitez un affichage différent, vous pouvez également sélectionner l’onglet **Personnalisé** et définir :</span><span class="sxs-lookup"><span data-stu-id="45ea5-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="45ea5-146">la mesure (UC, Durée, Nombre d’exécutions) ;</span><span class="sxs-lookup"><span data-stu-id="45ea5-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="45ea5-147">l’intervalle de temps (Dernières 24 heures, Semaine dernière, Mois dernier) ;</span><span class="sxs-lookup"><span data-stu-id="45ea5-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="45ea5-148">le nombre de requêtes ;</span><span class="sxs-lookup"><span data-stu-id="45ea5-148">Number of queries.</span></span>
   * <span data-ttu-id="45ea5-149">la fonction d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-149">Aggregation function.</span></span>
     
     ![Paramètres](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="45ea5-151">Affichage des détails d’une requête individuelle</span><span class="sxs-lookup"><span data-stu-id="45ea5-151">Viewing individual query details</span></span>
<span data-ttu-id="45ea5-152">Détails de la requête tooview :</span><span class="sxs-lookup"><span data-stu-id="45ea5-152">tooview query details:</span></span>

1. <span data-ttu-id="45ea5-153">Cliquez sur une requête dans la liste hello des premières requêtes.</span><span class="sxs-lookup"><span data-stu-id="45ea5-153">Click any query in hello list of top queries.</span></span>
   
    ![détails](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="45ea5-155">affichage des détails Hello s’ouvre et nombre de consommation ou durée/de l’exécution de processeurs de requêtes hello est divisé au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="45ea5-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="45ea5-156">Cliquez sur le graphique hello pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="45ea5-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="45ea5-157">Graphique supérieure montre la ligne avec global % DTU de base de données, et les barres de hello sont % processeur consommé par la requête sélectionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="45ea5-158">Le deuxième graphique montre la durée totale par requête hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="45ea5-159">Graphique de bas indique le nombre total d’exécutions par requête sélectionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![détails de la requête][3]
4. <span data-ttu-id="45ea5-161">Si vous le souhaitez, utiliser des curseurs, boutons de zoom ou cliquez sur **paramètres** toocustomize affichage des données de la requête ou toopick une période de temps différent.</span><span class="sxs-lookup"><span data-stu-id="45ea5-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="45ea5-162">Révision des requêtes principales par durée</span><span class="sxs-lookup"><span data-stu-id="45ea5-162">Review top queries per duration</span></span>
<span data-ttu-id="45ea5-163">Dans la mise à jour de la récente hello de Query Performance Insight, nous avons introduit deux nouvelles mesures qui peuvent vous aider à identifier les goulots d’étranglement potentiels : nombre de durée et de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="45ea5-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="45ea5-164">Requêtes longues ont hello plus grande pour plus de ressources de verrouillage, de bloquer d’autres utilisateurs et de limiter l’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="45ea5-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="45ea5-165">Ils sont également hello meilleurs éléments pour l’optimisation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="45ea5-166">tooidentify les longues requêtes :</span><span class="sxs-lookup"><span data-stu-id="45ea5-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="45ea5-167">Ouvrez l’onglet **Personnalisé** dans Query Performance Insight pour la base de données sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="45ea5-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="45ea5-168">Modifier les mesures toobe **durée**</span><span class="sxs-lookup"><span data-stu-id="45ea5-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="45ea5-169">Sélectionner le nombre de requêtes et l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="45ea5-170">Sélectionnez la fonction d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="45ea5-171">**Somme** calcule le temps d’exécution total de toutes les requêtes pendant tout l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="45ea5-172">**Max** recherche le temps d’exécution maximum pendant l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="45ea5-173">**AVG** trouve durée moyenne d’exécution de toutes les exécutions de requête et vous montrent hello haut hors ces moyennes.</span><span class="sxs-lookup"><span data-stu-id="45ea5-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![durée de la requête][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="45ea5-175">Révision des requêtes principales par nombre d’exécutions</span><span class="sxs-lookup"><span data-stu-id="45ea5-175">Review top queries per execution count</span></span>
<span data-ttu-id="45ea5-176">Un nombre élevé d’exécutions peut ne pas affecter la base de données elle-même et l’utilisation de ressources peut être faible, mais l’application globale peut devenir lente.</span><span class="sxs-lookup"><span data-stu-id="45ea5-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="45ea5-177">Dans certains cas, le nombre d’exécutions très élevé peut entraîner des tooincrease du réseau les allers-retours.</span><span class="sxs-lookup"><span data-stu-id="45ea5-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="45ea5-178">Les allers-retours affectent considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="45ea5-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="45ea5-179">Elles sont une latence toonetwork sujet et latence du serveur toodownstream.</span><span class="sxs-lookup"><span data-stu-id="45ea5-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="45ea5-180">Par exemple, de nombreux piloté par les données de sites Web accéder largement à base de hello pour chaque demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="45ea5-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="45ea5-181">Durant le regroupement de connexions permet, hello augmenté le trafic réseau et la charge de traitement sur le serveur de base de données hello peuvent nuire aux performances.</span><span class="sxs-lookup"><span data-stu-id="45ea5-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="45ea5-182">Conseils généraux sont tookeep round allers-retours tooan strict minimum.</span><span class="sxs-lookup"><span data-stu-id="45ea5-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="45ea5-183">tooidentify exécutées fréquemment des requêtes de requêtes (« bavardes ») :</span><span class="sxs-lookup"><span data-stu-id="45ea5-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="45ea5-184">Ouvrez l’onglet **Personnalisé** dans Query Performance Insight pour la base de données sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="45ea5-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="45ea5-185">Modifier les mesures toobe **le nombre d’exécutions**</span><span class="sxs-lookup"><span data-stu-id="45ea5-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="45ea5-186">Sélectionner le nombre de requêtes et l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="45ea5-186">Select number of queries and observation interval</span></span>
   
    ![nombre d’exécutions de la requête][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="45ea5-188">Présentation des annotations de réglage des performances</span><span class="sxs-lookup"><span data-stu-id="45ea5-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="45ea5-189">Lors de l’exploration dans Query Performance Insight votre charge de travail, vous pouvez remarquer des icônes avec une ligne verticale sur le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="45ea5-190">Ces icônes sont des annotations. Elles représentent les performances qui affectent les actions effectuées par [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="45ea5-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="45ea5-191">Annotation de pointage, vous obtenez des informations de base sur l’action de hello :</span><span class="sxs-lookup"><span data-stu-id="45ea5-191">By hovering annotation, you get basic information about hello action:</span></span>

![annotation de requête][6]

<span data-ttu-id="45ea5-193">Si vous souhaitez tooknow plus ou appliquez les recommandations de l’Assistant, cliquez sur icône de hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="45ea5-194">Les détails de l’action s’ouvrent.</span><span class="sxs-lookup"><span data-stu-id="45ea5-194">It will open details of action.</span></span> <span data-ttu-id="45ea5-195">S’il s’agit d’une recommandation active, vous pouvez l’appliquer directement à l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="45ea5-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![détails d’annotation de requête][7]

### <a name="multiple-annotations"></a><span data-ttu-id="45ea5-197">Annotations multiples.</span><span class="sxs-lookup"><span data-stu-id="45ea5-197">Multiple annotations.</span></span>
<span data-ttu-id="45ea5-198">Il est possible qu’en raison du niveau de zoom, fermer tooeach autres annotations seront obtenir réduites en une seule.</span><span class="sxs-lookup"><span data-stu-id="45ea5-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="45ea5-199">Une icône spéciale s’affiche alors. Si vous cliquez dessus, un panneau s’ouvre, qui contient une liste d’annotations groupées.</span><span class="sxs-lookup"><span data-stu-id="45ea5-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="45ea5-200">Corrélation des requêtes et des actions de réglage des performances peut aider toobetter votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="45ea5-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="45ea5-201">Optimisation de la configuration du magasin de requêtes hello pour Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="45ea5-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="45ea5-202">Pendant votre utilisation de Query Performance Insight, vous pouvez rencontrer hello suivant des messages du magasin de requêtes :</span><span class="sxs-lookup"><span data-stu-id="45ea5-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="45ea5-203">« Le magasin de requête n’est pas correctement configuré dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="45ea5-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="45ea5-204">Cliquez ici toolearn plus. »</span><span class="sxs-lookup"><span data-stu-id="45ea5-204">Click here toolearn more."</span></span>
* <span data-ttu-id="45ea5-205">« Le magasin de requête n’est pas correctement configuré dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="45ea5-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="45ea5-206">Cliquez ici les paramètres toochange. »</span><span class="sxs-lookup"><span data-stu-id="45ea5-206">Click here toochange settings."</span></span> 

<span data-ttu-id="45ea5-207">Ces messages apparaissent généralement lorsque le magasin de requêtes n’est pas en mesure de toocollect de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="45ea5-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="45ea5-208">Le premier cas se produit lorsque le magasin de requêtes est en mode Lecture seule et si les paramètres sont définis de façon optimale.</span><span class="sxs-lookup"><span data-stu-id="45ea5-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="45ea5-209">Vous pouvez résoudre ce problème en augmentant la taille du magasin de requêtes ou en le nettoyant.</span><span class="sxs-lookup"><span data-stu-id="45ea5-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![bouton qds][8]

<span data-ttu-id="45ea5-211">Le deuxième cas se produit lorsque le magasin de requêtes est désactivé ou si les paramètres ne sont pas définis de façon optimale.</span><span class="sxs-lookup"><span data-stu-id="45ea5-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="45ea5-212">Vous pouvez modifier hello de rétention et de Capture de stratégie et d’activer le magasin de requêtes en exécutant les commandes ci-dessous, ou directement à partir de portail :</span><span class="sxs-lookup"><span data-stu-id="45ea5-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![bouton qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="45ea5-214">Stratégie de rétention et de capture recommandée</span><span class="sxs-lookup"><span data-stu-id="45ea5-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="45ea5-215">Il existe deux types de stratégies de rétention :</span><span class="sxs-lookup"><span data-stu-id="45ea5-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="45ea5-216">Taille en fonction - si tooAUTO ensemble il sera nettoyer les données automatiquement vers la taille maximale est atteinte.</span><span class="sxs-lookup"><span data-stu-id="45ea5-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="45ea5-217">Heure - par défaut, nous allons la définir too30 jours, ce qui signifie que, si le magasin de requêtes manquiez d’espace, elle supprimera interroger les informations datant de plus de 30 jours</span><span class="sxs-lookup"><span data-stu-id="45ea5-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="45ea5-218">La stratégie de capture peut avoir les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="45ea5-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="45ea5-219">**Tout** : toutes les requêtes sont capturées.</span><span class="sxs-lookup"><span data-stu-id="45ea5-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="45ea5-220">**Auto** : les requêtes peu fréquentes et les requêtes avec une durée de compilation et d’exécution insignifiante sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="45ea5-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="45ea5-221">Les seuils concernant le nombre d’exécutions, et la durée de compilation et d’exécution, sont déterminés en interne.</span><span class="sxs-lookup"><span data-stu-id="45ea5-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="45ea5-222">Il s’agit d’option par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-222">This is hello default option.</span></span>
* <span data-ttu-id="45ea5-223">**Aucune** : le magasin de requêtes arrête la capture de nouvelles requêtes, mais les statistiques d’exécution pour les requêtes déjà capturées sont toujours collectées.</span><span class="sxs-lookup"><span data-stu-id="45ea5-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="45ea5-224">Nous vous recommandons de définir toutes les stratégies tooAUTO et nouvelle stratégie too30 jours :</span><span class="sxs-lookup"><span data-stu-id="45ea5-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="45ea5-225">Augmentez la taille du magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="45ea5-225">Increase size of Query Store.</span></span> <span data-ttu-id="45ea5-226">Cela peut être exécutée par la connexion de base de données tooa et émetteur de la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="45ea5-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="45ea5-227">Appliquer ces paramètres finalement rend le magasin de requêtes collecte les nouvelles requêtes, toutefois, si vous ne souhaitez pas toowait, vous pouvez désactiver le magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="45ea5-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="45ea5-228">Exécution de la requête suivante va supprimer toutes les informations actuelles dans le magasin de requêtes de hello.</span><span class="sxs-lookup"><span data-stu-id="45ea5-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="45ea5-229">Résumé</span><span class="sxs-lookup"><span data-stu-id="45ea5-229">Summary</span></span>
<span data-ttu-id="45ea5-230">Query Performance Insight vous aide à comprendre l’impact hello de votre charge de travail de requête et de sa relation toodatabase la consommation des ressources.</span><span class="sxs-lookup"><span data-stu-id="45ea5-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="45ea5-231">Avec cette fonctionnalité, vous découvrez haut hello principales requêtes consommatrices et identifier facilement hello ceux toofix avant qu’ils deviennent un problème.</span><span class="sxs-lookup"><span data-stu-id="45ea5-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45ea5-232">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45ea5-232">Next steps</span></span>
<span data-ttu-id="45ea5-233">Pour obtenir des recommandations supplémentaires sur l’amélioration des performances hello de votre base de données SQL, cliquez sur [recommandations](sql-database-advisor.md) sur hello **Query Performance Insight** panneau.</span><span class="sxs-lookup"><span data-stu-id="45ea5-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

