---
title: "Se connecter à la base de données Azure pour PostgreSQL à l’aide de Java | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit plusieurs exemples de code Java, que vous pouvez utiliser pour vous connecter et interroger des données à partir de la base de données Azure pour PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="4f3f8-103">Base de données Azure pour PostgreSQL : Utilisation de Java pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="4f3f8-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="4f3f8-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour PostgreSQL en utilisant une application Java.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="4f3f8-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="4f3f8-106">Les étapes de cet article supposent que vous connaissez le développement avec Java et que vous ne savez pas utiliser la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f3f8-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4f3f8-107">Prerequisites</span></span>
<span data-ttu-id="4f3f8-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="4f3f8-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4f3f8-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="4f3f8-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="4f3f8-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4f3f8-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="4f3f8-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="4f3f8-111">You also need to:</span></span>
- <span data-ttu-id="4f3f8-112">Télécharger le [pilote de PostgreSQL JDBC](https://jdbc.postgresql.org/download.html) correspondant à votre version de Java et le kit de développement Java.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="4f3f8-113">Inclure le fichier .jar de PostgreSQL JDBC (postgresql-42.1.1.jar, par exemple) dans le chemin de classe de votre application.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="4f3f8-114">Pour plus d'informations, consultez la rubrique [Classpath](https://jdbc.postgresql.org/documentation/head/classpath.html) (Chemin de classe).</span><span class="sxs-lookup"><span data-stu-id="4f3f8-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4f3f8-115">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="4f3f8-115">Get connection information</span></span>
<span data-ttu-id="4f3f8-116">Obtenez les informations de connexion requises pour vous connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="4f3f8-117">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4f3f8-118">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f3f8-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f3f8-119">Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="4f3f8-120">Cliquez sur le nom du serveur **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="4f3f8-121">Sélectionnez la page **Présentation** du serveur.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="4f3f8-122">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4f3f8-123">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="4f3f8-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="4f3f8-124">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="4f3f8-125">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="4f3f8-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="4f3f8-126">Utilisez le code suivant pour vous connecter et charger les données à l’aide d’une instruction SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="4f3f8-127">Les méthodes [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) permettent de se connecter, de déposer et de créer une table.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="4f3f8-128">L’objet [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) permet de générer les commandes d’insertion, en utilisant les méthodes setString() et setInt() pour lier les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="4f3f8-129">La méthode [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) exécute la commande pour chaque ensemble de paramètres.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="4f3f8-130">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="4f3f8-131">Lire les données</span><span class="sxs-lookup"><span data-stu-id="4f3f8-131">Read data</span></span>
<span data-ttu-id="4f3f8-132">Utilisez le code suivant pour lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="4f3f8-133">Les méthodes [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) permettent de se connecter, de créer et d’exécuter l’instruction sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="4f3f8-134">Les résultats sont traités à l’aide de l’objet [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html).</span><span class="sxs-lookup"><span data-stu-id="4f3f8-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="4f3f8-135">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="4f3f8-136">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="4f3f8-136">Update data</span></span>
<span data-ttu-id="4f3f8-137">Utilisez le code suivant pour modifier les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="4f3f8-138">Les méthodes [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) permettent de se connecter, de préparer et d’exécuter l’instruction de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="4f3f8-139">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="4f3f8-140">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="4f3f8-140">Delete data</span></span>
<span data-ttu-id="4f3f8-141">Utilisez le code suivant pour supprimer des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="4f3f8-142">Les méthodes [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) permettent de se connecter, de préparer et d’exécuter l’instruction de suppression.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="4f3f8-143">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4f3f8-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="4f3f8-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f3f8-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4f3f8-145">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="4f3f8-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
