---
title: "aaaManage l’application Web sur Linux à l’aide d’Azure CLI 2.0 | Documents Microsoft"
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
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="492b6-104">Gérer l’application web sur Linux à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="492b6-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="492b6-105">À l’aide des commandes hello dans cet article sont en mesure de toocreate et gérer une application Web sur Linux à l’aide d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="492b6-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="492b6-106">Vous pouvez commencer à l’aide de la nouvelle version de hello Hello CLI de deux manières :</span><span class="sxs-lookup"><span data-stu-id="492b6-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="492b6-107">[Installation d’Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="492b6-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="492b6-108">Utilisation d’[Azure Cloud Shell (version préliminaire)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="492b6-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="492b6-109">Créer un plan App Service Linux</span><span class="sxs-lookup"><span data-stu-id="492b6-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="492b6-110">toocreate un Plan de Service d’application Linux, vous pouvez utiliser hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="492b6-111">Créer une application web de conteneur Docker personnalisé</span><span class="sxs-lookup"><span data-stu-id="492b6-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="492b6-112">toocreate une application web et configuration toorun conteneur Docker personnalisé, vous pouvez utiliser hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="492b6-113">Activer la journalisation de conteneur Docker hello</span><span class="sxs-lookup"><span data-stu-id="492b6-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="492b6-114">tooactivate hello journalisation du conteneur Docker, vous pouvez utiliser des hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="492b6-115">Modifier le conteneur Docker personnalisé de hello pour une application Web existante sur Linux d’application</span><span class="sxs-lookup"><span data-stu-id="492b6-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="492b6-116">toochange une application créée précédemment, à partir de hello Docker image tooa nouvelle image actuelle, vous pouvez utiliser hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="492b6-117">Utilisation d’images Docker d’un registre privé</span><span class="sxs-lookup"><span data-stu-id="492b6-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="492b6-118">Vous pouvez configurer des images de toouse votre application à partir d’un Registre privé.</span><span class="sxs-lookup"><span data-stu-id="492b6-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="492b6-119">Vous devez tooprovide hello url pour votre Registre, le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="492b6-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="492b6-120">Cela peut être obtenue à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="492b6-121">Activer les déploiements continus d’images Docker personnalisées</span><span class="sxs-lookup"><span data-stu-id="492b6-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="492b6-122">Avec hello commande suivante, vous pouvez activer la fonctionnalité de CD hello et obtenir l’url du webhook hello.</span><span class="sxs-lookup"><span data-stu-id="492b6-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="492b6-123">Cette url peut être utilisé tooconfigure vous référentiels docker Hub ou le Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="492b6-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="492b6-124">Créer une application web sur l’application Linux à l’aide de l’une de nos infrastructures d’exécution intégrées</span><span class="sxs-lookup"><span data-stu-id="492b6-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="492b6-125">toocreate application Web PHP 5.6 sur application Linux, vous pouvez utiliser hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="492b6-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="492b6-126">Modifier la version de l’infrastructure pour une application web existante sur l’application Linux</span><span class="sxs-lookup"><span data-stu-id="492b6-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="492b6-127">toochange une application créée précédemment, à partir de tooNode.js de version de framework actuel hello 6.11, vous pouvez utiliser hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="492b6-128">Configurer des déploiements Git pour votre application web</span><span class="sxs-lookup"><span data-stu-id="492b6-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="492b6-129">tooset des déploiements Git pour votre application, vous pouvez utiliser hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="492b6-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="492b6-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="492b6-130">Next steps</span></span>
* [<span data-ttu-id="492b6-131">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="492b6-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="492b6-132">Installation d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="492b6-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="492b6-133">Azure Cloud Shell (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="492b6-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="492b6-134">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="492b6-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="492b6-135">Déploiement continu avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="492b6-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
