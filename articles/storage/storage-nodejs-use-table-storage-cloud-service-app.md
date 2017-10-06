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
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="0c5c5-103">Application Web Node.js utilisant le stockage</span><span class="sxs-lookup"><span data-stu-id="0c5c5-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="0c5c5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0c5c5-104">Overview</span></span>
<span data-ttu-id="0c5c5-105">Dans ce didacticiel, vous allez étendre application hello créée dans le [Application de Web Node.js à l’aide de Express] didacticiel à l’aide des bibliothèques clientes de hello Microsoft Azure pour toowork Node.js avec les services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-105">In this tutorial, you will extend hello application created in the [Node.js Web Application using Express] tutorial by using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="0c5c5-106">Une application de la liste des tâches basée sur le web que vous pouvez déployer tooAzure, vous allez étendre toocreate de votre application.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-106">You will extend your application toocreate a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="0c5c5-107">liste des tâches Hello permet à un utilisateur à récupérer les tâches, ajouter de nouvelles tâches et marquer les tâches comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="0c5c5-108">éléments de tâche Hello sont stockés dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="0c5c5-109">qui offre le stockage de données non structurées à tolérance de panne et haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="0c5c5-110">Le stockage Azure inclut plusieurs structures de données dans laquelle vous pouvez stocker et accéder aux données et vous pouvez tirer parti des services de stockage hello de hello API incluses Bonjour Azure SDK pour Node.js ou via les API REST.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-110">Azure Storage includes several data structures where you can store and access data, and you can leverage hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="0c5c5-111">Pour plus d’informations, consultez la page [Stockage et accessibilité des données dans Azure].</span><span class="sxs-lookup"><span data-stu-id="0c5c5-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="0c5c5-112">Ce didacticiel suppose que vous avez effectué hello [Application Web Node.js] et [Node.js avec Express][Application de Web Node.js à l’aide de Express] didacticiels.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-112">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="0c5c5-113">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-113">You will learn:</span></span>

* <span data-ttu-id="0c5c5-114">Comment toowork avec hello moteur modèle Jade</span><span class="sxs-lookup"><span data-stu-id="0c5c5-114">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="0c5c5-115">Comment toowork avec les services de gestion des données Azure</span><span class="sxs-lookup"><span data-stu-id="0c5c5-115">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="0c5c5-116">Une capture d’écran de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-116">A screenshot of hello completed application is below:</span></span>

