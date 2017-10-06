---
title: "aaaNode.js hello Service de Table Azure à l’aide de l’application web"
description: "Ce didacticiel vous apprend comment toouse hello Azure Table service toostore des données à partir d’une application Node.js qui est hébergée dans Azure App Service Web Apps."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Application web Node.js à l’aide de hello Service de Table Azure
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment les service de Table toouse fournie par la gestion des données Azure toostore et accéder aux données à partir d’un [nœud] application hébergée dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) les applications Web. Ce didacticiel part du principe que vous avez déjà une certaine expérience en tant qu'utilisateur des applications node et de [Git]

Vous apprendrez à effectuer les opérations suivantes :

* Comment toouse npm (Gestionnaire de package de nœud) tooinstall hello les modules de nœud
* Comment toowork avec hello service Table Azure
* Comment toouse hello CLI d’Azure toocreate une application web.

Dans ce didacticiel, vous allez concevoir une application web simple qui permet de créer, récupérer et finaliser des tâches. tâches de Hello sont stockées dans hello service de Table.

Voici une application hello terminée :

![Une page Web avec une liste de tâches vide][node-table-finished]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="prerequisites"></a>Composants requis
Avant de suivre les instructions de hello dans cet article, assurez-vous d’avoir installé des éléments suivants hello :

* [nœud] version 0.10.24 ou supérieure
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Créez un compte de stockage.
Créez un compte de stockage Azure. application Hello utilisera cette éléments de hello toostore compte d’action.

