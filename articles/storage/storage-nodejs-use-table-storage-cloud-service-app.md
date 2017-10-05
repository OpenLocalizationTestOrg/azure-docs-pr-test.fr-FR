---
title: Application web avec stockage Table (Node.js) | Microsoft Docs
description: "Ce didacticiel ajoute les services Azure Storage et le module Azure au didacticiel Application web avec Express."
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
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="4cdb1-103">Application Web Node.js utilisant le stockage</span><span class="sxs-lookup"><span data-stu-id="4cdb1-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="4cdb1-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4cdb1-104">Overview</span></span>
<span data-ttu-id="4cdb1-105">Dans ce didacticiel, vous allez enrichir l’application créée dans le didacticiel [Application web Node.js avec Express] à l’aide des bibliothèques clientes Microsoft Azure pour Node.js afin qu’elle fonctionne avec les services de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="4cdb1-106">Vous allez étendre les fonctionnalités de votre application en vue de créer une application de liste de tâches Web que vous pouvez déployer sur Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="4cdb1-107">La liste de tâches permet à un utilisateur d'extraire des tâches, d'en ajouter de nouvelles et de marquer celles qui sont terminées.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="4cdb1-108">Les éléments de tâches sont stockés dans Azure Storage,</span><span class="sxs-lookup"><span data-stu-id="4cdb1-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="4cdb1-109">qui offre le stockage de données non structurées à tolérance de panne et haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="4cdb1-110">Azure Storage inclut plusieurs structures de données dans lesquelles vous pouvez stocker des données et y accéder. Vous pouvez également exploiter les services de stockage à partir des API incluses dans le Kit de développement logiciel (SDK) Azure pour Node.js ou via les API REST.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="4cdb1-111">Pour plus d’informations, consultez la page [Stockage et accessibilité des données dans Azure].</span><span class="sxs-lookup"><span data-stu-id="4cdb1-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="4cdb1-112">Ce didacticiel part du principe que vous avez suivi les didacticiels [Application web Node.js] et [Node.js avec Express][Application web Node.js avec Express].</span><span class="sxs-lookup"><span data-stu-id="4cdb1-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="4cdb1-113">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-113">You will learn:</span></span>

* <span data-ttu-id="4cdb1-114">utiliser le moteur de modèles Jade ;</span><span class="sxs-lookup"><span data-stu-id="4cdb1-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="4cdb1-115">utiliser les services de gestion de données Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="4cdb1-116">Voici une capture d’écran de l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-116">A screenshot of the completed application is below:</span></span>