![Hello terminé la page web dans internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="0c5c5-118">Définition des informations d'identification de stockage dans Web.Config</span><span class="sxs-lookup"><span data-stu-id="0c5c5-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="0c5c5-119">tooaccess stockage Azure, vous devez toopass dans les informations d’identification de stockage.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-119">tooaccess Azure Storage, you need toopass in storage credentials.</span></span> <span data-ttu-id="0c5c5-120">toodo, utiliser les paramètres de l’application web.config.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-120">toodo this, you utilize web.config application settings.</span></span>
<span data-ttu-id="0c5c5-121">Ces paramètres sont passés en tant que tooNode de variables d’environnement, qui sont ensuite lues par hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-121">Those settings will be passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="0c5c5-122">Informations d’identification de stockage sont utilisées uniquement lorsque l’application hello est tooAzure déployé.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-122">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="0c5c5-123">Lors de l’exécution dans l’émulateur de hello, application hello utilisera l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-123">When running in hello emulator, hello application will use hello storage emulator.</span></span>
>
>

<span data-ttu-id="0c5c5-124">Effectuer hello suit les informations d’identification du compte de stockage hello étapes tooretrieve et ajouter les paramètres du fichier web.config toohello :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-124">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="0c5c5-125">Si elle n’est pas déjà ouverte, démarrez hello Azure PowerShell à partir de hello **Démarrer** menu en développant **tous les programmes, Azure**, avec le bouton droit **Azure PowerShell**, puis sélectionnez  **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-125">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="0c5c5-126">Changer le dossier toohello répertoires contenant votre application.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-126">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="0c5c5-127">Par exemple, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="0c5c5-128">À partir de Azure Powershell hello entrez hello suit les informations de compte de stockage hello tooretrieve applet de commande :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-128">From hello Azure Powershell window enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="0c5c5-129">Cela extrait liste hello de comptes de stockage et le compte de clés associé à votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-129">This retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0c5c5-130">Étant donné que hello SDK Azure crée un compte de stockage lorsque vous déployez un service, un compte de stockage doit déjà exister à partir de déploiement de votre application dans les guides de hello précédente.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-130">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="0c5c5-131">Ouvrez hello **ServiceDefinition.csdef** fichier contenant les paramètres d’environnement hello sont utilisées lors de l’application hello est tooAzure déployé :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-131">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="0c5c5-132">Suivant de hello INSERT bloque sous **environnement** élément, en remplaçant {compte de stockage} et {clé d’accès} avec le nom du compte hello et de la clé primaire de hello pour le compte de stockage hello toouse souhaité pour le déploiement :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-132">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![contenu du fichier web.cloud.config Hello](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="0c5c5-134">Enregistrez le fichier de hello et fermez le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-134">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="0c5c5-135">Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0c5c5-135">Install additional modules</span></span>
1. <span data-ttu-id="0c5c5-136">Hello utilisation suivant commande tooinstall hello [azure], [uuid-nœud], [nconf] et [asynchrone] modules localement ainsi que des toosave une entrée pour les toohello **package.json** fichier :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-136">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="0c5c5-137">Hello une sortie de cette commande doit apparaître comme toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-137">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="0c5c5-138">À l’aide du service de Table hello dans une application de nœud</span><span class="sxs-lookup"><span data-stu-id="0c5c5-138">Using hello Table service in a node application</span></span>
<span data-ttu-id="0c5c5-139">Dans cette section, vous allez étendre les applications de base hello créée par hello **express** commande en ajoutant un **task.js** fichier qui contient le modèle hello pour vos tâches.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-139">In this section you will extend hello basic application created by hello **express** command by adding a **task.js** file which contains hello model for your tasks.</span></span> <span data-ttu-id="0c5c5-140">Vous allez également modifier hello existant **app.js** et créer un nouveau **tasklist.js** fichier qui utilise le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-140">You will also modify hello existing **app.js** and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="0c5c5-141">Créer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="0c5c5-141">Create hello model</span></span>
1. <span data-ttu-id="0c5c5-142">Bonjour **WebRole1** répertoire, créez un nouveau répertoire nommé **modèles**.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-142">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="0c5c5-143">Bonjour **modèles** répertoire, créez un nouveau fichier nommé **task.js**.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-143">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="0c5c5-144">Ce fichier contient le modèle hello pour les tâches hello créés par votre application.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-144">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="0c5c5-145">Au début de hello Hello **task.js** , ajoutez hello suivant tooreference requise des bibliothèques de code :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-145">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="0c5c5-146">Ensuite, vous ajoutez le code toodefine et exporter l’objet de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-146">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="0c5c5-147">Cet objet est chargé de connecter toohello table.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-147">This object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="0c5c5-148">Ensuite, ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-148">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="0c5c5-149">Enregistrez et fermez hello **task.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-149">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="0c5c5-150">Créer le contrôleur de hello</span><span class="sxs-lookup"><span data-stu-id="0c5c5-150">Create hello controller</span></span>
1. <span data-ttu-id="0c5c5-151">Bonjour **WebRole1/itinéraires** répertoire, créez un nouveau fichier nommé **tasklist.js** et ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-151">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="0c5c5-152">Ajouter hello suivant code trop**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-152">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="0c5c5-153">Cette opération charge hello azure et async modules qui sont utilisés par **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-153">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="0c5c5-154">Il définit également hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** définie précédemment l’objet :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-154">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="0c5c5-155">Poursuivre l’ajout de toohello **tasklist.js** fichier en ajoutant des méthodes hello utilisés trop**showTasks**, **addTask**, et **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="0c5c5-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="0c5c5-156">Enregistrer hello **tasklist.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="0c5c5-157">Modification de app.js</span><span class="sxs-lookup"><span data-stu-id="0c5c5-157">Modify app.js</span></span>
1. <span data-ttu-id="0c5c5-158">Bonjour **WebRole1** répertoire, ouvrez hello **app.js** fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="0c5c5-159">Au début de hello du fichier de hello, ajouter hello suivant du module de hello azure tooload et définissez la clé de nom et la partition de table hello :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="0c5c5-160">Dans le fichier de app.js hello, faites défiler toowhere vous consultez hello après la ligne :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="0c5c5-161">Remplacez hello au-dessus des lignes de code hello indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-161">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="0c5c5-162">Sera initialisé une instance de <strong>tâche</strong> avec un compte de stockage de tooyour de connexion.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-162">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="0c5c5-163">Il est passé toohello <strong>TaskList</strong>, qui utilisera toocommunicate avec hello service de Table :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-163">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="0c5c5-164">Enregistrer hello **app.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="0c5c5-165">Modifier la vue d’index hello</span><span class="sxs-lookup"><span data-stu-id="0c5c5-165">Modify hello index view</span></span>
1. <span data-ttu-id="0c5c5-166">Modifiez les répertoires toohello **vues** hello directory et ouvrez **index.jade** fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="0c5c5-167">Remplacez le contenu hello Hello **index.jade** fichier avec le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-167">Replace hello contents of hello **index.jade** file with hello code below.</span></span> <span data-ttu-id="0c5c5-168">Cela définit la vue hello pour l’affichage des tâches existantes, ainsi que d’un formulaire pour ajouter de nouvelles tâches et le marquage existants comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-168">This defines hello view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="0c5c5-169">Fermez et enregistrez le fichier **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="0c5c5-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="0c5c5-170">Modifier la disposition globale de hello</span><span class="sxs-lookup"><span data-stu-id="0c5c5-170">Modify hello global layout</span></span>
<span data-ttu-id="0c5c5-171">Hello **layout.jade** fichier Bonjour **vues** répertoire est utilisé en tant que modèle global pour d’autres **.jade** fichiers.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="0c5c5-172">Dans cette étape vous modifiera toouse [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement un site Web d’aspect intéressant.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-172">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="0c5c5-173">Téléchargez et extrayez les fichiers hello pour [amorçage de Twitter](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="0c5c5-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="0c5c5-174">Hello de copie **bootstrap.min.css** fichier hello **amorçage\\dist\\css** dossier toohello **public\\feuilles de style** répertoire de votre application de la liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="0c5c5-175">À partir de hello **vues** dossier, ouvrez hello **layout.jade** dans votre contenu texte éditeur et remplacer hello par hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-175">From hello **views** folder, open hello **layout.jade** in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="0c5c5-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="0c5c5-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="0c5c5-177">Enregistrer hello **layout.jade** fichier.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="0c5c5-178">En cours d’exécution hello Application Bonjour émulateur</span><span class="sxs-lookup"><span data-stu-id="0c5c5-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="0c5c5-179">Utilisez hello suite commande toostart hello application dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="0c5c5-180">navigateur de Hello s’ouvre et affiche hello suivant page :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-180">hello browser will open and displays hello following page:</span></span>

![Un site web paginé intitulée Ma liste de tâches avec une table contenant des tooadd de tâches et les champs une nouvelle tâche.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="0c5c5-182">Utiliser des éléments tooadd hello formulaire, ou supprimer des éléments existants en les marquant comme étant terminée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="0c5c5-183">Publication tooAzure d’Application hello</span><span class="sxs-lookup"><span data-stu-id="0c5c5-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="0c5c5-184">Dans la fenêtre Windows PowerShell de hello, appelez hello suivant l’applet de commande tooredeploy tooAzure de votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="0c5c5-185">Remplacez **myuniquename** par un nom unique pour cette application.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="0c5c5-186">Remplacez **datacentername** avec nom hello d’un centre de données Azure, tel que **ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="0c5c5-187">Une fois le déploiement de hello est terminé, vous devez voir s’afficher une réponse similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="0c5c5-188">Comme avant, car vous avez spécifié hello **-lancez** option, le navigateur de hello s’ouvre et affiche votre application s’exécutant dans Azure lors de la publication est terminée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-188">As before, because you specified hello **-launch** option, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Affichage de la page de liste des tâches mes hello une fenêtre de navigateur.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="0c5c5-191">Arrêt et suppression de votre application</span><span class="sxs-lookup"><span data-stu-id="0c5c5-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="0c5c5-192">Après avoir déployé votre application, vous souhaiterez peut-être toodisable donc vous pouvez éviter les coûts ou générer et déployer d’autres applications au sein de hello gratuite période d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="0c5c5-193">Azure facture les instances de rôle Web par heure de serveur consommée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="0c5c5-194">Heure du serveur est utilisée une fois que votre application est déployée, même si les instances ne sont pas en cours d’exécution et état de hello s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="0c5c5-195">Hello étapes suivantes vous montrent comment toostop et supprimer votre application.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="0c5c5-196">Dans la fenêtre Windows PowerShell de hello, arrêter le déploiement de service hello créé dans la section précédente de hello avec hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="0c5c5-197">L’arrêt du service de hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="0c5c5-198">Lors de l’arrêt du service de hello, vous recevez un message indiquant qu’il s’est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="0c5c5-199">service de hello toodelete, hello appel suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="0c5c5-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="0c5c5-200">Lorsque vous y êtes invité, entrez **Y** service de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="0c5c5-201">Suppression du service de hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="0c5c5-202">Une fois que le service de hello a été supprimé, vous recevez un message indiquant que le service de hello a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="0c5c5-202">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

[Application de Web Node.js à l’aide de Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Stockage et accessibilité des données dans Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Application Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


