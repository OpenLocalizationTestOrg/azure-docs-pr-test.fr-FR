---
title: "Utilisation de PHP pour interroger Azure SQL Database | Microsoft Docs"
description: "Cette rubrique vous explique comment utiliser PHP pour créer un programme qui se connecte à une base de données SQL Azure et l’interroger à l’aide d’instructions Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a43472ad2be4a0fd6f7126f72433acd8b5f25fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-php-to-query-an-azure-sql-database"></a><span data-ttu-id="8e8f4-103">Utilisation de PHP pour interroger une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8e8f4-103">Use PHP to query an Azure SQL database</span></span>

<span data-ttu-id="8e8f4-104">Ce didacticiel de démarrage rapide indique comment utiliser [PHP](http://php.net/manual/en/intro-whatis.php) pour créer un programme qui se connecte à une base de données SQL Azure et utiliser des instructions Transact-SQL pour interroger des données.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-104">This quick start tutorial demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e8f4-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e8f4-105">Prerequisites</span></span>

<span data-ttu-id="8e8f4-106">Pour suivre ce didacticiel de démarrage rapide, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8e8f4-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="8e8f4-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-107">An Azure SQL database.</span></span> <span data-ttu-id="8e8f4-108">Ce guide de démarrage rapide utilise les ressources créées dans l’une de ces instructions de démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="8e8f4-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="8e8f4-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="8e8f4-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="8e8f4-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="8e8f4-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="8e8f4-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e8f4-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="8e8f4-112">Une [règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de l’ordinateur que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="8e8f4-113">Vous avez installé PHP et les logiciels connexes pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="8e8f4-114">**MacOS** : installez Homebrew et PHP, installez le pilote ODBC et SQLCMD, puis installez le pilote PHP pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-114">**MacOS**: Install Homebrew and PHP, install the ODBC driver and SQLCMD, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="8e8f4-115">Consultez les [étapes 1.2, 1.3 et 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="8e8f4-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="8e8f4-116">**Ubuntu** : installez PHP et les autres packages requis, puis installez le pilote PHP pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-116">**Ubuntu**:  Install PHP and other required packages, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="8e8f4-117">Consultez les [étapes 1.2 et 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="8e8f4-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="8e8f4-118">**Windows**: installez la version la plus récente de PHP pour IIS Express, la version la plus récente des Pilotes Microsoft SQL Server dans IIS Express, Chocolatey, le pilote ODBC et SQLCMD.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-118">**Windows**: Install the newest version of PHP for IIS Express, the newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, the ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="8e8f4-119">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="8e8f4-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="8e8f4-120">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e8f4-120">SQL server connection information</span></span>

<span data-ttu-id="8e8f4-121">Obtenez les informations de connexion requises pour la connexion à la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="8e8f4-122">Vous aurez besoin du nom du serveur complet, du nom de la base de données et des informations de connexion dans les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="8e8f4-123">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8e8f4-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8e8f4-124">Sélectionnez **Bases de données SQL** dans le menu de gauche, puis cliquez sur votre base de données dans la page **Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="8e8f4-125">Sur la page **Vue d’ensemble** de votre base de données, vérifiez le nom complet du serveur, comme indiqué dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="8e8f4-126">Vous pouvez pointer sur le nom du serveur pour afficher l’option **Cliquez pour copier**.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="8e8f4-128">Si vous avez oublié vos informations de connexion au serveur, accédez à la page du serveur SQL Database pour afficher le nom de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="8e8f4-129">Insertion du code pour interroger la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="8e8f4-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="8e8f4-130">Dans votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="8e8f4-131">Remplacez le contenu par le code suivant et ajoutez les valeurs appropriées pour votre serveur, base de données, utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes the connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-the-code"></a><span data-ttu-id="8e8f4-132">Exécution du code</span><span class="sxs-lookup"><span data-stu-id="8e8f4-132">Run the code</span></span>

1. <span data-ttu-id="8e8f4-133">Exécutez ensuite les commandes suivantes dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="8e8f4-133">At the command prompt, run the following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="8e8f4-134">Vérifiez que les 20 premières lignes sont renvoyées, puis fermez la fenêtre d’application.</span><span class="sxs-lookup"><span data-stu-id="8e8f4-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e8f4-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e8f4-135">Next steps</span></span>
- [<span data-ttu-id="8e8f4-136">Concevoir votre première base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8e8f4-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="8e8f4-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/) (Pilotes PHP Microsoft pour SQL Server)</span><span class="sxs-lookup"><span data-stu-id="8e8f4-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/)</span></span>
- [<span data-ttu-id="8e8f4-138">Signaler des problèmes ou poser des questions</span><span class="sxs-lookup"><span data-stu-id="8e8f4-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
