---
title: "aaaUse Python tooquery base de données SQL Azure | Documents Microsoft"
description: "Cette rubrique vous montre comment toouse Python toocreate un programme qui se connecte tooan base de données SQL Azure et requête à l’aide d’instructions Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="31df5-103">Utiliser Python tooquery une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="31df5-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="31df5-104">Ce démarrage rapide montre comment toouse [Python](https://python.org) tooconnect tooan SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="31df5-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31df5-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="31df5-105">Prerequisites</span></span>

<span data-ttu-id="31df5-106">toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="31df5-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="31df5-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="31df5-107">An Azure SQL database.</span></span> <span data-ttu-id="31df5-108">Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="31df5-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="31df5-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="31df5-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="31df5-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="31df5-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="31df5-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="31df5-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="31df5-112">A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="31df5-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="31df5-113">Vous avez installé Python et les logiciels connexes pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="31df5-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="31df5-114">**MacOS**: Homebrew d’installer Python, installez le pilote ODBC de hello et SQLCMD et installez-les hello Python Driver pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="31df5-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="31df5-115">Consultez les [étapes 1.2, 1.3 et 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="31df5-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="31df5-116">**Ubuntu**: requis Python d’installer et d’autres packages, puis installer hello Python Driver pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="31df5-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="31df5-117">Consultez les [étapes 1.2, 1.3 et 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="31df5-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="31df5-118">**Windows**: installer la version la plus récente de Python (variable d’environnement est désormais configurée pour vous) hello, installez le pilote ODBC de hello et SQLCMD, puis installez hello Python Driver pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="31df5-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="31df5-119">Consultez les [étapes 1.2, 1.3 et 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="31df5-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="31df5-120">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="31df5-120">SQL server connection information</span></span>

<span data-ttu-id="31df5-121">Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="31df5-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="31df5-122">Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="31df5-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="31df5-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="31df5-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="31df5-124">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="31df5-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="31df5-125">Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="31df5-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="31df5-126">Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.</span><span class="sxs-lookup"><span data-stu-id="31df5-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="31df5-128">Si vous oubliez vos informations de connexion du serveur, accédez de nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="31df5-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="31df5-129">Insérer la base de données SQL de code tooquery</span><span class="sxs-lookup"><span data-stu-id="31df5-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="31df5-130">Dans votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="31df5-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="31df5-131">Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="31df5-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="31df5-132">Exécuter le code de hello</span><span class="sxs-lookup"><span data-stu-id="31df5-132">Run hello code</span></span>

1. <span data-ttu-id="31df5-133">À l’invite de commandes hello exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="31df5-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="31df5-134">Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="31df5-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31df5-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31df5-135">Next steps</span></span>

- [<span data-ttu-id="31df5-136">Concevoir votre première base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="31df5-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- <span data-ttu-id="31df5-137">[Python SQL Driver](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/) (Pilote SQL Python)</span><span class="sxs-lookup"><span data-stu-id="31df5-137">[Microsoft Python Drivers for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)</span></span>
- [<span data-ttu-id="31df5-138">Centre de développement Python</span><span class="sxs-lookup"><span data-stu-id="31df5-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

