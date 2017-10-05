---
title: "Utiliser le Kit de développement logiciel (SDK) de serveur principal Node.js pour Azure Mobile Apps | Microsoft Docs"
description: "Découvrez comment utiliser le Kit de développement logiciel (SDK) du serveur principal Node.js pour Azure App Service Mobile Apps."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="68869-103">Comment utiliser le Kit de développement logiciel Node.js dans Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="68869-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="68869-104">Cet article fournit des informations détaillées ainsi que des exemples sur l’utilisation d’un serveur principal Node.js dans Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="68869-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="68869-105"><a name="Introduction"></a>Introduction</span><span class="sxs-lookup"><span data-stu-id="68869-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="68869-106">Azure App Service Mobile Apps offre la possibilité d’ajouter à une application Web une API Web d’accès aux données optimisé pour les plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="68869-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="68869-107">Le Kit de développement logiciel (SDK) Azure App Service Mobile Apps est fourni pour les applications web ASP.NET et Node.js.</span><span class="sxs-lookup"><span data-stu-id="68869-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="68869-108">Le Kit offre les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="68869-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="68869-109">Opérations de table (Read, Insert, Update, Delete) pour l’accès aux données</span><span class="sxs-lookup"><span data-stu-id="68869-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="68869-110">Opérations d’API personnalisées</span><span class="sxs-lookup"><span data-stu-id="68869-110">Custom API operations</span></span>

<span data-ttu-id="68869-111">Les deux types d’opérations permettent une authentification entre tous les fournisseurs d’identité autorisés par Azure App Service, y compris les fournisseurs d’identité sociaux tels que Facebook, Twitter, Google et Microsoft, ainsi qu’Azure Active Directory pour les identités d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="68869-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="68869-112">Vous trouverez des exemples de chaque cas de figure dans le [répertoire d’exemples sur GitHub].</span><span class="sxs-lookup"><span data-stu-id="68869-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="68869-113">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="68869-113">Supported Platforms</span></span>
<span data-ttu-id="68869-114">Le kit de développement logiciel Node dans Azure Mobile Apps prend en charge la version actuelle de LTS de Node ainsi que les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="68869-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="68869-115">Au moment de la rédaction, la dernière version LTS de Node est 4.5.0.</span><span class="sxs-lookup"><span data-stu-id="68869-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="68869-116">Les autres versions de Node peuvent fonctionner, mais elles ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="68869-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="68869-117">Le kit de développement logiciel Node dans Azure Mobile Apps prend en charge deux pilotes de base de données : le pilote node-mssql prend en charge SQL Azure et les instances SQL Server locales.</span><span class="sxs-lookup"><span data-stu-id="68869-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="68869-118">Le pilote sqlite3 prend en charge les bases de données SQLite sur une seule instance.</span><span class="sxs-lookup"><span data-stu-id="68869-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="68869-119"><a name="howto-cmdline-basicapp"></a>Procédure : créer un serveur principal Node.js de base à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="68869-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="68869-120">Chaque serveur principal Node.js Azure App Service Mobile Apps démarre en tant qu’application ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="68869-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="68869-121">ExpressJS est l’infrastructure de service web la plus populaire pour le serveur principal Node.js.</span><span class="sxs-lookup"><span data-stu-id="68869-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="68869-122">Vous pouvez créer une application [Express] de base de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="68869-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="68869-123">Dans une commande ou une fenêtre PowerShell, créez un répertoire pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="68869-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="68869-124">Exécutez npm init pour initialiser la structure du package.</span><span class="sxs-lookup"><span data-stu-id="68869-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="68869-125">La commande npm init pose une série de questions pour initialiser le projet.</span><span class="sxs-lookup"><span data-stu-id="68869-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="68869-126">Consultez l’exemple pour voir le résultat obtenu :</span><span class="sxs-lookup"><span data-stu-id="68869-126">See the example output:</span></span>

    ![La sortie npm init][0]
