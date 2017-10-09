---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Documents Microsoft
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="54830-103">Se connecter tooSQL Data Warehouse avec Visual Studio et SSDT</span><span class="sxs-lookup"><span data-stu-id="54830-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54830-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="54830-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="54830-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="54830-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="54830-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54830-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="54830-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="54830-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="54830-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="54830-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="54830-109">Utilisez Visual Studio tooquery Azure SQL Data Warehouse dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="54830-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="54830-110">Cette méthode utilise l’extension de SQL Server Data Tools (SSDT) hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54830-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="54830-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="54830-111">Prerequisites</span></span>
<span data-ttu-id="54830-112">toouse ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="54830-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="54830-113">Un entrepôt de données SQL existant.</span><span class="sxs-lookup"><span data-stu-id="54830-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="54830-114">toocreate, consultez [créer un entrepôt de données SQL][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="54830-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="54830-115">SSDT pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54830-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="54830-116">Si vous avez Visual Studio, vous en disposez probablement déjà.</span><span class="sxs-lookup"><span data-stu-id="54830-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="54830-117">Pour obtenir des instructions et des options d’installation, consultez [Installation de Visual Studio et/ou SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="54830-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="54830-118">Hello complet nom SQL server.</span><span class="sxs-lookup"><span data-stu-id="54830-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="54830-119">toofind, consultez [connecter tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="54830-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="54830-120">1. Se connecter tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="54830-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="54830-121">Ouvrir Visual Studio 2013 ou 2015</span><span class="sxs-lookup"><span data-stu-id="54830-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="54830-122">Ouvrez l’Explorateur d’objets SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54830-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="54830-123">toodo cette option, sélectionnez **vue** > **l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="54830-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Explorateur d’objets SQL Server][1]
3. <span data-ttu-id="54830-125">Cliquez sur hello **ajouter SQL Server** icône.</span><span class="sxs-lookup"><span data-stu-id="54830-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Ajouter SQL Server][2]
4. <span data-ttu-id="54830-127">Renseignez les champs hello dans la fenêtre de tooServer hello se connecter.</span><span class="sxs-lookup"><span data-stu-id="54830-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Se connecter tooServer][3]
   
   * <span data-ttu-id="54830-129">**Nom du serveur**.</span><span class="sxs-lookup"><span data-stu-id="54830-129">**Server name**.</span></span> <span data-ttu-id="54830-130">Entrez hello **nom du serveur** précédemment identifiés.</span><span class="sxs-lookup"><span data-stu-id="54830-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="54830-131">**Authentification**.</span><span class="sxs-lookup"><span data-stu-id="54830-131">**Authentication**.</span></span> <span data-ttu-id="54830-132">Sélectionnez **Authentification SQL Server** ou **Authentification intégrée Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54830-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="54830-133">**Nom d’utilisateur** et **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="54830-133">**User Name** and **Password**.</span></span> <span data-ttu-id="54830-134">Entrez un nom d’utilisateur et mot de passe si l’authentification SQL Server a été sélectionnée plus haut.</span><span class="sxs-lookup"><span data-stu-id="54830-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="54830-135">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="54830-135">Click **Connect**.</span></span>
5. <span data-ttu-id="54830-136">tooexplore, développez votre serveur SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="54830-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="54830-137">Vous pouvez afficher les bases de données hello associés avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="54830-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="54830-138">Développez le nœud AdventureWorksDW toosee hello tables dans votre base de données exemple.</span><span class="sxs-lookup"><span data-stu-id="54830-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Explorer AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="54830-140">2. Exécuter un exemple de requête</span><span class="sxs-lookup"><span data-stu-id="54830-140">2. Run a sample query</span></span>
<span data-ttu-id="54830-141">Maintenant qu’une connexion a été établie tooyour de base de données, nous allons écrire une requête.</span><span class="sxs-lookup"><span data-stu-id="54830-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="54830-142">Cliquez avec le bouton droit sur votre base de données dans l’Explorateur d’objets SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54830-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="54830-143">Sélectionnez **Nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="54830-143">Select **New Query**.</span></span> <span data-ttu-id="54830-144">Une nouvelle fenêtre de requête s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="54830-144">A new query window opens.</span></span>
   
    ![Nouvelle requête][5]
3. <span data-ttu-id="54830-146">Copiez cette requête TSQL dans une fenêtre de requête de hello :</span><span class="sxs-lookup"><span data-stu-id="54830-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="54830-147">Exécutez une requête de hello.</span><span class="sxs-lookup"><span data-stu-id="54830-147">Run hello query.</span></span> <span data-ttu-id="54830-148">toodo, cliquez sur la flèche de hello vert ou utiliser hello suivant raccourci : `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="54830-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Exécuter une requête][6]
5. <span data-ttu-id="54830-150">Examinez les résultats de la requête hello.</span><span class="sxs-lookup"><span data-stu-id="54830-150">Look at hello query results.</span></span> <span data-ttu-id="54830-151">Dans cet exemple, la table FactInternetSales de hello a 60398 lignes.</span><span class="sxs-lookup"><span data-stu-id="54830-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Résultats de la requête][7]

## <a name="next-steps"></a><span data-ttu-id="54830-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54830-153">Next steps</span></span>
<span data-ttu-id="54830-154">Maintenant que vous pouvez vous connecter et de requête, essayez [visualisation des données hello avec Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="54830-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="54830-155">tooconfigure votre environnement pour l’authentification Azure Active Directory, voir [authentifier tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="54830-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
