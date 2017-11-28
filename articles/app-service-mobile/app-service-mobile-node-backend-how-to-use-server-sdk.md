---
title: toowork aaaHow avec serveur principal de Node.js hello SDK pour applications mobiles | Documents Microsoft
description: "Découvrez comment toowork avec hello Node.js principal serveur SDK pour applications de Azure App Service Mobile."
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
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="7fc91-103">Comment toouse hello Azure Mobile Apps Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="7fc91-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="7fc91-104">Cet article fournit des informations détaillées et des exemples montrant comment toowork avec un service principal de Node.js dans Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="7fc91-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="7fc91-105"><a name="Introduction"></a>Introduction</span><span class="sxs-lookup"><span data-stu-id="7fc91-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="7fc91-106">Azure App Service Mobile Apps permet un accès données hello capacité tooadd mobile-optimisé application web de tooa API Web.</span><span class="sxs-lookup"><span data-stu-id="7fc91-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="7fc91-107">Hello Kit de développement logiciel Azure App Service Mobile Apps est fournie pour les applications web ASP.NET et Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fc91-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="7fc91-108">Hello SDK fournit hello opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fc91-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="7fc91-109">Opérations de table (Read, Insert, Update, Delete) pour l’accès aux données</span><span class="sxs-lookup"><span data-stu-id="7fc91-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="7fc91-110">Opérations d’API personnalisées</span><span class="sxs-lookup"><span data-stu-id="7fc91-110">Custom API operations</span></span>

<span data-ttu-id="7fc91-111">Les deux types d’opérations permettent une authentification entre tous les fournisseurs d’identité autorisés par Azure App Service, y compris les fournisseurs d’identité sociaux tels que Facebook, Twitter, Google et Microsoft, ainsi qu’Azure Active Directory pour les identités d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7fc91-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="7fc91-112">Vous trouverez des exemples pour chaque cas d’usage dans hello [répertoire d’exemples sur GitHub].</span><span class="sxs-lookup"><span data-stu-id="7fc91-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="7fc91-113">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="7fc91-113">Supported Platforms</span></span>
<span data-ttu-id="7fc91-114">Bonjour Azure Mobile Apps nœud SDK prend en charge hello que LTS actuels de version de nœud et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="7fc91-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="7fc91-115">Au moment de la rédaction, dernière version LTS hello est v4.5.0 de nœud.</span><span class="sxs-lookup"><span data-stu-id="7fc91-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="7fc91-116">Les autres versions de Node peuvent fonctionner, mais elles ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7fc91-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="7fc91-117">Bonjour Azure Mobile Apps nœud SDK prend en charge deux pilotes de base de données - hello mssql de nœud pilote prend en charge SQL Azure et les instances locales de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7fc91-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="7fc91-118">pilote de sqlite3 Hello prend en charge les bases de données SQLite sur une seule instance.</span><span class="sxs-lookup"><span data-stu-id="7fc91-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="7fc91-119"><a name="howto-cmdline-basicapp"></a>Comment : créer un service principal de base Node.js à l’aide de la ligne de commande de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="7fc91-120">Chaque serveur principal Node.js Azure App Service Mobile Apps démarre en tant qu’application ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="7fc91-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="7fc91-121">ExpressJS est hello plus populaires infrastructure de service web disponible pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fc91-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="7fc91-122">Vous pouvez créer une application [Express] de base de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="7fc91-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="7fc91-123">Dans une commande ou une fenêtre PowerShell, créez un répertoire pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="7fc91-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="7fc91-124">Exécutez la structure du package npm init tooinitialize hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="7fc91-125">commande d’init Hello npm demande un ensemble d’un projet de questions tooinitialize hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="7fc91-126">Consultez la sortie de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="7fc91-126">See hello example output:</span></span>

    ![sortie d’init Hello npm][0]
