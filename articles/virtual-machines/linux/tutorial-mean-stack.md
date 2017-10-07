---
title: "aaaCreate moyenne d’une pile sur un VM Linux dans Azure | Documents Microsoft"
description: "Découvrez comment toocreate un MongoDB, Express, AngularJS et Node.js (moyenne) de la pile sur une VM Linux dans Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="4f745-103">Créer une pile MongoDB, Express, AngularJS et Node.js (MEAN) sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="4f745-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="4f745-104">Ce didacticiel vous montre comment tooimplement un MongoDB, Express, AngularJS et Node.js (moyenne) de la pile sur une VM Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4f745-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="4f745-105">pile moyenne Hello que vous créez permet l’ajout, la suppression et la liste des livres dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="4f745-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="4f745-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f745-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4f745-107">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="4f745-107">Create a Linux VM</span></span>
> * <span data-ttu-id="4f745-108">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="4f745-108">Install Node.js</span></span>
> * <span data-ttu-id="4f745-109">Installer MongoDB et configurer le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="4f745-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="4f745-110">Installer Express et configurer des itinéraires toohello serveur</span><span class="sxs-lookup"><span data-stu-id="4f745-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="4f745-111">Voies d’accès hello avec AngularJS</span><span class="sxs-lookup"><span data-stu-id="4f745-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="4f745-112">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="4f745-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4f745-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4f745-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4f745-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="4f745-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4f745-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4f745-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="4f745-116">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="4f745-116">Create a Linux VM</span></span>

