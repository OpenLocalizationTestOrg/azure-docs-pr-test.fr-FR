---
title: "aaaConnect tooAzure base de données PostgreSQL à l’aide de PHP | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code PHP, vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour PostgreSQL."
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
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="60716-103">Base de données Azure pour PostgreSQL : utilisez PHP tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="60716-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="60716-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données PostgreSQL utilisant un [PHP](http://php.net/manual/intro-whatis.php) application.</span><span class="sxs-lookup"><span data-stu-id="60716-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="60716-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="60716-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="60716-106">Cet article suppose que vous êtes familiarisé avec le développement à l’aide de PHP, mais que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="60716-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60716-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="60716-107">Prerequisites</span></span>
<span data-ttu-id="60716-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="60716-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="60716-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="60716-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="60716-110">Créer une base de données - Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="60716-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="60716-111">Installer PHP</span><span class="sxs-lookup"><span data-stu-id="60716-111">Install PHP</span></span>
<span data-ttu-id="60716-112">Installez PHP sur votre serveur, ou créez une [application web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure incluant PHP.</span><span class="sxs-lookup"><span data-stu-id="60716-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="60716-113">Windows</span><span class="sxs-lookup"><span data-stu-id="60716-113">Windows</span></span>
- <span data-ttu-id="60716-114">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="60716-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="60716-115">Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="60716-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="60716-116">code de Hello utilise hello **pgsql** classe (ext/php_pgsql.dll) qui est inclus dans hello installation PHP.</span><span class="sxs-lookup"><span data-stu-id="60716-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="60716-117">Hello activé **pgsql** extension en modifiant le fichier de configuration php.ini hello, situé généralement dans `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="60716-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="60716-118">fichier de configuration Hello doit contenir une ligne avec le texte hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="60716-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="60716-119">Si cela n’est pas indiqué, ajouter du texte de hello et enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="60716-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="60716-120">Si le texte hello est présent, mais mis en commentaire avec un préfixe point-virgule, ne pas commenter le texte hello en supprimant les points-virgules hello.</span><span class="sxs-lookup"><span data-stu-id="60716-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="60716-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="60716-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="60716-122">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="60716-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="60716-123">Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="60716-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="60716-124">code de Hello utilise hello **pgsql** classe (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="60716-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="60716-125">Installez-la en exécutant la commande `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="60716-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="60716-126">Hello activé **pgsql** extension en modifiant hello `/etc/php/7.0/mods-available/pgsql.ini` fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="60716-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="60716-127">fichier de configuration Hello doit contenir une ligne avec le texte hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="60716-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="60716-128">Si cela n’est pas indiqué, ajouter du texte de hello et enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="60716-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="60716-129">Si le texte hello est présent, mais mis en commentaire avec un préfixe point-virgule, ne pas commenter le texte hello en supprimant les points-virgules hello.</span><span class="sxs-lookup"><span data-stu-id="60716-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="60716-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="60716-130">MacOS</span></span>
- <span data-ttu-id="60716-131">Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="60716-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="60716-132">Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="60716-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="60716-133">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="60716-133">Get connection information</span></span>
<span data-ttu-id="60716-134">Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="60716-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="60716-135">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="60716-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="60716-136">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="60716-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="60716-137">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="60716-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="60716-138">Cliquez sur le nom du serveur hello **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="60716-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="60716-139">Serveur hello sélectionnez **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="60716-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="60716-140">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="60716-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="60716-141">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="60716-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="60716-142">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="60716-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="60716-143">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="60716-143">Connect and create a table</span></span>
<span data-ttu-id="60716-144">Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="60716-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="60716-145">méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="60716-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="60716-146">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) plusieurs fois toorun plusieurs commandes, et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite lors de chaque fois.</span><span class="sxs-lookup"><span data-stu-id="60716-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="60716-147">Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="60716-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="60716-148">Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="60716-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

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

## <a name="read-data"></a><span data-ttu-id="60716-149">Lire les données</span><span class="sxs-lookup"><span data-stu-id="60716-149">Read data</span></span>
<span data-ttu-id="60716-150">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="60716-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="60716-151">méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="60716-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="60716-152">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) commande SELECT toorun hello, en conservant les résultats hello dans un jeu de résultats et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="60716-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="60716-153">jeu de résultats tooread hello, méthode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) est appelée dans une boucle, une fois par ligne et hello ligne les données sont récupérées dans un tableau `$row`, avec la valeur de données par colonne dans chaque position du tableau.</span><span class="sxs-lookup"><span data-stu-id="60716-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="60716-154">jeu de résultats toofree hello, méthode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) est appelée.</span><span class="sxs-lookup"><span data-stu-id="60716-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="60716-155">Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="60716-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="60716-156">Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="60716-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
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

## <a name="update-data"></a><span data-ttu-id="60716-157">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="60716-157">Update data</span></span>
<span data-ttu-id="60716-158">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="60716-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="60716-159">méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="60716-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="60716-160">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun une commande, et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="60716-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="60716-161">Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="60716-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="60716-162">Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="60716-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

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


## <a name="delete-data"></a><span data-ttu-id="60716-163">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="60716-163">Delete data</span></span>
<span data-ttu-id="60716-164">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="60716-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="60716-165">méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect trop Azure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="60716-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="60716-166">Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun une commande, et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite.</span><span class="sxs-lookup"><span data-stu-id="60716-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="60716-167">Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="60716-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="60716-168">Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="60716-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

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

## <a name="next-steps"></a><span data-ttu-id="60716-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60716-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="60716-170">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="60716-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
