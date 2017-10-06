---
title: application aaaNode.js API dans Azure App Service | Documents Microsoft
description: "Découvrez comment toocreate une API RESTful Node.js et déployez-le application tooan API dans Azure App Service."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Générer une API RESTful Node.js et le déployer application tooan API dans Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Ce démarrage rapide montre comment toocreate une API REST, écrit avec Node.js [Express](http://expressjs.com/), en utilisant un [Swagger](http://swagger.io/) définition et les déployer en tant qu’un [application API](app-service-api-apps-why-best-platform.md) sur Azure. Créer l’application hello à l’aide des outils de ligne de commande, de configurer les ressources hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)et déployer l’application hello à l’aide de Git.  Lorsque vous avez terminé, vous disposez d’un exemple d’API REST fonctionnelle qui s’exécute sur Azure.

## <a name="prerequisites"></a>Composants requis

* [Git](https://git-scm.com/)
* [Node.js et NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Préparation de votre environnement

1. Dans une fenêtre de terminal, exécutez hello suivant machine locale tooyour d’exemple hello commande tooclone.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Remplacez le répertoire toohello qui contient des exemples de code hello.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Installez [Swaggerize](https://www.npmjs.com/package/swaggerize-express) sur votre ordinateur local. Swaggerize est un outil qui génère du code Node.js pour votre API REST à partir d’une définition Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Générer du code Node.js 

Cette section du didacticiel de hello Modélise un processus de développement des API dans lequel vous créez d’abord les métadonnées Swagger et utiliser ce tooscaffold (générer automatiquement) code de serveur pour API de hello. 

Modifier le répertoire toohello *Démarrer* dossier, puis exécutez `yo swaggerize`. Swaggerize crée un projet Node.js à votre API à partir de la définition de Swagger hello dans *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Lorsque Swaggerize demande un nom de projet, utilisez *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Personnaliser le code de projet hello

1. Hello de copie *lib* dossier hello *ContactList* dossier créé par `yo swaggerize`, puis changez de répertoire dans *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Installer hello `jsonpath` et `swaggerize-ui` des modules NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Remplacez le code hello Bonjour *handlers/contacts.js* avec hello suivant de code : 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Ce code utilise les données JSON hello stockées dans *lib/contacts.json* pris en charge par *lib/contactRepository.js*. Hello nouvelle *contacts.js* code retourne tous les contacts dans le référentiel hello comme une charge utile JSON. 

4. Remplacez le code hello Bonjour **handlers/contacts/{id}.js** fichier avec hello suivant de code :

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Ce code vous permet d’utiliser un contact hello uniquement de chemin d’accès tooreturn variable avec un ID donné.

5. Remplacez le code hello dans **server.js** avec hello suivant de code :

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    Ce code rend certaines toolet de petites modifications il fonctionne avec le Service d’application Azure et expose une interface web interactives à votre API.

### <a name="test-hello-api-locally"></a>Hello test API localement

1. Démarrer l’application hello Node.js
    ```bash
    npm start
    ```
    
2. Parcourir toohttp://localhost:8000 / contacte tooview hello JSON pour toute liste de contacts hello.
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. Parcourir le contact de hello tooview toohttp://localhost:8000/contacts/2 avec un `id` de deux.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. API de hello de test à l’aide de l’interface web hello Swagger à http://localhost : 8000/docs.
   
    ![Interface web Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> Créer une application API

Dans cette section, vous utilisez hello Azure CLI 2.0 toocreate Bonjour ressources toohost Bonjour API sur Azure App Service. 

1.  Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.

    ```azurecli-interactive
    az login
    ```

2. Si vous avez plusieurs abonnements Azure, la modification hello par défaut abonnement toohello souhaité une.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Déployer l’API hello avec Git

Déployer votre application API de toohello code en envoyant des validations à partir de votre tooAzure de référentiel Git local du Service d’applications.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Initialiser un nouveau référentiel Bonjour *ContactList* active. 

    ```bash
    git init .
    ```

3. Exclure hello *node_modules* répertoire créé par npm dans une étape antérieure dans le didacticiel hello à partir de Git. Créer un nouveau `.gitignore` hello répertoire en cours et ajoutez hello après le texte sur une nouvelle ligne n’importe où dans le fichier de hello.

    ```
    node_modules/
    ```
    Confirmer hello `node_modules` dossier est ignoré avec `git status`.

4. Valider hello modifications toohello référentiel.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Hello test API dans Azure

1. Ouvrez un navigateur toohttp://app_name.azurewebsites.net/contacts. Vous consultez hello que même JSON retourné en tant que lorsque vous avez effectué la demande hello localement précédemment dans le didacticiel de hello.

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. Dans un navigateur, accédez à toohello `http://app_name.azurewebsites.net/docs` tootry de point de terminaison out hello Swagger l’interface utilisateur en cours d’exécution sur Azure.

    ![Interface utilisateur Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Vous pouvez désormais déployer des mises à jour toohello exemple API tooAzure simplement en envoyant des validations toohello Azure Git référentiel.

## <a name="clean-up"></a>Nettoyer

tooclean des ressources hello créés dans ce démarrage rapide, exécutez hello suivant commande CLI d’Azure :

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Étape suivante 
> [!div class="nextstepaction"]
> [Consommer des applications API à partir de clients JavaScript avec CORS](app-service-api-cors-consume-javascript.md)

