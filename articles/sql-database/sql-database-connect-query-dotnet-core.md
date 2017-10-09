---
title: "aaaUse .NET Core tooquery base de données SQL Azure | Documents Microsoft"
description: "Cette rubrique vous montre comment toouse .NET Core toocreate un programme qui se connecte tooan base de données SQL Azure et les interroger à l’aide d’instructions Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 2d10c407f44f43b6baa3bf337cdd1173d9c9c35f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a>Utiliser le .NET Core (c#) tooquery une base de données SQL Azure

Ce didacticiel de démarrage rapide montre comment toouse [.NET Core](https://www.microsoft.com/net/) sur Linux/Windows/macOS toocreate c# programme tooconnect tooan SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.

## <a name="prerequisites"></a>Composants requis

toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivantes :

- base de données SQL Azure. Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides : 

   - [Créer une base de données - Portail](sql-database-get-started-portal.md)
   - [Créer une base de données - CLI](sql-database-get-started-cli.md)
   - [Créer une base de données - PowerShell](sql-database-get-started-powershell.md)

- A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.
- Vous avez installé [.NET Core pour votre système d’exploitation](https://www.microsoft.com/net/core). 

## <a name="sql-server-connection-information"></a>Informations de connexion SQL Server

Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database. Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 
3. Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image. Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option. 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si vous oubliez vos informations de connexion de serveur de base de données SQL Azure, accédez à nom d’administrateur serveur page tooview hello toohello base de données SQL server. Vous pouvez réinitialiser le mot de passe hello si nécessaire.

5. Cliquez sur **Afficher les chaînes de connexion de la base de données**.

6. Hello révision complète **ADO.NET** chaîne de connexion.

    ![Chaîne de connexion ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> Vous devez disposer d’une règle de pare-feu en place pour hello IP adresse publique de hello ordinateur sur lequel vous effectuez ce didacticiel. Si vous se trouvent sur un autre ordinateur ou que vous avez une autre adresse IP publique, créez un [règle de pare-feu de niveau serveur à l’aide de hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 
>
  
## <a name="create-a-new-net-project"></a>Création d'un nouveau projet .NET

1. Ouvrez une invite de commandes et créez un dossier nommé *sqltest*. Accédez toohello dossier vous avez créé et que vous exécutez hello de commande suivante :

    ```
    dotnet new console
    ```

2. Ouvrez ***sqltest.csproj*** avec votre éditeur de texte et ajoutez System.Data.SqlClient en tant que dépendance à l’aide de hello suivant de code :

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a>Insérer la base de données SQL de code tooquery

1. Dans votre environnement de développement ou votre éditeur de texte favori, ouvrez **Program.cs**

2. Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a>Exécuter le code de hello

1. À l’invite de commandes hello exécutez hello suivant de commandes :

   ```csharp
   dotnet restore
   dotnet run
   ```

2. Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.


## <a name="next-steps"></a>Étapes suivantes

- [Prise en main de .NET Core sur Windows/Linux/macOS à l’aide de la ligne de commande hello](/dotnet/core/tutorials/using-with-xplat-cli).
- Découvrez comment trop[connecter et interroger une base de données SQL Azure à l’aide de hello .NET framework et Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).  
- Découvrez comment trop[concevoir votre première base de données SQL Azure à l’aide de SSMS](sql-database-design-first-database.md) ou [concevoir votre première base de données SQL Azure à l’aide de .NET](sql-database-design-first-database-csharp.md).
- Pour plus d’informations sur .NET, consultez la [documentation .NET](https://docs.microsoft.com/dotnet/).
