---
title: "Exemple de script Azure CLI - Créer une application web avec un déploiement à partir de GitHub | Microsoft Docs"
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
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="97191-103">Créer une application web avec un déploiement à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="97191-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="97191-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel GitHub public (sans déploiement continu).</span><span class="sxs-lookup"><span data-stu-id="97191-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="97191-105">Pour le déploiement GitHub avec déploiement continu, consultez [Créer une application web avec un déploiement continu à partir de GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="97191-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="97191-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="97191-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="97191-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="97191-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="97191-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="97191-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="97191-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="97191-109">Sample script</span></span>

<span data-ttu-id="97191-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Créer une application web avec un déploiement à partir de GitHub")]</span><span class="sxs-lookup"><span data-stu-id="97191-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="97191-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="97191-111">Script explanation</span></span> 

<span data-ttu-id="97191-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="97191-112">This script uses the following commands.</span></span> <span data-ttu-id="97191-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="97191-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="97191-114">Commande</span><span class="sxs-lookup"><span data-stu-id="97191-114">Command</span></span> | <span data-ttu-id="97191-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="97191-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="97191-116">az group create</span><span class="sxs-lookup"><span data-stu-id="97191-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="97191-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="97191-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="97191-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="97191-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="97191-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="97191-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="97191-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="97191-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="97191-121">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="97191-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="97191-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="97191-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="97191-123">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="97191-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="97191-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="97191-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="97191-125">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="97191-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="97191-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="97191-126">Next steps</span></span>

<span data-ttu-id="97191-127">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97191-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="97191-128">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="97191-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
