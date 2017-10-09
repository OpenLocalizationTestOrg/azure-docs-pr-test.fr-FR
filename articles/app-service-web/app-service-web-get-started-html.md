---
title: "application web d’aaaCreate un code HTML statique dans Azure | Documents Microsoft"
description: "Découvrez comment toorun les applications web dans Azure App Service en déployant un code HTML statique exemple d’application."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="2fb57-103">Créer une application web HTML statique dans Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="2fb57-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="2fb57-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="2fb57-105">Ce démarrage rapide montre comment toodeploy HTML + CSS base site tooAzure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="2fb57-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="2fb57-106">Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et que vous utilisez Git toodeploy exemple HTML toohello contenu web d’application.</span><span class="sxs-lookup"><span data-stu-id="2fb57-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="2fb57-108">Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="2fb57-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="2fb57-109">Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fb57-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2fb57-110">Prerequisites</span></span>

<span data-ttu-id="2fb57-111">toocomplete ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="2fb57-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="2fb57-112">[Installez Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)].</span><span class="sxs-lookup"><span data-stu-id="2fb57-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2fb57-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2fb57-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="2fb57-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2fb57-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2fb57-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="2fb57-116">Télécharger l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-116">Download hello sample</span></span>

<span data-ttu-id="2fb57-117">Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="2fb57-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="2fb57-118">Vous utilisez des toutes les commandes hello toorun de cette fenêtre de terminal dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="2fb57-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="2fb57-119">Afficher hello HTML</span><span class="sxs-lookup"><span data-stu-id="2fb57-119">View hello HTML</span></span>

<span data-ttu-id="2fb57-120">Accédez répertoire toohello qui contient l’exemple hello HTML.</span><span class="sxs-lookup"><span data-stu-id="2fb57-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="2fb57-121">Ouvrez hello *index.html* fichier dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="2fb57-121">Open hello *index.html* file in your browser.</span></span>

![Page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="2fb57-124">Vous avez créé une application web vide dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="2fb57-125">Parcourir l’application de toohello</span><span class="sxs-lookup"><span data-stu-id="2fb57-125">Browse toohello app</span></span>

<span data-ttu-id="2fb57-126">Dans un navigateur, accédez à toohello URL de l’application web Azure :</span><span class="sxs-lookup"><span data-stu-id="2fb57-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="2fb57-127">page de Hello s’exécute comme une application web de Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-127">hello page is running as an Azure App Service web app.</span></span>

![Page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="2fb57-129">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="2fb57-129">**Congratulations!**</span></span> <span data-ttu-id="2fb57-130">Vous avez déployé votre tooApp d’application HTML premier Service.</span><span class="sxs-lookup"><span data-stu-id="2fb57-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="2fb57-131">Mettre à jour et redéployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="2fb57-131">Update and redeploy hello app</span></span>

<span data-ttu-id="2fb57-132">Ouvrez hello *index.html* de fichiers dans un éditeur de texte et une révision de toohello de modification.</span><span class="sxs-lookup"><span data-stu-id="2fb57-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="2fb57-133">Par exemple, remplacez le titre de hello H1 à partir de « Azure App Service – exemple Site HTML statique » toojust » du Service d’applications Azure ».</span><span class="sxs-lookup"><span data-stu-id="2fb57-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="2fb57-134">Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="2fb57-135">Une fois le déploiement terminé, actualisez vos modifications de hello toosee navigateur.</span><span class="sxs-lookup"><span data-stu-id="2fb57-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Mise à jour de la page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="2fb57-137">Gérer votre nouvelle application web Azure</span><span class="sxs-lookup"><span data-stu-id="2fb57-137">Manage your new Azure web app</span></span>

<span data-ttu-id="2fb57-138">Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="2fb57-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="2fb57-139">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb57-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="2fb57-141">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="2fb57-141">You see your web app's Overview page.</span></span> <span data-ttu-id="2fb57-142">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="2fb57-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Panneau App Service sur le portail Azure](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="2fb57-144">menu de gauche Hello fournit différentes pages de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="2fb57-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="2fb57-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2fb57-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2fb57-146">Mapper un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="2fb57-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
