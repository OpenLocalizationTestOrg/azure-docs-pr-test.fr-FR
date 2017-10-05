---
title: Application API Node.js dans Azure App Service | Microsoft Docs
description: "Découvrez comment créer une API RESTful Node.js et la déployer vers une application API dans Azure App Service."
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
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="3ba84-103">Créer une API RESTful Node.js et la déployer vers une application API dans Azure</span><span class="sxs-lookup"><span data-stu-id="3ba84-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="3ba84-104">Ce guide de démarrage rapide vous indique comment créer une API REST écrite avec Node.js [Express](http://expressjs.com/) à l’aide d’une définition [Swagger](http://swagger.io/), en la déployant sous forme [d’application API](app-service-api-apps-why-best-platform.md) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba84-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="3ba84-105">Vous créez l’application à l’aide d’outils en ligne de commande, configurez des ressources avec [l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), puis déployez l’application au moyen de Git.</span><span class="sxs-lookup"><span data-stu-id="3ba84-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="3ba84-106">Lorsque vous avez terminé, vous disposez d’un exemple d’API REST fonctionnelle qui s’exécute sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba84-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ba84-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3ba84-107">Prerequisites</span></span>

* [<span data-ttu-id="3ba84-108">Git</span><span class="sxs-lookup"><span data-stu-id="3ba84-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="3ba84-109">Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="3ba84-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3ba84-110">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3ba84-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3ba84-111">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3ba84-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="3ba84-112">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3ba84-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="3ba84-113">Préparation de votre environnement</span><span class="sxs-lookup"><span data-stu-id="3ba84-113">Prepare your environment</span></span>

1. <span data-ttu-id="3ba84-114">Dans une fenêtre de terminal, exécutez la commande ci-après pour cloner l’exemple sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="3ba84-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="3ba84-115">Passez au répertoire qui contient l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="3ba84-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="3ba84-116">Installez [Swaggerize](https://www.npmjs.com/package/swaggerize-express) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="3ba84-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="3ba84-117">Swaggerize est un outil qui génère du code Node.js pour votre API REST à partir d’une définition Swagger.</span><span class="sxs-lookup"><span data-stu-id="3ba84-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="3ba84-118">Générer du code Node.js</span><span class="sxs-lookup"><span data-stu-id="3ba84-118">Generate Node.js code</span></span> 

<span data-ttu-id="3ba84-119">Cette section du didacticiel modélise un workflow de développement d’API dans lequel vous créez d’abord les métadonnées Swagger, puis les utilisez pour structurer (auto-générer) le code serveur pour l’API.</span><span class="sxs-lookup"><span data-stu-id="3ba84-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="3ba84-120">Accédez au dossier *start*, puis exécutez `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="3ba84-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="3ba84-121">Swaggerize crée un projet Node.js pour votre API à partir de la définition Swagger dans *api.json*.</span><span class="sxs-lookup"><span data-stu-id="3ba84-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="3ba84-122">Lorsque Swaggerize demande un nom de projet, utilisez *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="3ba84-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="3ba84-123">Personnaliser le code du projet</span><span class="sxs-lookup"><span data-stu-id="3ba84-123">Customize the project code</span></span>

1. <span data-ttu-id="3ba84-124">Copiez le dossier *lib* dans le dossier *ContactList* créé par `yo swaggerize`, puis accédez au dossier *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="3ba84-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="3ba84-125">Installez les modules NPM `jsonpath` et `swaggerize-ui`.</span><span class="sxs-lookup"><span data-stu-id="3ba84-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="3ba84-126">Remplacez le code figurant dans *handlers/contacts.js* par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3ba84-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="3ba84-127">Ce code utilise les données JSON stockées dans *lib/contacts.json* traité par *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="3ba84-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="3ba84-128">Le nouveau code *contacts.js* renvoie tous les contacts du référentiel sous la forme d’une charge utile JSON.</span><span class="sxs-lookup"><span data-stu-id="3ba84-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="3ba84-129">Remplacez le code du fichier **handlers/contacts/{id}.js** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3ba84-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="3ba84-130">Ce code vous permet d’utiliser une variable de chemin d’accès afin que seul le contact présentant un ID spécifique soit renvoyé.</span><span class="sxs-lookup"><span data-stu-id="3ba84-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="3ba84-131">Remplacez le code figurant dans **server.js** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3ba84-131">Replace the code in **server.js** with the following code:</span></span>

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

    <span data-ttu-id="3ba84-132">Ce code apporte quelques modifications minimes pour être en mesure de fonctionner avec Azure App Service et expose une interface web interactive pour votre API.</span><span class="sxs-lookup"><span data-stu-id="3ba84-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="3ba84-133">Tester l’API localement</span><span class="sxs-lookup"><span data-stu-id="3ba84-133">Test the API locally</span></span>

1. <span data-ttu-id="3ba84-134">Démarrer l’application Node.js</span><span class="sxs-lookup"><span data-stu-id="3ba84-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="3ba84-135">Accédez à http://localhost:8000/contacts pour visualiser le code JSON de l’intégralité de la liste de contacts.</span><span class="sxs-lookup"><span data-stu-id="3ba84-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
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

3. <span data-ttu-id="3ba84-136">Accédez à http://localhost:8000/contacts/2 pour visualiser le contact présentant un `id` égal à 2.</span><span class="sxs-lookup"><span data-stu-id="3ba84-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="3ba84-137">Testez l’API à l’aide de l’interface web Swagger à l’adresse http://localhost:8000/docs.</span><span class="sxs-lookup"><span data-stu-id="3ba84-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interface web Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="3ba84-139"><a id="createapiapp"></a> Créer une application API</span><span class="sxs-lookup"><span data-stu-id="3ba84-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="3ba84-140">Dans cette section, vous utilisez Azure CLI 2.0 afin de créer les ressources nécessaires pour l’hébergement de l’API sur Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3ba84-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="3ba84-141">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="3ba84-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="3ba84-142">Si vous avez plusieurs abonnements Azure, modifiez l’abonnement par défaut pour accéder à l’abonnement souhaité.</span><span class="sxs-lookup"><span data-stu-id="3ba84-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="3ba84-143">Déployer l’API avec Git</span><span class="sxs-lookup"><span data-stu-id="3ba84-143">Deploy the API with Git</span></span>

<span data-ttu-id="3ba84-144">Déployez votre code dans l’application API en envoyant des validations de votre référentiel Git local vers Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3ba84-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="3ba84-145">Initialisez un nouveau référentiel dans le répertoire *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="3ba84-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="3ba84-146">Excluez de Git le répertoire *node_modules* créé par npm au cours d’une étape précédente du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3ba84-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="3ba84-147">Créez un fichier `.gitignore` dans le répertoire actuel, puis ajoutez le texte ci-après sur une nouvelle ligne à un emplacement quelconque du fichier.</span><span class="sxs-lookup"><span data-stu-id="3ba84-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="3ba84-148">Vérifiez que le dossier `node_modules` est ignoré avec la commande `git status`.</span><span class="sxs-lookup"><span data-stu-id="3ba84-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="3ba84-149">Validez les modifications apportées au référentiel.</span><span class="sxs-lookup"><span data-stu-id="3ba84-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="3ba84-150">Tester l’API dans Azure</span><span class="sxs-lookup"><span data-stu-id="3ba84-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="3ba84-151">Ouvrez un navigateur et accédez à http://app_name.azurewebsites.net/contacts.</span><span class="sxs-lookup"><span data-stu-id="3ba84-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="3ba84-152">Le code JSON renvoyé est le même que lorsque vous avez exécuté la requête au niveau local lors d’une étape précédente du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3ba84-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

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

2. <span data-ttu-id="3ba84-153">Dans un navigateur, accédez au point de terminaison `http://app_name.azurewebsites.net/docs` pour tester l’interface utilisateur Swagger s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba84-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Interface utilisateur Swagger](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="3ba84-155">Vous pouvez désormais déployer des mises à jour de l’exemple d’API vers Azure en envoyant simplement des validations au référentiel Git Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba84-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="3ba84-156">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="3ba84-156">Clean up</span></span>

<span data-ttu-id="3ba84-157">Pour nettoyer les ressources créées dans le cadre de ce guide de démarrage rapide, exécutez la commande Azure CLI suivante :</span><span class="sxs-lookup"><span data-stu-id="3ba84-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="3ba84-158">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="3ba84-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="3ba84-159">Consommer des applications API à partir de clients JavaScript avec CORS</span><span class="sxs-lookup"><span data-stu-id="3ba84-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