1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).
2. Cliquez sur hello **nouveau** icône sous hello à gauche du portail de hello, puis cliquez sur **données + stockage** > **stockage**. Donnez un nom unique à compte de stockage hello et créer un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md) pour celle-ci.
   
      ![Bouton Nouveau](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Lorsque le compte de stockage hello a été créé, hello **Notifications** un vert clignote en bouton **réussite** et panneau du compte de stockage hello est ouvert tooshow qu’il appartient toohello nouvelle ressource groupe que vous avez créé.
3. Dans le panneau de hello compte de stockage, cliquez sur **paramètres** > **clés**. Copiez le Presse-papiers de toohello clé d’accès primaire hello.
   
    ![Clé d’accès][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Installation des modules et création de la structure
Dans cette section vous créez une nouvelle application de nœud et utiliser les packages de module tooadd npm. Pour cette application, vous allez utiliser hello [Express] et [Azure] modules. module de Express Hello fournit une infrastructure de modèle-Vue-contrôleur pour le nœud, hello lors de modules Azure fournit le service de connectivité toohello Table.

### <a name="install-express-and-generate-scaffolding"></a>Installation express et création de la structure
1. À partir de la ligne de commande hello, créer un nouveau répertoire nommé **tasklist** et commutateur toothat active.  
2. Entrez hello suivant le module de commande tooinstall hello Express.
   
        npm install express-generator@4.2.0 -g
   
    En fonction du système d’exploitation de hello, vous devrez peut-être tooput « sudo » avant la commande hello :
   
        sudo npm install express-generator@4.2.0 -g
   
    sortie de Hello apparaît toohello similaire, l’exemple suivant :
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Hello '-g' paramètre installe le module de hello globalement. De cette façon, nous pouvons utiliser **express** toogenerate web application génération de modèles automatique sans avoir tootype dans les informations de chemin d’accès supplémentaire.
   > 
   > 
3. génération de modèles automatique pour une application hello, hello toocreate entrez hello **express** commande :
   
        express
   
    sortie Hello de cette commande s’affiche comme toohello l’exemple suivant :
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    Vous avez maintenant plusieurs nouveaux répertoires et fichiers Bonjour **tasklist** active.

### <a name="install-additional-modules"></a>Installation de modules supplémentaires
Un des hello fichiers **express** crée est **package.json**. Ce fichier contient une liste de dépendances de module. Plus tard, lorsque vous déployez hello application tooApp Service Web Apps, ce fichier détermine quels modules doivent toobe installé sur Azure.

À partir de hello de ligne de commande, entrez hello suivant des modules de hello tooinstall de commande décrites dans hello **package.json** fichier. Vous devrez peut-être toouse « sudo ».

    npm install

sortie Hello de cette commande s’affiche comme toohello l’exemple suivant :

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Ensuite, entrez hello suivant commande tooinstall hello [azure], [uuid de nœud], [nconf] et [async] modules :

    npm install azure-storage node-uuid async nconf --save

Hello **--enregistrer** indicateur ajoute des entrées pour ces modules de toohello **package.json** fichier.

sortie Hello de cette commande s’affiche comme toohello l’exemple suivant :

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Créer l’application hello
Nous sommes maintenant application hello de toobuild prêt.

### <a name="create-a-model"></a>Création d’un modèle
A *modèle* est un objet qui représente les données de salutation dans votre application. Pour l’application hello, modèle uniquement de hello est un objet de tâche, qui représente un élément dans la liste des tâches de hello. Tâches aura hello champs qui suivent :

* PartitionKey
* RowKey
* nom (chaîne)
* catégorie (chaîne)
* terminé (booléen)

**PartitionKey** et **RowKey** sont utilisés par hello Service de Table en tant que clés de table. Pour plus d’informations, consultez [modèle de données du Service de Table présentation hello](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. Bonjour **tasklist** répertoire, créez un nouveau répertoire nommé **modèles**.
2. Bonjour **modèles** répertoire, créez un nouveau fichier nommé **task.js**. Ce fichier contient le modèle hello pour les tâches hello créés par votre application.
3. Au début de hello Hello **task.js** , ajoutez hello suivant tooreference requise des bibliothèques de code :
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Ajouter suivant de hello toodefine de code et d’exporter l’objet de tâche hello. Cet objet est chargé de connecter toohello table.
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. Ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la table de hello :
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. Enregistrez et fermez hello **task.js** fichier.

### <a name="create-a-controller"></a>Création d’un contrôleur
A *contrôleur* gère les requêtes HTTP et restitue la réponse de hello HTML.

1. Bonjour **tasklist/itinéraires** répertoire, créez un nouveau fichier nommé **tasklist.js** et ouvrez-le dans un éditeur de texte.
2. Ajouter hello suivant code trop**tasklist.js**. Cette opération charge hello azure et async modules qui sont utilisés par **tasklist.js**. Il définit également hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** définie précédemment l’objet :
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Définissez un objet **TaskList** .
   
        function TaskList(task) {
          this.task = task;
        }
4. Ajouter hello méthodes suivantes trop**TaskList**:
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a>Modification de app.js
1. À partir de hello **tasklist** répertoire, ouvrez hello **app.js** fichier. Ce fichier a été créé précédemment en exécutant hello **express** commande.
2. Au début de hello du fichier de hello, ajoutez hello suivant tooload hello azure module, nom de la table ensemble hello, clé de partition et informations d’identification du stockage ensemble hello utilisées par cet exemple :
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf charge les valeurs de configuration hello des variables d’environnement ou hello **config.json** fichier, nous allons créer plus tard.
   > 
   > 
3. Dans le fichier de app.js hello, faites défiler toowhere vous consultez hello après la ligne :
   
        app.use('/', routes);
        app.use('/users', users);
   
    Remplacez hello au-dessus des lignes de code hello indiqué ci-dessous. Sera initialisé une instance de <strong>tâche</strong> avec un compte de stockage de tooyour de connexion. Il est passé toohello <strong>TaskList</strong>, qui utilisera toocommunicate avec hello service de Table :
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Enregistrer hello **app.js** fichier.

### <a name="modify-hello-index-view"></a>Modifier la vue d’index hello
1. Ouvrez hello **tasklist/views/index.jade** fichier dans un éditeur de texte.
2. Remplacez hello tout contenu de fichier de hello hello suivant de code. Ceci définit une vue qui affiche les tâches et comprend un formulaire permettant d’ajouter des tâches et de les marquer comme terminées.
   
        extends layout
   
        block content
          h1= title
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
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. Fermez et enregistrez le fichier **index.jade** .

### <a name="modify-hello-global-layout"></a>Modifier la disposition globale de hello
Hello **layout.jade** fichier Bonjour **vues** active est un modèle global pour d’autres **.jade** fichiers. Dans cette étape vous modifiera toouse [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement une application web d’aspect intéressant.

Téléchargez et extrayez les fichiers hello pour [amorçage de Twitter](http://getbootstrap.com/). Hello de copie **bootstrap.min.css** fichier hello Bootstrap **css** dossier hello **public/feuilles de style** répertoire de votre application.

À partir de hello **vues** dossier, ouvrez **layout.jade** et remplacez le contenu entier de hello par qui suit hello :

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a>Création d’un fichier de configuration
application hello toorun localement, nous allons présenter des informations d’identification de stockage Azure dans un fichier de configuration. Créez un fichier nommé **config.json* * avec hello suivant JSON :

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Remplacez **nom de compte de stockage** avec nom hello du stockage de hello compte que vous avez créé précédemment, puis remplacez **clé d’accès** avec la clé d’accès primaire hello pour votre compte de stockage. Par exemple :

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Enregistrez ce fichier *supérieurs d’un répertoire* à hello **tasklist** répertoire, comme suit :

    parent/
      |-- config.json
      |-- tasklist/

Hello cela fait tooavoid vérification du fichier de configuration hello dans le contrôle de code source, où il risque de devenir public. Lors du déploiement de hello application tooAzure, nous allons utiliser des variables d’environnement au lieu d’un fichier de configuration.

## <a name="run-hello-application-locally"></a>Exécutez hello application localement
application de hello tootest sur votre ordinateur local, procédez hello comme suit :

1. Hello de ligne de commande, de modifier répertoires toohello **tasklist** active.
2. Utilisez hello suite commande toolaunch application hello localement :
   
        npm start
3. Ouvrez un navigateur web et accédez toohttp://127.0.0.1:3000.
   
    Un toohello similaire de page web exemple suivant s’affiche.
   
    ![Une page Web affiche une liste de tâches vide.][node-table-finished]
4. toocreate un nouvel élément de tâche, entrez un nom et une catégorie, puis cliquez sur **ajouter un élément**. 
5. toomark une tâche comme étant terminée, vérifiez **Complete** et cliquez sur **des tâches de mise à jour**.
   
    ![Une image de hello un nouvel élément dans la liste de hello de tâches][node-table-list-items]

Bien que l’application hello s’exécute localement, il stocke des données de hello Bonjour service Table Azure.

## <a name="deploy-your-application-tooazure"></a>Déployer votre application tooAzure
étapes Hello dans cette section utilisent toocreate des outils de ligne de commande Azure hello une application web dans le Service d’application, puis utilisent Git toodeploy votre application. tooperform ces étapes, vous devez avoir un abonnement Azure.

> [!NOTE]
> Ces étapes peuvent également être effectuées à l’aide de hello [Azure Portal](https://portal.azure.com/). Consultez [Créer et déployer une application web Node.js dans Azure App Service].
> 
> Si c’est la première application web hello, que vous avez créé, vous devez utiliser cette application hello Azure Portal toodeploy.
> 
> 

tooget démarré, installez hello [CLI d’Azure] en entrant la commande suivante à partir de la ligne de commande hello de hello :

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importation de paramètres de publication
Dans cette étape, vous allez télécharger un fichier contenant des informations sur votre abonnement.

1. Entrez hello de commande suivante :
   
        azure login
   
    Cette commande lance un navigateur et navigue page de téléchargement toohello. Si vous y êtes invité, connectez-vous avec le compte de hello associé à votre abonnement Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    téléchargement du fichier Hello commence automatiquement ; Si elle n’est pas le cas, vous pouvez cliquer sur lien hello au début de hello hello toomanually téléchargement hello du fichier de page. Enregistrez hello fichier et notez hello chemin d’accès.
2. Entrez hello suivant les paramètres de commande tooimport hello :
   
        azure account import <path-to-file>
   
    Spécifiez hello chemin d’accès et le nom de publication du fichier de paramètres que vous avez téléchargé à l’étape précédente de hello de hello.
3. Après avoir importé les paramètres de hello, hello de supprimer le fichier de paramètres de publication. Ce fichier n’est plus nécessaire, et il contient des informations sensibles concernant votre abonnement Azure.

### <a name="create-an-app-service-web-app"></a>Créer une application web App Service
1. Hello de ligne de commande, de modifier répertoires toohello **tasklist** active.
2. Utilisez hello suivant commande toocreate une application web.
   
        azure site create --git
   
    Vous devez pour l’emplacement et le nom de l’application web hello. Fournissez un nom unique et sélectionnez hello même emplacement géographique que votre compte de stockage Azure.
   
    Hello `--git` paramètre crée un référentiel Git sur Azure pour cette application web. Elle initialise également un référentiel Git dans le répertoire en cours de hello si aucune n’existe et ajoute un [Git remote] nommé « azure », qui est utilisé toopublish hello application tooAzure. Enfin, il crée un **web.config** fichier, qui contient les paramètres utilisés par les applications de nœud Azure toohost. Si vous omettez hello `--git` paramètre mais hello répertoire contient un référentiel Git, commande hello crée toujours à distance de hello 'azure'.
   
    Une fois cette commande terminée, vous verrez suivant toohello similaire de sortie. Notez qu’à partir à la ligne hello avec **site Web créé à** contient l’URL de hello pour l’application web de hello.
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > S’il s’agit de hello première application du Service d’applications web pour votre abonnement, vous sera demandé toouse hello Azure Portal toocreate hello web app. Pour plus d’informations, consultez la page [Créer et déployer une application web Node.js dans Azure App Service].
   > 
   > 

### <a name="set-environment-variables"></a>Définition des variables d'environnement
Dans cette étape, vous allez ajouter la configuration de l’application web tooyour variables environnement sur Azure.
À partir de la ligne de commande hello, entrez suivante de hello :

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Remplacez  **<storage account name>**  avec nom hello du stockage de hello compte que vous avez créé précédemment, puis remplacez  **<storage access key>**  avec la clé d’accès primaire hello pour votre compte de stockage. (Utilisez hello mêmes valeurs en tant que fichier config.json hello que vous avez créé précédemment).

Vous pouvez également définir des variables d’environnement Bonjour [portail Azure](https://portal.azure.com/):

1. Ouvrez le panneau de l’application hello web en cliquant sur **Parcourir** > **Web Apps** > nom de votre application web.
2. Dans le volet de votre application web, cliquez sur **Tous les paramètres** > **Paramètres de l’application**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Faites défiler vers le bas toohello **paramètres de l’application** section et ajouter des paires clé/valeur hello.
   
     ![Paramètres de l'application](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Cliquez sur **ENREGISTRER**.

### <a name="publish-hello-application"></a>Publier l’application hello
application de hello toopublish, validez les tooGit de fichiers de code hello et puis envoyez tooazure/maître.

1. Définissez vos informations d'identification de déploiement.
   
        azure site deployment user set <name> <password>
2. Ajoutez et validez vos fichiers d'application.
   
        git add .
        git commit -m "adding files"
3. Push hello validation toohello application Service web d’application :
   
        git push azure master
   
    Utilisez **master** en tant que branche de cible hello. Extrémité hello du déploiement de hello, vous voyez un toohello similaire instruction l’exemple suivant :
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Issue de l’opération de diffusion hello, parcourir les URL de l’application web toohello retourné précédemment par hello `azure create site` commande tooview votre application.

## <a name="next-steps"></a>Étapes suivantes
Lorsque les étapes de hello dans cet article décrivent l’utilisation de hello Service de Table toostore d’informations, vous pouvez également utiliser [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Ressources supplémentaires
[CLI d’Azure]

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[Créer et déployer une application web Node.js dans Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nœud]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remote]: http://git-scm.com/docs/git-remote

[CLI d’Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid de nœud]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
