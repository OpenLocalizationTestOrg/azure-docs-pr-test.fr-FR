---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Documents Microsoft
description: "Utilisez SQL Server Management Studio (SSMS) tooconnect tooand requête Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="c0c61-103">Se connecter tooSQL l’entrepôt de données avec SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="c0c61-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0c61-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="c0c61-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="c0c61-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c0c61-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="c0c61-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0c61-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="c0c61-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c0c61-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="c0c61-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="c0c61-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="c0c61-109">Utilisez SQL Server Management Studio (SSMS) tooconnect tooand requête Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c0c61-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c0c61-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c0c61-110">Prerequisites</span></span>
<span data-ttu-id="c0c61-111">toouse ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="c0c61-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="c0c61-112">Un entrepôt de données SQL existant.</span><span class="sxs-lookup"><span data-stu-id="c0c61-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="c0c61-113">toocreate, consultez [créer un entrepôt de données SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c0c61-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="c0c61-114">SQL Server Management Studio (SSMS) installé.</span><span class="sxs-lookup"><span data-stu-id="c0c61-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="c0c61-115">[Installez SSMS][Install SSMS] gratuitement si vous ne l’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="c0c61-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="c0c61-116">Hello complet nom SQL server.</span><span class="sxs-lookup"><span data-stu-id="c0c61-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="c0c61-117">toofind, consultez [connecter tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c0c61-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="c0c61-118">1. Se connecter tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c0c61-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="c0c61-119">Ouvrez SSMS.</span><span class="sxs-lookup"><span data-stu-id="c0c61-119">Open SSMS.</span></span>
2. <span data-ttu-id="c0c61-120">Ouvrez l’Explorateur d'objets.</span><span class="sxs-lookup"><span data-stu-id="c0c61-120">Open Object Explorer.</span></span> <span data-ttu-id="c0c61-121">toodo cette option, sélectionnez **fichier** > **connecter l’Explorateur d’objets**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Explorateur d’objets SQL Server][1]
3. <span data-ttu-id="c0c61-123">Renseignez les champs hello dans la fenêtre de tooServer hello se connecter.</span><span class="sxs-lookup"><span data-stu-id="c0c61-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Se connecter tooServer][2]
   
   * <span data-ttu-id="c0c61-125">**Nom du serveur**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-125">**Server name**.</span></span> <span data-ttu-id="c0c61-126">Entrez hello **nom du serveur** précédemment identifiés.</span><span class="sxs-lookup"><span data-stu-id="c0c61-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="c0c61-127">**Authentification**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-127">**Authentication**.</span></span> <span data-ttu-id="c0c61-128">Sélectionnez **Authentification SQL Server** ou **Authentification intégrée Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="c0c61-129">**Nom d’utilisateur** et **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-129">**User Name** and **Password**.</span></span> <span data-ttu-id="c0c61-130">Entrez un nom d’utilisateur et mot de passe si l’authentification SQL Server a été sélectionnée plus haut.</span><span class="sxs-lookup"><span data-stu-id="c0c61-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="c0c61-131">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-131">Click **Connect**.</span></span>
4. <span data-ttu-id="c0c61-132">tooexplore, développez votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c61-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="c0c61-133">Vous pouvez afficher les bases de données hello associés avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="c0c61-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="c0c61-134">Développez le nœud AdventureWorksDW toosee hello tables dans votre base de données exemple.</span><span class="sxs-lookup"><span data-stu-id="c0c61-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorer AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="c0c61-136">2. Exécuter un exemple de requête</span><span class="sxs-lookup"><span data-stu-id="c0c61-136">2. Run a sample query</span></span>
<span data-ttu-id="c0c61-137">Maintenant qu’une connexion a été établie tooyour de base de données, nous allons écrire une requête.</span><span class="sxs-lookup"><span data-stu-id="c0c61-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="c0c61-138">Cliquez avec le bouton droit sur votre base de données dans l’Explorateur d’objets SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c0c61-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="c0c61-139">Sélectionnez **Nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-139">Select **New Query**.</span></span> <span data-ttu-id="c0c61-140">Une nouvelle fenêtre de requête s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c0c61-140">A new query window opens.</span></span>
   
    ![Nouvelle requête][4]
3. <span data-ttu-id="c0c61-142">Copiez cette requête TSQL dans une fenêtre de requête de hello :</span><span class="sxs-lookup"><span data-stu-id="c0c61-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="c0c61-143">Exécutez une requête de hello.</span><span class="sxs-lookup"><span data-stu-id="c0c61-143">Run hello query.</span></span> <span data-ttu-id="c0c61-144">toodo, cliquez sur `Execute` ou utilisez hello suit raccourci : `F5`.</span><span class="sxs-lookup"><span data-stu-id="c0c61-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Exécuter une requête][5]
5. <span data-ttu-id="c0c61-146">Examinez les résultats de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="c0c61-146">Look at hello query results.</span></span> <span data-ttu-id="c0c61-147">Dans cet exemple, la table FactInternetSales de hello a 60398 lignes.</span><span class="sxs-lookup"><span data-stu-id="c0c61-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Résultats de la requête][6]

## <a name="next-steps"></a><span data-ttu-id="c0c61-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0c61-149">Next steps</span></span>
<span data-ttu-id="c0c61-150">Maintenant que vous pouvez vous connecter et de requête, essayez [visualisation des données hello avec Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="c0c61-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="c0c61-151">tooconfigure votre environnement pour l’authentification Azure Active Directory, voir [authentifier tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="c0c61-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
