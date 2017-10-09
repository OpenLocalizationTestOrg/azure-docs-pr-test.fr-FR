---
title: aaaCreate application web Python dans Azure | Documents Microsoft
description: "Déployez votre premier programme Hello World Python dans Azure App Service Web Apps en quelques minutes."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="0c4a4-103">Créer une application web Python dans Azure</span><span class="sxs-lookup"><span data-stu-id="0c4a4-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="0c4a4-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="0c4a4-105">Ce démarrage rapide décrit en détail le toodevelop et déployer un tooAzure d’application Python les applications Web.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="0c4a4-106">Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et que vous utilisez Git toodeploy exemple Python code toohello web app.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="0c4a4-108">Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="0c4a4-109">Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="0c4a4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c4a4-110">Prerequisites</span></span>

<span data-ttu-id="0c4a4-111">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="0c4a4-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="0c4a4-112">Installez Git</span><span class="sxs-lookup"><span data-stu-id="0c4a4-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="0c4a4-113">Installez Python</span><span class="sxs-lookup"><span data-stu-id="0c4a4-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0c4a4-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0c4a4-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0c4a4-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0c4a4-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="0c4a4-117">Télécharger l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="0c4a4-117">Download hello sample</span></span>

<span data-ttu-id="0c4a4-118">Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="0c4a4-119">Vous utilisez des toutes les commandes hello toorun de cette fenêtre de terminal dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="0c4a4-120">Remplacez le répertoire toohello qui contient des exemples de code hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="0c4a4-121">Exécuter des application hello localement</span><span class="sxs-lookup"><span data-stu-id="0c4a4-121">Run hello app locally</span></span>

<span data-ttu-id="0c4a4-122">Installer les packages hello requis à l’aide de `pip`.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="0c4a4-123">Exécuter des application hello localement en ouvrant une fenêtre de terminal et en utilisant de hello `Python` serveur web intégré Python de commande toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="0c4a4-124">Ouvrez un navigateur web et accédez toohello exemple d’application à http://localhost : 5000.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="0c4a4-125">Vous pouvez voir hello **Hello World** message à partir de l’application d’exemple hello affichée dans la page de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="0c4a4-127">Dans la fenêtre de terminal, appuyez sur **Ctrl + C** serveur web de hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="0c4a4-129">Vous avez créé une application web vide dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="0c4a4-130">Configurer toouse Python</span><span class="sxs-lookup"><span data-stu-id="0c4a4-130">Configure toouse Python</span></span>

<span data-ttu-id="0c4a4-131">Hello d’utilisation [az webapp configuration défini](/cli/azure/webapp/config#set) version Python de commande tooconfigure hello web application toouse `3.4`.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="0c4a4-132">Paramètre de version de Python hello ainsi utilise un conteneur par défaut fourni par la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="0c4a4-133">toouse votre propre conteneur, consultez hello référence CLI pour hello [az webapp configuration conteneur défini](/cli/azure/webapp/config/container#set) commande.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="0c4a4-134">Parcourir l’application de toohello</span><span class="sxs-lookup"><span data-stu-id="0c4a4-134">Browse toohello app</span></span>

<span data-ttu-id="0c4a4-135">Parcourir toohello déployé l’application à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="0c4a4-136">Hello, exemple de code Python est en cours d’exécution dans une application web de Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="0c4a4-138">**Félicitations !**</span><span class="sxs-lookup"><span data-stu-id="0c4a4-138">**Congratulations!**</span></span> <span data-ttu-id="0c4a4-139">Vous avez déployé votre tooApp d’application Python premier Service.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="0c4a4-140">Mettre à jour et redéployer les code hello</span><span class="sxs-lookup"><span data-stu-id="0c4a4-140">Update and redeploy hello code</span></span>

<span data-ttu-id="0c4a4-141">À l’aide d’un éditeur de texte local, ouvrez hello `main.py` de fichiers dans l’application de Python hello et apporter un toohello suivant de petite modification toohello texte `return` instruction :</span><span class="sxs-lookup"><span data-stu-id="0c4a4-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="0c4a4-142">Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="0c4a4-143">Une fois le déploiement terminé, basculer l’arrière toohello navigateur ouvert dans hello [Parcourir toohello application](#browse-to-the-app) étape et actualisation hello page.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="0c4a4-145">Gérer votre nouvelle application web Azure</span><span class="sxs-lookup"><span data-stu-id="0c4a4-145">Manage your new Azure web app</span></span>

<span data-ttu-id="0c4a4-146">Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage vous avez créé l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="0c4a4-147">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="0c4a4-149">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-149">You see your web app's Overview page.</span></span> <span data-ttu-id="0c4a4-150">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="0c4a4-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Panneau App Service sur le portail Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="0c4a4-152">menu de gauche Hello fournit différentes pages de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="0c4a4-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="0c4a4-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c4a4-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c4a4-154">Python avec PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0c4a4-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
