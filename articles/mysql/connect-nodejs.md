---
title: "Se connecter tooAzure de base de données de MySQL à partir de Node.js | Documents Microsoft"
description: "Ce démarrage rapide fournit plusieurs exemples de code Node.js vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/17/2017
ms.openlocfilehash: ed9a39b5ab003e8216cef1c0f6a95a75c3db8458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="9c15f-103">Base de données Azure pour MySQL : utilisez Node.js tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="9c15f-103">Azure Database for MySQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="9c15f-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données pour l’utilisation de MySQL [Node.js](https://nodejs.org/) de plateformes Windows, Ubuntu Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="9c15f-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="9c15f-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="9c15f-106">Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de Node.js, et que vous êtes tooworking nouvelle base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c15f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9c15f-107">Prerequisites</span></span>
<span data-ttu-id="9c15f-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="9c15f-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9c15f-109">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="9c15f-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="9c15f-110">Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9c15f-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="9c15f-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="9c15f-111">You also need to:</span></span>
- <span data-ttu-id="9c15f-112">Installer hello [Node.js](https://nodejs.org) runtime.</span><span class="sxs-lookup"><span data-stu-id="9c15f-112">Install hello [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="9c15f-113">Installer [mysql2](https://www.npmjs.com/package/mysql2) tooMySQL tooconnect de hello application Node.js du package.</span><span class="sxs-lookup"><span data-stu-id="9c15f-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package tooconnect tooMySQL from hello Node.js application.</span></span> 

## <a name="install-nodejs-and-hello-mysql-connector"></a><span data-ttu-id="9c15f-114">Installation de Node.js et hello connecteur MySQL</span><span class="sxs-lookup"><span data-stu-id="9c15f-114">Install Node.js and hello MySQL connector</span></span>
<span data-ttu-id="9c15f-115">Selon votre plateforme, suivez hello instructions appropriées tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="9c15f-115">Depending on your platform, follow hello appropriate instructions tooinstall Node.js.</span></span> <span data-ttu-id="9c15f-116">Utilisez npm tooinstall hello mysql2 package et ses dépendances dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="9c15f-116">Use npm tooinstall hello mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="9c15f-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="9c15f-117">**Windows**</span></span>
1. <span data-ttu-id="9c15f-118">Visitez hello [page de téléchargements de Node.js](https://nodejs.org/en/download/) et sélectionnez votre option de programme d’installation de Windows souhaitée.</span><span class="sxs-lookup"><span data-stu-id="9c15f-118">Visit hello [Node.js downloads page](https://nodejs.org/en/download/) and select your desired Windows installer option.</span></span>
2. <span data-ttu-id="9c15f-119">Créez un dossier de projet local, tel que `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="9c15f-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="9c15f-120">Lancez invite de commandes hello et cd dans le dossier du projet hello, telles que`cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="9c15f-120">Launch hello command prompt and cd into hello project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="9c15f-121">Exécuter la bibliothèque de hello NPM outil tooinstall hello mysql2 dans le dossier du projet hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-121">Run hello NPM tool tooinstall hello mysql2 library into hello project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="9c15f-122">Vérifier l’installation de hello en hello `npm list` sortie texte pour `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="9c15f-122">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="9c15f-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="9c15f-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="9c15f-124">Suivante d’exécution hello commandes tooinstall **Node.js** et **npm** Gestionnaire de package de hello pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="9c15f-124">Run hello following commands tooinstall **Node.js** and **npm** hello package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="9c15f-125">Exécutez hello suivant de commandes toomake un dossier de projet `mysqlnodejs` et installer le package de mysql2 hello dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="9c15f-125">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="9c15f-126">Vérifier l’installation de hello en vérifiant le texte de sortie de liste de npm pour `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="9c15f-126">Verify hello installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="9c15f-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="9c15f-127">**Mac OS**</span></span>
1. <span data-ttu-id="9c15f-128">Entrez hello suivant de commandes tooinstall **brew**, un gestionnaire de package de facile à utiliser pour Mac OS X et **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="9c15f-128">Enter hello following commands tooinstall **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="9c15f-129">Exécutez hello suivant de commandes toomake un dossier de projet `mysqlnodejs` et installer le package de mysql2 hello dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="9c15f-129">Run hello following commands toomake a project folder `mysqlnodejs` and install hello mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="9c15f-130">Vérifier l’installation de hello en hello `npm list` sortie texte pour `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="9c15f-130">Verify hello installation by checking hello `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="9c15f-131">numéro de version Hello peut varier comme nouveaux correctifs sont publiés.</span><span class="sxs-lookup"><span data-stu-id="9c15f-131">hello version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="9c15f-132">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="9c15f-132">Get connection information</span></span>
<span data-ttu-id="9c15f-133">Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="9c15f-134">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="9c15f-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9c15f-135">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c15f-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9c15f-136">Dans le volet gauche de hello, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé (par exemple, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="9c15f-136">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="9c15f-137">Cliquez sur le nom du serveur hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="9c15f-137">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="9c15f-138">Serveur hello sélectionnez **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="9c15f-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="9c15f-139">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="9c15f-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9c15f-140">![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-nodejs/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="9c15f-140">![Azure Database for MySQL - Server Admin Login](./media/connect-nodejs/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="9c15f-141">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="9c15f-142">En cours d’exécution du code JavaScript hello dans Node.js</span><span class="sxs-lookup"><span data-stu-id="9c15f-142">Running hello JavaScript code in Node.js</span></span>
1. <span data-ttu-id="9c15f-143">Collez le code JavaScript de hello dans des fichiers texte et l’enregistrer dans un dossier de projet avec l’extension de fichier .js, tels que C:\nodejsmysql\createtable.js ou /home/username/nodejsmysql/createtable.js</span><span class="sxs-lookup"><span data-stu-id="9c15f-143">Paste hello JavaScript code into text files, and save into a project folder with file extension .js, such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js</span></span>
2. <span data-ttu-id="9c15f-144">Lancez l’invite de commandes hello ou bash shell.</span><span class="sxs-lookup"><span data-stu-id="9c15f-144">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="9c15f-145">Basculez dans votre dossier de projet : `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="9c15f-145">Change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="9c15f-146">application de hello toorun, tapez Bonjour nœud commande est suivi par nom de fichier hello, tel que `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="9c15f-146">toorun hello application, type hello node command followed by hello file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="9c15f-147">Sur Windows, si l’application du nœud hello n’est pas dans votre variable d’environnement path, vous devrez peut-être toouse hello chemin d’accès complet toolaunch hello nœud application tel que`"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="9c15f-147">On Windows, if hello node application is not in your environment variable path, you may need toouse hello full path toolaunch hello node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="9c15f-148">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="9c15f-148">Connect, create table, and insert data</span></span>
<span data-ttu-id="9c15f-149">Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-149">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="9c15f-150">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-150">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="9c15f-151">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) fonction est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="9c15f-151">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="9c15f-152">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-152">hello [query()](https://github.com/mysqljs/mysql#performing-queries) function is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="9c15f-153">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-153">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="9c15f-154">Lire les données</span><span class="sxs-lookup"><span data-stu-id="9c15f-154">Read data</span></span>
<span data-ttu-id="9c15f-155">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-155">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="9c15f-156">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-156">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="9c15f-157">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) méthode est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="9c15f-157">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="9c15f-158">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) méthode est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-158">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> <span data-ttu-id="9c15f-159">tableau de résultats Hello est toohold utilisé hello des résultats de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-159">hello results array is used toohold hello results of hello query.</span></span>

<span data-ttu-id="9c15f-160">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-160">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="9c15f-161">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="9c15f-161">Update data</span></span>
<span data-ttu-id="9c15f-162">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-162">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="9c15f-163">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-163">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="9c15f-164">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) méthode est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="9c15f-164">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="9c15f-165">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) méthode est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-165">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="9c15f-166">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="9c15f-167">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="9c15f-167">Delete data</span></span>
<span data-ttu-id="9c15f-168">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-168">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="9c15f-169">Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-169">hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used toointerface with hello MySQL server.</span></span> <span data-ttu-id="9c15f-170">Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) méthode est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="9c15f-170">hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="9c15f-171">Hello [query()](https://github.com/mysqljs/mysql#performing-queries) méthode est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="9c15f-171">hello [query()](https://github.com/mysqljs/mysql#performing-queries) method is used tooexecute hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="9c15f-172">Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="9c15f-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'myserver4demo.mysql.database.azure.com',
    user: 'myadmin@myserver4demo',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="9c15f-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c15f-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9c15f-174">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="9c15f-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
