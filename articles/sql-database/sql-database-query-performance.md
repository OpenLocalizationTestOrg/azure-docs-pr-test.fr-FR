---
title: "Analyse des performances des données pour Azure SQL Database | Microsoft Docs"
description: "La surveillance des performances des requêtes identifie les requêtes consommant le plus d’UC pour une base de données SQL Azure."
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
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="5f6cd-103">Query Performance Insight pour base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="5f6cd-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="5f6cd-104">La gestion et le réglage des performances des bases de données relationnelles est une tâche complexe qui nécessite une réelle expertise et un investissement en temps.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="5f6cd-105">Query Performance Insight vous permet de passer moins de temps à résoudre les problèmes de performances des bases de données en fournissant :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="5f6cd-106">Une meilleure compréhension de la consommation des ressources des bases de données (DTU).</span><span class="sxs-lookup"><span data-stu-id="5f6cd-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="5f6cd-107">Les requêtes principales par consommation d’UC/durée/exécution, qui peuvent être réglées pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="5f6cd-108">La possibilité de connaître les détails d’une requête, d’afficher son texte et l’historique d’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="5f6cd-109">Des annotations de réglage des performances qui indiquent les actions effectuées par [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="5f6cd-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="5f6cd-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5f6cd-110">Prerequisites</span></span>
* <span data-ttu-id="5f6cd-111">Query Performance Insight nécessite que le [magasin de requêtes](https://msdn.microsoft.com/library/dn817826.aspx) soit actif sur votre base de données.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="5f6cd-112">Si le magasin de requêtes ne fonctionne pas, le portail vous invite à l’activer.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="5f6cd-113">Autorisations</span><span class="sxs-lookup"><span data-stu-id="5f6cd-113">Permissions</span></span>
<span data-ttu-id="5f6cd-114">Les autorisations [de contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md) suivantes sont requises pour utiliser Query Performance Insight :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="5f6cd-115">Les autorisations **Reader**, **Owner**, **Contributor**, **SQL DB Contributor** ou **SQL Server Contributor** sont requises pour afficher les requêtes et graphiques consommant le plus de ressources.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="5f6cd-116">Les autorisations **Owner**, **Contributor**, **SQL DB Contributor** ou **SQL Server Contributor** sont requises pour afficher le texte de requête.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="5f6cd-117">Utilisation de Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="5f6cd-117">Using Query Performance Insight</span></span>
<span data-ttu-id="5f6cd-118">Query Performance Insight est simple d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="5f6cd-119">Ouvrez le [portail Azure](https://portal.azure.com/) et recherchez la base de données que vous souhaitez examiner.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="5f6cd-120">Dans le menu de gauche, sous Support et dépannage, sélectionnez « Query Performance Insight ».</span><span class="sxs-lookup"><span data-stu-id="5f6cd-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="5f6cd-121">Dans le premier onglet, passez en revue la liste des requêtes consommant le plus de ressources.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="5f6cd-122">Sélectionnez une requête pour en afficher les détails.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="5f6cd-123">Ouvrez [SQL Azure Database Advisor](sql-database-advisor.md) , puis regardez si des recommandations sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="5f6cd-124">Utilisez les icônes de curseurs ou de zoom pour modifier l’intervalle observé.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![tableau de bord des performances](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="5f6cd-126">Quelques heures de données doivent être capturées par le magasin de requêtes pour que la base de données SQL fournisse des informations sur les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="5f6cd-127">Si la base de données n’a aucune activité ou que Query Store est resté inactif pendant une certaine période, les graphiques seront vides lors de l’affichage de cette période.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="5f6cd-128">Vous pouvez activer Query Store à tout moment s’il n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="5f6cd-129">Consultez les requêtes principales consommatrices d’UC</span><span class="sxs-lookup"><span data-stu-id="5f6cd-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="5f6cd-130">Dans le [portail](http://portal.azure.com) , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="5f6cd-131">Accédez à une base de données SQL, puis cliquez sur **Tous les paramètres** > **Support et dépannage** > **Analyse des performances des requêtes**.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Query performance insight][1]
   
    <span data-ttu-id="5f6cd-133">La vue des principales requêtes s’ouvre, affichant une liste des requêtes consommant le plus d’UC.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="5f6cd-134">Cliquez sur le graphique pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-134">Click around the chart for details.</span></span><br><span data-ttu-id="5f6cd-135">La première ligne affiche le pourcentage de DTU global de la base de données, tandis que les barres affichent le pourcentage d’UC consommé par les requêtes sélectionnées pendant l’intervalle sélectionné (par exemple, si **Semaine dernière** est sélectionné, chaque barre représente un jour).</span><span class="sxs-lookup"><span data-stu-id="5f6cd-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![principales requêtes][2]
   
    <span data-ttu-id="5f6cd-137">Le tableau du bas contient des informations agrégées concernant les requêtes visibles.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="5f6cd-138">ID de requête : identificateur unique de la requête dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="5f6cd-139">UC par requête pendant l’intervalle observable (dépend de la fonction d’agrégation).</span><span class="sxs-lookup"><span data-stu-id="5f6cd-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="5f6cd-140">Durée par requête (dépend de la fonction d’agrégation).</span><span class="sxs-lookup"><span data-stu-id="5f6cd-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="5f6cd-141">Nombre total d’exécutions pour une requête particulière.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="5f6cd-142">Sélectionnez ou supprimez des requêtes individuelles pour les inclure ou les exclure du graphique à l’aide des cases à cocher.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="5f6cd-143">Si vos données deviennent obsolètes, cliquez sur le bouton **Actualiser** .</span><span class="sxs-lookup"><span data-stu-id="5f6cd-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="5f6cd-144">Vous pouvez utiliser les curseurs et les boutons de zoom pour modifier l’intervalle d’observation et examiner les pics d’activité : ![paramètres](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="5f6cd-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="5f6cd-145">Si vous souhaitez un affichage différent, vous pouvez également sélectionner l’onglet **Personnalisé** et définir :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="5f6cd-146">la mesure (UC, Durée, Nombre d’exécutions) ;</span><span class="sxs-lookup"><span data-stu-id="5f6cd-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="5f6cd-147">l’intervalle de temps (Dernières 24 heures, Semaine dernière, Mois dernier) ;</span><span class="sxs-lookup"><span data-stu-id="5f6cd-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="5f6cd-148">le nombre de requêtes ;</span><span class="sxs-lookup"><span data-stu-id="5f6cd-148">Number of queries.</span></span>
   * <span data-ttu-id="5f6cd-149">la fonction d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-149">Aggregation function.</span></span>
     
     ![Paramètres](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="5f6cd-151">Affichage des détails d’une requête individuelle</span><span class="sxs-lookup"><span data-stu-id="5f6cd-151">Viewing individual query details</span></span>
<span data-ttu-id="5f6cd-152">Pour afficher les détails d’une requête :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-152">To view query details:</span></span>

1. <span data-ttu-id="5f6cd-153">Cliquez sur n’importe quelle requête dans la liste des principales requêtes.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-153">Click any query in the list of top queries.</span></span>
   
    ![détails](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="5f6cd-155">La vue détaillée s’ouvre et la consommation d’UC/la durée/le nombre d’exécutions des requêtes sont répartie dans le temps.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="5f6cd-156">Cliquez sur le graphique pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="5f6cd-157">Le graphique supérieur affiche la ligne avec le pourcentage de DTU de base de données global, et les barres indiquent le pourcentage de l’UC consommé par la requête sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="5f6cd-158">Le deuxième graphique affiche la durée totale pour la requête sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="5f6cd-159">Le graphique du bas affiche le nombre total d’exécutions pour la requête sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![détails de la requête][3]
4. <span data-ttu-id="5f6cd-161">Vous pouvez également utiliser les curseurs ou les boutons de zoom ou cliquer sur **Paramètres** pour personnaliser l’affichage des données ou pour afficher une autre période.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="5f6cd-162">Révision des requêtes principales par durée</span><span class="sxs-lookup"><span data-stu-id="5f6cd-162">Review top queries per duration</span></span>
<span data-ttu-id="5f6cd-163">Dans la mise à jour récente de Query Performance Insight, nous avons introduit deux nouvelles mesures qui peuvent vous aider à identifier les goulots d’étranglement potentiels : la durée et le nombre d’exécutions.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="5f6cd-164">Les requêtes de longue durée ont le plus grand risque de verrouiller des ressources le plus longtemps, de bloquer d’autres utilisateurs et de limiter l’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="5f6cd-165">Mais elles peuvent être également facilement optimisées.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="5f6cd-166">Pour identifier les requêtes de longue durée :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-166">To identify long running queries:</span></span>

1. <span data-ttu-id="5f6cd-167">Ouvrez l’onglet **Personnalisé** dans Query Performance Insight pour la base de données sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="5f6cd-168">Sélectionnez la mesure **durée**</span><span class="sxs-lookup"><span data-stu-id="5f6cd-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="5f6cd-169">Sélectionner le nombre de requêtes et l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="5f6cd-170">Sélectionnez la fonction d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="5f6cd-171">**Somme** calcule le temps d’exécution total de toutes les requêtes pendant tout l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="5f6cd-172">**Max** recherche le temps d’exécution maximum pendant l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="5f6cd-173">**Moy** calcule la durée d’exécution moyenne de toutes les exécutions de requête et affiche ces moyennes.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![durée de la requête][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="5f6cd-175">Révision des requêtes principales par nombre d’exécutions</span><span class="sxs-lookup"><span data-stu-id="5f6cd-175">Review top queries per execution count</span></span>
<span data-ttu-id="5f6cd-176">Un nombre élevé d’exécutions peut ne pas affecter la base de données elle-même et l’utilisation de ressources peut être faible, mais l’application globale peut devenir lente.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="5f6cd-177">Dans certains cas, un nombre d’exécutions très élevé peut augmenter les allers-retours réseau.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="5f6cd-178">Les allers-retours affectent considérablement les performances.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="5f6cd-179">Ils peuvent entraîner une latence du réseau et une latence du serveur en aval.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="5f6cd-180">Par exemple, de nombreux sites web centrés sur les données accèdent à la base de données à chaque requête de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="5f6cd-181">Alors que le regroupement de connexions a un effet positif, l’augmentation du trafic réseau et la charge de traitement dans la base de données peuvent nuire aux performances.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="5f6cd-182">Il est généralement conseillé de limiter les allers-retours au strict minimum.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="5f6cd-183">Pour identifier les requêtes fréquemment exécutées (« bavardes ») :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="5f6cd-184">Ouvrez l’onglet **Personnalisé** dans Query Performance Insight pour la base de données sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="5f6cd-185">Sélectionnez la mesure **nombre d’exécutions**</span><span class="sxs-lookup"><span data-stu-id="5f6cd-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="5f6cd-186">Sélectionner le nombre de requêtes et l’intervalle d’observation.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-186">Select number of queries and observation interval</span></span>
   
    ![nombre d’exécutions de la requête][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="5f6cd-188">Présentation des annotations de réglage des performances</span><span class="sxs-lookup"><span data-stu-id="5f6cd-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="5f6cd-189">Lors de l’analyse de votre charge de travail dans Query Performance Insight, vous pouvez remarquer des icônes avec une ligne verticale en haut du graphique.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="5f6cd-190">Ces icônes sont des annotations. Elles représentent les performances qui affectent les actions effectuées par [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="5f6cd-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="5f6cd-191">En pointant sur une annotation, vous obtenez des informations de base sur l’action :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-191">By hovering annotation, you get basic information about the action:</span></span>

![annotation de requête][6]

<span data-ttu-id="5f6cd-193">Si vous souhaitez en savoir plus ou appliquer des recommandations de SQL Azure Database Advisor, cliquez sur l’icône.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="5f6cd-194">Les détails de l’action s’ouvrent.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-194">It will open details of action.</span></span> <span data-ttu-id="5f6cd-195">S’il s’agit d’une recommandation active, vous pouvez l’appliquer directement à l’aide de la commande.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![détails d’annotation de requête][7]

### <a name="multiple-annotations"></a><span data-ttu-id="5f6cd-197">Annotations multiples.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-197">Multiple annotations.</span></span>
<span data-ttu-id="5f6cd-198">Il est possible qu’en raison du niveau de zoom, les annotations qui sont proches les unes des autres soient réduites en une seule.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="5f6cd-199">Une icône spéciale s’affiche alors. Si vous cliquez dessus, un panneau s’ouvre, qui contient une liste d’annotations groupées.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="5f6cd-200">La corrélation de requêtes et des actions de réglage des performances peut vous aider à mieux comprendre votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="5f6cd-201">Optimisation de la configuration du magasin de requêtes pour Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="5f6cd-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="5f6cd-202">Pendant l’utilisation de Query Performance Insight, vous pouvez rencontrer les messages suivants du magasin de requêtes :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="5f6cd-203">« Le magasin de requête n’est pas correctement configuré dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="5f6cd-204">Cliquez ici pour en savoir plus. »</span><span class="sxs-lookup"><span data-stu-id="5f6cd-204">Click here to learn more."</span></span>
* <span data-ttu-id="5f6cd-205">« Le magasin de requête n’est pas correctement configuré dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="5f6cd-206">Cliquez ici pour modifier les paramètres. »</span><span class="sxs-lookup"><span data-stu-id="5f6cd-206">Click here to change settings."</span></span> 

<span data-ttu-id="5f6cd-207">Ces messages s’affichent généralement lorsque le magasin de requêtes ne peut plus collecter de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="5f6cd-208">Le premier cas se produit lorsque le magasin de requêtes est en mode Lecture seule et si les paramètres sont définis de façon optimale.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="5f6cd-209">Vous pouvez résoudre ce problème en augmentant la taille du magasin de requêtes ou en le nettoyant.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![bouton qds][8]

<span data-ttu-id="5f6cd-211">Le deuxième cas se produit lorsque le magasin de requêtes est désactivé ou si les paramètres ne sont pas définis de façon optimale.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="5f6cd-212">Vous pouvez modifier la stratégie de rétention et de capture et activer le magasin de requêtes en exécutant les commandes ci-dessous ou directement à partir du portail :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![bouton qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="5f6cd-214">Stratégie de rétention et de capture recommandée</span><span class="sxs-lookup"><span data-stu-id="5f6cd-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="5f6cd-215">Il existe deux types de stratégies de rétention :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="5f6cd-216">Basée sur la taille : si la valeur AUTO est définie, les données sont automatiquement supprimées quand la taille maximale est proche.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="5f6cd-217">Basée sur le temps : la période par défaut est de 30 jours. Ainsi, si le magasin de requêtes manque d’espace, il supprimera les informations liées aux requêtes âgées de plus de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="5f6cd-218">La stratégie de capture peut avoir les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="5f6cd-219">**Tout** : toutes les requêtes sont capturées.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="5f6cd-220">**Auto** : les requêtes peu fréquentes et les requêtes avec une durée de compilation et d’exécution insignifiante sont ignorées.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="5f6cd-221">Les seuils concernant le nombre d’exécutions, et la durée de compilation et d’exécution, sont déterminés en interne.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="5f6cd-222">Il s'agit de l'option par défaut.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-222">This is the default option.</span></span>
* <span data-ttu-id="5f6cd-223">**Aucune** : le magasin de requêtes arrête la capture de nouvelles requêtes, mais les statistiques d’exécution pour les requêtes déjà capturées sont toujours collectées.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="5f6cd-224">Nous vous recommandons de définir toutes les stratégies sur AUTO, et de définir la stratégie de suppression des anciennes requêtes sur 30 jours :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="5f6cd-225">Augmentez la taille du magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-225">Increase size of Query Store.</span></span> <span data-ttu-id="5f6cd-226">Pour cela, connectez-vous à une base de données et exécutez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="5f6cd-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="5f6cd-227">Lorsque ces paramètres sont appliqués, le magasin de requêtes collecte finalement les nouvelles requêtes, mais vous pouvez effacer les données du magasin de requêtes si vous ne souhaitez pas attendre.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="5f6cd-228">L’exécution de la requête suivante supprime l’ensemble des informations du magasin de requêtes.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="5f6cd-229">Résumé</span><span class="sxs-lookup"><span data-stu-id="5f6cd-229">Summary</span></span>
<span data-ttu-id="5f6cd-230">Query Performance Insight vous permet de comprendre l’impact de votre charge de travail de requêtes et la relation de celle-ci avec la consommation des ressources de base de données.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="5f6cd-231">Cette fonctionnalité vous permettra d’en savoir plus sur les requêtes les plus gourmandes et d’identifier facilement les requêtes à corriger avant qu’elles ne deviennent un problème.</span><span class="sxs-lookup"><span data-stu-id="5f6cd-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f6cd-232">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f6cd-232">Next steps</span></span>
<span data-ttu-id="5f6cd-233">Pour obtenir d’autres recommandations concernant l’amélioration des performances de votre base de données SQL, cliquez sur [Recommandations](sql-database-advisor.md) dans le panneau **Query Performance Insight** .</span><span class="sxs-lookup"><span data-stu-id="5f6cd-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

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

