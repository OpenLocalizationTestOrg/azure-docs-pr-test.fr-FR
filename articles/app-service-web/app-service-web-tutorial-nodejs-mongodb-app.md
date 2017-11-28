---
title: aaaBuild une application web Node.js et MongoDB dans Azure | Documents Microsoft
description: "Découvrez comment tooget une application Node.js dans Azure, avec une connexion tooa Cosmos base de données de base de données avec une chaîne de connexion MongoDB."
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
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="0562d-103">Créer une application web Node.js et MongoDB dans Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="0562d-104">Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0562d-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="0562d-105">Ce didacticiel montre comment toocreate un Node.js web application dans Azure et le connecter tooa MongoDB base de données.</span><span class="sxs-lookup"><span data-stu-id="0562d-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="0562d-106">Lorsque vous aurez terminé, vous disposerez d’une application MEAN (MongoDB, Express, AngularJS et Node.js) exécutée sous [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0562d-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="0562d-107">Par souci de simplicité, exemple d’application hello utilise hello [framework de web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="0562d-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Application MEAN.js exécutée dans Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="0562d-109">Ce que vous allez apprendre :</span><span class="sxs-lookup"><span data-stu-id="0562d-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0562d-110">Créer une base de données MongoDB dans Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="0562d-111">Se connecter à un tooMongoDB d’application Node.js</span><span class="sxs-lookup"><span data-stu-id="0562d-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="0562d-112">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="0562d-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="0562d-113">Mettre à jour le modèle de données hello et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="0562d-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="0562d-114">Diffusion des journaux de diagnostic à partir d’Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="0562d-115">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0562d-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0562d-116">Prerequisites</span></span>

<span data-ttu-id="0562d-117">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="0562d-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="0562d-118">Installez Git</span><span class="sxs-lookup"><span data-stu-id="0562d-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="0562d-119">Installez Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="0562d-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="0562d-120">[Installer Gulp.js](http://gulpjs.com/) (requis par [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="0562d-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="0562d-121">Installez et exécutez MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="0562d-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0562d-122">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0562d-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0562d-123">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0562d-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0562d-124">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0562d-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="0562d-125">Tester la base de données MongoDB locale</span><span class="sxs-lookup"><span data-stu-id="0562d-125">Test local MongoDB</span></span>

<span data-ttu-id="0562d-126">Fenêtre de terminal ouverte hello et `cd` toohello `bin` répertoire de votre installation MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0562d-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="0562d-127">Vous pouvez utiliser cette fenêtre de terminal de toorun toutes les commandes hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0562d-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="0562d-128">Exécutez `mongo` sur le serveur de MongoDB local hello terminal tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="0562d-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="0562d-129">Si la connexion est établie, cela signifie que votre base de données MongoDB est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0562d-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="0562d-130">Dans le cas contraire, assurez-vous que votre base de données MongoDB locale est démarré en suivant les étapes de hello à [installer MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="0562d-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="0562d-131">Souvent, MongoDB est installé, mais vous devez toujours toostart en réexécutant `mongod`.</span><span class="sxs-lookup"><span data-stu-id="0562d-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="0562d-132">Lorsque vous avez terminé votre base de données MongoDB de test, tapez `Ctrl+C` Bonjour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="0562d-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="0562d-133">Créer une application Node.js locale</span><span class="sxs-lookup"><span data-stu-id="0562d-133">Create local Node.js app</span></span>

<span data-ttu-id="0562d-134">Dans cette étape, vous définir un projet local Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="0562d-135">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="0562d-135">Clone hello sample application</span></span>

