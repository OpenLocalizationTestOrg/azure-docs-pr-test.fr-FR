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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="7864d-103">Générer une API RESTful Node.js et le déployer application tooan API dans Azure</span><span class="sxs-lookup"><span data-stu-id="7864d-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="7864d-104">Ce démarrage rapide montre comment toocreate une API REST, écrit avec Node.js [Express](http://expressjs.com/), en utilisant un [Swagger](http://swagger.io/) définition et les déployer en tant qu’un [application API](app-service-api-apps-why-best-platform.md) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7864d-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="7864d-105">Créer l’application hello à l’aide des outils de ligne de commande, de configurer les ressources hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)et déployer l’application hello à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="7864d-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="7864d-106">Lorsque vous avez terminé, vous disposez d’un exemple d’API REST fonctionnelle qui s’exécute sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7864d-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7864d-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7864d-107">Prerequisites</span></span>

* [<span data-ttu-id="7864d-108">Git</span><span class="sxs-lookup"><span data-stu-id="7864d-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="7864d-109">Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="7864d-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7864d-110">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7864d-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7864d-111">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="7864d-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7864d-112">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7864d-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="7864d-113">Préparation de votre environnement</span><span class="sxs-lookup"><span data-stu-id="7864d-113">Prepare your environment</span></span>

1. <span data-ttu-id="7864d-114">Dans une fenêtre de terminal, exécutez hello suivant machine locale tooyour d’exemple hello commande tooclone.</span><span class="sxs-lookup"><span data-stu-id="7864d-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="7864d-115">Remplacez le répertoire toohello qui contient des exemples de code hello.</span><span class="sxs-lookup"><span data-stu-id="7864d-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="7864d-116">Installez [Swaggerize](https://www.npmjs.com/package/swaggerize-express) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7864d-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="7864d-117">Swaggerize est un outil qui génère du code Node.js pour votre API REST à partir d’une définition Swagger.</span><span class="sxs-lookup"><span data-stu-id="7864d-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="7864d-118">Générer du code Node.js</span><span class="sxs-lookup"><span data-stu-id="7864d-118">Generate Node.js code</span></span> 

<span data-ttu-id="7864d-119">Cette section du didacticiel de hello Modélise un processus de développement des API dans lequel vous créez d’abord les métadonnées Swagger et utiliser ce tooscaffold (générer automatiquement) code de serveur pour API de hello.</span><span class="sxs-lookup"><span data-stu-id="7864d-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="7864d-120">Modifier le répertoire toohello *Démarrer* dossier, puis exécutez `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="7864d-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="7864d-121">Swaggerize crée un projet Node.js à votre API à partir de la définition de Swagger hello dans *api.json*.</span><span class="sxs-lookup"><span data-stu-id="7864d-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="7864d-122">Lorsque Swaggerize demande un nom de projet, utilisez *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="7864d-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="7864d-123">Personnaliser le code de projet hello</span><span class="sxs-lookup"><span data-stu-id="7864d-123">Customize hello project code</span></span>

1. <span data-ttu-id="7864d-124">Hello de copie *lib* dossier hello *ContactList* dossier créé par `yo swaggerize`, puis changez de répertoire dans *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="7864d-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="7864d-125">Installer hello `jsonpath` et `swaggerize-ui` des modules NPM.</span><span class="sxs-lookup"><span data-stu-id="7864d-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="7864d-126">Remplacez le code hello Bonjour *handlers/contacts.js* avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7864d-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="7864d-127">Ce code utilise les données JSON hello stockées dans *lib/contacts.json* pris en charge par *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="7864d-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="7864d-128">Hello nouvelle *contacts.js* code retourne tous les contacts dans le référentiel hello comme une charge utile JSON.</span><span class="sxs-lookup"><span data-stu-id="7864d-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="7864d-129">Remplacez le code hello Bonjour **handlers/contacts/{id}.js** fichier avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7864d-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="7864d-130">Ce code vous permet d’utiliser un contact hello uniquement de chemin d’accès tooreturn variable avec un ID donné.</span><span class="sxs-lookup"><span data-stu-id="7864d-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="7864d-131">Remplacez le code hello dans **server.js** avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7864d-131">Replace hello code in **server.js** with hello following code:</span></span>

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

    <span data-ttu-id="7864d-132">Ce code rend certaines toolet de petites modifications il fonctionne avec le Service d’application Azure et expose une interface web interactives à votre API.</span><span class="sxs-lookup"><span data-stu-id="7864d-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="7864d-133">Hello test API localement</span><span class="sxs-lookup"><span data-stu-id="7864d-133">Test hello API locally</span></span>

1. <span data-ttu-id="7864d-134">Démarrer l’application hello Node.js</span><span class="sxs-lookup"><span data-stu-id="7864d-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="7864d-135">Parcourir toohttp://localhost:8000 / contacte tooview hello JSON pour toute liste de contacts hello.</span><span class="sxs-lookup"><span data-stu-id="7864d-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
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

3. <span data-ttu-id="7864d-136">Parcourir le contact de hello tooview toohttp://localhost:8000/contacts/2 avec un `id` de deux.</span><span class="sxs-lookup"><span data-stu-id="7864d-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="7864d-137">API de hello de test à l’aide de l’interface web hello Swagger à http://localhost : 8000/docs.</span><span class="sxs-lookup"><span data-stu-id="7864d-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interface web Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="7864d-139"><a id="createapiapp"></a> Créer une application API</span><span class="sxs-lookup"><span data-stu-id="7864d-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="7864d-140">Dans cette section, vous utilisez hello Azure CLI 2.0 toocreate Bonjour ressources toohost Bonjour API sur Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7864d-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="7864d-141">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="7864d-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="7864d-142">Si vous avez plusieurs abonnements Azure, la modification hello par défaut abonnement toohello souhaité une.</span><span class="sxs-lookup"><span data-stu-id="7864d-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="7864d-143">Déployer l’API hello avec Git</span><span class="sxs-lookup"><span data-stu-id="7864d-143">Deploy hello API with Git</span></span>

<span data-ttu-id="7864d-144">Déployer votre application API de toohello code en envoyant des validations à partir de votre tooAzure de référentiel Git local du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="7864d-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="7864d-145">Initialiser un nouveau référentiel Bonjour *ContactList* active.</span><span class="sxs-lookup"><span data-stu-id="7864d-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="7864d-146">Exclure hello *node_modules* répertoire créé par npm dans une étape antérieure dans le didacticiel hello à partir de Git.</span><span class="sxs-lookup"><span data-stu-id="7864d-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="7864d-147">Créer un nouveau `.gitignore` hello répertoire en cours et ajoutez hello après le texte sur une nouvelle ligne n’importe où dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7864d-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="7864d-148">Confirmer hello `node_modules` dossier est ignoré avec `git status`.</span><span class="sxs-lookup"><span data-stu-id="7864d-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="7864d-149">Valider hello modifications toohello référentiel.</span><span class="sxs-lookup"><span data-stu-id="7864d-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="7864d-150">Hello test API dans Azure</span><span class="sxs-lookup"><span data-stu-id="7864d-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="7864d-151">Ouvrez un navigateur toohttp://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="7864d-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="7864d-152">Vous consultez hello que même JSON retourné en tant que lorsque vous avez effectué la demande hello localement précédemment dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="7864d-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

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

2. <span data-ttu-id="7864d-153">Dans un navigateur, accédez à toohello `http://app_name.azurewebsites.net/docs` tootry de point de terminaison out hello Swagger l’interface utilisateur en cours d’exécution sur Azure.</span><span class="sxs-lookup"><span data-stu-id="7864d-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Interface utilisateur Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="7864d-155">Vous pouvez désormais déployer des mises à jour toohello exemple API tooAzure simplement en envoyant des validations toohello Azure Git référentiel.</span><span class="sxs-lookup"><span data-stu-id="7864d-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="7864d-156">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="7864d-156">Clean up</span></span>

<span data-ttu-id="7864d-157">tooclean des ressources hello créés dans ce démarrage rapide, exécutez hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="7864d-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="7864d-158">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="7864d-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="7864d-159">Consommer des applications API à partir de clients JavaScript avec CORS</span><span class="sxs-lookup"><span data-stu-id="7864d-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

