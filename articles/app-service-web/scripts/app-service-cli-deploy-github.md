---
title: "aaaAzure exemple de Script CLI - créer une application web avec le déploiement à partir de GitHub | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une application web avec un déploiement à partir de GitHub"
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
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="ce27e-103">Créer une application web avec un déploiement à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="ce27e-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="ce27e-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel GitHub public (sans déploiement continu).</span><span class="sxs-lookup"><span data-stu-id="ce27e-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="ce27e-105">Pour le déploiement GitHub avec déploiement continu, consultez [Créer une application web avec un déploiement continu à partir de GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="ce27e-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ce27e-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ce27e-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ce27e-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="ce27e-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ce27e-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ce27e-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ce27e-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ce27e-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ce27e-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ce27e-110">Script explanation</span></span> 

<span data-ttu-id="ce27e-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="ce27e-111">This script uses hello following commands.</span></span> <span data-ttu-id="ce27e-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="ce27e-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ce27e-113">Commande</span><span class="sxs-lookup"><span data-stu-id="ce27e-113">Command</span></span> | <span data-ttu-id="ce27e-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="ce27e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ce27e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ce27e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ce27e-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="ce27e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ce27e-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ce27e-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ce27e-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="ce27e-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ce27e-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ce27e-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ce27e-120">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ce27e-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ce27e-121">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="ce27e-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="ce27e-122">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="ce27e-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="ce27e-123">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="ce27e-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ce27e-124">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="ce27e-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ce27e-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce27e-125">Next steps</span></span>

<span data-ttu-id="ce27e-126">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce27e-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ce27e-127">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ce27e-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
