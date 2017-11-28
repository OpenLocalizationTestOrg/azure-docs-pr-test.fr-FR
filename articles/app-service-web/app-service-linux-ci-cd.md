---
title: "Déploiement continu avec l’application web Azure sur Linux | Microsoft Docs"
description: "Configuration du déploiement continu Docker Hub avec l’application web Azure sur Linux."
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="05bc7-104">Déploiement continu avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="05bc7-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="05bc7-105">Dans ce didacticiel, vous allez configurer le déploiement continu d’une image de conteneur personnalisée à partir des référentiels [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) gérés ou du [hub Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="05bc7-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="05bc7-106">Étape 1 : se connecter à Azure</span><span class="sxs-lookup"><span data-stu-id="05bc7-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="05bc7-107">Connectez-vous au portail Azure à l’adresse http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="05bc7-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="05bc7-108">Étape 2 : Activer la fonctionnalité de déploiement continu de conteneur</span><span class="sxs-lookup"><span data-stu-id="05bc7-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="05bc7-109">Vous pouvez activer la fonctionnalité de déploiement continu avec [l’interface de ligne de commande Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) et en exécutant la commande suivante</span><span class="sxs-lookup"><span data-stu-id="05bc7-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="05bc7-110">Dans le **[portail Azure](https://portal.azure.com/)**, cliquez sur l’option **App Service** sur le côté gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="05bc7-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="05bc7-111">Cliquez sur le nom de l’application pour laquelle vous souhaitez configurer le déploiement continu Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="05bc7-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="05bc7-112">Dans **Paramètres de l’application**, ajoutez un paramètre d’application nommé `DOCKER_ENABLE_CI` avec la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="05bc7-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![insérer une image de Paramètres de l’application](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="05bc7-114">Étape 3 : préparer l’URL du webhook</span><span class="sxs-lookup"><span data-stu-id="05bc7-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="05bc7-115">Vous pouvez obtenir l’URL du Webhook avec [l’interface de ligne de commande Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) et en exécutant la commande suivante</span><span class="sxs-lookup"><span data-stu-id="05bc7-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="05bc7-116">Pour l’URL du Webhook, vous devez disposer du point de terminaison suivant : `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="05bc7-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="05bc7-117">Vous pouvez obtenir votre `publishingusername` et `publishingpwd` en téléchargeant le profil de publication de l’application web à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="05bc7-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![insérer une image de l’ajout du webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="05bc7-119">Étape 4 : ajouter un webhook</span><span class="sxs-lookup"><span data-stu-id="05bc7-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="05bc7-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="05bc7-120">Azure Container Registry</span></span>

<span data-ttu-id="05bc7-121">Dans le panneau de portail de votre registre, cliquez sur **Webhooks** et créez un nouveau webhook en cliquant sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="05bc7-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="05bc7-122">Dans le panneau **Create webhook** (Créer un webhook), donnez un nom à votre webhook.</span><span class="sxs-lookup"><span data-stu-id="05bc7-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="05bc7-123">Pour l’URI du webhook, vous devez fournir l’URL obtenue à l’**étape 3**.</span><span class="sxs-lookup"><span data-stu-id="05bc7-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="05bc7-124">Veillez à définir l’étendue comme référentiel qui contient votre image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="05bc7-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![insérer une image de webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="05bc7-126">Lorsque l’image est mise à jour, l’application web est mise à jour automatiquement avec la nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="05bc7-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="05bc7-127">Hub Docker</span><span class="sxs-lookup"><span data-stu-id="05bc7-127">Docker Hub</span></span>

<span data-ttu-id="05bc7-128">Dans votre page Docker Hub, cliquez sur **Webhooks**, puis sur **Créer un Webhook**.</span><span class="sxs-lookup"><span data-stu-id="05bc7-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![insérer une image de l’ajout du webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="05bc7-130">Pour l’URL du webhook, vous devez fournir l’URL obtenue à l’**étape 3**.</span><span class="sxs-lookup"><span data-stu-id="05bc7-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![insérer une image de l’ajout du webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="05bc7-132">Lorsque l’image est mise à jour, l’application web est mise à jour automatiquement avec la nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="05bc7-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05bc7-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05bc7-133">Next steps</span></span>
* [<span data-ttu-id="05bc7-134">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="05bc7-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="05bc7-135">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="05bc7-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="05bc7-136">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="05bc7-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="05bc7-137">Utilisation de .NET Core dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="05bc7-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="05bc7-138">Utilisation de Ruby dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="05bc7-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="05bc7-139">Comment utiliser une image Docker personnalisée pour l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="05bc7-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="05bc7-140">FAQ de Web App d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="05bc7-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="05bc7-141">Gérer l’application web sur Linux à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="05bc7-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



