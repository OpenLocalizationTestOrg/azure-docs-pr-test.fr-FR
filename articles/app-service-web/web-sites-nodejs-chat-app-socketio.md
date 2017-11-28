---
title: "Créer une application de conversation instantanée Node.js avec Socket.IO dans Azure App Service"
description: "Didacticiel démontrant l’utilisation de socket.io dans une application web node.js hébergée sur Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="139e8-103">Créer une application de conversation instantanée Node.js avec Socket.IO dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="139e8-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="139e8-104">Socket.IO offre une communication en temps réel entre votre serveur node.js et vos clients à l'aide de WebSockets.</span><span class="sxs-lookup"><span data-stu-id="139e8-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="139e8-105">Il prend également en charge l’utilisation d’autres transports (tels que l’interrogation longue) qui fonctionnent avec des navigateurs plus anciens.</span><span class="sxs-lookup"><span data-stu-id="139e8-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="139e8-106">Ce didacticiel décrit la procédure d’hébergement d’une application de conversation instantanée Socket.IO sous la forme d’une application web Azure et explique comment la mettre à l’échelle à l’aide d’ [Cache Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="139e8-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="139e8-107">Pour plus d’informations sur Socket.IO, consultez le site <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="139e8-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="139e8-108">Les procédures de cette tâche s’appliquent à [App Service Web Apps]. Pour Services cloud, consultez la page [Création d’une application de conversation instantanée Node.js avec Socket.IO sur un service cloud Azure].</span><span class="sxs-lookup"><span data-stu-id="139e8-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="139e8-109">Télécharger l’exemple de conversation instantanée</span><span class="sxs-lookup"><span data-stu-id="139e8-109">Download the chat example</span></span>
<span data-ttu-id="139e8-110">Pour ce projet, nous utiliserons un exemple de conversation instantanée obtenu depuis le [référentiel GitHub Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="139e8-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="139e8-111">Procédez comme suit pour télécharger l'exemple et l'ajouter au projet créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="139e8-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="139e8-112">Téléchargez une [version archivée ZIP ou GZ] du projet Socket.IO (la version 1.3.5 a été utilisée pour ce document).</span><span class="sxs-lookup"><span data-stu-id="139e8-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="139e8-113">Extrayez l’archive et copiez le répertoire **examples\\chat** dans un nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="139e8-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="139e8-114">Par exemple, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="139e8-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="139e8-115">Modifier le fichier app.js et installer les modules</span><span class="sxs-lookup"><span data-stu-id="139e8-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="139e8-116">Renommez le fichier **index.js** en **app.js**.</span><span class="sxs-lookup"><span data-stu-id="139e8-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="139e8-117">Cela permet à Azure de détecter qu'il s'agit d'une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="139e8-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="139e8-118">Ouvrez le fichier **app.js** dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="139e8-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="139e8-119">Modifiez la ligne contenant `var io = require('../..')(server);` comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="139e8-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="139e8-120">Ouvrez le fichier**package.json** et ajoutez une référence à socket.io sous `dependencies`, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="139e8-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="139e8-121">Depuis la ligne de commande, accédez au répertoire **\\node\\chat** et utilisez la commande npm pour installer les modules requis par cette application :</span><span class="sxs-lookup"><span data-stu-id="139e8-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="139e8-122">Cette opération installe les modules dans un sous-dossier nommé **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="139e8-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="139e8-123">Créer une application web Azure</span><span class="sxs-lookup"><span data-stu-id="139e8-123">Create an Azure Web App</span></span>
<span data-ttu-id="139e8-124">Suivez la procédure ci-après pour créer une application web Azure, activer la publication Git, puis activer la prise en charge de WebSocket pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="139e8-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="139e8-125">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="139e8-126">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="139e8-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="139e8-127">Pour plus d’informations, consultez la page <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Version d’essai gratuite d’Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="139e8-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="139e8-128">Installez l’interface de ligne de commande Azure (CLI Azure) et connectez-la à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="139e8-129">Consultez [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="139e8-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="139e8-130">Si vous configurez un référentiel pour la première fois dans Azure, vous devez créer des informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="139e8-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="139e8-131">À partir de l’interface de ligne de commande Azure, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="139e8-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="139e8-132">Accédez au répertoire **\\node\chat**, puis utilisez la commande ci-après pour créer une application web Azure et un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="139e8-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="139e8-133">Cette commande crée également un Git distant nommé ’azure’.</span><span class="sxs-lookup"><span data-stu-id="139e8-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="139e8-134">Vous devez remplacer ’mysitename’ par le nom unique de votre application web.</span><span class="sxs-lookup"><span data-stu-id="139e8-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="139e8-135">Validez les fichiers existants dans le référentiel local en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="139e8-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="139e8-136">Utilisez la commande ci-après pour transmettre les fichiers au référentiel Azure Web Apps :</span><span class="sxs-lookup"><span data-stu-id="139e8-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="139e8-137">Lorsque vous y êtes invité, entrez vos informations d'identification de l'étape 2.</span><span class="sxs-lookup"><span data-stu-id="139e8-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="139e8-138">Vous recevez des messages d'état au fur et à mesure que les modules sont importés sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="139e8-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="139e8-139">Une fois ce processus terminé, l’application est hébergée sur votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="139e8-140">Lors de l’installation du module, il est possible que des erreurs du type ’Le projet importé... est introuvable’ s’affichent.</span><span class="sxs-lookup"><span data-stu-id="139e8-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="139e8-141">Vous pouvez les ignorer sans problème.</span><span class="sxs-lookup"><span data-stu-id="139e8-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="139e8-142">Socket.IO utilise WebSockets, qui n'est pas activé par défaut sur Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="139e8-143">Pour activer WebSockets, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="139e8-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="139e8-144">Si vous y êtes invité, entrez le nom de l’application web.</span><span class="sxs-lookup"><span data-stu-id="139e8-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="139e8-145">La commande ’azure site set -w’ ne fonctionne qu’avec la version 0.7.4 ou une version ultérieure de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="139e8-146">Vous pouvez également activer la prise en charge de WebSocket à l’aide du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="139e8-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="139e8-147">Pour activer WebSockets à l’aide du portail Azure, cliquez sur l’application web dans le panneau Web Apps, puis sur **Tous les paramètres** > **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="139e8-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="139e8-148">Sous **WebSockets**, cliquez sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="139e8-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="139e8-149">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="139e8-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="139e8-150">Pour visualiser l’application web sur Azure, utilisez la commande ci-après afin de lancer votre navigateur web et d’accéder à l’application web hébergée :</span><span class="sxs-lookup"><span data-stu-id="139e8-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="139e8-151">Votre application s’exécute à présent sur Azure et peut relayer des messages de conversation instantanée entre différents clients en utilisant Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="139e8-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="139e8-152">Montée en charge</span><span class="sxs-lookup"><span data-stu-id="139e8-152">Scale out</span></span>
<span data-ttu-id="139e8-153">Vous pouvez faire monter en charge les applications Socket.IO en utilisant un **adaptateur** pour distribuer les messages et les événements entre plusieurs instances d’application.</span><span class="sxs-lookup"><span data-stu-id="139e8-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="139e8-154">Plusieurs adaptateurs sont disponibles, mais [socket.io-redis] est très facile à utiliser avec la fonctionnalité de cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="139e8-155">Une autre condition requise par la montée en charge d’une solution Socket.IO est la prise en charge des sessions rémanentes.</span><span class="sxs-lookup"><span data-stu-id="139e8-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="139e8-156">Celles-ci sont activées par défaut pour Azure Web Apps par l’intermédiaire d’Azure Request Routing.</span><span class="sxs-lookup"><span data-stu-id="139e8-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="139e8-157">Pour plus d'informations, consultez [Affinité d'instance dans Sites Web Azure].</span><span class="sxs-lookup"><span data-stu-id="139e8-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="139e8-158">Création d'un cache Redis</span><span class="sxs-lookup"><span data-stu-id="139e8-158">Create a Redis cache</span></span>
<span data-ttu-id="139e8-159">Pour créer un cache, effectuez les étapes décrites dans [Création d'un cache dans le cache Azure Redis] .</span><span class="sxs-lookup"><span data-stu-id="139e8-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="139e8-160">Enregistrez le **Nom d’hôte** et la **Clé primaire** de votre cache, car ces paramètres seront nécessaires lors des étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="139e8-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="139e8-161">Ajout des modules redis et socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="139e8-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="139e8-162">Sur la ligne de commande, accédez au répertoire **\\node\\chat** et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="139e8-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="139e8-163">Les versions spécifiées dans cette commande sont celles utilisées lors des tests de cet article.</span><span class="sxs-lookup"><span data-stu-id="139e8-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="139e8-164">Modifiez le fichier **app.js** en lui ajoutant les lignes suivantes juste après `var io = require('socket.io')(server);`.</span><span class="sxs-lookup"><span data-stu-id="139e8-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="139e8-165">Remplacez **redishostname** et **rediskey** par le nom d’hôte et la clé de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="139e8-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="139e8-166">Cette commande permet de créer un client de publication et d'abonnement pour le cache Redis créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="139e8-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="139e8-167">Les clients sont ensuite utilisés avec l'adaptateur pour configurer Socket.IO de sorte à utiliser le cache Redis pour le transfert des messages et des événements entre les instances de votre application.</span><span class="sxs-lookup"><span data-stu-id="139e8-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="139e8-168">Bien que l’adaptateur **socket.io-redis** puisse communiquer directement avec Redis, la version actuelle ne prend pas en charge l’authentification requise par le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="139e8-169">La connexion initiale est donc créée à l’aide du module **redis**, puis le client est transféré à l’adaptateur **socket.io-redis**.</span><span class="sxs-lookup"><span data-stu-id="139e8-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="139e8-170">Bien que Cache Redis Azure prenne en charge les connexions sécurisées sur le port 6380, les modules utilisés dans cet exemple ne gèrent pas les connexions sécurisées depuis le 14/07/2014.</span><span class="sxs-lookup"><span data-stu-id="139e8-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="139e8-171">Le code ci-dessus utilise le port non sécurisé par défaut 6379.</span><span class="sxs-lookup"><span data-stu-id="139e8-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="139e8-172">Enregistrez le fichier **app.js** modifié.</span><span class="sxs-lookup"><span data-stu-id="139e8-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="139e8-173">Validation des modifications et redéploiement</span><span class="sxs-lookup"><span data-stu-id="139e8-173">Commit changes and redeploy</span></span>
<span data-ttu-id="139e8-174">Depuis la ligne de commande dans le répertoire **\\node\\chat**, utilisez les commandes suivantes pour valider les modifications et redéployer l’application.</span><span class="sxs-lookup"><span data-stu-id="139e8-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="139e8-175">Une fois les modifications transmises au serveur, vous pouvez distribuer votre site sur plusieurs instances en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="139e8-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="139e8-176">Où **#** correspond au nombre d’instances à créer.</span><span class="sxs-lookup"><span data-stu-id="139e8-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="139e8-177">Vous pouvez vous connecter à votre application web à partir de plusieurs navigateurs ou ordinateurs pour vérifier que les messages sont correctement envoyés à tous les clients.</span><span class="sxs-lookup"><span data-stu-id="139e8-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="139e8-178">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="139e8-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="139e8-179">Limites de connexions</span><span class="sxs-lookup"><span data-stu-id="139e8-179">Connection limits</span></span>
<span data-ttu-id="139e8-180">La fonctionnalité Azure Web Apps est disponible dans plusieurs références (SKU) qui déterminent les ressources disponibles pour votre site.</span><span class="sxs-lookup"><span data-stu-id="139e8-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="139e8-181">Cela inclut le nombre de connexions WebSocket autorisées.</span><span class="sxs-lookup"><span data-stu-id="139e8-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="139e8-182">Pour plus d’informations, consultez la [page de tarification de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="139e8-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="139e8-183">Les messages ne sont pas envoyés avec WebSockets</span><span class="sxs-lookup"><span data-stu-id="139e8-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="139e8-184">Si les navigateurs clients utilisent l'interrogation longue plutôt que WebSockets, essayez d'appliquer les solutions suivantes.</span><span class="sxs-lookup"><span data-stu-id="139e8-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="139e8-185">**Tentative de limitation du transport à WebSockets**</span><span class="sxs-lookup"><span data-stu-id="139e8-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="139e8-186">Pour que Socket.IO utilise WebSockets comme transport de messagerie, le serveur et le client doivent tous deux prendre en charge WebSockets.</span><span class="sxs-lookup"><span data-stu-id="139e8-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="139e8-187">Si ce n'est pas le cas, Socket.IO négocie un autre transport, tel que l'interrogation longue.</span><span class="sxs-lookup"><span data-stu-id="139e8-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="139e8-188">La liste par défaut des transports utilisés par Socket.IO est ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="139e8-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="139e8-189">Vous pouvez le forcer à n’utiliser que WebSockets en ajoutant le code suivant au fichier **app.js** après la ligne contenant `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="139e8-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="139e8-190">Notez que les navigateurs plus anciens qui ne prennent pas en charge WebSockets ne pourront pas se connecter au site pendant que le code ci-dessus est actif, car il limite les communications à WebSockets.</span><span class="sxs-lookup"><span data-stu-id="139e8-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="139e8-191">**Utilisation du protocole SSL**</span><span class="sxs-lookup"><span data-stu-id="139e8-191">**Use SSL**</span></span>
  
    <span data-ttu-id="139e8-192">WebSockets repose sur des en-têtes HTTP moins utilisés, tels que **Upgrade** .</span><span class="sxs-lookup"><span data-stu-id="139e8-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="139e8-193">Certains périphériques réseau intermédiaires, tels que les proxys web, peuvent supprimer ces en-têtes.</span><span class="sxs-lookup"><span data-stu-id="139e8-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="139e8-194">Pour éviter ce problème, vous pouvez établir la connexion WebSocket sur le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="139e8-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="139e8-195">Le moyen le plus simple consiste à configurer Socket.IO avec `match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="139e8-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="139e8-196">Socket.IO se charge alors de sécuriser les communications WebSockets de la même manière que la requête HTTP/HTTPS d'origine pour la page web.</span><span class="sxs-lookup"><span data-stu-id="139e8-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="139e8-197">Si un navigateur utilise une URL HTTPS pour accéder à votre site web, les communications WebSocket ultérieures par l'intermédiaire de Socket.IO seront sécurisées sur SSL.</span><span class="sxs-lookup"><span data-stu-id="139e8-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="139e8-198">Pour modifier cet exemple et activer cette configuration, ajoutez le code suivant au fichier **app.js** après la ligne contenant `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="139e8-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="139e8-199">**Vérification des paramètres de web.config**</span><span class="sxs-lookup"><span data-stu-id="139e8-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="139e8-200">Les applications web Azure qui hébergent des applications Node.js utilisent le fichier **web.config** pour acheminer les demandes entrantes vers l’application Node.js.</span><span class="sxs-lookup"><span data-stu-id="139e8-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="139e8-201">Pour que WebSockets fonctionne correctement avec les applications Node.js, le fichier **web.config** doit contenir l'entrée suivante.</span><span class="sxs-lookup"><span data-stu-id="139e8-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="139e8-202">Cela désactive le module WebSockets IIS, qui comprend sa propre implémentation de WebSockets et entre en conflit avec les modules WebSocket spécifiques à Node.js tels que Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="139e8-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="139e8-203">Si cette ligne est absente ou a la valeur `true`, ceci peut expliquer que le transport WebSocket ne fonctionne pas sur votre application.</span><span class="sxs-lookup"><span data-stu-id="139e8-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="139e8-204">Normalement, les applications Node.js n’incluent pas de fichier **web.config**. Par conséquent, l’offre Sites Web Azure en génère un automatiquement pour les applications Node.js lors de leur déploiement.</span><span class="sxs-lookup"><span data-stu-id="139e8-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="139e8-205">Ce fichier étant généré automatiquement sur le serveur, vous devez utiliser l'URL FTP ou FTPS de votre site web pour l'afficher.</span><span class="sxs-lookup"><span data-stu-id="139e8-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="139e8-206">Vous pouvez obtenir les URL FTP et FTPS de votre site dans le portail Azure Classic en sélectionnant votre application web, puis le lien **Tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="139e8-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="139e8-207">Les URL sont affichées dans la section **aperçu rapide**.</span><span class="sxs-lookup"><span data-stu-id="139e8-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="139e8-208">Le fichier **web.config** n’est généré par Sites Web Azure que si votre application n’en fournit pas.</span><span class="sxs-lookup"><span data-stu-id="139e8-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="139e8-209">Si vous fournissez un fichier **web.config** à la racine de votre projet d’application, il sera utilisé par Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="139e8-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="139e8-210">Si l’entrée est absente ou a la valeur `true`, vous devez créer un fichier **web.config** à la racine de votre application Node.js et spécifier la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="139e8-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="139e8-211">Vous trouverez ci-dessous un fichier **web.config** par défaut pour une application qui utilise **app.js** comme point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="139e8-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="139e8-212">Si votre application utilise un autre point d’entrée que **app.js**, vous devez remplacer toutes les occurrences d’**app.js** par le point d’entrée approprié.</span><span class="sxs-lookup"><span data-stu-id="139e8-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="139e8-213">Par exemple, vous devez remplacer **app.js** par **server.js**.</span><span class="sxs-lookup"><span data-stu-id="139e8-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="139e8-214">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service], où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="139e8-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="139e8-215">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="139e8-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="139e8-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="139e8-216">Next steps</span></span>
<span data-ttu-id="139e8-217">Ce didacticiel vous a expliqué comment créer une application de conversation instantanée hébergée dans une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="139e8-218">Vous pouvez également héberger cette application dans le service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="139e8-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="139e8-219">Pour savoir comment procéder, consultez la page [Création d’une application de conversation instantanée Node.js avec Socket.IO sur un service cloud Azure].</span><span class="sxs-lookup"><span data-stu-id="139e8-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="139e8-220">Pour plus d'informations, consultez aussi le [Centre pour développeurs Node.js].</span><span class="sxs-lookup"><span data-stu-id="139e8-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="139e8-221">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="139e8-221">What's changed</span></span>
* <span data-ttu-id="139e8-222">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants].</span><span class="sxs-lookup"><span data-stu-id="139e8-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="139e8-223">[Cache Redis Azure]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="139e8-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="139e8-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="139e8-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="139e8-225">[page de tarification de Web Apps]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="139e8-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="139e8-226">[Création d’une application de conversation instantanée Node.js avec Socket.IO sur un service cloud Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="139e8-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="139e8-227">[Azure App Service et les services Azure existants]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="139e8-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="139e8-228">[Centre pour développeurs Node.js]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="139e8-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="139e8-229">[Essayer App Service]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="139e8-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="139e8-230">[Affinité d'instance dans Sites Web Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="139e8-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="139e8-231">[Création d'un cache dans le cache Azure Redis]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="139e8-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="139e8-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="139e8-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="139e8-233">[référentiel GitHub Socket.IO]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="139e8-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="139e8-234">[version archivée ZIP ou GZ]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="139e8-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
