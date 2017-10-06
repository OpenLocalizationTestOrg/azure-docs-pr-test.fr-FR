---
title: "application d’aaaWeb avec le stockage de table (Node.js) | Documents Microsoft"
description: "Un didacticiel qui s’appuie sur hello application Web Express didacticiel en ajoutant des services Azure Storage et hello module Azure."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a>Application Web Node.js utilisant le stockage
## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous allez étendre application hello créée dans le [Application de Web Node.js à l’aide de Express] didacticiel à l’aide des bibliothèques clientes de hello Microsoft Azure pour toowork Node.js avec les services de gestion de données. Une application de la liste des tâches basée sur le web que vous pouvez déployer tooAzure, vous allez étendre toocreate de votre application. liste des tâches Hello permet à un utilisateur à récupérer les tâches, ajouter de nouvelles tâches et marquer les tâches comme étant terminée.

éléments de tâche Hello sont stockés dans le stockage Azure. qui offre le stockage de données non structurées à tolérance de panne et haute disponibilité. Le stockage Azure inclut plusieurs structures de données dans laquelle vous pouvez stocker et accéder aux données et vous pouvez tirer parti des services de stockage hello de hello API incluses Bonjour Azure SDK pour Node.js ou via les API REST. Pour plus d’informations, consultez la page [Stockage et accessibilité des données dans Azure].

Ce didacticiel suppose que vous avez effectué hello [Application Web Node.js] et [Node.js avec Express][Application de Web Node.js à l’aide de Express] didacticiels.

Vous apprendrez à effectuer les opérations suivantes :

* Comment toowork avec hello moteur modèle Jade
* Comment toowork avec les services de gestion des données Azure

Une capture d’écran de l’application hello terminée est ci-dessous :

