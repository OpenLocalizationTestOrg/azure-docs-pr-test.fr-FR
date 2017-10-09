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
# <a name="_Toc395783175"></a>Création d’une application web Node.js avec Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Ce didacticiel Node.js vous montre comment toouse base de données Azure Cosmos et hello API DocumentDB toostore et accéder aux données à partir d’une application Node.js Express hébergés sur des sites Web Azure. Vous allez créer une simple application web de gestion des tâches, une application ToDo, qui permet de créer, de récupérer et de terminer des tâches. tâches de Hello sont stockées sous forme de documents JSON dans la base de données Azure Cosmos. Ce didacticiel vous guide à travers la création de hello et le déploiement de l’application hello et explique ce qui se passe dans chaque extrait de code.

![Capture d’écran de hello application ma liste de tâches créée dans ce didacticiel Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Ne pas avoir didacticiel de temps toocomplete hello et souhaitez solution complète de tooget hello ? Pas de problème, vous pouvez obtenir solution exemple complet hello [GitHub][GitHub]. Lire hello [Lisez-moi](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) fichier pour obtenir des instructions sur la façon dont toorun hello application.

## <a name="_Toc395783176"></a>Configuration requise
> [!TIP]
> Ce didacticiel Node.js part du principe que vous avez déjà utilisé Node.js et Sites Web Azure.
> 
> 

Avant de suivre les instructions de hello dans cet article, vous devez vous assurer que vous disposez des éléments suivants de hello :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).

   OU

   Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md) (Windows uniquement).
