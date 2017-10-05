---
title: "Création d’une application Ruby dans Web Apps sur Linux | Microsoft Docs"
description: "Apprenez à créer des applications Ruby avec Web Apps sur Linux."
keywords: azure app service, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="4852e-104">Création d’une application Ruby dans Web Apps sur Linux</span><span class="sxs-lookup"><span data-stu-id="4852e-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="4852e-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="4852e-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="4852e-106">Ce guide de démarrage rapide vous montre comment créer une application Ruby on Rails de base puis la déployer dans Azure Web App sur Linux.</span><span class="sxs-lookup"><span data-stu-id="4852e-106">This quickstart shows you how to create a basic Ruby on Rails application you then deploy it to Azure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="4852e-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4852e-108">Prerequisites</span></span>

* <span data-ttu-id="4852e-109">[Ruby 2.4.1 ou une version ultérieure](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="4852e-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="4852e-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="4852e-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="4852e-111">Un [abonnement Azure actif](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4852e-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="4852e-112">Téléchargez l’exemple</span><span class="sxs-lookup"><span data-stu-id="4852e-112">Download the sample</span></span>

<span data-ttu-id="4852e-113">Dans une fenêtre de terminal, exécutez la commande ci-après pour cloner le référentiel de l’exemple d’application sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="4852e-113">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a><span data-ttu-id="4852e-114">Exécution locale de l'application</span><span class="sxs-lookup"><span data-stu-id="4852e-114">Run the application locally</span></span>

<span data-ttu-id="4852e-115">Exécutez le serveur Rails afin que l’application fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4852e-115">Run the rails server in order for the application to work.</span></span> <span data-ttu-id="4852e-116">Passez au répertoire *hello-world* et démarrez le serveur avec la commande `rails server`.</span><span class="sxs-lookup"><span data-stu-id="4852e-116">Change to the *hello-world* directory, and the `rails server` command starts the server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="4852e-117">À l’aide de votre navigateur web, accédez à `http://localhost:3000` pour tester l’application en local.</span><span class="sxs-lookup"><span data-stu-id="4852e-117">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>    

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a><span data-ttu-id="4852e-119">Modification de l’application pour afficher un message d’accueil</span><span class="sxs-lookup"><span data-stu-id="4852e-119">Modify app to display welcome message</span></span>

<span data-ttu-id="4852e-120">Modifiez l’application afin qu’elle affiche un message d’accueil.</span><span class="sxs-lookup"><span data-stu-id="4852e-120">Modify the application so it displays a welcome message.</span></span> <span data-ttu-id="4852e-121">Modifiez le contrôleur de l’application de sorte pour qu’il renvoie le message au format HTML au navigateur.</span><span class="sxs-lookup"><span data-stu-id="4852e-121">Change the application's controller so it returns the message as HTML to the browser.</span></span> 

<span data-ttu-id="4852e-122">Ouvrez *~/workspace/hello-world/app/controllers/application_controller.rb* pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="4852e-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="4852e-123">Modifiez la classe `ApplicationController` pour qu’elle ressemble à l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="4852e-123">Modify the `ApplicationController` class to look like the following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="4852e-124">Votre application est désormais configurée.</span><span class="sxs-lookup"><span data-stu-id="4852e-124">Your app is now configured.</span></span> <span data-ttu-id="4852e-125">À l’aide de votre navigateur web, accédez à `http://localhost:3000` pour vérifier la page d’accueil racine.</span><span class="sxs-lookup"><span data-stu-id="4852e-125">Using your web browser, navigate to `http://localhost:3000` to confirm the root landing page.</span></span>

![Hello World configurée](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="4852e-127">Créer une application web Ruby sur Azure</span><span class="sxs-lookup"><span data-stu-id="4852e-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="4852e-128">Utilisez la commande [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) pour créer un plan de service d’application pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="4852e-128">Use the [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command to create an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="4852e-129">Ensuite, utilisez la commande [az webapp créer](https://docs.microsoft.com/cli/azure/webapp) pour créer l’application web qui utilise le plan de service nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="4852e-129">Next, issue the [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command to create the web app that uses the newly created service plan.</span></span> <span data-ttu-id="4852e-130">Notez que le runtime est défini sur `ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="4852e-130">Notice that the runtime is set to `ruby|2.3`.</span></span> <span data-ttu-id="4852e-131">N’oubliez pas de remplacer `<app name>` par un nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="4852e-131">Don't forget to replace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="4852e-132">Une fois l’application web créée, une page **Vue d’ensemble** est disponible à l’affichage.</span><span class="sxs-lookup"><span data-stu-id="4852e-132">Once the web app is created, an **Overview** page is available to view.</span></span> <span data-ttu-id="4852e-133">Naviguez vers cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="4852e-133">Navigate to it.</span></span> <span data-ttu-id="4852e-134">La page de démarrage suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="4852e-134">The following splash page is displayed:</span></span>

![Page de démarrage](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="4852e-136">Déployer votre application</span><span class="sxs-lookup"><span data-stu-id="4852e-136">Deploy your application</span></span>

<span data-ttu-id="4852e-137">Utilisez Git pour déployer l’application Ruby sur Azure.</span><span class="sxs-lookup"><span data-stu-id="4852e-137">Use Git to deploy the Ruby application to Azure.</span></span> <span data-ttu-id="4852e-138">Un déploiement Git est déjà configuré sur l’application web.</span><span class="sxs-lookup"><span data-stu-id="4852e-138">The web app already has a Git deployment configured.</span></span> <span data-ttu-id="4852e-139">Vous pouvez récupérer l’URL de déploiement en utilisant une commande [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment).</span><span class="sxs-lookup"><span data-stu-id="4852e-139">You can retrieve the deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="4852e-140">Notez que l’URL Git a la forme suivante, selon le nom de votre application web :</span><span class="sxs-lookup"><span data-stu-id="4852e-140">Notice that the Git URL has the following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="4852e-141">Exécutez les commandes suivantes pour déployer l’application locale sur votre site web Azure :</span><span class="sxs-lookup"><span data-stu-id="4852e-141">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="4852e-142">Vérifiez que les opérations de déploiement à distance réussissent.</span><span class="sxs-lookup"><span data-stu-id="4852e-142">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="4852e-143">Les commandes produisent une sortie semblable au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="4852e-143">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="4852e-144">Une fois le déploiement terminé, redémarrez votre application web pour que le déploiement prenne effet en utilisant la commande [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart), comme présenté ici :</span><span class="sxs-lookup"><span data-stu-id="4852e-144">Once the deployment has completed, restart your web app for the deployment to take effect by using the [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="4852e-145">Accédez à votre site et vérifiez les résultats.</span><span class="sxs-lookup"><span data-stu-id="4852e-145">Navigate to your site and verify the results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![application web mise à jour](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="4852e-147">Si vous tentez de parcourir les résultats du site pendant que l’application redémarre, vous recevrez une erreur HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="4852e-147">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="4852e-148">Le redémarrage complet peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4852e-148">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="4852e-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4852e-149">Next steps</span></span>

[<span data-ttu-id="4852e-150">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="4852e-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)