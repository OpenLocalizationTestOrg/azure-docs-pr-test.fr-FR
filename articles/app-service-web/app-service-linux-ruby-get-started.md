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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>Création d’une application Ruby dans Web Apps sur Linux 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques. Ce démarrage rapide vous montre comment toocreate base Ruby sur l’application de quadrillage puis déployez-le tooAzure comme une application Web sur Linux.

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>Composants requis

* [Ruby 2.4.1 ou une version ultérieure](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).
* [Git](https://git-scm.com/downloads).
* Un [abonnement Azure actif](https://azure.microsoft.com/pricing/free-trial/).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Télécharger l’exemple hello

Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local :

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>Exécutez hello application localement

Exécuter le serveur de rails de hello dans l’ordre pour hello application toowork. Modifier toohello *-hello world* active et hello `rails server` commande démarre hello serveur.

```bash
cd hello-world\bin
rails server
```
    
À l’aide de votre navigateur web, accédez trop`http://localhost:3000` tootest hello application localement.  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>Modifier le message d’accueil application toodisplay

Modifier l’application hello afin qu’elle affiche un message d’accueil. Modifier le contrôleur de l’application hello de sorte qu’elle retourne le message de type hello en tant que navigateur de toohello HTML. 

Ouvrez *~/workspace/hello-world/app/controllers/application_controller.rb* pour le modifier. Modifier hello `ApplicationController` toolook de classe comme hello suivant l’exemple de code :

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

Votre application est désormais configurée. À l’aide de votre navigateur web, accédez trop`http://localhost:3000` page d’accueil tooconfirm hello racine.

![Hello World configurée](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>Créer une application web Ruby sur Azure

Hello d’utilisation [création d’un plan de az](https://docs.microsoft.com/cli/azure/appservice/plan#create) commande toocreate un plan de service d’application pour votre application web. 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

Ensuite, émettez hello [az webapp créer](https://docs.microsoft.com/cli/azure/webapp) commande toocreate hello l’application web qui utilise le plan de service hello nouvellement créé. Notez ce runtime hello est défini trop`ruby|2.3`. N’oubliez pas tooreplace `<app name>` avec un nom d’application unique.

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

Une fois l’application hello web est créée, un **vue d’ensemble** page est tooview disponible. Accédez à tooit. Hello suivant page de démarrage s’affiche :

![Page de démarrage](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>Déployer votre application

Utiliser Git toodeploy hello application Ruby tooAzure. l’application web Hello dispose déjà d’un déploiement de Git configuré. Vous pouvez récupérer des URL de déploiement hello en émettant un [déploiement d’application Web az](https://docs.microsoft.com/cli/azure/webapp/deployment) commande.  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

Notez que hello URL Git a hello suivant du formulaire basé sur le nom de votre application web :

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

Exécutez hello suivant de commandes toodeploy hello application locale tooyour site Web Azure :

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

Vérifiez que les opérations de déploiement à distance de hello signalent la réussite. Hello commandes produisent toohello similaire après le texte de sortie :

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

Une fois le déploiement de hello est terminée, redémarrez votre application web pour effet de tootake hello déploiement à l’aide de hello [redémarrage de webapp az](https://docs.microsoft.com/cli/azure/webapp#restart) de commande, comme indiqué ici :

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

Accédez tooyour site et vérifier les résultats de hello.

```bash
http://<your web app name>.azurewebsites.net
```
![application web mise à jour](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Pendant le redémarrage, application hello tentative toobrowse hello site entraîne un code d’état HTTP `Error 503 Server unavailable`. Il peut prendre quelques minutes toofully redémarrage.
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>Étapes suivantes

[FAQ de l’application web Azure App Service sur Linux](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)