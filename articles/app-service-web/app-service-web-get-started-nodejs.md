---
title: "Créer une application web Node.js dans Azure | Microsoft Docs"
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
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="7fb6d-103">Créer une application web Node.js dans Azure</span><span class="sxs-lookup"><span data-stu-id="7fb6d-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="7fb6d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="7fb6d-105">Ce guide de démarrage rapide vous indique comment déployer une application Node.js dans Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="7fb6d-106">Vous créez l’application web à l’aide de [l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et vous utilisez Git pour déployer l’exemple de code Node.js dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="7fb6d-108">Vous pouvez suivre les étapes ci-dessous en utilisant un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="7fb6d-109">Une fois les composants requis installés, l’exécution de cette procédure prend environ cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="7fb6d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7fb6d-110">Prerequisites</span></span>

<span data-ttu-id="7fb6d-111">Pour effectuer ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="7fb6d-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="7fb6d-112">Installez Git</span><span class="sxs-lookup"><span data-stu-id="7fb6d-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="7fb6d-113">Installez Node.js et NPM</span><span class="sxs-lookup"><span data-stu-id="7fb6d-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7fb6d-114">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7fb6d-115">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="7fb6d-116">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7fb6d-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="7fb6d-117">Téléchargez l’exemple</span><span class="sxs-lookup"><span data-stu-id="7fb6d-117">Download the sample</span></span>

<span data-ttu-id="7fb6d-118">Dans une fenêtre de terminal, exécutez la commande ci-après pour cloner le référentiel de l’exemple d’application sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="7fb6d-119">Vous utilisez cette fenêtre de terminal pour exécuter toutes les commandes de ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="7fb6d-120">Passez au répertoire qui contient l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="7fb6d-121">Exécutez l’application localement.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-121">Run the app locally</span></span>

<span data-ttu-id="7fb6d-122">Exécutez l’application localement en ouvrant une fenêtre de terminal et en utilisant le script `npm start` pour lancer le serveur HTTP Node.js intégré.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="7fb6d-123">Ouvrez un navigateur web et accédez à l’exemple d’application à l’adresse http://localhost:1337.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="7fb6d-124">Vous voyez apparaître sur la page le message **Hello World** de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="7fb6d-126">Dans la fenêtre de terminal, appuyez sur **Ctrl + C** pour quitter le serveur web.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="7fb6d-128">Vous avez créé une application web vide dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
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
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="7fb6d-129">Accéder à l’application</span><span class="sxs-lookup"><span data-stu-id="7fb6d-129">Browse to the app</span></span>

<span data-ttu-id="7fb6d-130">Accédez à l’application déployée à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="7fb6d-131">L’exemple de code Node.js s’exécute dans une application web Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="7fb6d-133">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="7fb6d-133">**Congratulations!**</span></span> <span data-ttu-id="7fb6d-134">Vous avez déployé votre première application Node.js dans App Service.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="7fb6d-135">Mettre à jour et redéployer le code</span><span class="sxs-lookup"><span data-stu-id="7fb6d-135">Update and redeploy the code</span></span>

<span data-ttu-id="7fb6d-136">À l’aide d’un éditeur de texte, ouvrez le fichier `index.js` dans l’application Node.js et apportez une petite modification au texte contenu dans l’appel pour `response.end` :</span><span class="sxs-lookup"><span data-stu-id="7fb6d-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="7fb6d-137">Validez vos modifications dans Git, puis envoyez les modifications de code à Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="7fb6d-138">Une fois le déploiement terminé, revenez à la fenêtre du navigateur ouverte à l’étape **Accéder à l’application**, puis cliquez sur Actualiser.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7fb6d-140">Gérer votre nouvelle application web Azure</span><span class="sxs-lookup"><span data-stu-id="7fb6d-140">Manage your new Azure web app</span></span>

<span data-ttu-id="7fb6d-141">Accédez au <a href="https://portal.azure.com" target="_blank">Portail Azure</a> pour gérer l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="7fb6d-142">Dans le menu de gauche, cliquez sur **App Services**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="7fb6d-144">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-144">You see your web app's Overview page.</span></span> <span data-ttu-id="7fb6d-145">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="7fb6d-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Panneau App Service sur le portail Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="7fb6d-147">Le menu de gauche fournit différentes pages vous permettant de configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="7fb6d-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="7fb6d-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7fb6d-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fb6d-149">Node.js avec MongoDB</span><span class="sxs-lookup"><span data-stu-id="7fb6d-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
