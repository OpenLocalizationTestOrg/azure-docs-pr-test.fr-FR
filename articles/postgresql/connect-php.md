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
ms.date: 11/03/2017
ms.openlocfilehash: dec02baf0ae9df4860a3f67e67b0f62e356658ff
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2017
---
# <a name="azure-database-for-postgresql-use-php-to-connect-and-query-data"></a>Base de données Azure pour PostgreSQL : Utilisation de PHP pour se connecter et interroger des données
Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour PostgreSQL en utilisant une application [PHP](http://php.net/manual/intro-whatis.php). Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer. Cet article suppose que vous connaissez les bases du développement via PHP, et que vous ne savez pas utiliser Azure Database pour PostgreSQL.

## <a name="prerequisites"></a>Composants requis
Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :
- [Créer une base de données - Portail](quickstart-create-server-database-portal.md)
- [Créer une base de données - Interface de ligne de commande Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Installer PHP
Installez PHP sur votre serveur, ou créez une [application web](../app-service/app-service-web-overview.md) Azure incluant PHP.

### <a name="windows"></a>Windows
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)
- Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration
- Le code utilise la classe **pgsql** (ext/php_pgsql.dll) qui est incluse dans l’installation de PHP. 
- Activez l’extension **pgsql** en modifiant le fichier de configuration php.ini, qui se trouve généralement ici : `C:\Program Files\PHP\v7.1\php.ini`. Le fichier de configuration doit contenir une ligne présentant le texte `extension=php_pgsql.so`. Si elle n’apparaît pas, ajoutez le texte et enregistrez le fichier. Si le texte est présent, mais mis en commentaire avec un préfixe point-virgule, supprimez les marques de commentaire en retirant le point-virgule.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php) 
- Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration
- Le code utilise la classe **pgsql** (php_pgsql.so). Installez-la en exécutant la commande `sudo apt-get install php-pgsql`.
- Activez l’extension **pgsql** en modifiant le fichier de configuration `/etc/php/7.0/mods-available/pgsql.ini`. Le fichier de configuration doit contenir une ligne présentant le texte `extension=php_pgsql.so`. Si elle n’apparaît pas, ajoutez le texte et enregistrez le fichier. Si le texte est présent, mais mis en commentaire avec un préfixe point-virgule, supprimez les marques de commentaire en retirant le point-virgule.

### <a name="macos"></a>MacOS
- Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)
- Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenez les informations de connexion requises pour vous connecter à la base de données Azure pour PostgreSQL. Vous devez disposer du nom de serveur complet et des informations d’identification.

1. Connectez-vous au [portail Azure](https://portal.azure.com/).
2. Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **mypgserver-20170401**.
3. Cliquez sur le nom du serveur **mypgserver-20170401**.
4. Sélectionnez la page **Présentation** du serveur. Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.
 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-php/1-connection-string.png)
5. Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.

## <a name="connect-and-create-a-table"></a>Se connecter et créer une table
Utilisez le code suivant pour vous connecter et créer une table à l’aide de l’instruction **CREATE TABLE**, suivie des instructions SQL **INSERT INTO** pour ajouter des lignes à la table.

Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) plusieurs fois pour exécuter plusieurs commandes, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite à chaque fois. Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.

Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs. 

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

## <a name="read-data"></a>Lire les données
Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**. 

 Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) pour exécuter la commande SELECT, en conservant les résultats dans un jeu de résultats, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite.  Pour lire le jeu de résultats, le système appelle la méthode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) en boucle, une fois par ligne, et récupère les données des lignes dans un tableau `$row`, en affichant une valeur de données par colonne dans chaque position dans le tableau.  Pour libérer le jeu de résultats, le système appelle la méthode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php). Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.

Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs. 

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

## <a name="update-data"></a>Mettre à jour des données
Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.

Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) pour exécuter une commande, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite. Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.

Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs. 

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


## <a name="delete-data"></a>Suppression de données
Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **DELETE**. 

 Le code appelle la méthode [pg_connect()](http://php.net/manual/en/function.pg-connect.php) pour se connecter à la base de données Azure pour PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) pour exécuter une commande, et la méthode [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) pour vérifier les détails, si une erreur s’est produite. Enfin, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) pour fermer la connexion.

Remplacez les paramètres `$host`, `$database`, `$user` et `$password` par vos propres valeurs. 

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

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./howto-migrate-using-export-and-import.md)
