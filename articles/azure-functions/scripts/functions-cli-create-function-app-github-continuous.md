---
title: "aaaCreate une application de la fonction et déployer le code de fonction à partir de GitHub | Documents Microsoft"
description: "Créer une Function App et déployer le code de fonction à partir de GitHub"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="a0724-103">Créer un App Service</span><span class="sxs-lookup"><span data-stu-id="a0724-103">Create an App Service</span></span>

<span data-ttu-id="a0724-104">Cet exemple de script crée une application de la fonction à l’aide de hello [le plan de la consommation](../functions-scale.md#consumption-plan) avec ses ressources connexes et en permanence déploie votre code de fonction à partir d’un référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0724-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="a0724-105">Dans cet exemple, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a0724-105">In this sample, you need:</span></span>

* <span data-ttu-id="a0724-106">Un référentiel GitHub avec du code de fonction, pour lequel vous disposez d’autorisations d’administration.</span><span class="sxs-lookup"><span data-stu-id="a0724-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="a0724-107">Un [jeton d’accès personnel](https://help.github.com/articles/creating-an-access-token-for-command-line-use) pour votre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0724-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a0724-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a0724-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a0724-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a0724-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a0724-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a0724-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a0724-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a0724-111">Sample script</span></span>

<span data-ttu-id="a0724-112">Cet exemple crée une Function App Azure et déploie le code de fonction à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0724-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a0724-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a0724-113">Script explanation</span></span>

<span data-ttu-id="a0724-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="a0724-114">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="a0724-115">Ce script utilise hello :</span><span class="sxs-lookup"><span data-stu-id="a0724-115">This script uses hello following:</span></span>

| <span data-ttu-id="a0724-116">Commande</span><span class="sxs-lookup"><span data-stu-id="a0724-116">Command</span></span> | <span data-ttu-id="a0724-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="a0724-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a0724-118">az group create</span><span class="sxs-lookup"><span data-stu-id="a0724-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a0724-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a0724-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a0724-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="a0724-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a0724-121">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="a0724-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a0724-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="a0724-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="a0724-123">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="a0724-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="a0724-124">Associe une Function App à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="a0724-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a0724-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0724-125">Next steps</span></span>

<span data-ttu-id="a0724-126">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0724-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a0724-127">Vous trouverez des exemples supplémentaires de script CLI de fonctions Azure Bonjour [documentation Azure fonctions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a0724-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
