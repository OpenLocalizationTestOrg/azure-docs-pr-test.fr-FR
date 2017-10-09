---
title: "Se connecter tooAzure de base de données de MySQL à partir de PHP | Documents Microsoft"
description: "Ce démarrage rapide fournit plusieurs exemples de code PHP vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Base de données Azure pour MySQL : utilisez PHP tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide un [PHP](http://php.net/manual/intro-whatis.php) application. Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Cet article suppose que vous êtes familiarisé avec le développement à l’aide de PHP, mais que vous êtes tooworking nouvelle base de données Azure pour MySQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>Installer PHP
Installez PHP sur votre serveur, ou créez une [application web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure incluant PHP.

### <a name="macos"></a>MacOS
- Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)
- Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php)
- Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration

### <a name="windows"></a>Windows
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)
- Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le volet gauche de hello, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé (par exemple, **myserver4demo**).
3. Cliquez sur le nom du serveur hello.
4. Serveur hello sélectionnez **propriétés** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Nom du serveur de base de données Azure pour MySQL](./media/connect-php/1_server-properties-name-login.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="connect-and-create-a-table"></a>Se connecter et créer une table
Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL. 

code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP. méthodes d’appel de code de Hello [mysqli_init](http://php.net/manual/mysqli.init.php) et [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. Ensuite, il appelle la méthode [mysqli_query](http://php.net/manual/mysqli.query.php) requête de hello toorun. Ensuite, il appelle la méthode [mysqli_close](http://php.net/manual/mysqli.close.php) connexion de hello tooclose.

Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Insertion des données
Suivante de hello utilisation tooconnect de code et insérer des données à l’aide un **insérer** instruction SQL.

code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP. code de Hello utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate préparation d’une instruction d’insertion, puis lie hello paramètres pour chaque valeur de la colonne insérée à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). code de Hello s’exécute l’instruction hello à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) et par la suite ferme hello instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.  code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP. code de Hello utilise la méthode [mysqli_query](http://php.net/manual/mysqli.query.php) effectuer la requête sql hello et utilise [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch de la méthode hello lignes résultant.

Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Mettre à jour des données
Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.

code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP. code de Hello utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate une instruction update préparée, puis lie les paramètres pour chaque valeur de colonne mise à jour à l’aide de la méthode hello [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). code de Hello s’exécute l’instruction hello à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) et par la suite ferme hello instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. 

code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP. code de Hello utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate préparation d’une instruction de suppression, puis lie hello paramètres pour hello où clause d’instruction hello à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). code de Hello s’exécute l’instruction hello à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) et par la suite ferme hello instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Créer une application web PHP et MySQL dans Azure](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
