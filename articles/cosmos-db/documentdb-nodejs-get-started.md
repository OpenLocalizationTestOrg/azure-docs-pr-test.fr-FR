---
title: "Didacticiel Node.js pour l’API DocumentDB d’Azure Cosmos DB | Microsoft Docs"
description: "Un didacticiel Node.js qui crée une base de données Cosmos DB avec l’API DocumentDB."
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
ms.openlocfilehash: 6510e0270bb2efa252a2b2ad40014c5d26b74a81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-tutorial-use-the-documentdb-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="f1630-104">Didacticiel Node.js : utilisez l’API DocumentDB dans Azure Cosmos DB pour créer une application de console Node.js</span><span class="sxs-lookup"><span data-stu-id="f1630-104">Node.js tutorial: Use the DocumentDB API in Azure Cosmos DB to create a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1630-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f1630-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f1630-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f1630-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f1630-107">Node.js pour MongoDB</span><span class="sxs-lookup"><span data-stu-id="f1630-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f1630-108">Node.JS</span><span class="sxs-lookup"><span data-stu-id="f1630-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f1630-109">Java</span><span class="sxs-lookup"><span data-stu-id="f1630-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f1630-110">C++</span><span class="sxs-lookup"><span data-stu-id="f1630-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="f1630-111">Bienvenue dans le didacticiel Node.js pour le Kit de développement logiciel (SDK) Node.js d’Azure Cosmos DB !</span><span class="sxs-lookup"><span data-stu-id="f1630-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="f1630-112">À la fin de ce didacticiel, vous disposerez d’une application de console qui crée et interroge des ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="f1630-113">Nous allons aborder les points suivants :</span><span class="sxs-lookup"><span data-stu-id="f1630-113">We'll cover:</span></span>

* <span data-ttu-id="f1630-114">Création et connexion à un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f1630-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="f1630-115">Configuration de votre application</span><span class="sxs-lookup"><span data-stu-id="f1630-115">Setting up your application</span></span>
* <span data-ttu-id="f1630-116">Création d’une base de données de nœud</span><span class="sxs-lookup"><span data-stu-id="f1630-116">Creating a node database</span></span>
* <span data-ttu-id="f1630-117">Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="f1630-117">Creating a collection</span></span>
* <span data-ttu-id="f1630-118">Création de documents JSON</span><span class="sxs-lookup"><span data-stu-id="f1630-118">Creating JSON documents</span></span>
* <span data-ttu-id="f1630-119">Interrogation de la collection</span><span class="sxs-lookup"><span data-stu-id="f1630-119">Querying the collection</span></span>
* <span data-ttu-id="f1630-120">Remplacement d'un document</span><span class="sxs-lookup"><span data-stu-id="f1630-120">Replacing a document</span></span>
* <span data-ttu-id="f1630-121">Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="f1630-121">Deleting a document</span></span>
* <span data-ttu-id="f1630-122">Suppression de la base de données du nœud</span><span class="sxs-lookup"><span data-stu-id="f1630-122">Deleting the node database</span></span>