3. <span data-ttu-id="68869-128">Installez les bibliothèques express et azure-mobile-apps à partir du référentiel npm.</span><span class="sxs-lookup"><span data-stu-id="68869-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="68869-129">Créez un fichier app.js pour implémenter le serveur mobile de base.</span><span class="sxs-lookup"><span data-stu-id="68869-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="68869-130">Cette application crée une WebAPI optimisée pour les applications mobiles avec un seul point de terminaison (`/tables/TodoItem`) qui fournit un accès non authentifié à un datastore SQL sous-jacent à l’aide d’un schéma dynamique.</span><span class="sxs-lookup"><span data-stu-id="68869-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="68869-131">Cette API est adaptée pour les démarrages rapides de bibliothèques client suivants :</span><span class="sxs-lookup"><span data-stu-id="68869-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="68869-132">[Android Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="68869-133">[Apache Cordova Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="68869-134">[iOS Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="68869-135">[Windows Store Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="68869-136">[Xamarin.iOS Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="68869-137">[Xamarin.Android Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="68869-138">[Xamarin.Forms Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="68869-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="68869-139">Vous trouverez le code pour cette application de base dans l’ [exemple basicapp sur GitHub].</span><span class="sxs-lookup"><span data-stu-id="68869-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="68869-140"><a name="howto-vs2015-basicapp"></a>Procédure : créer un serveur principal Node avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="68869-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="68869-141">Visual Studio 2015 requiert une extension pour développer les applications Node.js dans l’IDE.</span><span class="sxs-lookup"><span data-stu-id="68869-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="68869-142">Pour commencer, installez le fichier [Node.js Tools 1.1 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="68869-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="68869-143">Une fois le programme Node.js Tools pour Visual Studio installé, créez une application Express 4.x :</span><span class="sxs-lookup"><span data-stu-id="68869-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="68869-144">Ouvrez la boîte de dialogue **Nouveau projet** (dans le menu **Fichier** > **Nouveau** > **Projet...**).</span><span class="sxs-lookup"><span data-stu-id="68869-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="68869-145">Développez **Modèles** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="68869-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="68869-146">Sélectionnez **Basic Azure Node.js Express 4 Application**.</span><span class="sxs-lookup"><span data-stu-id="68869-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="68869-147">Renseignez le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="68869-147">Fill in the project name.</span></span>  <span data-ttu-id="68869-148">Cliquez sur *OK*.</span><span class="sxs-lookup"><span data-stu-id="68869-148">Click *OK*.</span></span>

    ![Visual Studio 2015 Nouveau projet][1]
5. <span data-ttu-id="68869-150">Cliquez avec le bouton droit de la souris sur le nœud **npm** et sélectionnez **Installer de nouveaux packages npm...**.</span><span class="sxs-lookup"><span data-stu-id="68869-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="68869-151">Vous devrez peut-être actualiser le catalogue npm lors de la création de votre première application Node.js.</span><span class="sxs-lookup"><span data-stu-id="68869-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="68869-152">Cliquez sur **Actualiser** si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="68869-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="68869-153">Dans la zone de recherche, entrez *azure-mobile-apps* .</span><span class="sxs-lookup"><span data-stu-id="68869-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="68869-154">Cliquez sur le package **azure-mobile-apps 2.0.0**, puis cliquez sur **Installer le package**.</span><span class="sxs-lookup"><span data-stu-id="68869-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Installer de nouveaux packages npm][2]
8. <span data-ttu-id="68869-156">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="68869-156">Click **Close**.</span></span>
9. <span data-ttu-id="68869-157">Ouvrez le fichier *app.js* pour ajouter la prise en charge du SDK Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="68869-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="68869-158">À la ligne 6 des instructions require de la bibliothèque, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="68869-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="68869-159">Environ à la ligne 27, après les autres instructions app.use, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="68869-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="68869-160">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="68869-160">Save the file.</span></span>
10. <span data-ttu-id="68869-161">Exécutez l’application en local (l’API est disponible sur http://localhost:3000) ou publiez-la dans Azure.</span><span class="sxs-lookup"><span data-stu-id="68869-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="68869-162"><a name="create-node-backend-portal"></a>Comment : créer un serveur principal Node.js à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="68869-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="68869-163">Vous pouvez créer un serveur principal d'application mobile dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="68869-164">Vous pouvez suivre la procédure ci-dessous, ou créer simultanément un client et un serveur en suivant le didacticiel [Créer une application mobile](app-service-mobile-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="68869-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="68869-165">Ce didacticiel contient une version simplifiée de ces instructions et convient mieux aux projets de preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="68869-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="68869-166">Dans le panneau *Prise en main*, sous **Créer table API de table**, sélectionnez **Node.js** en tant que **langue de backend**.</span><span class="sxs-lookup"><span data-stu-id="68869-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="68869-167">Cochez la case « **Je reconnais que cette opération va remplacer tout le contenu du site.** », puis cliquez sur **Créer une table TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="68869-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="68869-168"><a name="download-quickstart"></a>Procédure : télécharger le projet de code quickstart du serveur principal Node.js à l’aide de Git</span><span class="sxs-lookup"><span data-stu-id="68869-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="68869-169">Lorsque vous créez un serveur principal Node.js Mobile App à l’aide du panneau **Démarrage rapide** du portail, un projet Node.js est créé et déployé sur votre site.</span><span class="sxs-lookup"><span data-stu-id="68869-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="68869-170">Vous pouvez ajouter des tables et des API et modifier les fichiers de code pour le serveur principal Node.js dans le portail.</span><span class="sxs-lookup"><span data-stu-id="68869-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="68869-171">Vous pouvez également utiliser l’un des divers outils de déploiement pour télécharger le projet de serveur principal afin de pouvoir ajouter ou modifier des tables et des API, avant de publier à nouveau le projet.</span><span class="sxs-lookup"><span data-stu-id="68869-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="68869-172">Pour plus d’informations, consultez le [Guide de déploiement d’Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="68869-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="68869-173">La procédure suivante utilise un référentiel Git pour télécharger le code de projet quickstart.</span><span class="sxs-lookup"><span data-stu-id="68869-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="68869-174">Si vous ne l’avez pas déjà fait, installez Git.</span><span class="sxs-lookup"><span data-stu-id="68869-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="68869-175">La procédure requise pour installer Git diffère selon les systèmes d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="68869-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="68869-176">Consultez la rubrique [Installation de Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) pour accéder aux distributions et consignes d'installation propres aux différents systèmes d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="68869-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="68869-177">Suivez les étapes de la rubrique [Activer le référentiel de l’application App Service](../app-service-web/app-service-deploy-local-git.md#Step3) pour activer le référentiel Git pour votre backend, en prenant note du nom d’utilisateur et du mot de passe utilisés pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="68869-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="68869-178">Dans le panneau de votre serveur principal Mobile App, prenez note du paramètre **URL de clone Git** .</span><span class="sxs-lookup"><span data-stu-id="68869-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="68869-179">Exécutez la commande `git clone` à l’aide de l’URL de clone Git, en saisissant si besoin votre mot de passe, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="68869-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="68869-180">Accédez au répertoire local (/todolist dans l’exemple précédent). Vous remarquerez que les fichiers de projet ont été téléchargés.</span><span class="sxs-lookup"><span data-stu-id="68869-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="68869-181">Recherchez le fichier `todoitem.json` dans le répertoire `/tables`.</span><span class="sxs-lookup"><span data-stu-id="68869-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="68869-182">Ce fichier définit les autorisations sur la table.</span><span class="sxs-lookup"><span data-stu-id="68869-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="68869-183">Recherchez également le fichier `todoitem.js` dans le même répertoire, qui définit les scripts de cette opération CRUD pour la table.</span><span class="sxs-lookup"><span data-stu-id="68869-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="68869-184">Après avoir apporté vos modifications aux fichiers de projet, exécutez les commandes suivantes pour ajouter, valider, puis charger les modifications sur le site :</span><span class="sxs-lookup"><span data-stu-id="68869-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="68869-185">Lorsque vous ajoutez de nouveaux fichiers au projet, vous devez tout d’abord exécuter la commande `git add .`.</span><span class="sxs-lookup"><span data-stu-id="68869-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="68869-186">Le site est republié chaque fois qu’un nouvel ensemble de validations est transmis au site.</span><span class="sxs-lookup"><span data-stu-id="68869-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="68869-187"><a name="howto-publish-to-azure"></a>Procédure : publier votre serveur principal Node.js dans Azure</span><span class="sxs-lookup"><span data-stu-id="68869-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="68869-188">Microsoft Azure propose plusieurs mécanismes permettant de publier votre serveur principal Node.js Azure App Service Mobile Apps sur le service Azure.</span><span class="sxs-lookup"><span data-stu-id="68869-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="68869-189">En fonction du contrôle de la source, vous pouvez notamment utiliser les outils de déploiement intégrés à Visual Studio, les outils de ligne de commande et les options de déploiement continu.</span><span class="sxs-lookup"><span data-stu-id="68869-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="68869-190">Pour plus d’informations sur ce sujet, reportez-vous au [Guide de déploiement d’Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="68869-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="68869-191">Avant le déploiement, vous devriez prendre connaissance des recommandations suivantes pour l’application Node.js avec Azure App Service :</span><span class="sxs-lookup"><span data-stu-id="68869-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="68869-192">Comment [spécifier la version de Node]</span><span class="sxs-lookup"><span data-stu-id="68869-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="68869-193">Comment [utiliser les modules Node]</span><span class="sxs-lookup"><span data-stu-id="68869-193">How to [use Node modules]</span></span>

### <span data-ttu-id="68869-194"><a name="howto-enable-homepage"></a>Procédure : activation d’une page d’accueil pour votre application</span><span class="sxs-lookup"><span data-stu-id="68869-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="68869-195">De nombreuses applications regroupent à la fois des applications web et des applications mobiles ; l’infrastructure ExpressJS vous permet de combiner ces deux facettes.</span><span class="sxs-lookup"><span data-stu-id="68869-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="68869-196">Il peut cependant être préférable, parfois, d’implémenter uniquement une interface mobile.</span><span class="sxs-lookup"><span data-stu-id="68869-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="68869-197">Il est utile de fournir une page d’accueil pour obtenir la garantie que le service d’application fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="68869-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="68869-198">Vous pouvez soit fournir votre propre page d’accueil, soit activer une page d’accueil temporaire.</span><span class="sxs-lookup"><span data-stu-id="68869-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="68869-199">Pour activer une page d’accueil temporaire, utilisez ce qui suit pour instancier Azure Mobile Apps :</span><span class="sxs-lookup"><span data-stu-id="68869-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="68869-200">Si vous voulez que cette option soit disponible uniquement pour un développement en local, vous pouvez ajouter ce paramètre à votre fichier `azureMobile.js` .</span><span class="sxs-lookup"><span data-stu-id="68869-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="68869-201"><a name="TableOperations"></a>Opérations de table</span><span class="sxs-lookup"><span data-stu-id="68869-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="68869-202">Le Kit de développement logiciel Node.js Server azure-mobile-apps fournit des mécanismes permettant d’exposer les tables de données stockées dans la base de données SQL Azure sous la forme d’une WebAPI.</span><span class="sxs-lookup"><span data-stu-id="68869-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="68869-203">Cinq opérations sont fournies.</span><span class="sxs-lookup"><span data-stu-id="68869-203">Five operations are provided.</span></span>

| <span data-ttu-id="68869-204">Opération</span><span class="sxs-lookup"><span data-stu-id="68869-204">Operation</span></span> | <span data-ttu-id="68869-205">Description</span><span class="sxs-lookup"><span data-stu-id="68869-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68869-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="68869-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="68869-207">Extraire tous les enregistrements de la table</span><span class="sxs-lookup"><span data-stu-id="68869-207">Get all records in the table</span></span> |
| <span data-ttu-id="68869-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="68869-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="68869-209">Extraire un enregistrement spécifique de la table</span><span class="sxs-lookup"><span data-stu-id="68869-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="68869-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="68869-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="68869-211">Créer un enregistrement dans la table</span><span class="sxs-lookup"><span data-stu-id="68869-211">Create a record in the table</span></span> |
| <span data-ttu-id="68869-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="68869-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="68869-213">Mettre à jour un enregistrement dans la table</span><span class="sxs-lookup"><span data-stu-id="68869-213">Update a record in the table</span></span> |
| <span data-ttu-id="68869-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="68869-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="68869-215">Supprimer un enregistrement de la table</span><span class="sxs-lookup"><span data-stu-id="68869-215">Delete a record in the table</span></span> |

<span data-ttu-id="68869-216">Cette WebAPI prend en charge [OData] et étend le schéma de table pour prendre en charge [la synchronisation des données hors connexion].</span><span class="sxs-lookup"><span data-stu-id="68869-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="68869-217"><a name="howto-dynamicschema"></a>Procédure : définir des tables à l’aide d’un schéma dynamique</span><span class="sxs-lookup"><span data-stu-id="68869-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="68869-218">Avant de pouvoir utiliser une table, vous devez la définir.</span><span class="sxs-lookup"><span data-stu-id="68869-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="68869-219">Les tables peuvent être définies avec un schéma statique (dans lequel le développeur définit les colonnes du schéma) ou dynamique (dans lequel le SDK contrôle le schéma en fonction des demandes entrantes).</span><span class="sxs-lookup"><span data-stu-id="68869-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="68869-220">En outre, le développeur peut contrôler des aspects spécifiques de la WebAPI en ajoutant du code Javascript à la définition.</span><span class="sxs-lookup"><span data-stu-id="68869-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="68869-221">Il est recommandé de définir chaque table dans un fichier Javascript du répertoire de tables, puis d’utiliser la méthode tables.import() pour importer les tables.</span><span class="sxs-lookup"><span data-stu-id="68869-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="68869-222">En étendant l’application de base, le fichier app.js sera ajusté comme suit :</span><span class="sxs-lookup"><span data-stu-id="68869-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="68869-223">Définissez la table dans ./tables/TodoItem.js :</span><span class="sxs-lookup"><span data-stu-id="68869-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="68869-224">Par défaut, les tables utilisent le schéma dynamique.</span><span class="sxs-lookup"><span data-stu-id="68869-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="68869-225">Pour désactiver globalement le schéma dynamique, définissez le paramètre d’application **MS_DynamicSchema** sur False dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68869-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="68869-226">Vous en trouverez un exemple complet dans l’ [exemple todo sur GitHub].</span><span class="sxs-lookup"><span data-stu-id="68869-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="68869-227"><a name="howto-staticschema"></a>Procédure : définir des tables à l’aide d’un schéma statique</span><span class="sxs-lookup"><span data-stu-id="68869-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="68869-228">Vous pouvez définir explicitement les colonnes à exposer via la WebAPI.</span><span class="sxs-lookup"><span data-stu-id="68869-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="68869-229">Le SDK Node/js azure-mobile-apps ajoute automatiquement à la liste que vous fournissez toutes les colonnes supplémentaires requises pour la synchronisation des données hors connexion.</span><span class="sxs-lookup"><span data-stu-id="68869-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="68869-230">Par exemple, les applications clientes QuickStart requièrent une table à deux colonnes : une colonne texte (une chaîne) et une colonne complète (une valeur booléenne).</span><span class="sxs-lookup"><span data-stu-id="68869-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="68869-231">Vous pouvez définir ces colonnes dans le fichier JavaScript de définition de table (situé dans le répertoire de tables) comme suit :</span><span class="sxs-lookup"><span data-stu-id="68869-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="68869-232">Si vous définissez des tables de manière statique, vous devez également appeler la méthode tables.initialize() pour créer le schéma de base de données au démarrage.</span><span class="sxs-lookup"><span data-stu-id="68869-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="68869-233">La méthode tables.initialize() renvoie un objet [Promise] qui permet de s’assurer que le service web ne traite pas les requêtes avant l’initialisation de la base de données.</span><span class="sxs-lookup"><span data-stu-id="68869-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="68869-234"><a name="howto-sqlexpress-setup"></a>Procédure : utiliser SQL Express comme datastore de développement sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="68869-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="68869-235">Le SDK Node Azure Mobile Apps propose trois options de distribution standard des données :</span><span class="sxs-lookup"><span data-stu-id="68869-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="68869-236">Utilisez le pilote **memory** pour fournir un exemple de datastore non persistant</span><span class="sxs-lookup"><span data-stu-id="68869-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="68869-237">Utilisez le pilote **mssql** pour fournir un datastore SQL Express utilisé pour le développement</span><span class="sxs-lookup"><span data-stu-id="68869-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="68869-238">Utilisez le pilote **mssql** pour fournir un datastore de base de données SQL Azure utilisé pour la production</span><span class="sxs-lookup"><span data-stu-id="68869-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="68869-239">Le SDK Node.js Azure Mobile Apps utilise le [package mssql Node] pour établir et utiliser une connexion à SQL Express et à la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="68869-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="68869-240">Ce package nécessite l’activation de connexions TCP sur votre instance SQL Express.</span><span class="sxs-lookup"><span data-stu-id="68869-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="68869-241">Le pilote memory ne fournit pas un ensemble complet de fonctionnalités à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="68869-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="68869-242">Si vous souhaitez tester localement votre serveur principal, nous vous recommandons d’utiliser un datastore SQL Express et d’utiliser le pilote mssql.</span><span class="sxs-lookup"><span data-stu-id="68869-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="68869-243">Téléchargez et installez [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="68869-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="68869-244">Veillez à bien installer SQL Server 2014 Express avec l’édition Tools.</span><span class="sxs-lookup"><span data-stu-id="68869-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="68869-245">À moins que vous ayez explicitement besoin d’une prise en charge 64 bits, la version 32 bits consomme moins de mémoire lors de son exécution.</span><span class="sxs-lookup"><span data-stu-id="68869-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="68869-246">Exécutez le Gestionnaire de configuration de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="68869-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="68869-247">Développez le nœud **SQL Server Network Configuration** dans le menu de l’arborescence de gauche.</span><span class="sxs-lookup"><span data-stu-id="68869-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="68869-248">Cliquez sur **Protocols for SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="68869-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="68869-249">Cliquez avec le bouton droit sur **TCP/IP**, puis sélectionnez **Enable**.</span><span class="sxs-lookup"><span data-stu-id="68869-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="68869-250">Cliquez sur **OK** dans la boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="68869-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="68869-251">Cliquez avec le bouton droit sur **TCP/IP**, puis sélectionnez **Properties**.</span><span class="sxs-lookup"><span data-stu-id="68869-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="68869-252">Cliquez sur l'onglet **IP Addresses** .</span><span class="sxs-lookup"><span data-stu-id="68869-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="68869-253">Recherchez le nœud **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="68869-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="68869-254">Dans le champ **TCP Port**, entrez **1433**.</span><span class="sxs-lookup"><span data-stu-id="68869-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="68869-255">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68869-255">Click **OK**.</span></span>  <span data-ttu-id="68869-256">Cliquez sur **OK** dans la boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="68869-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="68869-257">Cliquez sur **SQL Server Services** dans le menu de l’arborescence de gauche.</span><span class="sxs-lookup"><span data-stu-id="68869-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="68869-258">Cliquez avec le bouton droit sur **SQL Server (SQLEXPRESS)**, puis sélectionnez **Restart**.</span><span class="sxs-lookup"><span data-stu-id="68869-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="68869-259">Fermez le Gestionnaire de configuration de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="68869-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="68869-260">Exécutez l’instance SQL Server 2014 Management Studio et connectez-vous à votre instance locale de SQL Express.</span><span class="sxs-lookup"><span data-stu-id="68869-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="68869-261">Dans l’Explorateur d’objets, cliquez avec le bouton droit sur votre instance et sélectionnez **Properties**</span><span class="sxs-lookup"><span data-stu-id="68869-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="68869-262">Sélectionnez la page **Security** .</span><span class="sxs-lookup"><span data-stu-id="68869-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="68869-263">Assurez-vous que le **mode d’authentification SQL Server et Windows** est bien sélectionné.</span><span class="sxs-lookup"><span data-stu-id="68869-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="68869-264">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="68869-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="68869-265">Développez **Security** > **Logins** dans l’Explorateur d’objets.</span><span class="sxs-lookup"><span data-stu-id="68869-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="68869-266">Cliquez avec le bouton droit sur **Connexions** et sélectionnez **Nouvelle connexion...**.</span><span class="sxs-lookup"><span data-stu-id="68869-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="68869-267">Entrez un nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="68869-267">Enter a Login name.</span></span>  <span data-ttu-id="68869-268">Sélectionnez **Authentification SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="68869-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="68869-269">Entrez un mot de passe, puis saisissez le même mot de passe dans le champ **Confirmer le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="68869-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="68869-270">Le mot de passe doit répondre aux exigences de complexité de Windows.</span><span class="sxs-lookup"><span data-stu-id="68869-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="68869-271">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="68869-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="68869-272">Cliquez avec le bouton droit sur votre nouveau compte de connexion et sélectionnez **Properties**</span><span class="sxs-lookup"><span data-stu-id="68869-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="68869-273">Sélectionnez la page **Server Roles** .</span><span class="sxs-lookup"><span data-stu-id="68869-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="68869-274">Cochez la case en regard du rôle de serveur **dbcreator** .</span><span class="sxs-lookup"><span data-stu-id="68869-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="68869-275">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="68869-275">Click **OK**</span></span>
   13. <span data-ttu-id="68869-276">Fermez SQL Server 2015 Management Studio.</span><span class="sxs-lookup"><span data-stu-id="68869-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="68869-277">Veillez à enregistrer les nom d’utilisateur et mot de passe que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="68869-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="68869-278">Vous devrez peut-être affecter des rôles serveur ou autorisations supplémentaires selon les besoins spécifiques de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="68869-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="68869-279">L’application Node.js lit la variable d’environnement **SQLCONNSTR_MS_TableConnectionString** pour la chaîne de connexion de cette base de données.</span><span class="sxs-lookup"><span data-stu-id="68869-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="68869-280">Vous pouvez définir cette variable dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="68869-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="68869-281">Par exemple, vous pouvez utiliser PowerShell pour définir cette variable d’environnement :</span><span class="sxs-lookup"><span data-stu-id="68869-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="68869-282">Accédez à la base de données via une connexion TCP/IP et fournissez un nom d’utilisateur et un mot de passe pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="68869-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="68869-283"><a name="howto-config-localdev"></a>Procédure : configurer votre projet pour un développement local</span><span class="sxs-lookup"><span data-stu-id="68869-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="68869-284">Azure Mobile Apps lit un fichier JavaScript appelé *azureMobile.js* à partir du système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="68869-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="68869-285">N’utilisez pas ce fichier pour configurer le SDK Azure Mobile Apps en production, mais plutôt les paramètres d’application du [portail Azure] .</span><span class="sxs-lookup"><span data-stu-id="68869-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="68869-286">Le fichier *azureMobile.js* doit exporter un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="68869-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="68869-287">Les paramètres les plus courants sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="68869-287">The most common settings are:</span></span>

* <span data-ttu-id="68869-288">Paramètres de base de données</span><span class="sxs-lookup"><span data-stu-id="68869-288">Database Settings</span></span>
* <span data-ttu-id="68869-289">Paramètres de journalisation des diagnostics</span><span class="sxs-lookup"><span data-stu-id="68869-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="68869-290">Paramètres CORS de remplacement</span><span class="sxs-lookup"><span data-stu-id="68869-290">Alternate CORS Settings</span></span>

<span data-ttu-id="68869-291">Vous trouverez ci-dessous un exemple de fichier *azureMobile.js* implémentant ces paramètres de base de données :</span><span class="sxs-lookup"><span data-stu-id="68869-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="68869-292">Nous vous recommandons d’ajouter *azureMobile.js* à votre fichier *.gitignore* (ou un autre fichier ignore de contrôle du code source) pour éviter que les mots de passe soient stockés dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="68869-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="68869-293">Veillez à toujours configurer les paramètres de production dans les paramètres d’application du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="68869-294"><a name="howto-appsettings"></a>Procédure : configuration des paramètres d’application pour votre application mobile</span><span class="sxs-lookup"><span data-stu-id="68869-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="68869-295">La plupart des paramètres du fichier *azureMobile.js* ont un paramètre équivalent dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="68869-296">Utilisez la liste suivante pour configurer votre application dans les paramètres d’application :</span><span class="sxs-lookup"><span data-stu-id="68869-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="68869-297">Paramètre d'application</span><span class="sxs-lookup"><span data-stu-id="68869-297">App Setting</span></span> | <span data-ttu-id="68869-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="68869-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="68869-299">Description</span><span class="sxs-lookup"><span data-stu-id="68869-299">Description</span></span> | <span data-ttu-id="68869-300">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="68869-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="68869-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="68869-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="68869-302">name</span><span class="sxs-lookup"><span data-stu-id="68869-302">name</span></span> |<span data-ttu-id="68869-303">Nom de l’application</span><span class="sxs-lookup"><span data-stu-id="68869-303">The name of the app</span></span> |<span data-ttu-id="68869-304">string</span><span class="sxs-lookup"><span data-stu-id="68869-304">string</span></span> |
| <span data-ttu-id="68869-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="68869-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="68869-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="68869-306">logging.level</span></span> |<span data-ttu-id="68869-307">Niveau minimal de journal pour les messages à consigner</span><span class="sxs-lookup"><span data-stu-id="68869-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="68869-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="68869-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="68869-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="68869-309">**MS_DebugMode**</span></span> |<span data-ttu-id="68869-310">debug</span><span class="sxs-lookup"><span data-stu-id="68869-310">debug</span></span> |<span data-ttu-id="68869-311">Activer ou désactiver le mode débogage</span><span class="sxs-lookup"><span data-stu-id="68869-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="68869-312">true, false</span><span class="sxs-lookup"><span data-stu-id="68869-312">true, false</span></span> |
| <span data-ttu-id="68869-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="68869-313">**MS_TableSchema**</span></span> |<span data-ttu-id="68869-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="68869-314">data.schema</span></span> |<span data-ttu-id="68869-315">Nom de schéma par défaut pour les tables SQL</span><span class="sxs-lookup"><span data-stu-id="68869-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="68869-316">string (valeur par défaut : dbo)</span><span class="sxs-lookup"><span data-stu-id="68869-316">string (default: dbo)</span></span> |
| <span data-ttu-id="68869-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="68869-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="68869-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="68869-318">data.dynamicSchema</span></span> |<span data-ttu-id="68869-319">Activer ou désactiver le mode débogage</span><span class="sxs-lookup"><span data-stu-id="68869-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="68869-320">true, false</span><span class="sxs-lookup"><span data-stu-id="68869-320">true, false</span></span> |
| <span data-ttu-id="68869-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="68869-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="68869-322">version (sur Undefined)</span><span class="sxs-lookup"><span data-stu-id="68869-322">version (set to undefined)</span></span> |<span data-ttu-id="68869-323">Désactive l'en-tête X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="68869-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="68869-324">true, false</span><span class="sxs-lookup"><span data-stu-id="68869-324">true, false</span></span> |
| <span data-ttu-id="68869-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="68869-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="68869-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="68869-326">skipversioncheck</span></span> |<span data-ttu-id="68869-327">Désactive la vérification de la version de l’API client</span><span class="sxs-lookup"><span data-stu-id="68869-327">Disables the client API version check</span></span> |<span data-ttu-id="68869-328">true, false</span><span class="sxs-lookup"><span data-stu-id="68869-328">true, false</span></span> |

<span data-ttu-id="68869-329">Pour définir un paramètre d’application :</span><span class="sxs-lookup"><span data-stu-id="68869-329">To set an App Setting:</span></span>

1. <span data-ttu-id="68869-330">Connectez-vous au [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="68869-331">Sélectionnez **Toutes les ressources** ou **App Services**, puis cliquez sur le nom de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="68869-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="68869-332">Le panneau Paramètres s’ouvre par défaut.</span><span class="sxs-lookup"><span data-stu-id="68869-332">The Settings blade opens by default.</span></span> <span data-ttu-id="68869-333">Si ce n’est pas le cas, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="68869-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="68869-334">Cliquez sur **Paramètres de l’application** dans le menu GÉNÉRAL.</span><span class="sxs-lookup"><span data-stu-id="68869-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="68869-335">Accédez à la section Paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="68869-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="68869-336">Si votre paramètre d’application existe déjà, cliquez sur la valeur correspondante pour la modifier.</span><span class="sxs-lookup"><span data-stu-id="68869-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="68869-337">Si votre paramètre d’application n’existe pas, saisissez-le dans la zone Clé et la valeur dans la zone Valeur.</span><span class="sxs-lookup"><span data-stu-id="68869-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="68869-338">Une fois que vous avez terminé, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="68869-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="68869-339">La modification de la plupart des paramètres requiert le redémarrage du service.</span><span class="sxs-lookup"><span data-stu-id="68869-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="68869-340"><a name="howto-use-sqlazure"></a>Procédure : utiliser la base de données SQL comme datastore de production</span><span class="sxs-lookup"><span data-stu-id="68869-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="68869-341">L’utilisation de la base de données SQL Azure en tant que datastore est identique pour tous les types d’applications Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="68869-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="68869-342">Si vous ne l’avez pas déjà fait, suivez ces étapes pour créer un serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="68869-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="68869-343">Connectez-vous au [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="68869-344">Dans le coin supérieur gauche de la fenêtre, cliquez sur le **+ nouveau** bouton > **Web + Mobile** > **l’application Mobile**, puis indiquez un nom pour votre serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="68869-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="68869-345">Dans la zone **Groupe de ressources** , entrez le même nom que votre application.</span><span class="sxs-lookup"><span data-stu-id="68869-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="68869-346">Le plan App Service par défaut est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="68869-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="68869-347">Pour modifier votre plan App Service, cliquez sur le plan App Service > **+ Créer nouveau**.</span><span class="sxs-lookup"><span data-stu-id="68869-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="68869-348">Indiquez le nom du nouveau plan App Service et sélectionnez un emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="68869-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="68869-349">Cliquez sur Niveau de tarification et sélectionnez un niveau de tarification approprié pour le service.</span><span class="sxs-lookup"><span data-stu-id="68869-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="68869-350">Sélectionnez **Afficher tout** pour afficher davantage d’options de tarification, telles que **Gratuit** et **Partagé**.</span><span class="sxs-lookup"><span data-stu-id="68869-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="68869-351">Une fois que vous avez sélectionné le niveau de tarification, cliquez sur le bouton **Sélectionner** .</span><span class="sxs-lookup"><span data-stu-id="68869-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="68869-352">Retournez dans le panneau **Plan App Service**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68869-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="68869-353">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="68869-353">Click **Create**.</span></span> <span data-ttu-id="68869-354">La configuration d’un serveur principal d’application mobile peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="68869-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="68869-355">Une fois le serveur principal d’application mobile configuré, le portail ouvre le panneau **Paramètres** correspondant au serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="68869-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="68869-356">Une fois le serveur principal d’application mobile créé, vous pouvez choisir de connecter une base de données SQL existante à votre serveur principal d’application mobile ou de créer une nouvelle base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="68869-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="68869-357">Dans cette section, nous créons une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="68869-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="68869-358">Si vous avez déjà une base de données dans le même emplacement que le serveur principal d’application mobile, vous pouvez choisir **Utiliser une base de données** et sélectionner la base de données.</span><span class="sxs-lookup"><span data-stu-id="68869-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="68869-359">Il est déconseillé d’utiliser une base de données dans un autre emplacement en raison de latences plus importantes.</span><span class="sxs-lookup"><span data-stu-id="68869-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="68869-360">Dans le nouveau serveur principal d’application mobile, cliquez sur **Paramètres** > **Application mobile** > **Données** > **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="68869-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="68869-361">Dans le panneau **Ajouter une connexion de données**, cliquez sur **Base de données SQL - Configurer les paramètres requis** > **Créer une base de données**.</span><span class="sxs-lookup"><span data-stu-id="68869-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="68869-362">Entrez le nom de la nouvelle base de données dans le champ **Nom** .</span><span class="sxs-lookup"><span data-stu-id="68869-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="68869-363">Cliquez sur **Serveur**.</span><span class="sxs-lookup"><span data-stu-id="68869-363">Click **Server**.</span></span>  <span data-ttu-id="68869-364">Dans le panneau **Nouveau serveur**, entrez un nom de serveur unique dans le champ **Nom du serveur**, et indiquez un **nom de connexion d’administration serveur** et un **mot de passe** appropriés.</span><span class="sxs-lookup"><span data-stu-id="68869-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="68869-365">Vérifiez que l'option **Autoriser les services Azure à accéder au serveur** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="68869-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="68869-366">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68869-366">Click **OK**.</span></span>

    ![Création d’une base de données SQL Azure][6]
4. <span data-ttu-id="68869-368">Dans le panneau **Nouvelle base de données**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68869-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="68869-369">Dans le panneau **Ajouter une connexion de données**, sélectionnez **Chaîne de connexion**, entrez le nom de connexion et le mot de passe que vous avez indiqués lors de la création de la base de données.</span><span class="sxs-lookup"><span data-stu-id="68869-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="68869-370">Si vous utilisez une base de données existante, indiquez les informations d’identification de connexion à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="68869-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="68869-371">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="68869-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="68869-372">Dans le panneau **Ajouter une connexion de données**, cliquez sur **OK** pour créer la base de données.</span><span class="sxs-lookup"><span data-stu-id="68869-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="68869-373">La création de la base de données prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="68869-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="68869-374">Utilisez la zone **Notifications** pour surveiller la progression du déploiement.</span><span class="sxs-lookup"><span data-stu-id="68869-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="68869-375">Attendez la fin du déploiement avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="68869-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="68869-376">Une fois le déploiement effectué, une chaîne de connexion est créée pour l’instance de base de données SQL dans les paramètres d’application de votre serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="68869-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="68869-377">Vous pouvez voir ce paramètre d’application dans **Paramètres** > **Paramètres de l’application** > **Chaînes de connexion**.</span><span class="sxs-lookup"><span data-stu-id="68869-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="68869-378"><a name="howto-tables-auth"></a>Procédure : exiger une authentification pour l’accès aux tables</span><span class="sxs-lookup"><span data-stu-id="68869-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="68869-379">Si vous souhaitez utiliser l’authentification App Service avec le point de terminaison des tables, vous devez d’abord configurer l’authentification App Service dans le [portail Azure] .</span><span class="sxs-lookup"><span data-stu-id="68869-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="68869-380">Pour plus d’informations sur la configuration de l’authentification dans Azure App Service, consultez le Guide de configuration du fournisseur d’identité que vous souhaitez utiliser :</span><span class="sxs-lookup"><span data-stu-id="68869-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="68869-381">[Comment configurer votre application pour utiliser la connexion Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="68869-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="68869-382">[Comment configurer votre application pour utiliser une connexion Facebook]</span><span class="sxs-lookup"><span data-stu-id="68869-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="68869-383">[Comment configurer votre application pour utiliser une connexion Google]</span><span class="sxs-lookup"><span data-stu-id="68869-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="68869-384">[Comment configurer votre application pour utiliser une connexion par compte Microsoft]</span><span class="sxs-lookup"><span data-stu-id="68869-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="68869-385">[Comment configurer votre application pour utiliser une connexion Twitter]</span><span class="sxs-lookup"><span data-stu-id="68869-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="68869-386">Chaque table possède une propriété d’accès que vous pouvez utiliser pour contrôler l’accès à la table.</span><span class="sxs-lookup"><span data-stu-id="68869-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="68869-387">L’exemple suivant illustre une table définie de façon statique avec l’authentification requise.</span><span class="sxs-lookup"><span data-stu-id="68869-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="68869-388">La propriété d’accès peut prendre trois valeurs :</span><span class="sxs-lookup"><span data-stu-id="68869-388">The access property can take one of three values</span></span>

* <span data-ttu-id="68869-389">*anonymous* indique que l’application cliente est autorisée à lire les données sans authentification</span><span class="sxs-lookup"><span data-stu-id="68869-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="68869-390">*authenticated* indique que l’application cliente doit envoyer un jeton d’authentification valide avec la requête</span><span class="sxs-lookup"><span data-stu-id="68869-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="68869-391">*disabled* indique que cette table est actuellement désactivée</span><span class="sxs-lookup"><span data-stu-id="68869-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="68869-392">Si la propriété d’accès n’est pas définie, l’accès non authentifié est autorisé.</span><span class="sxs-lookup"><span data-stu-id="68869-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="68869-393"><a name="howto-tables-getidentity"></a>Procédure : utilisation des revendications d’authentification avec vos tables</span><span class="sxs-lookup"><span data-stu-id="68869-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="68869-394">Vous pouvez configurer différentes revendications qui sont demandées lors de la configuration de l'authentification.</span><span class="sxs-lookup"><span data-stu-id="68869-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="68869-395">Ces revendications ne sont normalement pas disponibles via l’objet `context.user` .</span><span class="sxs-lookup"><span data-stu-id="68869-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="68869-396">Toutefois, elles peuvent être récupérées à l'aide de la méthode `context.user.getIdentity()` .</span><span class="sxs-lookup"><span data-stu-id="68869-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="68869-397">La méthode `getIdentity()` renvoie une promesse qui correspond à un objet.</span><span class="sxs-lookup"><span data-stu-id="68869-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="68869-398">L'objet est indexé par la méthode d'authentification (facebook, google, twitter, microsoftaccount ou aad).</span><span class="sxs-lookup"><span data-stu-id="68869-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="68869-399">Par exemple, si vous configurez l'authentification de compte Microsoft et demandez la revendication des adresses de messagerie, vous pouvez ajouter l'adresse de messagerie à l'enregistrement avec le contrôleur de table suivant :</span><span class="sxs-lookup"><span data-stu-id="68869-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="68869-400">Pour voir les revendications disponibles, utilisez un navigateur web pour afficher le point de terminaison `/.auth/me` de votre site.</span><span class="sxs-lookup"><span data-stu-id="68869-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="68869-401"><a name="howto-tables-disabled"></a>Procédure : désactiver l’accès à des opérations de table spécifiques</span><span class="sxs-lookup"><span data-stu-id="68869-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="68869-402">En plus d’apparaître sur la table, la propriété d’accès peut être utilisée pour contrôler des opérations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="68869-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="68869-403">Il existe quatre opérations :</span><span class="sxs-lookup"><span data-stu-id="68869-403">There are four operations:</span></span>

* <span data-ttu-id="68869-404">*read* : opération GET RESTful sur la table</span><span class="sxs-lookup"><span data-stu-id="68869-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="68869-405">*insert* : opération POST RESTful sur la table</span><span class="sxs-lookup"><span data-stu-id="68869-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="68869-406">*update* : opération PATCH RESTful sur la table</span><span class="sxs-lookup"><span data-stu-id="68869-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="68869-407">*delete* : opération DELETE RESTful sur la table</span><span class="sxs-lookup"><span data-stu-id="68869-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="68869-408">Vous pouvez, par exemple, souhaiter fournir une table non authentifiée en lecture seule :</span><span class="sxs-lookup"><span data-stu-id="68869-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="68869-409"><a name="howto-tables-query"></a>Procédure : ajuster la requête utilisée avec les opérations de table</span><span class="sxs-lookup"><span data-stu-id="68869-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="68869-410">On attend souvent des opérations de table qu’elles soient capables de fournir une vue restreinte des données.</span><span class="sxs-lookup"><span data-stu-id="68869-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="68869-411">Par exemple, vous pouvez fournir une table marquée avec l’ID de l’utilisateur authentifié, vous permettant uniquement de lire ou de mettre à jour vos propres enregistrements.</span><span class="sxs-lookup"><span data-stu-id="68869-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="68869-412">La définition de table suivante offre cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="68869-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="68869-413">Les opérations qui exécutent normalement une requête ont une propriété de requête que vous pouvez ajuster avec une clause where.</span><span class="sxs-lookup"><span data-stu-id="68869-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="68869-414">La propriété de requête est un objet [QueryJS] utilisé pour convertir une requête OData en données que le serveur principal pourra traiter.</span><span class="sxs-lookup"><span data-stu-id="68869-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="68869-415">Pour les cas d’égalité simple (comme dans l’exemple précédent), vous pouvez utiliser un mappage.</span><span class="sxs-lookup"><span data-stu-id="68869-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="68869-416">Vous pouvez également ajouter des clauses SQL spécifiques :</span><span class="sxs-lookup"><span data-stu-id="68869-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="68869-417"><a name="howto-tables-softdelete"></a>Procédure : configurer une suppression réversible sur une table</span><span class="sxs-lookup"><span data-stu-id="68869-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="68869-418">La suppression réversible (Soft Delete) ne supprime pas réellement les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="68869-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="68869-419">Elle les marque comme étant supprimés dans la base de données en définissant la colonne supprimée sur true.</span><span class="sxs-lookup"><span data-stu-id="68869-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="68869-420">Le SDK Azure Mobile Apps supprime automatiquement des résultats les enregistrements ainsi supprimés, sauf si le SDK Mobile Client utilise IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="68869-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="68869-421">Pour configurer une table pour une suppression réversible, définissez la propriété `softDelete` dans le fichier de définition de table :</span><span class="sxs-lookup"><span data-stu-id="68869-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="68869-422">Vous devez établir un mécanisme pour purger les enregistrements, à partir d’une application cliente, via un WebJob, via une fonction Azure ou via une API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="68869-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="68869-423"><a name="howto-tables-seeding"></a>Procédure : alimenter votre base de données</span><span class="sxs-lookup"><span data-stu-id="68869-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="68869-424">Lorsque vous créez une nouvelle application, vous souhaiterez sans doute alimenter une table avec des données.</span><span class="sxs-lookup"><span data-stu-id="68869-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="68869-425">Pour ce faire, vous pouvez utiliser le fichier JavaScript de définition de table, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="68869-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="68869-426">L’amorçage de données n’est possible que lorsque la table est créée à l’aide du SDK Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="68869-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="68869-427">Si la table existe déjà dans la base de données, aucune donnée ne sera injectée dans la table.</span><span class="sxs-lookup"><span data-stu-id="68869-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="68869-428">Si le schéma dynamique est activé, alors le schéma est déduit des données amorcées.</span><span class="sxs-lookup"><span data-stu-id="68869-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="68869-429">Nous vous recommandons d’appeler explicitement la méthode `tables.initialize()` pour créer la table au début de l’exécution du service.</span><span class="sxs-lookup"><span data-stu-id="68869-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="68869-430"><a name="Swagger"></a>Procédure : activation de la prise en charge de Swagger</span><span class="sxs-lookup"><span data-stu-id="68869-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="68869-431">Azure App Service Mobile Apps prend nativement en charge l’interface [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="68869-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="68869-432">Pour activer la prise en charge de Swagger, commencez par installer l’interface utilisateur Swagger en tant que dépendance :</span><span class="sxs-lookup"><span data-stu-id="68869-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="68869-433">Une fois l’installation effectuée, vous pouvez activer la prise en charge de Swagger dans le constructeur Azure Mobile Apps :</span><span class="sxs-lookup"><span data-stu-id="68869-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="68869-434">Vous préférerez probablement activer la prise en charge de Swagger uniquement dans les éditions de développement.</span><span class="sxs-lookup"><span data-stu-id="68869-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="68869-435">Pour ce faire, vous pouvez utiliser le paramètre d’application `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="68869-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="68869-436">Le point de terminaison swagger se trouve à l’adresse http://*VotreSite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="68869-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="68869-437">Vous pouvez accéder à l’interface utilisateur Swagger via le point de terminaison `/swagger/ui`.</span><span class="sxs-lookup"><span data-stu-id="68869-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="68869-438">Si vous décidez de demander une authentification sur l’ensemble de votre application, Swagger génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="68869-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="68869-439">Pour obtenir de meilleurs résultats, autorisez les demandes non authentifiées via les paramètres d’authentification et d’autorisation d’Azure App Service. Vous pouvez ensuite contrôler l’authentification en utilisant la propriété `table.access`.</span><span class="sxs-lookup"><span data-stu-id="68869-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="68869-440">Vous pouvez également ajouter l’option Swagger à votre fichier `azureMobile.js` si vous voulez activer la prise en charge de Swagger uniquement dans le cadre d’un développement en local.</span><span class="sxs-lookup"><span data-stu-id="68869-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="68869-441"><a name="push">Notifications Push</span><span class="sxs-lookup"><span data-stu-id="68869-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="68869-442">Mobile Apps s’intègre à Azure Notification Hubs pour vous permettre d’envoyer des notifications Push ciblées à des millions d’appareils utilisant toutes les plateformes les plus populaires.</span><span class="sxs-lookup"><span data-stu-id="68869-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="68869-443">Notification Hubs vous permet d’envoyer des notifications Push aux appareils iOS, Android et Windows.</span><span class="sxs-lookup"><span data-stu-id="68869-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="68869-444">Pour plus d'informations sur ce que Notification Hubs vous permet de faire, consultez [Vue d'ensemble de Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68869-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="68869-445"></a><a name="send-push"></a>Procédure : envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="68869-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="68869-446">Le code suivant vous montre comment utiliser l’objet Push pour envoyer une notification Push de diffusion à des appareils iOS inscrits :</span><span class="sxs-lookup"><span data-stu-id="68869-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="68869-447">En créant un modèle d’inscription Push à partir du client, vous pouvez simplement envoyer un modèle de message Push à des appareils sur toutes les plateformes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="68869-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="68869-448">Le code suivant montre comment envoyer un modèle de notification :</span><span class="sxs-lookup"><span data-stu-id="68869-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="68869-449"><a name="push-user"></a>Procédure : envoi de notifications Push à un utilisateur authentifié à l’aide de balises</span><span class="sxs-lookup"><span data-stu-id="68869-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="68869-450">Lorsqu’un utilisateur authentifié s’inscrit aux notifications Push, une balise avec l’ID d’utilisateur est automatiquement ajoutée à l’inscription.</span><span class="sxs-lookup"><span data-stu-id="68869-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="68869-451">Grâce à cette balise, vous pouvez envoyer des notifications Push à tous les appareils inscrits par un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="68869-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="68869-452">Le code suivant permet d’obtenir le SID de l’utilisateur qui émet la demande et d’envoyer un modèle de notification Push à chaque inscription d’appareil pour cet utilisateur :</span><span class="sxs-lookup"><span data-stu-id="68869-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="68869-453">Quand vous vous inscrivez à des notifications Push à partir d’un client authentifié, assurez-vous au préalable que l’authentification est bien terminée.</span><span class="sxs-lookup"><span data-stu-id="68869-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="68869-454"><a name="CustomAPI"></a> API personnalisées</span><span class="sxs-lookup"><span data-stu-id="68869-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="68869-455"><a name="howto-customapi-basic"></a>Procédure : définition d'une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="68869-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="68869-456">Outre l’API d’accès aux données via le point de terminaison /tables, Azure Mobile Apps peut fournir une couverture d’API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="68869-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="68869-457">Les API personnalisées sont définies de manière similaire aux définitions de table et sont accessibles à toutes les mêmes fonctionnalités, y compris l’authentification.</span><span class="sxs-lookup"><span data-stu-id="68869-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="68869-458">Si vous souhaitez utiliser l’authentification App Service avec une API personnalisée, vous devez d’abord configurer l’authentification App Service dans le [portail Azure] .</span><span class="sxs-lookup"><span data-stu-id="68869-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="68869-459">Pour plus d’informations sur la configuration de l’authentification dans Azure App Service, consultez le Guide de configuration du fournisseur d’identité que vous souhaitez utiliser :</span><span class="sxs-lookup"><span data-stu-id="68869-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="68869-460">[Comment configurer votre application pour utiliser la connexion Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="68869-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="68869-461">[Comment configurer votre application pour utiliser une connexion Facebook]</span><span class="sxs-lookup"><span data-stu-id="68869-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="68869-462">[Comment configurer votre application pour utiliser une connexion Google]</span><span class="sxs-lookup"><span data-stu-id="68869-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="68869-463">[Comment configurer votre application pour utiliser une connexion par compte Microsoft]</span><span class="sxs-lookup"><span data-stu-id="68869-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="68869-464">[Comment configurer votre application pour utiliser une connexion Twitter]</span><span class="sxs-lookup"><span data-stu-id="68869-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="68869-465">La définition des API personnalisées est largement similaire à celle des API de tables.</span><span class="sxs-lookup"><span data-stu-id="68869-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="68869-466">Créez un répertoire **api** .</span><span class="sxs-lookup"><span data-stu-id="68869-466">Create an **api** directory</span></span>
2. <span data-ttu-id="68869-467">Créez un fichier JavaScript de définition d’API dans le répertoire **api** .</span><span class="sxs-lookup"><span data-stu-id="68869-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="68869-468">Utilisez la méthode import pour importer le répertoire **api** .</span><span class="sxs-lookup"><span data-stu-id="68869-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="68869-469">Voici le prototype de définition d’API dérivé de l’exemple d’application de base utilisé précédemment.</span><span class="sxs-lookup"><span data-stu-id="68869-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="68869-470">Prenons un exemple d’API qui renvoie la date du serveur à l’aide de la méthode *Date.now()* .</span><span class="sxs-lookup"><span data-stu-id="68869-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="68869-471">Voici le fichier api/date.js :</span><span class="sxs-lookup"><span data-stu-id="68869-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="68869-472">Chaque paramètre correspond à l’un des verbes RESTful standard : GET, POST, PATCH ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="68869-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="68869-473">La méthode est une fonction [ExpressJS Middleware] standard qui envoie la sortie requise.</span><span class="sxs-lookup"><span data-stu-id="68869-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="68869-474"><a name="howto-customapi-auth"></a>Procédure : exiger une authentification pour l’accès à une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="68869-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="68869-475">Le SDK Azure Mobile Apps implémente l’authentification de la même façon pour le point de terminaison des tables et pour les API personnalisées.</span><span class="sxs-lookup"><span data-stu-id="68869-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="68869-476">Pour ajouter l’authentification à l’API développée dans la section précédente, ajoutez une propriété **access** :</span><span class="sxs-lookup"><span data-stu-id="68869-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="68869-477">Vous pouvez également spécifier l’authentification sur des opérations spécifiques :</span><span class="sxs-lookup"><span data-stu-id="68869-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="68869-478">Pour les API personnalisées qui requièrent une authentification, vous devez utiliser le même jeton que celui utilisé pour le point de terminaison des tables.</span><span class="sxs-lookup"><span data-stu-id="68869-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="68869-479"><a name="howto-customapi-auth"></a>Procédure : gestion des téléchargements de fichiers volumineux</span><span class="sxs-lookup"><span data-stu-id="68869-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="68869-480">Le Kit de développement logiciel (SDK) Azure Mobile Apps utilise l’ [intergiciel corps-parser](https://github.com/expressjs/body-parser) pour accepter et décoder le contenu du corps de votre demande.</span><span class="sxs-lookup"><span data-stu-id="68869-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="68869-481">Vous pouvez préconfigurer corps-parser pour accepter les téléchargements de fichiers plus volumineux :</span><span class="sxs-lookup"><span data-stu-id="68869-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="68869-482">Le fichier est codé en base 64 avant la transmission.</span><span class="sxs-lookup"><span data-stu-id="68869-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="68869-483">Cela augmente la taille du téléchargement réel (et par conséquent la taille dont vous devez tenir compte).</span><span class="sxs-lookup"><span data-stu-id="68869-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="68869-484"><a name="howto-customapi-sql"></a>Procédure : exécution d’instructions SQL personnalisées</span><span class="sxs-lookup"><span data-stu-id="68869-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="68869-485">Le kit de développement logiciel (SDK) Azure Mobile Apps permet d’accéder à l’ensemble du contexte via l’objet de la demande, ce qui vous permet d’exécuter facilement des instructions SQL paramétrées pour le fournisseur de données défini :</span><span class="sxs-lookup"><span data-stu-id="68869-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="68869-486"><a name="Debugging"></a>Débogage, Tables facile et API simples</span><span class="sxs-lookup"><span data-stu-id="68869-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="68869-487"><a name="howto-diagnostic-logs"></a>Procédure : débogage, diagnostic et résolution des problèmes sur Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="68869-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="68869-488">Azure App Service fournit plusieurs techniques de débogage et de résolution des problèmes pour les applications Node.js.</span><span class="sxs-lookup"><span data-stu-id="68869-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="68869-489">Consultez les articles suivants pour prendre en main le dépannage de votre serveur principal mobile Node.js :</span><span class="sxs-lookup"><span data-stu-id="68869-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="68869-490">[Surveiller les applications web dans Microsoft Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="68869-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="68869-491">[Activer la journalisation des diagnostics pour les applications web dans Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="68869-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="68869-492">[Dépanner un service Azure App dans Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="68869-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="68869-493">Les applications Node.js ont accès à un large éventail d’outils de journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="68869-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="68869-494">En interne, le SDK Node.js Azure Mobile Apps utilise [Winston] pour la journalisation des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="68869-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="68869-495">La journalisation est activée automatiquement si vous activez le mode débogage ou définissez le paramètre d’application **MS_DebugMode** sur true dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="68869-496">Les journaux générés s’affichent dans les journaux de diagnostic sur le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="68869-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="68869-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Procédure : utilisation de l’outil Tables faciles dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="68869-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="68869-498">L’outil Easy Tables du portail vous permet de créer et utiliser des tables directement dans le portail.</span><span class="sxs-lookup"><span data-stu-id="68869-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="68869-499">Vous pouvez même modifier les opérations de table à l’aide de l’éditeur App Service.</span><span class="sxs-lookup"><span data-stu-id="68869-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="68869-500">Lorsque vous cliquez sur **Easy Tables** dans vos paramètres de site principal, vous pouvez ajouter, modifier ou supprimer une table.</span><span class="sxs-lookup"><span data-stu-id="68869-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="68869-501">Vous pouvez également voir les données de la table.</span><span class="sxs-lookup"><span data-stu-id="68869-501">You can also see data in the table.</span></span>

![Utilisation de l’outil Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="68869-503">Les commandes suivantes sont disponibles dans la barre de commandes d’une table :</span><span class="sxs-lookup"><span data-stu-id="68869-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="68869-504">**Modifier les autorisations** : modifier l’autorisation pour les opérations de lecture, d’insertion, de mise à jour et de suppression sur la table.</span><span class="sxs-lookup"><span data-stu-id="68869-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="68869-505">Vous avez la possibilité d’autoriser l’accès anonyme, d’exiger une authentification ou de désactiver tous les accès à l’opération.</span><span class="sxs-lookup"><span data-stu-id="68869-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="68869-506">**Modifier le script** : le fichier de script de la table est ouvert dans l’éditeur App Service.</span><span class="sxs-lookup"><span data-stu-id="68869-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="68869-507">**Gérer un schéma** : ajouter ou supprimer des colonnes ou modifier l’index de la table.</span><span class="sxs-lookup"><span data-stu-id="68869-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="68869-508">**Effacer la table** : tronque une table existante en supprimant toutes les lignes de données tout en conservant le schéma à l’identique.</span><span class="sxs-lookup"><span data-stu-id="68869-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="68869-509">**Supprimer des lignes** : supprimer des lignes de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="68869-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="68869-510">**Afficher les journaux de diffusion en continu** : permet de vous connecter au service de journaux de diffusion en continu de votre site.</span><span class="sxs-lookup"><span data-stu-id="68869-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="68869-511"><a name="work-easy-apis"></a>Procédure : utiliser l’outil Easy APIs dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="68869-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="68869-512">L’outil Easy APIs du portail vous permet de créer et utiliser des API personnalisées directement dans le portail.</span><span class="sxs-lookup"><span data-stu-id="68869-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="68869-513">Vous pouvez modifier des scripts API à l’aide de l’éditeur App Service.</span><span class="sxs-lookup"><span data-stu-id="68869-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="68869-514">Lorsque vous cliquez sur **Easy APIs** dans vos paramètres de site principal, vous pouvez ajouter modifier ou supprimer un point de terminaison API personnalisé.</span><span class="sxs-lookup"><span data-stu-id="68869-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Utilisation de l’outil Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="68869-516">Dans le portail, vous pouvez modifier les autorisations d’accès pour une action HTTP donnée, modifier le fichier de script d’API dans l’éditeur App Service ou afficher les journaux de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="68869-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="68869-517"><a name="online-editor"></a>Comment : modifier le code dans l’éditeur App Service</span><span class="sxs-lookup"><span data-stu-id="68869-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="68869-518">Le portail Azure vous permet de modifier les fichiers de script de votre serveur principal Node.js dans l’éditeur App Service sans avoir à télécharger le projet sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="68869-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="68869-519">Pour modifier les fichiers de script dans l’éditeur en ligne :</span><span class="sxs-lookup"><span data-stu-id="68869-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="68869-520">Dans le panneau de votre serveur principal d’application mobile, cliquez sur **Tous les paramètres** > **Tables faciles** ou **API faciles**, cliquez sur une table ou une API, puis cliquez sur **Modifier le script**.</span><span class="sxs-lookup"><span data-stu-id="68869-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="68869-521">Le fichier de script est ouvert dans l’éditeur App Service.</span><span class="sxs-lookup"><span data-stu-id="68869-521">The script file is opened in the App Service Editor.</span></span>

    ![Éditeur App Service](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="68869-523">Apportez vos modifications au fichier de code dans l’éditeur en ligne.</span><span class="sxs-lookup"><span data-stu-id="68869-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="68869-524">Les modifications sont enregistrées automatiquement au fil de la saisie.</span><span class="sxs-lookup"><span data-stu-id="68869-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="68869-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="68869-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="68869-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="68869-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="68869-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="68869-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="68869-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="68869-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="68869-532">[la synchronisation des données hors connexion]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="68869-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="68869-533">[Comment configurer votre application pour utiliser la connexion Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="68869-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="68869-534">[Comment configurer votre application pour utiliser une connexion Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="68869-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="68869-535">[Comment configurer votre application pour utiliser une connexion Google]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="68869-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="68869-536">[Comment configurer votre application pour utiliser une connexion par compte Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="68869-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="68869-537">[Comment configurer votre application pour utiliser une connexion Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="68869-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="68869-538">[Guide de déploiement d’Azure App Service]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="68869-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="68869-539">[Surveiller les applications web dans Microsoft Azure App Service]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="68869-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="68869-540">[Activer la journalisation des diagnostics pour les applications web dans Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="68869-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="68869-541">[Dépanner un service Azure App dans Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="68869-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="68869-542">[spécifier la version de Node]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="68869-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="68869-543">[utiliser les modules Node]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="68869-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="68869-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="68869-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="68869-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="68869-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="68869-546">[portail Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="68869-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="68869-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="68869-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="68869-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="68869-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="68869-549">[exemple basicapp sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="68869-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="68869-550">[exemple todo sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="68869-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="68869-551">[répertoire d’exemples sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="68869-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="68869-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="68869-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="68869-553">[Node.js Tools 1.1 pour Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="68869-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="68869-554">[package mssql Node]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="68869-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="68869-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="68869-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="68869-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="68869-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="68869-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="68869-557">[Winston]: https://github.com/winstonjs/winston</span></span>