![Hello terminé la page web dans internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Définition des informations d'identification de stockage dans Web.Config
tooaccess stockage Azure, vous devez toopass dans les informations d’identification de stockage. toodo, utiliser les paramètres de l’application web.config.
Ces paramètres sont passés en tant que tooNode de variables d’environnement, qui sont ensuite lues par hello Azure SDK.

> [!NOTE]
> Informations d’identification de stockage sont utilisées uniquement lorsque l’application hello est tooAzure déployé. Lors de l’exécution dans l’émulateur de hello, application hello utilisera l’émulateur de stockage hello.
>
>

Effectuer hello suit les informations d’identification du compte de stockage hello étapes tooretrieve et ajouter les paramètres du fichier web.config toohello :

1. Si elle n’est pas déjà ouverte, démarrez hello Azure PowerShell à partir de hello **Démarrer** menu en développant **tous les programmes, Azure**, avec le bouton droit **Azure PowerShell**, puis sélectionnez  **Exécuter en tant qu’administrateur**.
2. Changer le dossier toohello répertoires contenant votre application. Par exemple, C:\\node\\tasklist\\WebRole1.
3. À partir de Azure Powershell hello entrez hello suit les informations de compte de stockage hello tooretrieve applet de commande :

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Cela extrait liste hello de comptes de stockage et le compte de clés associé à votre service hébergé.

   > [!NOTE]
   > Étant donné que hello SDK Azure crée un compte de stockage lorsque vous déployez un service, un compte de stockage doit déjà exister à partir de déploiement de votre application dans les guides de hello précédente.
   >
   >
4. Ouvrez hello **ServiceDefinition.csdef** fichier contenant les paramètres d’environnement hello sont utilisées lors de l’application hello est tooAzure déployé :

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. Suivant de hello INSERT bloque sous **environnement** élément, en remplaçant {compte de stockage} et {clé d’accès} avec le nom du compte hello et de la clé primaire de hello pour le compte de stockage hello toouse souhaité pour le déploiement :

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenu du fichier web.cloud.config Hello](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. Enregistrez le fichier de hello et fermez le bloc-notes.

### <a name="install-additional-modules"></a>Installation de modules supplémentaires
1. Hello utilisation suivant commande tooinstall hello [azure], [uuid-nœud], [nconf] et [asynchrone] modules localement ainsi que des toosave une entrée pour les toohello **package.json** fichier :

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  Hello une sortie de cette commande doit apparaître comme toohello suivantes :

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a>À l’aide du service de Table hello dans une application de nœud
Dans cette section, vous allez étendre les applications de base hello créée par hello **express** commande en ajoutant un **task.js** fichier qui contient le modèle hello pour vos tâches. Vous allez également modifier hello existant **app.js** et créer un nouveau **tasklist.js** fichier qui utilise le modèle de hello.

### <a name="create-hello-model"></a>Créer le modèle de hello
1. Bonjour **WebRole1** répertoire, créez un nouveau répertoire nommé **modèles**.
2. Bonjour **modèles** répertoire, créez un nouveau fichier nommé **task.js**. Ce fichier contient le modèle hello pour les tâches hello créés par votre application.
3. Au début de hello Hello **task.js** , ajoutez hello suivant tooreference requise des bibliothèques de code :

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Ensuite, vous ajoutez le code toodefine et exporter l’objet de tâche hello. Cet objet est chargé de connecter toohello table.

    ```nodejs
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
    ```

5. Ensuite, ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la table de hello :

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. Enregistrez et fermez hello **task.js** fichier.

### <a name="create-hello-controller"></a>Créer le contrôleur de hello
1. Bonjour **WebRole1/itinéraires** répertoire, créez un nouveau fichier nommé **tasklist.js** et ouvrez-le dans un éditeur de texte.
2. Ajouter hello suivant code trop**tasklist.js**. Cette opération charge hello azure et async modules qui sont utilisés par **tasklist.js**. Il définit également hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** définie précédemment l’objet :

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Poursuivre l’ajout de toohello **tasklist.js** fichier en ajoutant des méthodes hello utilisés trop**showTasks**, **addTask**, et **completeTasks**:

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. Enregistrer hello **tasklist.js** fichier.

### <a name="modify-appjs"></a>Modification de app.js
1. Bonjour **WebRole1** répertoire, ouvrez hello **app.js** fichier dans un éditeur de texte.
2. Au début de hello du fichier de hello, ajouter hello suivant du module de hello azure tooload et définissez la clé de nom et la partition de table hello :

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. Dans le fichier de app.js hello, faites défiler toowhere vous consultez hello après la ligne :

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Remplacez hello au-dessus des lignes de code hello indiqué ci-dessous. Sera initialisé une instance de <strong>tâche</strong> avec un compte de stockage de tooyour de connexion. Il est passé toohello <strong>TaskList</strong>, qui utilisera toocommunicate avec hello service de Table :

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Enregistrer hello **app.js** fichier.

### <a name="modify-hello-index-view"></a>Modifier la vue d’index hello
1. Modifiez les répertoires toohello **vues** hello directory et ouvrez **index.jade** fichier dans un éditeur de texte.
2. Remplacez le contenu hello Hello **index.jade** fichier avec le code hello ci-dessous. Cela définit la vue hello pour l’affichage des tâches existantes, ainsi que d’un formulaire pour ajouter de nouvelles tâches et le marquage existants comme étant terminée.

    ```
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
          if tasks != []
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
    ```

3. Fermez et enregistrez le fichier **index.jade** .

### <a name="modify-hello-global-layout"></a>Modifier la disposition globale de hello
Hello **layout.jade** fichier Bonjour **vues** répertoire est utilisé en tant que modèle global pour d’autres **.jade** fichiers. Dans cette étape vous modifiera toouse [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement un site Web d’aspect intéressant.

1. Téléchargez et extrayez les fichiers hello pour [amorçage de Twitter](http://getbootstrap.com/). Hello de copie **bootstrap.min.css** fichier hello **amorçage\\dist\\css** dossier toohello **public\\feuilles de style** répertoire de votre application de la liste des tâches.
2. À partir de hello **vues** dossier, ouvrez hello **layout.jade** dans votre contenu texte éditeur et remplacer hello par hello qui suit :

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. Enregistrer hello **layout.jade** fichier.

### <a name="running-hello-application-in-hello-emulator"></a>En cours d’exécution hello Application Bonjour émulateur
Utilisez hello suite commande toostart hello application dans l’émulateur de hello.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

navigateur de Hello s’ouvre et affiche hello suivant page :

![Un site web paginé intitulée Ma liste de tâches avec une table contenant des tooadd de tâches et les champs une nouvelle tâche.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

Utiliser des éléments tooadd hello formulaire, ou supprimer des éléments existants en les marquant comme étant terminée.

## <a name="publishing-hello-application-tooazure"></a>Publication tooAzure d’Application hello
Dans la fenêtre Windows PowerShell de hello, appelez hello suivant l’applet de commande tooredeploy tooAzure de votre service hébergé.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Remplacez **myuniquename** par un nom unique pour cette application. Remplacez **datacentername** avec nom hello d’un centre de données Azure, tel que **ouest des États-Unis**.

Une fois le déploiement de hello est terminé, vous devez voir s’afficher une réponse similaire toohello :

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

Comme avant, car vous avez spécifié hello **-lancez** option, le navigateur de hello s’ouvre et affiche votre application s’exécutant dans Azure lors de la publication est terminée.

![Affichage de la page de liste des tâches mes hello une fenêtre de navigateur. URL de Hello indique la page de hello maintenant est hébergé sur Azure.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Arrêt et suppression de votre application
Après avoir déployé votre application, vous souhaiterez peut-être toodisable donc vous pouvez éviter les coûts ou générer et déployer d’autres applications au sein de hello gratuite période d’évaluation.

Azure facture les instances de rôle Web par heure de serveur consommée.
Heure du serveur est utilisée une fois que votre application est déployée, même si les instances ne sont pas en cours d’exécution et état de hello s’est arrêté.

Hello étapes suivantes vous montrent comment toostop et supprimer votre application.

1. Dans la fenêtre Windows PowerShell de hello, arrêter le déploiement de service hello créé dans la section précédente de hello avec hello suivant l’applet de commande :

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   L’arrêt du service de hello peut prendre plusieurs minutes. Lors de l’arrêt du service de hello, vous recevez un message indiquant qu’il s’est arrêtée.

2. service de hello toodelete, hello appel suivant l’applet de commande :

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   Lorsque vous y êtes invité, entrez **Y** service de hello toodelete.

   Suppression du service de hello peut prendre plusieurs minutes. Une fois que le service de hello a été supprimé, vous recevez un message indiquant que le service de hello a été supprimée.

[Application de Web Node.js à l’aide de Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Stockage et accessibilité des données dans Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Application Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


