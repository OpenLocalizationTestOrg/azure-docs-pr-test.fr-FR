---
title: aaaCreate une application de conversation Node.js avec Socket.IO dans Azure App Service
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
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="02017-103">Créer une application de conversation instantanée Node.js avec Socket.IO dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="02017-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="02017-104">Socket.IO offre une communication en temps réel entre votre serveur node.js et vos clients à l'aide de WebSockets.</span><span class="sxs-lookup"><span data-stu-id="02017-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="02017-105">Il prend également en charge les transports de secours tooother (par exemple, d’interrogation longue) qui fonctionnent avec les navigateurs plus anciens.</span><span class="sxs-lookup"><span data-stu-id="02017-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="02017-106">Ce didacticiel vous guide hébergeant une application de conversation Socket.IO basé sous forme d’application web Azure et vous montrent comment tooscale hello à l’aide de l’application [Cache Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="02017-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="02017-107">Pour plus d’informations sur Socket.IO, consultez le site <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="02017-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="02017-108">les procédures dans cette tâche Hello appliquent trop[App Service Web Apps]; pour les Services de cloud computing, consultez [générer une Application de Chat Node.js avec Socket.IO sur un Service Cloud Azure].</span><span class="sxs-lookup"><span data-stu-id="02017-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="02017-109">Télécharger l’exemple de conversation hello</span><span class="sxs-lookup"><span data-stu-id="02017-109">Download hello chat example</span></span>
<span data-ttu-id="02017-110">Pour ce projet, nous allons utiliser exemple hello conversation hello [référentiel GitHub de Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="02017-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="02017-111">Effectuer hello étapes toodownload hello exemple suivant et l’ajouter projet toohello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="02017-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="02017-112">Télécharger un [ZIP ou GZ archivé version] du projet de Socket.IO hello (version 1.3.5 a été utilisée pour ce document)</span><span class="sxs-lookup"><span data-stu-id="02017-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="02017-113">Extraire hello de copie et d’archivage hello **exemples\\chat** nouvel emplacement de répertoire tooa.</span><span class="sxs-lookup"><span data-stu-id="02017-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="02017-114">Par exemple, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="02017-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="02017-115">Modifier le fichier app.js et installer les modules</span><span class="sxs-lookup"><span data-stu-id="02017-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="02017-116">Renommer hello **index.js** trop de fichiers**app.js**.</span><span class="sxs-lookup"><span data-stu-id="02017-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="02017-117">Cela permet à Azure toodetect qu’il s’agit d’une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="02017-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="02017-118">Ouvrez hello **app.js** fichier dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="02017-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="02017-119">Qui contient la ligne hello modification `var io = require('../..')(server);` comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="02017-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="02017-120">Ouvrez hello **package.json** et ajoutez un toosocket.io référence sous `dependencies`, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="02017-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="02017-121">Hello de ligne de commande, de modifier toohello  **\\nœud\\chat** active et l’utilisation tooinstall hello des modules npm requis par cette application :</span><span class="sxs-lookup"><span data-stu-id="02017-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="02017-122">Les modules hello va être installé dans un sous-dossier nommé **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="02017-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="02017-123">Créer une application web Azure</span><span class="sxs-lookup"><span data-stu-id="02017-123">Create an Azure Web App</span></span>
<span data-ttu-id="02017-124">Suivez ces étapes de toocreate une application web Azure, activer la publication Git et activer la prise en charge de WebSocket pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="02017-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="02017-125">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="02017-126">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="02017-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="02017-127">Pour plus d'informations, consultez la page <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Version d'évaluation gratuite d'Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="02017-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="02017-128">Installer hello Azure Interface de ligne (Azure) et se connecter tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="02017-129">Consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="02017-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="02017-130">S’il s’agit de votre premier paramètre de temps un référentiel dans Azure, vous avez besoin des informations d’identification de connexion toocreate.</span><span class="sxs-lookup"><span data-stu-id="02017-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="02017-131">À partir de hello CLI d’Azure, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02017-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="02017-132">Modifier toohello  **\\node\chat** active et suit de hello utilisez commande toocreate une nouvelle application web Azure et un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="02017-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="02017-133">Cette commande crée également un Git distant nommé ’azure’.</span><span class="sxs-lookup"><span data-stu-id="02017-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="02017-134">Vous devez remplacer ’mysitename’ par le nom unique de votre application web.</span><span class="sxs-lookup"><span data-stu-id="02017-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="02017-135">Valider le référentiel local hello existant fichiers toohello à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="02017-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="02017-136">Push référentiel des applications Web Azure hello fichiers toohello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02017-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="02017-137">Lorsque vous y êtes invité, entrez vos informations d'identification de l'étape 2.</span><span class="sxs-lookup"><span data-stu-id="02017-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="02017-138">Vous recevez des messages d’état comme les modules sont importés sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="02017-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="02017-139">Une fois ce processus terminé, application hello sera hébergée sur votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="02017-140">Pendant l’installation du module, vous remarquerez peut-être des erreurs qui « hello projet importé... n’a été trouvé ».</span><span class="sxs-lookup"><span data-stu-id="02017-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="02017-141">Vous pouvez les ignorer sans problème.</span><span class="sxs-lookup"><span data-stu-id="02017-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="02017-142">Socket.IO utilise WebSockets, qui n'est pas activé par défaut sur Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="02017-143">tooenable WebSocket, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02017-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="02017-144">Si vous y êtes invité, entrez le nom hello de hello web app.</span><span class="sxs-lookup"><span data-stu-id="02017-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="02017-145">Bonjour va de commande 'site azure set -w' fonctionnent uniquement avec la version 0.7.4 ou une version ultérieure de hello Interface de ligne de commande de Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="02017-146">Vous pouvez également activer la prise en charge de WebSocket à l’aide de hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02017-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="02017-147">à l’aide du protocole WebSocket tooenable hello portail Azure, cliquez sur l’application web à partir du panneau des applications Web hello hello **tous les paramètres** > **paramètres de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="02017-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="02017-148">Sous **WebSockets**, cliquez sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="02017-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="02017-149">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="02017-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="02017-150">tooview hello web application Azure, suivant le hello utilisez commande toolaunch votre navigateur web et accédez toohello hébergé l’application web :</span><span class="sxs-lookup"><span data-stu-id="02017-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="02017-151">Votre application s’exécute à présent sur Azure et peut relayer des messages de conversation instantanée entre différents clients en utilisant Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="02017-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="02017-152">Montée en charge</span><span class="sxs-lookup"><span data-stu-id="02017-152">Scale out</span></span>
<span data-ttu-id="02017-153">Les applications Socket.IO peuvent être monté en charge à l’aide un **carte** toodistribute messages et les événements entre plusieurs instances d’application.</span><span class="sxs-lookup"><span data-stu-id="02017-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="02017-154">Lorsqu’il existe plusieurs adaptateurs disponibles, hello [socket.io-redis] adaptateur peut être facilement utilisé avec la fonctionnalité de Cache Redis Azure hello.</span><span class="sxs-lookup"><span data-stu-id="02017-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="02017-155">Une autre condition requise par la montée en charge d’une solution Socket.IO est la prise en charge des sessions rémanentes.</span><span class="sxs-lookup"><span data-stu-id="02017-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="02017-156">Celles-ci sont activées par défaut pour Azure Web Apps par l’intermédiaire d’Azure Request Routing.</span><span class="sxs-lookup"><span data-stu-id="02017-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="02017-157">Pour plus d'informations, consultez [Affinité d'instance dans Sites Web Azure].</span><span class="sxs-lookup"><span data-stu-id="02017-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="02017-158">Création d'un cache Redis</span><span class="sxs-lookup"><span data-stu-id="02017-158">Create a Redis cache</span></span>
<span data-ttu-id="02017-159">Effectuez les étapes de hello dans [créer un cache dans le Cache Redis Azure] toocreate un nouveau cache.</span><span class="sxs-lookup"><span data-stu-id="02017-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="02017-160">Enregistrer hello **nom d’hôte** et **clé primaire** pour votre cache, car elles seront nécessaires dans hello étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="02017-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="02017-161">Ajouter les redis hello et les modules de socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="02017-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="02017-162">À partir d’une ligne de commande, modifiez toohello  **\\nœud\\chat** active et l’utilisation hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="02017-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="02017-163">les versions de Hello spécifiées dans cette commande sont des versions de hello utilisées lors du test de cet article.</span><span class="sxs-lookup"><span data-stu-id="02017-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="02017-164">Modifier hello **app.js** suivant de fichier tooadd hello lignes immédiatement après`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="02017-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="02017-165">Remplacez **redishostname** et **rediskey** avec le nom d’hôte hello et clé de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="02017-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="02017-166">Cela créera une publication et abonnement client toohello cache Redis créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="02017-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="02017-167">les clients de Hello sont ensuite utilisés avec hello adaptateur tooconfigure cache Redis de Socket.IO toouse hello pour le transfert des messages et les événements entre instances de votre application</span><span class="sxs-lookup"><span data-stu-id="02017-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="02017-168">Lors de hello **socket.io-redis** adaptateur peut communiquer directement tooRedis, la version actuelle de hello ne prend pas en charge l’authentification hello requise par le cache Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="02017-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="02017-169">Pour la connexion initiale hello est créée à l’aide de hello **redis** module, puis client de hello est passé toohello **socket.io-redis** carte.</span><span class="sxs-lookup"><span data-stu-id="02017-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="02017-170">Cache Redis Azure prend en charge les connexions sécurisées à l’aide du port 6380, modules hello utilisés dans cet exemple ne prennent pas en charge les connexions sécurisées à compter du 14/7/2014.</span><span class="sxs-lookup"><span data-stu-id="02017-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="02017-171">Hello au-dessus de code utilise par défaut hello, un port non sécurisé de 6379.</span><span class="sxs-lookup"><span data-stu-id="02017-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="02017-172">Hello enregistrer modifié **app.js**</span><span class="sxs-lookup"><span data-stu-id="02017-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="02017-173">Validation des modifications et redéploiement</span><span class="sxs-lookup"><span data-stu-id="02017-173">Commit changes and redeploy</span></span>
<span data-ttu-id="02017-174">À partir de hello de ligne de commande Bonjour  **\\nœud\\chat** active, utilisez hello commandes toocommit modifications suivantes et redéployer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="02017-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="02017-175">Une fois les modifications hello ont été déplacées toohello serveur, vous pouvez faire évoluer votre site sur plusieurs instances à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="02017-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="02017-176">Où  **#**  est le nombre de hello d’instances toocreate.</span><span class="sxs-lookup"><span data-stu-id="02017-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="02017-177">Vous pouvez vous connecter à l’application web tooyour à partir de plusieurs tooverify de navigateurs ou les ordinateurs qui sont correctement envoyés tooall clients.</span><span class="sxs-lookup"><span data-stu-id="02017-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="02017-178">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="02017-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="02017-179">Limites de connexions</span><span class="sxs-lookup"><span data-stu-id="02017-179">Connection limits</span></span>
<span data-ttu-id="02017-180">Les applications Web Azure est disponible dans plusieurs SKU, qui déterminent le site de hello ressources tooyour disponibles.</span><span class="sxs-lookup"><span data-stu-id="02017-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="02017-181">Cela inclut le nombre de hello de WebSocket de connexions autorisées.</span><span class="sxs-lookup"><span data-stu-id="02017-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="02017-182">Pour plus d’informations, consultez hello [page de tarification des applications Web].</span><span class="sxs-lookup"><span data-stu-id="02017-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="02017-183">Les messages ne sont pas envoyés avec WebSockets</span><span class="sxs-lookup"><span data-stu-id="02017-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="02017-184">Si les navigateurs clients conservent revenir toolong d’interrogation au lieu d’utiliser le protocole WebSocket, il peut être en raison d’une des manières suivantes les hello.</span><span class="sxs-lookup"><span data-stu-id="02017-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="02017-185">**Essayez en limitant hello transport toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="02017-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="02017-186">Dans l’ordre pour Socket.IO toouse WebSocket en tant que hello transport de messagerie, hello serveur et le client doivent prendre en charge WebSocket.</span><span class="sxs-lookup"><span data-stu-id="02017-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="02017-187">Si un ou hello autres n’existe pas, Socket.IO va négocier un autre transport, telles que l’interrogation longue.</span><span class="sxs-lookup"><span data-stu-id="02017-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="02017-188">liste des transports utilisés par Socket.IO par défaut de Hello est ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="02017-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="02017-189">Vous pouvez forcer il tooonly utiliser WebSocket en ajoutant hello suivant code toohello **app.js** fichier, après la ligne contenant de hello `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="02017-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="02017-190">Notez que les navigateurs plus anciens qui ne prennent pas en charge les WebSockets ne seront pas en mesure de tooconnect toohello site alors que hello au-dessus de code est actif, il restreint uniquement tooWebSockets de communication.</span><span class="sxs-lookup"><span data-stu-id="02017-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="02017-191">**Utilisation du protocole SSL**</span><span class="sxs-lookup"><span data-stu-id="02017-191">**Use SSL**</span></span>
  
    <span data-ttu-id="02017-192">Protocole WebSocket s’appuie sur certains en-têtes HTTP utilisés moindre, par exemple hello **mise à niveau** en-tête.</span><span class="sxs-lookup"><span data-stu-id="02017-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="02017-193">Certains périphériques réseau intermédiaires, tels que les proxys web, peuvent supprimer ces en-têtes.</span><span class="sxs-lookup"><span data-stu-id="02017-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="02017-194">tooavoid ce problème, vous pouvez établir la connexion WebSocket hello via le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="02017-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="02017-195">Un moyen simple de tooaccomplish Voici tooconfigure Socket.IO trop`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="02017-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="02017-196">Cela indique hello de communication Socket.IO toosecure WebSockets identique hello origine HTTP/HTTPS demande de page web de hello.</span><span class="sxs-lookup"><span data-stu-id="02017-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="02017-197">Si un navigateur utilise un toovisit URL HTTPS à votre site Web, les communications ultérieures WebSocket via Socket.IO seront sécurisées via le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="02017-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="02017-198">toomodify tooenable de cet exemple montre comment cette configuration, ajoutez hello suivant code toohello **app.js** fichier après hello ligne contenant `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="02017-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="02017-199">**Vérification des paramètres de web.config**</span><span class="sxs-lookup"><span data-stu-id="02017-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="02017-200">Les applications web Azure qui hébergent des applications Node.js utilisent hello **web.config** tooroute fichier entrant demande toohello Node.js application.</span><span class="sxs-lookup"><span data-stu-id="02017-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="02017-201">Pour toofunction WebSockets correctement avec les applications Node.js, hello **web.config** doit contenir hello entrée suivante.</span><span class="sxs-lookup"><span data-stu-id="02017-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="02017-202">Cela désactive le module WebSockets IIS hello, qui inclut sa propre implémentation de WebSocket et est en conflit avec les modules Node.js de WebSocket spécifiques telles que Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="02017-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="02017-203">Si cette ligne n’est pas présente ou est définie trop`true`, cela peut être la raison de hello transport WebSocket de hello ne fonctionne pas pour votre application.</span><span class="sxs-lookup"><span data-stu-id="02017-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="02017-204">Normalement, les applications Node.js n’incluent pas de fichier **web.config**. Par conséquent, l’offre Sites Web Azure en génère un automatiquement pour les applications Node.js lors de leur déploiement.</span><span class="sxs-lookup"><span data-stu-id="02017-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="02017-205">Étant donné que ce fichier est généré automatiquement sur le serveur de hello, vous devez utiliser hello FTP ou FTPS une URL pour votre site Web tooview de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="02017-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="02017-206">Vous pouvez trouver hello FTP et FTPS des URL de votre site dans le portail classique de hello en sélectionnant votre application web et puis hello **tableau de bord** lien.</span><span class="sxs-lookup"><span data-stu-id="02017-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="02017-207">Hello URL sont affichés dans hello **coup de œil rapide** section.</span><span class="sxs-lookup"><span data-stu-id="02017-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="02017-208">Hello **web.config** fichier est généré uniquement par les sites Web Azure si votre application n’en fournit pas.</span><span class="sxs-lookup"><span data-stu-id="02017-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="02017-209">Si vous fournissez un **web.config** fichier racine hello de votre projet d’application, il sera utilisé par les applications Web Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="02017-210">Si les entrée hello n’est pas présente ou a la valeur tooa de `true`, vous devez créer un **web.config** hello racine de votre application Node.js et spécifiez la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="02017-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="02017-211">Pour référence, hello ci-dessous est une valeur par défaut **web.config** pour une application qui utilise **app.js** en tant que point d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="02017-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="02017-212">Si votre application utilise un point d’entrée autre que **app.js**, vous devez remplacer toutes les occurrences de **app.js** avec hello corriger le point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="02017-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="02017-213">Par exemple, vous devez remplacer **app.js** par **server.js**.</span><span class="sxs-lookup"><span data-stu-id="02017-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="02017-214">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications], où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="02017-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="02017-215">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="02017-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="02017-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02017-216">Next steps</span></span>
<span data-ttu-id="02017-217">Dans ce didacticiel, vous avez appris comment toocreate une application de conversation hébergé dans une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="02017-218">Vous pouvez également héberger cette application dans le service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="02017-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="02017-219">Pour obtenir des instructions sur la façon de tooaccomplish, consultez [générer une Application de Chat Node.js avec Socket.IO sur un Service Cloud Azure].</span><span class="sxs-lookup"><span data-stu-id="02017-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="02017-220">Pour plus d’informations, consultez également hello [centre de développement Node.js].</span><span class="sxs-lookup"><span data-stu-id="02017-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="02017-221">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="02017-221">What's changed</span></span>
* <span data-ttu-id="02017-222">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants].</span><span class="sxs-lookup"><span data-stu-id="02017-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Cache Redis Azure]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[page de tarification des applications Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[générer une Application de Chat Node.js avec Socket.IO sur un Service Cloud Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service et son Impact sur les Services Azure existants]: http://go.microsoft.com/fwlink/?LinkId=529714
[centre de développement Node.js]: /develop/nodejs/
[essayez du Service d’applications]: https://azure.microsoft.com/try/app-service/
[Affinité d'instance dans Sites Web Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[créer un cache dans le Cache Redis Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[référentiel GitHub de Socket.IO]: https://github.com/socketio/socket.io
[ZIP ou GZ archivé version]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
