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
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="fac2e-103">Application web Node.js à l’aide de hello Service de Table Azure</span><span class="sxs-lookup"><span data-stu-id="fac2e-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="fac2e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fac2e-104">Overview</span></span>
<span data-ttu-id="fac2e-105">Ce didacticiel vous montre comment les service de Table toouse fournie par la gestion des données Azure toostore et accéder aux données à partir d’un [nœud] application hébergée dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) les applications Web.</span><span class="sxs-lookup"><span data-stu-id="fac2e-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="fac2e-106">Ce didacticiel part du principe que vous avez déjà une certaine expérience en tant qu'utilisateur des applications node et de [Git]</span><span class="sxs-lookup"><span data-stu-id="fac2e-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="fac2e-107">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fac2e-107">You will learn:</span></span>

* <span data-ttu-id="fac2e-108">Comment toouse npm (Gestionnaire de package de nœud) tooinstall hello les modules de nœud</span><span class="sxs-lookup"><span data-stu-id="fac2e-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="fac2e-109">Comment toowork avec hello service Table Azure</span><span class="sxs-lookup"><span data-stu-id="fac2e-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="fac2e-110">Comment toouse hello CLI d’Azure toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="fac2e-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="fac2e-111">Dans ce didacticiel, vous allez concevoir une application web simple qui permet de créer, récupérer et finaliser des tâches.</span><span class="sxs-lookup"><span data-stu-id="fac2e-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="fac2e-112">tâches de Hello sont stockées dans hello service de Table.</span><span class="sxs-lookup"><span data-stu-id="fac2e-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="fac2e-113">Voici une application hello terminée :</span><span class="sxs-lookup"><span data-stu-id="fac2e-113">Here is hello completed application:</span></span>

![Une page Web avec une liste de tâches vide][node-table-finished]

