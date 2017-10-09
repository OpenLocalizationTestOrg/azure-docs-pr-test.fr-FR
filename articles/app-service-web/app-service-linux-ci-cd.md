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
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="261dc-104">Déploiement continu avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="261dc-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="261dc-105">Dans ce didacticiel, vous allez configurer le déploiement continu d’une image de conteneur personnalisée à partir des référentiels [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) gérés ou du [hub Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="261dc-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="261dc-106">Étape 1 - tooAzure de connexion</span><span class="sxs-lookup"><span data-stu-id="261dc-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="261dc-107">Se connecter toohello portail Azure à http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="261dc-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="261dc-108">Étape 2 : Activer la fonctionnalité de déploiement continu de conteneur</span><span class="sxs-lookup"><span data-stu-id="261dc-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="261dc-109">Vous pouvez activer à l’aide des fonctionnalités de déploiement continu hello [CLI d’Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) et l’exécution de hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="261dc-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="261dc-110">Bonjour  **[portail Azure](https://portal.azure.com/)**, cliquez sur hello **du Service d’applications** option à gauche de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="261dc-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="261dc-111">Cliquez sur nom hello de votre application de déploiement continu de Hub d’ancrage tooconfigure pour souhaitées.</span><span class="sxs-lookup"><span data-stu-id="261dc-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="261dc-112">Bonjour **paramètres de l’application**, ajouter une application appelé `DOCKER_ENABLE_CI` avec la valeur de hello `true`.</span><span class="sxs-lookup"><span data-stu-id="261dc-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![insérer une image de Paramètres de l’application](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="261dc-114">Étape 3 : préparer l’URL du webhook</span><span class="sxs-lookup"><span data-stu-id="261dc-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="261dc-115">Vous pouvez obtenir à l’aide de l’URL du Webhook hello [CLI d’Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) et l’exécution de hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="261dc-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="261dc-116">Pourquoi l’URL du Webhook, vous devez hello toohave après le point de terminaison : `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="261dc-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="261dc-117">Vous pouvez obtenir votre `publishingusername` et `publishingpwd` en téléchargeant hello web application publier le profil à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="261dc-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![insérer une image de l’ajout du webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="261dc-119">Étape 4 : ajouter un webhook</span><span class="sxs-lookup"><span data-stu-id="261dc-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="261dc-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="261dc-120">Azure Container Registry</span></span>

<span data-ttu-id="261dc-121">Dans le panneau de portail de votre registre, cliquez sur **Webhooks** et créez un nouveau webhook en cliquant sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="261dc-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="261dc-122">Bonjour **créer webhook** panneau, donnez un nom à votre webhook.</span><span class="sxs-lookup"><span data-stu-id="261dc-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="261dc-123">Pourquoi Webhook URI, vous devez tooprovide hello URL est obtenue à partir **étape 3**</span><span class="sxs-lookup"><span data-stu-id="261dc-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="261dc-124">Assurez-vous que vous définissez comme hello référentiel qui contient votre image de conteneur d’étendue de hello.</span><span class="sxs-lookup"><span data-stu-id="261dc-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![insérer une image de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="261dc-126">Lorsque l’image de hello est mise à jour, l’application hello web mis à jour automatiquement avec la nouvelle image de hello.</span><span class="sxs-lookup"><span data-stu-id="261dc-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="261dc-127">Hub Docker</span><span class="sxs-lookup"><span data-stu-id="261dc-127">Docker Hub</span></span>

<span data-ttu-id="261dc-128">Dans votre page Docker Hub, cliquez sur **Webhooks**, puis sur **Créer un Webhook**.</span><span class="sxs-lookup"><span data-stu-id="261dc-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![insérer une image de l’ajout du webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="261dc-130">Pourquoi l’URL du Webhook, vous devez tooprovide hello URL est obtenue à partir **étape 3**</span><span class="sxs-lookup"><span data-stu-id="261dc-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![insérer une image de l’ajout du webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="261dc-132">Lorsque l’image de hello est mise à jour, l’application hello web mis à jour automatiquement avec la nouvelle image de hello.</span><span class="sxs-lookup"><span data-stu-id="261dc-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="261dc-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="261dc-133">Next steps</span></span>
* [<span data-ttu-id="261dc-134">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="261dc-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="261dc-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="261dc-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="261dc-136">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="261dc-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="261dc-137">Utilisation de .NET Core dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="261dc-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="261dc-138">Utilisation de Ruby dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="261dc-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="261dc-139">Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="261dc-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="261dc-140">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="261dc-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="261dc-141">Gérer l’application web sur Linux à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="261dc-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



