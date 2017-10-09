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
# <a name="create-a-static-html-web-app-in-azure"></a>Créer une application web HTML statique dans Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.  Ce démarrage rapide montre comment toodeploy HTML + CSS base site tooAzure Web Apps. Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et que vous utilisez Git toodeploy exemple HTML toohello contenu web d’application.

![Page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux. Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.

## <a name="prerequisites"></a>Composants requis

toocomplete ce démarrage rapide :

- [Installez Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)].

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Télécharger l’exemple hello

Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Vous utilisez des toutes les commandes hello toorun de cette fenêtre de terminal dans ce démarrage rapide.

## <a name="view-hello-html"></a>Afficher hello HTML

Accédez répertoire toohello qui contient l’exemple hello HTML. Ouvrez hello *index.html* fichier dans votre navigateur.

![Page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-html/app-service-web-service-created.png)

Vous avez créé une application web vide dans Azure.

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

## <a name="browse-toohello-app"></a>Parcourir l’application de toohello

Dans un navigateur, accédez à toohello URL de l’application web Azure :

```
http://<app_name>.azurewebsites.net
```

page de Hello s’exécute comme une application web de Service d’applications Azure.

![Page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**Félicitations !** Vous avez déployé votre tooApp d’application HTML premier Service.

## <a name="update-and-redeploy-hello-app"></a>Mettre à jour et redéployer l’application hello

Ouvrez hello *index.html* de fichiers dans un éditeur de texte et une révision de toohello de modification. Par exemple, remplacez le titre de hello H1 à partir de « Azure App Service – exemple Site HTML statique » toojust » du Service d’applications Azure ».

Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.

```bash
git commit -am "updated HTML"
git push azure master
```

Une fois le déploiement terminé, actualisez vos modifications de hello toosee navigateur.

![Mise à jour de la page d’accueil de l’exemple d’application](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Gérer votre nouvelle application web Azure

Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage vous avez créé l’application web hello.

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-html/portal1.png)

Vous voyez apparaître la page Vue d’ensemble de votre application web. Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). 

![Panneau App Service sur le portail Azure](./media/app-service-web-get-started-html/portal2.png)

menu de gauche Hello fournit différentes pages de configuration de votre application. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Mapper un domaine personnalisé](app-service-web-tutorial-custom-domain.md)
