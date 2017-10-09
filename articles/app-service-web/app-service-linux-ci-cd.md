---
title: "aaaContinuous déploiement avec l’application Web Azure sous Linux | Documents Microsoft"
description: "Comment toosetup le déploiement continu dans l’application Web Azure sous Linux."
keywords: azure app service, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Déploiement continu avec l’application web Azure sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Dans ce didacticiel, vous allez configurer le déploiement continu d’une image de conteneur personnalisée à partir des référentiels [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) gérés ou du [hub Docker](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Étape 1 - tooAzure de connexion

Se connecter toohello portail Azure à http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Étape 2 : Activer la fonctionnalité de déploiement continu de conteneur

Vous pouvez activer à l’aide des fonctionnalités de déploiement continu hello [CLI d’Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) et l’exécution de hello commande suivante

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

Bonjour  **[portail Azure](https://portal.azure.com/)**, cliquez sur hello **du Service d’applications** option à gauche de hello de page de hello.

Cliquez sur nom hello de votre application de déploiement continu de Hub d’ancrage tooconfigure pour souhaitées.

Bonjour **paramètres de l’application**, ajouter une application appelé `DOCKER_ENABLE_CI` avec la valeur de hello `true`.

![insérer une image de Paramètres de l’application](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Étape 3 : préparer l’URL du webhook

Vous pouvez obtenir à l’aide de l’URL du Webhook hello [CLI d’Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) et l’exécution de hello commande suivante

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Pourquoi l’URL du Webhook, vous devez hello toohave après le point de terminaison : `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Vous pouvez obtenir votre `publishingusername` et `publishingpwd` en téléchargeant hello web application publier le profil à l’aide de hello portail Azure.

![insérer une image de l’ajout du webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Étape 4 : ajouter un webhook

### <a name="azure-container-registry"></a>Azure Container Registry

Dans le panneau de portail de votre registre, cliquez sur **Webhooks** et créez un nouveau webhook en cliquant sur **Ajouter**. Bonjour **créer webhook** panneau, donnez un nom à votre webhook. Pourquoi Webhook URI, vous devez tooprovide hello URL est obtenue à partir **étape 3**

Assurez-vous que vous définissez comme hello référentiel qui contient votre image de conteneur d’étendue de hello.

![insérer une image de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Lorsque l’image de hello est mise à jour, l’application hello web mis à jour automatiquement avec la nouvelle image de hello.

### <a name="docker-hub"></a>Hub Docker

Dans votre page Docker Hub, cliquez sur **Webhooks**, puis sur **Créer un Webhook**.

![insérer une image de l’ajout du webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Pourquoi l’URL du Webhook, vous devez tooprovide hello URL est obtenue à partir **étape 3**

![insérer une image de l’ajout du webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Lorsque l’image de hello est mise à jour, l’application hello web mis à jour automatiquement avec la nouvelle image de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Qu’est-ce qu’Azure Web App sur Linux ?](./app-service-linux-intro.md)
* [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/)
* [Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux](app-service-linux-using-nodejs-pm2.md)
* [Utilisation de .NET Core dans l’application web Azure sur Linux](app-service-linux-using-dotnetcore.md)
* [Utilisation de Ruby dans l’application web Azure sur Linux](app-service-linux-ruby-get-started.md)
* [Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux](./app-service-linux-using-custom-docker-image.md)
* [FAQ de l’application web Azure App Service sur Linux](./app-service-linux-faq.md) 
* [Gérer l’application web sur Linux à l’aide d’Azure CLI 2.0](./app-service-linux-cli.md)



