---
title: "aaaUse Node.js tooquery base de données SQL Azure | Documents Microsoft"
description: "Cette rubrique vous montre comment toouse Node.js toocreate un programme qui se connecte tooan base de données SQL Azure et requête à l’aide d’instructions Transact-SQL."
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
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="b135f-103">Utiliser Node.js tooquery une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b135f-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="b135f-104">Ce didacticiel de démarrage rapide montre comment toouse [Node.js](https://nodejs.org/en/) toocreate un tooan tooconnect de programme SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="b135f-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b135f-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b135f-105">Prerequisites</span></span>

<span data-ttu-id="b135f-106">toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="b135f-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="b135f-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b135f-107">An Azure SQL database.</span></span> <span data-ttu-id="b135f-108">Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="b135f-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="b135f-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="b135f-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="b135f-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="b135f-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="b135f-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b135f-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="b135f-112">A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="b135f-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="b135f-113">Vous avez installé Node.js et les logiciels connexes pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="b135f-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="b135f-114">**MacOS**: installer Homebrew et Node.js, puis installez le pilote ODBC de hello et SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="b135f-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="b135f-115">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span><span class="sxs-lookup"><span data-stu-id="b135f-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="b135f-116">**Ubuntu**: installer Node.js, puis installez le pilote ODBC de hello et SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="b135f-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="b135f-117">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="b135f-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="b135f-118">**Windows**: installer Chocolatey et Node.js, puis installez le pilote ODBC de hello et SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="b135f-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="b135f-119">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span><span class="sxs-lookup"><span data-stu-id="b135f-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="b135f-120">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="b135f-120">SQL server connection information</span></span>

<span data-ttu-id="b135f-121">Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="b135f-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="b135f-122">Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="b135f-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="b135f-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b135f-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b135f-124">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="b135f-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="b135f-125">Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="b135f-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="b135f-126">Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.</span><span class="sxs-lookup"><span data-stu-id="b135f-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="b135f-128">Si vous avez oublié des informations de connexion hello pour votre serveur de base de données SQL Azure, accédez nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="b135f-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b135f-129">Vous devez disposer d’une règle de pare-feu en place pour hello IP adresse publique de hello ordinateur sur lequel vous effectuez ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b135f-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="b135f-130">Si vous se trouvent sur un autre ordinateur ou que vous avez une autre adresse IP publique, créez un [règle de pare-feu de niveau serveur à l’aide de hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="b135f-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="b135f-131">Création d’un projet Node.js</span><span class="sxs-lookup"><span data-stu-id="b135f-131">Create a Node.js project</span></span>

<span data-ttu-id="b135f-132">Ouvrez une invite de commandes et créez un dossier nommé *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="b135f-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="b135f-133">Accédez toohello dossier vous avez créé et que vous exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b135f-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="b135f-134">Insérer la base de données SQL de code tooquery</span><span class="sxs-lookup"><span data-stu-id="b135f-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="b135f-135">Dans votre environnement de développement ou votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.js**.</span><span class="sxs-lookup"><span data-stu-id="b135f-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="b135f-136">Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b135f-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
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

   // Attempt tooconnect and execute queries if connection goes through
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
      { console.log('Reading rows from hello Table...');

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

## <a name="run-hello-code"></a><span data-ttu-id="b135f-137">Exécuter le code de hello</span><span class="sxs-lookup"><span data-stu-id="b135f-137">Run hello code</span></span>

1. <span data-ttu-id="b135f-138">À l’invite de commandes hello exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="b135f-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="b135f-139">Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b135f-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b135f-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b135f-140">Next steps</span></span>

- <span data-ttu-id="b135f-141">En savoir plus sur hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="b135f-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="b135f-142">Découvrez comment trop[connecter et interroger une base de données SQL Azure à l’aide de .NET core](sql-database-connect-query-dotnet-core.md) sur Linux/Windows/macOS.</span><span class="sxs-lookup"><span data-stu-id="b135f-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="b135f-143">En savoir plus sur [prise en main de .NET Core sur Windows/Linux/macOS à l’aide de la ligne de commande hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b135f-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="b135f-144">Découvrez comment trop[concevoir votre première base de données SQL Azure à l’aide de SSMS](sql-database-design-first-database.md) ou [concevoir votre première base de données SQL Azure à l’aide de .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b135f-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="b135f-145">Découvrez comment trop[se connecter et requête avec SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="b135f-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="b135f-146">Découvrez comment trop[se connecter et requête avec le Code de Visual Studio](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="b135f-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


