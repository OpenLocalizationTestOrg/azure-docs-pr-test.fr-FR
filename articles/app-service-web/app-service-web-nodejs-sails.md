---
title: "aaaDeploy un tooAzure d’application Sails.js web du Service d’applications | Documents Microsoft"
description: "Découvrez comment toodeploy une application Node.js Azure App Service. Ce didacticiel vous montre comment toodeploy un Sails.js web app."
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
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="e6f78-104">Déployer un ordinateur Sails.js web application tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="e6f78-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="e6f78-105">Ce didacticiel vous montre comment toodeploy un tooAzure d’application Sails.js du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e6f78-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="e6f78-106">Dans le processus de hello, vous pouvez en déduire des connaissances générales sur la façon de tooconfigure votre toorun d’application Node.js dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e6f78-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="e6f78-107">Vous y gagnerez des compétences utiles telles que :</span><span class="sxs-lookup"><span data-stu-id="e6f78-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="e6f78-108">la configuration d’une application Sails.js s’exécutant dans App Service ;</span><span class="sxs-lookup"><span data-stu-id="e6f78-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="e6f78-109">Déployer une application de tooApp Service à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="e6f78-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="e6f78-110">Stdout et stderr lecture consigne tootroubleshoot tout problème de déploiement.</span><span class="sxs-lookup"><span data-stu-id="e6f78-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="e6f78-111">le stockage de variables d’environnement en dehors du contrôle de code source ;</span><span class="sxs-lookup"><span data-stu-id="e6f78-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="e6f78-112">l’accès aux variables d’environnement Azure à partir de votre application ;</span><span class="sxs-lookup"><span data-stu-id="e6f78-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="e6f78-113">Connecter la base de données tooa (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e6f78-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="e6f78-114">Vous devriez avec une bonne connaissance de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e6f78-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="e6f78-115">Ce didacticiel n’est pas prévue toohelp des problèmes liés toorunning Sail.js en général.</span><span class="sxs-lookup"><span data-stu-id="e6f78-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e6f78-116">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="e6f78-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="e6f78-117">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6f78-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e6f78-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="e6f78-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="e6f78-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="e6f78-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f78-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e6f78-120">Prerequisites</span></span>
* [<span data-ttu-id="e6f78-121">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e6f78-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="e6f78-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="e6f78-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="e6f78-123">Git</span><span class="sxs-lookup"><span data-stu-id="e6f78-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="e6f78-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e6f78-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="e6f78-125">Un compte Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e6f78-125">A Microsoft Azure account.</span></span> <span data-ttu-id="e6f78-126">Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e6f78-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="e6f78-127">Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e6f78-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="e6f78-128">Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.</span><span class="sxs-lookup"><span data-stu-id="e6f78-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="e6f78-129">Étape 1 : Créer et configurer une application Sails.js localement</span><span class="sxs-lookup"><span data-stu-id="e6f78-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="e6f78-130">Commencez par créer rapidement une application Sails.js par défaut dans votre environnement de développement en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6f78-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="e6f78-131">Terminal de ligne de commande de hello ouverte de votre choix et `CD` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="e6f78-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="e6f78-132">Créez une application Sails.js et exécutez-la :</span><span class="sxs-lookup"><span data-stu-id="e6f78-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="e6f78-133">Assurez-vous que vous pouvez parcourir la page d’accueil par défaut toohello à http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="e6f78-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="e6f78-134">Ensuite, activez la journalisation pour Azure.</span><span class="sxs-lookup"><span data-stu-id="e6f78-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="e6f78-135">Dans le répertoire racine, créez un fichier appelé `iisnode.yml` et ajoutez hello deux lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6f78-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="e6f78-136">La journalisation est maintenant activée pour hello [iisnode](https://github.com/tjanczuk/iisnode) serveur qu’Azure App Service utilisé par les applications Node.js toorun.</span><span class="sxs-lookup"><span data-stu-id="e6f78-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="e6f78-137">Pour plus d’informations sur le fonctionnement, consultez [comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="e6f78-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="e6f78-138">Ensuite, configurez les variables d’environnement Azure hello Sails.js application toouse.</span><span class="sxs-lookup"><span data-stu-id="e6f78-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="e6f78-139">Ouvrez config/env/production.js tooconfigure votre environnement de production, puis définissez `port` et `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="e6f78-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="e6f78-140">La description de ces paramètres de configuration est disponible dans la [documentation Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="e6f78-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="e6f78-141">Ensuite, coder en dur hello Node.js version de toouse.</span><span class="sxs-lookup"><span data-stu-id="e6f78-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="e6f78-142">Dans package.json, ajoutez suivant de hello `engines` propriété tooset hello Node.js version tooone que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="e6f78-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="e6f78-143">Enfin, initialisez un référentiel Git et validez vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="e6f78-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="e6f78-144">Dans l’hello racine de l’application (où est package.json), exécutez hello suivant de commandes Git :</span><span class="sxs-lookup"><span data-stu-id="e6f78-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="e6f78-145">Votre code est toobe prêt déployée.</span><span class="sxs-lookup"><span data-stu-id="e6f78-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="e6f78-146">Étape 2 : Créer une application Azure et déployer Sails.js</span><span class="sxs-lookup"><span data-stu-id="e6f78-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="e6f78-147">Ensuite, créez des hello ressource du Service de l’application dans Azure et déployer votre tooit d’application Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e6f78-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="e6f78-148">Ouvrez une session tooAzure comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6f78-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="e6f78-149">Suivez hello toocontinue invite hello compte de connexion dans un navigateur avec un compte Microsoft qui a votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e6f78-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="e6f78-150">Définir l’utilisateur du déploiement hello pour le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e6f78-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="e6f78-151">Vous déploierez le code ultérieurement à l’aide de ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e6f78-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="e6f78-152">Créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) avec un nom.</span><span class="sxs-lookup"><span data-stu-id="e6f78-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="e6f78-153">Pour ce didacticiel Node.js, vous n’ayez pas besoin tooknow qu’il est.</span><span class="sxs-lookup"><span data-stu-id="e6f78-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="e6f78-154">toosee quel possible les valeurs que vous pouvez utiliser pour `<location>`, utilisez hello `az appservice list-locations` commande CLI.</span><span class="sxs-lookup"><span data-stu-id="e6f78-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="e6f78-155">Créez un [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) « FREE » avec un nom.</span><span class="sxs-lookup"><span data-stu-id="e6f78-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="e6f78-156">Pour ce didacticiel node.js, sachez que vous ne serez pas facturé pour les Web Apps utilisées dans le cadre de cette offre.</span><span class="sxs-lookup"><span data-stu-id="e6f78-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="e6f78-157">Créez une application web avec un nom unique dans `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="e6f78-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="e6f78-158">Étape 3 : Configurer et déployer votre application Sails.js</span><span class="sxs-lookup"><span data-stu-id="e6f78-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="e6f78-159">Configurer un déploiement Git local pour votre application web avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e6f78-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="e6f78-160">Vous obtenez une sortie JSON comme celui-ci, ce qui signifie que hello le référentiel Git distant est configuré :</span><span class="sxs-lookup"><span data-stu-id="e6f78-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="e6f78-161">Ajouter des URL de hello Bonjour JSON comme un Git à distance pour votre référentiel local (appelé `azure` par souci de simplicité).</span><span class="sxs-lookup"><span data-stu-id="e6f78-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="e6f78-162">Déployer votre toohello du code exemple `azure` Git remote.</span><span class="sxs-lookup"><span data-stu-id="e6f78-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="e6f78-163">Lorsque vous y êtes invité, utiliser des informations d’identification du déploiement hello configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="e6f78-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="e6f78-164">Pour finir, lancez votre application Azure en temps réel dans le navigateur de hello :</span><span class="sxs-lookup"><span data-stu-id="e6f78-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="e6f78-165">Vous devez maintenant voir hello même Sails.js page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="e6f78-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="e6f78-166">Résoudre les problèmes de votre déploiement</span><span class="sxs-lookup"><span data-stu-id="e6f78-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="e6f78-167">Si votre application Sails.js échoue pour une raison quelconque dans le Service d’applications, \Journaux hello stderr toohelp de le résoudre.</span><span class="sxs-lookup"><span data-stu-id="e6f78-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="e6f78-168">Pour plus d’informations, consultez [comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="e6f78-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="e6f78-169">Si l’application hello a démarré avec succès, journal de stdout hello doit afficher message de type hello familier :</span><span class="sxs-lookup"><span data-stu-id="e6f78-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="e6f78-170">Vous pouvez contrôler la granularité des journaux de stdout hello Bonjour [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) fichier.</span><span class="sxs-lookup"><span data-stu-id="e6f78-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="e6f78-171">Se connecter tooa de base de données dans Azure</span><span class="sxs-lookup"><span data-stu-id="e6f78-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="e6f78-172">base de données tooconnect tooa dans Azure, vous créez des hello de base de données de votre choix dans Azure, telles que la base de données SQL Azure, MySQL, MongoDB, le Cache Azure (Redis), etc. et utilisez hello correspondant [adaptateur de magasin de données](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="e6f78-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="e6f78-173">Hello étapes décrites dans cette section vous montrent comment tooMongoDB tooconnect à l’aide un [base de données Azure Cosmos](../documentdb/documentdb-protocol-mongodb.md) base de données, ce qui peut prendre en charge les connexions de client MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e6f78-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="e6f78-174">[Créez un compte Cosmos DB prenant en charge le protocole MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="e6f78-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="e6f78-175">[Créez une collection et une base de données Cosmos DB](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="e6f78-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="e6f78-176">nom Hello de collection de hello n’a pas d’importance, mais vous devez nom hello de base de données hello lorsque vous vous connectez à partir de Sails.js.</span><span class="sxs-lookup"><span data-stu-id="e6f78-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="e6f78-177">[Rechercher les informations de connexion de hello pour votre base de données de la base de données Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="e6f78-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="e6f78-178">À partir de votre terminal de ligne de commande, installez l’adaptateur MongoDB hello :</span><span class="sxs-lookup"><span data-stu-id="e6f78-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="e6f78-179">Ouvrez config/connections.js et ajoutez les hello suivant connexion objet toohello liste :</span><span class="sxs-lookup"><span data-stu-id="e6f78-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="e6f78-180">Hello `ssl: true` option est importante car [Cosmos DB exige](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="e6f78-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="e6f78-181">Pour chaque variable d’environnement (`process.env.*`), vous devez tooset dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e6f78-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="e6f78-182">toodo, hello exécution suivant des commandes à partir de votre terminal.</span><span class="sxs-lookup"><span data-stu-id="e6f78-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="e6f78-183">Utilisez les informations de connexion de hello pour votre base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e6f78-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="e6f78-184">Activer vos paramètres dans les paramètres de l’application Azure conserve les données sensibles hors de votre contrôle de source (Git).</span><span class="sxs-lookup"><span data-stu-id="e6f78-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="e6f78-185">Ensuite, vous allez configurer votre développement environnement toouse hello les mêmes informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="e6f78-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="e6f78-186">Ouvrez config/local.js et ajoutez les hello connexions objet :</span><span class="sxs-lookup"><span data-stu-id="e6f78-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="e6f78-187">Cette configuration remplace les paramètres de hello dans votre fichier config/connections.js pour l’environnement local de hello.</span><span class="sxs-lookup"><span data-stu-id="e6f78-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="e6f78-188">Ce fichier est exclu par .gitignore par défaut de hello dans votre projet, donc il n’est pas stocké dans Git.</span><span class="sxs-lookup"><span data-stu-id="e6f78-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="e6f78-189">Maintenant, vous êtes en mesure de tooconnect tooyour Cosmos DB (MongoDB) base de données de votre application web Azure et de votre environnement de développement local.</span><span class="sxs-lookup"><span data-stu-id="e6f78-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="e6f78-190">Ouvrez config/env/production.js tooconfigure votre environnement de production et ajoutez hello suit `models` objet :</span><span class="sxs-lookup"><span data-stu-id="e6f78-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="e6f78-191">Ouvrez config/env/development.js tooconfigure votre environnement de développement et ajoutez hello suit `models` objet :</span><span class="sxs-lookup"><span data-stu-id="e6f78-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="e6f78-192">`migrate: 'alter'`vous permet d’utiliser toocreate de fonctionnalités de migration de base de données et mettre à jour facilement des collections de base de données ou des tables.</span><span class="sxs-lookup"><span data-stu-id="e6f78-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="e6f78-193">Toutefois, `migrate: 'safe'` est utilisé pour votre environnement Azure (production), car Sails.js ne vous autorise pas toouse `migrate: 'alter'` dans un environnement de production (voir [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="e6f78-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="e6f78-194">À partir de hello terminal, [générer](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) un Sails.js [Géomètre API](http://sailsjs.org/documentation/concepts/blueprints) comme vous normalement, puis exécutez `sails lift` créer la base de données de hello Sails.js la migration de base de données.</span><span class="sxs-lookup"><span data-stu-id="e6f78-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="e6f78-195">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e6f78-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="e6f78-196">Hello `mywidget` modèle généré par cette commande est vide, mais nous pouvons utiliser tooshow que nous disposons de connectivité de base de données.</span><span class="sxs-lookup"><span data-stu-id="e6f78-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="e6f78-197">Lorsque vous exécutez `sails lift`, il crée des collections de manquant hello et tables pour hello modélise par votre application.</span><span class="sxs-lookup"><span data-stu-id="e6f78-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="e6f78-198">Accès aux API de plan hello vous venez de créer dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e6f78-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="e6f78-199">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e6f78-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="e6f78-200">Hello API doit retourner tooyou arrière d’entrée hello créé dans la fenêtre de navigateur hello, ce qui signifie que votre collection est créée avec succès.</span><span class="sxs-lookup"><span data-stu-id="e6f78-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="e6f78-201">Maintenant, push tooAzure de vos modifications et parcourir toomake d’application tooyour qu’il fonctionne toujours.</span><span class="sxs-lookup"><span data-stu-id="e6f78-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="e6f78-202">Accès aux API de plan hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e6f78-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="e6f78-203">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e6f78-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="e6f78-204">Si hello API retourne une autre nouvelle entrée, puis votre application web Azure communique avec une base de données tooyour Cosmos DB (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="e6f78-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="e6f78-205">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="e6f78-205">More resources</span></span>
* [<span data-ttu-id="e6f78-206">Prise en main des applications web Node.js dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e6f78-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="e6f78-207">Utilisation de modules Node.js avec des applications Azure</span><span class="sxs-lookup"><span data-stu-id="e6f78-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
