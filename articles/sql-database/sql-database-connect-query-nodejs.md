---
title: "Utilisation de Node.js pour interroger Azure SQL Database | Microsoft Docs"
description: "Cette rubrique vous explique comment utiliser Node.js pour créer un programme qui se connecte à une base de données SQL Azure et l’interroger à l’aide d’instructions Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 1907a95df9132c059d7985b6d5cd913536bf3403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-nodejs-to-query-an-azure-sql-database"></a><span data-ttu-id="02285-103">Utilisation de Node.js pour interroger une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="02285-103">Use Node.js to query an Azure SQL database</span></span>

<span data-ttu-id="02285-104">Ce didacticiel de démarrage rapide indique comment utiliser [Node.js](https://nodejs.org/en/) pour créer un programme qui se connecte à une base de données SQL Azure et utiliser des instructions Transact-SQL pour interroger des données.</span><span class="sxs-lookup"><span data-stu-id="02285-104">This quick start tutorial demonstrates how to use [Node.js](https://nodejs.org/en/) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02285-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="02285-105">Prerequisites</span></span>

<span data-ttu-id="02285-106">Pour suivre ce didacticiel de démarrage rapide, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="02285-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="02285-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02285-107">An Azure SQL database.</span></span> <span data-ttu-id="02285-108">Ce guide de démarrage rapide utilise les ressources créées dans l’une de ces instructions de démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="02285-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="02285-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="02285-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="02285-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="02285-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="02285-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="02285-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="02285-112">Une [règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de l’ordinateur que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="02285-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="02285-113">Vous avez installé Node.js et les logiciels connexes pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="02285-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="02285-114">**MacOS** : installez Homebrew et Node.js, puis installez le pilote ODBC et SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="02285-114">**MacOS**: Install Homebrew and Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="02285-115">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="02285-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="02285-116">**Ubuntu** : installez Node.js, puis installez le pilote ODBC et SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="02285-116">**Ubuntu**: Install Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="02285-117">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="02285-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="02285-118">**Windows** : installez Chocolatey et Node.js, puis installez le pilote ODBC et SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="02285-118">**Windows**: Install Chocolatey and Node.js, and then install the ODBC driver and SQL CMD.</span></span> <span data-ttu-id="02285-119">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="02285-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="02285-120">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="02285-120">SQL server connection information</span></span>

<span data-ttu-id="02285-121">Obtenez les informations de connexion requises pour la connexion à la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02285-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="02285-122">Vous aurez besoin du nom du serveur complet, du nom de la base de données et des informations de connexion dans les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="02285-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="02285-123">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02285-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="02285-124">Sélectionnez **Bases de données SQL** dans le menu de gauche, puis cliquez sur votre base de données dans la page **Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="02285-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="02285-125">Sur la page **Vue d’ensemble** de votre base de données, vérifiez le nom complet du serveur, comme indiqué dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="02285-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="02285-126">Vous pouvez pointer sur le nom du serveur pour afficher l’option **Cliquez pour copier**.</span><span class="sxs-lookup"><span data-stu-id="02285-126">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="02285-128">Si vous avez oublié vos informations de connexion à votre serveur Azure SQL Database, accédez à la page du serveur SQL Database pour afficher le nom de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="02285-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02285-129">Une règle de pare-feu doit être en place pour l’adresse IP publique de l’ordinateur sur lequel vous effectuez ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="02285-129">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="02285-130">Si vous êtes sur un autre ordinateur ou si vous avez une autre adresse IP publique, créez une [règle de pare-feu au niveau du serveur à l’aide du portail Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="02285-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="02285-131">Création d’un projet Node.js</span><span class="sxs-lookup"><span data-stu-id="02285-131">Create a Node.js project</span></span>

<span data-ttu-id="02285-132">Ouvrez une invite de commandes et créez un dossier nommé *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="02285-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="02285-133">Accédez au dossier que vous avez créé et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02285-133">Navigate to the folder you created and run the following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="02285-134">Insertion du code pour interroger la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="02285-134">Insert code to query SQL database</span></span>

1. <span data-ttu-id="02285-135">Dans votre environnement de développement ou votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="02285-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="02285-136">Remplacez le contenu par le code suivant et ajoutez les valeurs appropriées pour votre serveur, base de données, utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="02285-136">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection to database
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt to connect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from the Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-the-code"></a><span data-ttu-id="02285-137">Exécution du code</span><span class="sxs-lookup"><span data-stu-id="02285-137">Run the code</span></span>

1. <span data-ttu-id="02285-138">Exécutez ensuite les commandes suivantes dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="02285-138">At the command prompt, run the following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="02285-139">Vérifiez que les 20 premières lignes sont renvoyées, puis fermez la fenêtre d’application.</span><span class="sxs-lookup"><span data-stu-id="02285-139">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02285-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02285-140">Next steps</span></span>

- <span data-ttu-id="02285-141">En savoir plus sur le [pilote Microsoft Node.js pour SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="02285-141">Learn about the [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="02285-142">Découvrez comment [connecter et interroger une base de données SQL Azure à l’aide de .NET Core](sql-database-connect-query-dotnet-core.md) sur Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="02285-142">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="02285-143">En savoir plus sur la [prise en main de .NET Core sur Windows/Linux/macOS à l’aide de la ligne de commande](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="02285-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="02285-144">Découvrez comment [concevoir votre première base de données SQL Azure à l’aide de SSMS](sql-database-design-first-database.md) ou [concevoir votre première base de données SQL Azure à l’aide de .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="02285-144">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="02285-145">Découvrez comment [se connecter et effectuer des requêtes avec SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="02285-145">Learn how to [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="02285-146">Découvrez comment [se connecter et effectuer des requêtes avec Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="02285-146">Learn how to [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


