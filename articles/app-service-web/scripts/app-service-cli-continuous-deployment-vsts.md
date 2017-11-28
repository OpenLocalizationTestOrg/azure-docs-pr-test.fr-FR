---
title: "aaaAzure exemple de Script CLI - créer une application web avec un déploiement continu à partir de Visual Studio Team Services | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une application web avec un déploiement continu à partir de Visual Studio Team Services"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="738e6-103">Créer une application web avec un déploiement continu à partir de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="738e6-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="738e6-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis configure un déploiement continu à partir d’un dépôt Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="738e6-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="738e6-105">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="738e6-105">For this sample, you will need:</span></span>

* <span data-ttu-id="738e6-106">Un référentiel Visual Studio Team Services avec le code de l’application, pour lequel vous disposez d’autorisations d’administration.</span><span class="sxs-lookup"><span data-stu-id="738e6-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="738e6-107">Un [jeton d’accès personnel ](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)pour votre compte Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="738e6-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="738e6-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="738e6-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="738e6-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="738e6-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="738e6-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="738e6-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="738e6-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="738e6-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="738e6-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="738e6-112">Script explanation</span></span>

<span data-ttu-id="738e6-113">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="738e6-113">This script uses hello following commands.</span></span> <span data-ttu-id="738e6-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="738e6-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="738e6-115">Commande</span><span class="sxs-lookup"><span data-stu-id="738e6-115">Command</span></span> | <span data-ttu-id="738e6-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="738e6-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="738e6-117">az group create</span><span class="sxs-lookup"><span data-stu-id="738e6-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="738e6-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="738e6-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="738e6-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="738e6-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="738e6-120">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="738e6-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="738e6-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="738e6-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="738e6-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="738e6-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="738e6-123">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="738e6-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="738e6-124">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="738e6-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="738e6-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="738e6-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="738e6-126">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="738e6-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="738e6-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="738e6-127">Next steps</span></span>

<span data-ttu-id="738e6-128">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="738e6-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="738e6-129">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="738e6-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
