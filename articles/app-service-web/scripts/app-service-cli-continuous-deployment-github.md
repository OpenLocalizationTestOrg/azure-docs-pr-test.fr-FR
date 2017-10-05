---
title: "Exemple de script Azure CLI - Créer une application web avec un déploiement continu à partir de GitHub | Microsoft Docs"
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
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="29813-103">Créer une application web avec un déploiement continu à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="29813-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="29813-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis configure un déploiement continu à partir d’un dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="29813-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="29813-105">Pour le déploiement GitHub sans déploiement continu, consultez [Créer une application web et déployer du code à partir de GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="29813-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="29813-106">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29813-106">In this sample, you will need:</span></span>

* <span data-ttu-id="29813-107">Un dépôt GitHub avec le code de l’application, pour lequel vous disposez d’autorisations d’administration.</span><span class="sxs-lookup"><span data-stu-id="29813-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="29813-108">Un [jeton d’accès personnel](https://help.github.com/articles/creating-an-access-token-for-command-line-use) pour votre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="29813-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="29813-109">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="29813-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="29813-110">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="29813-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="29813-111">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="29813-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="29813-112">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="29813-112">Sample script</span></span>

<span data-ttu-id="29813-113">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Créer une application web avec un déploiement continu à partir de GitHub")]</span><span class="sxs-lookup"><span data-stu-id="29813-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="29813-114">Explication du script</span><span class="sxs-lookup"><span data-stu-id="29813-114">Script explanation</span></span>

<span data-ttu-id="29813-115">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="29813-115">This script uses the following commands.</span></span> <span data-ttu-id="29813-116">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="29813-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="29813-117">Commande</span><span class="sxs-lookup"><span data-stu-id="29813-117">Command</span></span> | <span data-ttu-id="29813-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="29813-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="29813-119">az group create</span><span class="sxs-lookup"><span data-stu-id="29813-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="29813-120">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="29813-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="29813-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="29813-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="29813-122">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="29813-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="29813-123">az webapp create</span><span class="sxs-lookup"><span data-stu-id="29813-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="29813-124">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="29813-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="29813-125">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="29813-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="29813-126">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="29813-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="29813-127">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="29813-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="29813-128">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="29813-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="29813-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29813-129">Next steps</span></span>

<span data-ttu-id="29813-130">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="29813-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="29813-131">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="29813-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
