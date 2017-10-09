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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Base de données Azure pour PostgreSQL : utilisez PHP tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données PostgreSQL utilisant un [PHP](http://php.net/manual/intro-whatis.php) application. Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Cet article suppose que vous êtes familiarisé avec le développement à l’aide de PHP, mais que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Créer une base de données - Portail](quickstart-create-server-database-portal.md)
- [Créer une base de données - Interface de ligne de commande Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Installer PHP
Installez PHP sur votre serveur, ou créez une [application web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure incluant PHP.

### <a name="windows"></a>Windows
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)
- Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration
- code de Hello utilise hello **pgsql** classe (ext/php_pgsql.dll) qui est inclus dans hello installation PHP. 
- Hello activé **pgsql** extension en modifiant le fichier de configuration php.ini hello, situé généralement dans `C:\Program Files\PHP\v7.1\php.ini`. fichier de configuration Hello doit contenir une ligne avec le texte hello `extension=php_pgsql.so`. Si cela n’est pas indiqué, ajouter du texte de hello et enregistrez le fichier de hello. Si le texte hello est présent, mais mis en commentaire avec un préfixe point-virgule, ne pas commenter le texte hello en supprimant les points-virgules hello.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php) 
- Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration
- code de Hello utilise hello **pgsql** classe (php_pgsql.so). Installez-la en exécutant la commande `sudo apt-get install php-pgsql`.
- Hello activé **pgsql** extension en modifiant hello `/etc/php/7.0/mods-available/pgsql.ini` fichier de configuration. fichier de configuration Hello doit contenir une ligne avec le texte hello `extension=php_pgsql.so`. Si cela n’est pas indiqué, ajouter du texte de hello et enregistrez le fichier de hello. Si le texte hello est présent, mais mis en commentaire avec un préfixe point-virgule, ne pas commenter le texte hello en supprimant les points-virgules hello.

### <a name="macos"></a>MacOS
- Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)
- Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **mypgserver-20170401**.
3. Cliquez sur le nom du serveur hello **mypgserver-20170401**.
4. Serveur hello sélectionnez **vue d’ensemble** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-php/1-connection-string.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="connect-and-create-a-table"></a>Se connecter et créer une table
Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL, suivie de **INSERT INTO** lignes de tooadd d’instructions SQL dans la table de hello.

méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) plusieurs fois toorun plusieurs commandes, et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite lors de chaque fois. Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.

Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs. 

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

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. 

 méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) commande SELECT toorun hello, en conservant les résultats hello dans un jeu de résultats et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite.  jeu de résultats tooread hello, méthode [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) est appelée dans une boucle, une fois par ligne et hello ligne les données sont récupérées dans un tableau `$row`, avec la valeur de données par colonne dans chaque position du tableau.  jeu de résultats toofree hello, méthode [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) est appelée. Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.

Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs. 

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

## <a name="update-data"></a>Mettre à jour des données
Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.

méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure base de données PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun une commande, et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite. Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.

Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs. 

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


## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. 

 méthode d’appel de code de Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect trop Azure base de données PostgreSQL. Ensuite, il appelle la méthode [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun une commande, et [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello détails si une erreur s’est produite. Ensuite, il appelle la méthode [pg_close()](http://php.net/manual/en/function.pg-close.php) connexion de hello tooclose.

Remplacez hello `$host`, `$database`, `$user`, et `$password` paramètres avec vos propres valeurs. 

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

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./howto-migrate-using-export-and-import.md)