![Page Web terminée dans Internet Explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="4cdb1-118">Définition des informations d'identification de stockage dans Web.Config</span><span class="sxs-lookup"><span data-stu-id="4cdb1-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="4cdb1-119">Pour accéder à Azure Storage, vous devez transmettre les informations d'identification de stockage.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="4cdb1-120">Pour ce faire, vous utilisez les paramètres d'application web.config.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="4cdb1-121">Ceux-ci sont transmis en tant que variables d'environnement à Node, qui sont alors lues par le Kit de développement logiciel (SDK) Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="4cdb1-122">Les informations d'identification de stockage sont uniquement utilisées lors du déploiement de l'application sur Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="4cdb1-123">Lorsqu'elle est exécutée dans l'émulateur, l'application utilise l'émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="4cdb1-124">Procédez comme suit pour extraire les informations d'identification de stockage et les ajouter aux paramètres web.config :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="4cdb1-125">Si ce n’est pas déjà le cas, ouvrez Azure PowerShell à partir du menu **Démarrer** en développant **Tous les programmes, Azure**, cliquez avec le bouton droit sur **Azure PowerShell**, puis sélectionnez **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="4cdb1-126">Remplacez les répertoires par le dossier contenant votre application.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="4cdb1-127">Par exemple, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="4cdb1-128">Dans la fenêtre Azure Powershell, entrez la cmdlet suivante pour extraire les informations du compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="4cdb1-129">Cette action permet d'extraire la liste des comptes de stockage et les clés de compte associées à votre service hébergé.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4cdb1-130">Dans la mesure où le Kit de développement logiciel (SDK) Azure crée un compte de stockage lorsque vous déployez un service, un compte de stockage doit déjà exister puisque vous avez déployé votre application dans les guides précédents.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="4cdb1-131">Ouvrez le fichier **ServiceDefinition.csdef** contenant les paramètres d’environnement utilisés lorsque l’application est déployée vers Azure :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="4cdb1-132">Insérez le bloc suivant sous l’élément **Environment**, en remplaçant {STORAGE ACCOUNT} et {STORAGE ACCESS KEY} par le nom de compte et la clé primaire du compte de stockage que vous souhaitez utiliser pour le déploiement :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Contenu du fichier web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="4cdb1-134">Enregistrez le fichier et fermez le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="4cdb1-135">Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4cdb1-135">Install additional modules</span></span>
1. <span data-ttu-id="4cdb1-136">Utilisez la commande suivante pour installer les modules [azure], [node-uuid], [nconf] et [async] en local et pour enregistrer une entrée leur correspondant dans le fichier **package.json** :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="4cdb1-137">Le résultat de cette commande doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-137">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="4cdb1-138">Utilisation du service de Table dans une application Node</span><span class="sxs-lookup"><span data-stu-id="4cdb1-138">Using the Table service in a node application</span></span>
<span data-ttu-id="4cdb1-139">Dans cette section, vous allez étendre l’application de base créée par la commande **express** en ajoutant un fichier **task.js** qui contient le modèle de vos tâches.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="4cdb1-140">Vous allez également modifier le fichier **app.js** existant et créer un fichier **tasklist.js** qui utilise le modèle.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="4cdb1-141">Création du modèle</span><span class="sxs-lookup"><span data-stu-id="4cdb1-141">Create the model</span></span>
1. <span data-ttu-id="4cdb1-142">Dans le répertoire **WebRole1**, créez un répertoire appelé **models**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="4cdb1-143">Dans le répertoire **models**, créez un fichier appelé **task.js**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="4cdb1-144">Ce fichier contiendra le modèle des tâches créées par votre application.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="4cdb1-145">Au début du fichier **task.js** , ajoutez le code suivant pour référencer les bibliothèques nécessaires :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="4cdb1-146">Ensuite, vous allez ajouter du code pour définir et exporter l'objet Task.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="4cdb1-147">Cet objet est responsable de la connexion vers la table.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-147">This object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="4cdb1-148">Ensuite, ajoutez le code suivant pour définir des méthodes supplémentaires sur l'objet Task permettant d'interagir avec les données stockées dans la table :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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
        // use entityGenerator to set types
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

6. <span data-ttu-id="4cdb1-149">Enregistrez, puis fermez le fichier **task.js** .</span><span class="sxs-lookup"><span data-stu-id="4cdb1-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="4cdb1-150">Création du contrôleur</span><span class="sxs-lookup"><span data-stu-id="4cdb1-150">Create the controller</span></span>
1. <span data-ttu-id="4cdb1-151">Dans le répertoire **WebRole1/routes**, créez un fichier **tasklist.js** et ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="4cdb1-152">Ajoutez le code suivant dans **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="4cdb1-153">Cela charge les modules azure et async, qui sont utilisés par **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="4cdb1-154">Cela définit également la fonction **TaskList** à qui est transmise une instance de l’objet **Task** défini précédemment :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="4cdb1-155">Continuez à modifier le fichier **tasklist.js** en ajoutant les méthodes utilisées pour **afficher les tâches (showTasks)**, **ajouter les tâches (addTask)** et **marquer les tâches comme terminées (completeTasks)** :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="4cdb1-156">Enregistrez le fichier **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="4cdb1-157">Modification de app.js</span><span class="sxs-lookup"><span data-stu-id="4cdb1-157">Modify app.js</span></span>
1. <span data-ttu-id="4cdb1-158">Dans le répertoire **WebRole1**, ouvrez le fichier **app.js** dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="4cdb1-159">Au début du fichier, ajoutez ce qui suit pour charger le module azure, et définissez le nom de la table et la clé de partition :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="4cdb1-160">Dans le fichier app.js, faites défiler le contenu jusqu'à la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="4cdb1-161">Remplacez les lignes ci-dessus par le code affiché ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="4cdb1-162">Cela initialise une instance de <strong>Task</strong> avec une connexion à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="4cdb1-163">Elle est transmise à <strong>TaskList</strong>qui l'utilise pour communiquer avec le service de Table :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="4cdb1-164">Enregistrez le fichier **app.js** .</span><span class="sxs-lookup"><span data-stu-id="4cdb1-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="4cdb1-165">Modification de la vue d'index</span><span class="sxs-lookup"><span data-stu-id="4cdb1-165">Modify the index view</span></span>
1. <span data-ttu-id="4cdb1-166">Passez dans le répertoire **views** et ouvrez le fichier **index.jade** dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="4cdb1-167">Remplacez le contenu du fichier **index.jade** par le code qui suit.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="4cdb1-168">Ce code définit la vue pour l'affichage des tâches existantes, ainsi qu'un formulaire pour l'ajout de nouvelles tâches et pour marquer les tâches existantes comme terminées.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="4cdb1-169">Fermez et enregistrez le fichier **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="4cdb1-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="4cdb1-170">Modification de la disposition générale</span><span class="sxs-lookup"><span data-stu-id="4cdb1-170">Modify the global layout</span></span>
<span data-ttu-id="4cdb1-171">Le fichier **layout.jade** du répertoire **views** sert de modèle global aux autres fichiers **.jade**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="4cdb1-172">Dans cette étape, vous allez le modifier pour utiliser [Twitter Bootstrap](https://github.com/twbs/bootstrap), qui est un kit de ressources qui facilite la conception d'un site web bien présenté.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="4cdb1-173">Téléchargez les fichiers du [Twitter Bootstrap](http://getbootstrap.com/), puis procédez à l'extraction.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="4cdb1-174">Copiez le fichier **bootstrap.min.css** du dossier **bootstrap\\dist\\css** vers le répertoire **public\\stylesheets** de votre application de liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="4cdb1-175">Dans le dossier **views**, ouvrez **layout.jade** dans votre éditeur de texte et remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="4cdb1-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="4cdb1-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="4cdb1-177">Enregistrez le fichier **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="4cdb1-178">Exécution de l'application dans l'émulateur</span><span class="sxs-lookup"><span data-stu-id="4cdb1-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="4cdb1-179">Utilisez la commande suivante pour lancer l'application dans l'émulateur.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="4cdb1-180">Le navigateur s'ouvre et affiche la page suivante :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-180">The browser will open and displays the following page:</span></span>

![Page Web intitulée My Task List avec une table contenant les tâches et les domaines pour ajouter une nouvelle tâche](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="4cdb1-182">Utilisez le formulaire pour ajouter des éléments ou supprimez des éléments en les marquant comme terminés.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="4cdb1-183">Publication de l'application dans Azure</span><span class="sxs-lookup"><span data-stu-id="4cdb1-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="4cdb1-184">Dans la fenêtre Windows PowerShell, appelez la cmdlet suivante pour redéployer votre service hébergé vers Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="4cdb1-185">Remplacez **myuniquename** par un nom unique pour cette application.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="4cdb1-186">Remplacez **datacentername** par le nom d’un centre de données Azure, tel que **Ouest des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="4cdb1-187">Une fois le déploiement terminé, une réponse similaire à celle présentée ci-dessous doit s'afficher :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="4cdb1-188">Comme auparavant, dans la mesure où vous avez spécifié l’option **-launch**, le navigateur s’ouvre et affiche votre application qui s’exécute dans Azure une fois la publication effectuée.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Fenêtre de navigateur affichant la page My Task List.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="4cdb1-191">Arrêt et suppression de votre application</span><span class="sxs-lookup"><span data-stu-id="4cdb1-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="4cdb1-192">Après avoir déployé votre application, vous pouvez la désactiver afin d'éviter des coûts ou de générer et de déployer d'autres applications au cours de la période d'évaluation gratuite.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="4cdb1-193">Azure facture les instances de rôle Web par heure de serveur consommée.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="4cdb1-194">Une fois votre application déployée, elle consomme du temps de serveur, même si les instances ne sont pas exécutées et sont arrêtées.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="4cdb1-195">La procédure suivante présente l'arrêt et la suppression de l'application.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="4cdb1-196">Dans la fenêtre Windows PowerShell, arrêtez le déploiement du service créé dans la section précédente à l'aide de la cmdlet suivante :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="4cdb1-197">L'arrêt du service peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="4cdb1-198">Une fois le service arrêté, vous recevez un message confirmant l'arrêt du service.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="4cdb1-199">Pour supprimer le service, utilisez la cmdlet suivante :</span><span class="sxs-lookup"><span data-stu-id="4cdb1-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="4cdb1-200">Lorsque vous y êtes invité, entrez **Y** pour supprimer le service.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="4cdb1-201">La suppression du service peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="4cdb1-202">Une fois le service supprimé, vous recevez un message confirmant la suppression du service.</span><span class="sxs-lookup"><span data-stu-id="4cdb1-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="4cdb1-203">[Application web Node.js avec Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="4cdb1-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="4cdb1-204">[Stockage et accessibilité des données dans Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="4cdb1-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="4cdb1-205">[Application web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="4cdb1-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>


