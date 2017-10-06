---
title: aaaCreate une application Ruby avec les applications Web sur Linux | Documents Microsoft
description: En savoir plus toocreate Ruby applications avec les fournisseurs de services web Azure sous Linux.
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
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="cb59f-104">Création d’une application Ruby dans Web Apps sur Linux</span><span class="sxs-lookup"><span data-stu-id="cb59f-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="cb59f-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="cb59f-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="cb59f-106">Ce démarrage rapide vous montre comment toocreate base Ruby sur l’application de quadrillage puis déployez-le tooAzure comme une application Web sur Linux.</span><span class="sxs-lookup"><span data-stu-id="cb59f-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="cb59f-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cb59f-108">Prerequisites</span></span>

* <span data-ttu-id="cb59f-109">[Ruby 2.4.1 ou une version ultérieure](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="cb59f-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="cb59f-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="cb59f-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="cb59f-111">Un [abonnement Azure actif](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb59f-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="cb59f-112">Télécharger l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="cb59f-112">Download hello sample</span></span>

<span data-ttu-id="cb59f-113">Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="cb59f-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="cb59f-114">Exécutez hello application localement</span><span class="sxs-lookup"><span data-stu-id="cb59f-114">Run hello application locally</span></span>

<span data-ttu-id="cb59f-115">Exécuter le serveur de rails de hello dans l’ordre pour hello application toowork.</span><span class="sxs-lookup"><span data-stu-id="cb59f-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="cb59f-116">Modifier toohello *-hello world* active et hello `rails server` commande démarre hello serveur.</span><span class="sxs-lookup"><span data-stu-id="cb59f-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="cb59f-117">À l’aide de votre navigateur web, accédez trop`http://localhost:3000` tootest hello application localement.</span><span class="sxs-lookup"><span data-stu-id="cb59f-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="cb59f-119">Modifier le message d’accueil application toodisplay</span><span class="sxs-lookup"><span data-stu-id="cb59f-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="cb59f-120">Modifier l’application hello afin qu’elle affiche un message d’accueil.</span><span class="sxs-lookup"><span data-stu-id="cb59f-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="cb59f-121">Modifier le contrôleur de l’application hello de sorte qu’elle retourne le message de type hello en tant que navigateur de toohello HTML.</span><span class="sxs-lookup"><span data-stu-id="cb59f-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="cb59f-122">Ouvrez *~/workspace/hello-world/app/controllers/application_controller.rb* pour le modifier.</span><span class="sxs-lookup"><span data-stu-id="cb59f-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="cb59f-123">Modifier hello `ApplicationController` toolook de classe comme hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="cb59f-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="cb59f-124">Votre application est désormais configurée.</span><span class="sxs-lookup"><span data-stu-id="cb59f-124">Your app is now configured.</span></span> <span data-ttu-id="cb59f-125">À l’aide de votre navigateur web, accédez trop`http://localhost:3000` page d’accueil tooconfirm hello racine.</span><span class="sxs-lookup"><span data-stu-id="cb59f-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Hello World configurée](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="cb59f-127">Créer une application web Ruby sur Azure</span><span class="sxs-lookup"><span data-stu-id="cb59f-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="cb59f-128">Hello d’utilisation [création d’un plan de az](https://docs.microsoft.com/cli/azure/appservice/plan#create) commande toocreate un plan de service d’application pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="cb59f-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="cb59f-129">Ensuite, émettez hello [az webapp créer](https://docs.microsoft.com/cli/azure/webapp) commande toocreate hello l’application web qui utilise le plan de service hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="cb59f-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="cb59f-130">Notez ce runtime hello est défini trop`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="cb59f-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="cb59f-131">N’oubliez pas tooreplace `<app name>` avec un nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="cb59f-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="cb59f-132">Une fois l’application hello web est créée, un **vue d’ensemble** page est tooview disponible.</span><span class="sxs-lookup"><span data-stu-id="cb59f-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="cb59f-133">Accédez à tooit.</span><span class="sxs-lookup"><span data-stu-id="cb59f-133">Navigate tooit.</span></span> <span data-ttu-id="cb59f-134">Hello suivant page de démarrage s’affiche :</span><span class="sxs-lookup"><span data-stu-id="cb59f-134">hello following splash page is displayed:</span></span>

![Page de démarrage](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="cb59f-136">Déployer votre application</span><span class="sxs-lookup"><span data-stu-id="cb59f-136">Deploy your application</span></span>

<span data-ttu-id="cb59f-137">Utiliser Git toodeploy hello application Ruby tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cb59f-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="cb59f-138">l’application web Hello dispose déjà d’un déploiement de Git configuré.</span><span class="sxs-lookup"><span data-stu-id="cb59f-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="cb59f-139">Vous pouvez récupérer des URL de déploiement hello en émettant un [déploiement d’application Web az](https://docs.microsoft.com/cli/azure/webapp/deployment) commande.</span><span class="sxs-lookup"><span data-stu-id="cb59f-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="cb59f-140">Notez que hello URL Git a hello suivant du formulaire basé sur le nom de votre application web :</span><span class="sxs-lookup"><span data-stu-id="cb59f-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="cb59f-141">Exécutez hello suivant de commandes toodeploy hello application locale tooyour site Web Azure :</span><span class="sxs-lookup"><span data-stu-id="cb59f-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="cb59f-142">Vérifiez que les opérations de déploiement à distance de hello signalent la réussite.</span><span class="sxs-lookup"><span data-stu-id="cb59f-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="cb59f-143">Hello commandes produisent toohello similaire après le texte de sortie :</span><span class="sxs-lookup"><span data-stu-id="cb59f-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="cb59f-144">Une fois le déploiement de hello est terminée, redémarrez votre application web pour effet de tootake hello déploiement à l’aide de hello [redémarrage de webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) de commande, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="cb59f-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="cb59f-145">Accédez tooyour site et vérifier les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="cb59f-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![application web mise à jour](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="cb59f-147">Pendant le redémarrage, application hello tentative toobrowse hello site entraîne un code d’état HTTP `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="cb59f-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="cb59f-148">Il peut prendre quelques minutes toofully redémarrage.</span><span class="sxs-lookup"><span data-stu-id="cb59f-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="cb59f-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cb59f-149">Next steps</span></span>

[<span data-ttu-id="cb59f-150">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="cb59f-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)