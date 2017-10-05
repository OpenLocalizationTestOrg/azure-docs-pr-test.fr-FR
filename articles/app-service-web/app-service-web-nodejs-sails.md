---
title: "Déploiement d’une application web Sails.js dans Azure App Service | Microsoft Docs"
description: "Découvrez comment déployer une application Node.js dans Azure App Service. Ce didacticiel vous explique comment déployer une application web Sails.js."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="c16c0-104">Déployer une application web Sails.js dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c16c0-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="c16c0-105">Ce didacticiel vous montre comment déployer une application Sails.js dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c16c0-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="c16c0-106">Il permet également de comprendre comment configurer votre application Node.js à des fins d’exécution dans App Service.</span><span class="sxs-lookup"><span data-stu-id="c16c0-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="c16c0-107">Vous y gagnerez des compétences utiles telles que :</span><span class="sxs-lookup"><span data-stu-id="c16c0-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="c16c0-108">la configuration d’une application Sails.js s’exécutant dans App Service ;</span><span class="sxs-lookup"><span data-stu-id="c16c0-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="c16c0-109">le déploiement d’une application dans App Service à partir de la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="c16c0-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="c16c0-110">la lecture de journaux stderr et stdout pour résoudre les éventuels problèmes de déploiement ;</span><span class="sxs-lookup"><span data-stu-id="c16c0-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="c16c0-111">le stockage de variables d’environnement en dehors du contrôle de code source ;</span><span class="sxs-lookup"><span data-stu-id="c16c0-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="c16c0-112">l’accès aux variables d’environnement Azure à partir de votre application ;</span><span class="sxs-lookup"><span data-stu-id="c16c0-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="c16c0-113">la connexion à une base de données (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="c16c0-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="c16c0-114">Vous devriez avec une bonne connaissance de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="c16c0-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="c16c0-115">Ce didacticiel n’est pas destiné à résoudre les problèmes liés à l’exécution de Sail.js en général.</span><span class="sxs-lookup"><span data-stu-id="c16c0-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c16c0-116">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="c16c0-116">CLI versions to complete the task</span></span>

