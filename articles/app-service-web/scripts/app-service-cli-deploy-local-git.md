---
title: "Exemple de script Azure CLI - Créer une application web et déployer du code à partir d’un référentiel Git local | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer une application web et déployer du code à partir d’un référentiel Git local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="31872-103">Créer une application web et déployer du code à partir d’un référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="31872-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="31872-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="31872-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="31872-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="31872-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="31872-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="31872-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="31872-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="31872-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="31872-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="31872-108">Sample script</span></span>

<span data-ttu-id="31872-109">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Créer une application web et déployer du code à partir d’un référentiel Git")]</span><span class="sxs-lookup"><span data-stu-id="31872-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="31872-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="31872-110">Script explanation</span></span>

<span data-ttu-id="31872-111">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="31872-111">This script uses the following commands.</span></span> <span data-ttu-id="31872-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="31872-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="31872-113">Commande</span><span class="sxs-lookup"><span data-stu-id="31872-113">Command</span></span> | <span data-ttu-id="31872-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="31872-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="31872-115">az group create</span><span class="sxs-lookup"><span data-stu-id="31872-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="31872-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="31872-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="31872-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="31872-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="31872-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="31872-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="31872-119">az webapp create</span><span class="sxs-lookup"><span data-stu-id="31872-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="31872-120">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="31872-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="31872-121">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="31872-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="31872-122">Définit les informations d’identification de déploiement au niveau des comptes pour App Service.</span><span class="sxs-lookup"><span data-stu-id="31872-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="31872-123">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="31872-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="31872-124">Crée une configuration de contrôle source pour un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="31872-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="31872-125">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="31872-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="31872-126">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="31872-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="31872-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31872-127">Next steps</span></span>

<span data-ttu-id="31872-128">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31872-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="31872-129">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="31872-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
