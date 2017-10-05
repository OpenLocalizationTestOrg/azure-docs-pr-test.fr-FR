---
title: "Exemple de script Azure CLI - Créer une application web avec un déploiement continu à partir de Visual Studio Team Services | Microsoft Docs"
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
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="e487f-103">Créer une application web avec un déploiement continu à partir de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="e487f-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="e487f-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis configure un déploiement continu à partir d’un dépôt Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e487f-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="e487f-105">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e487f-105">For this sample, you will need:</span></span>

* <span data-ttu-id="e487f-106">Un référentiel Visual Studio Team Services avec le code de l’application, pour lequel vous disposez d’autorisations d’administration.</span><span class="sxs-lookup"><span data-stu-id="e487f-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="e487f-107">Un [jeton d’accès personnel ](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate)pour votre compte Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e487f-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e487f-108">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e487f-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e487f-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="e487f-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="e487f-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e487f-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e487f-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e487f-111">Sample script</span></span>

<span data-ttu-id="e487f-112">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Créer une application web avec un déploiement continu à partir de Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="e487f-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e487f-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e487f-113">Script explanation</span></span>

<span data-ttu-id="e487f-114">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="e487f-114">This script uses the following commands.</span></span> <span data-ttu-id="e487f-115">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="e487f-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e487f-116">Commande</span><span class="sxs-lookup"><span data-stu-id="e487f-116">Command</span></span> | <span data-ttu-id="e487f-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="e487f-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e487f-118">az group create</span><span class="sxs-lookup"><span data-stu-id="e487f-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e487f-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e487f-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e487f-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e487f-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e487f-121">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e487f-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e487f-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e487f-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e487f-123">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e487f-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e487f-124">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="e487f-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="e487f-125">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="e487f-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="e487f-126">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="e487f-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="e487f-127">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="e487f-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e487f-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e487f-128">Next steps</span></span>

<span data-ttu-id="e487f-129">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e487f-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e487f-130">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e487f-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
