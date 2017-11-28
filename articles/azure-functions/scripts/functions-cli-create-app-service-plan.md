---
title: "Exemple de script Azure CLI - Créer une Function App dans un plan App Service | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer une Function App dans un plan App Service"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="dcce9-103">Créer une Function App dans un plan App Service</span><span class="sxs-lookup"><span data-stu-id="dcce9-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="dcce9-104">Cet exemple de script crée une Function App Azure, qui constitue un conteneur pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="dcce9-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="dcce9-105">La Function App est créée à l’aide d’un plan App Service dédié, ce qui signifie que vos ressources serveur sont toujours disponibles.</span><span class="sxs-lookup"><span data-stu-id="dcce9-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dcce9-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="dcce9-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dcce9-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="dcce9-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="dcce9-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dcce9-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dcce9-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="dcce9-109">Sample script</span></span>

<span data-ttu-id="dcce9-110">Ce script crée une Function App d’Azure en utilisant un [plan App Service](../functions-scale.md#app-service-plan) dédié.</span><span class="sxs-lookup"><span data-stu-id="dcce9-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="dcce9-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Créer une fonction Azure Functions sur un plan App Service")]</span><span class="sxs-lookup"><span data-stu-id="dcce9-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dcce9-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="dcce9-112">Script explanation</span></span>

<span data-ttu-id="dcce9-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="dcce9-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="dcce9-114">Ce script utilise les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dcce9-114">This script uses the following commands:</span></span>

| <span data-ttu-id="dcce9-115">Commande</span><span class="sxs-lookup"><span data-stu-id="dcce9-115">Command</span></span> | <span data-ttu-id="dcce9-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="dcce9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dcce9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="dcce9-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dcce9-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="dcce9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dcce9-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="dcce9-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="dcce9-120">Crée un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="dcce9-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="dcce9-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="dcce9-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="dcce9-122">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="dcce9-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="dcce9-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="dcce9-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="dcce9-124">Crée une Function App Azure.</span><span class="sxs-lookup"><span data-stu-id="dcce9-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcce9-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcce9-125">Next steps</span></span>

<span data-ttu-id="dcce9-126">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dcce9-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dcce9-127">Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dcce9-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
