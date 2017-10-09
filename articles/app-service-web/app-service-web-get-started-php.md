---
title: aaaCreate PHP web application dans Azure | Documents Microsoft
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
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a>Créer une application web PHP dans Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.  Ce didacticiel de démarrage rapide montre comment toodeploy un tooAzure d’application PHP applications Web. Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) en environnement de Cloud et vous utilisez Git toodeploy exemple code toohello web d’application PHP.

![Exemple d’application s’exécutant dans Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)

Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux. Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.

## <a name="prerequisites"></a>Composants requis

toocomplete ce démarrage rapide :

* [Installez Git](https://git-scm.com/)
* [Installez PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Télécharger l’exemple hello localement

Dans une fenêtre de terminal, exécutez hello suivant les commandes. Cette opération cloner l’ordinateur local du tooyour application exemple hello et accédez toohello répertoire conteneur hello exemple de code.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Exécuter des application hello localement

Exécuter des application hello localement en ouvrant une fenêtre de terminal et en utilisant de hello `php` serveur web intégré PHP de commande toolaunch hello.

```bash
php -S localhost:8080
```

Ouvrez un navigateur web et accédez toohello exemple d’application à http://localhost : 8080.

Vous consultez hello **Hello World !** message à partir de l’application d’exemple hello affichée dans la page de hello.

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

Dans la fenêtre de terminal, appuyez sur **Ctrl + C** serveur web de hello tooexit.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Page d’application web vide](media/app-service-web-get-started-php/app-service-web-service-created.png)

Vous avez créé une application web vide dans Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a>Parcourir l’application toohello localement

Parcourir toohello déployé l’application à l’aide de votre navigateur web.

```bash
http://<app_name>.azurewebsites.net
```

Hello, exemple de code PHP est en cours d’exécution dans une application web de Service d’applications Azure.

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Félicitations !** Vous avez déployé votre tooApp d’application PHP premier Service.

## <a name="update-locally-and-redeploy-hello-code"></a>Mettre à jour localement et redéployer les code hello

À l’aide d’un éditeur de texte local, ouvrez hello `index.php` au sein de l’application PHP hello et effectuez un texte de toohello petite modification au sein de la chaîne de hello ensuite trop`echo`:

```php
echo "Hello Azure!";
```

Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.

```bash
git commit -am "updated output"
git push azure master
```

Une fois le déploiement terminé, basculer l’arrière toohello navigateur ouvert dans hello **Parcourir toohello application** étape et actualisation hello page.

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gérer votre nouvelle application web Azure

Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage vous avez créé l’application web hello.

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

Vous voyez apparaître la page Vue d’ensemble de votre application web. Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).

![Panneau App Service sur le portail Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

menu de gauche Hello fournit différentes pages de configuration de votre application. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [PHP avec MySQL](app-service-web-tutorial-php-mysql.md)
