---
title: "aaaAzure exemple de Script CLI - créer une application de web ASP.NET Core dans un conteneur Docker à partir du Registre de conteneur Azure | Documents Microsoft"
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
ms.openlocfilehash: 0d4b1e706c2401ef813f48ef4de3d17fa2b6c9e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container-from-azure-container-registry"></a><span data-ttu-id="921aa-103">Créer une application ASP.NET Core dans un conteneur Docker à partir d’Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="921aa-103">Create an ASP.NET Core web app in a Docker container from Azure Container Registry</span></span>

<span data-ttu-id="921aa-104">Dans ce scénario, vous allez apprendre comment toocreate un groupe de ressources, les applications Linux plan et l’application web de service et déployer une application ASP.NET Core à l’aide d’un conteneur Docker à partir de hello Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="921aa-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container from hello Azure Container Registry.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="921aa-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="921aa-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="921aa-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="921aa-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="921aa-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="921aa-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="921aa-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="921aa-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-acr/deploy-linux-acr.sh?highlight=6-9 "Linux Azure Container Registry")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="921aa-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="921aa-109">Script explanation</span></span>

<span data-ttu-id="921aa-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="921aa-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="921aa-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="921aa-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="921aa-112">Commande</span><span class="sxs-lookup"><span data-stu-id="921aa-112">Command</span></span> | <span data-ttu-id="921aa-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="921aa-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="921aa-114">az group create</span><span class="sxs-lookup"><span data-stu-id="921aa-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="921aa-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="921aa-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="921aa-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="921aa-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="921aa-117">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="921aa-117">Creates an App Service plan.</span></span> <span data-ttu-id="921aa-118">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="921aa-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="921aa-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="921aa-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="921aa-120">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="921aa-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="921aa-121">az webapp config container set</span><span class="sxs-lookup"><span data-stu-id="921aa-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="921aa-122">Définit le conteneur Docker de hello pour hello Azure web app.</span><span class="sxs-lookup"><span data-stu-id="921aa-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="921aa-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="921aa-123">Next steps</span></span>

<span data-ttu-id="921aa-124">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="921aa-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="921aa-125">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="921aa-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
