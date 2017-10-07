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
# <a name="azure-database-for-mysql-use-nodejs-tooconnect-and-query-data"></a>Base de données Azure pour MySQL : utilisez Node.js tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données pour l’utilisation de MySQL [Node.js](https://nodejs.org/) de plateformes Windows, Ubuntu Linux et Mac. Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de Node.js, et que vous êtes tooworking nouvelle base de données Azure pour MySQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

Il vous faudra également :
- Installer hello [Node.js](https://nodejs.org) runtime.
- Installer [mysql2](https://www.npmjs.com/package/mysql2) tooMySQL tooconnect de hello application Node.js du package. 

## <a name="install-nodejs-and-hello-mysql-connector"></a>Installation de Node.js et hello connecteur MySQL
Selon votre plateforme, suivez hello instructions appropriées tooinstall Node.js. Utilisez npm tooinstall hello mysql2 package et ses dépendances dans votre dossier de projet.

### <a name="windows"></a>**Windows**
1. Visitez hello [page de téléchargements de Node.js](https://nodejs.org/en/download/) et sélectionnez votre option de programme d’installation de Windows souhaitée.
2. Créez un dossier de projet local, tel que `nodejsmysql`. 
3. Lancez invite de commandes hello et cd dans le dossier du projet hello, telles que`cd c:\nodejsmysql\`
4. Exécuter la bibliothèque de hello NPM outil tooinstall hello mysql2 dans le dossier du projet hello.

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. Vérifier l’installation de hello en hello `npm list` sortie texte pour `mysql2@1.3.5`.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
1. Suivante d’exécution hello commandes tooinstall **Node.js** et **npm** Gestionnaire de package de hello pour Node.js.

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. Exécutez hello suivant de commandes toomake un dossier de projet `mysqlnodejs` et installer le package de mysql2 hello dans ce dossier.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. Vérifier l’installation de hello en vérifiant le texte de sortie de liste de npm pour `mysql2@1.3.5`.

### <a name="mac-os"></a>**Mac OS**
1. Entrez hello suivant de commandes tooinstall **brew**, un gestionnaire de package de facile à utiliser pour Mac OS X et **Node.js**.

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. Exécutez hello suivant de commandes toomake un dossier de projet `mysqlnodejs` et installer le package de mysql2 hello dans ce dossier.

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. Vérifier l’installation de hello en hello `npm list` sortie texte pour `mysql2@1.3.6`. numéro de version Hello peut varier comme nouveaux correctifs sont publiés.

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le volet gauche de hello, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé (par exemple, **myserver4demo**).
3. Cliquez sur le nom du serveur hello **myserver4demo**.
4. Serveur hello sélectionnez **propriétés** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Azure Database pour MySQL - Connexion d’administrateur du serveur](./media/connect-nodejs/1_server-properties-name-login.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>En cours d’exécution du code JavaScript hello dans Node.js
1. Collez le code JavaScript de hello dans des fichiers texte et l’enregistrer dans un dossier de projet avec l’extension de fichier .js, tels que C:\nodejsmysql\createtable.js ou /home/username/nodejsmysql/createtable.js
2. Lancez l’invite de commandes hello ou bash shell. Basculez dans votre dossier de projet : `cd nodejsmysql`.
3. application de hello toorun, tapez Bonjour nœud commande est suivi par nom de fichier hello, tel que `node createtable.js`.
4. Sur Windows, si l’application du nœud hello n’est pas dans votre variable d’environnement path, vous devrez peut-être toouse hello chemin d’accès complet toolaunch hello nœud application tel que`"C:\Program Files\nodejs\node.exe" createtable.js`

## <a name="connect-create-table-and-insert-data"></a>Se connecter, créer des tables et insérer des données
Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL.

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello. Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) fonction est utilisée tooestablish hello connexion toohello du serveur. Hello [query()](https://github.com/mysqljs/mysql#performing-queries) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL. 

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

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

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. 

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello. Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) méthode est utilisée tooestablish hello connexion toohello du serveur. Hello [query()](https://github.com/mysqljs/mysql#performing-queries) méthode est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL. tableau de résultats Hello est toohold utilisé hello des résultats de requête de hello.

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

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

## <a name="update-data"></a>Mettre à jour des données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL. 

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello. Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) méthode est utilisée tooestablish hello connexion toohello du serveur. Hello [query()](https://github.com/mysqljs/mysql#performing-queries) méthode est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL. 

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

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

## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. 

Hello [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) méthode est toointerface utilisé avec le serveur MySQL de hello. Hello [connect()](https://github.com/mysqljs/mysql#establishing-connections) méthode est utilisée tooestablish hello connexion toohello du serveur. Hello [query()](https://github.com/mysqljs/mysql#performing-queries) méthode est la requête SQL hello tooexecute utilisé par rapport à la base de données MySQL. 

Remplacez hello `host`, `user`, `password`, et `database` paramètres avec des valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello.

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

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./concepts-migrate-import-export.md)
