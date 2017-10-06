---
title: "didacticiel aaaNode.js pour hello API DocumentDB de base de données Azure Cosmos | Documents Microsoft"
description: "Didacticiel Node.js qui crée une base de données Cosmos avec hello API DocumentDB."
keywords: "didacticiel node.js, base de données du nœud"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Didacticiel de Node.js : hello utilisation API DocumentDB dans la base de données Azure Cosmos toocreate une application de console Node.js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js pour MongoDB](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bienvenue dans le didacticiel de Node.js toohello pour hello Azure Cosmos DB Node.js SDK ! À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.

Nous allons aborder les points suivants :

* Création et connexion de compte de base de données Azure Cosmos tooan
* Configuration de votre application
* Création d’une base de données de nœud
* Création d’une collection
* Création de documents JSON
* Interrogation de collection de hello
* Remplacement d'un document
* Suppression d’un document
* Suppression de base de données du nœud hello

Vous n’avez pas le temps ? Ne vous inquiétez pas ! solution complète de Hello est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Consultez [obtenir la solution complète de hello](#GetSolution) pour obtenir des instructions rapides.

Une fois que vous avez terminé le didacticiel de Node.js hello, veuillez utiliser hello des boutons de vote en haut de hello et en bas de cette page de toogive nous vos commentaires. Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires.

Commençons dès maintenant !

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Configuration requise pour le didacticiel de Node.js hello
Vérifiez que vous avez hello suivantes :

* Un compte Azure actif. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.
    * Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.
* [Node.js](https://nodejs.org/) version v0.10.29 ou supérieure.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Étape 1 : créer un compte Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[configurer votre application Node.js](#SetupNode). Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre application Node.js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Étape 2 : configurer votre application Node.js
1. Ouvrez votre terminal préféré.
2. Recherchez hello dossier ou un répertoire où vous souhaitez toosave votre application Node.js.
3. Créez deux fichiers JavaScript vides avec hello suivant de commandes :
   * Windows :
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X :
     * ```touch app.js```
     * ```touch config.js```
4. Installez le module de documentdb hello via npm. Utilisez hello de commande suivante :
   * ```npm install documentdb --save```

Parfait ! Vous avez terminé l’installation, nous pouvons donc passer à l’écriture du code.

## <a id="Config"></a>Étape 3 : définir les configurations de votre application
Ouvrez ```config.js``` dans l’éditeur de texte de votre choix.

Ensuite, copiez et collez hello extrait de code ci-dessous et définir des propriétés ```config.endpoint``` et ```config.primaryKey``` tooyour base de données Azure Cosmos uri de point de terminaison et la clé primaire. Vous trouverez ces deux configurations Bonjour [portail Azure](https://portal.azure.com).

![Didacticiel de Node.js - capture d’écran de hello portail Azure, indiquant un compte de base de données Azure Cosmos, avec un concentrateur actif de hello mis en surbrillance, bouton de clés hello mise en surbrillance dans le panneau de compte de base de données Azure Cosmos hello et hello URI, valeurs de clés primaires et secondaires mis en surbrillance sur hello Panneau clés - base de données du nœud][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Copiez et collez hello ```database id```, ```collection id```, et ```JSON documents``` tooyour ```config``` objet ci-dessous, où vous avez défini votre ```config.endpoint``` et ```config.authKey``` propriétés. Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser Azure Cosmos DB [l’outil de Migration de données](import-data.md) au lieu d’ajouter des définitions de document hello.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Hello de base de données, la collection et les définitions de document agira en tant que votre base de données Azure Cosmos ```database id```, ```collection id```et les données de documents.

Enfin, exportez votre ```config``` de l’objet, afin que vous pouvez le référencer dans hello ```app.js``` fichier.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Étape 4 : Connexion de compte de base de données Azure Cosmos tooan
Ouvrez votre vide ```app.js``` fichier dans l’éditeur de texte hello. Copiez et collez le code hello ci-dessous tooimport hello ```documentdb``` module et votre nouvellement créé ```config``` module.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Copiez et collez hello de toouse code hello précédemment enregistré ```config.endpoint``` et ```config.primaryKey``` toocreate un DocumentClient de nouveau.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Maintenant que vous avez des clients de base de données Azure Cosmos hello code tooinitialize hello, examinons une utilisation des ressources de base de données Azure Cosmos.

## <a name="step-5-create-a-node-database"></a>Étape 5 : Création d’une base de données de nœud
Copiez et collez le code hello ci-dessous tooset hello état HTTP pour introuvable, l’url de base de données hello et url de collection de hello. Ces URL est comment client de base de données Azure Cosmos hello trouve hello de base de données à droite et de la collection.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) fonction Hello **DocumentClient** classe. Une base de données est un conteneur logique de hello de stockage de documents partitionné entre des collections.

Copiez et collez hello **getDatabase** (fonction) pour la création de votre nouvelle base de données dans le fichier app.js hello hello ```id``` spécifié dans hello ```config``` objet. Hello fonction vérifiera si hello de base de données avec hello même ```FamilyRegistry``` id n’existe pas déjà. Si elle existe, nous allons retourner cette base de données au lieu d’en créer une.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copiez et collez code hello ci-dessous lorsque vous définissez hello **getDatabase** fonction fonction d’assistance de hello tooadd **quitter** qui imprime message de sortie hello et appel de hello trop**getDatabase** (fonction).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Félicitations ! Vous avez créé une base de données Azure Cosmos DB.

## <a id="CreateColl"></a>Étape 6 : Création d’une collection
> [!WARNING]
> **CreateDocumentCollectionAsync** crée une collection, ce qui a des conséquences tarifaires. Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) fonction Hello **DocumentClient** classe. Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.

Copiez et collez hello **getCollection** fonction sous hello **getDatabase** de fonction dans hello app.js fichier toocreate votre nouvelle collection avec hello ```id``` spécifié dans hello ```config```objet. Là encore, nous vérifierons toomake vraiment une collection de hello même ```FamilyCollection``` id n’existe pas déjà. Si elle existe, nous allons retourner cette collection au lieu d’en créer une.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Copiez et collez le code hello sous l’appel de hello trop**getDatabase** tooexecute hello **getCollection** (fonction).

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Félicitations ! Vous avez créé une collection Azure Cosmos DB.

## <a id="CreateDoc"></a>Étape 7 : Création d’un document
A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) fonction Hello **DocumentClient** classe. Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur. Vous pouvez maintenant insérer un document dans Azure Cosmos DB.

Copiez et collez hello **getFamilyDocument** fonction sous hello **getCollection** fonction pour créer des documents hello contenant des données JSON hello économisées hello ```config``` objet. Là encore, nous allons Vérifiez toomake un document avec hello même id n’existe pas déjà.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Copiez et collez le code hello sous l’appel de hello trop**getCollection** tooexecute hello **getFamilyDocument** (fonction).

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Félicitations ! Vous avez créé un document Azure Cosmos DB.

![La base de données - diagramme illustrant la relation hiérarchique de hello entre le compte de hello, la base de données hello, collection de hello et documents de hello - nœud didacticiel de Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Étape 8 : interroger les ressources Azure Cosmos DB
Azure Cosmos DB prend en charge les [requêtes enrichies](documentdb-sql-query.md) sur les documents JSON stockés dans chaque collection. Hello exemple de code suivant montre une requête que vous pouvez exécuter par rapport aux documents de hello dans votre collection.

Copiez et collez hello **queryCollection** fonction sous hello **getFamilyDocument** fonction hello app.js fichier. Azure Cosmos DB prend en charge des requêtes similaires à SQL, comme indiqué ci-dessous. Pour plus d’informations sur la création des requêtes complexes, consultez hello [Query Playground](https://www.documentdb.com/sql/demo) et hello [requête documentation](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


Hello suivant le diagramme illustre la requête SQL de base de données Azure Cosmos de hello syntaxe est appelée sur la collection de hello créée.

![La base de données - diagramme illustrant la portée de hello et ce qui signifie que de requête de hello - nœud didacticiel de Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) mot clé est facultatif dans la requête de hello, car les requêtes de base de données Azure Cosmos sont déjà incluses dans l’étendue tooa unique collection. Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez. Base de données Azure Cosmos déduira familles, racine ou le nom de la variable hello choisie, référence hello de collection actuel par défaut.

Copiez et collez le code hello sous l’appel de hello trop**getFamilyDocument** tooexecute hello **queryCollection** (fonction).

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Félicitations ! Vous avez interrogé des documents Azure Cosmos DB.

## <a id="ReplaceDocument"></a>Étape 9 : Remplacement d’un document
Azure Cosmos DB prend en charge le remplacement des documents JSON.

Copiez et collez hello **replaceFamilyDocument** fonction sous hello **queryCollection** fonction hello app.js fichier.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copiez et collez le code hello sous l’appel de hello trop**queryCollection** tooexecute hello **replaceDocument** (fonction). En outre, ajoutez hello code toocall **queryCollection** encore tooverify document hello avait a été modifié.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Félicitations ! Vous avez remplacé un document Azure Cosmos DB.

## <a id="DeleteDocument"></a>Étape 10 : Suppression d’un document
Azure Cosmos DB prend en charge la suppression des documents JSON.

Copiez et collez hello **deleteFamilyDocument** fonction sous hello **replaceFamilyDocument** (fonction).

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Copiez et collez le code hello ci-dessous hello appel toohello deuxième **queryCollection** tooexecute hello **deleteDocument** (fonction).

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Félicitations ! Vous avez supprimé un document Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Étape 11 : Supprimer la base de données du nœud hello
Suppression hello créé la base de données supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).

Copiez et collez hello **nettoyage** fonction sous hello **deleteFamilyDocument** fonction de base de données tooremove hello et toutes les ressources enfants de hello.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Copiez et collez le code hello sous l’appel de hello trop**deleteFamilyDocument** tooexecute hello **nettoyage** (fonction).

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>Étape 12 : Exécution de l’application Node.js
Complètement, séquence hello pour appeler vos fonctions doit ressembler à ceci :

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```

Vous devez voir la sortie hello de votre application démarrée get. sortie de Hello doit correspondre au texte d’exemple hello ci-dessous.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Félicitations ! Créée, vous avez terminé hello Node.js didacticiel et avez votre première application de console de base de données Azure Cosmos !

## <a id="GetSolution"></a>Obtenir complète solution du didacticiel Node.js hello
Si vous n’avez temps toocomplete hello des étapes de ce didacticiel, ou code de hello toodownload uniquement, vous pouvez l’obtenir à partir de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

toorun hello GetStarted solution qui contient tous les exemples hello dans cet article vous serez hello éléments suivants sont nécessaires :

* [Un compte Azure Cosmos DB][create-account].
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution disponible sur GitHub.

Installer hello **documentdb** module via npm. Utilisez hello de commande suivante :

* ```npm install documentdb --save```

Ensuite, dans hello ```config.js``` de fichiers, les valeurs mises à jour hello config.endpoint et config.authKey comme décrit dans [étape 3 : définir des configurations de votre application](#Config). 

Puis, dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello : ```node app.js```.

Voilà, vous n’avez plus qu’à générer l’élément pour être sur la bonne voie ! 

## <a name="next-steps"></a>Étapes suivantes
* Vous voulez un exemple de Node.js plus complexe ? Consultez [Création d’une application web Node.js avec Azure Cosmos DB](documentdb-nodejs-application.md).
* Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).
* Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
* En savoir plus sur le modèle de programmation hello Bonjour section développer Hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
