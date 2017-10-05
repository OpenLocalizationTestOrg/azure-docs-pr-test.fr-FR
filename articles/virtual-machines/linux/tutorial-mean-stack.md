---
title: "Créer une pile MEAN sur une machine virtuelle Linux dans Azure | Microsoft Docs"
description: "Découvrez comment créer une pile MongoDB, Express, AngularJS et Node.js (MEAN) sur une machine virtuelle Linux dans Azure."
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
ms.openlocfilehash: 892d3481b4ec70fb8434cb25013c5cfd8ab85051
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="547f3-103">Créer une pile MongoDB, Express, AngularJS et Node.js (MEAN) sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="547f3-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="547f3-104">Ce didacticiel montre comment implémenter une pile MongoDB, Express, AngularJS et Node.js (MEAN) sur une machine virtuelle Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="547f3-104">This tutorial shows you how to implement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="547f3-105">La pile MEAN que vous créez permet l’ajout, la suppression et le référencement de livres dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="547f3-105">The MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="547f3-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="547f3-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="547f3-107">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="547f3-107">Create a Linux VM</span></span>
> * <span data-ttu-id="547f3-108">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="547f3-108">Install Node.js</span></span>
> * <span data-ttu-id="547f3-109">Installer MongoDB et configurer le serveur</span><span class="sxs-lookup"><span data-stu-id="547f3-109">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="547f3-110">Installer Express et définir les itinéraires au serveur</span><span class="sxs-lookup"><span data-stu-id="547f3-110">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="547f3-111">Accéder aux itinéraires avec AngularJS</span><span class="sxs-lookup"><span data-stu-id="547f3-111">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="547f3-112">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="547f3-112">Run the application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="547f3-113">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="547f3-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="547f3-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="547f3-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="547f3-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="547f3-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="547f3-116">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="547f3-116">Create a Linux VM</span></span>

