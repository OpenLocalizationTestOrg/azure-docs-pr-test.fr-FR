---
title: "Se connecter à Azure SQL Data Warehouse - VSTS | Microsoft Docs"
description: Interrogez SQL Data Warehouse avec Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="a4b69-103">Se connecter à SQL Data Warehouse avec Visual Studio et SSDT</span><span class="sxs-lookup"><span data-stu-id="a4b69-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4b69-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="a4b69-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="a4b69-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a4b69-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="a4b69-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a4b69-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="a4b69-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="a4b69-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="a4b69-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="a4b69-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="a4b69-109">Utilisez Visual Studio pour interroger Azure SQL Data Warehouse en seulement quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a4b69-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="a4b69-110">Cette méthode utilise l’extension de SQL Server Data Tools (SSDT) dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4b69-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a4b69-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a4b69-111">Prerequisites</span></span>
<span data-ttu-id="a4b69-112">Pour utiliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a4b69-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="a4b69-113">Un entrepôt de données SQL existant.</span><span class="sxs-lookup"><span data-stu-id="a4b69-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="a4b69-114">Pour en créer un, consultez la page [Créer un entrepôt de données SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a4b69-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="a4b69-115">SSDT pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4b69-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="a4b69-116">Si vous avez Visual Studio, vous en disposez probablement déjà.</span><span class="sxs-lookup"><span data-stu-id="a4b69-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="a4b69-117">Pour obtenir des instructions et des options d’installation, consultez [Installation de Visual Studio et/ou SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="a4b69-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="a4b69-118">Le nom complet du serveur SQL.</span><span class="sxs-lookup"><span data-stu-id="a4b69-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="a4b69-119">Pour le trouver, consultez la page [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse](Connexion à SQL Data Warehouse).</span><span class="sxs-lookup"><span data-stu-id="a4b69-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="a4b69-120">1. Connexion à votre SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a4b69-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="a4b69-121">Ouvrir Visual Studio 2013 ou 2015</span><span class="sxs-lookup"><span data-stu-id="a4b69-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="a4b69-122">Ouvrez l’Explorateur d’objets SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4b69-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="a4b69-123">Pour ce faire, sélectionnez **Affichage** > **Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Explorateur d’objets SQL Server][1]
3. <span data-ttu-id="a4b69-125">Cliquez sur l’icône **Ajouter SQL Server** .</span><span class="sxs-lookup"><span data-stu-id="a4b69-125">Click the **Add SQL Server** icon.</span></span>
   
    ![Ajouter SQL Server][2]
4. <span data-ttu-id="a4b69-127">Renseignez les champs dans la fenêtre Se connecter au serveur.</span><span class="sxs-lookup"><span data-stu-id="a4b69-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Se connecter au serveur][3]
   
   * <span data-ttu-id="a4b69-129">**Nom du serveur**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-129">**Server name**.</span></span> <span data-ttu-id="a4b69-130">Saisissez le **nom du serveur** précédemment identifié.</span><span class="sxs-lookup"><span data-stu-id="a4b69-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="a4b69-131">**Authentification**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-131">**Authentication**.</span></span> <span data-ttu-id="a4b69-132">Sélectionnez **Authentification SQL Server** ou **Authentification intégrée Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="a4b69-133">**Nom d’utilisateur** et **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-133">**User Name** and **Password**.</span></span> <span data-ttu-id="a4b69-134">Entrez un nom d’utilisateur et mot de passe si l’authentification SQL Server a été sélectionnée plus haut.</span><span class="sxs-lookup"><span data-stu-id="a4b69-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="a4b69-135">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-135">Click **Connect**.</span></span>
5. <span data-ttu-id="a4b69-136">Pour voir plus d’informations, développez votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b69-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="a4b69-137">Vous pouvez afficher les bases de données associées au serveur.</span><span class="sxs-lookup"><span data-stu-id="a4b69-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="a4b69-138">Développez AdventureWorksDW pour voir les tables de votre exemple de base de données.</span><span class="sxs-lookup"><span data-stu-id="a4b69-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explorer AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="a4b69-140">2. Exécuter un exemple de requête</span><span class="sxs-lookup"><span data-stu-id="a4b69-140">2. Run a sample query</span></span>
<span data-ttu-id="a4b69-141">Maintenant qu’une connexion à votre base de données a été établie, passons à l’écriture d’une requête.</span><span class="sxs-lookup"><span data-stu-id="a4b69-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="a4b69-142">Cliquez avec le bouton droit sur votre base de données dans l’Explorateur d’objets SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4b69-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="a4b69-143">Sélectionnez **Nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="a4b69-143">Select **New Query**.</span></span> <span data-ttu-id="a4b69-144">Une nouvelle fenêtre de requête s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a4b69-144">A new query window opens.</span></span>
   
    ![Nouvelle requête][5]
3. <span data-ttu-id="a4b69-146">Copiez la requête TSQL suivante dans la fenêtre de requête :</span><span class="sxs-lookup"><span data-stu-id="a4b69-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="a4b69-147">Exécutez la requête.</span><span class="sxs-lookup"><span data-stu-id="a4b69-147">Run the query.</span></span> <span data-ttu-id="a4b69-148">Pour ce faire, cliquez sur la flèche verte ou utilisez le raccourci `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="a4b69-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Exécuter une requête][6]
5. <span data-ttu-id="a4b69-150">Passez en revue les résultats de la requête.</span><span class="sxs-lookup"><span data-stu-id="a4b69-150">Look at the query results.</span></span> <span data-ttu-id="a4b69-151">Dans cet exemple, la table FactInternetSales a 60 398 lignes.</span><span class="sxs-lookup"><span data-stu-id="a4b69-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Résultats de la requête][7]

## <a name="next-steps"></a><span data-ttu-id="a4b69-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4b69-153">Next steps</span></span>
<span data-ttu-id="a4b69-154">Comme vous pouvez à présent vous connecter et exécuter des requêtes, essayez de [visualiser les données avec Power BI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="a4b69-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="a4b69-155">Pour configurer votre environnement pour l’authentification Azure Active Directory, voir [Authentification vers SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a4b69-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