* [Node.js][Node.js] version v0.10.29 ou supérieure.
* [Générateur Express](http://www.expressjs.com/starter/generator.html) (installation possible via `npm install express-generator -g`)
* [Git][Git].

## <a name="_Toc395637761"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous déjà disposez d’un compte ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[étape 2 : créer une application Node.js](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Étape 2 : création d’une application Node.js
Maintenant nous allons en un projet Hello World Node.js base à l’aide de hello savoir toocreate [Express](http://expressjs.com/) framework.

1. Ouvrez votre terminal favoris, tels que de l’invite de commande Node.js hello.
2. Accédez répertoire toohello dans lequel vous souhaitez que nouvelle application de toostore hello.
3. Utilisez hello générateur express toogenerate est une nouvelle application appelée **todo**.
   
        express todo
4. Ouvrez votre nouveau répertoire **todo** et installez les dépendances.
   
        cd todo
        npm install
5. Exécutez votre nouvelle application.
   
        npm start
6. Vous pouvez afficher votre nouvelle application en accédant via votre navigateur trop[http://localhost:3000](http://localhost:3000).
   
    ![En savoir plus Node.js - capture d’écran de hello application Hello World dans une fenêtre de navigateur](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Ensuite, toostop hello application, appuyez sur CTRL + C dans la fenêtre de terminal hello, puis sur **y** tooterminate par lots hello.

## <a name="_Toc395783179"></a>Étape 3 : installation de modules supplémentaires
Hello **package.json** fichier est un des fichiers de hello créés dans racine hello du projet de hello. Il contient une liste de modules supplémentaires qui sont nécessaires pour les applications Node.js. Ultérieurement, lorsque vous déployez cette tooAzure application des sites Web, ce fichier est utilisé toodetermine le toobe besoin de modules installés sur Azure toosupport votre application. Nous devons encore tooinstall deux packages supplémentaires pour ce didacticiel.

1. Dans hello Terminal Server, installez hello **async** module via npm.
   
        npm install async --save
2. Installer hello **documentdb** module via npm. Il s’agit de module hello où magique de base de données Azure Cosmos hello tous les cas.
   
        npm install documentdb --save
3. Une vérification rapide de hello **package.json** fichier de l’application hello doit afficher hello modules supplémentaires. Ce fichier sera indiquer à quel toodownload packages Azure et installer lors de l’exécution de votre application. Il doit ressembler à exemple hello ci-dessous.
   
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
   
    Ce code indique à Node (et à Azure ultérieurement) que votre application dépend de ces modules supplémentaires.

## <a name="_Toc395783180"></a>Étape 4 : Utilisation de service de base de données Azure Cosmos hello dans une application de nœud
Qui prend en charge de tous les paramètres initiaux de hello et la configuration, maintenant nous allons get vers le bas toowhy nous sommes là, et qui est toowrite certaines de code à l’aide de la base de données Azure Cosmos.

### <a name="create-hello-model"></a>Créer le modèle de hello
1. Dans le répertoire du projet hello, créez un nouveau répertoire nommé **modèles** Bonjour même répertoire que le fichier du package.json hello.
2. Bonjour **modèles** répertoire, créez un nouveau fichier nommé **taskDao.js**. Ce fichier contient le modèle hello pour les tâches de hello créées par notre application.
3. Dans hello même **modèles** répertoire, créez un autre fichier nommé **docdbUtils.js**. Ce fichier contient du code utile et réutilisable que nous utiliserons dans notre application. 
4. Copie hello de code suivant dans trop**docdbUtils.js**
   
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
   
5. Enregistrez et fermez hello **docdbUtils.js** fichier.
6. Au début de hello Hello **taskDao.js** , ajoutez hello suivant hello tooreference de code **DocumentDBClient** et hello **docdbUtils.js** créée précédemment :
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Ensuite, vous ajoutez le code toodefine et exporter l’objet de tâche hello. Il est responsable de l’initialisation de notre objet de tâche et hello paramétrage de base de données et de la Collection de documents que nous allons utiliser.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Ensuite, ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la base de données Azure Cosmos.
   
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
9. Enregistrez et fermez hello **taskDao.js** fichier. 

### <a name="create-hello-controller"></a>Créer le contrôleur de hello
1. Bonjour **itinéraires** répertoire de votre projet, créez un nouveau fichier nommé **tasklist.js**. 
2. Ajouter hello suivant code trop**tasklist.js**. Cette opération charge hello DocumentDBClient et async modules qui sont utilisés par **tasklist.js**. Cela défini également hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** définie précédemment l’objet :
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Poursuivre l’ajout de toohello **tasklist.js** fichier en ajoutant des méthodes hello utilisés trop**showTasks, addTask**, et **completeTasks**:
   
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
4. Enregistrez et fermez hello **tasklist.js** fichier.

### <a name="add-configjs"></a>Ajout de config.js
1. Dans le répertoire de projet, créez un fichier nommé **config.js**.
2. Ajouter hello suivant trop**config.js**. Définit les paramètres de configuration et les valeurs nécessaires à notre application.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. Bonjour **config.js** de fichiers, valeurs hello de mise à jour de l’hôte et AUTH_KEY à l’aide des valeurs hello dans le panneau de clés hello de votre compte de base de données Azure Cosmos sur hello [portail Microsoft Azure](https://portal.azure.com).
4. Enregistrez et fermez hello **config.js** fichier.

### <a name="modify-appjs"></a>Modification de app.js
1. Dans le répertoire du projet hello, ouvrez hello **app.js** fichier. Ce fichier a été créé précédemment lors de l’application de web Express hello a été créée.
2. Ajouter hello suivant en haut de toohello de code de **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Ce code définit hello config fichier toobe utilisé et poursuit tooread les valeurs de ce fichier dans des variables, que nous allons utiliser dès.
4. Remplacez hello après deux lignes dans **app.js** fichier :
   
        app.use('/', index);
        app.use('/users', users); 
   
      avec hello suivant extrait de code :
   
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
5. Ces lignes définissent une nouvelle instance de notre **TaskDao** objet, avec un nouveau tooAzure de connexion Cosmos DB (à l’aide des valeurs de hello lire à partir de hello **config.js**), d’initialiser l’objet de tâche hello, puis lier les actions de formulaire toomethods sur notre **TaskList** contrôleur. 
6. Enfin, enregistrez et fermez hello **app.js** fichier, nous avons presque terminé.

## <a name="_Toc395783181"></a>Étape 5 : création d'une interface utilisateur
Maintenant nous allons activer notre interface utilisateur de votre attention toobuilding hello pour un utilisateur puisse réellement interagir avec votre application. Hello rapide d’application créé utilise **Jade** en tant que moteur d’affichage hello. Pour plus d’informations sur Jade reportez-vous trop[http://jade-lang.com/](http://jade-lang.com/).

1. Hello **layout.jade** fichier Bonjour **vues** répertoire est utilisé en tant que modèle global pour d’autres **.jade** fichiers. Dans cette étape vous modifiera toouse [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement un site Web d’aspect intéressant. 
2. Ouvrez hello **layout.jade** fichier trouvé dans hello **vues** contenu de hello dossier et le remplacer par hello qui suit :

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

    Cela indique en réalité hello **Jade** toorender du moteur du code HTML pour notre application et crée un **bloc** appelé **contenu** où nous puissions fournir la mise en page hello pour notre contenu pages.

    Enregistrez et fermez ce fichier **layout.jade** .

3. Ouvrez maintenant hello **index.jade** fichier, vue hello qui sera utilisé par notre application et remplacez le contenu du fichier de hello hello par qui suit hello :
   
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
   

Cela étend la disposition et fournit du contenu pour hello **contenu** espace réservé que nous avons vu dans hello **layout.jade** fichier précédemment.
   
Dans cette mise en page, nous avons créé deux fichiers HTML.

formulaire de premier Hello contient une table pour nos données et un bouton qui nous permet de tooupdate éléments en publiant trop**/completetask** méthode de notre contrôleur.
    
deuxième forme de Hello contient deux champs d’entrée et un bouton qui nous permet de toocreate un nouvel élément en publiant trop**/addtask** méthode de notre contrôleur.

Il doit s’agir de tout ce dont nous avons besoin pour notre toowork de l’application.

## <a name="_Toc395783181"></a>Étape 6 : exécution locale de l'application
1. application de hello tootest sur votre ordinateur local, exécutez `npm start` dans hello toostart terminal de votre application, puis actualisez votre [http://localhost:3000](http://localhost:3000) page du navigateur. page de Hello doit maintenant ressembler à image hello ci-dessous :
   
    ![Capture d’écran de hello application MyTodo liste dans une fenêtre de navigateur](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Si vous recevez une erreur sur la mise en retrait hello dans le fichier de layout.jade hello ou hello index.jade, vérifiez que hello deux premières lignes dans les deux fichiers est justifié à gauche, sans espaces. S’il existe des espaces avant les deux premières lignes de hello, les supprimer, enregistrer les deux fichiers, puis actualisez votre navigateur. 

2. Utilisez les champs d’élément, nom de l’élément et catégorie hello tooenter une nouvelle tâche, puis cliquez sur **ajouter un élément**. Cette opération permet de créer un document présentant ces propriétés dans Azure Cosmos DB. 
3. page de Hello doit mettre à jour hello toodisplay nouvellement créé élément dans la liste de tâches hello.
   
    ![Capture d’écran de l’application hello avec un nouvel élément dans la liste de tâches hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete une tâche, cochez simplement la case à cocher hello dans la colonne hello, puis cliquez sur **mettre à jour les tâches**. Ce document hello de mises à jour déjà créé.

5. application de hello toostop, appuyez sur CTRL + C dans la fenêtre de terminal hello, puis cliquez sur **Y** tooterminate par lots hello.

## <a name="_Toc395783182"></a>Étape 7 : Déployer votre tooAzure de projet de développement application des sites Web
1. Si vous ne l'avez pas encore fait, activez un référentiel git pour votre site web Azure. Vous trouverez des instructions sur la façon de toodo cela Bonjour [tooAzure de déploiement Git Local du Service d’applications](../app-service-web/app-service-deploy-local-git.md) rubrique.
2. Ajoutez votre site web Azure en tant que git distant.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Déployer en envoyant toohello à distance.
   
        git push azure master
4. En quelques secondes, git achève la publication de votre application web et lance un navigateur, dans lequel vous pouvez voir votre réalisation exécutée dans Azure.

    Félicitations ! Vous avez juste créé votre premier Node.js Express Application Web à l’aide de la base de données Azure Cosmos et publié tooAzure sites Web.

    Si vous souhaitez toodownload ou consultez toohello d’application de référence complète pour ce didacticiel, il peut être téléchargé à partir de [GitHub][GitHub].

## <a name="_Toc395637775"></a>Étapes suivantes

* Vous souhaitez tooperform mise à l’échelle et des tests de performances avec la base de données Azure Cosmos ? Consultez la page [Test des performances et de la mise à l’échelle avec Azure Cosmos DB](performance-testing.md).
* Découvrez comment trop[surveiller un compte de base de données Azure Cosmos](monitor-accounts.md).
* Exécuter des requêtes dans notre exemple de dataset Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
* Explorer hello [documentation de base de données Azure Cosmos](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

