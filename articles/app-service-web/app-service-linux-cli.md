---
title: "Gérer l’application web sur Linux à l’aide d’Azure CLI 2.0 | Microsoft Docs"
description: "Gérez l’application web sur Linux à l’aide d’Azure CLI."
keywords: azure app service, application web, cli, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="5fda9-104">Gérer l’application web sur Linux à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5fda9-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="5fda9-105">À l’aide des commandes de cet article, vous pouvez créer et gérer une application web sur Linux à l’aide d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5fda9-105">Using the commands in this article you are able to create and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="5fda9-106">Vous pouvez commencer à utiliser la nouvelle version de la CLI de deux manières :</span><span class="sxs-lookup"><span data-stu-id="5fda9-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="5fda9-107">[Installation d’Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5fda9-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="5fda9-108">Utilisation d’[Azure Cloud Shell (version préliminaire)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="5fda9-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="5fda9-109">Créer un plan App Service Linux</span><span class="sxs-lookup"><span data-stu-id="5fda9-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="5fda9-110">Pour créer un plan App Service Linux, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="5fda9-111">Créer une application web de conteneur Docker personnalisé</span><span class="sxs-lookup"><span data-stu-id="5fda9-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="5fda9-112">Pour créer une application web et la configurer pour utiliser un conteneur Docker personnalisé, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="5fda9-113">Activer la journalisation du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="5fda9-113">Activate the Docker container logging</span></span>

<span data-ttu-id="5fda9-114">Pour activer la journalisation du conteneur Docker, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="5fda9-115">Modifier le conteneur Docker personnalisé pour une application web existante sur l’application Linux</span><span class="sxs-lookup"><span data-stu-id="5fda9-115">Change the custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="5fda9-116">Pour modifier une application créée précédemment, de l’image Docker actuelle en une nouvelle image, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="5fda9-117">Utilisation d’images Docker d’un registre privé</span><span class="sxs-lookup"><span data-stu-id="5fda9-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="5fda9-118">Vous pouvez configurer votre application pour utiliser des images d’un registre privé.</span><span class="sxs-lookup"><span data-stu-id="5fda9-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="5fda9-119">Vous devez fournir l’URL de votre registre, le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5fda9-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="5fda9-120">Ceci peut être effectué à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="5fda9-121">Activer les déploiements continus d’images Docker personnalisées</span><span class="sxs-lookup"><span data-stu-id="5fda9-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="5fda9-122">Avec la commande suivante, vous pouvez activer la fonctionnalité CD et obtenir l’URL webhook.</span><span class="sxs-lookup"><span data-stu-id="5fda9-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="5fda9-123">Cette URL peut être utilisée pour configurer votre référentiel DockerHub ou Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="5fda9-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="5fda9-124">Créer une application web sur l’application Linux à l’aide de l’une de nos infrastructures d’exécution intégrées</span><span class="sxs-lookup"><span data-stu-id="5fda9-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="5fda9-125">Pour créer une application web PHP 5.6 sur l’application Linux, vous pouvez utiliser la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="5fda9-125">To create a PHP 5.6 Web App on Linux App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="5fda9-126">Modifier la version de l’infrastructure pour une application web existante sur l’application Linux</span><span class="sxs-lookup"><span data-stu-id="5fda9-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="5fda9-127">Pour modifier une application créée précédemment, de la version d’infrastructure actuelle en Node.js 6.11, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="5fda9-128">Configurer des déploiements Git pour votre application web</span><span class="sxs-lookup"><span data-stu-id="5fda9-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="5fda9-129">Pour configurer des déploiements Git pour votre application, vous pouvez utiliser la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5fda9-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="5fda9-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5fda9-130">Next steps</span></span>
* [<span data-ttu-id="5fda9-131">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="5fda9-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="5fda9-132">Installation d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5fda9-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="5fda9-133">Azure Cloud Shell (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="5fda9-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="5fda9-134">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5fda9-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="5fda9-135">Déploiement continu avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="5fda9-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
