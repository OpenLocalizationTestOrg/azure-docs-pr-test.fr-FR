---
title: "Se connecter à la base de données Azure pour MySQL à l’aide de Java | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit plusieurs exemples de code Java, que vous pouvez utiliser pour vous connecter et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: 6ffcf3b38a3d868dfa10ea2e2a9d097441387d4f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-java-to-connect-and-query-data"></a><span data-ttu-id="9ee21-103">Base de données Azure pour MySQL : Utilisation de Java pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="9ee21-103">Azure Database for MySQL: Use Java to connect and query data</span></span>
<span data-ttu-id="9ee21-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour MySQL en utilisant une application Java.</span><span class="sxs-lookup"><span data-stu-id="9ee21-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="9ee21-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="9ee21-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="9ee21-106">Les étapes de cet article supposent que vous connaissez le développement avec Java, mais que vous ne savez pas utiliser la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="9ee21-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ee21-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9ee21-107">Prerequisites</span></span>
<span data-ttu-id="9ee21-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="9ee21-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9ee21-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="9ee21-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="9ee21-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ee21-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="9ee21-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="9ee21-111">You also need to:</span></span>
- <span data-ttu-id="9ee21-112">Télécharger le pilote JDBC [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="9ee21-112">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="9ee21-113">Inclure le fichier jar JDBC (par exemple, mysql-connector-java-5.1.42-bin.jar) dans le chemin de classe de votre application.</span><span class="sxs-lookup"><span data-stu-id="9ee21-113">Include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="9ee21-114">Si vous rencontrez un problème, consultez la documentation de votre environnement pour obtenir des détails sur le chemin d’accès de classe, comme [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) ou [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="9ee21-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="9ee21-115">Vous assurer que votre base de données Azure pour la sécurité de connexion MySQL est configurée avec le pare-feu ouvert et les paramètres SSL adaptés à votre application pour une connexion réussie.</span><span class="sxs-lookup"><span data-stu-id="9ee21-115">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="9ee21-116">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="9ee21-116">Get connection information</span></span>
<span data-ttu-id="9ee21-117">Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="9ee21-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="9ee21-118">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9ee21-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9ee21-119">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9ee21-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9ee21-120">Dans le volet gauche, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous avez créé (par exemple, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="9ee21-120">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="9ee21-121">Cliquez sur le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="9ee21-121">Click the server name.</span></span>
4. <span data-ttu-id="9ee21-122">Sélectionnez la page **Propriétés** du serveur.</span><span class="sxs-lookup"><span data-stu-id="9ee21-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="9ee21-123">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="9ee21-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9ee21-124">![Nom du serveur de base de données Azure pour MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="9ee21-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="9ee21-125">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9ee21-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="9ee21-126">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="9ee21-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="9ee21-127">Utilisez le code suivant pour vous connecter et charger les données à l’aide d’une instruction SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="9ee21-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="9ee21-128">La méthode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) permet de se connecter à MySQL.</span><span class="sxs-lookup"><span data-stu-id="9ee21-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="9ee21-129">Les méthodes [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) et execute() permettent de supprimer et de créer la table.</span><span class="sxs-lookup"><span data-stu-id="9ee21-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span></span> <span data-ttu-id="9ee21-130">L’objet prepareStatement permet de générer les commandes d’insertion, en se servant des méthodes setString() et setInt() pour lier les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="9ee21-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="9ee21-131">La méthode executeUpdate() exécute la commande pour chaque ensemble de paramètres afin d’insérer les valeurs.</span><span class="sxs-lookup"><span data-stu-id="9ee21-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span></span> 

<span data-ttu-id="9ee21-132">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="9ee21-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="9ee21-133">Lire les données</span><span class="sxs-lookup"><span data-stu-id="9ee21-133">Read data</span></span>
<span data-ttu-id="9ee21-134">Utilisez le code suivant pour lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="9ee21-134">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="9ee21-135">La méthode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) permet de se connecter à MySQL.</span><span class="sxs-lookup"><span data-stu-id="9ee21-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="9ee21-136">Les méthodes [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) et executeQuery() permettent de se connecter et d’exécuter l’instruction sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="9ee21-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span></span> <span data-ttu-id="9ee21-137">Les résultats sont traités à l’aide de l’objet [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html).</span><span class="sxs-lookup"><span data-stu-id="9ee21-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="9ee21-138">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="9ee21-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="9ee21-139">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="9ee21-139">Update data</span></span>
<span data-ttu-id="9ee21-140">Utilisez le code suivant pour modifier les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="9ee21-140">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="9ee21-141">La méthode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) permet de se connecter à MySQL.</span><span class="sxs-lookup"><span data-stu-id="9ee21-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="9ee21-142">Les méthodes [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) et executeUpdate() permettent de préparer et d’exécuter l’instruction de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="9ee21-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="9ee21-143">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="9ee21-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="9ee21-144">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="9ee21-144">Delete data</span></span>
<span data-ttu-id="9ee21-145">Utilisez le code suivant pour supprimer des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="9ee21-145">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="9ee21-146">La méthode [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) permet de se connecter à MySQL.</span><span class="sxs-lookup"><span data-stu-id="9ee21-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span>  <span data-ttu-id="9ee21-147">Les méthodes [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) et executeUpdate() permettent de préparer et d’exécuter l’instruction de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="9ee21-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="9ee21-148">Remplacez les paramètres d’hôte, de la base de données, d’utilisateur et du mot de passe par les valeurs spécifiées lors de la création de votre serveur et de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="9ee21-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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

## <a name="next-steps"></a><span data-ttu-id="9ee21-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ee21-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9ee21-150">Migrer une base de données MySQL vers une base de données Azure pour MySQL à l’aide des images mémoire et de la restauration</span><span class="sxs-lookup"><span data-stu-id="9ee21-150">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
