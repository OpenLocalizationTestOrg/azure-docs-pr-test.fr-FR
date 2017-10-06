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
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="0213f-104">Didacticiel de Node.js : hello utilisation API DocumentDB dans la base de données Azure Cosmos toocreate une application de console Node.js</span><span class="sxs-lookup"><span data-stu-id="0213f-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0213f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0213f-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="0213f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0213f-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="0213f-107">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="0213f-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="0213f-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0213f-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="0213f-109">Java</span><span class="sxs-lookup"><span data-stu-id="0213f-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="0213f-110">C++</span><span class="sxs-lookup"><span data-stu-id="0213f-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="0213f-111">Bienvenue dans le didacticiel de Node.js toohello pour hello Azure Cosmos DB Node.js SDK !</span><span class="sxs-lookup"><span data-stu-id="0213f-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="0213f-112">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="0213f-113">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0213f-113">We'll cover:</span></span>

* <span data-ttu-id="0213f-114">Création et connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="0213f-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="0213f-115">Configuration de votre application</span><span class="sxs-lookup"><span data-stu-id="0213f-115">Setting up your application</span></span>
* <span data-ttu-id="0213f-116">Création d’une base de données de nœud</span><span class="sxs-lookup"><span data-stu-id="0213f-116">Creating a node database</span></span>
* <span data-ttu-id="0213f-117">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="0213f-117">Creating a collection</span></span>
* <span data-ttu-id="0213f-118">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="0213f-118">Creating JSON documents</span></span>
* <span data-ttu-id="0213f-119">Interrogation de collection de hello</span><span class="sxs-lookup"><span data-stu-id="0213f-119">Querying hello collection</span></span>
* <span data-ttu-id="0213f-120">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="0213f-120">Replacing a document</span></span>
* <span data-ttu-id="0213f-121">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="0213f-121">Deleting a document</span></span>
* <span data-ttu-id="0213f-122">Suppression de base de données du nœud hello</span><span class="sxs-lookup"><span data-stu-id="0213f-122">Deleting hello node database</span></span>