<span data-ttu-id="0562d-136">Dans la fenêtre de terminal hello, `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="0562d-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="0562d-137">Exécutez hello suivant le dépôt d’exemples de commande tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="0562d-138">Ce dépôt d’exemples contient une copie de hello [MEAN.js référentiel](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="0562d-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="0562d-139">Il est modifié toorun sur le Service d’application (pour plus d’informations, consultez le référentiel de MEAN.js hello [fichier Lisez-moi](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="0562d-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="0562d-140">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="0562d-140">Run hello application</span></span>

<span data-ttu-id="0562d-141">Exécutez hello suivant des packages de commandes tooinstall hello requis et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="0562d-142">Lors de l’application hello est entièrement chargée, vous voyez quelque chose de similaire toohello message suivant :</span><span class="sxs-lookup"><span data-stu-id="0562d-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="0562d-143">Accédez toohttp://localhost:3000 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="0562d-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="0562d-144">Cliquez sur **s’inscrire** hello menu supérieur et créer un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="0562d-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="0562d-145">Hello MEAN.js exemple d’application stocke les données utilisateur dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="0562d-146">Si vous parvenez à la création d’un utilisateur et l’ouverture de session, votre application écrit les données toohello MongoDB base de données locale.</span><span class="sxs-lookup"><span data-stu-id="0562d-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js se connecte correctement tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="0562d-148">Sélectionnez **administration > Gérer les Articles** tooadd certains articles.</span><span class="sxs-lookup"><span data-stu-id="0562d-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="0562d-149">Appuyez sur la touche Node.js à tout moment, toostop `Ctrl+C` Bonjour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="0562d-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="0562d-150">Créer une base de données MongoDB de production</span><span class="sxs-lookup"><span data-stu-id="0562d-150">Create production MongoDB</span></span>

<span data-ttu-id="0562d-151">Dans cette étape, vous allez créer une base de données MongoDB dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="0562d-152">Lorsque votre application est déployée tooAzure, il utilise cette base de données du cloud.</span><span class="sxs-lookup"><span data-stu-id="0562d-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="0562d-153">Pour MongoDB, ce didacticiel utilise [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0562d-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="0562d-154">Cosmos DB prend en charge les connexions client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0562d-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="0562d-155">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="0562d-155">Log in tooAzure</span></span>

<span data-ttu-id="0562d-156">Vous allez utiliser hello Azure CLI 2.0 toocreate hello ressources nécessaires toohost votre application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="0562d-157">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="0562d-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="0562d-158">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0562d-158">Create a resource group</span></span>

<span data-ttu-id="0562d-159">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="0562d-160">Hello exemple suivant crée un groupe de ressources dans la région Europe de l’ouest hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="0562d-161">Hello d’utilisation [Liste emplacements az appservice](/cli/azure/appservice#list-locations) les emplacements disponibles toolist de commande CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="0562d-162">Création d’un compte Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0562d-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="0562d-163">Créer un compte de base de données Cosmos avec hello [az cosmosdb créer](/cli/azure/cosmosdb#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="0562d-164">Bonjour suivant de commande, remplacez par un nom unique de la base de données Cosmos pour hello  *\<cosmosdb_name >* espace réservé.</span><span class="sxs-lookup"><span data-stu-id="0562d-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="0562d-165">Ce nom est utilisé en tant que partie hello du point de terminaison de base de données Cosmos hello `https://<cosmosdb_name>.documents.azure.com/`, de sorte que le nom hello doit toobe unique dans tous les comptes de base de données Cosmos dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="0562d-166">Hello nom doit contenir uniquement des lettres minuscules, des chiffres et des caractères de trait d’union (-) hello et doit être comprise entre 3 et 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="0562d-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="0562d-167">Hello *--MongoDB kind* paramètre permet les connexions clientes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0562d-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="0562d-168">Lorsque hello Cosmos DB compte est créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0562d-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="0562d-169">Connecter l’application tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="0562d-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="0562d-170">Dans cette étape, vous vous connectez votre MEAN.js application toohello Cosmos DB base de données exemple que vous venez de créer, à l’aide d’une chaîne de connexion MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0562d-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="0562d-171">Récupérer la clé de base de données hello</span><span class="sxs-lookup"><span data-stu-id="0562d-171">Retrieve hello database key</span></span>