<span data-ttu-id="f1630-123">Vous n’avez pas le temps ?</span><span class="sxs-lookup"><span data-stu-id="f1630-123">Don't have time?</span></span> <span data-ttu-id="f1630-124">Ne vous inquiétez pas !</span><span class="sxs-lookup"><span data-stu-id="f1630-124">Don't worry!</span></span> <span data-ttu-id="f1630-125">La solution complète est disponible sur [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f1630-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="f1630-126">Pour obtenir des instructions rapides, consultez [Obtenir la solution complète](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="f1630-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="f1630-127">Une fois que vous avez terminé le didacticiel Node.js, utilisez les boutons de vote en haut et en bas de cette page pour nous faire part de vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="f1630-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="f1630-128">Si vous souhaitez que nous vous contactions directement, n’hésitez pas à inclure votre adresse de messagerie dans vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="f1630-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="f1630-129">Commençons dès maintenant !</span><span class="sxs-lookup"><span data-stu-id="f1630-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="f1630-130">Configuration requise pour le didacticiel Node.js</span><span class="sxs-lookup"><span data-stu-id="f1630-130">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="f1630-131">Vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f1630-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="f1630-132">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="f1630-132">An active Azure account.</span></span> <span data-ttu-id="f1630-133">Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit des services Azure](https://azure.microsoft.com/pricing/free-trial/)dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="f1630-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="f1630-134">Vous pouvez également utiliser [l’émulateur Azure Cosmos DB](local-emulator.md) pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f1630-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="f1630-135">[Node.js](https://nodejs.org/) version v0.10.29 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="f1630-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f1630-136">Étape 1 : créer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f1630-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f1630-137">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f1630-138">Si vous avez déjà un compte que vous souhaitez utiliser, vous pouvez passer directement à l’étape [Configurer votre application Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f1630-138">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="f1630-139">Si vous utilisez l’émulateur Azure Cosmos DB, suivez les étapes de la section [Émulateur Azure Cosmos DB](local-emulator.md) pour le configurer, puis passez directement à l’étape [Configurer votre application Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="f1630-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f1630-140"><a id="SetupNode"></a>Étape 2 : configurer votre application Node.js</span><span class="sxs-lookup"><span data-stu-id="f1630-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="f1630-141">Ouvrez votre terminal préféré.</span><span class="sxs-lookup"><span data-stu-id="f1630-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="f1630-142">Recherchez le dossier ou le répertoire où vous souhaitez enregistrer votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="f1630-142">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="f1630-143">Créez deux fichiers JavaScript vides avec les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1630-143">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="f1630-144">Windows :</span><span class="sxs-lookup"><span data-stu-id="f1630-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="f1630-145">Linux/OS X :</span><span class="sxs-lookup"><span data-stu-id="f1630-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="f1630-146">Installez le module documentdb via npm.</span><span class="sxs-lookup"><span data-stu-id="f1630-146">Install the documentdb module via npm.</span></span> <span data-ttu-id="f1630-147">Utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1630-147">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="f1630-148">Parfait !</span><span class="sxs-lookup"><span data-stu-id="f1630-148">Great!</span></span> <span data-ttu-id="f1630-149">Vous avez terminé l’installation, nous pouvons donc passer à l’écriture du code.</span><span class="sxs-lookup"><span data-stu-id="f1630-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="f1630-150"><a id="Config"></a>Étape 3 : définir les configurations de votre application</span><span class="sxs-lookup"><span data-stu-id="f1630-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="f1630-151">Ouvrez ```config.js``` dans l’éditeur de texte de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f1630-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="f1630-152">Puis, copiez et collez l’extrait de code ci-dessous et attribuez aux propriétés ```config.endpoint``` et ```config.primaryKey``` l’URI de votre point de terminaison Azure Cosmos DB et votre clé primaire.</span><span class="sxs-lookup"><span data-stu-id="f1630-152">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="f1630-153">Ces deux configurations se trouvent dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f1630-153">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![Didacticiel Node.js : capture d’écran du portail Azure, présentant un compte Azure Cosmos DB, avec le hub ACTIF et le bouton CLÉS mis en surbrillance dans le panneau du compte Azure Cosmos DB, et les valeurs d’URI, de CLÉ PRIMAIRE et de CLÉ SECONDAIRE mises en surbrillance dans le panneau Clés - Base de données de nœud][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="f1630-155">Copiez et collez ```database id```, ```collection id``` et ```JSON documents``` dans votre objet ```config``` ci-dessous, où vous avez défini vos propriétés ```config.endpoint``` et ```config.authKey```.</span><span class="sxs-lookup"><span data-stu-id="f1630-155">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="f1630-156">Si vous disposez déjà de données que vous souhaitez stocker dans votre base de données, vous pouvez utiliser [l’outil de migration de données](import-data.md) d’Azure Cosmos DB au lieu d’ajouter les définitions de document.</span><span class="sxs-lookup"><span data-stu-id="f1630-156">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="f1630-157">Les définitions de base de données, de collection et de document vous servent de ```database id```, de ```collection id``` et de données de documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-157">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="f1630-158">Enfin, exportez votre objet ```config``` pour pouvoir y faire référence dans le fichier ```app.js```.</span><span class="sxs-lookup"><span data-stu-id="f1630-158">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <span data-ttu-id="f1630-159"><a id="Connect"></a> Étape 4 : se connecter à un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f1630-159"><a id="Connect"></a> Step 4: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="f1630-160">Ouvrez votre fichier ```app.js``` vide dans l’éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="f1630-160">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="f1630-161">Copiez et collez le code ci-dessous pour importer le module ```documentdb``` et le module ```config``` que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="f1630-161">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="f1630-162">Copiez et collez le code pour utiliser l’élément ```config.endpoint``` déjà enregistré et ```config.primaryKey``` pour créer un DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="f1630-162">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="f1630-163">Maintenant que vous avez le code permettant d’initialiser le client Azure Cosmos DB, voyons comment utiliser les ressources Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-163">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="f1630-164">Étape 5 : Création d’une base de données de nœud</span><span class="sxs-lookup"><span data-stu-id="f1630-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="f1630-165">Copiez et collez le code ci-dessous pour définir l’état HTTP correspondant à Non trouvé, l’URL de la base de données et l’URL de la collection.</span><span class="sxs-lookup"><span data-stu-id="f1630-165">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="f1630-166">Le client Azure Cosmos DB utilise ces URL pour trouver la base de données et la collection appropriées.</span><span class="sxs-lookup"><span data-stu-id="f1630-166">These urls are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="f1630-167">Vous pouvez créer une [base de données](documentdb-resources.md#databases) à l’aide de la fonction [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f1630-167">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f1630-168">Une base de données est le conteneur logique de stockage de documents partitionné entre les collections.</span><span class="sxs-lookup"><span data-stu-id="f1630-168">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="f1630-169">Copiez et collez la fonction **getDatabase** pour créer votre base de données dans le fichier app.js avec l’élément ```config``` spécifié dans l’objet ```id```.</span><span class="sxs-lookup"><span data-stu-id="f1630-169">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="f1630-170">La fonction vérifie qu’il existe aucune base de données ayant l’ID ```FamilyRegistry``` .</span><span class="sxs-lookup"><span data-stu-id="f1630-170">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="f1630-171">Si elle existe, nous allons retourner cette base de données au lieu d’en créer une.</span><span class="sxs-lookup"><span data-stu-id="f1630-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f1630-172">Copiez et collez le code suivant où vous avez défini la fonction **getDatabase** pour ajouter la fonction d’assistance **exit** qui imprime le message de sortie et l’appel à la fonction **getDatabase**.</span><span class="sxs-lookup"><span data-stu-id="f1630-172">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f1630-173">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-173">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-174">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-174">Congratulations!</span></span> <span data-ttu-id="f1630-175">Vous avez créé une base de données Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="f1630-176"><a id="CreateColl"></a>Étape 6 : Création d’une collection</span><span class="sxs-lookup"><span data-stu-id="f1630-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="f1630-177">**CreateDocumentCollectionAsync** crée une collection, ce qui a des conséquences tarifaires.</span><span class="sxs-lookup"><span data-stu-id="f1630-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="f1630-178">Pour plus d'informations, visitez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f1630-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="f1630-179">Vous pouvez créer une [collection](documentdb-resources.md#collections) à l’aide de la fonction [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f1630-179">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f1630-180">Une collection est un conteneur de documents JSON. Elle est associée à une logique d'application JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f1630-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="f1630-181">Dans le fichier app.js, copiez et collez la fonction **getCollection** sous la fonction **getDatabase** pour créer votre collection avec l’élément ```id``` spécifié dans l’objet ```config```.</span><span class="sxs-lookup"><span data-stu-id="f1630-181">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="f1630-182">Là encore, nous allons nous assurer qu’il n’existe aucune collection avec l’ID ```FamilyCollection``` .</span><span class="sxs-lookup"><span data-stu-id="f1630-182">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="f1630-183">Si elle existe, nous allons retourner cette collection au lieu d’en créer une.</span><span class="sxs-lookup"><span data-stu-id="f1630-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f1630-184">Copiez et collez le code sous l’appel à **getDatabase** pour exécuter la fonction **getCollection**.</span><span class="sxs-lookup"><span data-stu-id="f1630-184">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f1630-185">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-185">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-186">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-186">Congratulations!</span></span> <span data-ttu-id="f1630-187">Vous avez créé une collection Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="f1630-188"><a id="CreateDoc"></a>Étape 7 : Création d’un document</span><span class="sxs-lookup"><span data-stu-id="f1630-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="f1630-189">Vous pouvez créer un [document](documentdb-resources.md#documents) à l’aide de la fonction [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) de la classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f1630-189">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="f1630-190">Les documents correspondent à du contenu JSON (arbitraire) défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f1630-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f1630-191">Vous pouvez maintenant insérer un document dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="f1630-192">Copiez et collez la fonction **getFamilyDocument** sous la fonction **getCollection** pour créer les documents contenant les données JSON enregistrées dans l’objet ```config```.</span><span class="sxs-lookup"><span data-stu-id="f1630-192">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="f1630-193">Là encore, nous allons nous assurer qu’un document avec le même ID n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="f1630-193">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f1630-194">Copiez et collez le code situé sous l’appel à **getCollection** pour exécuter la fonction **getFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="f1630-194">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f1630-195">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-195">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-196">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-196">Congratulations!</span></span> <span data-ttu-id="f1630-197">Vous avez créé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Didacticiel Node.js : diagramme illustrant la relation hiérarchique existant entre le compte, la base de données, la collection et les documents - Base de données de nœud](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="f1630-199"><a id="Query"></a>Étape 8 : interroger les ressources Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f1630-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f1630-200">Azure Cosmos DB prend en charge les [requêtes enrichies](documentdb-sql-query.md) sur les documents JSON stockés dans chaque collection.</span><span class="sxs-lookup"><span data-stu-id="f1630-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="f1630-201">L’exemple de code suivant illustre une requête que vous pouvez exécuter sur les documents dans votre collection.</span><span class="sxs-lookup"><span data-stu-id="f1630-201">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="f1630-202">Copiez et collez la fonction **queryCollection** sous la fonction **getFamilyDocument** dans le fichier app.js.</span><span class="sxs-lookup"><span data-stu-id="f1630-202">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="f1630-203">Azure Cosmos DB prend en charge des requêtes similaires à SQL, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f1630-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="f1630-204">Pour plus d’informations sur la création de requêtes complexes, consultez [Query Playground](https://www.documentdb.com/sql/demo) et la [documentation relative aux requêtes](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="f1630-204">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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


<span data-ttu-id="f1630-205">Le schéma suivant montre comment la syntaxe de requête SQL d’Azure Cosmos DB est appelée sur la collection que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="f1630-205">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![Didacticiel Node.js : diagramme illustrant l’étendue et la signification de la requête - Base de données de nœud](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="f1630-207">Le mot clé [FROM](documentdb-sql-query.md#FromClause) est facultatif dans la requête, car les requêtes Azure Cosmos DB sont déjà étendues à une collection unique.</span><span class="sxs-lookup"><span data-stu-id="f1630-207">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="f1630-208">Par conséquent, « FROM Families f » peut être remplacé par «FROM root r » ou par tout autre nom de variable que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="f1630-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="f1630-209">Azure Cosmos DB déduit alors que Families, root ou le nom de variable choisi fait par défaut référence à la collection actuelle.</span><span class="sxs-lookup"><span data-stu-id="f1630-209">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="f1630-210">Copiez et collez le code sous l’appel à **getFamilyDocument** pour exécuter la fonction **queryCollection**.</span><span class="sxs-lookup"><span data-stu-id="f1630-210">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f1630-211">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-211">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-212">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-212">Congratulations!</span></span> <span data-ttu-id="f1630-213">Vous avez interrogé des documents Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="f1630-214"><a id="ReplaceDocument"></a>Étape 9 : Remplacement d’un document</span><span class="sxs-lookup"><span data-stu-id="f1630-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="f1630-215">Azure Cosmos DB prend en charge le remplacement des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="f1630-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="f1630-216">Copiez et collez la fonction **replaceFamilyDocument** sous la fonction **queryCollection** dans le fichier app.js.</span><span class="sxs-lookup"><span data-stu-id="f1630-216">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f1630-217">Copiez et collez le code sous l’appel à **queryCollection** pour exécuter la fonction **replaceDocument**.</span><span class="sxs-lookup"><span data-stu-id="f1630-217">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="f1630-218">De plus, ajoutez le code permettant d’appeler **queryCollection** à nouveau pour vérifier que le document a bien été modifié.</span><span class="sxs-lookup"><span data-stu-id="f1630-218">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f1630-219">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-219">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-220">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-220">Congratulations!</span></span> <span data-ttu-id="f1630-221">Vous avez remplacé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f1630-222"><a id="DeleteDocument"></a>Étape 10 : Suppression d’un document</span><span class="sxs-lookup"><span data-stu-id="f1630-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="f1630-223">Azure Cosmos DB prend en charge la suppression des documents JSON.</span><span class="sxs-lookup"><span data-stu-id="f1630-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="f1630-224">Copiez et collez la fonction **deleteFamilyDocument** sous la fonction **replaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="f1630-224">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="f1630-225">Copiez et collez le code sous l’appel à la deuxième fonction **queryCollection** pour exécuter la fonction **deleteDocument**.</span><span class="sxs-lookup"><span data-stu-id="f1630-225">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f1630-226">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-226">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-227">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-227">Congratulations!</span></span> <span data-ttu-id="f1630-228">Vous avez supprimé un document Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f1630-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f1630-229"><a id="DeleteDatabase"></a>Étape 11 : Suppression de la base de données de nœud</span><span class="sxs-lookup"><span data-stu-id="f1630-229"><a id="DeleteDatabase"></a>Step 11: Delete the Node database</span></span>
<span data-ttu-id="f1630-230">Supprimer la base de données créée revient à supprimer la base de données et toutes les ressources enfants (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="f1630-230">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="f1630-231">Copiez et collez la fonction **cleanup** sous la fonction **deleteFamilyDocument** pour supprimer la base de données et toutes ses ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="f1630-231">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="f1630-232">Copiez et collez le code sous l’appel à la fonction **deleteFamilyDocument** pour exécuter la fonction **cleanup**.</span><span class="sxs-lookup"><span data-stu-id="f1630-232">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="f1630-233"><a id="Run"></a>Étape 12 : Exécution de l’application Node.js</span><span class="sxs-lookup"><span data-stu-id="f1630-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="f1630-234">La séquence permettant d’appeler vos fonctions doit être similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="f1630-234">Altogether, the sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="f1630-235">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande : ```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f1630-235">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="f1630-236">La sortie de votre application de prise en main doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="f1630-236">You should see the output of your get started app.</span></span> <span data-ttu-id="f1630-237">La sortie doit correspondre au texte en exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f1630-237">The output should match the example text below.</span></span>

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
    Press any key to exit

<span data-ttu-id="f1630-238">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="f1630-238">Congratulations!</span></span> <span data-ttu-id="f1630-239">Vous avez créé et terminé le didacticiel Node.js et disposez à présent de votre première application de console Azure Cosmos DB !</span><span class="sxs-lookup"><span data-stu-id="f1630-239">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="f1630-240"><a id="GetSolution"></a>Obtenir la solution complète du didacticiel Node.js</span><span class="sxs-lookup"><span data-stu-id="f1630-240"><a id="GetSolution"></a>Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="f1630-241">Si vous n’avez pas le temps de suivre les étapes de ce didacticiel, ou que vous voulez simplement télécharger le code, vous pouvez l’obtenir à partir de [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f1630-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="f1630-242">Pour exécuter la solution GetStarted qui contient tous les exemples de cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f1630-242">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="f1630-243">[Un compte Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="f1630-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="f1630-244">La solution [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="f1630-244">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="f1630-245">Installez le module **documentdb** via npm.</span><span class="sxs-lookup"><span data-stu-id="f1630-245">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="f1630-246">Utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1630-246">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="f1630-247">Ensuite, dans le fichier ```config.js```, mettez à jour les valeurs de config.endpoint et de config.authKey, comme indiqué à l’[étape 3 : Définition des configurations de votre application](#Config).</span><span class="sxs-lookup"><span data-stu-id="f1630-247">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="f1630-248">Sur votre terminal, recherchez votre fichier ```app.js``` et exécutez la commande suivante : ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="f1630-248">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="f1630-249">Voilà, vous n’avez plus qu’à générer l’élément pour être sur la bonne voie !</span><span class="sxs-lookup"><span data-stu-id="f1630-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f1630-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1630-250">Next steps</span></span>
* <span data-ttu-id="f1630-251">Vous voulez un exemple de Node.js plus complexe ?</span><span class="sxs-lookup"><span data-stu-id="f1630-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="f1630-252">Consultez [Création d’une application web Node.js avec Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="f1630-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="f1630-253">Découvrez comment [surveiller un compte Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f1630-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f1630-254">Exécutez des requêtes sur notre exemple de dataset dans le [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f1630-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f1630-255">Consultez la section Developer (Développeur) de la [page de documentation Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/) pour découvrir plus en détail le modèle de programmation.</span><span class="sxs-lookup"><span data-stu-id="f1630-255">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
