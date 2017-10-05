---
title: "Créer une Function App et déployer le code de fonction à partir de GitHub | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer une Function App et déployer le code de fonction à partir de GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="569c0-103">Créer une Function App et déployer le code de fonction à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="569c0-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="569c0-104">Cet exemple de script crée une Function App à l’aide du [plan de consommation](../functions-scale.md#consumption-plan) avec les ressources associées et déploie votre code de fonction à partir d’un référentiel GitHub public (sans déploiement continu).</span><span class="sxs-lookup"><span data-stu-id="569c0-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="569c0-105">En ce qui concerne la livraison continue du code de fonction à partir de GitHub, consultez la page [Créer une Function App et déployer en continu à partir de GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="569c0-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="569c0-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="569c0-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="569c0-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="569c0-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="569c0-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="569c0-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="569c0-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="569c0-109">Sample script</span></span>

<span data-ttu-id="569c0-110">Cet exemple crée une Function App Azure et déploie le code de fonction à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="569c0-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="569c0-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Créer une Function App avec un déploiement à partir de GitHub")]</span><span class="sxs-lookup"><span data-stu-id="569c0-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="569c0-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="569c0-112">Script explanation</span></span>

<span data-ttu-id="569c0-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="569c0-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="569c0-114">Ce script utilise les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="569c0-114">This script uses the following commands:</span></span>

| <span data-ttu-id="569c0-115">Commande</span><span class="sxs-lookup"><span data-stu-id="569c0-115">Command</span></span> | <span data-ttu-id="569c0-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="569c0-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="569c0-117">az group create</span><span class="sxs-lookup"><span data-stu-id="569c0-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="569c0-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="569c0-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="569c0-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="569c0-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="569c0-120">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="569c0-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="569c0-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="569c0-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="569c0-122">Crée une Function App Azure.</span><span class="sxs-lookup"><span data-stu-id="569c0-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="569c0-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="569c0-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="569c0-124">Associe une Function App à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="569c0-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="569c0-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="569c0-125">Next steps</span></span>

<span data-ttu-id="569c0-126">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="569c0-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="569c0-127">Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="569c0-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
