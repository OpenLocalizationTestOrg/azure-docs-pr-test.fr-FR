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
# <a name="use-net-core-c-tooquery-an-azure-sql-database"></a><span data-ttu-id="6341e-103">Utiliser le .NET Core (c#) tooquery une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6341e-103">Use .NET Core (C#) tooquery an Azure SQL database</span></span>

<span data-ttu-id="6341e-104">Ce didacticiel de démarrage rapide montre comment toouse [.NET Core](https://www.microsoft.com/net/) sur Linux/Windows/macOS toocreate c# programme tooconnect tooan SQL Azure de base de données et utiliser des données de tooquery d’instructions Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="6341e-104">This quick start tutorial demonstrates how toouse [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS toocreate a C# program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6341e-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6341e-105">Prerequisites</span></span>

<span data-ttu-id="6341e-106">toocomplete rapide de ce didacticiel de démarrage, assurez-vous que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="6341e-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="6341e-107">base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6341e-107">An Azure SQL database.</span></span> <span data-ttu-id="6341e-108">Ce démarrage rapide utilise des ressources hello créés dans une de ces Démarrages rapides :</span><span class="sxs-lookup"><span data-stu-id="6341e-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="6341e-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="6341e-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="6341e-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="6341e-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="6341e-111">Créer une base de données - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6341e-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="6341e-112">A [règle de pare-feu de niveau serveur](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) pour l’adresse IP publique de hello d’ordinateur de hello que vous utilisez pour ce didacticiel de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="6341e-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="6341e-113">Vous avez installé [.NET Core pour votre système d’exploitation](https://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="6341e-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="6341e-114">Informations de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="6341e-114">SQL server connection information</span></span>

<span data-ttu-id="6341e-115">Obtenir hello connexion informations nécessaires tooconnect toohello Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="6341e-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="6341e-116">Vous devez le nom du serveur complet hello, nom de la base de données et les informations de connexion dans les procédures suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="6341e-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="6341e-117">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6341e-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6341e-118">Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.</span><span class="sxs-lookup"><span data-stu-id="6341e-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="6341e-119">Sur hello **vue d’ensemble** page de votre base de données, révision hello serveur nom complet comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="6341e-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="6341e-120">Vous pouvez pointer sur toobring de nom de serveur hello des hello **cliquez sur toocopy** option.</span><span class="sxs-lookup"><span data-stu-id="6341e-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="6341e-122">Si vous oubliez vos informations de connexion de serveur de base de données SQL Azure, accédez à nom d’administrateur serveur page tooview hello toohello base de données SQL server.</span><span class="sxs-lookup"><span data-stu-id="6341e-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="6341e-123">Vous pouvez réinitialiser le mot de passe hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6341e-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="6341e-124">Cliquez sur **Afficher les chaînes de connexion de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="6341e-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="6341e-125">Hello révision complète **ADO.NET** chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="6341e-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Chaîne de connexion ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="6341e-127">Vous devez disposer d’une règle de pare-feu en place pour hello IP adresse publique de hello ordinateur sur lequel vous effectuez ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6341e-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="6341e-128">Si vous se trouvent sur un autre ordinateur ou que vous avez une autre adresse IP publique, créez un [règle de pare-feu de niveau serveur à l’aide de hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="6341e-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="6341e-129">Création d'un nouveau projet .NET</span><span class="sxs-lookup"><span data-stu-id="6341e-129">Create a new .NET project</span></span>

1. <span data-ttu-id="6341e-130">Ouvrez une invite de commandes et créez un dossier nommé *sqltest*.</span><span class="sxs-lookup"><span data-stu-id="6341e-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="6341e-131">Accédez toohello dossier vous avez créé et que vous exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6341e-131">Navigate toohello folder you created and run hello following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="6341e-132">Ouvrez ***sqltest.csproj*** avec votre éditeur de texte et ajoutez System.Data.SqlClient en tant que dépendance à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="6341e-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using hello following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="6341e-133">Insérer la base de données SQL de code tooquery</span><span class="sxs-lookup"><span data-stu-id="6341e-133">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="6341e-134">Dans votre environnement de développement ou votre éditeur de texte favori, ouvrez **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="6341e-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="6341e-135">Remplacez les contenu hello hello suivante de code et ajoutez hello les valeurs appropriées pour votre serveur, une base de données, un utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6341e-135">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="6341e-136">Exécuter le code de hello</span><span class="sxs-lookup"><span data-stu-id="6341e-136">Run hello code</span></span>

1. <span data-ttu-id="6341e-137">À l’invite de commandes hello exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="6341e-137">At hello command prompt, run hello following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="6341e-138">Vérifiez que hello supérieur des 20 lignes sont retournées, puis fermez la fenêtre de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6341e-138">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6341e-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6341e-139">Next steps</span></span>

- <span data-ttu-id="6341e-140">[Prise en main de .NET Core sur Windows/Linux/macOS à l’aide de la ligne de commande hello](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="6341e-140">[Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="6341e-141">Découvrez comment trop[connecter et interroger une base de données SQL Azure à l’aide de hello .NET framework et Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6341e-141">Learn how too[connect and query an Azure SQL database using hello .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="6341e-142">Découvrez comment trop[concevoir votre première base de données SQL Azure à l’aide de SSMS](sql-database-design-first-database.md) ou [concevoir votre première base de données SQL Azure à l’aide de .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="6341e-142">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="6341e-143">Pour plus d’informations sur .NET, consultez la [documentation .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="6341e-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
