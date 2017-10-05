---
title: "Exemple de script Azure CLI - Créer une application ASP.NET Core dans un conteneur Docker à partir d’Azure Container Registry | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer une application ASP.NET Core dans un conteneur Docker à partir d’Azure Container Registry"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2556947d7cdd1475ae82ac2e1d61ad30ebd0d29f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="974c5-103">Créer une application ASP.NET Core dans un conteneur Docker à partir d’Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="974c5-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="974c5-104">Dans ce scénario, vous allez apprendre à créer un groupe de ressources, un plan App Service Linux et une application web, et à déployer une application ASP.NET Core à l’aide d’un conteneur Docker à partir d’Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="974c5-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from the Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="974c5-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="974c5-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="974c5-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="974c5-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="974c5-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="974c5-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="974c5-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="974c5-108">Sample script</span></span>

<span data-ttu-id="974c5-109">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span><span class="sxs-lookup"><span data-stu-id="974c5-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="974c5-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="974c5-110">Script explanation</span></span>

<span data-ttu-id="974c5-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="974c5-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="974c5-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="974c5-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="974c5-113">Commande</span><span class="sxs-lookup"><span data-stu-id="974c5-113">Command</span></span> | <span data-ttu-id="974c5-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="974c5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="974c5-115">az group create</span><span class="sxs-lookup"><span data-stu-id="974c5-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="974c5-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="974c5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="974c5-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="974c5-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="974c5-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="974c5-118">Creates an App Service plan.</span></span> <span data-ttu-id="974c5-119">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="974c5-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="974c5-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="974c5-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="974c5-121">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="974c5-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="974c5-122">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="974c5-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="974c5-123">Définit le conteneur Docker pour l’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="974c5-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="974c5-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="974c5-124">Next steps</span></span>

<span data-ttu-id="974c5-125">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="974c5-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="974c5-126">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="974c5-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
