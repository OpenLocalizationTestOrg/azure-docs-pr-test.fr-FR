---
title: "aaaCreate une application de la fonction et déployer le code de fonction à partir de GitHub | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une Function App et déployer le code de fonction à partir de GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="a8d72-103">Créer une Function App et déployer le code de fonction à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="a8d72-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="a8d72-104">Cet exemple de script crée une application de la fonction à l’aide de hello [le plan de la consommation](../functions-scale.md#consumption-plan) avec ses ressources connexes et déploie votre code de fonction à partir d’un référentiel GitHub public (sans déploiement continu).</span><span class="sxs-lookup"><span data-stu-id="a8d72-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="a8d72-105">En ce qui concerne la livraison continue du code de fonction à partir de GitHub, consultez la page [Créer une Function App et déployer en continu à partir de GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="a8d72-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a8d72-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a8d72-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a8d72-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a8d72-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a8d72-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8d72-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a8d72-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a8d72-109">Sample script</span></span>

<span data-ttu-id="a8d72-110">Cet exemple crée une Function App Azure et déploie le code de fonction à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8d72-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a8d72-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a8d72-111">Script explanation</span></span>

<span data-ttu-id="a8d72-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="a8d72-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="a8d72-113">Ce script utilise hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="a8d72-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="a8d72-114">Commande</span><span class="sxs-lookup"><span data-stu-id="a8d72-114">Command</span></span> | <span data-ttu-id="a8d72-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="a8d72-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a8d72-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a8d72-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a8d72-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a8d72-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a8d72-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="a8d72-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a8d72-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="a8d72-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a8d72-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="a8d72-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="a8d72-121">Crée une Function App Azure.</span><span class="sxs-lookup"><span data-stu-id="a8d72-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="a8d72-122">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="a8d72-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="a8d72-123">Associe une Function App à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="a8d72-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8d72-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8d72-124">Next steps</span></span>

<span data-ttu-id="a8d72-125">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a8d72-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a8d72-126">Vous trouverez des exemples supplémentaires de script CLI de fonctions Azure Bonjour [documentation Azure fonctions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a8d72-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
