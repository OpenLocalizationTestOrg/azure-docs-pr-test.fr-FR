---
title: aaaCreate application web Node.js dans Azure | Documents Microsoft
description: "Déployez votre premier programme Hello World Node.js dans Azure App Service Web Apps en quelques minutes."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a>Créer une application web Node.js dans Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.  Ce démarrage rapide montre comment toodeploy un tooAzure d’application Node.js applications Web. Vous créez une application web de hello à l’aide de hello [CLI d’Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), et que vous utilisez Git toodeploy exemple Node.js code toohello web app.

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux. Une fois les conditions préalables de hello installés, il prend environ cinq minutes toocomplete étapes de hello.   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a>Composants requis

toocomplete ce démarrage rapide :

* [Installez Git](https://git-scm.com/)
* [Installez Node.js et NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Télécharger l’exemple hello

Dans une fenêtre de terminal, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

Vous utilisez des toutes les commandes hello toorun de cette fenêtre de terminal dans ce démarrage rapide.

Remplacez le répertoire toohello qui contient des exemples de code hello.

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Exécuter des application hello localement

Exécuter des application hello localement en ouvrant une fenêtre de terminal et en utilisant de hello `npm start` hello toolaunch de script serveur Node.js HTTP intégrée.

```bash
npm start
```

Ouvrez un navigateur web et accédez toohello exemple d’application à http://localhost:1337.

Vous consultez hello **Hello World** message à partir de l’application d’exemple hello affichée dans la page de hello.

![Exemple d’application s’exécutant localement](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

Dans la fenêtre de terminal, appuyez sur **Ctrl + C** serveur web de hello tooexit.

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Page d’application web vide](media/app-service-web-get-started-php/app-service-web-service-created.png)

Vous avez créé une application web vide dans Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Parcourir l’application de toohello

Parcourir toohello déployé l’application à l’aide de votre navigateur web.

```bash
http://<app_name>.azurewebsites.net
```

Hello Node.js exemple de code est en cours d’exécution dans une application web de Service d’applications Azure.

![Exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

**Félicitations !** Vous avez déployé votre tooApp d’application Node.js premier Service.

## <a name="update-and-redeploy-hello-code"></a>Mettre à jour et redéployer les code hello

À l’aide d’un éditeur de texte, ouvrez hello `index.js` de fichiers dans l’application de Node.js hello et apporter un petite modification du texte du toohello dans l’appel de hello trop`response.end`:

```nodejs
response.end("Hello Azure!");
```

Valider les modifications apportées dans Git et puis envoyez tooAzure de modifications de code hello.

```bash
git commit -am "updated output"
git push azure master
```

Une fois le déploiement terminé, basculer l’arrière toohello navigateur ouvert dans hello **Parcourir toohello application** pas à pas et cliquez sur Actualiser.

![Mise à jour de l’exemple d’application s’exécutant dans Azure](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

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
> [Node.js avec MongoDB](app-service-web-tutorial-nodejs-mongodb-app.md)
