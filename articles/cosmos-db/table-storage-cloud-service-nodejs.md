---
title: "application d’aaaWeb avec le stockage de table (Node.js) | Documents Microsoft"
description: "Un didacticiel qui s’appuie sur hello application Web Express didacticiel en ajoutant des services Azure Storage et hello module Azure."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="a12ba-103">Application Web Node.js utilisant le stockage</span><span class="sxs-lookup"><span data-stu-id="a12ba-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="a12ba-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a12ba-104">Overview</span></span>
<span data-ttu-id="a12ba-105">Dans ce didacticiel, hello application que vous avez créé dans le [Application de Web Node.js à l’aide de Express] didacticiel est étendu à l’aide des bibliothèques clientes de hello Microsoft Azure pour toowork Node.js avec les services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="a12ba-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="a12ba-106">Vous étendez votre application en créant une application de la liste des tâches basée sur le web que vous pouvez déployer tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a12ba-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="a12ba-107">liste des tâches Hello permet à un utilisateur à récupérer les tâches, ajouter de nouvelles tâches et marquer les tâches comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="a12ba-108">éléments de tâche Hello sont stockés dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="a12ba-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="a12ba-109">qui offre le stockage de données non structurées à tolérance de panne et haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="a12ba-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="a12ba-110">Le service Stockage Azure englobe plusieurs structures de données dans lesquelles vous pouvez stocker des données et y accéder.</span><span class="sxs-lookup"><span data-stu-id="a12ba-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="a12ba-111">Vous pouvez utiliser les services de stockage hello de hello API incluses Bonjour Azure SDK pour Node.js ou via les API REST.</span><span class="sxs-lookup"><span data-stu-id="a12ba-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="a12ba-112">Pour plus d’informations, consultez la page [Stockage et accessibilité des données dans Azure].</span><span class="sxs-lookup"><span data-stu-id="a12ba-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="a12ba-113">Ce didacticiel suppose que vous avez effectué hello [Application Web Node.js] et [Node.js avec Express][Application de Web Node.js à l’aide de Express] didacticiels.</span><span class="sxs-lookup"><span data-stu-id="a12ba-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="a12ba-114">Il contient hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a12ba-114">It contains hello following information:</span></span>

* <span data-ttu-id="a12ba-115">Comment toowork avec hello moteur modèle Jade</span><span class="sxs-lookup"><span data-stu-id="a12ba-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="a12ba-116">Comment toowork avec les services de gestion des données Azure</span><span class="sxs-lookup"><span data-stu-id="a12ba-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="a12ba-117">Hello suivant capture d’écran montre application hello terminée :</span><span class="sxs-lookup"><span data-stu-id="a12ba-117">hello following screenshot shows hello completed application:</span></span>

