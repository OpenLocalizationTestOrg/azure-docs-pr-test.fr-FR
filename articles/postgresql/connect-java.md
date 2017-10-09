---
title: "Se connecter tooAzure de base de données pour PostgreSQL à l’aide de Java | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code Java, vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour PostgreSQL."
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
ms.openlocfilehash: 8f6e0a47a0d6dfebf29eb56c31ccccabd7c2b670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="0896b-103">Base de données Azure pour PostgreSQL : utiliser Java tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="0896b-103">Azure Database for PostgreSQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="0896b-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données PostgreSQL à l’aide d’une application Java.</span><span class="sxs-lookup"><span data-stu-id="0896b-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="0896b-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0896b-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="0896b-106">Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de Java et que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0896b-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0896b-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0896b-107">Prerequisites</span></span>
<span data-ttu-id="0896b-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="0896b-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0896b-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="0896b-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="0896b-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="0896b-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="0896b-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="0896b-111">You also need to:</span></span>
- <span data-ttu-id="0896b-112">Télécharger hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) correspondant à votre version de Java et hello Kit de développement Java.</span><span class="sxs-lookup"><span data-stu-id="0896b-112">Download hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and hello Java Development Kit.</span></span>
- <span data-ttu-id="0896b-113">Inclure hello le fichier jar PostgreSQL JDBC (par exemple postgresql 42.1.1.jar) dans votre chemin de classe d’application.</span><span class="sxs-lookup"><span data-stu-id="0896b-113">Include hello PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="0896b-114">Pour plus d'informations, consultez la rubrique [Classpath](https://jdbc.postgresql.org/documentation/head/classpath.html) (Chemin de classe).</span><span class="sxs-lookup"><span data-stu-id="0896b-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0896b-115">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="0896b-115">Get connection information</span></span>
<span data-ttu-id="0896b-116">Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="0896b-116">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="0896b-117">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="0896b-117">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0896b-118">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0896b-118">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0896b-119">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="0896b-119">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="0896b-120">Cliquez sur le nom du serveur hello **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="0896b-120">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="0896b-121">Serveur hello sélectionnez **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="0896b-121">Select hello server's **Overview** page.</span></span> <span data-ttu-id="0896b-122">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="0896b-122">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0896b-123">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="0896b-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="0896b-124">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="0896b-124">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0896b-125">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="0896b-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="0896b-126">Hello utilisation code tooconnect et charge hello données suivantes à l’aide de la fonction hello avec un **insérer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="0896b-126">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="0896b-127">méthodes de Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) sont utilisé tooconnect, supprimez et recréez la table de hello.</span><span class="sxs-lookup"><span data-stu-id="0896b-127">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, drop, and create hello table.</span></span> <span data-ttu-id="0896b-128">Hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) objet est commandes insert hello toobuild utilisé, avec des valeurs de paramètre de hello toobind setString() et setInt().</span><span class="sxs-lookup"><span data-stu-id="0896b-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="0896b-129">Méthode [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) séries hello commande pour chaque jeu de paramètres.</span><span class="sxs-lookup"><span data-stu-id="0896b-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs hello command for each set of parameters.</span></span> 

<span data-ttu-id="0896b-130">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0896b-130">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

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

## <a name="read-data"></a><span data-ttu-id="0896b-131">Lire les données</span><span class="sxs-lookup"><span data-stu-id="0896b-131">Read data</span></span>
<span data-ttu-id="0896b-132">Suivant de hello d’utilisation de code tooread les données de salutation avec un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="0896b-132">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="0896b-133">méthodes de Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) sont utilisé tooconnect, créer et exécuter l’instruction select de hello.</span><span class="sxs-lookup"><span data-stu-id="0896b-133">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, create, and run hello select statement.</span></span> <span data-ttu-id="0896b-134">les résultats de Hello sont traités à l’aide un [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) objet.</span><span class="sxs-lookup"><span data-stu-id="0896b-134">hello results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="0896b-135">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0896b-135">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

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
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="0896b-136">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="0896b-136">Update data</span></span>
<span data-ttu-id="0896b-137">Suivant de hello d’utilisation de code toochange les données de salutation avec une **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="0896b-137">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="0896b-138">Hello méthodes [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) sont utilisé tooconnect, préparer et exécuter l’instruction de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="0896b-138">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello update statement.</span></span> 

<span data-ttu-id="0896b-139">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0896b-139">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

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
## <a name="delete-data"></a><span data-ttu-id="0896b-140">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="0896b-140">Delete data</span></span>
<span data-ttu-id="0896b-141">Données tooremove avec du code suivant de hello utilisation un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="0896b-141">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="0896b-142">méthodes de Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), et [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) sont utilisé tooconnect, préparer et exécuter l’instruction delete de hello.</span><span class="sxs-lookup"><span data-stu-id="0896b-142">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello delete statement.</span></span> 

<span data-ttu-id="0896b-143">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé votre propre serveur et la base de données hôte de hello, base de données, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0896b-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

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

## <a name="next-steps"></a><span data-ttu-id="0896b-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0896b-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0896b-145">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="0896b-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