<span data-ttu-id="547f3-117">Créez un groupe de ressources avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create), puis créez une machine virtuelle Linux avec la commande [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="547f3-117">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="547f3-118">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="547f3-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="547f3-119">L’exemple suivant utilise Azure CLI pour créer un groupe de ressources nommé *myResourceGroupMEAN* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="547f3-119">The following example uses the Azure CLI to create a resource group named *myResourceGroupMEAN* in the *eastus* location.</span></span> <span data-ttu-id="547f3-120">Une machine virtuelle nommée *myVM* est créée à l’aide de clés SSH si elles n’existent pas déjà à un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="547f3-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="547f3-121">Pour utiliser un ensemble spécifique de clés, utilisez l’option --ssh-key-value.</span><span class="sxs-lookup"><span data-stu-id="547f3-121">To use a specific set of keys, use the --ssh-key-value option.</span></span>

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

<span data-ttu-id="547f3-122">Lorsque la machine virtuelle est créée, l’interface de ligne de commande Azure affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="547f3-122">When the VM has been created, the Azure CLI shows information similar to the following example:</span></span> 

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
<span data-ttu-id="547f3-123">Notez la valeur de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="547f3-123">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="547f3-124">Cette adresse est utilisée pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="547f3-124">This address is used to access the VM.</span></span>

<span data-ttu-id="547f3-125">Utilisez la commande suivante pour créer une session SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="547f3-125">Use the following command to create an SSH session with the VM.</span></span> <span data-ttu-id="547f3-126">Veillez à utiliser l’adresse IP publique correcte.</span><span class="sxs-lookup"><span data-stu-id="547f3-126">Make sure to use the correct public IP address.</span></span> <span data-ttu-id="547f3-127">Dans l’exemple ci-dessus, notre adresse IP était 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="547f3-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="547f3-128">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="547f3-128">Install Node.js</span></span>

<span data-ttu-id="547f3-129">[Node.js](https://nodejs.org/en/) est un runtime JavaScript reposant sur le moteur JavaScript V8 de Chrome.</span><span class="sxs-lookup"><span data-stu-id="547f3-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="547f3-130">Node.js est utilisé dans ce didacticiel pour configurer les itinéraires Express et les contrôleurs AngularJS.</span><span class="sxs-lookup"><span data-stu-id="547f3-130">Node.js is used in this tutorial to set up the Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="547f3-131">Sur la machine virtuelle, installez Node.js à l’aide de l’interpréteur de commandes Bash que vous avez ouvert avec SSH.</span><span class="sxs-lookup"><span data-stu-id="547f3-131">On the VM, using the bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-the-server"></a><span data-ttu-id="547f3-132">Installer MongoDB et configurer le serveur</span><span class="sxs-lookup"><span data-stu-id="547f3-132">Install MongoDB and set up the server</span></span>
<span data-ttu-id="547f3-133">[MongoDB](http://www.mongodb.com) stocke les données dans des documents flexibles, similaires à JSON.</span><span class="sxs-lookup"><span data-stu-id="547f3-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="547f3-134">Les champs d’une base de données peuvent varier d’un document à l’autre, et la structure des données peut changer au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="547f3-134">Fields in a database can vary from document to document and data structure can be changed over time.</span></span> <span data-ttu-id="547f3-135">Pour notre exemple d’application, nous ajoutons à MongoDB des enregistrements de livre qui contiennent le nom du livre, le numéro isbn, l’auteur et le nombre de pages.</span><span class="sxs-lookup"><span data-stu-id="547f3-135">For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="547f3-136">Sur la machine virtuelle, définissez la clé MongoDB à l’aide de l’interpréteur de commandes Bash que vous avez ouvert avec SSH.</span><span class="sxs-lookup"><span data-stu-id="547f3-136">On the VM, using the bash shell that you opened with SSH, set the MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="547f3-137">Mettez à jour le Gestionnaire de package avec la clé.</span><span class="sxs-lookup"><span data-stu-id="547f3-137">Update the package manager with the key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="547f3-138">Installez MongoDB.</span><span class="sxs-lookup"><span data-stu-id="547f3-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="547f3-139">Démarrez le serveur.</span><span class="sxs-lookup"><span data-stu-id="547f3-139">Start the server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="547f3-140">Nous devons également installer le package [body-parser](https://www.npmjs.com/package/body-parser-json) afin de pouvoir traiter les requêtes passées JSON sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="547f3-140">We also need to install the [body-parser](https://www.npmjs.com/package/body-parser-json) package to help us process the JSON passed in requests to the server.</span></span>

    <span data-ttu-id="547f3-141">Installez le Gestionnaire de package npm.</span><span class="sxs-lookup"><span data-stu-id="547f3-141">Install the npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="547f3-142">Installez le package body-parser.</span><span class="sxs-lookup"><span data-stu-id="547f3-142">Install the body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="547f3-143">Créez un dossier du nom de *Books* et ajoutez-y un fichier nommé *server.js* qui contient la configuration du serveur web.</span><span class="sxs-lookup"><span data-stu-id="547f3-143">Create a folder named *Books* and add a file to it named *server.js* that contains the configuration for the web server.</span></span>

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

## <a name="install-express-and-set-up-routes-to-the-server"></a><span data-ttu-id="547f3-144">Installer Express et définir les itinéraires au serveur</span><span class="sxs-lookup"><span data-stu-id="547f3-144">Install Express and set up routes to the server</span></span>

<span data-ttu-id="547f3-145">[Express](https://expressjs.com) est un framework d’applications web Node.js flexible et minimal qui fournit des fonctionnalités aux applications web et mobiles.</span><span class="sxs-lookup"><span data-stu-id="547f3-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="547f3-146">Express est utilisé dans ce didacticiel pour transmettre des informations de livre en provenance ou à destination de notre base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="547f3-146">Express is used in this tutorial to pass book information to and from our MongoDB database.</span></span> <span data-ttu-id="547f3-147">[Mongoose](http://mongoosejs.com) offre une solution simple, reposant sur un schéma, pour modéliser les données de vos applications.</span><span class="sxs-lookup"><span data-stu-id="547f3-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution to model your application data.</span></span> <span data-ttu-id="547f3-148">Dans ce didacticiel, Mongoose sert à fournir un schéma de livre pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="547f3-148">Mongoose is used in this tutorial to provide a book schema for the database.</span></span>

1. <span data-ttu-id="547f3-149">Installez Express et Mongoose.</span><span class="sxs-lookup"><span data-stu-id="547f3-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="547f3-150">Dans le dossier *Books*, créez un dossier appelé *apps* et ajoutez un fichier nommé *routes.js* avec les itinéraires Express définis.</span><span class="sxs-lookup"><span data-stu-id="547f3-150">In the *Books* folder, create a folder named *apps* and add a file named *routes.js* with the express routes defined.</span></span>

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
            message: "Successfully deleted the book",
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

3. <span data-ttu-id="547f3-151">Dans le dossier *apps*, créez un dossier appelé *models* et ajoutez un fichier nommé *book.js* avec la configuration de modèle de livre définie.</span><span class="sxs-lookup"><span data-stu-id="547f3-151">In the *apps* folder, create a folder named *models* and add a file named *book.js* with the book model configuration defined.</span></span>  

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

## <a name="access-the-routes-with-angularjs"></a><span data-ttu-id="547f3-152">Accéder aux itinéraires avec AngularJS</span><span class="sxs-lookup"><span data-stu-id="547f3-152">Access the routes with AngularJS</span></span>

<span data-ttu-id="547f3-153">[AngularJS](https://angularjs.org) fournit un framework web permettant de créer des vues dynamiques dans vos applications web.</span><span class="sxs-lookup"><span data-stu-id="547f3-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="547f3-154">Dans ce didacticiel, nous utilisons AngularJS pour connecter notre page web à Express et effectuer des actions sur notre base de données de livres.</span><span class="sxs-lookup"><span data-stu-id="547f3-154">In this tutorial, we use AngularJS to connect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="547f3-155">Changez le répertoire de sauvegarde pour *Books* (`cd ../..`), puis créez un dossier du nom de *public* et ajoutez un fichier nommé *script.js* avec la configuration de contrôleur définie.</span><span class="sxs-lookup"><span data-stu-id="547f3-155">Change the directory back up to *Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with the controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="547f3-156">Dans le dossier *public*, créez un fichier du nom de *index.html* avec la page web définie.</span><span class="sxs-lookup"><span data-stu-id="547f3-156">In the *public* folder, create a file named *index.html* with the web page defined.</span></span>

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

##  <a name="run-the-application"></a><span data-ttu-id="547f3-157">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="547f3-157">Run the application</span></span>

1. <span data-ttu-id="547f3-158">Changez le répertoire de sauvegarde pour *Books* (`cd ..`) et démarrez le serveur en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="547f3-158">Change the directory back up to *Books* (`cd ..`) and start the server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="547f3-159">Ouvrez un navigateur web à l’adresse que vous avez enregistrée pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="547f3-159">Open a web browser to the address that you recorded for the VM.</span></span> <span data-ttu-id="547f3-160">Par exemple, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="547f3-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="547f3-161">Un résultat similaire à cette page doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="547f3-161">You should see something like the following page:</span></span>

    ![Enregistrement de livre](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="547f3-163">Renseignez les zones de texte et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="547f3-163">Enter data into the textboxes and click **Add**.</span></span> <span data-ttu-id="547f3-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="547f3-164">For example:</span></span>

    ![Ajout d’un enregistrement de livre](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="547f3-166">Après avoir actualisé la page, vous devez afficher un résultat ressemblant à cette page :</span><span class="sxs-lookup"><span data-stu-id="547f3-166">After refreshing the page, you should see something like this page:</span></span>

    ![Liste des enregistrements de livre](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="547f3-168">Vous pouvez cliquer sur **Supprimer** et supprimer l’enregistrement de livre à partir de la base de données.</span><span class="sxs-lookup"><span data-stu-id="547f3-168">You could click **Delete** and remove the book record from the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="547f3-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="547f3-169">Next steps</span></span>

<span data-ttu-id="547f3-170">Dans ce didacticiel, vous avez créé une application web qui effectue le suivi d’enregistrements de livre à l’aide d’une pile MEAN sur une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="547f3-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="547f3-171">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="547f3-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="547f3-172">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="547f3-172">Create a Linux VM</span></span>
> * <span data-ttu-id="547f3-173">Installer Node.js</span><span class="sxs-lookup"><span data-stu-id="547f3-173">Install Node.js</span></span>
> * <span data-ttu-id="547f3-174">Installer MongoDB et configurer le serveur</span><span class="sxs-lookup"><span data-stu-id="547f3-174">Install MongoDB and set up the server</span></span>
> * <span data-ttu-id="547f3-175">Installer Express et définir les itinéraires au serveur</span><span class="sxs-lookup"><span data-stu-id="547f3-175">Install Express and set up routes to the server</span></span>
> * <span data-ttu-id="547f3-176">Accéder aux itinéraires avec AngularJS</span><span class="sxs-lookup"><span data-stu-id="547f3-176">Access the routes with AngularJS</span></span>
> * <span data-ttu-id="547f3-177">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="547f3-177">Run the application</span></span>

<span data-ttu-id="547f3-178">Passez au didacticiel suivant pour savoir comment mieux protéger les serveurs SSL à l’aide des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="547f3-178">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="547f3-179">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="547f3-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