3. <span data-ttu-id="7fc91-128">Installer les bibliothèques d’express et applications azure-mobile de hello de dépôt de npm hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="7fc91-129">Création d’un serveur app.js fichier tooimplement hello base mobile.</span><span class="sxs-lookup"><span data-stu-id="7fc91-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="7fc91-130">Cette application crée un WebAPI mobile optimisé avec un seul point de terminaison (`/tables/TodoItem`) qui fournit des tooan accès non authentifié sous-jacent du magasin de données SQL à l’aide d’un schéma dynamique.</span><span class="sxs-lookup"><span data-stu-id="7fc91-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="7fc91-131">Cette API est adaptée pour les démarrages rapides de bibliothèques client suivants :</span><span class="sxs-lookup"><span data-stu-id="7fc91-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="7fc91-132">[Android Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="7fc91-133">[Apache Cordova Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="7fc91-134">[iOS Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="7fc91-135">[Windows Store Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="7fc91-136">[Xamarin.iOS Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="7fc91-137">[Xamarin.Android Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="7fc91-138">[Xamarin.Forms Client QuickStart]</span><span class="sxs-lookup"><span data-stu-id="7fc91-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="7fc91-139">Vous pouvez trouver le code de hello pour cette application de base hello [exemple basicapp sur GitHub].</span><span class="sxs-lookup"><span data-stu-id="7fc91-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="7fc91-140"><a name="howto-vs2015-basicapp"></a>Procédure : créer un serveur principal Node avec Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7fc91-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="7fc91-141">Visual Studio 2015 requiert une extension toodevelop Node.js les applications au sein de hello IDE.</span><span class="sxs-lookup"><span data-stu-id="7fc91-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="7fc91-142">toostart, installation hello [Node.js Tools 1.1 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="7fc91-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="7fc91-143">Une fois que hello Node.js Tools pour Visual Studio sont installés, créer une application de 4.x Express :</span><span class="sxs-lookup"><span data-stu-id="7fc91-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="7fc91-144">Ouvrez hello **nouveau projet** boîte de dialogue (à partir de **fichier** > **nouveau** > **projet...** ).</span><span class="sxs-lookup"><span data-stu-id="7fc91-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="7fc91-145">Développez **Modèles** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="7fc91-146">Sélectionnez hello **Basic Azure Node.js Express 4 Application**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="7fc91-147">Renseignez le nom du projet hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-147">Fill in hello project name.</span></span>  <span data-ttu-id="7fc91-148">Cliquez sur *OK*.</span><span class="sxs-lookup"><span data-stu-id="7fc91-148">Click *OK*.</span></span>

    ![Visual Studio 2015 Nouveau projet][1]
5. <span data-ttu-id="7fc91-150">Avec le bouton hello **npm** nœud et sélectionnez **installer de nouveaux packages npm...** .</span><span class="sxs-lookup"><span data-stu-id="7fc91-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="7fc91-151">Vous devrez peut-être le catalogue de npm toorefresh hello sur la création de votre première application Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fc91-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="7fc91-152">Cliquez sur **Actualiser** si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7fc91-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="7fc91-153">Entrez *azure-mobile-apps* dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="7fc91-154">Cliquez sur hello **azure-mobile-apps 2.0.0** du package, puis cliquez sur **installer le Package**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Installer de nouveaux packages npm][2]
8. <span data-ttu-id="7fc91-156">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-156">Click **Close**.</span></span>
9. <span data-ttu-id="7fc91-157">Ouvrez hello *app.js* hello Azure Mobile Apps SDK tooadd prise en charge de fichiers.</span><span class="sxs-lookup"><span data-stu-id="7fc91-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="7fc91-158">À la ligne 6 at hello en bas de la bibliothèque de hello nécessitent des instructions, ajoutez les hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7fc91-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="7fc91-159">À la ligne environ 27 après hello autres instructions app.use, ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7fc91-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="7fc91-160">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-160">Save hello file.</span></span>
10. <span data-ttu-id="7fc91-161">Exécutez l’application hello localement (hello API est pris en charge sur http://localhost:3000) soit publier tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7fc91-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="7fc91-162"><a name="create-node-backend-portal"></a>Comment : créer un serveur Node.js principal à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fc91-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="7fc91-163">Vous pouvez créer un droit de principal de l’application Mobile Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="7fc91-164">Vous pouvez suivre soit hello en suivant les étapes ou créer un client et un serveur ensemble en suivant les hello [créer une application mobile](app-service-mobile-ios-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7fc91-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="7fc91-165">didacticiel de Hello contient une version simplifiée de ces instructions et convient pour la preuve de projets de concept.</span><span class="sxs-lookup"><span data-stu-id="7fc91-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="7fc91-166">Dans hello *prise en main* panneau, sous **créer une table API**, choisissez **Node.js** en tant que votre **principal langage**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="7fc91-167">Case de hello pour «**je reconnais que cette opération va remplacer tout contenu de site.**», puis cliquez sur **table TodoItem de créer**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="7fc91-168"><a name="download-quickstart"></a>Comment : télécharger hello Node.js principal quickstart projet de code à l’aide de Git</span><span class="sxs-lookup"><span data-stu-id="7fc91-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="7fc91-169">Lorsque vous créez un service principal de l’application Mobile Node.js à l’aide du portail de hello **démarrage rapide** panneau, un projet Node.js est créé pour vous et le site de tooyour déployé.</span><span class="sxs-lookup"><span data-stu-id="7fc91-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="7fc91-170">Vous pouvez ajouter des tables et des API et modifier des fichiers de code pour le serveur principal de Node.js hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="7fc91-171">Vous pouvez également utiliser le projet de service principal hello différents déploiement outils toodownload afin que vous pouvez ajouter ou modifier des tables et des API, puis republier le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="7fc91-172">Pour plus d’informations, consultez le [Guide de déploiement d’Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="7fc91-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="7fc91-173">Hello procédure suivante utilise un code de projet de démarrage rapide Git référentiel toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="7fc91-174">Si vous ne l’avez pas déjà fait, installez Git.</span><span class="sxs-lookup"><span data-stu-id="7fc91-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="7fc91-175">tooinstall requis des étapes de Hello Git varient entre les systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="7fc91-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="7fc91-176">Consultez la rubrique [Installation de Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) pour accéder aux distributions et consignes d'installation propres aux différents systèmes d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="7fc91-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="7fc91-177">Suivez les étapes de hello dans [activer hello référentiel d’application de Service d’applications](../app-service-web/app-service-deploy-local-git.md#Step3) référentiel de Git tooenable hello pour votre site principal, une annotation de nom d’utilisateur du déploiement hello et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7fc91-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="7fc91-178">Dans le panneau de hello pour votre serveur principal de l’application Mobile, prenez note de hello **URL de clone Git** paramètre.</span><span class="sxs-lookup"><span data-stu-id="7fc91-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="7fc91-179">Exécutez hello `git clone` commande à l’aide des URL de clone Git hello, entrer votre mot de passe à la demande, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7fc91-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="7fc91-180">Parcourir toolocal répertoire Bonjour précédent exemple /todolist et notez que les fichiers de projet ont été téléchargés.</span><span class="sxs-lookup"><span data-stu-id="7fc91-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="7fc91-181">Recherchez hello `todoitem.json` fichier Bonjour `/tables` active.</span><span class="sxs-lookup"><span data-stu-id="7fc91-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="7fc91-182">Ce fichier définit les autorisations sur la table.</span><span class="sxs-lookup"><span data-stu-id="7fc91-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="7fc91-183">Recherche également les hello `todoitem.js` fichier Bonjour même répertoire, qui définit les opérations CRUD sont effectuées de scripts pour la table de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="7fc91-184">Une fois que vous avez apporté des modifications tooproject fichiers, exécutez hello suivant les commandes tooadd, valider, puis télécharger le site de toohello de modifications :</span><span class="sxs-lookup"><span data-stu-id="7fc91-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="7fc91-185">Lorsque vous ajoutez de nouveau projet toohello de fichiers, vous devez tout d’abord tooexecute hello `git add .` commande.</span><span class="sxs-lookup"><span data-stu-id="7fc91-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="7fc91-186">site de Hello est republiée chaque fois qu’un nouvel ensemble de validation est transmise toohello site.</span><span class="sxs-lookup"><span data-stu-id="7fc91-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="7fc91-187"><a name="howto-publish-to-azure"></a>Comment : publier votre tooAzure de back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="7fc91-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="7fc91-188">Microsoft Azure fournit plusieurs mécanismes pour la publication de votre serveur principal d’Azure App Service Mobile applications Node.js pour hello service Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc91-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="7fc91-189">En fonction du contrôle de la source, vous pouvez notamment utiliser les outils de déploiement intégrés à Visual Studio, les outils de ligne de commande et les options de déploiement continu.</span><span class="sxs-lookup"><span data-stu-id="7fc91-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="7fc91-190">Pour plus d’informations sur ce sujet, reportez-vous au [Guide de déploiement d’Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="7fc91-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="7fc91-191">Avant le déploiement, vous devriez prendre connaissance des recommandations suivantes pour l’application Node.js avec Azure App Service :</span><span class="sxs-lookup"><span data-stu-id="7fc91-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="7fc91-192">Comment trop[spécifier hello Version du nœud]</span><span class="sxs-lookup"><span data-stu-id="7fc91-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="7fc91-193">Comment trop[utiliser des modules de nœud]</span><span class="sxs-lookup"><span data-stu-id="7fc91-193">How too[use Node modules]</span></span>

### <span data-ttu-id="7fc91-194"><a name="howto-enable-homepage"></a>Procédure : activation d’une page d’accueil pour votre application</span><span class="sxs-lookup"><span data-stu-id="7fc91-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="7fc91-195">De nombreuses applications sont une combinaison d’applications web et mobiles et hello ExpressJS infrastructure permet de toocombine les deux facettes.</span><span class="sxs-lookup"><span data-stu-id="7fc91-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="7fc91-196">Dans certains cas, toutefois, vous pouvez choisir tooonly implémentent une interface mobile.</span><span class="sxs-lookup"><span data-stu-id="7fc91-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="7fc91-197">Il est utile tooprovide qu'un lancement page tooensure hello app service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7fc91-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="7fc91-198">Vous pouvez soit fournir votre propre page d’accueil, soit activer une page d’accueil temporaire.</span><span class="sxs-lookup"><span data-stu-id="7fc91-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="7fc91-199">tooenable une page d’accueil temporaire, utilisez hello suivant tooinstantiate Azure Mobile Apps :</span><span class="sxs-lookup"><span data-stu-id="7fc91-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="7fc91-200">Si vous ne souhaitez que cette option disponible lors du développement localement, vous pouvez ajouter cette tooyour paramètre `azureMobile.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="7fc91-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="7fc91-201"><a name="TableOperations"></a>Opérations de table</span><span class="sxs-lookup"><span data-stu-id="7fc91-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="7fc91-202">Bonjour azure-mobile-applications Node.js serveur SDK fournit des mécanismes tooexpose données tables stockées dans la base de données SQL Azure comme un WebAPI.</span><span class="sxs-lookup"><span data-stu-id="7fc91-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="7fc91-203">Cinq opérations sont fournies.</span><span class="sxs-lookup"><span data-stu-id="7fc91-203">Five operations are provided.</span></span>

| <span data-ttu-id="7fc91-204">Opération</span><span class="sxs-lookup"><span data-stu-id="7fc91-204">Operation</span></span> | <span data-ttu-id="7fc91-205">Description</span><span class="sxs-lookup"><span data-stu-id="7fc91-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7fc91-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="7fc91-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="7fc91-207">Obtenir tous les enregistrements dans la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-207">Get all records in hello table</span></span> |
| <span data-ttu-id="7fc91-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="7fc91-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="7fc91-209">Obtenir un enregistrement spécifique dans la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="7fc91-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="7fc91-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="7fc91-211">Créer un enregistrement dans la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-211">Create a record in hello table</span></span> |
| <span data-ttu-id="7fc91-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="7fc91-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="7fc91-213">Mettre à jour un enregistrement dans la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-213">Update a record in hello table</span></span> |
| <span data-ttu-id="7fc91-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="7fc91-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="7fc91-215">Supprimer un enregistrement dans la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-215">Delete a record in hello table</span></span> |

<span data-ttu-id="7fc91-216">Prend en charge de cette WebAPI [OData] et étend hello table schéma toosupport [synchronisation des données hors connexion].</span><span class="sxs-lookup"><span data-stu-id="7fc91-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="7fc91-217"><a name="howto-dynamicschema"></a>Procédure : définir des tables à l’aide d’un schéma dynamique</span><span class="sxs-lookup"><span data-stu-id="7fc91-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="7fc91-218">Avant de pouvoir utiliser une table, vous devez la définir.</span><span class="sxs-lookup"><span data-stu-id="7fc91-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="7fc91-219">Les tables peuvent être définies avec un schéma statique (où les développeurs hello définit colonnes hello dans le schéma de hello) ou dynamique (où hello SDK contrôle schéma hello en fonction des demandes entrantes).</span><span class="sxs-lookup"><span data-stu-id="7fc91-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="7fc91-220">En outre, développeur de hello peut contrôler des aspects spécifiques du hello WebAPI en ajoutant la définition toohello du code Javascript.</span><span class="sxs-lookup"><span data-stu-id="7fc91-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="7fc91-221">Comme meilleure pratique, vous devez définir chaque table dans un fichier Javascript dans le répertoire de tables hello, puis utiliser les tables de hello tables.import() méthode tooimport.</span><span class="sxs-lookup"><span data-stu-id="7fc91-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="7fc91-222">Extension basic-application hello, fichier de app.js hello seront ajusté :</span><span class="sxs-lookup"><span data-stu-id="7fc91-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="7fc91-223">Définir la table hello dans. / tables/TodoItem.js :</span><span class="sxs-lookup"><span data-stu-id="7fc91-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="7fc91-224">Par défaut, les tables utilisent le schéma dynamique.</span><span class="sxs-lookup"><span data-stu-id="7fc91-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="7fc91-225">tooturn hors schéma dynamique définie globalement, hello paramètre d’application **MS_DynamicSchema** toofalse dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7fc91-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="7fc91-226">Vous trouverez un exemple complet dans hello [exemple todo sur GitHub].</span><span class="sxs-lookup"><span data-stu-id="7fc91-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="7fc91-227"><a name="howto-staticschema"></a>Procédure : définir des tables à l’aide d’un schéma statique</span><span class="sxs-lookup"><span data-stu-id="7fc91-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="7fc91-228">Vous pouvez définir explicitement tooexpose de colonnes hello via hello WebAPI.</span><span class="sxs-lookup"><span data-stu-id="7fc91-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="7fc91-229">Bonjour qu'azure-mobile-applications Node.js SDK ajoute automatiquement des colonnes supplémentaires requis pour la liste de toohello de synchronisation des données hors connexion que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="7fc91-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="7fc91-230">Par exemple, les applications clientes QuickStart requièrent une table à deux colonnes : une colonne texte (une chaîne) et une colonne complète (une valeur booléenne).</span><span class="sxs-lookup"><span data-stu-id="7fc91-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="7fc91-231">table de Hello peut être défini dans hello tableau JavaScript fichier de définition (situé dans le répertoire de tables hello) comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fc91-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="7fc91-232">Si vous définissez des tables statiquement, vous devez également appeler schéma de la base de données hello tables.initialize() méthode toocreate hello au démarrage.</span><span class="sxs-lookup"><span data-stu-id="7fc91-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="7fc91-233">Hello tables.initialize() méthode retourne un [promesse] afin que le service web de hello n’utilise pas les demandes avant l’initialisation de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="7fc91-234"><a name="howto-sqlexpress-setup"></a>Procédure : utiliser SQL Express comme datastore de développement sur votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="7fc91-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="7fc91-235">les applications mobiles Azure hello AzureMobile applications nœud SDK Hello offre trois options pour traiter les données en dehors de la zone de hello : Kit de développement logiciel offre trois options pour traiter les données en dehors de la zone de hello :</span><span class="sxs-lookup"><span data-stu-id="7fc91-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="7fc91-236">Hello d’utilisation **mémoire** magasin pilote tooprovide non persistant</span><span class="sxs-lookup"><span data-stu-id="7fc91-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="7fc91-237">Hello d’utilisation **mssql** pilote tooprovide un magasin de données SQL Express pour le développement</span><span class="sxs-lookup"><span data-stu-id="7fc91-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="7fc91-238">Hello d’utilisation **mssql** pilote tooprovide une banque de données de base de données SQL Azure pour la production</span><span class="sxs-lookup"><span data-stu-id="7fc91-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="7fc91-239">Bonjour Azure Mobile Apps Node.js SDK utilise hello [mssql Node.js package] tooestablish et utiliser un tooboth de connexion SQL Express et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7fc91-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="7fc91-240">Ce package nécessite l’activation de connexions TCP sur votre instance SQL Express.</span><span class="sxs-lookup"><span data-stu-id="7fc91-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="7fc91-241">pilote de la mémoire Hello ne fournit pas un ensemble complet des installations de test.</span><span class="sxs-lookup"><span data-stu-id="7fc91-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="7fc91-242">Si vous le souhaitez tootest votre serveur principal localement, nous vous recommandons d’utiliser un magasin de données SQL Express hello et hello mssql pilote.</span><span class="sxs-lookup"><span data-stu-id="7fc91-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="7fc91-243">Téléchargez et installez [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="7fc91-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="7fc91-244">Assurez-vous que vous installez hello SQL Server 2014 Express avec l’édition des outils.</span><span class="sxs-lookup"><span data-stu-id="7fc91-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="7fc91-245">Sauf si vous avez besoin explicitement la prise en charge 64 bits, version 32 bits de hello consomme moins de mémoire lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="7fc91-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="7fc91-246">Exécutez hello Gestionnaire de Configuration SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="7fc91-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="7fc91-247">Développez hello **Configuration du réseau SQL Server** nœud dans le menu de gauche arborescence hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="7fc91-248">Cliquez sur **Protocols for SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="7fc91-249">Cliquez avec le bouton droit sur **TCP/IP**, puis sélectionnez **Enable**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="7fc91-250">Cliquez sur **OK** dans la boîte de dialogue contextuelle hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="7fc91-251">Cliquez avec le bouton droit sur **TCP/IP**, puis sélectionnez **Properties**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="7fc91-252">Cliquez sur hello **des adresses IP** onglet.</span><span class="sxs-lookup"><span data-stu-id="7fc91-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="7fc91-253">Recherche hello **IPAll** nœud.</span><span class="sxs-lookup"><span data-stu-id="7fc91-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="7fc91-254">Bonjour **le Port TCP** , entrez **1433**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="7fc91-255">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-255">Click **OK**.</span></span>  <span data-ttu-id="7fc91-256">Cliquez sur **OK** dans la boîte de dialogue contextuelle hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="7fc91-257">Cliquez sur **Services SQL Server** dans le menu de gauche arborescence hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="7fc91-258">Cliquez avec le bouton droit sur **SQL Server (SQLEXPRESS)**, puis sélectionnez **Restart**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="7fc91-259">Fermez hello Gestionnaire de Configuration SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="7fc91-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="7fc91-260">Exécutez hello SQL Server 2014 Management Studio et se connecter à l’instance SQL Express local tooyour</span><span class="sxs-lookup"><span data-stu-id="7fc91-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="7fc91-261">Avec le bouton droit de votre instance Bonjour l’Explorateur d’objets et sélectionnez **propriétés**</span><span class="sxs-lookup"><span data-stu-id="7fc91-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="7fc91-262">Sélectionnez hello **sécurité** page.</span><span class="sxs-lookup"><span data-stu-id="7fc91-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="7fc91-263">Assurez-vous de hello **mode d’authentification SQL Server et Windows** est sélectionné</span><span class="sxs-lookup"><span data-stu-id="7fc91-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="7fc91-264">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="7fc91-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="7fc91-265">Développez **sécurité** > **connexions** Bonjour l’Explorateur d’objets</span><span class="sxs-lookup"><span data-stu-id="7fc91-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="7fc91-266">Cliquez avec le bouton droit sur **Connexions** et sélectionnez **Nouvelle connexion...**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="7fc91-267">Entrez un nom de connexion.</span><span class="sxs-lookup"><span data-stu-id="7fc91-267">Enter a Login name.</span></span>  <span data-ttu-id="7fc91-268">Sélectionnez **Authentification SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="7fc91-269">Entrez un mot de passe, puis entrez hello dans le même mot de passe **confirmer le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="7fc91-270">mot de passe Hello doit répondre aux exigences de complexité Windows.</span><span class="sxs-lookup"><span data-stu-id="7fc91-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="7fc91-271">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="7fc91-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="7fc91-272">Cliquez avec le bouton droit sur votre nouveau compte de connexion et sélectionnez **Properties**</span><span class="sxs-lookup"><span data-stu-id="7fc91-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="7fc91-273">Sélectionnez hello **rôles serveur** page</span><span class="sxs-lookup"><span data-stu-id="7fc91-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="7fc91-274">Vérifiez toohello suivant de zone hello **dbcreator** rôle de serveur</span><span class="sxs-lookup"><span data-stu-id="7fc91-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="7fc91-275">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="7fc91-275">Click **OK**</span></span>
   13. <span data-ttu-id="7fc91-276">Hello fermer SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="7fc91-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="7fc91-277">Vérifiez que vous vous avez sélectionné un mot de passe et de nom d’utilisateur de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="7fc91-278">Vous devrez peut-être tooassign des rôles serveur supplémentaires ou des autorisations en fonction de vos besoins spécifiques de la base de données.</span><span class="sxs-lookup"><span data-stu-id="7fc91-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="7fc91-279">Hello application Node.js lit hello **SQLCONNSTR_MS_TableConnectionString** variable d’environnement pour la chaîne de connexion hello pour cette base de données.</span><span class="sxs-lookup"><span data-stu-id="7fc91-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="7fc91-280">Vous pouvez définir cette variable dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="7fc91-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="7fc91-281">Par exemple, vous pouvez utiliser PowerShell tooset cette variable d’environnement :</span><span class="sxs-lookup"><span data-stu-id="7fc91-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="7fc91-282">Hello d’accès via une connexion TCP/IP de base de données et fournir un nom d’utilisateur et un mot de passe de connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="7fc91-283"><a name="howto-config-localdev"></a>Procédure : configurer votre projet pour un développement local</span><span class="sxs-lookup"><span data-stu-id="7fc91-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="7fc91-284">Azure Mobile Apps lit un fichier JavaScript nommé *azureMobile.js* hello de système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="7fc91-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="7fc91-285">Effectuer pas utiliser cette hello tooconfigure de fichier Azure Mobile Apps SDK en production, utiliser les paramètres de l’application au sein de hello [portail Azure] à la place.</span><span class="sxs-lookup"><span data-stu-id="7fc91-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="7fc91-286">Hello *azureMobile.js* fichier doit exporter un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="7fc91-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="7fc91-287">Hello plus courantes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fc91-287">hello most common settings are:</span></span>

* <span data-ttu-id="7fc91-288">Paramètres de base de données</span><span class="sxs-lookup"><span data-stu-id="7fc91-288">Database Settings</span></span>
* <span data-ttu-id="7fc91-289">Paramètres de journalisation des diagnostics</span><span class="sxs-lookup"><span data-stu-id="7fc91-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="7fc91-290">Paramètres CORS de remplacement</span><span class="sxs-lookup"><span data-stu-id="7fc91-290">Alternate CORS Settings</span></span>

<span data-ttu-id="7fc91-291">Un exemple *azureMobile.js* fichier mettant en œuvre hello précédant suit les paramètres de base de données :</span><span class="sxs-lookup"><span data-stu-id="7fc91-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

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

<span data-ttu-id="7fc91-292">Nous vous conseillons *azureMobile.js* tooyour *.gitignore* fichier (ou un autre contrôle de code source ignorer le fichier) tooprevent les mots de passe d’être stockées dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="7fc91-293">Configurez toujours les paramètres de production dans les paramètres de l’application au sein de hello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="7fc91-294"><a name="howto-appsettings"></a>Procédure : configuration des paramètres d’application pour votre application mobile</span><span class="sxs-lookup"><span data-stu-id="7fc91-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="7fc91-295">La plupart des paramètres hello *azureMobile.js* fichier a un paramètre d’application équivalent Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="7fc91-296">Utilisez hello suivant liste tooconfigure votre application dans les paramètres de l’application :</span><span class="sxs-lookup"><span data-stu-id="7fc91-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="7fc91-297">Paramètre d'application</span><span class="sxs-lookup"><span data-stu-id="7fc91-297">App Setting</span></span> | <span data-ttu-id="7fc91-298">*azureMobile.js*</span><span class="sxs-lookup"><span data-stu-id="7fc91-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="7fc91-299">Description</span><span class="sxs-lookup"><span data-stu-id="7fc91-299">Description</span></span> | <span data-ttu-id="7fc91-300">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="7fc91-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="7fc91-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="7fc91-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="7fc91-302">name</span><span class="sxs-lookup"><span data-stu-id="7fc91-302">name</span></span> |<span data-ttu-id="7fc91-303">nom de l’application hello de Hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-303">hello name of hello app</span></span> |<span data-ttu-id="7fc91-304">string</span><span class="sxs-lookup"><span data-stu-id="7fc91-304">string</span></span> |
| <span data-ttu-id="7fc91-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="7fc91-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="7fc91-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="7fc91-306">logging.level</span></span> |<span data-ttu-id="7fc91-307">Niveau de journal minimal de messages toolog</span><span class="sxs-lookup"><span data-stu-id="7fc91-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="7fc91-308">error, warning, info, verbose, debug, silly</span><span class="sxs-lookup"><span data-stu-id="7fc91-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="7fc91-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="7fc91-309">**MS_DebugMode**</span></span> |<span data-ttu-id="7fc91-310">debug</span><span class="sxs-lookup"><span data-stu-id="7fc91-310">debug</span></span> |<span data-ttu-id="7fc91-311">Activer ou désactiver le mode débogage</span><span class="sxs-lookup"><span data-stu-id="7fc91-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="7fc91-312">true, false</span><span class="sxs-lookup"><span data-stu-id="7fc91-312">true, false</span></span> |
| <span data-ttu-id="7fc91-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="7fc91-313">**MS_TableSchema**</span></span> |<span data-ttu-id="7fc91-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="7fc91-314">data.schema</span></span> |<span data-ttu-id="7fc91-315">Nom de schéma par défaut pour les tables SQL</span><span class="sxs-lookup"><span data-stu-id="7fc91-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="7fc91-316">string (valeur par défaut : dbo)</span><span class="sxs-lookup"><span data-stu-id="7fc91-316">string (default: dbo)</span></span> |
| <span data-ttu-id="7fc91-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="7fc91-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="7fc91-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="7fc91-318">data.dynamicSchema</span></span> |<span data-ttu-id="7fc91-319">Activer ou désactiver le mode débogage</span><span class="sxs-lookup"><span data-stu-id="7fc91-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="7fc91-320">true, false</span><span class="sxs-lookup"><span data-stu-id="7fc91-320">true, false</span></span> |
| <span data-ttu-id="7fc91-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="7fc91-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="7fc91-322">version (jeu tooundefined)</span><span class="sxs-lookup"><span data-stu-id="7fc91-322">version (set tooundefined)</span></span> |<span data-ttu-id="7fc91-323">Désactive l’en-tête de hello X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="7fc91-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="7fc91-324">true, false</span><span class="sxs-lookup"><span data-stu-id="7fc91-324">true, false</span></span> |
| <span data-ttu-id="7fc91-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="7fc91-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="7fc91-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="7fc91-326">skipversioncheck</span></span> |<span data-ttu-id="7fc91-327">Désactive la vérification de la version API client hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-327">Disables hello client API version check</span></span> |<span data-ttu-id="7fc91-328">true, false</span><span class="sxs-lookup"><span data-stu-id="7fc91-328">true, false</span></span> |

<span data-ttu-id="7fc91-329">tooset un paramètre d’application :</span><span class="sxs-lookup"><span data-stu-id="7fc91-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="7fc91-330">Connectez-vous à toohello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="7fc91-331">Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre application Mobile.</span><span class="sxs-lookup"><span data-stu-id="7fc91-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="7fc91-332">Panneau de paramètres Hello s’ouvre par défaut.</span><span class="sxs-lookup"><span data-stu-id="7fc91-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="7fc91-333">Si ce n’est pas le cas, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="7fc91-334">Cliquez sur **paramètres de l’Application** menu général de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="7fc91-335">Faites défiler toohello section de paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="7fc91-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="7fc91-336">Si votre application de définir déjà existe, cliquez sur valeur hello valeur hello tooedit du paramètre d’application hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="7fc91-337">Si votre paramètre d’application n’existe pas, entrez hello paramètre d’application dans la boîte de clé hello et valeur hello dans la zone de valeur hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="7fc91-338">Une fois que vous avez terminé, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="7fc91-339">La modification de la plupart des paramètres requiert le redémarrage du service.</span><span class="sxs-lookup"><span data-stu-id="7fc91-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="7fc91-340"><a name="howto-use-sqlazure"></a>Procédure : utiliser la base de données SQL comme datastore de production</span><span class="sxs-lookup"><span data-stu-id="7fc91-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="7fc91-341">L’utilisation de la base de données SQL Azure en tant que datastore est identique pour tous les types d’applications Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7fc91-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="7fc91-342">Si vous n’avez pas déjà fait, suivez ces étapes de toocreate un service principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="7fc91-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="7fc91-343">Connectez-vous à toohello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="7fc91-344">Dans hello haut à gauche de la fenêtre hello, cliquez sur hello **+ nouveau** bouton > **Web + Mobile** > **l’application Mobile**, puis indiquez un nom pour votre serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="7fc91-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="7fc91-345">Bonjour **groupe de ressources** , entrez le même nom que celui de hello en tant que votre application.</span><span class="sxs-lookup"><span data-stu-id="7fc91-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="7fc91-346">plan de Service par défaut de l’application Hello est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="7fc91-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="7fc91-347">Si vous le souhaitez toochange votre plan App Service, vous pouvez le faire en cliquant sur hello Plan App Service > **+ créer de nouveaux**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="7fc91-348">Fournir un nom d’un nouveau plan de Service de l’application hello et sélectionnez un emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="7fc91-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="7fc91-349">Cliquez sur le niveau de tarification hello et sélectionnez un niveau de tarification approprié pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="7fc91-350">Sélectionnez **afficher toutes les** tooview plus tarification options, telles que **libre** et **partagé**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="7fc91-351">Une fois que vous avez sélectionné le niveau de tarification, cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="7fc91-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="7fc91-352">Dans hello **plan App Service** panneau, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="7fc91-353">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-353">Click **Create**.</span></span> <span data-ttu-id="7fc91-354">La configuration d’un serveur principal d’application mobile peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7fc91-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="7fc91-355">Une fois que le serveur principal de l’application Mobile hello est configuré, le portail de hello ouvre hello **paramètres** panneau pour le serveur principal de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="7fc91-356">Une fois que le principal de l’application Mobile hello est créé, vous pouvez choisir tooeither se connecter à une base de données SQL existante principale de l’application Mobile tooyour ou créer une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7fc91-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="7fc91-357">Dans cette section, nous créons une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7fc91-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="7fc91-358">Si vous disposez déjà d’une base de données Bonjour même emplacement en tant que serveur principal d’application mobile hello, vous pouvez à la place choisir **utiliser une base de données** , puis sélectionnez la base de données.</span><span class="sxs-lookup"><span data-stu-id="7fc91-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="7fc91-359">utilisation de Hello d’une base de données dans un autre emplacement n’est pas recommandée en raison des latences supérieures.</span><span class="sxs-lookup"><span data-stu-id="7fc91-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="7fc91-360">Dans le nouveau principal d’application Mobile hello, cliquez sur **paramètres** > **l’application Mobile** > **données** > **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="7fc91-361">Bonjour **ajouter une connexion de données** panneau, cliquez sur **base de données SQL - configurer les paramètres requis** > **créer une base de données**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="7fc91-362">Entrez le nom hello de base de données hello Bonjour **nom** champ.</span><span class="sxs-lookup"><span data-stu-id="7fc91-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="7fc91-363">Cliquez sur **Serveur**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-363">Click **Server**.</span></span>  <span data-ttu-id="7fc91-364">Bonjour **nouveau serveur** panneau, entrez un nom de serveur unique Bonjour **nom du serveur** champ et fournir un approprié **ouverture de session de serveur admin** et **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="7fc91-365">Vérifiez **server d’Autoriser les services azure tooaccess** est activée.</span><span class="sxs-lookup"><span data-stu-id="7fc91-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="7fc91-366">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-366">Click **OK**.</span></span>

    ![Création d’une base de données SQL Azure][6]
4. <span data-ttu-id="7fc91-368">Sur hello **nouvelle base de données** panneau, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="7fc91-369">Retour sur hello **ajouter une connexion de données** panneau, sélectionnez **chaîne de connexion**, entrez le compte de connexion hello et un mot de passe que vous avez fourni lors de la création de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="7fc91-370">Si vous utilisez une base de données existante, fournissez les informations d’identification du compte de connexion de hello pour cette base de données.</span><span class="sxs-lookup"><span data-stu-id="7fc91-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="7fc91-371">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="7fc91-372">Retour sur hello **ajouter une connexion de données** panneau, cliquez sur **OK** base de données toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="7fc91-373">La création de base de données hello peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7fc91-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="7fc91-374">Hello d’utilisation **Notifications** progression de hello toomonitor zone du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="7fc91-375">Ne progressent pas jusqu'à ce que la base de données hello a été déployée avec succès.</span><span class="sxs-lookup"><span data-stu-id="7fc91-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="7fc91-376">Une fois déployée, une chaîne de connexion est créée pour l’instance de base de données SQL hello dans vos paramètres de l’application de service principal Mobile.</span><span class="sxs-lookup"><span data-stu-id="7fc91-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="7fc91-377">Vous pouvez voir ce paramètre d’application Bonjour **paramètres** > **paramètres de l’Application** > **les chaînes de connexion**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="7fc91-378"><a name="howto-tables-auth"></a>Comment : demander l’authentification pour accès tootables</span><span class="sxs-lookup"><span data-stu-id="7fc91-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="7fc91-379">Si vous le souhaitez toouse authentification de Service d’application avec un point de terminaison hello tables, vous devez configurer l’authentification du Service application Bonjour [portail Azure] première.</span><span class="sxs-lookup"><span data-stu-id="7fc91-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="7fc91-380">Pour plus d’informations sur la configuration de l’authentification dans un Service d’application Azure, passez en revue les hello Guide de Configuration pour le fournisseur d’identité hello vous avez l’intention de toouse :</span><span class="sxs-lookup"><span data-stu-id="7fc91-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="7fc91-381">[Comment tooconfigure authentification Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7fc91-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="7fc91-382">[Comment tooconfigure l’authentification Facebook]</span><span class="sxs-lookup"><span data-stu-id="7fc91-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="7fc91-383">[Comment tooconfigure l’authentification Google]</span><span class="sxs-lookup"><span data-stu-id="7fc91-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="7fc91-384">[Comment tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="7fc91-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="7fc91-385">[Comment tooconfigure Twitter de l’authentification]</span><span class="sxs-lookup"><span data-stu-id="7fc91-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="7fc91-386">Chaque table possède une propriété d’accès qui peut être utilisé toocontrol accès toohello table.</span><span class="sxs-lookup"><span data-stu-id="7fc91-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="7fc91-387">Hello suivant l’exemple affiche un tableau défini de façon statique avec l’authentification requise.</span><span class="sxs-lookup"><span data-stu-id="7fc91-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="7fc91-388">propriété d’accès Hello peut prendre une des trois valeurs</span><span class="sxs-lookup"><span data-stu-id="7fc91-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="7fc91-389">*anonyme* indique que hello client d’autorisation tooread des données sans authentification</span><span class="sxs-lookup"><span data-stu-id="7fc91-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="7fc91-390">*authentifié* indique que hello doit envoyer un jeton d’authentification valide avec la demande de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="7fc91-391">*disabled* indique que cette table est actuellement désactivée</span><span class="sxs-lookup"><span data-stu-id="7fc91-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="7fc91-392">Si la propriété d’accès hello n’est pas définie, l’accès non authentifié est autorisé.</span><span class="sxs-lookup"><span data-stu-id="7fc91-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="7fc91-393"><a name="howto-tables-getidentity"></a>Procédure : utilisation des revendications d’authentification avec vos tables</span><span class="sxs-lookup"><span data-stu-id="7fc91-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="7fc91-394">Vous pouvez configurer différentes revendications qui sont demandées lors de la configuration de l'authentification.</span><span class="sxs-lookup"><span data-stu-id="7fc91-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="7fc91-395">Ces revendications ne sont pas normalement disponibles via hello `context.user` objet.</span><span class="sxs-lookup"><span data-stu-id="7fc91-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="7fc91-396">Toutefois, elles peuvent être récupérées à l’aide de hello `context.user.getIdentity()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="7fc91-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="7fc91-397">Hello `getIdentity()` méthode retourne une promesse résolue tooan objet.</span><span class="sxs-lookup"><span data-stu-id="7fc91-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="7fc91-398">objet de Hello est indexé par la méthode d’authentification (facebook, google, twitter, microsoftaccount ou aad).</span><span class="sxs-lookup"><span data-stu-id="7fc91-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="7fc91-399">Par exemple, si vous configurez l’authentification de Microsoft Account et demande hello messagerie adresses revendication, vous pouvez ajouter enregistrement de toohello adresse hello par courrier électronique avec hello suivant du contrôleur de table :</span><span class="sxs-lookup"><span data-stu-id="7fc91-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="7fc91-400">toosee les revendications sont disponibles, utilisez un Bonjour tooview de navigateur web `/.auth/me` point de terminaison de votre site.</span><span class="sxs-lookup"><span data-stu-id="7fc91-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="7fc91-401"><a name="howto-tables-disabled"></a>Comment : désactiver les opérations de table accès toospecific</span><span class="sxs-lookup"><span data-stu-id="7fc91-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="7fc91-402">Dans tooappearing d’ajout sur la table de hello, propriété d’accès hello peut être utilisé toocontrol des opérations individuelles.</span><span class="sxs-lookup"><span data-stu-id="7fc91-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="7fc91-403">Il existe quatre opérations :</span><span class="sxs-lookup"><span data-stu-id="7fc91-403">There are four operations:</span></span>

* <span data-ttu-id="7fc91-404">*lire* est hello RESTful une opération GET sur la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="7fc91-405">*Insérer* est opération POST RESTful de hello sur la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="7fc91-406">*mettre à jour* est hello correctif RESTful opération sur la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="7fc91-407">*supprimer* est l’opération de suppression RESTful hello sur la table de hello</span><span class="sxs-lookup"><span data-stu-id="7fc91-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="7fc91-408">Par exemple, vous souhaiterez peut-être tooprovide une table non authentifiée en lecture seule :</span><span class="sxs-lookup"><span data-stu-id="7fc91-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="7fc91-409"><a name="howto-tables-query"></a>Comment : régler requête hello qui est utilisé avec les opérations de table</span><span class="sxs-lookup"><span data-stu-id="7fc91-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="7fc91-410">Une exigence courante pour les opérations de table est tooprovide une vue restreinte des données de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="7fc91-411">Par exemple, vous pouvez fournir une table qui est marquée avec hello authentifié ID d’utilisateur, telles que vous pouvez uniquement lire ou mettre à jour vos propres enregistrements.</span><span class="sxs-lookup"><span data-stu-id="7fc91-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="7fc91-412">Hello, suivant la définition de table fournit cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="7fc91-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="7fc91-413">Les opérations qui exécutent normalement une requête ont une propriété de requête que vous pouvez ajuster avec une clause where.</span><span class="sxs-lookup"><span data-stu-id="7fc91-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="7fc91-414">propriété de requête Hello est un [QueryJS] de l’objet qui est utilisé tooconvert un toosomething de requête OData qui hello de données principal peut traiter.</span><span class="sxs-lookup"><span data-stu-id="7fc91-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="7fc91-415">Pour les cas d’égalité simple (par exemple hello précédant un), une carte peut servir.</span><span class="sxs-lookup"><span data-stu-id="7fc91-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="7fc91-416">Vous pouvez également ajouter des clauses SQL spécifiques :</span><span class="sxs-lookup"><span data-stu-id="7fc91-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="7fc91-417"><a name="howto-tables-softdelete"></a>Procédure : configurer une suppression réversible sur une table</span><span class="sxs-lookup"><span data-stu-id="7fc91-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="7fc91-418">La suppression réversible (Soft Delete) ne supprime pas réellement les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="7fc91-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="7fc91-419">À la place il les marque comme étant supprimées dans la base de données hello en définissant tootrue de colonne hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="7fc91-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="7fc91-420">Bonjour Azure Mobile Apps SDK supprime automatiquement supprimé des enregistrements à partir des résultats, sauf si hello Mobile Client SDK utilise IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="7fc91-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="7fc91-421">tooconfigure supprimer d’une table pour soft, définissez hello `softDelete` propriété dans le fichier de définition de table hello :</span><span class="sxs-lookup"><span data-stu-id="7fc91-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="7fc91-422">Vous devez établir un mécanisme pour purger les enregistrements, à partir d’une application cliente, via un WebJob, via une fonction Azure ou via une API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7fc91-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="7fc91-423"><a name="howto-tables-seeding"></a>Procédure : alimenter votre base de données</span><span class="sxs-lookup"><span data-stu-id="7fc91-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="7fc91-424">Lorsque vous créez une nouvelle application, vous pouvez tooseed une table avec des données.</span><span class="sxs-lookup"><span data-stu-id="7fc91-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="7fc91-425">Cela est possible dans un fichier JavaScript de définition de table hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fc91-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="7fc91-426">L’amorçage de données s’effectue uniquement lors de la table de hello est créée par hello Azure Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="7fc91-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="7fc91-427">Si hello existe déjà dans la base de données hello, aucune donnée n’est introduite dans un tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="7fc91-428">Si le schéma dynamique est activé, le schéma est déduit à partir des données de hello d’amorçage.</span><span class="sxs-lookup"><span data-stu-id="7fc91-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="7fc91-429">Nous recommandons d’appeler explicitement hello `tables.initialize()` table de hello toocreate mode de démarrage du service de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7fc91-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="7fc91-430"><a name="Swagger"></a>Procédure : activation de la prise en charge de Swagger</span><span class="sxs-lookup"><span data-stu-id="7fc91-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="7fc91-431">Azure App Service Mobile Apps prend nativement en charge l’interface [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="7fc91-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="7fc91-432">tooenable prise en charge de Swagger, installez tout d’abord hello swagger interface utilisateur en tant que dépendance :</span><span class="sxs-lookup"><span data-stu-id="7fc91-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="7fc91-433">Une fois installé, vous pouvez activer la prise en charge de Swagger dans le constructeur d’applications mobiles Azure hello :</span><span class="sxs-lookup"><span data-stu-id="7fc91-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="7fc91-434">Vous tooenable que vous souhaitez probablement uniquement prise en charge de Swagger dans les éditions de développement.</span><span class="sxs-lookup"><span data-stu-id="7fc91-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="7fc91-435">Pour ce faire, vous pouvez utiliser le paramètre d’application `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="7fc91-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="7fc91-436">Hello point de terminaison swagger se trouve à http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="7fc91-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="7fc91-437">Vous pouvez accéder à hello Swagger de l’interface utilisateur via hello `/swagger/ui` point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7fc91-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="7fc91-438">Si vous choisissez l’authentification de toorequire dans toute votre application, Swagger génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="7fc91-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="7fc91-439">Pour de meilleurs résultats, choisissez demandes tooallow non authentifiée via Bonjour Azure App Service authentification / paramètres d’autorisation, puis contrôler l’authentification à l’aide de hello `table.access` propriété.</span><span class="sxs-lookup"><span data-stu-id="7fc91-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="7fc91-440">Vous pouvez également ajouter hello Swagger option tooyour `azureMobile.js` fichier si vous souhaitez uniquement prise en charge de Swagger lors du développement localement.</span><span class="sxs-lookup"><span data-stu-id="7fc91-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="7fc91-441"><a name="push">Notifications Push</span><span class="sxs-lookup"><span data-stu-id="7fc91-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="7fc91-442">Applications mobiles s’intègre à Azure Notification Hubs tooenable vous toomillions de notifications push toosend ciblé d’appareils sur toutes les plateformes principales.</span><span class="sxs-lookup"><span data-stu-id="7fc91-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="7fc91-443">À l’aide de concentrateurs de Notification, vous pouvez envoyer push notifications tooiOS, appareils Android et Windows.</span><span class="sxs-lookup"><span data-stu-id="7fc91-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="7fc91-444">consultez des concentrateurs de Notification, toolearn plus que vous peuvent faire avec [vue d’ensemble des concentrateurs de Notification](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7fc91-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="7fc91-445"></a><a name="send-push"></a>Procédure : envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="7fc91-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="7fc91-446">Hello suivant de code montre comment toouse hello push objet toosend une diffusion push des appareils iOS notification tooregistered :</span><span class="sxs-lookup"><span data-stu-id="7fc91-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="7fc91-447">En créant un enregistrement de push de modèle à partir du client de hello, vous pouvez à la place envoyer un toodevices de message push modèle sur toutes les plateformes prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7fc91-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="7fc91-448">Hello suivant de code montre comment toosend une notification de modèle :</span><span class="sxs-lookup"><span data-stu-id="7fc91-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="7fc91-449"><a name="push-user"></a>Comment : envoi push notifications tooan authentifié l’utilisateur à l’aide de balises</span><span class="sxs-lookup"><span data-stu-id="7fc91-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="7fc91-450">Lorsqu’un utilisateur authentifié s’inscrit pour les notifications push, une balise d’ID utilisateur est automatiquement ajoutée l’enregistrement de toohello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="7fc91-451">À l’aide de cette balise, vous pouvez envoyer des périphériques de tooall notifications inscrits par un utilisateur spécifique par émission de données.</span><span class="sxs-lookup"><span data-stu-id="7fc91-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="7fc91-452">Hello de code suivant obtient hello SID de l’utilisateur qui effectue la demande de hello et envoie une inscription de périphérique modèle push notification tooevery pour cet utilisateur :</span><span class="sxs-lookup"><span data-stu-id="7fc91-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="7fc91-453">Quand vous vous inscrivez à des notifications Push à partir d’un client authentifié, assurez-vous au préalable que l’authentification est bien terminée.</span><span class="sxs-lookup"><span data-stu-id="7fc91-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="7fc91-454"><a name="CustomAPI"></a> API personnalisées</span><span class="sxs-lookup"><span data-stu-id="7fc91-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="7fc91-455"><a name="howto-customapi-basic"></a>Procédure : définition d'une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="7fc91-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="7fc91-456">En outre toohello d’accès aux données API via le point de terminaison /tables hello, les applications mobiles Azure peut fournir une couverture API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7fc91-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="7fc91-457">API personnalisées sont définies dans une façon toohello table des définitions similaires et peuvent accéder à tous les hello mêmes installations, y compris l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7fc91-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="7fc91-458">Si vous le souhaitez toouse authentification de Service d’application avec une API personnalisée, vous devez configurer l’authentification du Service application Bonjour [portail Azure] première.</span><span class="sxs-lookup"><span data-stu-id="7fc91-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="7fc91-459">Pour plus d’informations sur la configuration de l’authentification dans un Service d’application Azure, passez en revue les hello Guide de Configuration pour le fournisseur d’identité hello vous avez l’intention de toouse :</span><span class="sxs-lookup"><span data-stu-id="7fc91-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="7fc91-460">[Comment tooconfigure authentification Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7fc91-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="7fc91-461">[Comment tooconfigure l’authentification Facebook]</span><span class="sxs-lookup"><span data-stu-id="7fc91-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="7fc91-462">[Comment tooconfigure l’authentification Google]</span><span class="sxs-lookup"><span data-stu-id="7fc91-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="7fc91-463">[Comment tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="7fc91-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="7fc91-464">[Comment tooconfigure Twitter de l’authentification]</span><span class="sxs-lookup"><span data-stu-id="7fc91-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="7fc91-465">Les API personnalisées sont définies à peu près comme hello API Tables hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="7fc91-466">Créez un répertoire **api** .</span><span class="sxs-lookup"><span data-stu-id="7fc91-466">Create an **api** directory</span></span>
2. <span data-ttu-id="7fc91-467">Créer un fichier JavaScript de définition API Bonjour **api** active.</span><span class="sxs-lookup"><span data-stu-id="7fc91-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="7fc91-468">Utilisez Bonjour importation méthode tooimport Bonjour **api** active.</span><span class="sxs-lookup"><span data-stu-id="7fc91-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="7fc91-469">Voici la définition de l’api prototype hello basée sur d’exemple hello basic-app utilisé précédemment.</span><span class="sxs-lookup"><span data-stu-id="7fc91-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="7fc91-470">Prenons un exemple API qui renvoie la date du serveur hello à l’aide de hello *Date.now()* (méthode).</span><span class="sxs-lookup"><span data-stu-id="7fc91-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="7fc91-471">Voici le fichier de api/date.js hello :</span><span class="sxs-lookup"><span data-stu-id="7fc91-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="7fc91-472">Chaque paramètre est un des hello RESTful verbes standard - GET, POST, PATCH ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="7fc91-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="7fc91-473">méthode Hello est une norme [ExpressJS Middleware] fonction qui envoie la sortie de hello requis.</span><span class="sxs-lookup"><span data-stu-id="7fc91-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="7fc91-474"><a name="howto-customapi-auth"></a>Comment : exiger l’authentification pour l’API personnalisée d’accès tooa</span><span class="sxs-lookup"><span data-stu-id="7fc91-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="7fc91-475">Kit de développement Azure Mobile Apps implémente l’authentification dans hello identique pour le point de terminaison hello tables et des API personnalisées.</span><span class="sxs-lookup"><span data-stu-id="7fc91-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="7fc91-476">Pour ajouter l’authentification toohello API est développé dans la section précédente de hello, ajoutez un **accès** propriété :</span><span class="sxs-lookup"><span data-stu-id="7fc91-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="7fc91-477">Vous pouvez également spécifier l’authentification sur des opérations spécifiques :</span><span class="sxs-lookup"><span data-stu-id="7fc91-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="7fc91-478">Hello même jeton qui est utilisé pour le point de terminaison hello tables doit être utilisé pour les API personnalisées nécessitant une authentification.</span><span class="sxs-lookup"><span data-stu-id="7fc91-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="7fc91-479"><a name="howto-customapi-auth"></a>Procédure : gestion des téléchargements de fichiers volumineux</span><span class="sxs-lookup"><span data-stu-id="7fc91-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="7fc91-480">Azure Mobile Apps SDK utilise hello [corps-analyseur intergiciel (middleware)](https://github.com/expressjs/body-parser) tooaccept et décoder le contenu du corps de votre demande.</span><span class="sxs-lookup"><span data-stu-id="7fc91-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="7fc91-481">Vous pouvez préconfigurer les téléchargements de fichiers plus volumineux corps-analyseur tooaccept :</span><span class="sxs-lookup"><span data-stu-id="7fc91-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="7fc91-482">fichier de Hello est codée avant la transmission en base-64.</span><span class="sxs-lookup"><span data-stu-id="7fc91-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="7fc91-483">Cela augmente la taille hello de téléchargement réelle de hello (et donc hello taille, que vous devez prendre en compte).</span><span class="sxs-lookup"><span data-stu-id="7fc91-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="7fc91-484"><a name="howto-customapi-sql"></a>Procédure : exécution d’instructions SQL personnalisées</span><span class="sxs-lookup"><span data-stu-id="7fc91-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="7fc91-485">Hello Azure Mobile Apps SDK permet l’accès toohello ensemble du contexte via l’objet de demande hello, ce qui vous tooexecute paramétrables fournisseur de données SQL instructions toohello facilement :</span><span class="sxs-lookup"><span data-stu-id="7fc91-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="7fc91-486"><a name="Debugging"></a>Débogage, Tables facile et API simples</span><span class="sxs-lookup"><span data-stu-id="7fc91-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="7fc91-487"><a name="howto-diagnostic-logs"></a>Procédure : débogage, diagnostic et résolution des problèmes sur Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="7fc91-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="7fc91-488">Hello du Service d’applications Azure fournit plusieurs de débogage et de résolution des problèmes techniques pour les applications de Node.js.</span><span class="sxs-lookup"><span data-stu-id="7fc91-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="7fc91-489">Consultez toohello suivant tooget articles démarré dans Résolution des problèmes de votre serveur principal Node.js Mobile :</span><span class="sxs-lookup"><span data-stu-id="7fc91-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="7fc91-490">[Surveiller les applications web dans Microsoft Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="7fc91-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="7fc91-491">[Activer la journalisation des diagnostics pour les applications web dans Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="7fc91-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="7fc91-492">[Dépanner un service Azure App dans Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="7fc91-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="7fc91-493">Les applications Node.js ont accès tooa une large gamme d’outils de diagnostic de journal.</span><span class="sxs-lookup"><span data-stu-id="7fc91-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="7fc91-494">En interne, les hello Azure Mobile Apps Node.js SDK utilise [Winston] pour la journalisation des Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="7fc91-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="7fc91-495">La journalisation est activée automatiquement en activant le mode de débogage ou en définissant un hello **MS_DebugMode** tootrue de paramètre d’application Bonjour [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="7fc91-496">Journaux générés s’affichent dans hello des journaux de Diagnostic sur hello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="7fc91-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="7fc91-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Comment : utiliser des Tables facile Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fc91-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="7fc91-498">Tables facile dans le portail de hello vous permettent de créer et manipuler directement de tables dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="7fc91-499">Vous pouvez modifier les opérations de table à l’aide de hello éditeur de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="7fc91-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="7fc91-500">Lorsque vous cliquez sur **Easy Tables** dans vos paramètres de site principal, vous pouvez ajouter, modifier ou supprimer une table.</span><span class="sxs-lookup"><span data-stu-id="7fc91-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="7fc91-501">Vous pouvez également voir les données de table de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-501">You can also see data in hello table.</span></span>

![Utilisation de l’outil Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="7fc91-503">Hello commandes suivantes sont disponibles sur la barre de commandes hello pour une table :</span><span class="sxs-lookup"><span data-stu-id="7fc91-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="7fc91-504">**Modifier les autorisations** - modifier l’autorisation hello pour la lecture, insérer, mettre à jour et opérations delete sur la table de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="7fc91-505">Les options sont tooallow l’accès anonyme, une authentification toorequire ou toodisable tous les accès toohello opération.</span><span class="sxs-lookup"><span data-stu-id="7fc91-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="7fc91-506">**Modifier le script** -fichier de script hello pour la table de hello est ouvert dans hello éditeur de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="7fc91-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="7fc91-507">**Gérer le schéma** - ajouter ou supprimer des colonnes ou modifier des index de table hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="7fc91-508">**Effacer le tableau** -tronque une table existante Supprimer toutes les lignes de données mais en laissant le schéma de hello reste la même.</span><span class="sxs-lookup"><span data-stu-id="7fc91-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="7fc91-509">**Supprimer des lignes** : supprimer des lignes de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7fc91-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="7fc91-510">**Affichage des journaux de diffusion en continu** -vous connecte toohello service de journal de votre site de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="7fc91-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="7fc91-511"><a name="work-easy-apis"></a>Comment : travailler avec les API facile Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="7fc91-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="7fc91-512">Une API simple dans le portail de hello vous permettre de créer et manipuler le droit d’API personnalisé dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="7fc91-513">Vous pouvez modifier les scripts d’API à l’aide de hello éditeur de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="7fc91-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="7fc91-514">Lorsque vous cliquez sur **Easy APIs** dans vos paramètres de site principal, vous pouvez ajouter modifier ou supprimer un point de terminaison API personnalisé.</span><span class="sxs-lookup"><span data-stu-id="7fc91-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Utilisation de l’outil Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="7fc91-516">Dans le portail hello, vous pouvez modifier les autorisations d’accès hello pour une action HTTP donnés, modifier le fichier de script d’API hello dans l’éditeur de Service application ou afficher les journaux de diffusion en continu hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="7fc91-517"><a name="online-editor"></a>Comment : modifier le code dans hello éditeur de Service d’applications</span><span class="sxs-lookup"><span data-stu-id="7fc91-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="7fc91-518">Hello portail Azure vous permet de modifier vos fichiers de script principal Node.js Bonjour éditeur de Service d’applications sans avoir à télécharger l’ordinateur local de hello projet tooyour.</span><span class="sxs-lookup"><span data-stu-id="7fc91-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="7fc91-519">tooedit des fichiers de script dans l’éditeur en ligne hello :</span><span class="sxs-lookup"><span data-stu-id="7fc91-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="7fc91-520">Dans le panneau de votre serveur principal d’application mobile, cliquez sur **Tous les paramètres** > **Tables faciles** ou **API faciles**, cliquez sur une table ou une API, puis cliquez sur **Modifier le script**.</span><span class="sxs-lookup"><span data-stu-id="7fc91-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="7fc91-521">fichier de script Hello est ouvert dans hello éditeur de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="7fc91-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Éditeur App Service](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="7fc91-523">Vérifiez votre fichier de code toohello modifications dans l’éditeur en ligne hello.</span><span class="sxs-lookup"><span data-stu-id="7fc91-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="7fc91-524">Les modifications sont enregistrées automatiquement au fil de la saisie.</span><span class="sxs-lookup"><span data-stu-id="7fc91-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android Client QuickStart]: app-service-mobile-android-get-started.md
[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md
[iOS Client QuickStart]: app-service-mobile-ios-get-started.md
[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md
[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[synchronisation des données hors connexion]: app-service-mobile-offline-data-sync.md
[Comment tooconfigure authentification Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Comment tooconfigure l’authentification Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Comment tooconfigure l’authentification Google]: app-service-mobile-how-to-configure-google-authentication.md
[Comment tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Comment tooconfigure Twitter de l’authentification]: app-service-mobile-how-to-configure-twitter-authentication.md
[Guide de déploiement d’Azure App Service]: ../app-service-web/web-sites-deploy.md
[Surveiller les applications web dans Microsoft Azure App Service]: ../app-service-web/web-sites-monitor.md
[Activer la journalisation des diagnostics pour les applications web dans Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Dépanner un service Azure App dans Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[spécifier hello Version du nœud]: ../nodejs-specify-node-version-azure-apps.md
[utiliser des modules de nœud]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portail Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[promesse]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[exemple basicapp sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[exemple todo sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[répertoire d’exemples sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 pour Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
