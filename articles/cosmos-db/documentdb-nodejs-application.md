---
title: "aaaBuild une application web de Node.js pour la base de données Azure Cosmos | Documents Microsoft"
description: "Ce didacticiel Node.js explore comment toouse données de base de données Microsoft Azure Cosmos toostore et l’accès à partir d’une application web de Node.js Express hébergés sur des sites Web Azure."
keywords: "Développement d’applications, didacticiel de base de données, apprendre node.js, didacticiel node.js"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="495c6-104"><a name="_Toc395783175"></a>Création d’une application web Node.js avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="495c6-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="495c6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="495c6-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="495c6-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="495c6-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="495c6-107">Java</span><span class="sxs-lookup"><span data-stu-id="495c6-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="495c6-108">Python</span><span class="sxs-lookup"><span data-stu-id="495c6-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="495c6-109">Ce didacticiel Node.js vous montre comment toouse base de données Azure Cosmos et hello API DocumentDB toostore et accéder aux données à partir d’une application Node.js Express hébergés sur des sites Web Azure.</span><span class="sxs-lookup"><span data-stu-id="495c6-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="495c6-110">Vous allez créer une simple application web de gestion des tâches, une application ToDo, qui permet de créer, de récupérer et de terminer des tâches.</span><span class="sxs-lookup"><span data-stu-id="495c6-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="495c6-111">tâches de Hello sont stockées sous forme de documents JSON dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="495c6-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="495c6-112">Ce didacticiel vous guide à travers la création de hello et le déploiement de l’application hello et explique ce qui se passe dans chaque extrait de code.</span><span class="sxs-lookup"><span data-stu-id="495c6-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Capture d’écran de hello application ma liste de tâches créée dans ce didacticiel Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="495c6-114">Ne pas avoir didacticiel de temps toocomplete hello et souhaitez solution complète de tooget hello ?</span><span class="sxs-lookup"><span data-stu-id="495c6-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="495c6-115">Pas de problème, vous pouvez obtenir solution exemple complet hello [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="495c6-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="495c6-116">Lire hello [Lisez-moi](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) fichier pour obtenir des instructions sur la façon dont toorun hello application.</span><span class="sxs-lookup"><span data-stu-id="495c6-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="495c6-117"><a name="_Toc395783176"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="495c6-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="495c6-118">Ce didacticiel Node.js part du principe que vous avez déjà utilisé Node.js et Sites Web Azure.</span><span class="sxs-lookup"><span data-stu-id="495c6-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="495c6-119">Avant de suivre les instructions de hello dans cet article, vous devez vous assurer que vous disposez des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="495c6-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="495c6-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="495c6-120">An active Azure account.</span></span> <span data-ttu-id="495c6-121">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="495c6-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="495c6-122">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="495c6-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="495c6-123">OU</span><span class="sxs-lookup"><span data-stu-id="495c6-123">OR</span></span>

   <span data-ttu-id="495c6-124">Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md) (Windows uniquement).</span><span class="sxs-lookup"><span data-stu-id="495c6-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="495c6-125">[Node.js][Node.js] version v0.10.29 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="495c6-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="495c6-126">[Générateur Express](http://www.expressjs.com/starter/generator.html) (installation possible via `npm install express-generator -g`)</span><span class="sxs-lookup"><span data-stu-id="495c6-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="495c6-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="495c6-127">[Git][Git].</span></span>

## <span data-ttu-id="495c6-128"><a name="_Toc395637761"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="495c6-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="495c6-129">Commençons par créer un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="495c6-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="495c6-130">Si vous déjà disposez d’un compte ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[étape 2 : créer une application Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="495c6-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="495c6-131"><a name="_Toc395783178"></a>Étape 2 : création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="495c6-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="495c6-132">Maintenant nous allons en un projet Hello World Node.js base à l’aide de hello savoir toocreate [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="495c6-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="495c6-133">Ouvrez votre terminal favoris, tels que de l’invite de commande Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="495c6-134">Accédez répertoire toohello dans lequel vous souhaitez que nouvelle application de toostore hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="495c6-135">Utilisez hello générateur express toogenerate est une nouvelle application appelée **todo**.</span><span class="sxs-lookup"><span data-stu-id="495c6-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="495c6-136">Ouvrez votre nouveau répertoire **todo** et installez les dépendances.</span><span class="sxs-lookup"><span data-stu-id="495c6-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="495c6-137">Exécutez votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="495c6-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="495c6-138">Vous pouvez afficher votre nouvelle application en accédant via votre navigateur trop[http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="495c6-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![En savoir plus Node.js - capture d’écran de hello application Hello World dans une fenêtre de navigateur](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="495c6-140">Ensuite, toostop hello application, appuyez sur CTRL + C dans la fenêtre de terminal hello, puis sur **y** tooterminate par lots hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="495c6-141"><a name="_Toc395783179"></a>Étape 3 : installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="495c6-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="495c6-142">Hello **package.json** fichier est un des fichiers de hello créés dans racine hello du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="495c6-143">Il contient une liste de modules supplémentaires qui sont nécessaires pour les applications Node.js.</span><span class="sxs-lookup"><span data-stu-id="495c6-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="495c6-144">Ultérieurement, lorsque vous déployez cette tooAzure application des sites Web, ce fichier est utilisé toodetermine le toobe besoin de modules installés sur Azure toosupport votre application.</span><span class="sxs-lookup"><span data-stu-id="495c6-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="495c6-145">Nous devons encore tooinstall deux packages supplémentaires pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="495c6-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="495c6-146">Dans hello Terminal Server, installez hello **async** module via npm.</span><span class="sxs-lookup"><span data-stu-id="495c6-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="495c6-147">Installer hello **documentdb** module via npm.</span><span class="sxs-lookup"><span data-stu-id="495c6-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="495c6-148">Il s’agit de module hello où magique de base de données Azure Cosmos hello tous les cas.</span><span class="sxs-lookup"><span data-stu-id="495c6-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="495c6-149">Une vérification rapide de hello **package.json** fichier de l’application hello doit afficher hello modules supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="495c6-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="495c6-150">Ce fichier sera indiquer à quel toodownload packages Azure et installer lors de l’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="495c6-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="495c6-151">Il doit ressembler à exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="495c6-151">It should resemble hello example below.</span></span>
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    <span data-ttu-id="495c6-152">Ce code indique à Node (et à Azure ultérieurement) que votre application dépend de ces modules supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="495c6-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="495c6-153"><a name="_Toc395783180"></a>Étape 4 : Utilisation de service de base de données Azure Cosmos hello dans une application de nœud</span><span class="sxs-lookup"><span data-stu-id="495c6-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="495c6-154">Qui prend en charge de tous les paramètres initiaux de hello et la configuration, maintenant nous allons get vers le bas toowhy nous sommes là, et qui est toowrite certaines de code à l’aide de la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="495c6-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="495c6-155">Créer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="495c6-155">Create hello model</span></span>
1. <span data-ttu-id="495c6-156">Dans le répertoire du projet hello, créez un nouveau répertoire nommé **modèles** Bonjour même répertoire que le fichier du package.json hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="495c6-157">Bonjour **modèles** répertoire, créez un nouveau fichier nommé **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="495c6-158">Ce fichier contient le modèle hello pour les tâches de hello créées par notre application.</span><span class="sxs-lookup"><span data-stu-id="495c6-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="495c6-159">Dans hello même **modèles** répertoire, créez un autre fichier nommé **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="495c6-160">Ce fichier contient du code utile et réutilisable que nous utiliserons dans notre application.</span><span class="sxs-lookup"><span data-stu-id="495c6-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="495c6-161">Copie hello de code suivant dans trop**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="495c6-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. <span data-ttu-id="495c6-162">Enregistrez et fermez hello **docdbUtils.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="495c6-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="495c6-163">Au début de hello Hello **taskDao.js** , ajoutez hello suivant hello tooreference de code **DocumentDBClient** et hello **docdbUtils.js** créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="495c6-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="495c6-164">Ensuite, vous ajoutez le code toodefine et exporter l’objet de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="495c6-165">Il est responsable de l’initialisation de notre objet de tâche et hello paramétrage de base de données et de la Collection de documents que nous allons utiliser.</span><span class="sxs-lookup"><span data-stu-id="495c6-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="495c6-166">Ensuite, ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="495c6-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. <span data-ttu-id="495c6-167">Enregistrez et fermez hello **taskDao.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="495c6-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="495c6-168">Créer le contrôleur de hello</span><span class="sxs-lookup"><span data-stu-id="495c6-168">Create hello controller</span></span>
1. <span data-ttu-id="495c6-169">Bonjour **itinéraires** répertoire de votre projet, créez un nouveau fichier nommé **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="495c6-170">Ajouter hello suivant code trop**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="495c6-171">Cette opération charge hello DocumentDBClient et async modules qui sont utilisés par **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="495c6-172">Cela défini également hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** définie précédemment l’objet :</span><span class="sxs-lookup"><span data-stu-id="495c6-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="495c6-173">Poursuivre l’ajout de toohello **tasklist.js** fichier en ajoutant des méthodes hello utilisés trop**showTasks, addTask**, et **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="495c6-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. <span data-ttu-id="495c6-174">Enregistrez et fermez hello **tasklist.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="495c6-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="495c6-175">Ajout de config.js</span><span class="sxs-lookup"><span data-stu-id="495c6-175">Add config.js</span></span>
1. <span data-ttu-id="495c6-176">Dans le répertoire de projet, créez un fichier nommé **config.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="495c6-177">Ajouter hello suivant trop**config.js**.</span><span class="sxs-lookup"><span data-stu-id="495c6-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="495c6-178">Définit les paramètres de configuration et les valeurs nécessaires à notre application.</span><span class="sxs-lookup"><span data-stu-id="495c6-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="495c6-179">Bonjour **config.js** de fichiers, valeurs hello de mise à jour de l’hôte et AUTH_KEY à l’aide des valeurs hello dans le panneau de clés hello de votre compte de base de données Azure Cosmos sur hello [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="495c6-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="495c6-180">Enregistrez et fermez hello **config.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="495c6-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="495c6-181">Modification de app.js</span><span class="sxs-lookup"><span data-stu-id="495c6-181">Modify app.js</span></span>
1. <span data-ttu-id="495c6-182">Dans le répertoire du projet hello, ouvrez hello **app.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="495c6-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="495c6-183">Ce fichier a été créé précédemment lors de l’application de web Express hello a été créée.</span><span class="sxs-lookup"><span data-stu-id="495c6-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="495c6-184">Ajouter hello suivant en haut de toohello de code de **app.js**</span><span class="sxs-lookup"><span data-stu-id="495c6-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="495c6-185">Ce code définit hello config fichier toobe utilisé et poursuit tooread les valeurs de ce fichier dans des variables, que nous allons utiliser dès.</span><span class="sxs-lookup"><span data-stu-id="495c6-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="495c6-186">Remplacez hello après deux lignes dans **app.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="495c6-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="495c6-187">avec hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="495c6-187">with hello following snippet:</span></span>
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. <span data-ttu-id="495c6-188">Ces lignes définissent une nouvelle instance de notre **TaskDao** objet, avec un nouveau tooAzure de connexion Cosmos DB (à l’aide des valeurs de hello lire à partir de hello **config.js**), d’initialiser l’objet de tâche hello, puis lier les actions de formulaire toomethods sur notre **TaskList** contrôleur.</span><span class="sxs-lookup"><span data-stu-id="495c6-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="495c6-189">Enfin, enregistrez et fermez hello **app.js** fichier, nous avons presque terminé.</span><span class="sxs-lookup"><span data-stu-id="495c6-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="495c6-190"><a name="_Toc395783181"></a>Étape 5 : création d'une interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="495c6-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="495c6-191">Maintenant nous allons activer notre interface utilisateur de votre attention toobuilding hello pour un utilisateur puisse réellement interagir avec votre application.</span><span class="sxs-lookup"><span data-stu-id="495c6-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="495c6-192">Hello rapide d’application créé utilise **Jade** en tant que moteur d’affichage hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="495c6-193">Pour plus d’informations sur Jade reportez-vous trop[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="495c6-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="495c6-194">Hello **layout.jade** fichier Bonjour **vues** répertoire est utilisé en tant que modèle global pour d’autres **.jade** fichiers.</span><span class="sxs-lookup"><span data-stu-id="495c6-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="495c6-195">Dans cette étape vous modifiera toouse [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement un site Web d’aspect intéressant.</span><span class="sxs-lookup"><span data-stu-id="495c6-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="495c6-196">Ouvrez hello **layout.jade** fichier trouvé dans hello **vues** contenu de hello dossier et le remplacer par hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="495c6-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    <span data-ttu-id="495c6-197">Cela indique en réalité hello **Jade** toorender du moteur du code HTML pour notre application et crée un **bloc** appelé **contenu** où nous puissions fournir la mise en page hello pour notre contenu pages.</span><span class="sxs-lookup"><span data-stu-id="495c6-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="495c6-198">Enregistrez et fermez ce fichier **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="495c6-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="495c6-199">Ouvrez maintenant hello **index.jade** fichier, vue hello qui sera utilisé par notre application et remplacez le contenu du fichier de hello hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="495c6-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

<span data-ttu-id="495c6-200">Cela étend la disposition et fournit du contenu pour hello **contenu** espace réservé que nous avons vu dans hello **layout.jade** fichier précédemment.</span><span class="sxs-lookup"><span data-stu-id="495c6-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="495c6-201">Dans cette mise en page, nous avons créé deux fichiers HTML.</span><span class="sxs-lookup"><span data-stu-id="495c6-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="495c6-202">formulaire de premier Hello contient une table pour nos données et un bouton qui nous permet de tooupdate éléments en publiant trop**/completetask** méthode de notre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="495c6-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="495c6-203">deuxième forme de Hello contient deux champs d’entrée et un bouton qui nous permet de toocreate un nouvel élément en publiant trop**/addtask** méthode de notre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="495c6-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="495c6-204">Il doit s’agir de tout ce dont nous avons besoin pour notre toowork de l’application.</span><span class="sxs-lookup"><span data-stu-id="495c6-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="495c6-205"><a name="_Toc395783181"></a>Étape 6 : exécution locale de l'application</span><span class="sxs-lookup"><span data-stu-id="495c6-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="495c6-206">application de hello tootest sur votre ordinateur local, exécutez `npm start` dans hello toostart terminal de votre application, puis actualisez votre [http://localhost:3000](http://localhost:3000) page du navigateur.</span><span class="sxs-lookup"><span data-stu-id="495c6-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="495c6-207">page de Hello doit maintenant ressembler à image hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="495c6-207">hello page should now look like hello image below:</span></span>
   
    ![Capture d’écran de hello application MyTodo liste dans une fenêtre de navigateur](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="495c6-209">Si vous recevez une erreur sur la mise en retrait hello dans le fichier de layout.jade hello ou hello index.jade, vérifiez que hello deux premières lignes dans les deux fichiers est justifié à gauche, sans espaces.</span><span class="sxs-lookup"><span data-stu-id="495c6-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="495c6-210">S’il existe des espaces avant les deux premières lignes de hello, les supprimer, enregistrer les deux fichiers, puis actualisez votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="495c6-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="495c6-211">Utilisez les champs d’élément, nom de l’élément et catégorie hello tooenter une nouvelle tâche, puis cliquez sur **ajouter un élément**.</span><span class="sxs-lookup"><span data-stu-id="495c6-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="495c6-212">Cette opération permet de créer un document présentant ces propriétés dans Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="495c6-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="495c6-213">page de Hello doit mettre à jour hello toodisplay nouvellement créé élément dans la liste de tâches hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Capture d’écran de l’application hello avec un nouvel élément dans la liste de tâches hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="495c6-215">toocomplete une tâche, cochez simplement la case à cocher hello dans la colonne hello, puis cliquez sur **mettre à jour les tâches**.</span><span class="sxs-lookup"><span data-stu-id="495c6-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="495c6-216">Ce document hello de mises à jour déjà créé.</span><span class="sxs-lookup"><span data-stu-id="495c6-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="495c6-217">application de hello toostop, appuyez sur CTRL + C dans la fenêtre de terminal hello, puis cliquez sur **Y** tooterminate par lots hello.</span><span class="sxs-lookup"><span data-stu-id="495c6-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="495c6-218"><a name="_Toc395783182"></a>Étape 7 : Déployer votre tooAzure de projet de développement application des sites Web</span><span class="sxs-lookup"><span data-stu-id="495c6-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="495c6-219">Si vous ne l'avez pas encore fait, activez un référentiel git pour votre site web Azure.</span><span class="sxs-lookup"><span data-stu-id="495c6-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="495c6-220">Vous trouverez des instructions sur la façon de toodo cela Bonjour [tooAzure de déploiement Git Local du Service d’applications](../app-service-web/app-service-deploy-local-git.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="495c6-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="495c6-221">Ajoutez votre site web Azure en tant que git distant.</span><span class="sxs-lookup"><span data-stu-id="495c6-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="495c6-222">Déployer en envoyant toohello à distance.</span><span class="sxs-lookup"><span data-stu-id="495c6-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="495c6-223">En quelques secondes, git achève la publication de votre application web et lance un navigateur, dans lequel vous pouvez voir votre réalisation exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="495c6-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="495c6-224">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="495c6-224">Congratulations!</span></span> <span data-ttu-id="495c6-225">Vous avez juste créé votre premier Node.js Express Application Web à l’aide de la base de données Azure Cosmos et publié tooAzure sites Web.</span><span class="sxs-lookup"><span data-stu-id="495c6-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="495c6-226">Si vous souhaitez toodownload ou consultez toohello d’application de référence complète pour ce didacticiel, il peut être téléchargé à partir de [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="495c6-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="495c6-227"><a name="_Toc395637775"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="495c6-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="495c6-228">Vous souhaitez tooperform mise à l’échelle et des tests de performances avec la base de données Azure Cosmos ?</span><span class="sxs-lookup"><span data-stu-id="495c6-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="495c6-229">Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="495c6-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="495c6-230">Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="495c6-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="495c6-231">Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="495c6-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="495c6-232">Explorer hello [documentation de base de données Azure Cosmos](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="495c6-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

