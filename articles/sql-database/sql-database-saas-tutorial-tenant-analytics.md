---
title: "Exécuter des requêtes d’analyse sur plusieurs bases de données SQL Azure | Microsoft Docs"
description: "Extraire des données à partir de bases de données du locataire dans une base de données d’analyse pour une analyse hors connexion"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="f9d2d-104">Extraire des données à partir de bases de données du locataire dans une base de données d’analyse pour une analyse hors connexion</span><span class="sxs-lookup"><span data-stu-id="f9d2d-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="f9d2d-105">Dans ce didacticiel, vous utilisez un travail élastique pour exécuter des requêtes sur chaque base de données du locataire.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="f9d2d-106">Le travail extrait les données de ventes de ticket et les charge dans une base de données d’analyse (ou entrepôt de données) pour analyse.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="f9d2d-107">Cette base de données d’analyse peut être interrogée pour extraire les informations dans les données opérationnelles quotidiennes de tous les locataires.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="f9d2d-108">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9d2d-109">Créer la base de données d’analyse du locataire</span><span class="sxs-lookup"><span data-stu-id="f9d2d-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="f9d2d-110">Créer un travail planifié pour récupérer les données et remplir la base de données d’analyse</span><span class="sxs-lookup"><span data-stu-id="f9d2d-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="f9d2d-111">Pour suivre ce didacticiel, vérifiez que les conditions préalables ci-dessous sont bien satisfaites :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="f9d2d-112">L’application SaaS Wingtip est déployée.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="f9d2d-113">Pour procéder à un déploiement en moins de cinq minutes, consultez la page [Déployer et explorer une application SaaS Wingtip](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="f9d2d-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="f9d2d-114">Azure PowerShell est installé.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="f9d2d-115">Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="f9d2d-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="f9d2d-116">La dernière version de SQL Server Management Studio (SSMS) est installée.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="f9d2d-117">Télécharger et installer SSMS</span><span class="sxs-lookup"><span data-stu-id="f9d2d-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="f9d2d-118">Modèle d’analyse opérationnelle du locataire</span><span class="sxs-lookup"><span data-stu-id="f9d2d-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="f9d2d-119">Une des grandes opportunités avec les applications SaaS est l’exploitation des nombreuses données de locataire qui sont stockées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="f9d2d-120">Utilisez ces données pour obtenir des informations sur le fonctionnement et l’utilisation de votre application, et sur vos locataires.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="f9d2d-121">Ces données peuvent guider le développement des fonctionnalités, les améliorations de convivialité et autres investissements dans l’application et la plateforme.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="f9d2d-122">Lorsqu’il se fait dans une seule base de données mutualisée, l’accès à ces données est facile, mais pas si simple lors d’une distribution à grande échelle sur des milliers de bases de données.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="f9d2d-123">Pour accéder à ces données, une approche consiste à utiliser des travaux élastiques, qui permettent la capture des résultats des requêtes lors de l’exécution du travail dans une base de données de sortie et dans une table.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="f9d2d-124">Obtenir les scripts d’application Wingtip</span><span class="sxs-lookup"><span data-stu-id="f9d2d-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="f9d2d-125">Les scripts et le code source de l’application SaaS Wingtip sont disponibles dans le référentiel GitHub [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS).</span><span class="sxs-lookup"><span data-stu-id="f9d2d-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="f9d2d-126">[Étapes de téléchargement des scripts SaaS Wingtip](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="f9d2d-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="f9d2d-127">Déployer une base de données pour les résultats d’analyse du locataire</span><span class="sxs-lookup"><span data-stu-id="f9d2d-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="f9d2d-128">Ce didacticiel nécessite que vous ayez déployé une base de données, afin de capturer les résultats de l’exécution du travail de scripts, qui contiennent les requêtes qui renvoient des résultats.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="f9d2d-129">À cet effet, nous allons créer une base de données appelée tenantanalytics.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="f9d2d-130">Ouvrez ...\\Modules d’apprentissage\\Operational Analytics\\Tenants Analytics\\*Demo-TenantAnalyticsDB.ps1* dans *PowerShell ISE* et définissez la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="f9d2d-131">**$DemoScenario** = **2** *Déployer une base de données d’analyse opérationnelle*</span><span class="sxs-lookup"><span data-stu-id="f9d2d-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="f9d2d-132">Appuyez sur **F5** pour exécuter le script de démonstration (qui appelle le script *Deploy-TenantAnalyticsDB.ps1*), qui crée la base de données d’analyse du locataire.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="f9d2d-133">Créer des données pour la démonstration</span><span class="sxs-lookup"><span data-stu-id="f9d2d-133">Create some data for the demo</span></span>

1. <span data-ttu-id="f9d2d-134">Ouvrez ...\\Modules d’apprentissage\\Operational Analytics\\Tenants Analytics\\*Demo-TenantAnalyticsDB.ps1* dans *PowerShell ISE* et définissez la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="f9d2d-135">**$DemoScenario** = **1** *Acheter des tickets pour des événements dans tous les lieux*</span><span class="sxs-lookup"><span data-stu-id="f9d2d-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="f9d2d-136">Appuyez sur **F5** pour exécuter le script et créez un historique d’achat de tickets.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="f9d2d-137">Créer un travail planifié pour récupérer l’analyse du locataire concernant l’achat de tickets</span><span class="sxs-lookup"><span data-stu-id="f9d2d-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="f9d2d-138">Ce script crée un travail permettant de récupérer les informations d’achat de tickets par tous les locataires.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="f9d2d-139">Une fois ces données regroupées dans une seule table, vous pouvez obtenir des mesures pertinentes sur l’achat de tickets par les locataires.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="f9d2d-140">Ouvrez SSMS et connectez-vous au serveur catalog-&lt;user&gt;.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="f9d2d-141">Ouvrez ...\\Modules d’apprentissage\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="f9d2d-142">Modifiez &lt;User&gt; (Utilisateur), servez-vous du nom d’utilisateur utilisé lors du déploiement de l’application SaaS Wingtip au début du script, **sp\_add\_target\_group\_member** et **sp\_add\_jobstep**</span><span class="sxs-lookup"><span data-stu-id="f9d2d-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="f9d2d-143">Si vous n’êtes pas déjà connecté, cliquez avec le bouton droit, sélectionnez **Connexion** et connectez-vous au serveur catalog-&lt;User&gt;.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9d2d-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="f9d2d-144">Assurez-vous que vous êtes connecté à la base de données **jobaccount**, puis appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="f9d2d-145">**sp\_add\_target\_group** crée le nom du groupe cible *TenantGroup*. Nous devons à présent ajouter des membres cibles.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="f9d2d-146">**sp\_add\_target\_group\_member** ajoute un type de membre cible *server*, qui considère qu’au moment de l’exécution du travail, toutes les bases de données dans ce serveur (notez qu’il s’agit du serveur customer1-&lt;User&gt; contenant les bases de données des locataires) doivent être incluses dans le travail.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="f9d2d-147">**sp\_add\_job** crée un nouveau travail hebdomadaire planifié appelé « Achat de tickets par tous les locataires ».</span><span class="sxs-lookup"><span data-stu-id="f9d2d-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="f9d2d-148">**sp\_add\_jobstep** crée l’étape du travail contenant le texte de la commande T-SQL pour récupérer toutes les informations liées aux achats de tickets par tous les locataires, et pour copier le résultat renvoyé défini dans une table appelée *AllTicketsPurchasesfromAllTenants*.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="f9d2d-149">Les autres vues dans le script indiquent l’existence des objets et contrôlent l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="f9d2d-150">Surveillez la valeur de l’état dans la colonne **lifecycle**.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="f9d2d-151">Une fois, Réussi, le travail a réussi sur toutes les bases de données locataires et les deux autres bases de données contenant la table de référence.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="f9d2d-152">Si le script s’exécute correctement, vous devez obtenir des résultats similaires :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-152">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="f9d2d-154">Créer un travail permettant de récupérer un résumé du nombre d’achats de tickets par tous les locataires</span><span class="sxs-lookup"><span data-stu-id="f9d2d-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="f9d2d-155">Ce script crée un travail permettant de récupérer la somme des achats de tickets par tous les locataires.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="f9d2d-156">Ouvrez SSMS et connectez-vous au serveur *catalog-&lt;User&gt;.database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="f9d2d-157">Ouvrez le fichier... \\Modules d’apprentissage\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="f9d2d-158">Modifiez &lt;User&gt; (Utilisateur), servez-vous du nom d’utilisateur utilisé lors du déploiement de l’application SaaS Wingtip dans le script, dans la procédure stockée **sp\_add\_jobstep**</span><span class="sxs-lookup"><span data-stu-id="f9d2d-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="f9d2d-159">Si vous n’êtes pas déjà connecté, cliquez avec le bouton droit, sélectionnez **Connexion** et connectez-vous au serveur catalog-&lt;User&gt;.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9d2d-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="f9d2d-160">Assurez-vous que vous êtes connecté à la base de données **tenantanalytics**, puis appuyez sur **F5** pour exécuter le script.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="f9d2d-161">Si le script s’exécute correctement, vous devez obtenir des résultats similaires :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-161">Successfully running the script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="f9d2d-163">**sp\_add\_job** crée un travail hebdomadaire planifié appelé « ResultsTicketsOrders ».</span><span class="sxs-lookup"><span data-stu-id="f9d2d-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="f9d2d-164">**sp\_add\_jobstep** crée l’étape du travail contenant le texte de la commande T-SQL pour récupérer toutes les informations liées aux achats de tickets par tous les locataires, et pour copier le résultat renvoyé défini dans une table appelée CountofTicketOrders.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="f9d2d-165">Les autres vues dans le script indiquent l’existence des objets et contrôlent l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="f9d2d-166">Surveillez la valeur de l’état dans la colonne **lifecycle**.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="f9d2d-167">Une fois, Réussi, le travail a réussi sur toutes les bases de données locataires et les deux autres bases de données contenant la table de référence.</span><span class="sxs-lookup"><span data-stu-id="f9d2d-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f9d2d-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9d2d-168">Next steps</span></span>

<span data-ttu-id="f9d2d-169">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="f9d2d-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9d2d-170">Déployez une base de données d’analyse du locataire</span><span class="sxs-lookup"><span data-stu-id="f9d2d-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="f9d2d-171">Créer un travail planifié permettant de récupérer des données d’analyse sur les locataires</span><span class="sxs-lookup"><span data-stu-id="f9d2d-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="f9d2d-172">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f9d2d-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9d2d-173">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f9d2d-173">Additional resources</span></span>

* <span data-ttu-id="f9d2d-174">Autres [didacticiels reposant sur l’application SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="f9d2d-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="f9d2d-175">Tâches élastiques</span><span class="sxs-lookup"><span data-stu-id="f9d2d-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
