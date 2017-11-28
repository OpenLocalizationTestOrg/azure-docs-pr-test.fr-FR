---
title: "Utilisation de .NET Core pour interroger Azure SQL Database | Microsoft Docs"
description: "Cette rubrique vous explique comment utiliser .NET Core pour créer un programme qui se connecte à une base de données SQL Azure et l’interroger à l’aide d’instructions Transact-SQL."
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
ms.openlocfilehash: 046322624d3b89bb983acee863534256fee94b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-core-c-to-query-an-azure-sql-database"></a><span data-ttu-id="f7bb4-103">Utilisation de .NET Core (C#) pour interroger une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f7bb4-103">Use .NET Core (C#) to query an Azure SQL database</span></span>

<span data-ttu-id="f7bb4-104">Ce didacticiel de démarrage rapide indique comment utiliser [.NET Core](https://www.microsoft.com/net/) sur Windows/Linux/macOS pour créer un programme C# qui se connecte à une base de données SQL Azure et utiliser des instructions Transact-SQL pour interroger des données.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-104">This quick start tutorial demonstrates how to use [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS to create a C# program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7bb4-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f7bb4-105">Prerequisites</span></span>

<span data-ttu-id="f7bb4-106">Pour suivre ce didacticiel de démarrage rapide, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f7bb4-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="f7bb4-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-107">An Azure SQL database.</span></span> <span data-ttu-id="f7bb4-108">Ce guide de démarrage rapide utilise les ressources créées dans l’une de ces instructions de démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="f7bb4-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="f7bb4-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="f7bb4-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="f7bb4-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="f7bb4-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="f7bb4-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7bb4-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="f7bb4-112">Une [règle de pare-feu au niveau du serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de l’ordinateur que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="f7bb4-113">Vous avez installé [.NET Core pour votre système d’exploitation](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="f7bb4-114">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="f7bb4-114">SQL server connection information</span></span>

<span data-ttu-id="f7bb4-115">Obtenez les informations de connexion requises pour la connexion à la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="f7bb4-116">Vous aurez besoin du nom du serveur complet, du nom de la base de données et des informations de connexion dans les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="f7bb4-117">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f7bb4-118">Sélectionnez **Bases de données SQL** dans le menu de gauche, puis cliquez sur votre base de données dans la page **Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="f7bb4-119">Sur la page **Vue d’ensemble** de votre base de données, vérifiez le nom complet du serveur, comme indiqué dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="f7bb4-120">Vous pouvez pointer sur le nom du serveur pour afficher l’option **Cliquez pour copier**.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="f7bb4-122">Si vous avez oublié vos informations de connexion au serveur Azure SQL Database, accédez à la page du serveur SQL Database pour afficher le nom de l’administrateur du serveur.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="f7bb4-123">Vous pouvez réinitialiser le mot de passe si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="f7bb4-124">Cliquez sur **Afficher les chaînes de connexion de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="f7bb4-125">Passez en revue la chaîne de connexion **ADO.NET** complète.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-125">Review the complete **ADO.NET** connection string.</span></span>

    ![Chaîne de connexion ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="f7bb4-127">Une règle de pare-feu doit être en place pour l’adresse IP publique de l’ordinateur sur lequel vous effectuez ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="f7bb4-128">Si vous êtes sur un autre ordinateur ou si vous avez une autre adresse IP publique, créez une [règle de pare-feu au niveau du serveur à l’aide du portail Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="f7bb4-129">Création d'un nouveau projet .NET</span><span class="sxs-lookup"><span data-stu-id="f7bb4-129">Create a new .NET project</span></span>

1. <span data-ttu-id="f7bb4-130">Ouvrez une invite de commandes et créez un dossier nommé *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="f7bb4-131">Accédez au dossier que vous avez créé et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f7bb4-131">Navigate to the folder you created and run the following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="f7bb4-132">Ouvrez ***sqltest.csproj*** avec votre éditeur de texte favori et ajoutez System.Data.SqlClient en tant que dépendance en utilisant le code suivant :</span><span class="sxs-lookup"><span data-stu-id="f7bb4-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using the following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="f7bb4-133">Insertion du code pour interroger la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="f7bb4-133">Insert code to query SQL database</span></span>

1. <span data-ttu-id="f7bb4-134">Dans votre environnement de développement ou votre éditeur de texte favori, ouvrez **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="f7bb4-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="f7bb4-135">Remplacez le contenu par le code suivant et ajoutez les valeurs appropriées pour votre serveur, base de données, utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-135">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="f7bb4-136">Exécution du code</span><span class="sxs-lookup"><span data-stu-id="f7bb4-136">Run the code</span></span>

1. <span data-ttu-id="f7bb4-137">Exécutez ensuite les commandes suivantes dans l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="f7bb4-137">At the command prompt, run the following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="f7bb4-138">Vérifiez que les 20 premières lignes sont renvoyées, puis fermez la fenêtre d’application.</span><span class="sxs-lookup"><span data-stu-id="f7bb4-138">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7bb4-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7bb4-139">Next steps</span></span>

- <span data-ttu-id="f7bb4-140">[Prise en main de .NET Core sur Windows/Linux/macOS à l’aide de la ligne de commande](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-140">[Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="f7bb4-141">Découvrez comment [connecter et interroger une base de données SQL Azure à l’aide de .NET Framework et Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-141">Learn how to [connect and query an Azure SQL database using the .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="f7bb4-142">Découvrez comment [concevoir votre première base de données SQL Azure à l’aide de SSMS](sql-database-design-first-database.md) ou [concevoir votre première base de données SQL Azure à l’aide de .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-142">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="f7bb4-143">Pour plus d’informations sur .NET, consultez la [documentation .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="f7bb4-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
