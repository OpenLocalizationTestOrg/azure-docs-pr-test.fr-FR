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
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a>Utiliser Node.js tooquery une base de données SQL Azure

Ce didacticiel de démarrage rapide montre comment toouse [Node.js](https://nodejs.org/en/) toocreate un tooan tooconnect de programme SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.

## <a name="prerequisites"></a>Composants requis

toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivantes :

- base de données SQL Azure. Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides : 

   - [Créer une base de données - Portail](sql-database-get-started-portal.md)
   - [Créer une base de données - CLI](sql-database-get-started-cli.md)
   - [Créer une base de données - PowerShell](sql-database-get-started-powershell.md)

- A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.
- Vous avez installé Node.js et les logiciels connexes pour votre système d’exploitation.
    - **MacOS**: installer Homebrew et Node.js, puis installez le pilote ODBC de hello et SQLCMD. Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).
    - **Ubuntu**: installer Node.js, puis installez le pilote ODBC de hello et SQLCMD. Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/).
    - **Windows**: installer Chocolatey et Node.js, puis installez le pilote ODBC de hello et SQL CMD. Consultez les [étapes 1.2 et 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).

## <a name="sql-server-connection-information"></a>Informations de connexion SQL Server

Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database. Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 
3. Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image. Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si vous avez oublié des informations de connexion hello pour votre serveur de base de données SQL Azure, accédez nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.

> [!IMPORTANT]
> Vous devez disposer d’une règle de pare-feu en place pour hello IP adresse publique de hello ordinateur sur lequel vous effectuez ce didacticiel. Si vous se trouvent sur un autre ordinateur ou que vous avez une autre adresse IP publique, créez un [règle de pare-feu de niveau serveur à l’aide de hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="create-a-nodejs-project"></a>Création d’un projet Node.js

Ouvrez une invite de commandes et créez un dossier nommé *sqltest*. Accédez toohello dossier vous avez créé et que vous exécutez hello de commande suivante :

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a>Insérer la base de données SQL de code tooquery

1. Dans votre environnement de développement ou votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.js**.

2. Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.

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

## <a name="run-hello-code"></a>Exécuter le code de hello

1. À l’invite de commandes hello exécutez hello suivant de commandes :

   ```js
   node sqltest.js
   ```

2. Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)
- Découvrez comment trop[connecter et interroger une base de données SQL Azure à l’aide de .NET core](sql-database-connect-query-dotnet-core.md) sur Linux/Windows/macOS.  
- En savoir plus sur [prise en main de .NET Core sur Windows/Linux/macOS à l’aide de la ligne de commande hello](/dotnet/core/tutorials/using-with-xplat-cli).
- Découvrez comment trop[concevoir votre première base de données SQL Azure à l’aide de SSMS](sql-database-design-first-database.md) ou [concevoir votre première base de données SQL Azure à l’aide de .NET](sql-database-design-first-database-csharp.md).
- Découvrez comment trop[se connecter et requête avec SSMS](sql-database-connect-query-ssms.md)
- Découvrez comment trop[se connecter et requête avec le Code de Visual Studio](sql-database-connect-query-vscode.md).


