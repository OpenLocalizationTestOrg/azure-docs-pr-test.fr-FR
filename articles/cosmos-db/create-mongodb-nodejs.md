---
title: "aaaConnect un tooAzure d’application MongoDB Cosmos DB à l’aide de Node.js | Documents Microsoft"
description: "Découvrez comment tooconnect un tooAzure d’application existant Node.js MongoDB Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="725f0-103">Azure Cosmos DB : migrer une application web MongoDB Node.js existante</span><span class="sxs-lookup"><span data-stu-id="725f0-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="725f0-104">Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale.</span><span class="sxs-lookup"><span data-stu-id="725f0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="725f0-105">Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="725f0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="725f0-106">Ce démarrage rapide montre comment toouse existant [MongoDB](mongodb-introduction.md) application écrite en Node.js et le connecter à base de données de base de données Azure Cosmos tooyour, qui prend en charge les connexions clientes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="725f0-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="725f0-107">En d’autres termes, votre application Node.js sait uniquement qu’il se connecte à l’aide de MongoDB APIs de la base de données tooa.</span><span class="sxs-lookup"><span data-stu-id="725f0-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="725f0-108">Il est transparent toohello application hello les données est stockée dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="725f0-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="725f0-109">Lorsque vous aurez terminé, vous disposerez d’une MEAN (MongoDB, Express, AngularJS et Node.js) exécutée sous [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="725f0-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Application MEAN.js exécutée dans Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="725f0-111">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="725f0-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="725f0-112">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="725f0-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="725f0-113">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="725f0-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="725f0-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="725f0-114">Prerequisites</span></span> 
<span data-ttu-id="725f0-115">En outre tooAzure CLI, vous devez [Node.js](https://nodejs.org/) et [Git](http://www.git-scm.com/downloads) installé localement toorun `npm` et `git` commandes.</span><span class="sxs-lookup"><span data-stu-id="725f0-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="725f0-116">Vous devriez avoir une bonne connaissance de Node.js.</span><span class="sxs-lookup"><span data-stu-id="725f0-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="725f0-117">Ce démarrage rapide n’est pas prévue toohelp vous avec le développement d’applications Node.js en général.</span><span class="sxs-lookup"><span data-stu-id="725f0-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="725f0-118">Exemple d’application hello de cloner</span><span class="sxs-lookup"><span data-stu-id="725f0-118">Clone hello sample application</span></span>

<span data-ttu-id="725f0-119">Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="725f0-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="725f0-120">Exécutez hello suivant le dépôt d’exemples de commandes tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="725f0-121">Ce dépôt d’exemples contient la valeur par défaut hello [MEAN.js](http://meanjs.org/) application.</span><span class="sxs-lookup"><span data-stu-id="725f0-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="725f0-122">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="725f0-122">Run hello application</span></span>

<span data-ttu-id="725f0-123">Installer des packages hello requis et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="725f0-124">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="725f0-124">Log in tooAzure</span></span>

<span data-ttu-id="725f0-125">Si vous utilisez une installation CLI d’Azure, connectez-vous tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="725f0-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="725f0-126">Vous pouvez ignorer cette étape si vous utilisez hello Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="725f0-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="725f0-127">Ajouter le module de base de données Azure Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="725f0-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="725f0-128">Si vous utilisez une CLI d’Azure installés, vérifiez toosee si hello `cosmosdb` composant est déjà installé, exécutez hello `az` commande.</span><span class="sxs-lookup"><span data-stu-id="725f0-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="725f0-129">Si `cosmosdb` est hello la liste des commandes de base, continuer toohello prochaine commande.</span><span class="sxs-lookup"><span data-stu-id="725f0-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="725f0-130">Vous pouvez ignorer cette étape si vous utilisez hello Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="725f0-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="725f0-131">Si `cosmosdb` n’est pas en hello la liste des commandes de base, réinstallez [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="725f0-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="725f0-132">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="725f0-132">Create a resource group</span></span>

<span data-ttu-id="725f0-133">Créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec hello [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="725f0-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="725f0-134">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="725f0-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="725f0-135">Hello exemple suivant crée un groupe de ressources dans la région Europe de l’ouest hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="725f0-136">Choisissez un nom unique pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="725f0-137">Si vous utilisez un environnement de Cloud Azure, cliquez sur **essayer**, suivez toologin des invites à l’écran hello, puis copiez la commande hello dans l’invite de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="725f0-138">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="725f0-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="725f0-139">Créer un compte de base de données Azure Cosmos avec hello [az cosmosdb créer](/cli/azure/cosmosdb#create) commande.</span><span class="sxs-lookup"><span data-stu-id="725f0-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="725f0-140">Bonjour suivant de commande, veuillez remplacer votre propre nom de compte de base de données Azure Cosmos unique dans lequel vous consultez hello `<cosmosdb-name>` espace réservé.</span><span class="sxs-lookup"><span data-stu-id="725f0-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="725f0-141">Ce nom unique sera utilisé dans le cadre de votre point de terminaison de base de données Azure Cosmos (`https://<cosmosdb-name>.documents.azure.com/`), de sorte que le nom hello doit toobe unique dans tous les comptes de base de données Azure Cosmos dans Azure.</span><span class="sxs-lookup"><span data-stu-id="725f0-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="725f0-142">Hello `--kind MongoDB` paramètre permet les connexions clientes MongoDB.</span><span class="sxs-lookup"><span data-stu-id="725f0-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="725f0-143">Hello compte de base de données Azure Cosmos est créé, hello CLI d’Azure indique des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="725f0-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="725f0-144">Cet exemple utilise JSON comme format de sortie hello CLI d’Azure, qui est la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="725f0-145">toouse une autre sortie de format, consultez [formats pour les commandes de Azure CLI 2.0 de sortie](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="725f0-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="725f0-146">Se connecter à votre base de données toohello d’application Node.js</span><span class="sxs-lookup"><span data-stu-id="725f0-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="725f0-147">Dans cette étape, vous vous connectez votre MEAN.js application tooan base de données Azure Cosmos base de données exemple que vous venez de créer, à l’aide d’une chaîne de connexion MongoDB.</span><span class="sxs-lookup"><span data-stu-id="725f0-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="725f0-148">Configurer la chaîne de connexion hello dans votre application Node.js</span><span class="sxs-lookup"><span data-stu-id="725f0-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="725f0-149">Dans votre référentiel MEAN.js, ouvrez `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="725f0-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="725f0-150">Remplacez le contenu de ce fichier hello hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="725f0-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="725f0-151">Veillez tooalso remplacer hello deux `<cosmosdb-name>` des espaces réservés avec le nom de votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="725f0-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="725f0-152">Récupérer la clé de hello</span><span class="sxs-lookup"><span data-stu-id="725f0-152">Retrieve hello key</span></span>

<span data-ttu-id="725f0-153">Dans la base de données de base de données Azure Cosmos de commande tooconnect tooan, vous devez la clé de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="725f0-154">Hello d’utilisation [liste clés az cosmosdb](/cli/azure/cosmosdb#list-keys) clé primaire de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="725f0-155">Hello CLI d’Azure génère des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="725f0-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="725f0-156">Copiez la valeur hello `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="725f0-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="725f0-157">Coller sur hello `<primary_master_key>` dans `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="725f0-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="725f0-158">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="725f0-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="725f0-159">Relancez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-159">Run hello application again.</span></span>

<span data-ttu-id="725f0-160">Exécutez de nouveau `npm start`.</span><span class="sxs-lookup"><span data-stu-id="725f0-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="725f0-161">Un message de console doit indiquer maintenant de que cet environnement de développement hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="725f0-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="725f0-162">Accédez trop`http://localhost:3000` dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="725f0-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="725f0-163">Cliquez sur **s’inscrire** dans toocreate supérieur de menu, puis réessayez de hello deux factice des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="725f0-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="725f0-164">Hello MEAN.js exemple d’application stocke les données utilisateur dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="725f0-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="725f0-165">Si vous êtes réussie et MEAN.js se connecte automatiquement à hello créé l’utilisateur, puis l’utilisation de votre connexion de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="725f0-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js se connecte correctement tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="725f0-167">Afficher les données dans l’Explorateur de données</span><span class="sxs-lookup"><span data-stu-id="725f0-167">View data in Data Explorer</span></span>

<span data-ttu-id="725f0-168">Les données stockées par une base de données Azure Cosmos soient tooview disponible, requête et exécution d’une logique métier sur Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="725f0-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="725f0-169">tooview, interroger et manipuler les données d’utilisateur hello créées à l’étape précédente hello, connexion toohello [portail Azure](https://portal.azure.com) dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="725f0-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="725f0-170">Dans la zone de recherche supérieure hello, type de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="725f0-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="725f0-171">Lorsque le panneau de votre compte Cosmos DB s’ouvre, sélectionnez votre compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="725f0-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="725f0-172">Bonjour barre de navigation gauche, cliquez sur Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="725f0-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="725f0-173">Développez votre collection dans le volet de Collections hello, puis vous pouvez afficher des documents de hello dans la collection de hello, interroger des données hello et même créer et exécuter des procédures stockées, des déclencheurs et des UDF.</span><span class="sxs-lookup"><span data-stu-id="725f0-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Explorateur de données Bonjour portail Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="725f0-175">Déployer hello Node.js application tooAzure</span><span class="sxs-lookup"><span data-stu-id="725f0-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="725f0-176">Dans cette étape, vous déployez votre tooAzure d’application connectée MongoDB de Node.js Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="725f0-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="725f0-177">Vous avez peut-être remarqué ce fichier de configuration hello que vous avez modifié précédemment est pour l’environnement de développement hello (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="725f0-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="725f0-178">Lorsque vous déployez votre tooApp application Service, il s’exécute dans un environnement de production hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="725f0-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="725f0-179">Maintenant, vous devez toomake hello même modifier le fichier de configuration respectifs toohello.</span><span class="sxs-lookup"><span data-stu-id="725f0-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="725f0-180">Dans votre référentiel MEAN.js, ouvrez `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="725f0-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="725f0-181">Bonjour `db` d’objet, remplacez la valeur hello `uri` comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="725f0-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="725f0-182">Être vraiment tooreplace hello des espaces réservés comme avant.</span><span class="sxs-lookup"><span data-stu-id="725f0-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="725f0-183">Hello `ssl=true` option est importante car [base de données Azure Cosmos requiert SSL](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="725f0-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="725f0-184">Bonjour terminal, valider toutes vos modifications dans Git.</span><span class="sxs-lookup"><span data-stu-id="725f0-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="725f0-185">Vous pouvez copier les deux toorun commandes ensemble.</span><span class="sxs-lookup"><span data-stu-id="725f0-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="725f0-186">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="725f0-186">Clean up resources</span></span>

<span data-ttu-id="725f0-187">Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="725f0-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="725f0-188">À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="725f0-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="725f0-189">Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="725f0-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="725f0-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="725f0-190">Next steps</span></span>

<span data-ttu-id="725f0-191">Ce guide de démarrage rapide, vous avez appris comment toocreate une base de données Azure Cosmos compte et créez une collection de MongoDB à l’aide de hello Explorateur de données.</span><span class="sxs-lookup"><span data-stu-id="725f0-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="725f0-192">Vous pouvez désormais migrer votre tooAzure de données MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="725f0-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="725f0-193">Importer des données MongoDB dans Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="725f0-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
