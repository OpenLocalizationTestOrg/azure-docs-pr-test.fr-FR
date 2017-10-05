---
title: "Se connecter à la base de données Azure pour MySQL avec PHP | Microsoft Docs"
description: "Ce guide de démarrage rapide fournit plusieurs exemples de code PHP, que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 59da1ab9e76685d7ed0c4415ef99578c982e956c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="3ef3c-103">Base de données Azure pour MySQL : Utilisation de PHP pour se connecter et interroger des données</span><span class="sxs-lookup"><span data-stu-id="3ef3c-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="3ef3c-104">Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour MySQL en utilisant une application [PHP](http://php.net/manual/intro-whatis.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="3ef3c-105">Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="3ef3c-106">Cet article suppose que vous connaissez les bases du développement à l’aide de PHP, mais que vous ne connaissez pas la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ef3c-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3ef3c-107">Prerequisites</span></span>
<span data-ttu-id="3ef3c-108">Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :</span><span class="sxs-lookup"><span data-stu-id="3ef3c-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="3ef3c-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3ef3c-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="3ef3c-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3ef3c-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="3ef3c-111">Installer PHP</span><span class="sxs-lookup"><span data-stu-id="3ef3c-111">Install PHP</span></span>
<span data-ttu-id="3ef3c-112">Installez PHP sur votre serveur, ou créez une [application web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure incluant PHP.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="3ef3c-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="3ef3c-113">MacOS</span></span>
- <span data-ttu-id="3ef3c-114">Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="3ef3c-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="3ef3c-115">Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="3ef3c-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="3ef3c-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="3ef3c-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="3ef3c-117">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="3ef3c-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="3ef3c-118">Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="3ef3c-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="3ef3c-119">Windows</span><span class="sxs-lookup"><span data-stu-id="3ef3c-119">Windows</span></span>
- <span data-ttu-id="3ef3c-120">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="3ef3c-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="3ef3c-121">Installez PHP et consultez le [manuel sur PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="3ef3c-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="3ef3c-122">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="3ef3c-122">Get connection information</span></span>
<span data-ttu-id="3ef3c-123">Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="3ef3c-124">Vous devez disposer du nom de serveur complet et des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="3ef3c-125">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3ef3c-126">Dans le volet gauche, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous avez créé (par exemple, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-126">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="3ef3c-127">Cliquez sur le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-127">Click the server name.</span></span>
4. <span data-ttu-id="3ef3c-128">Sélectionnez la page **Propriétés** du serveur.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-128">Select the server's **Properties** page.</span></span> <span data-ttu-id="3ef3c-129">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-129">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="3ef3c-130">![Nom du serveur de base de données Azure pour MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="3ef3c-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="3ef3c-131">Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-131">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="3ef3c-132">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="3ef3c-132">Connect and create a table</span></span>
<span data-ttu-id="3ef3c-133">Utilisez le code suivant pour vous connecter et créer une table à l’aide de l’instruction SQL **CREATE TABLE**.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-133">Use the following code to connect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="3ef3c-134">Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-134">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ef3c-135">Il appelle les méthodes [mysqli_init](http://php.net/manual/mysqli.init.php) et [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) pour se connecter à MySQL.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-135">The code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="3ef3c-136">Ensuite, il appelle la méthode [mysqli_query](http://php.net/manual/mysqli.query.php) pour exécuter la requête.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="3ef3c-137">Enfin, il appelle la méthode [mysqli_close](http://php.net/manual/mysqli.close.php) pour fermer la connexion.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="3ef3c-138">Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-138">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
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

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="3ef3c-139">Insertion des données</span><span class="sxs-lookup"><span data-stu-id="3ef3c-139">Insert data</span></span>
<span data-ttu-id="3ef3c-140">Utilisez le code suivant pour vous connecter et insérer des données à l’aide d’une instruction SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-140">Use the following code to connect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="3ef3c-141">Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-141">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ef3c-142">Le code utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) pour créer une instruction Insert préparée, puis lie les paramètres de chaque valeur de colonne insérée à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-142">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="3ef3c-143">Il exécute l’instruction à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php), puis ferme l’instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-143">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="3ef3c-144">Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-144">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
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

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="3ef3c-145">Lire les données</span><span class="sxs-lookup"><span data-stu-id="3ef3c-145">Read data</span></span>
<span data-ttu-id="3ef3c-146">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-146">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="3ef3c-147">Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-147">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ef3c-148">Le code utilise la méthode [mysqli_query](http://php.net/manual/mysqli.query.php) pour exécuter la requête sql, puis la méthode [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) pour extraire les lignes ainsi créées.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-148">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method to fetch the resulting rows.</span></span>

<span data-ttu-id="3ef3c-149">Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-149">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="3ef3c-150">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="3ef3c-150">Update data</span></span>
<span data-ttu-id="3ef3c-151">Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-151">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="3ef3c-152">Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-152">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ef3c-153">Le code utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) pour créer une instruction Update préparée, puis lie les paramètres de chaque valeur de colonne mise à jour à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-153">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="3ef3c-154">Il exécute l’instruction à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php), puis ferme l’instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-154">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="3ef3c-155">Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-155">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="3ef3c-156">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="3ef3c-156">Delete data</span></span>
<span data-ttu-id="3ef3c-157">Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-157">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="3ef3c-158">Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-158">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="3ef3c-159">Le code utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) pour créer une instruction Delete préparée, puis lie les paramètres de la clause Where à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-159">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="3ef3c-160">Il exécute l’instruction à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php), puis ferme l’instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="3ef3c-160">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="3ef3c-161">Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="3ef3c-161">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="3ef3c-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ef3c-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="3ef3c-163">Créer une application web PHP et MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="3ef3c-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
