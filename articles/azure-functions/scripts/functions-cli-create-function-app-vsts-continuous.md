---
title: "Créer une Function App et déployer le code de fonction à partir de Visual Studio Team Services | Microsoft Docs"
description: "Créer une Function App et déployer le code de fonction à partir de Visual Studio Team Services"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 2ef177b55ad7ffd351156821f429e6ff8fbeccc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="58ae7-103">Créer un App Service</span><span class="sxs-lookup"><span data-stu-id="58ae7-103">Create an App Service</span></span>

<span data-ttu-id="58ae7-104">Dans ce scénario, vous allez apprendre à créer une Function App à l’aide du [plan de consommation](../functions-scale.md#consumption-plan) avec les ressources associées, et à déployer en continu votre code de fonction à partir d’un référentiel Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="58ae7-104">In this scenario you will learn how to create a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="58ae7-105">Pour cet exemple, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="58ae7-105">In this sample, you will need:</span></span>

* <span data-ttu-id="58ae7-106">Un référentiel VSTS avec du code de fonction, pour lequel vous disposez d’autorisations d’administration.</span><span class="sxs-lookup"><span data-stu-id="58ae7-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="58ae7-107">Un [jeton d’accès personnel](https://help.github.com/articles/creating-an-access-token-for-command-line-use) pour votre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="58ae7-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="58ae7-108">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="58ae7-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="58ae7-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="58ae7-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="58ae7-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="58ae7-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="58ae7-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="58ae7-111">Sample script</span></span>

<span data-ttu-id="58ae7-112">Cet exemple crée une Function App Azure et déploie le code de la fonction à partir de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="58ae7-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

<span data-ttu-id="58ae7-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Service Azure")]</span><span class="sxs-lookup"><span data-stu-id="58ae7-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="58ae7-114">Explication du script</span><span class="sxs-lookup"><span data-stu-id="58ae7-114">Script explanation</span></span>

<span data-ttu-id="58ae7-115">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web, une instance DocumentDB et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="58ae7-115">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="58ae7-116">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="58ae7-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="58ae7-117">Commande</span><span class="sxs-lookup"><span data-stu-id="58ae7-117">Command</span></span> | <span data-ttu-id="58ae7-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="58ae7-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58ae7-119">az group create</span><span class="sxs-lookup"><span data-stu-id="58ae7-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="58ae7-120">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="58ae7-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58ae7-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="58ae7-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="58ae7-122">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="58ae7-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="58ae7-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="58ae7-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="58ae7-124">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="58ae7-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="58ae7-125">Associe une Function App à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="58ae7-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58ae7-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58ae7-126">Next steps</span></span>

<span data-ttu-id="58ae7-127">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="58ae7-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="58ae7-128">Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="58ae7-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
