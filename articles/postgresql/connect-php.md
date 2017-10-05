---
title: "Se connecter à la base de données Azure pour PostgreSQL à l’aide de PHP | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit un exemple de code PHP, que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: ed7c92e0689bca4056401d562271e3b6b7144dcf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a><span data-ttu-id="8e56f-103">Base de données Azure pour PostgreSQL : Utilisation de PHP pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="8e56f-103">Azure Database for PostgreSQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="8e56f-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour PostgreSQL en utilisant une application [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="8e56f-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="8e56f-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="8e56f-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="8e56f-106">Cet article suppose que vous connaissez les bases du développement à l’aide de PHP, mais que vous ne connaissez pas la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8e56f-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e56f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e56f-107">Prerequisites</span></span>
<span data-ttu-id="8e56f-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="8e56f-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="8e56f-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="8e56f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="8e56f-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8e56f-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="8e56f-111">Installer PHP</span><span class="sxs-lookup"><span data-stu-id="8e56f-111">Install PHP</span></span>
<span data-ttu-id="8e56f-112">Installez PHP sur votre serveur, ou créez une [application web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure incluant PHP.</span><span class="sxs-lookup"><span data-stu-id="8e56f-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="8e56f-113">Windows</span><span class="sxs-lookup"><span data-stu-id="8e56f-113">Windows</span></span>
- <span data-ttu-id="8e56f-114">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="8e56f-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="8e56f-115">Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="8e56f-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="8e56f-116">Le code utilise la classe **pgsql** (ext/php_pgsql.dll) qui est incluse dans l’installation de PHP.</span><span class="sxs-lookup"><span data-stu-id="8e56f-116">The code uses the **pgsql** class (ext/php_pgsql.dll)  that is included in the PHP installation.</span></span> 
- <span data-ttu-id="8e56f-117">Activez l’extension **pgsql** en modifiant le fichier de configuration php.ini, qui se trouve généralement ici : `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="8e56f-117">Enabled the **pgsql** extension by editing the php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="8e56f-118">Le fichier de configuration doit contenir une ligne présentant le texte `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="8e56f-118">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="8e56f-119">Si elle n’apparaît pas, ajoutez le texte et enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="8e56f-119">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="8e56f-120">Si le texte est présent, mais mis en commentaire avec un préfixe point-virgule, supprimez les marques de commentaire en retirant le point-virgule.</span><span class="sxs-lookup"><span data-stu-id="8e56f-120">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="8e56f-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="8e56f-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="8e56f-122">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="8e56f-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="8e56f-123">Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="8e56f-123">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="8e56f-124">Le code utilise la classe **pgsql** (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="8e56f-124">The code uses the **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="8e56f-125">Installez-la en exécutant la commande `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="8e56f-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="8e56f-126">Activez l’extension **pgsql** en modifiant le fichier de configuration `/etc/php/7.0/mods-available/pgsql.ini`.</span><span class="sxs-lookup"><span data-stu-id="8e56f-126">Enabled the **pgsql** extension by editing the `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="8e56f-127">Le fichier de configuration doit contenir une ligne présentant le texte `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="8e56f-127">The configuration file should contain a line with the text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="8e56f-128">Si elle n’apparaît pas, ajoutez le texte et enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="8e56f-128">If it is not shown, add the text and save the file.</span></span> <span data-ttu-id="8e56f-129">Si le texte est présent, mais mis en commentaire avec un préfixe point-virgule, supprimez les marques de commentaire en retirant le point-virgule.</span><span class="sxs-lookup"><span data-stu-id="8e56f-129">If the text is present, but commented with a semicolon prefix, uncomment the text by removing the semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="8e56f-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="8e56f-130">MacOS</span></span>
- <span data-ttu-id="8e56f-131">Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="8e56f-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="8e56f-132">Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="8e56f-132">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="8e56f-133">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="8e56f-133">Get connection information</span></span>
<span data-ttu-id="8e56f-134">Obtenez les informations de connexion requises pour vous connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8e56f-134">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8e56f-135">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="8e56f-135">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="8e56f-136">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8e56f-136">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8e56f-137">Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-137">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="8e56f-138">Cliquez sur le nom du serveur **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-138">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="8e56f-139">Sélectionnez la page **Présentation** du serveur.</span><span class="sxs-lookup"><span data-stu-id="8e56f-139">Select the server's **Overview** page.</span></span> <span data-ttu-id="8e56f-140">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-140">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="8e56f-141">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="8e56f-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="8e56f-142">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8e56f-142">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="8e56f-143">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="8e56f-143">Connect and create a table</span></span>
<span data-ttu-id="8e56f-144">Utilisez le code suivant pour vous connecter et créer une table à l’aide de l’instruction **CREATE TABLE**, suivie des instructions SQL **INSERT INTO** pour ajouter des lignes à la table.</span><span class="sxs-lookup"><span data-stu-id="8e56f-144">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="8e56f-145">Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8e56f-145">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8e56f-146">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) plusieurs fois pour exécuter plusieurs commandes, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="8e56f-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times to run several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred each time.</span></span> <span data-ttu-id="8e56f-147">Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.</span><span class="sxs-lookup"><span data-stu-id="8e56f-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="8e56f-148">Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="8e56f-148">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed to create connection to database: ". pg_last_error(). "<br/>");
    print "Successfully created connection to database.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a><span data-ttu-id="8e56f-149">Lire les données</span><span class="sxs-lookup"><span data-stu-id="8e56f-149">Read data</span></span>
<span data-ttu-id="8e56f-150">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-150">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="8e56f-151">Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8e56f-151">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8e56f-152">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) pour exécuter la commande SELECT, en conservant les résultats dans un jeu de résultats, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="8e56f-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run the SELECT command, keeping the results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span>  <span data-ttu-id="8e56f-153">Pour lire le jeu de résultats, le système appelle la méthode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) en boucle, une fois par ligne, et récupère les données des lignes dans un tableau `$row`, en affichant une valeur de données par colonne dans chaque position dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="8e56f-153">To read the result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and the row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="8e56f-154">Pour libérer le jeu de résultats, le système appelle la méthode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php).</span><span class="sxs-lookup"><span data-stu-id="8e56f-154">To free the result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="8e56f-155">Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.</span><span class="sxs-lookup"><span data-stu-id="8e56f-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="8e56f-156">Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="8e56f-156">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). "<br/>");

    print "Successfully created connection to database. <br/>";

    // Perform some SQL queries over the connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a><span data-ttu-id="8e56f-157">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="8e56f-157">Update data</span></span>
<span data-ttu-id="8e56f-158">Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-158">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="8e56f-159">Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8e56f-159">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8e56f-160">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) pour exécuter une commande, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="8e56f-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="8e56f-161">Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.</span><span class="sxs-lookup"><span data-stu-id="8e56f-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="8e56f-162">Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="8e56f-162">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed to create connection to database: ". pg_last_error(). ".<br/>");

    print "Successfully created connection to database. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a><span data-ttu-id="8e56f-163">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="8e56f-163">Delete data</span></span>
<span data-ttu-id="8e56f-164">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="8e56f-164">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="8e56f-165">Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8e56f-165">The code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) to connect to  Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8e56f-166">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) pour exécuter une commande, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="8e56f-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) to run a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) to check the details if an error occurred.</span></span> <span data-ttu-id="8e56f-167">Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.</span><span class="sxs-lookup"><span data-stu-id="8e56f-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) to close the connection.</span></span>

<span data-ttu-id="8e56f-168">Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="8e56f-168">Replace the `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed to create connection to database: ". pg_last_error(). ". </br>");

    print "Successfully created connection to database. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a><span data-ttu-id="8e56f-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e56f-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8e56f-170">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="8e56f-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
