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
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Utiliser Ruby tooquery une base de données SQL Azure

Ce didacticiel de démarrage rapide montre comment toouse [Ruby](https://www.ruby-lang.org) toocreate un tooan tooconnect de programme SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.

## <a name="prerequisites"></a>Composants requis

toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivant des conditions préalables :

- base de données SQL Azure. Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides : 

   - [Créer une base de données - Portail](sql-database-get-started-portal.md)
   - [Créer une base de données - CLI](sql-database-get-started-cli.md)
   - [Créer une base de données - PowerShell](sql-database-get-started-powershell.md)

- A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.
- Vous avez installé Ruby et les logiciels connexes pour votre système d’exploitation.
    - **MacOS** : installez Homebrew installez rbenv et ruby-build, installez Ruby, puis installez FreeTDS. Consultez les [étapes 1.2, 1.3, 1.4 et 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu** : installez les éléments requis pour Ruby, installez rbenv et ruby-build, installez Ruby, puis installez FreeTDS. Consultez les [étapes 1.2, 1.3, 1.4 et 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Informations de connexion SQL Server

Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database. Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 
3. Sur hello **vue d’ensemble** pour votre base de données, vérifiez le nom du serveur complet hello. Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option, comme indiqué dans hello suivant image :

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si vous avez oublié des informations de connexion hello pour votre serveur de base de données SQL Azure, accédez nom d’administrateur serveur page tooview hello toohello base de données SQL server et, si nécessaire, réinitialiser un mot de passe hello.

> [!IMPORTANT]
> Vous devez disposer d’une règle de pare-feu en place pour hello IP adresse publique de hello ordinateur sur lequel vous effectuez ce didacticiel. Si vous se trouvent sur un autre ordinateur ou que vous avez une autre adresse IP publique, créez un [règle de pare-feu de niveau serveur à l’aide de hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Insérer la base de données SQL de code tooquery

1. Dans votre éditeur de texte favori, créez un nouveau fichier nommé **sqltest.rb**

2. Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.

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

## <a name="run-hello-code"></a>Exécuter le code de hello

1. À l’invite de commandes hello exécutez hello suivant de commandes :

   ```bash
   ruby sqltest.rb
   ```

2. Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.


## <a name="next-steps"></a>Étapes suivantes
- [Concevoir votre première base de données SQL Azure](sql-database-design-first-database.md)
- [GitHub repository for TinyTDS](https://github.com/rails-sqlserver/tiny_tds) (Référentiel GitHub pour TinyTDS)
- [Signaler des problèmes ou poser des questions sur TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Ruby Driver for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/) (Pilote Ruby pour SQL Server)
