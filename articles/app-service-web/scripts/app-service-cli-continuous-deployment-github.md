---
title: "aaaAzure exemple de Script CLI - créer une application web avec un déploiement continu à partir de GitHub | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une application web avec un déploiement continu à partir de GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="fc4a8-103">Créer une application web avec un déploiement continu à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="fc4a8-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="fc4a8-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis configure un déploiement continu à partir d’un dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="fc4a8-105">Pour le déploiement GitHub sans déploiement continu, consultez [Créer une application web et déployer du code à partir de GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="fc4a8-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="fc4a8-106">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fc4a8-106">In this sample, you will need:</span></span>

* <span data-ttu-id="fc4a8-107">Un dépôt GitHub avec le code de l’application, pour lequel vous disposez d’autorisations d’administration.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="fc4a8-108">Un [jeton d’accès personnel](https://help.github.com/articles/creating-an-access-token-for-command-line-use) pour votre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fc4a8-109">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="fc4a8-110">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fc4a8-111">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fc4a8-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fc4a8-112">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="fc4a8-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="fc4a8-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="fc4a8-113">Script explanation</span></span>

<span data-ttu-id="fc4a8-114">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-114">This script uses hello following commands.</span></span> <span data-ttu-id="fc4a8-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fc4a8-116">Commande</span><span class="sxs-lookup"><span data-stu-id="fc4a8-116">Command</span></span> | <span data-ttu-id="fc4a8-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="fc4a8-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc4a8-118">az group create</span><span class="sxs-lookup"><span data-stu-id="fc4a8-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc4a8-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc4a8-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="fc4a8-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="fc4a8-121">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="fc4a8-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="fc4a8-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="fc4a8-123">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="fc4a8-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="fc4a8-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="fc4a8-125">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="fc4a8-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="fc4a8-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="fc4a8-127">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="fc4a8-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc4a8-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc4a8-128">Next steps</span></span>

<span data-ttu-id="fc4a8-129">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc4a8-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc4a8-130">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc4a8-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
