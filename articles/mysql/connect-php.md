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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="f74a8-103">Base de données Azure pour MySQL : utilisez PHP tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="f74a8-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="f74a8-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données MySQL à l’aide un [PHP](http://php.net/manual/intro-whatis.php) application.</span><span class="sxs-lookup"><span data-stu-id="f74a8-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="f74a8-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="f74a8-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="f74a8-106">Cet article suppose que vous êtes familiarisé avec le développement à l’aide de PHP, mais que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f74a8-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f74a8-107">Prerequisites</span></span>
<span data-ttu-id="f74a8-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="f74a8-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="f74a8-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f74a8-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="f74a8-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f74a8-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="f74a8-111">Installer PHP</span><span class="sxs-lookup"><span data-stu-id="f74a8-111">Install PHP</span></span>
<span data-ttu-id="f74a8-112">Installez PHP sur votre serveur, ou créez une [application web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) Azure incluant PHP.</span><span class="sxs-lookup"><span data-stu-id="f74a8-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="f74a8-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="f74a8-113">MacOS</span></span>
- <span data-ttu-id="f74a8-114">Téléchargez [PHP version 7.1.4](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="f74a8-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="f74a8-115">Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.macosx.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="f74a8-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="f74a8-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f74a8-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="f74a8-117">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="f74a8-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="f74a8-118">Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.unix.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="f74a8-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="f74a8-119">Windows</span><span class="sxs-lookup"><span data-stu-id="f74a8-119">Windows</span></span>
- <span data-ttu-id="f74a8-120">Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="f74a8-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="f74a8-121">Installer PHP et de faire référence toohello [manuel PHP](http://php.net/manual/install.windows.php) pour poursuivre la configuration</span><span class="sxs-lookup"><span data-stu-id="f74a8-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="f74a8-122">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="f74a8-122">Get connection information</span></span>
<span data-ttu-id="f74a8-123">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="f74a8-124">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="f74a8-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="f74a8-125">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f74a8-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f74a8-126">Dans le volet gauche de hello, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé (par exemple, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="f74a8-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="f74a8-127">Cliquez sur le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="f74a8-127">Click hello server name.</span></span>
4. <span data-ttu-id="f74a8-128">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="f74a8-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="f74a8-129">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="f74a8-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="f74a8-130">![Nom du serveur de base de données Azure pour MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="f74a8-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="f74a8-131">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="f74a8-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="f74a8-132">Se connecter et créer une table</span><span class="sxs-lookup"><span data-stu-id="f74a8-132">Connect and create a table</span></span>
<span data-ttu-id="f74a8-133">Suivante de hello utilisation tooconnect de code et créer une table à l’aide de **CREATE TABLE** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="f74a8-134">code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP.</span><span class="sxs-lookup"><span data-stu-id="f74a8-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="f74a8-135">méthodes d’appel de code de Hello [mysqli_init](http://php.net/manual/mysqli.init.php) et [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="f74a8-136">Ensuite, il appelle la méthode [mysqli_query](http://php.net/manual/mysqli.query.php) requête de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="f74a8-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="f74a8-137">Ensuite, il appelle la méthode [mysqli_close](http://php.net/manual/mysqli.close.php) connexion de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="f74a8-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="f74a8-138">Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f74a8-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="f74a8-139">Insertion des données</span><span class="sxs-lookup"><span data-stu-id="f74a8-139">Insert data</span></span>
<span data-ttu-id="f74a8-140">Suivante de hello utilisation tooconnect de code et insérer des données à l’aide un **insérer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="f74a8-141">code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP.</span><span class="sxs-lookup"><span data-stu-id="f74a8-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="f74a8-142">code de Hello utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate préparation d’une instruction d’insertion, puis lie hello paramètres pour chaque valeur de la colonne insérée à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="f74a8-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="f74a8-143">code de Hello s’exécute l’instruction hello à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) et par la suite ferme hello instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="f74a8-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="f74a8-144">Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f74a8-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="f74a8-145">Lire les données</span><span class="sxs-lookup"><span data-stu-id="f74a8-145">Read data</span></span>
<span data-ttu-id="f74a8-146">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="f74a8-147">code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP.</span><span class="sxs-lookup"><span data-stu-id="f74a8-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="f74a8-148">code de Hello utilise la méthode [mysqli_query](http://php.net/manual/mysqli.query.php) effectuer la requête sql hello et utilise [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch de la méthode hello lignes résultant.</span><span class="sxs-lookup"><span data-stu-id="f74a8-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="f74a8-149">Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f74a8-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="f74a8-150">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="f74a8-150">Update data</span></span>
<span data-ttu-id="f74a8-151">Suivant de hello utilisation tooconnect de code et mettre à jour les données de hello à l’aide un **mettre à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="f74a8-152">code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP.</span><span class="sxs-lookup"><span data-stu-id="f74a8-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="f74a8-153">code de Hello utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate une instruction update préparée, puis lie les paramètres pour chaque valeur de colonne mise à jour à l’aide de la méthode hello [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="f74a8-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="f74a8-154">code de Hello s’exécute l’instruction hello à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) et par la suite ferme hello instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="f74a8-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="f74a8-155">Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f74a8-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="f74a8-156">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="f74a8-156">Delete data</span></span>
<span data-ttu-id="f74a8-157">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="f74a8-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="f74a8-158">code de Hello utilise hello **MySQL amélioré l’extension** classe (mysqli) inclus dans PHP.</span><span class="sxs-lookup"><span data-stu-id="f74a8-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="f74a8-159">code de Hello utilise la méthode [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate préparation d’une instruction de suppression, puis lie hello paramètres pour hello où clause d’instruction hello à l’aide de la méthode [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="f74a8-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="f74a8-160">code de Hello s’exécute l’instruction hello à l’aide de la méthode [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) et par la suite ferme hello instruction à l’aide de la méthode [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="f74a8-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="f74a8-161">Remplacez les paramètres d’hôte, nom d’utilisateur, mot de passe et db_name hello par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f74a8-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="f74a8-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f74a8-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f74a8-163">Créer une application web PHP et MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="f74a8-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
