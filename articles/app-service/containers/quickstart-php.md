---
title: "Créer une application web PHP dans un conteneur Linux dans Azure | Microsoft Docs"
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
ms.date: 08/30/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2d5c8901e3deb126e216b58264c820b374b5670b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-php-web-app-in-a-linux-container-in-azure"></a>Créer une application web PHP dans un conteneur Linux dans Azure

[Web App for Containers](app-service-linux-intro.md) est un service d’hébergement web hautement scalable qui applique automatiquement des mises à jour correctives et utilise le système d’exploitation Linux. Ce didacticiel de démarrage rapide vous montre comment déployer une application PHP dans Azure Web App for Containers. Vous allez créer l’application web via [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) dans Cloud Shell et utiliser Git pour déployer le code PHP dans l’application web.

![Exemple d’application s’exécutant dans Azure]](media/quickstart-php/hello-world-in-browser.png)

Vous pouvez suivre les étapes ci-dessous en utilisant un ordinateur Mac, Windows ou Linux. 

## <a name="prerequisites"></a>Composants requis

Pour effectuer ce démarrage rapide :

* [Installez Git](https://git-scm.com/)
* [Installez PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a>Téléchargez l’exemple

Dans une fenêtre de terminal, exécutez les commandes suivantes pour cloner l’exemple d’application sur votre machine locale, puis accédez au répertoire contenant l’exemple de code.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a>Exécutez l’application localement.

Exécutez l’application localement en ouvrant une fenêtre de terminal et en utilisant la commande `php` pour lancer le serveur web PHP intégré.

```bash
php -S localhost:8080
```

Ouvrez un navigateur web et accédez à l’application exemple à l’adresse `http://localhost:8080`.

Vous voyez apparaître sur la page le message **Hello World !** de l’exemple d’application.

![Exemple d’application s’exécutant localement](media/quickstart-php/localhost-hello-world-in-browser.png)

Dans la fenêtre de terminal, appuyez sur **Ctrl + C** pour quitter le serveur web.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux.md)]

## <a name="create-a-web-app"></a>Créer une application web

[!INCLUDE [Create web app](../../../includes/app-service-web-create-web-app-linux-php-no-h.md)] 

Accédez au site pour voir votre nouvelle application web. Remplacez _&lt;app name>_ par un nom d’application unique.

```bash
http://<app name>.azurewebsites.net
```

![Page d’application web vide](media/quickstart-php/app-service-web-service-created.png)

Vous avez créé une application web vide dans un conteneur Linux avec le déploiement Git activé.

[!INCLUDE [Push to Azure](../../../includes/app-service-web-git-push-to-azure.md)] 

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

## <a name="browse-to-the-app"></a>Accéder à l’application

Accédez à l’application déployée à l’aide de votre navigateur web.

```bash
http://<app_name>.azurewebsites.net
```

L’exemple de code PHP s’exécute dans une application web Azure App Service.

![Exemple d’application s’exécutant dans Azure](media/quickstart-php/hello-world-in-browser.png)

**Félicitations !** Vous avez déployé votre première application en PHP dans App Service.

## <a name="update-locally-and-redeploy-the-code"></a>Mettre à jour localement et redéployer le code

À l’aide d’un éditeur de texte local, ouvrez le fichier `index.php` dans l’application PHP et modifiez une petite partie du texte contenu dans la chaîne en regard de l’élément `echo` :

```php
echo "Hello Azure!";
```

Validez vos modifications dans Git, puis envoyez les modifications de code à Azure.

```bash
git commit -am "updated output"
git push azure master
```

Une fois le déploiement terminé, revenez à la fenêtre du navigateur que vous avez ouverte à l’étape **Accéder à l’application**, puis actualisez la page.

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/quickstart-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gérer votre nouvelle application web Azure

Accédez au <a href="https://portal.azure.com" target="_blank">Portail Azure</a> pour gérer l’application web que vous avez créée.

Dans le menu de gauche, cliquez sur **App Services**, puis cliquez sur le nom de votre application web Azure.

![Navigation au sein du portail pour accéder à l’application web Azure](./media/quickstart-php/php-docs-hello-world-app-service-list.png)

Vous voyez apparaître la page Vue d’ensemble de votre application web. Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).

![Page App Service du Portail Azure](media/quickstart-php/php-docs-hello-world-app-service-detail.png)

Le menu de gauche fournit différentes pages vous permettant de configurer votre application. 

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [PHP avec MySQL](tutorial-php-mysql-app.md)
