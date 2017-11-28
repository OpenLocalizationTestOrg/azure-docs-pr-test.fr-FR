---
title: "Créer une application web PHP dans Azure | Microsoft Docs"
description: "Déployez votre premier programme Hello World PHP dans Azure App Service Web Apps en quelques minutes."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3a78e0b485046ad6228bf4819d3908042c298d1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="1403d-103">Créer une application web PHP dans Azure</span><span class="sxs-lookup"><span data-stu-id="1403d-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="1403d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="1403d-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="1403d-105">Ce guide de démarrage rapide vous indique comment déployer une application PHP dans Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1403d-105">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="1403d-106">Vous créez l’application web dans Cloud Shell grâce à l’interface [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et vous utilisez Git pour déployer l’exemple de code PHP dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="1403d-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

<span data-ttu-id="1403d-107">![Exemple d’application s’exécutant dans Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="1403d-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="1403d-108">Vous pouvez suivre les étapes ci-dessous en utilisant un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="1403d-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="1403d-109">Une fois les composants requis installés, l’exécution de cette procédure prend environ cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="1403d-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1403d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1403d-110">Prerequisites</span></span>

<span data-ttu-id="1403d-111">Pour effectuer ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="1403d-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="1403d-112">Installez Git</span><span class="sxs-lookup"><span data-stu-id="1403d-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="1403d-113">Installez PHP</span><span class="sxs-lookup"><span data-stu-id="1403d-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample-locally"></a><span data-ttu-id="1403d-114">Téléchargez l’exemple localement</span><span class="sxs-lookup"><span data-stu-id="1403d-114">Download the sample locally</span></span>

<span data-ttu-id="1403d-115">Exécutez les commandes suivantes dans une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="1403d-115">In a terminal window, run the following commands.</span></span> <span data-ttu-id="1403d-116">Cette action va cloner l’exemple d’application sur votre ordinateur local et vous faire accéder au répertoire contenant l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="1403d-116">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="1403d-117">Exécutez l’application localement.</span><span class="sxs-lookup"><span data-stu-id="1403d-117">Run the app locally</span></span>

<span data-ttu-id="1403d-118">Exécutez l’application localement en ouvrant une fenêtre de terminal et en utilisant la commande `php` pour lancer le serveur web PHP intégré.</span><span class="sxs-lookup"><span data-stu-id="1403d-118">Run the application locally by opening a terminal window and using the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="1403d-119">Ouvrez un navigateur web et accédez à l’exemple d’application à l’adresse http://localhost:8080.</span><span class="sxs-lookup"><span data-stu-id="1403d-119">Open a web browser, and navigate to the sample app at http://localhost:8080.</span></span>

<span data-ttu-id="1403d-120">Vous voyez apparaître sur la page le message **Hello World !**</span><span class="sxs-lookup"><span data-stu-id="1403d-120">You see the **Hello World!**</span></span> <span data-ttu-id="1403d-121">de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="1403d-121">message from the sample app displayed in the page.</span></span>

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="1403d-123">Dans la fenêtre de terminal, appuyez sur **Ctrl + C** pour quitter le serveur web.</span><span class="sxs-lookup"><span data-stu-id="1403d-123">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Page d’application web vide](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="1403d-125">Vous avez créé une application web vide dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1403d-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app-locally"></a><span data-ttu-id="1403d-126">Accéder à l’application localement</span><span class="sxs-lookup"><span data-stu-id="1403d-126">Browse to the app locally</span></span>

<span data-ttu-id="1403d-127">Accédez à l’application déployée à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="1403d-127">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="1403d-128">L’exemple de code PHP s’exécute dans une application web Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="1403d-128">The PHP sample code is running in an Azure App Service web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="1403d-130">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="1403d-130">**Congratulations!**</span></span> <span data-ttu-id="1403d-131">Vous avez déployé votre première application en PHP dans App Service.</span><span class="sxs-lookup"><span data-stu-id="1403d-131">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="1403d-132">Mettre à jour localement et redéployer le code</span><span class="sxs-lookup"><span data-stu-id="1403d-132">Update locally and redeploy the code</span></span>

<span data-ttu-id="1403d-133">À l’aide d’un éditeur de texte local, ouvrez le fichier `index.php` dans l’application PHP et modifiez une petite partie du texte contenu dans la chaîne en regard de l’élément `echo` :</span><span class="sxs-lookup"><span data-stu-id="1403d-133">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="1403d-134">Validez vos modifications dans Git, puis envoyez les modifications de code à Azure.</span><span class="sxs-lookup"><span data-stu-id="1403d-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="1403d-135">Une fois le déploiement terminé, revenez à la fenêtre du navigateur que vous avez ouverte à l’étape **Accéder à l’application**, puis actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="1403d-135">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="1403d-137">Gérer votre nouvelle application web Azure</span><span class="sxs-lookup"><span data-stu-id="1403d-137">Manage your new Azure web app</span></span>

<span data-ttu-id="1403d-138">Accédez au <a href="https://portal.azure.com" target="_blank">Portail Azure</a> pour gérer l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="1403d-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="1403d-139">Dans le menu de gauche, cliquez sur **App Services**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="1403d-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="1403d-141">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="1403d-141">You see your web app's Overview page.</span></span> <span data-ttu-id="1403d-142">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="1403d-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Panneau App Service sur le portail Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="1403d-144">Le menu de gauche fournit différentes pages vous permettant de configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="1403d-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="1403d-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1403d-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1403d-146">PHP avec MySQL</span><span class="sxs-lookup"><span data-stu-id="1403d-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
