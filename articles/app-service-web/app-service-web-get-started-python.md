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
# <a name="create-a-python-web-app-in-azure"></a>Créer une application web Python dans Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.  Ce démarrage rapide décrit en détail le toodevelop et déployer un tooAzure d’application Python les applications Web. Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et que vous utilisez Git toodeploy exemple Python code toohello web app.

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux. Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.
## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

1. [Installez Git](https://git-scm.com/)
1. [Installez Python](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Télécharger l’exemple hello

Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

Vous utilisez des toutes les commandes hello toorun de cette fenêtre de terminal dans ce démarrage rapide.

Remplacez le répertoire toohello qui contient des exemples de code hello.

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Exécuter des application hello localement

Installer les packages hello requis à l’aide de `pip`.

```bash
pip install -r requirements.txt
```

Exécuter des application hello localement en ouvrant une fenêtre de terminal et en utilisant de hello `Python` serveur web intégré Python de commande toolaunch hello.

```bash
python main.py
```

Ouvrez un navigateur web et accédez toohello exemple d’application à http://localhost : 5000.

Vous pouvez voir hello **Hello World** message à partir de l’application d’exemple hello affichée dans la page de hello.

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

Dans la fenêtre de terminal, appuyez sur **Ctrl + C** serveur web de hello tooexit.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-python/app-service-web-service-created.png)

Vous avez créé une application web vide dans Azure.

## <a name="configure-toouse-python"></a>Configurer toouse Python

Hello d’utilisation [az webapp configuration défini](/cli/azure/webapp/config#set) version Python de commande tooconfigure hello web application toouse `3.4`.

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


Paramètre de version de Python hello ainsi utilise un conteneur par défaut fourni par la plateforme de hello. toouse votre propre conteneur, consultez hello référence CLI pour hello [az webapp configuration conteneur défini](/cli/azure/webapp/config/container#set) commande.

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

## <a name="browse-toohello-app"></a>Parcourir l’application de toohello

Parcourir toohello déployé l’application à l’aide de votre navigateur web.

```bash
http://<app_name>.azurewebsites.net
```

Hello, exemple de code Python est en cours d’exécution dans une application web de Service d’applications Azure.

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-python/hello-world-in-browser.png)

**Félicitations !** Vous avez déployé votre tooApp d’application Python premier Service.

## <a name="update-and-redeploy-hello-code"></a>Mettre à jour et redéployer les code hello

À l’aide d’un éditeur de texte local, ouvrez hello `main.py` de fichiers dans l’application de Python hello et apporter un toohello suivant de petite modification toohello texte `return` instruction :

```python
return 'Hello, Azure!'
```

Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.

```bash
git commit -am "updated output"
git push azure master
```

Une fois le déploiement terminé, basculer l’arrière toohello navigateur ouvert dans hello [Parcourir toohello application](#browse-to-the-app) étape et actualisation hello page.

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gérer votre nouvelle application web Azure

Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage vous avez créé l’application web hello.

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

Vous voyez apparaître la page Vue d’ensemble de votre application web. Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). 

![Panneau App Service sur le portail Azure](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

menu de gauche Hello fournit différentes pages de configuration de votre application. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Python avec PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