<span data-ttu-id="4f745-117">Créer un groupe de ressources avec hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) de commandes et créer un VM Linux avec hello [az vm créer](https://docs.microsoft.com/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="4f745-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="4f745-118">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="4f745-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="4f745-119">exemple Hello utilise hello CLI d’Azure toocreate est un groupe de ressources nommé *myResourceGroupMEAN* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="4f745-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="4f745-120">Une machine virtuelle nommée *myVM* est créée à l’aide de clés SSH si elles n’existent pas déjà à un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="4f745-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="4f745-121">toouse un ensemble spécifique de clés, utilisez hello--ssh-clé-valeur option.</span><span class="sxs-lookup"><span data-stu-id="4f745-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="4f745-122">Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4f745-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="4f745-123">Prenez note de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="4f745-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="4f745-124">Cette adresse est utilisée tooaccess hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f745-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="4f745-125">La commande suivante de hello utilisation toocreate une session SSH avec hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f745-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="4f745-126">Assurez-vous que toouse hello une adresse IP publique correcte.</span><span class="sxs-lookup"><span data-stu-id="4f745-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="4f745-127">Dans l’exemple ci-dessus, notre adresse IP était 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="4f745-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="4f745-128">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="4f745-128">Install Node.js</span></span>

<span data-ttu-id="4f745-129">[Node.js](https://nodejs.org/en/) est un runtime JavaScript reposant sur le moteur JavaScript V8 de Chrome.</span><span class="sxs-lookup"><span data-stu-id="4f745-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="4f745-130">Node.js est utilisé dans ce didacticiel tooset hello Qu'express route des contrôleurs de AngularJS.</span><span class="sxs-lookup"><span data-stu-id="4f745-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="4f745-131">Sur hello machine virtuelle, à l’aide de commandes bash hello que vous avez ouvert avec SSH, installez Node.js.</span><span class="sxs-lookup"><span data-stu-id="4f745-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="4f745-132">Installer MongoDB et configurer le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="4f745-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="4f745-133">[MongoDB](http://www.mongodb.com) stocke les données dans des documents flexibles, similaires à JSON.</span><span class="sxs-lookup"><span data-stu-id="4f745-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="4f745-134">Les champs dans une base de données peuvent varier de document toodocument et structure de données peut être modifiée au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="4f745-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="4f745-135">Pour notre exemple d’application, nous ajoutons tooMongoDB enregistrements livre qui contiennent le nom de l’annuaire, numéro isbn, auteur et nombre de pages.</span><span class="sxs-lookup"><span data-stu-id="4f745-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="4f745-136">Machine virtuelle, à l’aide de commandes bash hello que vous avez ouvert avec SSH, définissez la clé de MongoDB de hello sur hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="4f745-137">Mettre à jour le Gestionnaire de package hello avec la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="4f745-138">Installez MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f745-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="4f745-139">Démarrez le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="4f745-140">Nous devons également tooinstall hello [corps-analyseur](https://www.npmjs.com/package/body-parser-json) package toohelp nous traiter hello JSON passé dans server toohello de requêtes.</span><span class="sxs-lookup"><span data-stu-id="4f745-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="4f745-141">Installer le Gestionnaire de package npm hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="4f745-142">Installez le package hello du corps de l’analyseur.</span><span class="sxs-lookup"><span data-stu-id="4f745-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="4f745-143">Créez un dossier nommé *la documentation* et ajoutez un tooit fichier nommé *server.js* qui contient la configuration de hello pour le serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="4f745-144">Installer Express et configurer des itinéraires toohello serveur</span><span class="sxs-lookup"><span data-stu-id="4f745-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="4f745-145">[Express](https://expressjs.com) est un framework d’applications web Node.js flexible et minimal qui fournit des fonctionnalités aux applications web et mobiles.</span><span class="sxs-lookup"><span data-stu-id="4f745-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="4f745-146">Express est utilisé dans cette tooand d’informations book toopass didacticiel à partir de notre base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f745-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="4f745-147">[Mongoose](http://mongoosejs.com) fournit une solution simple, basée sur un schéma de toomodel vos données d’application.</span><span class="sxs-lookup"><span data-stu-id="4f745-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="4f745-148">Mongoose est utilisé dans ce didacticiel tooprovide un schéma de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="4f745-149">Installez Express et Mongoose.</span><span class="sxs-lookup"><span data-stu-id="4f745-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="4f745-150">Bonjour *la documentation* dossier, créez un dossier nommé *applications* et ajoutez un fichier nommé *routes.js* avec hello express itinéraires définis.</span><span class="sxs-lookup"><span data-stu-id="4f745-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="4f745-151">Bonjour *applications* dossier, créez un dossier nommé *modèles* et ajoutez un fichier nommé *book.js* avec configuration de modèle de livre hello définie.</span><span class="sxs-lookup"><span data-stu-id="4f745-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="4f745-152">Voies d’accès hello avec AngularJS</span><span class="sxs-lookup"><span data-stu-id="4f745-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="4f745-153">[AngularJS](https://angularjs.org) fournit un framework web permettant de créer des vues dynamiques dans vos applications web.</span><span class="sxs-lookup"><span data-stu-id="4f745-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="4f745-154">Dans ce didacticiel, nous utiliser AngularJS tooconnect notre page web avec Express et effectuer des actions sur notre base de données de.</span><span class="sxs-lookup"><span data-stu-id="4f745-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="4f745-155">Basculez hello sauvegarder trop*la documentation* (`cd ../..`), puis créez un dossier nommé *public* et ajoutez un fichier nommé *script.js* avec le contrôleur de hello configuration définie.</span><span class="sxs-lookup"><span data-stu-id="4f745-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="4f745-156">Bonjour *public* dossier, créez un fichier nommé *index.html* avec la page web de hello définie.</span><span class="sxs-lookup"><span data-stu-id="4f745-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a><span data-ttu-id="4f745-157">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="4f745-157">Run hello application</span></span>

1. <span data-ttu-id="4f745-158">Basculez hello sauvegarder trop*la documentation* (`cd ..`) et démarrer le serveur de hello en exécutant cette commande :</span><span class="sxs-lookup"><span data-stu-id="4f745-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="4f745-159">Ouvrez une adresse toohello du navigateur web que vous avez enregistrée pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f745-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="4f745-160">Par exemple, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="4f745-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="4f745-161">Vous devez voir quelque chose comme hello suivant page :</span><span class="sxs-lookup"><span data-stu-id="4f745-161">You should see something like hello following page:</span></span>

    ![Enregistrement de livre](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="4f745-163">Entrer des données dans les zones de texte hello et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4f745-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="4f745-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4f745-164">For example:</span></span>

    ![Ajout d’un enregistrement de livre](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="4f745-166">Après avoir actualisé la page de hello, vous devez voir quelque chose comme cette page :</span><span class="sxs-lookup"><span data-stu-id="4f745-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Liste des enregistrements de livre](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="4f745-168">Vous pouvez cliquer sur **supprimer** et supprimer l’enregistrement de livre hello à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4f745-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f745-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f745-169">Next steps</span></span>

<span data-ttu-id="4f745-170">Dans ce didacticiel, vous avez créé une application web qui effectue le suivi d’enregistrements de livre à l’aide d’une pile MEAN sur une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="4f745-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="4f745-171">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f745-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4f745-172">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="4f745-172">Create a Linux VM</span></span>
> * <span data-ttu-id="4f745-173">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="4f745-173">Install Node.js</span></span>
> * <span data-ttu-id="4f745-174">Installer MongoDB et configurer le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="4f745-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="4f745-175">Installer Express et configurer des itinéraires toohello serveur</span><span class="sxs-lookup"><span data-stu-id="4f745-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="4f745-176">Voies d’accès hello avec AngularJS</span><span class="sxs-lookup"><span data-stu-id="4f745-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="4f745-177">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="4f745-177">Run hello application</span></span>

<span data-ttu-id="4f745-178">Avancer toolearn de didacticiel suivant toohello comment toosecure les serveurs web avec les certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="4f745-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f745-179">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="4f745-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