<span data-ttu-id="0562d-172">base de données de la base de données Cosmos tooconnect toohello, vous devez clé de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="0562d-173">Hello d’utilisation [liste clés az cosmosdb](/cli/azure/cosmosdb#list-keys) clé primaire de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="0562d-174">Hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0562d-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiez la valeur hello `primaryMasterKey`. <span data-ttu-id="0562d-176">Vous avez besoin de ces informations dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="0562d-177">Configurer la chaîne de connexion hello dans votre application Node.js</span><span class="sxs-lookup"><span data-stu-id="0562d-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="0562d-178">Dans votre référentiel MEAN.js, ouvrez _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0562d-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="0562d-179">Bonjour `db` d’objet, de mettre à jour la valeur hello `uri`:</span><span class="sxs-lookup"><span data-stu-id="0562d-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="0562d-180">Remplacez hello deux  *\<cosmosdb_name >* des espaces réservés avec votre nom de base de données de base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0562d-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="0562d-181">Remplacez hello  *\<primary_master_key >* espace réservé avec clé hello copiée à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="0562d-182">Hello de code suivant montre hello `db` objet :</span><span class="sxs-lookup"><span data-stu-id="0562d-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="0562d-183">Hello `ssl=true` option est requise car [Cosmos DB requiert SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="0562d-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="0562d-184">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="0562d-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="0562d-185">Tester l’application hello en mode de production</span><span class="sxs-lookup"><span data-stu-id="0562d-185">Test hello application in production mode</span></span> 

<span data-ttu-id="0562d-186">Exécutez hello suivant des scripts de commande toominify et de groupe pour l’environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="0562d-187">Ce processus génère des fichiers hello requis par l’environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="0562d-188">Exécution hello suivant de chaîne de connexion commande toouse hello vous avez configuré dans _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0562d-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="0562d-189">`NODE_ENV=production`définit la variable d’environnement hello indiquant Node.js toorun dans l’environnement de production hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="0562d-190">`node server.js`démarre hello serveur Node.js avec `server.js` racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="0562d-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="0562d-191">Voici comment est chargée votre application Node.js dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="0562d-192">Lors de l’application hello est chargée, vérifiez toomake qu’il fonctionne dans un environnement de production hello :</span><span class="sxs-lookup"><span data-stu-id="0562d-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="0562d-193">Accédez toohttp://localhost:8443 dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="0562d-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="0562d-194">Cliquez sur **s’inscrire** hello menu supérieur et créer un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="0562d-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="0562d-195">Si vous êtes réussi de création d’un utilisateur et de l’ouverture de session, puis votre application est l’écriture de base de données toohello Cosmos DB dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="0562d-196">Bonjour Terminal Server, arrêtez Node.js en tapant `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="0562d-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="0562d-197">Déployer l’application tooAzure</span><span class="sxs-lookup"><span data-stu-id="0562d-197">Deploy app tooAzure</span></span>

<span data-ttu-id="0562d-198">Dans cette étape, vous déployez votre tooAzure d’application connectée MongoDB de Node.js du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="0562d-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="0562d-199">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="0562d-199">Create an App Service plan</span></span>

<span data-ttu-id="0562d-200">Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="0562d-201">Hello exemple suivant crée un plan App Service nommé _myAppServicePlan_ à l’aide de hello **libre** niveau tarifaire :</span><span class="sxs-lookup"><span data-stu-id="0562d-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="0562d-202">Lorsque hello plan App Service est créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0562d-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="0562d-203">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="0562d-203">Create a web app</span></span>

<span data-ttu-id="0562d-204">Créer une application web Bonjour `myAppServicePlan` plan App Service avec hello [az webapp créer](/cli/azure/webapp#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="0562d-205">fournit les application Hello web vous un hébergement toodeploy votre code et de l’espace fournit une URL pour vous tooview hello déployé l’application.</span><span class="sxs-lookup"><span data-stu-id="0562d-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="0562d-206">Utilisez l’application web toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="0562d-207">Bonjour suivant de commande, remplacez hello  *\<nom_application >* espace réservé avec un nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="0562d-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="0562d-208">Ce nom est utilisé en tant que partie hello d’URL par défaut de hello pour l’application web de hello, le nom hello doit toobe unique entre toutes les applications dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0562d-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="0562d-209">Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0562d-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="0562d-210">Configurer une variable d’environnement</span><span class="sxs-lookup"><span data-stu-id="0562d-210">Configure an environment variable</span></span>

<span data-ttu-id="0562d-211">Plus haut dans hello didacticiel, vous codé en dur hello de base de données chaîne de connexion dans _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0562d-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="0562d-212">En fonction de la meilleure pratique de sécurité, vous souhaitez tookeep les données sensibles en dehors de votre référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="0562d-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="0562d-213">Pour l’application en cours d’exécution dans Azure, vous utiliserez plutôt une variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="0562d-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="0562d-214">Dans le Service d’application, vous définissez les variables d’environnement _paramètres de l’application_ à l’aide de hello [az webapp configuration appsettings mettre à jour](/cli/azure/webapp/config/appsettings#update) commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="0562d-215">Hello exemple suivant configure un `MONGODB_URI` paramètre d’application dans votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="0562d-216">Remplacez hello  *\<nom_application >*,  *\<cosmosdb_name >*, et  *\<primary_master_key >* des espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="0562d-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="0562d-217">Dans le code Node.js, vous accédez à ce paramètre d’application avec `process.env.MONGODB_URI`, comme vous accéderiez à n’importe quelle variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="0562d-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="0562d-218">Annuler maintenant, votre too_config/env/production.js_ modifications par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0562d-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="0562d-219">Ouvrez à nouveau _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0562d-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="0562d-220">Notez cette application de MEAN.js hello par défaut est déjà configuré toouse hello `MONGODB_URI` variable d’environnement que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="0562d-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="0562d-221">Configurer le déploiement Git local</span><span class="sxs-lookup"><span data-stu-id="0562d-221">Configure local git deployment</span></span> 

<span data-ttu-id="0562d-222">Hello d’utilisation [az webapp utilisateur de déploiement défini](/cli/azure/webapp/deployment/user#set) toocreate les informations d’identification pour le déploiement de la commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="0562d-223">Vous pouvez déployer votre application de tooAzure du Service d’applications de différentes manières, notamment FTP, Git local, GitHub, Visual Studio Team Services et BitBucket.</span><span class="sxs-lookup"><span data-stu-id="0562d-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="0562d-224">Pour FTP et Git local, il est nécessaire toohave un utilisateur du déploiement configuré sur hello server tooauthenticate votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="0562d-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="0562d-225">Cet utilisateur de déploiement se situe au niveau des comptes et est différent de votre compte d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="0562d-226">Vous ne devez tooconfigure cet utilisateur de déploiement une fois.</span><span class="sxs-lookup"><span data-stu-id="0562d-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="0562d-227">Bonjour suivant de commande, remplacez  *\<nom d’utilisateur >* et  *\<mot de passe >* avec un nouveau nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0562d-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="0562d-228">nom d’utilisateur Hello doit être unique.</span><span class="sxs-lookup"><span data-stu-id="0562d-228">hello user name must be unique.</span></span> <span data-ttu-id="0562d-229">Hello mot de passe doit comporter au moins huit caractères, avec deux hello suivant trois éléments : des lettres, des chiffres, des symboles.</span><span class="sxs-lookup"><span data-stu-id="0562d-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="0562d-230">Si vous obtenez un ` 'Conflict'. Details: 409` erreur, le nom d’utilisateur de modification hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="0562d-231">Si vous obtenez une erreur ` 'Bad Request'. Details: 400`, utilisez un mot de passe plus fort.</span><span class="sxs-lookup"><span data-stu-id="0562d-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="0562d-232">Enregistrement hello nom utilisateur et mot de passe pour une utilisation dans les étapes ultérieures lorsque vous déployez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="0562d-233">Hello d’utilisation [source liée à un déploiement de webapp dans az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) commande tooconfigure Git accès toohello Azure l’application web locale.</span><span class="sxs-lookup"><span data-stu-id="0562d-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="0562d-234">Lorsque l’utilisateur du déploiement hello est configuré, hello CLI d’Azure affiche hello les URL de déploiement pour votre application web Azure Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="0562d-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="0562d-235">Copiez hello la sortie à partir de Terminal Server hello, car il sera utilisé à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="0562d-236">TooAzure par émission de données à partir de Git</span><span class="sxs-lookup"><span data-stu-id="0562d-236">Push tooAzure from Git</span></span>

<span data-ttu-id="0562d-237">Ajouter un référentiel Git Azure tooyour à distance.</span><span class="sxs-lookup"><span data-stu-id="0562d-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="0562d-238">Push toohello Azure toodeploy à distance de votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="0562d-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="0562d-239">Vous demandera de mot de passe hello fourni précédemment dans le cadre de la création de l’utilisateur du déploiement hello hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="0562d-240">Au cours du déploiement, Azure App Service communique sa progression avec Git.</span><span class="sxs-lookup"><span data-stu-id="0562d-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="0562d-241">Vous pouvez remarquer que le processus de déploiement hello s’exécute [Gulp](http://gulpjs.com/) après `npm install`.</span><span class="sxs-lookup"><span data-stu-id="0562d-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="0562d-242">Service de l’application ne s’exécute pas Gulp ou Grunt tâches durant le déploiement, donc ce référentiel exemple a deux autres fichiers dans son tooenable du répertoire racine qu’il :</span><span class="sxs-lookup"><span data-stu-id="0562d-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="0562d-243">_.Deployment_ -ce fichier indique au Service d’applications toorun `bash deploy.sh` en tant que script de déploiement personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="0562d-244">_Deploy.sh_ -hello du script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0562d-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="0562d-245">Si vous passez en revue le fichier de hello, vous verrez qu’il s’exécute `gulp prod` après `npm install` et `bower install`.</span><span class="sxs-lookup"><span data-stu-id="0562d-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="0562d-246">Vous pouvez utiliser cette approche tooadd tout tooyour étape déploiement Git.</span><span class="sxs-lookup"><span data-stu-id="0562d-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="0562d-247">Notez que si vous redémarrez votre application web Azure à tout moment, App Service ne réexécute pas ces tâches d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="0562d-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="0562d-248">Parcourir toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="0562d-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="0562d-249">Parcourir l’application web toohello déployé à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="0562d-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="0562d-250">Cliquez sur **s’inscrire** dans hello menu supérieur et créez un utilisateur fictif.</span><span class="sxs-lookup"><span data-stu-id="0562d-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="0562d-251">Si vous êtes réussie et l’application hello se connecte automatiquement toohello créé l’utilisateur, puis votre application MEAN.js dans Azure a base de données de connectivité toohello (DB Cosmos) de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0562d-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Application MEAN.js exécutée dans Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="0562d-253">Sélectionnez **administration > Gérer les Articles** tooadd certains articles.</span><span class="sxs-lookup"><span data-stu-id="0562d-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="0562d-254">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="0562d-254">**Congratulations!**</span></span> <span data-ttu-id="0562d-255">Vous exécutez une application Node.js orientée données dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0562d-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="0562d-256">Mettre à jour le modèle de données et redéployer</span><span class="sxs-lookup"><span data-stu-id="0562d-256">Update data model and redeploy</span></span>

<span data-ttu-id="0562d-257">Dans cette étape, vous modifiez hello `article` de modèle de données et publier votre tooAzure de modification.</span><span class="sxs-lookup"><span data-stu-id="0562d-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="0562d-258">Mettre à jour le modèle de données hello</span><span class="sxs-lookup"><span data-stu-id="0562d-258">Update hello data model</span></span>

<span data-ttu-id="0562d-259">Ouvrez _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="0562d-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="0562d-260">Dans `ArticleSchema`, ajoutez un type `String` appelé `comment`.</span><span class="sxs-lookup"><span data-stu-id="0562d-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="0562d-261">Lorsque vous aurez terminé, votre code de schéma doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="0562d-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="0562d-262">Mettre à jour le code d’articles hello</span><span class="sxs-lookup"><span data-stu-id="0562d-262">Update hello articles code</span></span>

<span data-ttu-id="0562d-263">Mettre à jour des autres hello votre `articles` toouse de code `comment`.</span><span class="sxs-lookup"><span data-stu-id="0562d-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="0562d-264">Il existe cinq fichiers toomodify : serveur de contrôleur de hello et vues du client hello quatre.</span><span class="sxs-lookup"><span data-stu-id="0562d-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="0562d-265">Ouvrez _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="0562d-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="0562d-266">Bonjour `update` de fonction, ajouter une affectation pour `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="0562d-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="0562d-267">Hello de code suivant montre hello terminée `update` fonction :</span><span class="sxs-lookup"><span data-stu-id="0562d-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="0562d-268">Ouvrez _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0562d-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="0562d-269">Juste au-dessus de fermeture de hello `</section>` , ajoutez hello suivant ligne toodisplay `comment` ainsi que d’autres données de l’article hello hello :</span><span class="sxs-lookup"><span data-stu-id="0562d-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="0562d-270">Ouvrez _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0562d-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="0562d-271">Juste au-dessus de fermeture de hello `</a>` , ajoutez hello suivant ligne toodisplay `comment` ainsi que d’autres données de l’article hello hello :</span><span class="sxs-lookup"><span data-stu-id="0562d-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="0562d-272">Ouvrez _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0562d-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="0562d-273">À l’intérieur hello `<div class="list-group">` élément et juste au-dessus de fermeture de hello `</a>` , ajoutez hello suivant ligne toodisplay `comment` ainsi que d’autres données de l’article hello hello :</span><span class="sxs-lookup"><span data-stu-id="0562d-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="0562d-274">Ouvrez _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0562d-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="0562d-275">Recherche hello `<div class="form-group">` élément qui contient le bouton d’envoi hello, qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="0562d-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="0562d-276">Juste au-dessus de cette balise, ajoutez un autre `<div class="form-group">` élément permettant aux utilisateurs de modifier hello `comment` champ.</span><span class="sxs-lookup"><span data-stu-id="0562d-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="0562d-277">Votre nouvel élément doit avoir l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="0562d-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="0562d-278">Tester vos modifications en local</span><span class="sxs-lookup"><span data-stu-id="0562d-278">Test your changes locally</span></span>

<span data-ttu-id="0562d-279">Enregistrez toutes vos modifications.</span><span class="sxs-lookup"><span data-stu-id="0562d-279">Save all your changes.</span></span>

<span data-ttu-id="0562d-280">Testez de nouveau vos modifications en mode de production.</span><span class="sxs-lookup"><span data-stu-id="0562d-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="0562d-281">N’oubliez pas que votre _config/env/production.js_ a été annulée et hello `MONGODB_URI` variable d’environnement est définie uniquement dans votre application web Azure et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0562d-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="0562d-282">Si vous examinez le fichier de configuration hello, vous trouvez que hello configuration de production par défaut est toouse une base de données MongoDB local.</span><span class="sxs-lookup"><span data-stu-id="0562d-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="0562d-283">Cela vous évite de toucher aux données de production lorsque vous testez vos changements de code en local.</span><span class="sxs-lookup"><span data-stu-id="0562d-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="0562d-284">Accédez trop`http://localhost:8443` dans un navigateur et assurez-vous que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="0562d-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="0562d-285">Sélectionnez **administration > Gérer les Articles**, puis ajouter un article en sélectionnant hello  **+**  bouton.</span><span class="sxs-lookup"><span data-stu-id="0562d-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="0562d-286">Vous consultez hello nouvelle `Comment` textbox maintenant.</span><span class="sxs-lookup"><span data-stu-id="0562d-286">You see hello new `Comment` textbox now.</span></span>

![TooArticles de champ de commentaire ajouté](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="0562d-288">Bonjour Terminal Server, arrêtez Node.js en tapant `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="0562d-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="0562d-289">Publier les modifications tooAzure</span><span class="sxs-lookup"><span data-stu-id="0562d-289">Publish changes tooAzure</span></span>

<span data-ttu-id="0562d-290">Valider les modifications apportées dans Git, puis push tooAzure de modifications de code hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="0562d-291">Une fois hello `git push` terminée, accédez tooyour Azure web app et tester les nouvelles fonctionnalités de hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![Les modifications de modèle et de la base de données publiées tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="0562d-293">Si vous avez ajouté des articles précédemment, vous pouvez toujours les visualiser.</span><span class="sxs-lookup"><span data-stu-id="0562d-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="0562d-294">Les données existantes dans votre Cosmos DB ne sont pas perdues.</span><span class="sxs-lookup"><span data-stu-id="0562d-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="0562d-295">En outre, votre schéma de données pour les mises à jour toohello et conserve vos données existantes intact.</span><span class="sxs-lookup"><span data-stu-id="0562d-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="0562d-296">Diffuser les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="0562d-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="0562d-297">Pendant l’exécution de votre application Node.js dans Azure App Service, vous pouvez obtenir hello console journaux dirigée tooyour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="0562d-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="0562d-298">De cette façon, vous pouvez obtenir hello des messages de diagnostic mêmes toohelp vous déboguez des erreurs d’application.</span><span class="sxs-lookup"><span data-stu-id="0562d-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="0562d-299">journal toostart de diffusion en continu, utilisez hello [la fin du journal de az webapp](/cli/azure/webapp/log#tail) commande.</span><span class="sxs-lookup"><span data-stu-id="0562d-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="0562d-300">Une fois que le journal de diffusion en continu a démarré, actualisez votre application web Azure dans hello navigateur tooget certains types de trafic web.</span><span class="sxs-lookup"><span data-stu-id="0562d-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="0562d-301">Vous voyez maintenant les journaux de la console dirigés tooyour Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="0562d-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="0562d-302">Pour arrêter la diffusion de journaux à tout moment, tapez `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="0562d-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="0562d-303">Gérer votre application web Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-303">Manage your Azure web app</span></span>

<span data-ttu-id="0562d-304">Accédez toohello [portail Azure](https://portal.azure.com) toosee vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="0562d-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="0562d-305">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="0562d-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="0562d-307">Par défaut, le portail de hello affiche de votre application web **vue d’ensemble** page.</span><span class="sxs-lookup"><span data-stu-id="0562d-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="0562d-308">Cette page propose un aperçu de votre application.</span><span class="sxs-lookup"><span data-stu-id="0562d-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="0562d-309">Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="0562d-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="0562d-310">onglets Hello sur le côté gauche de hello de page de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="0562d-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Page App Service du Portail Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="0562d-312">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0562d-312">Next steps</span></span>

<span data-ttu-id="0562d-313">Vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0562d-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0562d-314">Créer une base de données MongoDB dans Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="0562d-315">Se connecter à un tooMongoDB d’application Node.js</span><span class="sxs-lookup"><span data-stu-id="0562d-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="0562d-316">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="0562d-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="0562d-317">Mettre à jour le modèle de données hello et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="0562d-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="0562d-318">Journaux des flux de données à partir d’Azure tooyour Terminal Server</span><span class="sxs-lookup"><span data-stu-id="0562d-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="0562d-319">Gérer l’application hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="0562d-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="0562d-320">Avancer toolearn de didacticiel suivant toohello tooyour l’application web de noms toomap DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0562d-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0562d-321">Mapper une tooAzure de nom DNS personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="0562d-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
