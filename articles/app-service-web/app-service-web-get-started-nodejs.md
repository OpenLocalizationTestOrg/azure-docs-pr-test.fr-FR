---
title: aaaCreate application web Node.js dans Azure | Documents Microsoft
description: "Déployez votre premier programme Hello World Node.js dans Azure App Service Web Apps en quelques minutes."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="6b2ae-103">Créer une application web Node.js dans Azure</span><span class="sxs-lookup"><span data-stu-id="6b2ae-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="6b2ae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="6b2ae-105">Ce démarrage rapide montre comment toodeploy un tooAzure d’application Node.js applications Web.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="6b2ae-106">Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et que vous utilisez Git toodeploy exemple Node.js code toohello web app.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="6b2ae-108">Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="6b2ae-109">Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="6b2ae-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6b2ae-110">Prerequisites</span></span>

<span data-ttu-id="6b2ae-111">toocomplete ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="6b2ae-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="6b2ae-112">Installez Git</span><span class="sxs-lookup"><span data-stu-id="6b2ae-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="6b2ae-113">Installez Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="6b2ae-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b2ae-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6b2ae-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6b2ae-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b2ae-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="6b2ae-117">Télécharger l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="6b2ae-117">Download hello sample</span></span>

<span data-ttu-id="6b2ae-118">Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="6b2ae-119">Vous utilisez des toutes les commandes hello toorun de cette fenêtre de terminal dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="6b2ae-120">Remplacez le répertoire toohello qui contient des exemples de code hello.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="6b2ae-121">Exécuter des application hello localement</span><span class="sxs-lookup"><span data-stu-id="6b2ae-121">Run hello app locally</span></span>

<span data-ttu-id="6b2ae-122">Exécuter des application hello localement en ouvrant une fenêtre de terminal et en utilisant de hello `npm start` hello toolaunch de script serveur Node.js HTTP intégrée.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="6b2ae-123">Ouvrez un navigateur web et accédez toohello exemple d’application à http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="6b2ae-124">Vous consultez hello **Hello World** message à partir de l’application d’exemple hello affichée dans la page de hello.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="6b2ae-126">Dans la fenêtre de terminal, appuyez sur **Ctrl + C** serveur web de hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="6b2ae-128">Vous avez créé une application web vide dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="6b2ae-129">Parcourir l’application de toohello</span><span class="sxs-lookup"><span data-stu-id="6b2ae-129">Browse toohello app</span></span>

<span data-ttu-id="6b2ae-130">Parcourir toohello déployé l’application à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="6b2ae-131">Hello Node.js exemple de code est en cours d’exécution dans une application web de Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="6b2ae-133">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="6b2ae-133">**Congratulations!**</span></span> <span data-ttu-id="6b2ae-134">Vous avez déployé votre tooApp d’application Node.js premier Service.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="6b2ae-135">Mettre à jour et redéployer les code hello</span><span class="sxs-lookup"><span data-stu-id="6b2ae-135">Update and redeploy hello code</span></span>

<span data-ttu-id="6b2ae-136">À l’aide d’un éditeur de texte, ouvrez hello `index.js` de fichiers dans l’application de Node.js hello et apporter un petite modification du texte du toohello dans l’appel de hello trop`response.end`:</span><span class="sxs-lookup"><span data-stu-id="6b2ae-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="6b2ae-137">Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="6b2ae-138">Une fois le déploiement terminé, basculer l’arrière toohello navigateur ouvert dans hello **Parcourir toohello application** pas à pas et cliquez sur Actualiser.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="6b2ae-140">Gérer votre nouvelle application web Azure</span><span class="sxs-lookup"><span data-stu-id="6b2ae-140">Manage your new Azure web app</span></span>

<span data-ttu-id="6b2ae-141">Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="6b2ae-142">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="6b2ae-144">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-144">You see your web app's Overview page.</span></span> <span data-ttu-id="6b2ae-145">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="6b2ae-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Panneau App Service sur le portail Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="6b2ae-147">menu de gauche Hello fournit différentes pages de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="6b2ae-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="6b2ae-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b2ae-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b2ae-149">Node.js avec MongoDB</span><span class="sxs-lookup"><span data-stu-id="6b2ae-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