![Hello terminé la page web dans internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="a12ba-119">Définition des informations d'identification de stockage dans Web.Config</span><span class="sxs-lookup"><span data-stu-id="a12ba-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="a12ba-120">Vous devez passer tooaccess informations d’identification de stockage Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a12ba-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="a12ba-121">Cela permet à l’aide des paramètres de l’application web.config hello.</span><span class="sxs-lookup"><span data-stu-id="a12ba-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="a12ba-122">les paramètres web.config Hello sont passées comme tooNode de variables d’environnement, qui sont ensuite lus par hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="a12ba-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="a12ba-123">Informations d’identification de stockage sont utilisées uniquement lorsque l’application hello est tooAzure déployé.</span><span class="sxs-lookup"><span data-stu-id="a12ba-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="a12ba-124">Lors de l’exécution dans l’émulateur de hello, application hello utilise l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a12ba-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="a12ba-125">Effectuer hello suit les informations d’identification du compte de stockage hello étapes tooretrieve et ajouter les paramètres du fichier web.config toohello :</span><span class="sxs-lookup"><span data-stu-id="a12ba-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="a12ba-126">Si elle n’est pas déjà ouverte, démarrez hello Azure PowerShell à partir de hello **Démarrer** menu en développant **tous les programmes, Azure**, avec le bouton droit **Azure PowerShell**, puis sélectionnez  **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="a12ba-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="a12ba-127">Changer le dossier toohello répertoires contenant votre application.</span><span class="sxs-lookup"><span data-stu-id="a12ba-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="a12ba-128">Par exemple, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="a12ba-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="a12ba-129">À partir de hello Azure Powershell, entrez hello suit les informations de compte de stockage hello tooretrieve applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a12ba-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="a12ba-130">Hello applet de commande précédente récupère la liste hello des comptes de stockage et les clés de compte associés à votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="a12ba-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a12ba-131">Étant donné que hello SDK Azure crée un compte de stockage lorsque vous déployez un service, un compte de stockage doit déjà exister à partir de déploiement de votre application dans les guides de hello précédente.</span><span class="sxs-lookup"><span data-stu-id="a12ba-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="a12ba-132">Ouvrez hello **ServiceDefinition.csdef** fichier contenant les paramètres d’environnement hello sont utilisées lors de l’application hello est tooAzure déployé :</span><span class="sxs-lookup"><span data-stu-id="a12ba-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="a12ba-133">Suivant de hello INSERT bloque sous **environnement** élément, en remplaçant {compte de stockage} et {clé d’accès} avec le nom du compte hello et de la clé primaire de hello pour le compte de stockage hello toouse souhaité pour le déploiement :</span><span class="sxs-lookup"><span data-stu-id="a12ba-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenu du fichier web.cloud.config Hello](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="a12ba-135">Enregistrez le fichier de hello et fermez le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="a12ba-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="a12ba-136">Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a12ba-136">Install additional modules</span></span>
1. <span data-ttu-id="a12ba-137">Hello utilisation suivant commande tooinstall hello [azure], [uuid-nœud], [nconf] et [asynchrone] modules localement ainsi que des toosave une entrée pour les toohello **package.json** fichier :</span><span class="sxs-lookup"><span data-stu-id="a12ba-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="a12ba-138">Hello une sortie de cette commande doit apparaître comme toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a12ba-138">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="a12ba-139">À l’aide du service de Table hello dans une application de nœud</span><span class="sxs-lookup"><span data-stu-id="a12ba-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="a12ba-140">Dans cette section, hello application de base créée par hello **express** commande est étendue en ajoutant un **task.js** fichier contenant le modèle hello pour vos tâches.</span><span class="sxs-lookup"><span data-stu-id="a12ba-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="a12ba-141">Modifiez hello **app.js** de fichiers et de créer un nouveau **tasklist.js** fichier qui utilise le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="a12ba-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="a12ba-142">Créer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="a12ba-142">Create hello model</span></span>
1. <span data-ttu-id="a12ba-143">Bonjour **WebRole1** répertoire, créez un nouveau répertoire nommé **modèles**.</span><span class="sxs-lookup"><span data-stu-id="a12ba-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="a12ba-144">Bonjour **modèles** répertoire, créez un nouveau fichier nommé **task.js**.</span><span class="sxs-lookup"><span data-stu-id="a12ba-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="a12ba-145">Ce fichier contient le modèle hello pour les tâches hello créés par votre application.</span><span class="sxs-lookup"><span data-stu-id="a12ba-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="a12ba-146">Au début de hello Hello **task.js** , ajoutez hello suivant tooreference requise des bibliothèques de code :</span><span class="sxs-lookup"><span data-stu-id="a12ba-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="a12ba-147">Ensuite, ajoutez le code toodefine et exporter l’objet de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="a12ba-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="a12ba-148">objet de tâche Hello est chargé de connecter toohello table.</span><span class="sxs-lookup"><span data-stu-id="a12ba-148">hello Task object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="a12ba-149">Ensuite, ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="a12ba-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="a12ba-150">Enregistrez et fermez hello **task.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="a12ba-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="a12ba-151">Créer le contrôleur de hello</span><span class="sxs-lookup"><span data-stu-id="a12ba-151">Create hello controller</span></span>
1. <span data-ttu-id="a12ba-152">Bonjour **WebRole1/itinéraires** répertoire, créez un nouveau fichier nommé **tasklist.js** et ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a12ba-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="a12ba-153">Ajouter hello suivant code trop**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="a12ba-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="a12ba-154">Ce code charge hello azure et les modules asynchrones, qui sont utilisés par **tasklist.js** et définit hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** nous l’objet défini précédemment :</span><span class="sxs-lookup"><span data-stu-id="a12ba-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="a12ba-155">Poursuivre l’ajout de toohello **tasklist.js** fichier en ajoutant des méthodes hello utilisés trop**showTasks**, **addTask**, et **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="a12ba-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="a12ba-156">Enregistrer hello **tasklist.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="a12ba-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="a12ba-157">Modification de app.js</span><span class="sxs-lookup"><span data-stu-id="a12ba-157">Modify app.js</span></span>
1. <span data-ttu-id="a12ba-158">Bonjour **WebRole1** répertoire, ouvrez hello **app.js** fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a12ba-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="a12ba-159">Au début de hello du fichier de hello, ajouter hello suivant du module de hello azure tooload et définissez la clé de nom et la partition de table hello :</span><span class="sxs-lookup"><span data-stu-id="a12ba-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="a12ba-160">Dans le fichier de app.js hello, faites défiler toowhere vous consultez hello après la ligne :</span><span class="sxs-lookup"><span data-stu-id="a12ba-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="a12ba-161">Remplacez hello précédant les lignes avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="a12ba-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="a12ba-162">Ce code initialise une instance de <strong>tâche</strong> avec un compte de stockage de tooyour de connexion.</span><span class="sxs-lookup"><span data-stu-id="a12ba-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="a12ba-163">Hello <strong>tâche</strong> est passé toohello <strong>TaskList</strong>, qui utilise toocommunicate avec service de Table hello :</span><span class="sxs-lookup"><span data-stu-id="a12ba-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="a12ba-164">Enregistrer hello **app.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="a12ba-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="a12ba-165">Modifier la vue d’index hello</span><span class="sxs-lookup"><span data-stu-id="a12ba-165">Modify hello index view</span></span>
1. <span data-ttu-id="a12ba-166">Modifiez les répertoires toohello **vues** hello directory et ouvrez **index.jade** fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a12ba-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="a12ba-167">Remplacez le contenu hello Hello **index.jade** fichier avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="a12ba-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="a12ba-168">Ce code définit l’affichage de hello pour l’affichage des tâches existantes et définit un formulaire pour ajouter de nouvelles tâches et le marquage existants comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="a12ba-169">Fermez et enregistrez le fichier **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="a12ba-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="a12ba-170">Modifier la disposition globale de hello</span><span class="sxs-lookup"><span data-stu-id="a12ba-170">Modify hello global layout</span></span>
<span data-ttu-id="a12ba-171">Hello **layout.jade** fichier Bonjour **vues** répertoire est utilisé en tant que modèle global pour d’autres **.jade** fichiers.</span><span class="sxs-lookup"><span data-stu-id="a12ba-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="a12ba-172">Dans cette étape, modifiez hello **layout.jade** toouse de fichiers [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement un site Web d’aspect intéressant.</span><span class="sxs-lookup"><span data-stu-id="a12ba-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="a12ba-173">Téléchargez et extrayez les fichiers hello pour [amorçage de Twitter](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="a12ba-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="a12ba-174">Hello de copie **bootstrap.min.css** fichier hello **amorçage\\dist\\css** dossier toohello **public\\feuilles de style** répertoire de votre application de la liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="a12ba-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="a12ba-175">À partir de hello **vues** dossier, ouvrez hello **layout.jade** dans votre éditeur de texte et remplacez le contenu de hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="a12ba-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="a12ba-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="a12ba-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="a12ba-177">Enregistrer hello **layout.jade** fichier.</span><span class="sxs-lookup"><span data-stu-id="a12ba-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="a12ba-178">En cours d’exécution hello Application Bonjour émulateur</span><span class="sxs-lookup"><span data-stu-id="a12ba-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="a12ba-179">Utilisez hello suite commande toostart hello application dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a12ba-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="a12ba-180">navigateur de Hello s’ouvre et affiche hello suivant page :</span><span class="sxs-lookup"><span data-stu-id="a12ba-180">hello browser opens and displays hello following page:</span></span>

![Un site web paginé intitulée Ma liste de tâches avec une table contenant des tooadd de tâches et les champs une nouvelle tâche.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="a12ba-182">Utiliser des éléments tooadd hello formulaire, ou supprimer des éléments existants en les marquant comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="a12ba-183">Publication tooAzure d’Application hello</span><span class="sxs-lookup"><span data-stu-id="a12ba-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="a12ba-184">Dans la fenêtre Windows PowerShell de hello, appelez hello suivant l’applet de commande tooredeploy tooAzure de votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="a12ba-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="a12ba-185">Remplacez **myuniquename** par un nom unique pour cette application.</span><span class="sxs-lookup"><span data-stu-id="a12ba-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="a12ba-186">Remplacez **datacentername** avec nom hello d’un centre de données Azure, tel que **ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="a12ba-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="a12ba-187">Une fois le déploiement de hello est terminé, vous devez voir s’afficher une réponse similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="a12ba-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="a12ba-188">En spécifiant hello **-lancez** option hello précédente applet de commande navigateur de hello s’ouvre et affiche votre application s’exécutant dans Azure lors de la publication est terminée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Affichage de la page de liste des tâches mes hello une fenêtre de navigateur.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="a12ba-191">Arrêt et suppression de votre application</span><span class="sxs-lookup"><span data-stu-id="a12ba-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="a12ba-192">Après avoir déployé votre application, vous souhaiterez peut-être toodisable donc vous pouvez éviter les coûts ou générer et déployer d’autres applications au sein de hello gratuite période d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="a12ba-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="a12ba-193">Azure facture les instances de rôle Web par heure de serveur consommée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="a12ba-194">Heure du serveur est utilisée une fois que votre application est déployée, même si les instances ne sont pas en cours d’exécution et état de hello s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="a12ba-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="a12ba-195">Hello étapes suivantes vous montrent comment toostop et supprimer votre application.</span><span class="sxs-lookup"><span data-stu-id="a12ba-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="a12ba-196">Dans la fenêtre Windows PowerShell de hello, arrêter le déploiement de service hello créé dans la section précédente de hello avec hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a12ba-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="a12ba-197">L’arrêt du service de hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="a12ba-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="a12ba-198">Lors de l’arrêt du service de hello, vous recevez un message indiquant qu’il s’est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="a12ba-199">service de hello toodelete, hello appel suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a12ba-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="a12ba-200">Lorsque vous y êtes invité, entrez **Y** service de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="a12ba-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="a12ba-201">Suppression du service de hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="a12ba-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="a12ba-202">Une fois que le service de hello est supprimé, vous recevrez un message indiquant que le service de hello a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="a12ba-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[Application de Web Node.js à l’aide de Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Stockage et accessibilité des données dans Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Application Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


