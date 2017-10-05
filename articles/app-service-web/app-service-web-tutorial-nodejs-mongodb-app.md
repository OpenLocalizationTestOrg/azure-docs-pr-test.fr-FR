---
title: "Créer une application web Node.js et MongoDB dans Azure | Microsoft Docs"
description: "Apprenez comment faire fonctionner une application Node.js dans Azure, avec une connexion à une base de données Cosmos DB, via une chaîne de connexion MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="b5288-103">Créer une application web Node.js et MongoDB dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="b5288-104">Azure Web Apps offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="b5288-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b5288-105">Ce didacticiel vous montre comment créer une application web Node.js dans Azure et comment la connecter à une base de données.</span><span class="sxs-lookup"><span data-stu-id="b5288-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="b5288-106">Lorsque vous aurez terminé, vous disposerez d’une application MEAN (MongoDB, Express, AngularJS et Node.js) exécutée sous [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5288-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="b5288-107">Pour plus de simplicité, l’exemple d’application utilise [l’infrastructure de développement web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="b5288-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![Application MEAN.js exécutée dans Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="b5288-109">Ce que vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="b5288-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5288-110">Créer une base de données MongoDB dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="b5288-111">Connecter une application Node.js à MongoDB</span><span class="sxs-lookup"><span data-stu-id="b5288-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="b5288-112">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="b5288-113">Mise à jour du modèle de données et redéploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="b5288-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="b5288-114">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="b5288-115">Gestion de l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5288-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b5288-116">Prerequisites</span></span>

<span data-ttu-id="b5288-117">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="b5288-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="b5288-118">Installez Git</span><span class="sxs-lookup"><span data-stu-id="b5288-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="b5288-119">Installez Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="b5288-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="b5288-120">[Installer Gulp.js](http://gulpjs.com/) (requis par [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="b5288-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="b5288-121">Installez et exécutez MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="b5288-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b5288-122">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b5288-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b5288-123">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="b5288-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="b5288-124">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5288-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="b5288-125">Tester la base de données MongoDB locale</span><span class="sxs-lookup"><span data-stu-id="b5288-125">Test local MongoDB</span></span>

<span data-ttu-id="b5288-126">Ouvrez la fenêtre du terminal et `cd` dans le répertoire `bin` de votre installation MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b5288-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="b5288-127">Vous pouvez utilisez cette fenêtre de terminal pour exécuter toutes les commandes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b5288-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="b5288-128">Exécutez `mongo` dans le terminal pour vous connecter à votre serveur MongoDB local.</span><span class="sxs-lookup"><span data-stu-id="b5288-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="b5288-129">Si la connexion est établie, cela signifie que votre base de données MongoDB est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b5288-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="b5288-130">Dans le cas contraire, assurez-vous que votre base de données MongoDB locale est démarrée en suivant les étapes de la procédure [d’installation de MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="b5288-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="b5288-131">Souvent, MongoDB est installé, mais vous devez néanmoins le démarrer en exécutant `mongod`.</span><span class="sxs-lookup"><span data-stu-id="b5288-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="b5288-132">Lorsque vous avez fini de tester votre base de données MongoDB, tapez `Ctrl+C` dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="b5288-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="b5288-133">Créer une application Node.js locale</span><span class="sxs-lookup"><span data-stu-id="b5288-133">Create local Node.js app</span></span>

<span data-ttu-id="b5288-134">Cette étape consiste à configurer le projet Node.js local.</span><span class="sxs-lookup"><span data-stu-id="b5288-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="b5288-135">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="b5288-135">Clone the sample application</span></span>

<span data-ttu-id="b5288-136">Dans la fenêtre de terminal, `cd` vers un répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="b5288-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="b5288-137">Exécutez la commande suivante pour cloner l’exemple de référentiel.</span><span class="sxs-lookup"><span data-stu-id="b5288-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="b5288-138">Cet exemple de référentiel contient une copie du référentiel [MEAN.js](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="b5288-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="b5288-139">Il est modifié pour s’exécuter sous App Service (pour plus d’informations, consultez le fichier [Lisez-moi](https://github.com/Azure-Samples/meanjs/blob/master/README.md) du référentiel MEAN.js).</span><span class="sxs-lookup"><span data-stu-id="b5288-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="b5288-140">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="b5288-140">Run the application</span></span>

<span data-ttu-id="b5288-141">Exécutez la commande suivante pour installer les packages requis et démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="b5288-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="b5288-142">Lorsque l’application est entièrement chargée, vous obtenez un message similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="b5288-142">When the app is fully loaded, you see something similar to the following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="b5288-143">Accédez à http://localhost:3000 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="b5288-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="b5288-144">Cliquez sur **S’inscrire** dans le menu supérieur et créez un utilisateur test.</span><span class="sxs-lookup"><span data-stu-id="b5288-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="b5288-145">L’exemple d’application MEAN.js stocke les données utilisateur dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="b5288-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="b5288-146">Si vous parvenez à créer un utilisateur et à vous connecter, votre application écrit les données dans la base de données MongoDB locale.</span><span class="sxs-lookup"><span data-stu-id="b5288-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js se connecte correctement à MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="b5288-148">Sélectionnez **Admin > Manage Articles** (Administrateur > Gérer les articles) pour ajouter des articles.</span><span class="sxs-lookup"><span data-stu-id="b5288-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="b5288-149">Pour arrêter Node.js à tout moment, appuyez sur `Ctrl+C` dans le terminal.</span><span class="sxs-lookup"><span data-stu-id="b5288-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="b5288-150">Créer une base de données MongoDB de production</span><span class="sxs-lookup"><span data-stu-id="b5288-150">Create production MongoDB</span></span>

<span data-ttu-id="b5288-151">Dans cette étape, vous allez créer une base de données MongoDB dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="b5288-152">Lorsque votre application est déployée sur Azure, elle utilise cette base de données cloud.</span><span class="sxs-lookup"><span data-stu-id="b5288-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="b5288-153">Pour MongoDB, ce didacticiel utilise [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b5288-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="b5288-154">Cosmos DB prend en charge les connexions client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b5288-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="b5288-155">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-155">Log in to Azure</span></span>

<span data-ttu-id="b5288-156">Azure CLI 2.0 vous permettra de créer les ressources nécessaires pour héberger votre application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="b5288-157">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="b5288-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="b5288-158">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="b5288-158">Create a resource group</span></span>

<span data-ttu-id="b5288-159">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b5288-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="b5288-160">L’exemple suivant crée un groupe de ressources dans la région Europe de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="b5288-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="b5288-161">Utilisez la commande d’interface de ligne de commande Azure [az appservice list-locations](/cli/azure/appservice#list-locations) pour répertorier les emplacements disponibles.</span><span class="sxs-lookup"><span data-stu-id="b5288-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="b5288-162">Création d’un compte Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b5288-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="b5288-163">Créez un compte Cosmos DB à l’aide de la commande [az cosmosdb create](/cli/azure/cosmosdb#create).</span><span class="sxs-lookup"><span data-stu-id="b5288-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="b5288-164">Dans la commande suivante, remplacez l’espace réservé *\<nom_cosmosdb>* par un nom unique Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5288-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="b5288-165">Ce nom est utilisé en tant que point de terminaison Cosmos DB, `https://<cosmosdb_name>.documents.azure.com/`. Pour cette raison, le nom doit être unique sur l’ensemble des comptes Cosmos DB dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="b5288-166">Le nom ne peut contenir que des minuscules, des chiffres, le tiret -) et doit compter entre 3 et 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="b5288-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="b5288-167">Le paramètre *--kind MongoDB* prend en charge les connexions clientes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b5288-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="b5288-168">Une fois le compte Cosmos DB créé, Azure CLI affiche des informations similaires à celles de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5288-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="b5288-169">Connecter l’application à la production MongoDB</span><span class="sxs-lookup"><span data-stu-id="b5288-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="b5288-170">Pendant cette étape, vous connectez votre exemple d’application MEAN.js à la base de données Cosmos DB que vous venez de créer, en utilisant une chaîne de connexion MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b5288-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="b5288-171">Récupérer la clé de la base de données</span><span class="sxs-lookup"><span data-stu-id="b5288-171">Retrieve the database key</span></span>

<span data-ttu-id="b5288-172">Pour se connecter à la base de données Cosmos DB, vous avez besoin de la clé de la base de données.</span><span class="sxs-lookup"><span data-stu-id="b5288-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="b5288-173">Utilisez la commande [az documentdb list-keys](/cli/azure/cosmosdb#list-keys) pour récupérer la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="b5288-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="b5288-174">L’interface de ligne de commande Azure montre des informations semblables à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b5288-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiez la valeur de `primaryMasterKey`. <span data-ttu-id="b5288-176">Vous aurez besoin de ces informations dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="b5288-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="b5288-177">Configurer la chaîne de connexion dans votre application Node.js</span><span class="sxs-lookup"><span data-stu-id="b5288-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="b5288-178">Dans votre référentiel MEAN.js, ouvrez _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="b5288-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="b5288-179">Dans l’objet `db`, mettez à jour la valeur de `uri` :</span><span class="sxs-lookup"><span data-stu-id="b5288-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="b5288-180">Remplacez les deux espaces réservés  *\<cosmosdb_name>* par votre nom de base de données Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5288-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="b5288-181">Remplacez l’espace réservé  *\<primary_master_key>* par la clé copiée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="b5288-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="b5288-182">Le code suivant montre l’objet `db` :</span><span class="sxs-lookup"><span data-stu-id="b5288-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="b5288-183">L’option `ssl=true` est requise, car [Cosmos DB nécessite SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="b5288-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="b5288-184">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b5288-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="b5288-185">Tester l’application en mode de production</span><span class="sxs-lookup"><span data-stu-id="b5288-185">Test the application in production mode</span></span> 

<span data-ttu-id="b5288-186">Exécutez la commande suivante pour réduire et regrouper des scripts pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b5288-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="b5288-187">Ce processus génère les fichiers nécessaires à l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b5288-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="b5288-188">Exécutez la commande suivante pour utiliser la chaîne de connexion que vous avez configurée dans _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="b5288-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="b5288-189">`NODE_ENV=production` définit la variable d’environnement qui indique à Node.js de s’exécuter dans l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b5288-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="b5288-190">`node server.js` démarre le serveur Node.js avec `server.js` à la racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="b5288-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="b5288-191">Voici comment est chargée votre application Node.js dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="b5288-192">Lorsque l’application est chargée, assurez-vous qu’elle s’exécute dans l’environnement de production :</span><span class="sxs-lookup"><span data-stu-id="b5288-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="b5288-193">Accédez à http://localhost:8443 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="b5288-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="b5288-194">Cliquez sur **S’inscrire** dans le menu supérieur et créez un utilisateur test.</span><span class="sxs-lookup"><span data-stu-id="b5288-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="b5288-195">Si vous parvenez à créer un utilisateur et à vous connecter, votre application écrit les données dans la base de données Cosmo DB dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="b5288-196">Dans le terminal, arrêtez Node.js en tapant `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="b5288-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="b5288-197">Déployer des applications dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-197">Deploy app to Azure</span></span>

<span data-ttu-id="b5288-198">Dans cette étape, vous allez déployer dans Azure App Service votre application Node.js connectée à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b5288-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="b5288-199">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="b5288-199">Create an App Service plan</span></span>

<span data-ttu-id="b5288-200">Créez un plan App Service avec la commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="b5288-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="b5288-201">L’exemple suivant crée un plan App Service nommé _myAppServicePlan_ en indiquant le niveau tarifaire **Gratuit** :</span><span class="sxs-lookup"><span data-stu-id="b5288-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="b5288-202">Lorsque le plan App Service est créé, l’interface Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5288-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="b5288-203">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="b5288-203">Create a web app</span></span>

<span data-ttu-id="b5288-204">Créez une application web dans le plan App Service `myAppServicePlan` avec la commande [az webapp create](/cli/azure/webapp#create).</span><span class="sxs-lookup"><span data-stu-id="b5288-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="b5288-205">L’application web vous offre un espace d’hébergement pour déployer votre code, et fournit une URL pour vous permettre d’afficher l’application déployée.</span><span class="sxs-lookup"><span data-stu-id="b5288-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="b5288-206">Utilisez  pour créer l’application web.</span><span class="sxs-lookup"><span data-stu-id="b5288-206">Use  to create the web app.</span></span> 

<span data-ttu-id="b5288-207">Dans la commande suivante, remplacez l’espace réservé *\<app_name>* par le nom unique de votre application.</span><span class="sxs-lookup"><span data-stu-id="b5288-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="b5288-208">Ce nom est utilisé dans l’URL par défaut de l’application web. Pour cette raison, ce nom doit être unique sur l’ensemble des applications dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b5288-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="b5288-209">Une fois l’application web créée, Azure CLI affiche des informations similaires à celles de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5288-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="b5288-210">Configurer une variable d’environnement</span><span class="sxs-lookup"><span data-stu-id="b5288-210">Configure an environment variable</span></span>

<span data-ttu-id="b5288-211">Précédemment dans ce didacticiel, vous avez codé en dur la chaîne de connexion de la base de données dans _config/env/prodution.js_.</span><span class="sxs-lookup"><span data-stu-id="b5288-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="b5288-212">Conformément aux meilleures pratiques de sécurité, vous allez vouloir conserver ces données sensibles en dehors de votre référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="b5288-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="b5288-213">Pour l’application en cours d’exécution dans Azure, vous utiliserez plutôt une variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="b5288-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="b5288-214">Dans App Service, vous définissez les variables d’environnement en tant que _paramètres d’application_ à l’aide de la commande [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update).</span><span class="sxs-lookup"><span data-stu-id="b5288-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="b5288-215">L’exemple suivant configure un paramètre d’application `MONGODB_URI` dans votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="b5288-216">Remplacez les espaces réservés *\<app_name>*, *\<cosmosdb_name>*, et *\<primary_master_key>*.</span><span class="sxs-lookup"><span data-stu-id="b5288-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="b5288-217">Dans le code Node.js, vous accédez à ce paramètre d’application avec `process.env.MONGODB_URI`, comme vous accéderiez à n’importe quelle variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="b5288-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="b5288-218">À présent, annulez vos modifications apportées à _config/env/production.js_ à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b5288-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="b5288-219">Ouvrez à nouveau _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="b5288-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="b5288-220">Notez que l’application MEAN.js par défaut est déjà configurée pour utiliser la variable d’environnement `MONGODB_URI` que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="b5288-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="b5288-221">Configurer le déploiement Git local</span><span class="sxs-lookup"><span data-stu-id="b5288-221">Configure local git deployment</span></span> 

<span data-ttu-id="b5288-222">Utilisez la commande [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) pour créer des informations d’identification de déploiement.</span><span class="sxs-lookup"><span data-stu-id="b5288-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="b5288-223">Vous pouvez déployer votre application dans Azure App Service de plusieurs façons, notamment FTP, Git local ainsi que GitHub, Visual Studio Team Services et Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="b5288-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="b5288-224">Pour les sites FTP et Git locaux, il est nécessaire de disposer d’un utilisateur de déploiement configuré sur le serveur pour authentifier votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="b5288-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="b5288-225">Cet utilisateur de déploiement se situe au niveau des comptes et est différent de votre compte d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="b5288-226">Vous n’avez à configurer cet utilisateur de déploiement qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="b5288-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="b5288-227">Dans la commande suivante, remplacez les valeurs *\<user-name>* et *\<password>* par le nom et le mot de passe du nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b5288-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="b5288-228">Le nom d’utilisateur doit être unique.</span><span class="sxs-lookup"><span data-stu-id="b5288-228">The user name must be unique.</span></span> <span data-ttu-id="b5288-229">Le mot de passe doit comporter au moins huit caractères et inclure deux des trois éléments suivants : lettres, chiffres et symboles.</span><span class="sxs-lookup"><span data-stu-id="b5288-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="b5288-230">Si vous obtenez une erreur ` 'Conflict'. Details: 409`, modifiez le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b5288-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="b5288-231">Si vous obtenez une erreur ` 'Bad Request'. Details: 400`, utilisez un mot de passe plus fort.</span><span class="sxs-lookup"><span data-stu-id="b5288-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="b5288-232">Enregistrez le nom d’utilisateur et le mot de passe pour les utiliser dans les étapes ultérieures du déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="b5288-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="b5288-233">Utilisez la commande [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) pour configurer l’accès Git local à l’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="b5288-234">Lorsque l’utilisateur du déploiement est configuré, l’interface Azure CLI affiche l’URL de déploiement pour votre application web Azure au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b5288-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="b5288-235">Copiez la sortie du terminal, car elle sera utilisée à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="b5288-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="b5288-236">Effectuer une transmission de type push vers Azure à partir de Git</span><span class="sxs-lookup"><span data-stu-id="b5288-236">Push to Azure from Git</span></span>

<span data-ttu-id="b5288-237">Ajoutez un référentiel distant Azure dans votre référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="b5288-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="b5288-238">Effectuez une transmission de type push vers le référentiel distant Azure pour déployer votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="b5288-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="b5288-239">Le mot de passe que vous avez fourni précédemment dans le cadre de la création de l’utilisateur du déploiement vous sera demandé.</span><span class="sxs-lookup"><span data-stu-id="b5288-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="b5288-240">Au cours du déploiement, Azure App Service communique sa progression avec Git.</span><span class="sxs-lookup"><span data-stu-id="b5288-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="b5288-241">Vous remarquerez peut-être que le processus de déploiement exécute [Gulp](http://gulpjs.com/) après `npm install`.</span><span class="sxs-lookup"><span data-stu-id="b5288-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="b5288-242">App Service n’exécute pas les tâches Gulp ou Grunt pendant le déploiement ; cet exemple de référentiel possède donc deux fichiers supplémentaires dans son répertoire racine pour l’activer :</span><span class="sxs-lookup"><span data-stu-id="b5288-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="b5288-243">_.deployment_ : ce fichier indique à App Service d’exécuter `bash deploy.sh` en tant que script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b5288-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="b5288-244">_deploy.sh_ : le script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b5288-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="b5288-245">Si vous examinez le fichier, vous verrez qu’il exécute `gulp prod` après `npm install` et `bower install`.</span><span class="sxs-lookup"><span data-stu-id="b5288-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="b5288-246">Vous pouvez utiliser cette approche pour ajouter une étape à votre déploiement Git.</span><span class="sxs-lookup"><span data-stu-id="b5288-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="b5288-247">Notez que si vous redémarrez votre application web Azure à tout moment, App Service ne réexécute pas ces tâches d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="b5288-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="b5288-248">Rechercher l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="b5288-249">Accédez à l’application web déployée à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b5288-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="b5288-250">Cliquez sur **S’inscrire** dans le menu supérieur et créez un utilisateur fictif.</span><span class="sxs-lookup"><span data-stu-id="b5288-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="b5288-251">Si vous réussissez, et si l’application se connecte automatiquement à l’utilisateur créé, cela signifie que votre application MEAN.js dans Azure dispose d’une connectivité à la base de données MongoDB (Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="b5288-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![Application MEAN.js exécutée dans Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="b5288-253">Sélectionnez **Admin > Manage Articles** (Administrateur > Gérer les articles) pour ajouter des articles.</span><span class="sxs-lookup"><span data-stu-id="b5288-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="b5288-254">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="b5288-254">**Congratulations!**</span></span> <span data-ttu-id="b5288-255">Vous exécutez une application Node.js orientée données dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b5288-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="b5288-256">Mettre à jour le modèle de données et redéployer</span><span class="sxs-lookup"><span data-stu-id="b5288-256">Update data model and redeploy</span></span>

<span data-ttu-id="b5288-257">Dans cette étape, vous allez changer le modèle de données `article` et publier vos modifications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="b5288-258">Mettre à jour le modèle de données</span><span class="sxs-lookup"><span data-stu-id="b5288-258">Update the data model</span></span>

<span data-ttu-id="b5288-259">Ouvrez _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="b5288-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="b5288-260">Dans `ArticleSchema`, ajoutez un type `String` appelé `comment`.</span><span class="sxs-lookup"><span data-stu-id="b5288-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="b5288-261">Lorsque vous aurez terminé, votre code de schéma doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b5288-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-the-articles-code"></a><span data-ttu-id="b5288-262">Mettre à jour le code d’articles</span><span class="sxs-lookup"><span data-stu-id="b5288-262">Update the articles code</span></span>

<span data-ttu-id="b5288-263">Mettez à jour le reste de votre code `articles` afin d’utiliser `comment`.</span><span class="sxs-lookup"><span data-stu-id="b5288-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="b5288-264">Vous avez cinq fichiers à modifier : le contrôleur de serveur et les quatre vues clientes.</span><span class="sxs-lookup"><span data-stu-id="b5288-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="b5288-265">Ouvrez _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="b5288-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="b5288-266">Dans la fonction `update`, ajoutez une affectation de `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="b5288-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="b5288-267">Le code suivant illustre la fonction `update` achevée :</span><span class="sxs-lookup"><span data-stu-id="b5288-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="b5288-268">Ouvrez _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="b5288-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="b5288-269">Juste au-dessus de la balise de fermeture `</section>`, ajoutez la ligne suivante pour afficher `comment` avec le reste des données de l’article :</span><span class="sxs-lookup"><span data-stu-id="b5288-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="b5288-270">Ouvrez _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="b5288-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="b5288-271">Juste au-dessus de la balise de fermeture `</a>`, ajoutez la ligne suivante pour afficher `comment` avec le reste des données de l’article :</span><span class="sxs-lookup"><span data-stu-id="b5288-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="b5288-272">Ouvrez _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="b5288-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="b5288-273">À l’intérieur de l’élément `<div class="list-group">`, juste au-dessus de la balise de fermeture `</a>`, ajoutez la ligne suivante pour afficher `comment` avec le reste des données de l’article :</span><span class="sxs-lookup"><span data-stu-id="b5288-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="b5288-274">Ouvrez _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="b5288-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="b5288-275">Recherchez l’élément `<div class="form-group">` qui contient le bouton Envoyer, qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="b5288-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="b5288-276">Juste au-dessus de cette balise, ajoutez un autre élément `<div class="form-group">` permettant aux utilisateurs de modifier le champ `comment`.</span><span class="sxs-lookup"><span data-stu-id="b5288-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="b5288-277">Votre nouvel élément doit avoir l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="b5288-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="b5288-278">Tester vos modifications en local</span><span class="sxs-lookup"><span data-stu-id="b5288-278">Test your changes locally</span></span>

<span data-ttu-id="b5288-279">Enregistrez toutes vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b5288-279">Save all your changes.</span></span>

<span data-ttu-id="b5288-280">Testez de nouveau vos modifications en mode de production.</span><span class="sxs-lookup"><span data-stu-id="b5288-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="b5288-281">N’oubliez pas que votre _config/env/production.js_ a été rétabli et que la variable d’environnement `MONGODB_URI` est définie uniquement dans votre application web Azure, et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="b5288-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="b5288-282">Si vous examinez le fichier de configuration, vous verrez que la configuration de production utilise par défaut une base de données MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b5288-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="b5288-283">Cela vous évite de toucher aux données de production lorsque vous testez vos changements de code en local.</span><span class="sxs-lookup"><span data-stu-id="b5288-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="b5288-284">Accédez à `http://localhost:8443` dans un navigateur et assurez-vous que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="b5288-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="b5288-285">Sélectionnez **Admin > Manage Articles** (Administrateur > Gérer les articles), puis ajoutez un article en cliquant sur le bouton **+**.</span><span class="sxs-lookup"><span data-stu-id="b5288-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="b5288-286">Vous voyez maintenant la nouvelle zone de texte `Comment`.</span><span class="sxs-lookup"><span data-stu-id="b5288-286">You see the new `Comment` textbox now.</span></span>

![Champ de commentaire ajouté aux Articles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="b5288-288">Dans le terminal, arrêtez Node.js en tapant `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="b5288-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="b5288-289">Publier les modifications dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-289">Publish changes to Azure</span></span>

<span data-ttu-id="b5288-290">Validez vos modifications dans Git, puis envoyez les modifications de code à Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="b5288-291">Une fois le `git push` terminé, accédez à votre application web Azure et essayez la nouvelle fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b5288-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Modifications du modèle et de la base de données publiées dans Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="b5288-293">Si vous avez ajouté des articles précédemment, vous pouvez toujours les visualiser.</span><span class="sxs-lookup"><span data-stu-id="b5288-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="b5288-294">Les données existantes dans votre Cosmos DB ne sont pas perdues.</span><span class="sxs-lookup"><span data-stu-id="b5288-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="b5288-295">De plus, les mises à jour que vous appliquez au schéma de données n’affectent pas vos données existantes.</span><span class="sxs-lookup"><span data-stu-id="b5288-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="b5288-296">Diffuser les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="b5288-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="b5288-297">Pendant l’exécution de votre application Node.js dans Azure App Service, vous pouvez acheminer les journaux de la console vers votre terminal.</span><span class="sxs-lookup"><span data-stu-id="b5288-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="b5288-298">De cette façon, vous pouvez obtenir les mêmes messages de diagnostic pour vous aider à déboguer les erreurs d’application.</span><span class="sxs-lookup"><span data-stu-id="b5288-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="b5288-299">Pour démarrer la diffusion de journaux, utilisez la commande [az webapp log tail](/cli/azure/webapp/log#tail).</span><span class="sxs-lookup"><span data-stu-id="b5288-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="b5288-300">Une fois que la diffusion a démarré, actualisez votre application web Azure dans le navigateur pour générer un trafic web.</span><span class="sxs-lookup"><span data-stu-id="b5288-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="b5288-301">Vous voyez maintenant les journaux de la console acheminés vers votre terminal.</span><span class="sxs-lookup"><span data-stu-id="b5288-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="b5288-302">Pour arrêter la diffusion de journaux à tout moment, tapez `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="b5288-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="b5288-303">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-303">Manage your Azure web app</span></span>

<span data-ttu-id="b5288-304">Accédez au [portail Azure](https://portal.azure.com) pour voir l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="b5288-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="b5288-305">Dans le menu de gauche, cliquez sur **App Services**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="b5288-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="b5288-307">Par défaut, le portail affiche la page **Vue d’ensemble** de votre application web.</span><span class="sxs-lookup"><span data-stu-id="b5288-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="b5288-308">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="b5288-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="b5288-309">Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="b5288-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="b5288-310">Les onglets sur le côté gauche de la page affichent les différentes pages de configuration que vous pouvez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b5288-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Page App Service du Portail Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="b5288-312">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5288-312">Next steps</span></span>

<span data-ttu-id="b5288-313">Vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5288-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b5288-314">Créer une base de données MongoDB dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="b5288-315">Connecter une application Node.js à MongoDB</span><span class="sxs-lookup"><span data-stu-id="b5288-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="b5288-316">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="b5288-317">Mettre à jour le modèle de données et redéployer l’application</span><span class="sxs-lookup"><span data-stu-id="b5288-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="b5288-318">Diffuser des journaux à partir d’Azure vers votre terminal</span><span class="sxs-lookup"><span data-stu-id="b5288-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="b5288-319">Gérer l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="b5288-320">Passez au didacticiel suivant pour découvrir comment mapper un nom DNS personnalisé à votre application web.</span><span class="sxs-lookup"><span data-stu-id="b5288-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="b5288-321">Mapper un nom DNS personnalisé existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="b5288-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