<span data-ttu-id="c16c0-117">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="c16c0-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="c16c0-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c16c0-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="c16c0-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c16c0-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c16c0-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c16c0-120">Prerequisites</span></span>
* [<span data-ttu-id="c16c0-121">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c16c0-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="c16c0-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="c16c0-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="c16c0-123">Git</span><span class="sxs-lookup"><span data-stu-id="c16c0-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="c16c0-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c16c0-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="c16c0-125">Un compte Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c16c0-125">A Microsoft Azure account.</span></span> <span data-ttu-id="c16c0-126">Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="c16c0-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="c16c0-127">Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure.</span><span class="sxs-lookup"><span data-stu-id="c16c0-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="c16c0-128">Créez une application de base et expérimentez-la pendant une heure, sans carte de paiement et sans engagement.</span><span class="sxs-lookup"><span data-stu-id="c16c0-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="c16c0-129">Étape 1 : Créer et configurer une application Sails.js localement</span><span class="sxs-lookup"><span data-stu-id="c16c0-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="c16c0-130">Commencez par créer rapidement une application Sails.js par défaut dans votre environnement de développement en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="c16c0-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="c16c0-131">Ouvrez le terminal de ligne de commande de votre choix et tapez la commande `CD` pointant vers un répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="c16c0-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="c16c0-132">Créez une application Sails.js et exécutez-la :</span><span class="sxs-lookup"><span data-stu-id="c16c0-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="c16c0-133">Vérifiez que vous pouvez accéder à la page d’accueil par défaut à l’adresse http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="c16c0-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="c16c0-134">Ensuite, activez la journalisation pour Azure.</span><span class="sxs-lookup"><span data-stu-id="c16c0-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="c16c0-135">Dans votre répertoire racine, créez un fichier nommé `iisnode.yml` et ajoutez les deux lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c16c0-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="c16c0-136">La journalisation est maintenant activée pour le serveur [iisnode](https://github.com/tjanczuk/iisnode) qu’Azure App Service utilise pour exécuter des applications Node.js.</span><span class="sxs-lookup"><span data-stu-id="c16c0-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="c16c0-137">Pour plus d’informations sur la façon dont ceci fonctionne, consultez [Guide pratique pour déboguer une application web Node.js dans Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c16c0-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="c16c0-138">Ensuite, configurez l’application Sails.js pour utiliser des variables d’environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c16c0-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="c16c0-139">Ouvrez config/env/production.js pour configurer votre environnement de production et définir `port` et `hookTimeout` :</span><span class="sxs-lookup"><span data-stu-id="c16c0-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="c16c0-140">La description de ces paramètres de configuration est disponible dans la [documentation Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="c16c0-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="c16c0-141">Ensuite, codez en dur la version de Node.js que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="c16c0-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="c16c0-142">Dans package.json, ajoutez le code `engines` suivant pour définir la version Node.js voulue.</span><span class="sxs-lookup"><span data-stu-id="c16c0-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="c16c0-143">Enfin, initialisez un référentiel Git et validez vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="c16c0-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="c16c0-144">Dans la racine de l’application (où se trouve package.json), exécutez les commandes Git suivantes :</span><span class="sxs-lookup"><span data-stu-id="c16c0-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="c16c0-145">Votre code est prêt à être déployé.</span><span class="sxs-lookup"><span data-stu-id="c16c0-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="c16c0-146">Étape 2 : Créer une application Azure et déployer Sails.js</span><span class="sxs-lookup"><span data-stu-id="c16c0-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="c16c0-147">Ensuite, créez la ressource App Service dans Azure et déployez votre application Sails.js dans celle-ci.</span><span class="sxs-lookup"><span data-stu-id="c16c0-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="c16c0-148">connectez-vous au portail Azure :</span><span class="sxs-lookup"><span data-stu-id="c16c0-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="c16c0-149">Suivez les instructions de l’invite pour poursuivre la connexion à un compte Microsoft associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c16c0-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="c16c0-150">Définissez l’utilisateur de déploiement pour App Service.</span><span class="sxs-lookup"><span data-stu-id="c16c0-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="c16c0-151">Vous déploierez le code ultérieurement à l’aide de ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c16c0-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="c16c0-152">Créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec un nom.</span><span class="sxs-lookup"><span data-stu-id="c16c0-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="c16c0-153">Pour ce didacticiel node.js, il n’est pas vraiment nécessaire de vous familiariser avec cela.</span><span class="sxs-lookup"><span data-stu-id="c16c0-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="c16c0-154">Pour connaître les valeurs possibles que vous pouvez utiliser pour `<location>`, utilisez la commande CLI `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="c16c0-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="c16c0-155">Créez un [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) « FREE » avec un nom.</span><span class="sxs-lookup"><span data-stu-id="c16c0-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="c16c0-156">Pour ce didacticiel node.js, sachez que vous ne serez pas facturé pour les Web Apps utilisées dans le cadre de cette offre.</span><span class="sxs-lookup"><span data-stu-id="c16c0-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="c16c0-157">Créez une application web avec un nom unique dans `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="c16c0-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="c16c0-158">Étape 3 : Configurer et déployer votre application Sails.js</span><span class="sxs-lookup"><span data-stu-id="c16c0-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="c16c0-159">Configurez le déploiement Git local pour votre nouvelle application web avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c16c0-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="c16c0-160">Vous obtenez une sortie JSON similaire à ce qui suit, ce qui signifie que le référentiel Git distant est configuré :</span><span class="sxs-lookup"><span data-stu-id="c16c0-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="c16c0-161">Ajoutez l’URL dans le fichier JSON en tant que Git distant pour votre référentiel local (appelé `azure` par souci de simplicité).</span><span class="sxs-lookup"><span data-stu-id="c16c0-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="c16c0-162">Déployez votre exemple de code dans le Git distant `azure`.</span><span class="sxs-lookup"><span data-stu-id="c16c0-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="c16c0-163">Lorsque vous y êtes invité, utilisez les informations d’identification de déploiement que vous avez configurées précédemment.</span><span class="sxs-lookup"><span data-stu-id="c16c0-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="c16c0-164">Pour terminer, lancez votre application Azure en direct dans le navigateur :</span><span class="sxs-lookup"><span data-stu-id="c16c0-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="c16c0-165">Vous devez maintenant voir la même page d’accueil Sails.js que ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c16c0-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="c16c0-166">Résoudre les problèmes de votre déploiement</span><span class="sxs-lookup"><span data-stu-id="c16c0-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="c16c0-167">Si votre application Sails.js échoue pour une raison quelconque dans App Service, référez-vous aux journaux stderr pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="c16c0-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="c16c0-168">Pour plus d’informations, consultez [Guide pratique pour déboguer une application web Node.js dans Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c16c0-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="c16c0-169">Si l’application a correctement démarré, le journal stdout doit afficher le message familier suivant :</span><span class="sxs-lookup"><span data-stu-id="c16c0-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="c16c0-170">Vous pouvez contrôler la granularité des journaux stdout dans le fichier [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) .</span><span class="sxs-lookup"><span data-stu-id="c16c0-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="c16c0-171">Se connecter à une base de données dans Azure</span><span class="sxs-lookup"><span data-stu-id="c16c0-171">Connect to a database in Azure</span></span>
<span data-ttu-id="c16c0-172">Pour vous connecter à une base de données dans Azure, créez la base de données de votre choix dans Azure, par exemple Azure SQL Database, MySQL, MongoDB, Cache (Redis) Azure, etc. et utilisez [l’adaptateur de banque de données](https://github.com/balderdashy/sails#compatibility) correspondant pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="c16c0-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="c16c0-173">Les étapes décrites dans cette section vous montrent comment se connecter à MongoDB à l’aide d’une base de données [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md), qui peut prendre en charge les connexions clientes à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c16c0-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="c16c0-174">[Créez un compte Cosmos DB prenant en charge le protocole MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="c16c0-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="c16c0-175">[Créez une collection et une base de données Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="c16c0-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="c16c0-176">Le nom de la collection n’a pas d’importance, mais vous avez besoin du nom de la base de données lorsque vous vous connectez à partir de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="c16c0-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="c16c0-177">[Recherchez les informations de connexion pour votre base de données Cosmos DB](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="c16c0-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="c16c0-178">Dans votre terminal de ligne de commande, installez l’adaptateur MongoDB :</span><span class="sxs-lookup"><span data-stu-id="c16c0-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="c16c0-179">Ouvrez config/connections.js et ajoutez l’objet de connexion suivant à la liste :</span><span class="sxs-lookup"><span data-stu-id="c16c0-179">Open config/connections.js and add the following connection object to the list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="c16c0-180">L’option `ssl: true` est importante, car [Cosmos DB en a besoin](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="c16c0-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="c16c0-181">Vous devez définir chaque variable d’environnement (`process.env.*`) dans App Service.</span><span class="sxs-lookup"><span data-stu-id="c16c0-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="c16c0-182">Pour ce faire, exécutez les commandes suivantes à partir de votre terminal.</span><span class="sxs-lookup"><span data-stu-id="c16c0-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="c16c0-183">Utilisez les informations de connexion pour Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c16c0-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="c16c0-184">Activer vos paramètres dans les paramètres de l’application Azure conserve les données sensibles hors de votre contrôle de source (Git).</span><span class="sxs-lookup"><span data-stu-id="c16c0-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="c16c0-185">Ensuite, vous configurez votre environnement de développement pour utiliser les mêmes informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="c16c0-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="c16c0-186">Ouvrez config/local.js et ajoutez l’objet connexion suivant :</span><span class="sxs-lookup"><span data-stu-id="c16c0-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="c16c0-187">Cette configuration remplace les paramètres de votre fichier config/connections.js pour l’environnement local.</span><span class="sxs-lookup"><span data-stu-id="c16c0-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="c16c0-188">Ce fichier est exclu par le .gitignore par défaut dans votre projet, il n’est donc pas stocké dans Git.</span><span class="sxs-lookup"><span data-stu-id="c16c0-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="c16c0-189">À présent, vous êtes en mesure de vous connecter à votre base de données Cosmos DB (MongoDB) depuis votre application web Azure et depuis votre environnement de développement local.</span><span class="sxs-lookup"><span data-stu-id="c16c0-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="c16c0-190">Ouvrez config/env/production.js pour configurer votre environnement de production et ajoutez l’objet `models` suivant :</span><span class="sxs-lookup"><span data-stu-id="c16c0-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="c16c0-191">Ouvrez config/env/development.js pour configurer votre environnement de développement et ajoutez l’objet `models` suivant :</span><span class="sxs-lookup"><span data-stu-id="c16c0-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="c16c0-192">`migrate: 'alter'` vous permet d’utiliser les fonctionnalités de migration de base de données pour créer et mettre à jour facilement des collections de bases de données ou des tables.</span><span class="sxs-lookup"><span data-stu-id="c16c0-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="c16c0-193">Cependant, `migrate: 'safe'` est utilisé pour votre environnement Azure (production), car Sails.js ne vous permet pas d’utiliser `migrate: 'alter'` dans un environnement de production (voir la [documentation Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="c16c0-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="c16c0-194">À partir du terminal, [générez](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) une [API blueprint](http://sailsjs.org/documentation/concepts/blueprints) Sails.js comme vous y êtes habitué, puis exécutez `sails lift` pour créer la base de données avec la de base de données de migration Sails.js.</span><span class="sxs-lookup"><span data-stu-id="c16c0-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="c16c0-195">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c16c0-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="c16c0-196">Le modèle `mywidget` généré par cette commande est vide, mais nous pouvons l’utiliser pour montrer que nous disposons d’une connectivité de base de données.</span><span class="sxs-lookup"><span data-stu-id="c16c0-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="c16c0-197">Lorsque vous exécutez `sails lift`, il crée les collections et les tables manquantes pour les modèles que votre application utilise.</span><span class="sxs-lookup"><span data-stu-id="c16c0-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="c16c0-198">À présent, accédez au modèle d’API que vous venez de créer dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="c16c0-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="c16c0-199">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c16c0-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="c16c0-200">L’API doit retourner l’entrée créée dans la fenêtre du navigateur, ce qui signifie que votre collection a été créée.</span><span class="sxs-lookup"><span data-stu-id="c16c0-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="c16c0-201">Maintenant, envoyez vos modifications dans Azure et accédez à votre application pour vérifier qu’elle fonctionne toujours.</span><span class="sxs-lookup"><span data-stu-id="c16c0-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="c16c0-202">Accédez au modèle d’API de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="c16c0-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="c16c0-203">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c16c0-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="c16c0-204">Si l’API renvoie une autre nouvelle entrée, votre application web Azure parle à votre base de données Cosmos DB (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="c16c0-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="c16c0-205">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="c16c0-205">More resources</span></span>
* [<span data-ttu-id="c16c0-206">Prise en main des applications web Node.js dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c16c0-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="c16c0-207">Utilisation de modules Node.js avec des applications Azure</span><span class="sxs-lookup"><span data-stu-id="c16c0-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
