---
title: "application de aaaNode.js à l’aide de Socket.io | Documents Microsoft"
description: "Découvrez comment socket.io toouse dans une application node.js hébergé sur Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="c550a-103">Création d'une application de conversation instantanée Node.js avec Socket.IO sur un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="c550a-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="c550a-104">Socket.IO permet une communication en temps réel entre votre serveur node.js et vos clients.</span><span class="sxs-lookup"><span data-stu-id="c550a-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="c550a-105">Ce didacticiel présente l'hébergement d'une application de conversation instantanée socket.IO dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c550a-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="c550a-106">Pour plus d’informations sur Socket.IO, consultez le site <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="c550a-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="c550a-107">Une capture d’écran de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c550a-107">A screenshot of hello completed application is below:</span></span>

![Une fenêtre de navigateur affichant service hello hébergé sur Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="c550a-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c550a-109">Prerequisites</span></span>
<span data-ttu-id="c550a-110">Vérifiez que hello suite de produits et les versions sont exemple hello complète de toosuccessfully installées dans cet article :</span><span class="sxs-lookup"><span data-stu-id="c550a-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="c550a-111">Installez [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="c550a-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="c550a-112">Installez [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="c550a-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="c550a-113">Installez [Python version 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="c550a-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="c550a-114">Création d'un projet de service cloud</span><span class="sxs-lookup"><span data-stu-id="c550a-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="c550a-115">Hello étapes suivantes créent projet de service cloud hello qui hébergera l’application de Socket.IO hello.</span><span class="sxs-lookup"><span data-stu-id="c550a-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="c550a-116">À partir de hello **Menu Démarrer** ou **écran d’accueil de**, recherchez **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c550a-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="c550a-117">Enfin, cliquez avec le bouton droit sur **Windows PowerShell** et sélectionnez **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="c550a-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icône Azure PowerShell][powershell-menu]
2. <span data-ttu-id="c550a-119">Créez un répertoire appelé **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="c550a-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="c550a-120">Modifiez les répertoires toohello **c:\\nœud** Active</span><span class="sxs-lookup"><span data-stu-id="c550a-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="c550a-121">Entrez hello suivant de commandes toocreate une solution nommée **chatapp** et un rôle de travail nommé **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="c550a-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="c550a-122">Vous verrez hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="c550a-122">You will see hello following response:</span></span>
   
    ![sortie Hello de hello nouvelle-azureservice et azurenodeworkerrolecmdlets ajouter](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="c550a-124">Télécharger hello Chat l’exemple</span><span class="sxs-lookup"><span data-stu-id="c550a-124">Download hello Chat Example</span></span>
<span data-ttu-id="c550a-125">Pour ce projet, nous allons utiliser exemple hello conversation hello [référentiel GitHub de Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="c550a-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="c550a-126">Effectuer hello étapes toodownload hello exemple suivant et l’ajouter projet toohello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c550a-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="c550a-127">Créer une copie locale du référentiel de hello à l’aide de hello **Clone** bouton.</span><span class="sxs-lookup"><span data-stu-id="c550a-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="c550a-128">Vous pouvez également utiliser hello **ZIP** projet de bouton toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="c550a-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Une fenêtre de navigateur affichage https://github.com/LearnBoost/socket.io/tree/master/examples/chat, avec l’icône de téléchargement ZIP hello mis en surbrillance][chat-example-view]
2. <span data-ttu-id="c550a-130">Parcourir la structure de répertoire de hello du référentiel local de hello jusqu'à ce que vous arriviez à hello **exemples\\chat** active.</span><span class="sxs-lookup"><span data-stu-id="c550a-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="c550a-131">Copier le contenu de hello de cette toothe active **C:\\nœud\\chatapp\\WorkerRole1** répertoire créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c550a-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Explorer, affichage du contenu des exemples de hello hello\\répertoire extraite à partir de l’archive de hello][chat-contents]
   
   <span data-ttu-id="c550a-133">Hello des éléments mis en surbrillance dans la capture d’écran hello ci-dessus sont des hello fichiers copiés à partir de hello **exemples\\chat** Active</span><span class="sxs-lookup"><span data-stu-id="c550a-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="c550a-134">Bonjour **C:\\nœud\\chatapp\\WorkerRole1** répertoire, delete hello **server.js** de fichiers, puis renommez hello **app.js**trop de fichiers**server.js**.</span><span class="sxs-lookup"><span data-stu-id="c550a-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="c550a-135">Cela supprime la valeur par défaut hello **server.js** fichier créé précédemment par hello **Add-AzureNodeWorkerRole** applet de commande et de remplacement avec une application hello à partir du fichier hello exemple de la conversation.</span><span class="sxs-lookup"><span data-stu-id="c550a-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="c550a-136">Modification du fichier Server.js et installation des modules</span><span class="sxs-lookup"><span data-stu-id="c550a-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="c550a-137">Avant l’application hello test Bonjour émulateur Azure, nous devons apporter de légères modifications.</span><span class="sxs-lookup"><span data-stu-id="c550a-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="c550a-138">Effectuez hello étapes toothe server.js fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="c550a-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="c550a-139">Ouvrez hello **server.js** fichier dans Visual Studio ou un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="c550a-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="c550a-140">Recherche hello **les dépendances de modules** section au début de hello de server.js et modifier hello ligne contenant **sio = require('.. //.. lib//Socket.IO')** trop**sio = require('socket.io')** comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c550a-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="c550a-141">application de hello tooensure écoute le port correct hello, ouvrez server.js dans le bloc-notes ou votre éditeur favori, puis modifiez la ligne suivante en remplaçant **3000** avec **process.env.port** comme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c550a-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="c550a-142">Après avoir enregistré les modifications de hello trop**server.js**, utilisez hello comme suit pour installer les modules requis, puis tester application hello dans l’émulateur Azure :</span><span class="sxs-lookup"><span data-stu-id="c550a-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="c550a-143">À l’aide de **Azure PowerShell**, modifiez les répertoires toohello **C:\\nœud\\chatapp\\WorkerRole1** hello active et l’utilisation après la commande tooinstall hello modules requis par cette application :</span><span class="sxs-lookup"><span data-stu-id="c550a-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="c550a-144">Cela va installer les modules hello répertoriés dans le fichier de package.json hello.</span><span class="sxs-lookup"><span data-stu-id="c550a-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="c550a-145">Une fois la commande hello terminée, vous devez voir s’afficher sortie similaire toothe :</span><span class="sxs-lookup"><span data-stu-id="c550a-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![commande d’installation de sortie Hello de hello npm][The-output-of-the-npm-install-command]
2. <span data-ttu-id="c550a-147">Dans la mesure où cet exemple a été initialement une partie de hello référentiel GitHub de Socket.IO bibliothèque Socket.IO de hello fait directement référence dans le chemin d’accès relatif, Socket.IO n’est pas référencée dans le fichier du package.json hello, donc nous devons l’installer en émettant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c550a-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="c550a-148">Test et déploiement</span><span class="sxs-lookup"><span data-stu-id="c550a-148">Test and Deploy</span></span>
1. <span data-ttu-id="c550a-149">Lancez l’émulateur de hello en émettant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c550a-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="c550a-150">Si vous rencontrez des problèmes pour le lancement de l’émulateur, par ex. : Start-AzureEmulator : une erreur inattendue est survenue.</span><span class="sxs-lookup"><span data-stu-id="c550a-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="c550a-151">Détails : A rencontré un erreur inattendue hello communication objet, System.ServiceModel.Channels.ServiceChannel ne peut pas servir pour la communication car il est déjà hello état Faulted.</span><span class="sxs-lookup"><span data-stu-id="c550a-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="c550a-152">réinstallez AzureAuthoringTools v 2.7.1 et AzureComputeEmulator v 2.7 : assurez-vous que la version correspond.</span><span class="sxs-lookup"><span data-stu-id="c550a-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="c550a-153">Ouvrez un navigateur et accédez trop**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="c550a-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="c550a-154">Lors de la fenêtre de navigateur hello s’ouvre, entrez le surnom et puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="c550a-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="c550a-155">Cela vous permettra toopost messages comme un surnom spécifique.</span><span class="sxs-lookup"><span data-stu-id="c550a-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="c550a-156">des fonctionnalités tootest multi-utilisateur, ouvrir des fenêtres de navigateur supplémentaires à l’aide de la même URL et entrez les surnoms différents.</span><span class="sxs-lookup"><span data-stu-id="c550a-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Deux fenêtres du navigateur affichant des messages de conversation instantanée des utilisateurs User1 et User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="c550a-158">Après l’application de test hello, arrêtez l’émulateur de hello en émettant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c550a-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="c550a-159">toodeploy tooAzure d’application hello, utilisez le **AzureServiceProject de publication** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="c550a-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="c550a-160">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c550a-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="c550a-161">Être vraiment toouse un nom unique, sinon hello processus de publication échoue.</span><span class="sxs-lookup"><span data-stu-id="c550a-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="c550a-162">Après la fin du déploiement de hello, navigateur de hello ouvrir et accédez toohello déployé service.</span><span class="sxs-lookup"><span data-stu-id="c550a-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="c550a-163">Si vous recevez une erreur indiquant que hello fourni de nom de l’abonnement n’existe pas dans hello importé le profil de publication, vous devez télécharger et importer le profil de publication hello pour votre abonnement avant de déployer tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c550a-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="c550a-164">Consultez hello **déploiement hello Application tooAzure** section [générer et déployer un tooan d’application Node.js Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="c550a-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Une fenêtre de navigateur affichant service hello hébergé sur Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="c550a-166">Si vous recevez une erreur indiquant que hello fourni de nom de l’abonnement n’existe pas dans hello importé le profil de publication, vous devez télécharger et importer le profil de publication hello pour votre abonnement avant de déployer tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c550a-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="c550a-167">Consultez hello **déploiement hello Application tooAzure** section [générer et déployer un tooan d’application Node.js Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="c550a-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="c550a-168">Votre application s'exécute à présent dans Azure, et peut transmettre des messages de conversation instantanée entre différents clients en utilisant Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="c550a-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="c550a-169">Par souci de simplicité, cet exemple est limitée toochatting entre toohello connecté des utilisateurs même instance.</span><span class="sxs-lookup"><span data-stu-id="c550a-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="c550a-170">Cela signifie que si le service de cloud computing hello crée deux instances de rôle de travail, les utilisateurs seulement pourront toochat avec d’autres utilisateurs connectés toohello même instance de rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="c550a-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="c550a-171">tooscale hello application toowork avec plusieurs instances de rôle, vous pouvez utiliser une technologie comme Service Bus tooshare hello Socket.IO stocker l’état entre les instances.</span><span class="sxs-lookup"><span data-stu-id="c550a-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="c550a-172">Pour obtenir des exemples, consultez Bonjour dans les exemples d’utilisation de files d’attente du Bus de Service et des rubriques hello [Azure SDK pour Node.js GitHub référentiel](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="c550a-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c550a-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c550a-173">Next steps</span></span>
<span data-ttu-id="c550a-174">Dans ce didacticiel, vous avez appris comment toocreate une application de base de conversation hébergés dans un Service Cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="c550a-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="c550a-175">toolearn toohost cette application dans un site Web Azure, voir [générer une Application de Chat Node.js avec Socket.IO sur un Site Web de Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="c550a-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="c550a-176">Pour plus d’informations, consultez également hello [centre de développement Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="c550a-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[référentiel GitHub de Socket.IO]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


