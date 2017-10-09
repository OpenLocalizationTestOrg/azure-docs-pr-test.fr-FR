---
title: "aaaUse Ruby tooquery de base de données SQL Azure | Documents Microsoft"
description: "Cette rubrique vous montre comment toouse Ruby toocreate un programme qui se connecte tooan base de données SQL Azure et requête à l’aide d’instructions Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a><span data-ttu-id="1b589-103">Utiliser Ruby tooquery une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b589-103">Use Ruby tooquery an Azure SQL database</span></span>

<span data-ttu-id="1b589-104">Ce didacticiel de démarrage rapide montre comment toouse [Ruby](https://www.ruby-lang.org) toocreate un tooan tooconnect de programme SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="1b589-104">This quick start tutorial demonstrates how toouse [Ruby](https://www.ruby-lang.org) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b589-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1b589-105">Prerequisites</span></span>

<span data-ttu-id="1b589-106">toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="1b589-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="1b589-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b589-107">An Azure SQL database.</span></span> <span data-ttu-id="1b589-108">Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="1b589-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="1b589-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="1b589-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="1b589-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="1b589-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="1b589-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b589-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="1b589-112">A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="1b589-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="1b589-113">Vous avez installé Ruby et les logiciels connexes pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1b589-113">You have installed Ruby and related software for your operating system.</span></span>
    - <span data-ttu-id="1b589-114">**MacOS** : installez Homebrew installez rbenv et ruby-build, installez Ruby, puis installez FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="1b589-114">**MacOS**: Install Homebrew, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="1b589-115">Consultez les [étapes 1.2, 1.3, 1.4 et 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span><span class="sxs-lookup"><span data-stu-id="1b589-115">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).</span></span>
    - <span data-ttu-id="1b589-116">**Ubuntu** : installez les éléments requis pour Ruby, installez rbenv et ruby-build, installez Ruby, puis installez FreeTDS.</span><span class="sxs-lookup"><span data-stu-id="1b589-116">**Ubuntu**: Install prerequisites for Ruby, install rbenv and ruby-build, install Ruby, and then install FreeTDS.</span></span> <span data-ttu-id="1b589-117">Consultez les [étapes 1.2, 1.3, 1.4 et 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="1b589-117">See [Step 1.2, 1.3, 1.4, and 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="1b589-118">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="1b589-118">SQL server connection information</span></span>

<span data-ttu-id="1b589-119">Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1b589-119">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="1b589-120">Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="1b589-120">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="1b589-121">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b589-121">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1b589-122">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="1b589-122">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="1b589-123">Sur hello **vue d’ensemble** pour votre base de données, vérifiez le nom du serveur complet hello.</span><span class="sxs-lookup"><span data-stu-id="1b589-123">On hello **Overview** page for your database, review hello fully qualified server name.</span></span> <span data-ttu-id="1b589-124">Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option, comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="1b589-124">You can hover over hello server name toobring up hello **Click toocopy** option, as shown in hello following image:</span></span>

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="1b589-126">Si vous avez oublié des informations de connexion hello pour votre serveur de base de données SQL Azure, accédez nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="1b589-126">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b589-127">Vous devez disposer d’une règle de pare-feu en place pour hello IP adresse publique de hello ordinateur sur lequel vous effectuez ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1b589-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="1b589-128">Si vous se trouvent sur un autre ordinateur ou que vous avez une autre adresse IP publique, créez un [règle de pare-feu de niveau serveur à l’aide de hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="1b589-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="1b589-129">Insérer la base de données SQL de code tooquery</span><span class="sxs-lookup"><span data-stu-id="1b589-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="1b589-130">Dans votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.rb**</span><span class="sxs-lookup"><span data-stu-id="1b589-130">In your favorite text editor, create a new file, **sqltest.rb**</span></span>

2. <span data-ttu-id="1b589-131">Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1b589-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a><span data-ttu-id="1b589-132">Exécuter le code de hello</span><span class="sxs-lookup"><span data-stu-id="1b589-132">Run hello code</span></span>

1. <span data-ttu-id="1b589-133">À l’invite de commandes hello exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1b589-133">At hello command prompt, run hello following commands:</span></span>

   ```bash
   ruby sqltest.rb
   ```

2. <span data-ttu-id="1b589-134">Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1b589-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b589-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b589-135">Next Steps</span></span>
- [<span data-ttu-id="1b589-136">Concevoir votre première base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b589-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="1b589-137">[GitHub repository for TinyTDS](https://github.com/rails-sqlserver/tiny_tds) (Référentiel GitHub pour TinyTDS)</span><span class="sxs-lookup"><span data-stu-id="1b589-137">[GitHub repository for TinyTDS](https://github.com/rails-sqlserver/tiny_tds)</span></span>
- [<span data-ttu-id="1b589-138">Signaler des problèmes ou poser des questions sur TinyTDS</span><span class="sxs-lookup"><span data-stu-id="1b589-138">Report issues or ask questions about TinyTDS</span></span>](https://github.com/rails-sqlserver/tiny_tds/issues)
- <span data-ttu-id="1b589-139">[Ruby Driver for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/) (Pilote Ruby pour SQL Server)</span><span class="sxs-lookup"><span data-stu-id="1b589-139">[Ruby Drivers for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)</span></span>
