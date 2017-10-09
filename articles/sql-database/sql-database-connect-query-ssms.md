---
title: "SSMS : Se connecter et interroger des données dans Azure SQL Database | Microsoft Docs"
description: "Découvrez comment tooconnect tooSQL de base de données sur Azure à l’aide de SQL Server Management Studio (SSMS). Ensuite, exécutez les instructions Transact-SQL (T-SQL) tooquery et modifier des données."
metacanonical: 
keywords: "se connecter à base de données toosql, studio de gestion sql server"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a><span data-ttu-id="23948-105">Base de données SQL Azure : Utilisez SQL Server Management Studio tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="23948-105">Azure SQL Database: Use SQL Server Management Studio tooconnect and query data</span></span>

<span data-ttu-id="23948-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) est un environnement intégré pour la gestion d’une infrastructure SQL, à partir de SQL Server tooSQL de base de données pour Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="23948-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span> <span data-ttu-id="23948-107">Ce démarrage rapide montre comment toouse SSMS tooconnect tooan Azure SQL database et puis tooquery d’instructions Transact-SQL d’utilisation, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="23948-107">This quick start demonstrates how toouse SSMS tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="23948-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="23948-108">Prerequisites</span></span>

<span data-ttu-id="23948-109">Ce démarrage rapide utilise en tant que ses ressources de hello de point de départ créés dans une de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="23948-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="23948-110">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="23948-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="23948-111">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="23948-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="23948-112">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="23948-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="23948-113">Avant de commencer, assurez-vous que vous avez installé la version la plus récente de hello [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="23948-113">Before you start, make sure you have installed hello newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="23948-114">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="23948-114">SQL server connection information</span></span>

<span data-ttu-id="23948-115">Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="23948-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="23948-116">Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="23948-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="23948-117">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="23948-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="23948-118">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="23948-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="23948-119">Sur hello **vue d’ensemble** pour votre base de données, vérifiez le nom du serveur complet hello comme indiqué dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="23948-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello image below.</span></span> <span data-ttu-id="23948-120">Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.</span><span class="sxs-lookup"><span data-stu-id="23948-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![informations de connexion](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="23948-122">Si vous avez oublié des informations de connexion hello pour votre serveur de base de données SQL Azure, accédez nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="23948-122">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="connect-tooyour-database"></a><span data-ttu-id="23948-123">Connexion de base de données tooyour</span><span class="sxs-lookup"><span data-stu-id="23948-123">Connect tooyour database</span></span>

<span data-ttu-id="23948-124">Utilisez SQL Server Management Studio tooestablish un serveur de base de données SQL Azure de tooyour de connexion.</span><span class="sxs-lookup"><span data-stu-id="23948-124">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="23948-125">Un serveur logique Azure SQL Database écoute sur le port 1433.</span><span class="sxs-lookup"><span data-stu-id="23948-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="23948-126">Si vous essayez de tooconnect tooan base de données SQL Azure serveur logique au sein d’un pare-feu d’entreprise, ce port doit être ouvert dans le pare-feu d’entreprise hello pour toosuccessfully de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="23948-126">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

1. <span data-ttu-id="23948-127">Ouvrez SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="23948-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="23948-128">Bonjour **connecter tooServer** boîte de dialogue, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="23948-128">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="23948-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="23948-129">Setting</span></span>       | <span data-ttu-id="23948-130">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="23948-130">Suggested value</span></span> | <span data-ttu-id="23948-131">Description</span><span class="sxs-lookup"><span data-stu-id="23948-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="23948-132">**Type de serveur**</span><span class="sxs-lookup"><span data-stu-id="23948-132">**Server type**</span></span> | <span data-ttu-id="23948-133">Moteur de base de données</span><span class="sxs-lookup"><span data-stu-id="23948-133">Database engine</span></span> | <span data-ttu-id="23948-134">Cette valeur est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="23948-134">This value is required.</span></span> |
   | <span data-ttu-id="23948-135">**Nom du serveur**</span><span class="sxs-lookup"><span data-stu-id="23948-135">**Server name**</span></span> | <span data-ttu-id="23948-136">nom du serveur complet Hello</span><span class="sxs-lookup"><span data-stu-id="23948-136">hello fully qualified server name</span></span> | <span data-ttu-id="23948-137">Hello nom doit être semblable à celui-ci : **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="23948-137">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="23948-138">**Authentification**</span><span class="sxs-lookup"><span data-stu-id="23948-138">**Authentication**</span></span> | <span data-ttu-id="23948-139">l’authentification SQL Server</span><span class="sxs-lookup"><span data-stu-id="23948-139">SQL Server Authentication</span></span> | <span data-ttu-id="23948-140">L’authentification SQL est hello seul type d’authentification que nous avons configuré dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="23948-140">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="23948-141">**Connexion**</span><span class="sxs-lookup"><span data-stu-id="23948-141">**Login**</span></span> | <span data-ttu-id="23948-142">compte d’administrateur serveur Hello</span><span class="sxs-lookup"><span data-stu-id="23948-142">hello server admin account</span></span> | <span data-ttu-id="23948-143">Il s’agit de compte hello que vous avez spécifié lors de la création du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="23948-143">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="23948-144">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="23948-144">**Password**</span></span> | <span data-ttu-id="23948-145">mot de passe Hello pour votre compte d’administrateur de serveur</span><span class="sxs-lookup"><span data-stu-id="23948-145">hello password for your server admin account</span></span> | <span data-ttu-id="23948-146">Il s’agit d’un mot de passe hello que vous avez spécifié lors de la création du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="23948-146">This is hello password that you specified when you created hello server.</span></span> |

   ![se connecter tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="23948-148">Cliquez sur **Options** Bonjour **connecter tooserver** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="23948-148">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="23948-149">Bonjour **connecter toodatabase** section, entrez **mySampleDatabase** tooconnect toothis base de données.</span><span class="sxs-lookup"><span data-stu-id="23948-149">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![se connecter toodb sur le serveur](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="23948-151">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="23948-151">Click **Connect**.</span></span> <span data-ttu-id="23948-152">Ouvre la fenêtre de l’Explorateur d’objets Hello dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="23948-152">hello Object Explorer window opens in SSMS.</span></span> 

   ![tooserver connecté](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="23948-154">Dans l’Explorateur d’objets, développez **bases de données** , puis **mySampleDatabase** tooview des objets de hello dans la base de données exemple hello.</span><span class="sxs-lookup"><span data-stu-id="23948-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="23948-155">Données de requête</span><span class="sxs-lookup"><span data-stu-id="23948-155">Query data</span></span>

<span data-ttu-id="23948-156">Tooquery pour les produits de 20 premiers hello de code suivant de hello d’utilisation par catégorie à l’aide de hello [sélectionnez](https://msdn.microsoft.com/library/ms189499.aspx) instruction Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="23948-156">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="23948-157">Dans l’Explorateur d’objets, cliquez avec le bouton droit sur **mySampleDatabase**, puis cliquez sur **Nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="23948-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="23948-158">Une fenêtre de requête vide s’ouvre tooyour connecté de base de données.</span><span class="sxs-lookup"><span data-stu-id="23948-158">A blank query window opens that is connected tooyour database.</span></span>
2. <span data-ttu-id="23948-159">Dans la fenêtre de requête hello, entrez hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="23948-159">In hello query window, enter hello following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="23948-160">Dans la barre d’outils de hello, cliquez sur **Execute** tooretrieve des données à partir des tables Product et ProductCategory de hello.</span><span class="sxs-lookup"><span data-stu-id="23948-160">On hello toolbar, click **Execute** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="23948-162">Insertion des données</span><span class="sxs-lookup"><span data-stu-id="23948-162">Insert data</span></span>

<span data-ttu-id="23948-163">Utilisez hello de code suivant tooinsert un nouveau produit dans table de SalesLT.Product hello à l’aide de hello [insérer](https://msdn.microsoft.com/library/ms174335.aspx) instruction Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="23948-163">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="23948-164">Dans la fenêtre de requête hello, remplacez les requêtes précédentes hello hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="23948-164">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="23948-165">Dans la barre d’outils de hello, cliquez sur **Execute** tooinsert une nouvelle ligne dans la table Product de hello.</span><span class="sxs-lookup"><span data-stu-id="23948-165">On hello toolbar, click **Execute**  tooinsert a new row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="23948-166">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="23948-166">Update data</span></span>

<span data-ttu-id="23948-167">Tooupdate hello produit que vous avez ajouté précédemment à l’aide de hello de code suivant de hello utilisation [mise à jour](https://msdn.microsoft.com/library/ms177523.aspx) instruction Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="23948-167">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="23948-168">Dans la fenêtre de requête hello, remplacez les requêtes précédentes hello hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="23948-168">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="23948-169">Dans la barre d’outils de hello, cliquez sur **Execute** ligne spécifiée de tooupdate hello dans la table Product de hello.</span><span class="sxs-lookup"><span data-stu-id="23948-169">On hello toolbar, click **Execute** tooupdate hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="23948-170">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="23948-170">Delete data</span></span>

<span data-ttu-id="23948-171">Toodelete hello produit que vous avez ajouté précédemment à l’aide de hello de code suivant de hello utilisation [supprimer](https://msdn.microsoft.com/library/ms189835.aspx) instruction Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="23948-171">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="23948-172">Dans la fenêtre de requête hello, remplacez les requêtes précédentes hello hello suivant la requête :</span><span class="sxs-lookup"><span data-stu-id="23948-172">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="23948-173">Dans la barre d’outils de hello, cliquez sur **Execute** ligne spécifiée de toodelete hello dans la table Product de hello.</span><span class="sxs-lookup"><span data-stu-id="23948-173">On hello toolbar, click **Execute** toodelete hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="23948-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="23948-174">Next steps</span></span>

- <span data-ttu-id="23948-175">toolearn sur la création et la gestion des serveurs et bases de données avec Transact-SQL, consultez [en savoir plus sur les serveurs de base de données SQL Azure et les bases de données](sql-database-servers-databases.md).</span><span class="sxs-lookup"><span data-stu-id="23948-175">toolearn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="23948-176">Pour plus d’informations sur SSMS, consultez [Utiliser SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="23948-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="23948-177">tooconnect et la requête à l’aide de Visual Studio Code, consultez [se connecter et requête avec le Code de Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="23948-177">tooconnect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="23948-178">tooconnect et la requête à l’aide de .NET, consultez [se connecter et requête avec .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="23948-178">tooconnect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="23948-179">tooconnect et la requête à l’aide de PHP, consultez [se connecter et requête avec PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="23948-179">tooconnect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="23948-180">tooconnect et la requête à l’aide de Node.js, consultez [se connecter et requête avec Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="23948-180">tooconnect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="23948-181">tooconnect et la requête à l’aide de Java, consultez [se connecter et requête avec Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="23948-181">tooconnect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="23948-182">tooconnect et la requête à l’aide de Python, consultez [se connecter et requête avec Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="23948-182">tooconnect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="23948-183">tooconnect et la requête à l’aide de Ruby, consultez [se connecter et requête Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="23948-183">tooconnect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