> [!NOTE]
> <span data-ttu-id="fac2e-115">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="fac2e-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fac2e-116">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="fac2e-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fac2e-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fac2e-117">Prerequisites</span></span>
<span data-ttu-id="fac2e-118">Avant de suivre les instructions de hello dans cet article, assurez-vous d’avoir installé des éléments suivants hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="fac2e-119">[nœud] version 0.10.24 ou supérieure</span><span class="sxs-lookup"><span data-stu-id="fac2e-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="fac2e-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="fac2e-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="fac2e-121">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fac2e-121">Create a storage account</span></span>
<span data-ttu-id="fac2e-122">Créez un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-122">Create an Azure storage account.</span></span> <span data-ttu-id="fac2e-123">application Hello utilisera cette éléments de hello toostore compte d’action.</span><span class="sxs-lookup"><span data-stu-id="fac2e-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="fac2e-124">Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fac2e-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fac2e-125">Cliquez sur hello **nouveau** icône sous hello à gauche du portail de hello, puis cliquez sur **données + stockage** > **stockage**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="fac2e-126">Donnez un nom unique à compte de stockage hello et créer un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md) pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="fac2e-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Bouton Nouveau](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="fac2e-128">Lorsque le compte de stockage hello a été créé, hello **Notifications** un vert clignote en bouton **réussite** et panneau du compte de stockage hello est ouvert tooshow qu’il appartient toohello nouvelle ressource groupe que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="fac2e-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="fac2e-129">Dans le panneau de hello compte de stockage, cliquez sur **paramètres** > **clés**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="fac2e-130">Copiez le Presse-papiers de toohello clé d’accès primaire hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Clé d’accès][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="fac2e-132">Installation des modules et création de la structure</span><span class="sxs-lookup"><span data-stu-id="fac2e-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="fac2e-133">Dans cette section vous créez une nouvelle application de nœud et utiliser les packages de module tooadd npm.</span><span class="sxs-lookup"><span data-stu-id="fac2e-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="fac2e-134">Pour cette application, vous allez utiliser hello [Express] et [Azure] modules.</span><span class="sxs-lookup"><span data-stu-id="fac2e-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="fac2e-135">module de Express Hello fournit une infrastructure de modèle-Vue-contrôleur pour le nœud, hello lors de modules Azure fournit le service de connectivité toohello Table.</span><span class="sxs-lookup"><span data-stu-id="fac2e-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="fac2e-136">Installation express et création de la structure</span><span class="sxs-lookup"><span data-stu-id="fac2e-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="fac2e-137">À partir de la ligne de commande hello, créer un nouveau répertoire nommé **tasklist** et commutateur toothat active.</span><span class="sxs-lookup"><span data-stu-id="fac2e-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="fac2e-138">Entrez hello suivant le module de commande tooinstall hello Express.</span><span class="sxs-lookup"><span data-stu-id="fac2e-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="fac2e-139">En fonction du système d’exploitation de hello, vous devrez peut-être tooput « sudo » avant la commande hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="fac2e-140">sortie de Hello apparaît toohello similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fac2e-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="fac2e-141">Hello '-g' paramètre installe le module de hello globalement.</span><span class="sxs-lookup"><span data-stu-id="fac2e-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="fac2e-142">De cette façon, nous pouvons utiliser **express** toogenerate web application génération de modèles automatique sans avoir tootype dans les informations de chemin d’accès supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="fac2e-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="fac2e-143">génération de modèles automatique pour une application hello, hello toocreate entrez hello **express** commande :</span><span class="sxs-lookup"><span data-stu-id="fac2e-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="fac2e-144">sortie Hello de cette commande s’affiche comme toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fac2e-144">hello output of this command appears similar toohello following example:</span></span>
   
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
   
    <span data-ttu-id="fac2e-145">Vous avez maintenant plusieurs nouveaux répertoires et fichiers Bonjour **tasklist** active.</span><span class="sxs-lookup"><span data-stu-id="fac2e-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="fac2e-146">Installation de modules supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fac2e-146">Install additional modules</span></span>
<span data-ttu-id="fac2e-147">Un des hello fichiers **express** crée est **package.json**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="fac2e-148">Ce fichier contient une liste de dépendances de module.</span><span class="sxs-lookup"><span data-stu-id="fac2e-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="fac2e-149">Plus tard, lorsque vous déployez hello application tooApp Service Web Apps, ce fichier détermine quels modules doivent toobe installé sur Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="fac2e-150">À partir de hello de ligne de commande, entrez hello suivant des modules de hello tooinstall de commande décrites dans hello **package.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="fac2e-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="fac2e-151">Vous devrez peut-être toouse « sudo ».</span><span class="sxs-lookup"><span data-stu-id="fac2e-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="fac2e-152">sortie Hello de cette commande s’affiche comme toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fac2e-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="fac2e-153">Ensuite, entrez hello suivant commande tooinstall hello [azure], [uuid de nœud], [nconf] et [async] modules :</span><span class="sxs-lookup"><span data-stu-id="fac2e-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="fac2e-154">Hello **--enregistrer** indicateur ajoute des entrées pour ces modules de toohello **package.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="fac2e-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="fac2e-155">sortie Hello de cette commande s’affiche comme toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fac2e-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="fac2e-156">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="fac2e-156">Create hello application</span></span>
<span data-ttu-id="fac2e-157">Nous sommes maintenant application hello de toobuild prêt.</span><span class="sxs-lookup"><span data-stu-id="fac2e-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="fac2e-158">Création d’un modèle</span><span class="sxs-lookup"><span data-stu-id="fac2e-158">Create a model</span></span>
<span data-ttu-id="fac2e-159">A *modèle* est un objet qui représente les données de salutation dans votre application.</span><span class="sxs-lookup"><span data-stu-id="fac2e-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="fac2e-160">Pour l’application hello, modèle uniquement de hello est un objet de tâche, qui représente un élément dans la liste des tâches de hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="fac2e-161">Tâches aura hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="fac2e-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="fac2e-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="fac2e-162">PartitionKey</span></span>
* <span data-ttu-id="fac2e-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="fac2e-163">RowKey</span></span>
* <span data-ttu-id="fac2e-164">nom (chaîne)</span><span class="sxs-lookup"><span data-stu-id="fac2e-164">name (string)</span></span>
* <span data-ttu-id="fac2e-165">catégorie (chaîne)</span><span class="sxs-lookup"><span data-stu-id="fac2e-165">category (string)</span></span>
* <span data-ttu-id="fac2e-166">terminé (booléen)</span><span class="sxs-lookup"><span data-stu-id="fac2e-166">completed (Boolean)</span></span>

<span data-ttu-id="fac2e-167">**PartitionKey** et **RowKey** sont utilisés par hello Service de Table en tant que clés de table.</span><span class="sxs-lookup"><span data-stu-id="fac2e-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="fac2e-168">Pour plus d’informations, consultez [modèle de données du Service de Table présentation hello](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="fac2e-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="fac2e-169">Bonjour **tasklist** répertoire, créez un nouveau répertoire nommé **modèles**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="fac2e-170">Bonjour **modèles** répertoire, créez un nouveau fichier nommé **task.js**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="fac2e-171">Ce fichier contient le modèle hello pour les tâches hello créés par votre application.</span><span class="sxs-lookup"><span data-stu-id="fac2e-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="fac2e-172">Au début de hello Hello **task.js** , ajoutez hello suivant tooreference requise des bibliothèques de code :</span><span class="sxs-lookup"><span data-stu-id="fac2e-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="fac2e-173">Ajouter suivant de hello toodefine de code et d’exporter l’objet de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="fac2e-174">Cet objet est chargé de connecter toohello table.</span><span class="sxs-lookup"><span data-stu-id="fac2e-174">This object is responsible for connecting toohello table.</span></span>
   
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
5. <span data-ttu-id="fac2e-175">Ajoutez hello suivant des méthodes supplémentaires de code toodefine sur l’objet de tâche hello, qui permettent des interactions avec les données stockées dans la table de hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
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
6. <span data-ttu-id="fac2e-176">Enregistrez et fermez hello **task.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="fac2e-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="fac2e-177">Création d’un contrôleur</span><span class="sxs-lookup"><span data-stu-id="fac2e-177">Create a controller</span></span>
<span data-ttu-id="fac2e-178">A *contrôleur* gère les requêtes HTTP et restitue la réponse de hello HTML.</span><span class="sxs-lookup"><span data-stu-id="fac2e-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="fac2e-179">Bonjour **tasklist/itinéraires** répertoire, créez un nouveau fichier nommé **tasklist.js** et ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="fac2e-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="fac2e-180">Ajouter hello suivant code trop**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="fac2e-181">Cette opération charge hello azure et async modules qui sont utilisés par **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="fac2e-182">Il définit également hello **TaskList** (fonction), qui est passée à une instance de hello **tâche** définie précédemment l’objet :</span><span class="sxs-lookup"><span data-stu-id="fac2e-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="fac2e-183">Définissez un objet **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="fac2e-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="fac2e-184">Ajouter hello méthodes suivantes trop**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="fac2e-184">Add hello following methods too**TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="fac2e-185">Modification de app.js</span><span class="sxs-lookup"><span data-stu-id="fac2e-185">Modify app.js</span></span>
1. <span data-ttu-id="fac2e-186">À partir de hello **tasklist** répertoire, ouvrez hello **app.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="fac2e-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="fac2e-187">Ce fichier a été créé précédemment en exécutant hello **express** commande.</span><span class="sxs-lookup"><span data-stu-id="fac2e-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="fac2e-188">Au début de hello du fichier de hello, ajoutez hello suivant tooload hello azure module, nom de la table ensemble hello, clé de partition et informations d’identification du stockage ensemble hello utilisées par cet exemple :</span><span class="sxs-lookup"><span data-stu-id="fac2e-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="fac2e-189">nconf charge les valeurs de configuration hello des variables d’environnement ou hello **config.json** fichier, nous allons créer plus tard.</span><span class="sxs-lookup"><span data-stu-id="fac2e-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="fac2e-190">Dans le fichier de app.js hello, faites défiler toowhere vous consultez hello après la ligne :</span><span class="sxs-lookup"><span data-stu-id="fac2e-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="fac2e-191">Remplacez hello au-dessus des lignes de code hello indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fac2e-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="fac2e-192">Sera initialisé une instance de <strong>tâche</strong> avec un compte de stockage de tooyour de connexion.</span><span class="sxs-lookup"><span data-stu-id="fac2e-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="fac2e-193">Il est passé toohello <strong>TaskList</strong>, qui utilisera toocommunicate avec hello service de Table :</span><span class="sxs-lookup"><span data-stu-id="fac2e-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="fac2e-194">Enregistrer hello **app.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="fac2e-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="fac2e-195">Modifier la vue d’index hello</span><span class="sxs-lookup"><span data-stu-id="fac2e-195">Modify hello index view</span></span>
1. <span data-ttu-id="fac2e-196">Ouvrez hello **tasklist/views/index.jade** fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="fac2e-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="fac2e-197">Remplacez hello tout contenu de fichier de hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="fac2e-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="fac2e-198">Ceci définit une vue qui affiche les tâches et comprend un formulaire permettant d’ajouter des tâches et de les marquer comme terminées.</span><span class="sxs-lookup"><span data-stu-id="fac2e-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="fac2e-199">Fermez et enregistrez le fichier **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="fac2e-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="fac2e-200">Modifier la disposition globale de hello</span><span class="sxs-lookup"><span data-stu-id="fac2e-200">Modify hello global layout</span></span>
<span data-ttu-id="fac2e-201">Hello **layout.jade** fichier Bonjour **vues** active est un modèle global pour d’autres **.jade** fichiers.</span><span class="sxs-lookup"><span data-stu-id="fac2e-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="fac2e-202">Dans cette étape vous modifiera toouse [amorçage de Twitter](https://github.com/twbs/bootstrap), qui est un toolkit qui rend toodesign facilement une application web d’aspect intéressant.</span><span class="sxs-lookup"><span data-stu-id="fac2e-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="fac2e-203">Téléchargez et extrayez les fichiers hello pour [amorçage de Twitter](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="fac2e-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="fac2e-204">Hello de copie **bootstrap.min.css** fichier hello Bootstrap **css** dossier hello **public/feuilles de style** répertoire de votre application.</span><span class="sxs-lookup"><span data-stu-id="fac2e-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="fac2e-205">À partir de hello **vues** dossier, ouvrez **layout.jade** et remplacez le contenu entier de hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="fac2e-206">Création d’un fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="fac2e-206">Create a config file</span></span>
<span data-ttu-id="fac2e-207">application hello toorun localement, nous allons présenter des informations d’identification de stockage Azure dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="fac2e-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="fac2e-208">Créez un fichier nommé **config.json* * avec hello suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="fac2e-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="fac2e-209">Remplacez **nom de compte de stockage** avec nom hello du stockage de hello compte que vous avez créé précédemment, puis remplacez **clé d’accès** avec la clé d’accès primaire hello pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fac2e-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="fac2e-210">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fac2e-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="fac2e-211">Enregistrez ce fichier *supérieurs d’un répertoire* à hello **tasklist** répertoire, comme suit :</span><span class="sxs-lookup"><span data-stu-id="fac2e-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="fac2e-212">Hello cela fait tooavoid vérification du fichier de configuration hello dans le contrôle de code source, où il risque de devenir public.</span><span class="sxs-lookup"><span data-stu-id="fac2e-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="fac2e-213">Lors du déploiement de hello application tooAzure, nous allons utiliser des variables d’environnement au lieu d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="fac2e-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="fac2e-214">Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="fac2e-214">Run hello application locally</span></span>
<span data-ttu-id="fac2e-215">application de hello tootest sur votre ordinateur local, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fac2e-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="fac2e-216">Hello de ligne de commande, de modifier répertoires toohello **tasklist** active.</span><span class="sxs-lookup"><span data-stu-id="fac2e-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="fac2e-217">Utilisez hello suite commande toolaunch application hello localement :</span><span class="sxs-lookup"><span data-stu-id="fac2e-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="fac2e-218">Ouvrez un navigateur web et accédez toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="fac2e-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="fac2e-219">Un toohello similaire de page web exemple suivant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fac2e-219">A web page similar toohello following example appears.</span></span>
   
    ![Une page Web affiche une liste de tâches vide.][node-table-finished]
4. <span data-ttu-id="fac2e-221">toocreate un nouvel élément de tâche, entrez un nom et une catégorie, puis cliquez sur **ajouter un élément**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="fac2e-222">toomark une tâche comme étant terminée, vérifiez **Complete** et cliquez sur **des tâches de mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Une image de hello un nouvel élément dans la liste de hello de tâches][node-table-list-items]

<span data-ttu-id="fac2e-224">Bien que l’application hello s’exécute localement, il stocke des données de hello Bonjour service Table Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="fac2e-225">Déployer votre application tooAzure</span><span class="sxs-lookup"><span data-stu-id="fac2e-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="fac2e-226">étapes Hello dans cette section utilisent toocreate des outils de ligne de commande Azure hello une application web dans le Service d’application, puis utilisent Git toodeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="fac2e-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="fac2e-227">tooperform ces étapes, vous devez avoir un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fac2e-228">Ces étapes peuvent également être effectuées à l’aide de hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fac2e-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="fac2e-229">Consultez [Créer et déployer une application web Node.js dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="fac2e-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="fac2e-230">Si c’est la première application web hello, que vous avez créé, vous devez utiliser cette application hello Azure Portal toodeploy.</span><span class="sxs-lookup"><span data-stu-id="fac2e-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="fac2e-231">tooget démarré, installez hello [CLI d’Azure] en entrant la commande suivante à partir de la ligne de commande hello de hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="fac2e-232">Importation de paramètres de publication</span><span class="sxs-lookup"><span data-stu-id="fac2e-232">Import publishing settings</span></span>
<span data-ttu-id="fac2e-233">Dans cette étape, vous allez télécharger un fichier contenant des informations sur votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="fac2e-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="fac2e-234">Entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fac2e-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="fac2e-235">Cette commande lance un navigateur et navigue page de téléchargement toohello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="fac2e-236">Si vous y êtes invité, connectez-vous avec le compte de hello associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="fac2e-237">téléchargement du fichier Hello commence automatiquement ; Si elle n’est pas le cas, vous pouvez cliquer sur lien hello au début de hello hello toomanually téléchargement hello du fichier de page.</span><span class="sxs-lookup"><span data-stu-id="fac2e-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="fac2e-238">Enregistrez hello fichier et notez hello chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="fac2e-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="fac2e-239">Entrez hello suivant les paramètres de commande tooimport hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="fac2e-240">Spécifiez hello chemin d’accès et le nom de publication du fichier de paramètres que vous avez téléchargé à l’étape précédente de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="fac2e-241">Après avoir importé les paramètres de hello, hello de supprimer le fichier de paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="fac2e-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="fac2e-242">Ce fichier n’est plus nécessaire, et il contient des informations sensibles concernant votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="fac2e-243">Créer une application web App Service</span><span class="sxs-lookup"><span data-stu-id="fac2e-243">Create an App Service web app</span></span>
1. <span data-ttu-id="fac2e-244">Hello de ligne de commande, de modifier répertoires toohello **tasklist** active.</span><span class="sxs-lookup"><span data-stu-id="fac2e-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="fac2e-245">Utilisez hello suivant commande toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="fac2e-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="fac2e-246">Vous devez pour l’emplacement et le nom de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="fac2e-247">Fournissez un nom unique et sélectionnez hello même emplacement géographique que votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="fac2e-248">Hello `--git` paramètre crée un référentiel Git sur Azure pour cette application web.</span><span class="sxs-lookup"><span data-stu-id="fac2e-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="fac2e-249">Elle initialise également un référentiel Git dans le répertoire en cours de hello si aucune n’existe et ajoute un [Git remote] nommé « azure », qui est utilisé toopublish hello application tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="fac2e-250">Enfin, il crée un **web.config** fichier, qui contient les paramètres utilisés par les applications de nœud Azure toohost.</span><span class="sxs-lookup"><span data-stu-id="fac2e-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="fac2e-251">Si vous omettez hello `--git` paramètre mais hello répertoire contient un référentiel Git, commande hello crée toujours à distance de hello 'azure'.</span><span class="sxs-lookup"><span data-stu-id="fac2e-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="fac2e-252">Une fois cette commande terminée, vous verrez suivant toohello similaire de sortie.</span><span class="sxs-lookup"><span data-stu-id="fac2e-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="fac2e-253">Notez qu’à partir à la ligne hello avec **site Web créé à** contient l’URL de hello pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
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
   > <span data-ttu-id="fac2e-254">S’il s’agit de hello première application du Service d’applications web pour votre abonnement, vous sera demandé toouse hello Azure Portal toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="fac2e-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="fac2e-255">Pour plus d’informations, consultez la page [Créer et déployer une application web Node.js dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="fac2e-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="fac2e-256">Définition des variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="fac2e-256">Set environment variables</span></span>
<span data-ttu-id="fac2e-257">Dans cette étape, vous allez ajouter la configuration de l’application web tooyour variables environnement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="fac2e-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="fac2e-258">À partir de la ligne de commande hello, entrez suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="fac2e-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="fac2e-259">Remplacez  **<storage account name>**  avec nom hello du stockage de hello compte que vous avez créé précédemment, puis remplacez  **<storage access key>**  avec la clé d’accès primaire hello pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fac2e-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="fac2e-260">(Utilisez hello mêmes valeurs en tant que fichier config.json hello que vous avez créé précédemment).</span><span class="sxs-lookup"><span data-stu-id="fac2e-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="fac2e-261">Vous pouvez également définir des variables d’environnement Bonjour [portail Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="fac2e-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="fac2e-262">Ouvrez le panneau de l’application hello web en cliquant sur **Parcourir** > **Web Apps** > nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="fac2e-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="fac2e-263">Dans le volet de votre application web, cliquez sur **Tous les paramètres** > **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="fac2e-264">Faites défiler vers le bas toohello **paramètres de l’application** section et ajouter des paires clé/valeur hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Paramètres de l'application](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="fac2e-266">Cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="fac2e-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="fac2e-267">Publier l’application hello</span><span class="sxs-lookup"><span data-stu-id="fac2e-267">Publish hello application</span></span>
<span data-ttu-id="fac2e-268">application de hello toopublish, validez les tooGit de fichiers de code hello et puis envoyez tooazure/maître.</span><span class="sxs-lookup"><span data-stu-id="fac2e-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="fac2e-269">Définissez vos informations d'identification de déploiement.</span><span class="sxs-lookup"><span data-stu-id="fac2e-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="fac2e-270">Ajoutez et validez vos fichiers d'application.</span><span class="sxs-lookup"><span data-stu-id="fac2e-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="fac2e-271">Push hello validation toohello application Service web d’application :</span><span class="sxs-lookup"><span data-stu-id="fac2e-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="fac2e-272">Utilisez **master** en tant que branche de cible hello.</span><span class="sxs-lookup"><span data-stu-id="fac2e-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="fac2e-273">Extrémité hello du déploiement de hello, vous voyez un toohello similaire instruction l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fac2e-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="fac2e-274">Issue de l’opération de diffusion hello, parcourir les URL de l’application web toohello retourné précédemment par hello `azure create site` commande tooview votre application.</span><span class="sxs-lookup"><span data-stu-id="fac2e-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fac2e-275">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fac2e-275">Next steps</span></span>
<span data-ttu-id="fac2e-276">Lorsque les étapes de hello dans cet article décrivent l’utilisation de hello Service de Table toostore d’informations, vous pouvez également utiliser [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="fac2e-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fac2e-277">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fac2e-277">Additional resources</span></span>
<span data-ttu-id="fac2e-278">[CLI d’Azure]</span><span class="sxs-lookup"><span data-stu-id="fac2e-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="fac2e-279">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="fac2e-279">What's changed</span></span>
* <span data-ttu-id="fac2e-280">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="fac2e-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
