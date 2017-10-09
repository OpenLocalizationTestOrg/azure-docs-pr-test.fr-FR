---
title: "aaaUse PHP tooquery base de données SQL Azure | Documents Microsoft"
description: "Cette rubrique vous montre comment toouse PHP toocreate un programme qui se connecte tooan base de données SQL Azure et requête à l’aide d’instructions Transact-SQL."
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
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="1fc6c-103">Utilisez PHP tooquery une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1fc6c-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="1fc6c-104">Ce didacticiel de démarrage rapide montre comment toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate un tooan tooconnect de programme SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fc6c-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1fc6c-105">Prerequisites</span></span>

<span data-ttu-id="1fc6c-106">toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1fc6c-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="1fc6c-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-107">An Azure SQL database.</span></span> <span data-ttu-id="1fc6c-108">Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="1fc6c-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="1fc6c-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="1fc6c-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="1fc6c-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="1fc6c-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="1fc6c-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fc6c-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="1fc6c-112">A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="1fc6c-113">Vous avez installé PHP et les logiciels connexes pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="1fc6c-114">**MacOS**: Homebrew d’installer PHP, installez le pilote ODBC de hello et SQLCMD et installez-les hello pilote PHP pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="1fc6c-115">Consultez les [étapes 1.2, 1.3 et 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span><span class="sxs-lookup"><span data-stu-id="1fc6c-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="1fc6c-116">**Ubuntu**: installation de PHP et d’autres requis des packages, puis installer hello pilote PHP pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="1fc6c-117">Consultez les [étapes 1.2 et 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="1fc6c-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="1fc6c-118">**Windows**: installation hello dernière version de PHP pour IIS Express, la version la plus récente de Microsoft Drivers for SQL Server dans IIS Express Chocolatey, pilote ODBC de hello et SQLCMD hello.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="1fc6c-119">Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span><span class="sxs-lookup"><span data-stu-id="1fc6c-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="1fc6c-120">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="1fc6c-120">SQL server connection information</span></span>

<span data-ttu-id="1fc6c-121">Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="1fc6c-122">Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="1fc6c-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1fc6c-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1fc6c-124">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="1fc6c-125">Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="1fc6c-126">Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="1fc6c-128">Si vous oubliez vos informations de connexion du serveur, accédez de nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="1fc6c-129">Insérer la base de données SQL de code tooquery</span><span class="sxs-lookup"><span data-stu-id="1fc6c-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="1fc6c-130">Dans votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.php**.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="1fc6c-131">Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
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

## <a name="run-hello-code"></a><span data-ttu-id="1fc6c-132">Exécuter le code de hello</span><span class="sxs-lookup"><span data-stu-id="1fc6c-132">Run hello code</span></span>

1. <span data-ttu-id="1fc6c-133">À l’invite de commandes hello exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1fc6c-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="1fc6c-134">Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1fc6c-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fc6c-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1fc6c-135">Next steps</span></span>
- [<span data-ttu-id="1fc6c-136">Concevoir votre première base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1fc6c-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="1fc6c-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/) (Pilotes PHP Microsoft pour SQL Server)</span><span class="sxs-lookup"><span data-stu-id="1fc6c-137">[Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/)</span></span>
- [<span data-ttu-id="1fc6c-138">Signaler des problèmes ou poser des questions</span><span class="sxs-lookup"><span data-stu-id="1fc6c-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
