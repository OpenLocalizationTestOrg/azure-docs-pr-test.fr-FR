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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Créer une pile MongoDB, Express, AngularJS et Node.js (MEAN) sur une machine virtuelle Linux dans Azure

Ce didacticiel vous montre comment tooimplement un MongoDB, Express, AngularJS et Node.js (moyenne) de la pile sur une VM Linux dans Azure. pile moyenne Hello que vous créez permet l’ajout, la suppression et la liste des livres dans une base de données. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer une machine virtuelle Linux
> * Installer Node.js
> * Installer MongoDB et configurer le serveur de hello
> * Installer Express et configurer des itinéraires toohello serveur
> * Voies d’accès hello avec AngularJS
> * Exécutez l’application hello

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Créer une machine virtuelle Linux

Créer un groupe de ressources avec hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) de commandes et créer un VM Linux avec hello [az vm créer](https://docs.microsoft.com/cli/azure/vm#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.

exemple Hello utilise hello CLI d’Azure toocreate est un groupe de ressources nommé *myResourceGroupMEAN* Bonjour *eastus* emplacement. Une machine virtuelle nommée *myVM* est créée à l’aide de clés SSH si elles n’existent pas déjà à un emplacement de clé par défaut. toouse un ensemble spécifique de clés, utilisez hello--ssh-clé-valeur option.

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

Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant : 

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
Prenez note de hello `publicIpAddress`. Cette adresse est utilisée tooaccess hello machine virtuelle.

La commande suivante de hello utilisation toocreate une session SSH avec hello machine virtuelle. Assurez-vous que toouse hello une adresse IP publique correcte. Dans l’exemple ci-dessus, notre adresse IP était 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Installer Node.js

[Node.js](https://nodejs.org/en/) est un runtime JavaScript reposant sur le moteur JavaScript V8 de Chrome. Node.js est utilisé dans ce didacticiel tooset hello Qu'express route des contrôleurs de AngularJS.

Sur hello machine virtuelle, à l’aide de commandes bash hello que vous avez ouvert avec SSH, installez Node.js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>Installer MongoDB et configurer le serveur de hello
[MongoDB](http://www.mongodb.com) stocke les données dans des documents flexibles, similaires à JSON. Les champs dans une base de données peuvent varier de document toodocument et structure de données peut être modifiée au fil du temps. Pour notre exemple d’application, nous ajoutons tooMongoDB enregistrements livre qui contiennent le nom de l’annuaire, numéro isbn, auteur et nombre de pages. 

1. Machine virtuelle, à l’aide de commandes bash hello que vous avez ouvert avec SSH, définissez la clé de MongoDB de hello sur hello.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Mettre à jour le Gestionnaire de package hello avec la clé de hello.
  
    ```bash
    sudo apt-get update
    ```

3. Installez MongoDB.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Démarrez le serveur de hello.

    ```bash
    sudo service mongodb start
    ```

5. Nous devons également tooinstall hello [corps-analyseur](https://www.npmjs.com/package/body-parser-json) package toohelp nous traiter hello JSON passé dans server toohello de requêtes.

    Installer le Gestionnaire de package npm hello.

    ```bash
    sudo apt-get install npm
    ```

    Installez le package hello du corps de l’analyseur.
    
    ```bash
    sudo npm install body-parser
    ```

6. Créez un dossier nommé *la documentation* et ajoutez un tooit fichier nommé *server.js* qui contient la configuration de hello pour le serveur web de hello.

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

## <a name="install-express-and-set-up-routes-toohello-server"></a>Installer Express et configurer des itinéraires toohello serveur

[Express](https://expressjs.com) est un framework d’applications web Node.js flexible et minimal qui fournit des fonctionnalités aux applications web et mobiles. Express est utilisé dans cette tooand d’informations book toopass didacticiel à partir de notre base de données MongoDB. [Mongoose](http://mongoosejs.com) fournit une solution simple, basée sur un schéma de toomodel vos données d’application. Mongoose est utilisé dans ce didacticiel tooprovide un schéma de base de données hello.

1. Installez Express et Mongoose.

    ```bash
    sudo npm install express mongoose
    ```

2. Bonjour *la documentation* dossier, créez un dossier nommé *applications* et ajoutez un fichier nommé *routes.js* avec hello express itinéraires définis.

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

3. Bonjour *applications* dossier, créez un dossier nommé *modèles* et ajoutez un fichier nommé *book.js* avec configuration de modèle de livre hello définie.  

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

## <a name="access-hello-routes-with-angularjs"></a>Voies d’accès hello avec AngularJS

[AngularJS](https://angularjs.org) fournit un framework web permettant de créer des vues dynamiques dans vos applications web. Dans ce didacticiel, nous utiliser AngularJS tooconnect notre page web avec Express et effectuer des actions sur notre base de données de.

1. Basculez hello sauvegarder trop*la documentation* (`cd ../..`), puis créez un dossier nommé *public* et ajoutez un fichier nommé *script.js* avec le contrôleur de hello configuration définie.

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
    
2. Bonjour *public* dossier, créez un fichier nommé *index.html* avec la page web de hello définie.

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

##  <a name="run-hello-application"></a>Exécutez l’application hello

1. Basculez hello sauvegarder trop*la documentation* (`cd ..`) et démarrer le serveur de hello en exécutant cette commande :

    ```bash
    nodejs server.js
    ```

2. Ouvrez une adresse toohello du navigateur web que vous avez enregistrée pour hello machine virtuelle. Par exemple, *http://13.72.77.9:3300*. Vous devez voir quelque chose comme hello suivant page :

    ![Enregistrement de livre](media/tutorial-mean/meanstack-init.png)

3. Entrer des données dans les zones de texte hello et cliquez sur **ajouter**. Par exemple :

    ![Ajout d’un enregistrement de livre](media/tutorial-mean/meanstack-add.png)

4. Après avoir actualisé la page de hello, vous devez voir quelque chose comme cette page :

    ![Liste des enregistrements de livre](media/tutorial-mean/meanstack-list.png)

5. Vous pouvez cliquer sur **supprimer** et supprimer l’enregistrement de livre hello à partir de la base de données hello.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez créé une application web qui effectue le suivi d’enregistrements de livre à l’aide d’une pile MEAN sur une machine virtuelle Linux. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer une machine virtuelle Linux
> * Installer Node.js
> * Installer MongoDB et configurer le serveur de hello
> * Installer Express et configurer des itinéraires toohello serveur
> * Voies d’accès hello avec AngularJS
> * Exécutez l’application hello

Avancer toolearn de didacticiel suivant toohello comment toosecure les serveurs web avec les certificats SSL.

> [!div class="nextstepaction"]
> [Sécuriser un serveur web avec SSL](tutorial-secure-web-server.md)