<span data-ttu-id="0213f-123">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="0213f-123">Don't have time?</span></span> <span data-ttu-id="0213f-124">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="0213f-124">Don't worry!</span></span> <span data-ttu-id="0213f-125">solution complète de Hello est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0213f-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="0213f-126">Consultez [obtenir la solution complète de hello](#GetSolution) pour obtenir des instructions rapides.</span><span class="sxs-lookup"><span data-stu-id="0213f-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="0213f-127">Une fois que vous avez terminé le didacticiel de Node.js hello, veuillez utiliser hello des boutons de vote en haut de hello et en bas de cette page de toogive nous vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="0213f-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="0213f-128">Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="0213f-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="0213f-129">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="0213f-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="0213f-130">Configuration requise pour le didacticiel de Node.js hello</span><span class="sxs-lookup"><span data-stu-id="0213f-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="0213f-131">Vérifiez que vous avez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0213f-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="0213f-132">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0213f-132">An active Azure account.</span></span> <span data-ttu-id="0213f-133">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="0213f-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="0213f-134">Vous pouvez également utiliser hello [Azure Cosmos DB émulateur](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0213f-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="0213f-135">[Node.js](https://nodejs.org/) version v0.10.29 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="0213f-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="0213f-136">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0213f-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="0213f-137">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="0213f-138">Si vous avez déjà un compte que vous souhaitez toouse, vous pouvez passer trop[configurer votre application Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="0213f-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="0213f-139">Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre application Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="0213f-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="0213f-140"><a id="SetupNode"></a>Étape 2 : configurer votre application Node.js</span><span class="sxs-lookup"><span data-stu-id="0213f-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="0213f-141">Ouvrez votre terminal préféré.</span><span class="sxs-lookup"><span data-stu-id="0213f-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="0213f-142">Recherchez hello dossier ou un répertoire où vous souhaitez toosave votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="0213f-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="0213f-143">Créez deux fichiers JavaScript vides avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="0213f-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="0213f-144">Windows :</span><span class="sxs-lookup"><span data-stu-id="0213f-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="0213f-145">Linux/OS X :</span><span class="sxs-lookup"><span data-stu-id="0213f-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="0213f-146">Installez le module de documentdb hello via npm.</span><span class="sxs-lookup"><span data-stu-id="0213f-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="0213f-147">Utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0213f-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="0213f-148">Parfait !</span><span class="sxs-lookup"><span data-stu-id="0213f-148">Great!</span></span> <span data-ttu-id="0213f-149">Vous avez terminé l’installation, nous pouvons donc passer à l’écriture du code.</span><span class="sxs-lookup"><span data-stu-id="0213f-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="0213f-150"><a id="Config"></a>Étape 3 : définir les configurations de votre application</span><span class="sxs-lookup"><span data-stu-id="0213f-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="0213f-151">Ouvrez ```config.js``` dans l’éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0213f-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="0213f-152">Ensuite, copiez et collez hello extrait de code ci-dessous et définir des propriétés ```config.endpoint``` et ```config.primaryKey``` tooyour base de données Azure Cosmos uri de point de terminaison et la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="0213f-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="0213f-153">Vous trouverez ces deux configurations Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0213f-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Didacticiel de Node.js - capture d’écran de hello portail Azure, indiquant un compte de base de données Azure Cosmos, avec un concentrateur actif de hello mis en surbrillance, bouton de clés hello mise en surbrillance dans le panneau de compte de base de données Azure Cosmos hello et hello URI, valeurs de clés primaires et secondaires mis en surbrillance sur hello Panneau clés - base de données du nœud][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="0213f-155">Copiez et collez hello ```database id```, ```collection id```, et ```JSON documents``` tooyour ```config``` objet ci-dessous, où vous avez défini votre ```config.endpoint``` et ```config.authKey``` propriétés.</span><span class="sxs-lookup"><span data-stu-id="0213f-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="0213f-156">Si vous avez déjà des données que vous souhaitez toostore dans votre base de données, vous pouvez utiliser Azure Cosmos DB [l’outil de Migration de données](import-data.md) au lieu d’ajouter des définitions de document hello.</span><span class="sxs-lookup"><span data-stu-id="0213f-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

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


<span data-ttu-id="0213f-157">Hello de base de données, la collection et les définitions de document agira en tant que votre base de données Azure Cosmos ```database id```, ```collection id```et les données de documents.</span><span class="sxs-lookup"><span data-stu-id="0213f-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="0213f-158">Enfin, exportez votre ```config``` de l’objet, afin que vous pouvez le référencer dans hello ```app.js``` fichier.</span><span class="sxs-lookup"><span data-stu-id="0213f-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="0213f-159"><a id="Connect"></a>Étape 4 : Connexion de compte de base de données Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="0213f-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="0213f-160">Ouvrez votre vide ```app.js``` fichier dans l’éditeur de texte hello.</span><span class="sxs-lookup"><span data-stu-id="0213f-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="0213f-161">Copiez et collez le code hello ci-dessous tooimport hello ```documentdb``` module et votre nouvellement créé ```config``` module.</span><span class="sxs-lookup"><span data-stu-id="0213f-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="0213f-162">Copiez et collez hello de toouse code hello précédemment enregistré ```config.endpoint``` et ```config.primaryKey``` toocreate un DocumentClient de nouveau.</span><span class="sxs-lookup"><span data-stu-id="0213f-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="0213f-163">Maintenant que vous avez des clients de base de données Azure Cosmos hello code tooinitialize hello, examinons une utilisation des ressources de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0213f-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="0213f-164">Étape 5 : Création d’une base de données de nœud</span><span class="sxs-lookup"><span data-stu-id="0213f-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="0213f-165">Copiez et collez le code hello ci-dessous tooset hello état HTTP pour introuvable, l’url de base de données hello et url de collection de hello.</span><span class="sxs-lookup"><span data-stu-id="0213f-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="0213f-166">Ces URL est comment client de base de données Azure Cosmos hello trouve hello de base de données à droite et de la collection.</span><span class="sxs-lookup"><span data-stu-id="0213f-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="0213f-167">A [base de données](documentdb-resources.md#databases) peuvent être créés à l’aide de hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) fonction Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="0213f-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="0213f-168">Une base de données est un conteneur logique de hello de stockage de documents partitionné entre des collections.</span><span class="sxs-lookup"><span data-stu-id="0213f-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="0213f-169">Copiez et collez hello **getDatabase** (fonction) pour la création de votre nouvelle base de données dans le fichier app.js hello hello ```id``` spécifié dans hello ```config``` objet.</span><span class="sxs-lookup"><span data-stu-id="0213f-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="0213f-170">Hello fonction vérifiera si hello de base de données avec hello même ```FamilyRegistry``` id n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="0213f-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="0213f-171">Si elle existe, nous allons retourner cette base de données au lieu d’en créer une.</span><span class="sxs-lookup"><span data-stu-id="0213f-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

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

<span data-ttu-id="0213f-172">Copiez et collez code hello ci-dessous lorsque vous définissez hello **getDatabase** fonction fonction d’assistance de hello tooadd **quitter** qui imprime message de sortie hello et appel de hello trop**getDatabase** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

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

<span data-ttu-id="0213f-173">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-174">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-174">Congratulations!</span></span> <span data-ttu-id="0213f-175">Vous avez créé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="0213f-176"><a id="CreateColl"></a>Étape 6 : Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="0213f-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="0213f-177">**CreateDocumentCollectionAsync** crée une collection, ce qui a des conséquences tarifaires.</span><span class="sxs-lookup"><span data-stu-id="0213f-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="0213f-178">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="0213f-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="0213f-179">A [collection](documentdb-resources.md#collections) peuvent être créés à l’aide de hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) fonction Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="0213f-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="0213f-180">Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0213f-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="0213f-181">Copiez et collez hello **getCollection** fonction sous hello **getDatabase** de fonction dans hello app.js fichier toocreate votre nouvelle collection avec hello ```id``` spécifié dans hello ```config```objet.</span><span class="sxs-lookup"><span data-stu-id="0213f-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="0213f-182">Là encore, nous vérifierons toomake vraiment une collection de hello même ```FamilyCollection``` id n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="0213f-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="0213f-183">Si elle existe, nous allons retourner cette collection au lieu d’en créer une.</span><span class="sxs-lookup"><span data-stu-id="0213f-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

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

<span data-ttu-id="0213f-184">Copiez et collez le code hello sous l’appel de hello trop**getDatabase** tooexecute hello **getCollection** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="0213f-185">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-186">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-186">Congratulations!</span></span> <span data-ttu-id="0213f-187">Vous avez créé une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="0213f-188"><a id="CreateDoc"></a>Étape 7 : Création d’un document</span><span class="sxs-lookup"><span data-stu-id="0213f-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="0213f-189">A [document](documentdb-resources.md#documents) peuvent être créés à l’aide de hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) fonction Hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="0213f-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="0213f-190">Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0213f-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="0213f-191">Vous pouvez maintenant insérer un document dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="0213f-192">Copiez et collez hello **getFamilyDocument** fonction sous hello **getCollection** fonction pour créer des documents hello contenant des données JSON hello économisées hello ```config``` objet.</span><span class="sxs-lookup"><span data-stu-id="0213f-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="0213f-193">Là encore, nous allons Vérifiez toomake un document avec hello même id n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="0213f-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

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

<span data-ttu-id="0213f-194">Copiez et collez le code hello sous l’appel de hello trop**getCollection** tooexecute hello **getFamilyDocument** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="0213f-195">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-196">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-196">Congratulations!</span></span> <span data-ttu-id="0213f-197">Vous avez créé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-197">You have successfully created an Azure Cosmos DB document.</span></span>

![La base de données - diagramme illustrant la relation hiérarchique de hello entre le compte de hello, la base de données hello, collection de hello et documents de hello - nœud didacticiel de Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="0213f-199"><a id="Query"></a>Étape 8 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0213f-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="0213f-200">Azure Cosmos DB prend en charge les [requêtes enrichies](documentdb-sql-query.md) sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="0213f-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="0213f-201">Hello exemple de code suivant montre une requête que vous pouvez exécuter par rapport aux documents de hello dans votre collection.</span><span class="sxs-lookup"><span data-stu-id="0213f-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="0213f-202">Copiez et collez hello **queryCollection** fonction sous hello **getFamilyDocument** fonction hello app.js fichier.</span><span class="sxs-lookup"><span data-stu-id="0213f-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="0213f-203">Azure Cosmos DB prend en charge des requêtes similaires à SQL, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0213f-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="0213f-204">Pour plus d’informations sur la création des requêtes complexes, consultez hello [Query Playground](https://www.documentdb.com/sql/demo) et hello [requête documentation](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="0213f-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

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


<span data-ttu-id="0213f-205">Hello suivant le diagramme illustre la requête SQL de base de données Azure Cosmos de hello syntaxe est appelée sur la collection de hello créée.</span><span class="sxs-lookup"><span data-stu-id="0213f-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![La base de données - diagramme illustrant la portée de hello et ce qui signifie que de requête de hello - nœud didacticiel de Node.js](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="0213f-207">Hello [FROM](documentdb-sql-query.md#FromClause) mot clé est facultatif dans la requête de hello, car les requêtes de base de données Azure Cosmos sont déjà incluses dans l’étendue tooa unique collection.</span><span class="sxs-lookup"><span data-stu-id="0213f-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="0213f-208">Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="0213f-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="0213f-209">Base de données Azure Cosmos déduira familles, racine ou le nom de la variable hello choisie, référence hello de collection actuel par défaut.</span><span class="sxs-lookup"><span data-stu-id="0213f-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="0213f-210">Copiez et collez le code hello sous l’appel de hello trop**getFamilyDocument** tooexecute hello **queryCollection** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="0213f-211">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-212">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-212">Congratulations!</span></span> <span data-ttu-id="0213f-213">Vous avez interrogé des documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="0213f-214"><a id="ReplaceDocument"></a>Étape 9 : Remplacement d’un document</span><span class="sxs-lookup"><span data-stu-id="0213f-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="0213f-215">Azure Cosmos DB prend en charge le remplacement des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="0213f-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="0213f-216">Copiez et collez hello **replaceFamilyDocument** fonction sous hello **queryCollection** fonction hello app.js fichier.</span><span class="sxs-lookup"><span data-stu-id="0213f-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

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

<span data-ttu-id="0213f-217">Copiez et collez le code hello sous l’appel de hello trop**queryCollection** tooexecute hello **replaceDocument** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="0213f-218">En outre, ajoutez hello code toocall **queryCollection** encore tooverify document hello avait a été modifié.</span><span class="sxs-lookup"><span data-stu-id="0213f-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="0213f-219">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-220">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-220">Congratulations!</span></span> <span data-ttu-id="0213f-221">Vous avez remplacé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="0213f-222"><a id="DeleteDocument"></a>Étape 10 : Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="0213f-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="0213f-223">Azure Cosmos DB prend en charge la suppression des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="0213f-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="0213f-224">Copiez et collez hello **deleteFamilyDocument** fonction sous hello **replaceFamilyDocument** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

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

<span data-ttu-id="0213f-225">Copiez et collez le code hello ci-dessous hello appel toohello deuxième **queryCollection** tooexecute hello **deleteDocument** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="0213f-226">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-227">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-227">Congratulations!</span></span> <span data-ttu-id="0213f-228">Vous avez supprimé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0213f-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="0213f-229"><a id="DeleteDatabase"></a>Étape 11 : Supprimer la base de données du nœud hello</span><span class="sxs-lookup"><span data-stu-id="0213f-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="0213f-230">Suppression hello créé la base de données supprime de la base de données hello et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="0213f-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="0213f-231">Copiez et collez hello **nettoyage** fonction sous hello **deleteFamilyDocument** fonction de base de données tooremove hello et toutes les ressources enfants de hello.</span><span class="sxs-lookup"><span data-stu-id="0213f-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

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

<span data-ttu-id="0213f-232">Copiez et collez le code hello sous l’appel de hello trop**deleteFamilyDocument** tooexecute hello **nettoyage** (fonction).</span><span class="sxs-lookup"><span data-stu-id="0213f-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="0213f-233"><a id="Run"></a>Étape 12 : Exécution de l’application Node.js</span><span class="sxs-lookup"><span data-stu-id="0213f-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="0213f-234">Complètement, séquence hello pour appeler vos fonctions doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="0213f-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="0213f-235">Dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello :```node app.js```</span><span class="sxs-lookup"><span data-stu-id="0213f-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="0213f-236">Vous devez voir la sortie hello de votre application démarrée get.</span><span class="sxs-lookup"><span data-stu-id="0213f-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="0213f-237">sortie de Hello doit correspondre au texte d’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0213f-237">hello output should match hello example text below.</span></span>

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

<span data-ttu-id="0213f-238">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0213f-238">Congratulations!</span></span> <span data-ttu-id="0213f-239">Créée, vous avez terminé hello Node.js didacticiel et avez votre première application de console de base de données Azure Cosmos !</span><span class="sxs-lookup"><span data-stu-id="0213f-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="0213f-240"><a id="GetSolution"></a>Obtenir complète solution du didacticiel Node.js hello</span><span class="sxs-lookup"><span data-stu-id="0213f-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="0213f-241">Si vous n’avez temps toocomplete hello des étapes de ce didacticiel, ou code de hello toodownload uniquement, vous pouvez l’obtenir à partir de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0213f-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="0213f-242">toorun hello GetStarted solution qui contient tous les exemples hello dans cet article vous serez hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="0213f-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="0213f-243">[Un compte Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="0213f-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="0213f-244">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="0213f-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="0213f-245">Installer hello **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="0213f-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="0213f-246">Utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0213f-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="0213f-247">Ensuite, dans hello ```config.js``` de fichiers, les valeurs mises à jour hello config.endpoint et config.authKey comme décrit dans [étape 3 : définir des configurations de votre application](#Config).</span><span class="sxs-lookup"><span data-stu-id="0213f-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="0213f-248">Puis, dans votre terminal, recherchez votre ```app.js``` de fichiers et d’exécuter la commande hello : ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="0213f-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="0213f-249">Voilà, vous n’avez plus qu’à générer l’élément pour être sur la bonne voie !</span><span class="sxs-lookup"><span data-stu-id="0213f-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0213f-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0213f-250">Next steps</span></span>
* <span data-ttu-id="0213f-251">Vous voulez un exemple de Node.js plus complexe ?</span><span class="sxs-lookup"><span data-stu-id="0213f-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="0213f-252">Consultez [Création d’une application web Node.js avec Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="0213f-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="0213f-253">Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="0213f-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="0213f-254">Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="0213f-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="0213f-255">En savoir plus sur le modèle de programmation hello Bonjour section développer Hello [page de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0213f-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
