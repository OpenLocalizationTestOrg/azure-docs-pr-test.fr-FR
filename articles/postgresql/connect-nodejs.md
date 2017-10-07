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
# <a name="azure-database-for-postgresql-use-nodejs-tooconnect-and-query-data"></a><span data-ttu-id="fbe9b-103">Base de données Azure pour PostgreSQL : utilisez Node.js tooconnect et interroger des données</span><span class="sxs-lookup"><span data-stu-id="fbe9b-103">Azure Database for PostgreSQL: Use Node.js tooconnect and query data</span></span>
<span data-ttu-id="fbe9b-104">Ce démarrage rapide montre comment tooconnect tooan Azure de base de données pour l’utilisation de PostgreSQL [Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="fbe9b-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using [Node.js](https://nodejs.org/).</span></span> <span data-ttu-id="fbe9b-105">Il montre comment toouse SQL instructions tooquery, insérer, mettre à jour et supprimer des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="fbe9b-106">Hello étapes décrites dans cet article supposent que vous êtes familiarisé avec le développement à l’aide de Node.js, et que vous êtes tooworking nouvelle base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-106">hello steps in this article assume that you are familiar with developing using Node.js, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbe9b-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fbe9b-107">Prerequisites</span></span>
<span data-ttu-id="fbe9b-108">Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :</span><span class="sxs-lookup"><span data-stu-id="fbe9b-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fbe9b-109">Créer une base de données - Portail</span><span class="sxs-lookup"><span data-stu-id="fbe9b-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="fbe9b-110">Créer une base de données - CLI</span><span class="sxs-lookup"><span data-stu-id="fbe9b-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="fbe9b-111">Il vous faudra également :</span><span class="sxs-lookup"><span data-stu-id="fbe9b-111">You also need to:</span></span>
- <span data-ttu-id="fbe9b-112">Installez [Node.js](https://nodejs.org)</span><span class="sxs-lookup"><span data-stu-id="fbe9b-112">Install [Node.js](https://nodejs.org)</span></span>

## <a name="install-pg-client"></a><span data-ttu-id="fbe9b-113">Installer le client pg</span><span class="sxs-lookup"><span data-stu-id="fbe9b-113">Install pg client</span></span>
<span data-ttu-id="fbe9b-114">Installez [pg](https://www.npmjs.com/package/pg), qui est un client PostgreSQL pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-114">Install [pg](https://www.npmjs.com/package/pg), which is a PostgreSQL client for Node.js.</span></span>

<span data-ttu-id="fbe9b-115">toodo exécuter par conséquent, le Gestionnaire de package de nœud hello (npm) pour JavaScript à partir de votre client de ligne de commande tooinstall hello pg.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-115">toodo so, run hello node package manager (npm) for JavaScript from your command line tooinstall hello pg client.</span></span>
```bash
npm install pg
```

<span data-ttu-id="fbe9b-116">Vérifier l’installation de hello en répertoriant les packages hello installés.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-116">Verify hello installation by listing hello packages installed.</span></span>
```bash
npm list
```

## <a name="get-connection-information"></a><span data-ttu-id="fbe9b-117">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="fbe9b-117">Get connection information</span></span>
<span data-ttu-id="fbe9b-118">Obtenir les informations nécessaires tooconnect toohello de hello connexion base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-118">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="fbe9b-119">Vous devez hello des informations d’identification de nom et la connexion serveur complet.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-119">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fbe9b-120">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fbe9b-120">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fbe9b-121">Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-121">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created.</span></span>
3. <span data-ttu-id="fbe9b-122">Cliquez sur le nom du serveur hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-122">Click hello server name.</span></span>
4. <span data-ttu-id="fbe9b-123">Serveur hello sélectionnez **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-123">Select hello server's **Overview** page.</span></span> <span data-ttu-id="fbe9b-124">Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-124">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fbe9b-125">![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/connect-nodejs/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="fbe9b-125">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-nodejs/1-connection-string.png)</span></span>
5. <span data-ttu-id="fbe9b-126">Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-126">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="running-hello-javascript-code-in-nodejs"></a><span data-ttu-id="fbe9b-127">En cours d’exécution du code JavaScript hello dans Node.js</span><span class="sxs-lookup"><span data-stu-id="fbe9b-127">Running hello JavaScript code in Node.js</span></span>
<span data-ttu-id="fbe9b-128">Vous pouvez lancer des Node.js à partir de hello un interpréteur de commandes shell ou windows invite de commandes en tapant `node`, puis exécuter du code JavaScript exemple hello de manière interactive par copie et les coller dans une invite de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-128">You may launch Node.js from hello bash shell or windows command prompt by typing `node`, then run hello example JavaScript code interactively by copy and pasting it onto hello prompt.</span></span> <span data-ttu-id="fbe9b-129">Ou bien, vous pouvez enregistrer le code JavaScript de hello dans un fichier texte et le lancement `node filename.js` avec le nom de fichier hello comme un paramètre de toorun il.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-129">Alternatively, you may save hello JavaScript code into a text file and launch `node filename.js` with hello file name as a parameter toorun it.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="fbe9b-130">Se connecter, créer des tables et insérer des données</span><span class="sxs-lookup"><span data-stu-id="fbe9b-130">Connect, create table, and insert data</span></span>
<span data-ttu-id="fbe9b-131">Suivante de hello utilisation tooconnect de code et chargez à l’aide de données hello **CREATE TABLE** et **INSERT INTO** instructions SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-131">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>
<span data-ttu-id="fbe9b-132">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-132">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="fbe9b-133">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-133">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="fbe9b-134">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-134">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="fbe9b-135">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-135">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

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

## <a name="read-data"></a><span data-ttu-id="fbe9b-136">Lire les données</span><span class="sxs-lookup"><span data-stu-id="fbe9b-136">Read data</span></span>
<span data-ttu-id="fbe9b-137">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **sélectionnez** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-137">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="fbe9b-138">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-138">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="fbe9b-139">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-139">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="fbe9b-140">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-140">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="fbe9b-141">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-141">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="fbe9b-142">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="fbe9b-142">Update data</span></span>
<span data-ttu-id="fbe9b-143">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **mise à jour** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-143">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="fbe9b-144">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-144">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="fbe9b-145">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-145">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="fbe9b-146">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-146">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="fbe9b-147">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-147">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="delete-data"></a><span data-ttu-id="fbe9b-148">Suppression de données</span><span class="sxs-lookup"><span data-stu-id="fbe9b-148">Delete data</span></span>
<span data-ttu-id="fbe9b-149">Suivante de hello utilisation tooconnect de code et lire à l’aide de données hello un **supprimer** instruction SQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-149">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="fbe9b-150">Hello [pg. Client](https://github.com/brianc/node-postgres/wiki/Client) objet est toointerface utilisé avec le serveur de PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-150">hello [pg.Client](https://github.com/brianc/node-postgres/wiki/Client) object is used toointerface with hello PostgreSQL server.</span></span> <span data-ttu-id="fbe9b-151">Hello [pg. Client.Connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) fonction est utilisée tooestablish hello connexion toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-151">hello [pg.Client.connect()](https://github.com/brianc/node-postgres/wiki/Client#method-connect) function is used tooestablish hello connection toohello server.</span></span> <span data-ttu-id="fbe9b-152">Hello [pg. Client.Query()](https://github.com/brianc/node-postgres/wiki/Query) fonction est la requête SQL hello tooexecute utilisé par rapport à la base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-152">hello [pg.Client.query()](https://github.com/brianc/node-postgres/wiki/Query) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> 

<span data-ttu-id="fbe9b-153">Remplacez les valeurs hello que vous avez spécifié lorsque vous avez créé la base de données et serveur de hello hello hôte, dbname, utilisateur et les paramètres de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="fbe9b-153">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="fbe9b-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fbe9b-154">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fbe9b-155">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="fbe9b-155">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
