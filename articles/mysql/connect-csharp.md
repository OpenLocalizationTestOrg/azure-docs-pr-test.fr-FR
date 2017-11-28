---
title: "Se connecter tooAzure de base de données de MySQL à partir de c# | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code c# (.NET) vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="7c215-103">Base de données Azure pour MySQL : l’utilisation de .NET (c#) tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="7c215-103">Azure Database for MySQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="7c215-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide d’une application c#.</span><span class="sxs-lookup"><span data-stu-id="7c215-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="7c215-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="7c215-106">Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de c#, et que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="7c215-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c215-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7c215-107">Prerequisites</span></span>
<span data-ttu-id="7c215-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="7c215-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="7c215-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="7c215-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="7c215-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c215-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="7c215-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="7c215-111">You also need to:</span></span>
- <span data-ttu-id="7c215-112">Installer [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="7c215-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="7c215-113">Suivez les étapes de hello de hello lié article tooinstall .NET spécifiquement pour votre plateforme (Windows, Ubuntu Linux ou macOS).</span><span class="sxs-lookup"><span data-stu-id="7c215-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="7c215-114">Installer [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7c215-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="7c215-115">Installer [le pilote ODBC pour MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="7c215-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="7c215-116">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="7c215-116">Get connection information</span></span>
<span data-ttu-id="7c215-117">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="7c215-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="7c215-118">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="7c215-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="7c215-119">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7c215-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7c215-120">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="7c215-120">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="7c215-121">Cliquez sur le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-121">Click hello server name.</span></span>
4. <span data-ttu-id="7c215-122">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="7c215-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="7c215-123">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="7c215-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="7c215-124">![Nom du serveur de base de données Azure pour MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="7c215-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="7c215-125">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="7c215-126">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="7c215-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="7c215-127">Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL.</span><span class="sxs-lookup"><span data-stu-id="7c215-127">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="7c215-128">code de Hello utilise la classe ODBC avec la méthode [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c215-128">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="7c215-129">Puis hello de code utilise la méthode [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), définit la propriété CommandText hello et appelle la méthode [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) commandes de base de données toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-129">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span> 

<span data-ttu-id="7c215-130">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-130">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="7c215-131">Lire les données</span><span class="sxs-lookup"><span data-stu-id="7c215-131">Read data</span></span>

<span data-ttu-id="7c215-132">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="7c215-132">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="7c215-133">code de Hello utilise la classe ODBC avec la méthode [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c215-133">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="7c215-134">Puis hello de code utilise la méthode [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) et méthode [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) commandes de base de données toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-134">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello database commands.</span></span> <span data-ttu-id="7c215-135">Ensuite hello de code utilise [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello les enregistrements dans les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-135">Next hello code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="7c215-136">Code de hello utilise ensuite les valeurs hello tooparse GetInt32 et GetString dans l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-136">Then hello code uses GetInt32 and GetString tooparse hello values in hello record.</span></span>

<span data-ttu-id="7c215-137">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-137">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="7c215-138">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="7c215-138">Update data</span></span>
<span data-ttu-id="7c215-139">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="7c215-139">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="7c215-140">code de Hello utilise la classe ODBC avec la méthode [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c215-140">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="7c215-141">Puis hello de code utilise la méthode [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), définit la propriété CommandText hello et appelle la méthode [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) commandes de base de données toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-141">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="7c215-142">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-142">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="7c215-143">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="7c215-143">Delete data</span></span>
<span data-ttu-id="7c215-144">Suivant de hello utilisation tooconnect de code et supprimer à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="7c215-144">Use hello following code tooconnect and delete hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="7c215-145">code de Hello utilise la classe ODBC avec la méthode [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish un tooMySQL de connexion.</span><span class="sxs-lookup"><span data-stu-id="7c215-145">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="7c215-146">Puis hello de code utilise la méthode [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), définit la propriété CommandText hello et appelle la méthode [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) commandes de base de données toorun hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-146">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="7c215-147">Remplacer les paramètres d’hôte, DBName, utilisateur et mot de passe hello avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="7c215-147">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="7c215-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c215-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7c215-149">Migrer votre tooAzure de base de données de base de données MySQL pour MySQL à l’aide de vidage et restauration</span><span class="sxs-lookup"><span data-stu-id="7c215-149">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
