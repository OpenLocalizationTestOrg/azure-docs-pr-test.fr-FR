---
title: "Se connecter tooAzure de base de données pour PostgreSQL à partir de Node.js | Documents Microsoft"
description: "Ce démarrage rapide fournit un exemple de code Node.js, vous pouvez utiliser tooconnect et interroger des données à partir de la base de données Azure pour PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 9b269d72068ecc24bcf3fb447a2efeda512c698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a>Base de données Azure pour PostgreSQL : utilisez Node.js tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan Azure de base de données pour l’utilisation de PostgreSQL [Node.js](https://nodejs.org/). Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello. Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de Node.js, et que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Créer une base de données - Portail](quickstart-create-server-database-portal.md)
- [Créer une base de données - CLI](quickstart-create-server-database-azure-cli.md)

Il vous faudra également :
- Installez [Node.js](https://nodejs.org)

## <a name="install-pg-client"></a>Installer le client pg
Installez [pg](https://www.npmjs.com/package/pg), qui est un client PostgreSQL pour Node.js.

toodo exécuter par conséquent, le Gestionnaire de package de nœud hello (npm) pour JavaScript à partir de votre client de ligne de commande tooinstall hello pg.
```bash
npm install pg
```

Vérifier l’installation de hello en répertoriant les packages hello installés.
```bash
npm list
```

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous venez de créer.
3. Cliquez sur le nom du serveur hello.
4. Serveur hello sélectionnez **vue d’ensemble** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.
 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-nodejs/1-connection-string.png)
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="running-hello-javascript-code-in-nodejs"></a>En cours d’exécution du code JavaScript hello dans Node.js
Vous pouvez lancer des Node.js à partir de hello un interpréteur de commandes shell ou windows invite de commandes en tapant `node`, puis exécuter du code JavaScript exemple hello de manière interactive par copie et les coller dans une invite de commandes hello. Ou bien, vous pouvez enregistrer le code JavaScript de hello dans un fichier texte et le lancement `node filename.js` avec le nom de fichier hello comme un paramètre de toorun il.

## <a name="connect-create-table-and-insert-data"></a>Se connecter, créer des tables et insérer des données
Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL.
Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur. Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL. 

Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DROP TABLE IF EXISTS inventory;
        CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
        INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
        INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
        INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    `;

    client
        .query(query)
        .then(() => {
            console.log('Table created successfully!');
            client.end(console.log('Closed client connection'));
        })
        .catch(err => console.log(err))
        .then(() => {
            console.log('Finished execution, exiting now');
            process.exit();
        });
}
```

## <a name="read-data"></a>Lire les données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL. Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur. Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL. 

Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else { queryDatabase(); }
});

function queryDatabase() {
  
    console.log(`Running query tooPostgreSQL server: ${config.host}`);

    const query = 'SELECT * FROM inventory;';

    client.query(query)
        .then(res => {
            const rows = res.rows;

            rows.map(row => {
                console.log(`Read: ${JSON.stringify(row)}`);
            });

            process.exit();
        })
        .catch(err => {
            console.log(err);
        });
}
```

## <a name="update-data"></a>Mettre à jour des données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL. Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur. Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL. 

Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) throw err;
    else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        UPDATE inventory 
        SET quantity= 1000 WHERE name='banana';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Update completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="delete-data"></a>Suppression de données
Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL. Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello. Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur. Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL. 

Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe. 

```javascript
const pg = require('pg');

const config = {
    host: '<your-db-server-name>.postgres.database.azure.com',
    // Do not hard code your username and password.
    // Consider using Node environment variables.
    user: '<your-db-username>',     
    password: '<your-password>',
    database: '<name-of-database>',
    port: 5432,
    ssl: true
};

const client = new pg.Client(config);

client.connect(err => {
    if (err) {
        throw err;
    } else {
        queryDatabase();
    }
});

function queryDatabase() {
    const query = `
        DELETE FROM inventory 
        WHERE name = 'apple';
    `;

    client
        .query(query)
        .then(result => {
            console.log('Delete completed');
            console.log(`Rows affected: ${result.rowCount}`);
        })
        .catch(err => {
            console.log(err);
            throw err;
        });
}
```

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./howto-migrate-using-export-and-import.md)
