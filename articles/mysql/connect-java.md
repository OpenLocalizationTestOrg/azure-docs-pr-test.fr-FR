---
title: "Se connecter tooAzure de base de données de MySQL à l’aide de Java | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code Java, vous pouvez utiliser tooconnect et interroger des données à partir d’une base de données Azure pour la base de données MySQL."
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
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="64032-103">Base de données Azure pour MySQL : utiliser Java tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="64032-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="64032-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide d’une application Java.</span><span class="sxs-lookup"><span data-stu-id="64032-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="64032-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="64032-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="64032-106">Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de Java et que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="64032-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64032-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64032-107">Prerequisites</span></span>
<span data-ttu-id="64032-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="64032-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="64032-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="64032-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="64032-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64032-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="64032-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="64032-111">You also need to:</span></span>
- <span data-ttu-id="64032-112">Télécharger le pilote JDBC de hello [MySQL connecteur/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="64032-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="64032-113">Inclure le fichier jar JDBC hello (par exemple mysql-connector-java-5.1.42-bin.jar) dans votre chemin de classe d’application.</span><span class="sxs-lookup"><span data-stu-id="64032-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="64032-114">Si vous rencontrez un problème, consultez la documentation de votre environnement pour obtenir des détails sur le chemin d’accès de classe, comme [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) ou [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="64032-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="64032-115">Assurez-vous que votre base de données Azure pour la sécurité de connexion MySQL est configuré avec le pare-feu hello ouvert et régler les paramètres de SSL pour votre application tooconnect avec succès.</span><span class="sxs-lookup"><span data-stu-id="64032-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="64032-116">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="64032-116">Get connection information</span></span>
<span data-ttu-id="64032-117">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="64032-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="64032-118">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="64032-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="64032-119">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="64032-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="64032-120">Dans le volet gauche de hello, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé (par exemple, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="64032-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="64032-121">Cliquez sur le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="64032-121">Click hello server name.</span></span>
4. <span data-ttu-id="64032-122">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="64032-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="64032-123">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="64032-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="64032-124">![Nom du serveur de base de données Azure pour MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="64032-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="64032-125">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="64032-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="64032-126">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="64032-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="64032-127">Hello utilisation code tooconnect et charge hello données suivantes à l’aide de la fonction hello avec un **insérer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="64032-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="64032-128">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) méthode est utilisée tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="64032-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="64032-129">Méthodes [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) et execute() sont toodrop utilisé et créer la table de hello.</span><span class="sxs-lookup"><span data-stu-id="64032-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="64032-130">objet de prepareStatement Hello est commandes insert hello toobuild utilisé, avec des valeurs de paramètre de hello toobind setString() et setInt().</span><span class="sxs-lookup"><span data-stu-id="64032-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="64032-131">Méthode executeUpdate() exécute la commande hello pour chaque ensemble de valeurs de paramètres tooinsert hello.</span><span class="sxs-lookup"><span data-stu-id="64032-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="64032-132">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="64032-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="read-data"></a><span data-ttu-id="64032-133">Lire les données</span><span class="sxs-lookup"><span data-stu-id="64032-133">Read data</span></span>
<span data-ttu-id="64032-134">Suivant de hello d’utilisation de code tooread les données de salutation avec un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="64032-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="64032-135">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) méthode est utilisée tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="64032-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="64032-136">méthodes de Hello [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) et executeQuery() sont tooconnect utilisé et exécuter l’instruction select de hello.</span><span class="sxs-lookup"><span data-stu-id="64032-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="64032-137">les résultats de Hello sont traités à l’aide un [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) objet.</span><span class="sxs-lookup"><span data-stu-id="64032-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="64032-138">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="64032-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="64032-139">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="64032-139">Update data</span></span>
<span data-ttu-id="64032-140">Suivant de hello d’utilisation de code toochange les données de salutation avec une **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="64032-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="64032-141">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) méthode est utilisée tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="64032-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="64032-142">méthodes de Hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) et executeUpdate() sont tooprepare utilisé et exécuter l’instruction de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="64032-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="64032-143">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="64032-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
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
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="64032-144">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="64032-144">Delete data</span></span>
<span data-ttu-id="64032-145">Données tooremove avec du code suivant de hello utilisation un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="64032-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="64032-146">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) méthode est utilisée tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="64032-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="64032-147">méthodes de Hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) et executeUpdate() sont tooprepare utilisé et exécuter l’instruction de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="64032-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="64032-148">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="64032-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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
        
        // check that hello driver is installed
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
            
            // set up hello connection properties
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="64032-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="64032-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="64032-150">Migrer votre tooAzure de base de données de base de données MySQL pour MySQL à l’aide de vidage et restauration</span><span class="sxs-lookup"><span data-stu-id="64032-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
