---
title: "Exemple de script Azure CLI - Créer une Function App pour une exécution sans serveur | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer une Function App pour une exécution sans serveur"
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
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="66b37-103">Créer une Function App pour une exécution sans serveur</span><span class="sxs-lookup"><span data-stu-id="66b37-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="66b37-104">Cet exemple de script crée une Function App Azure, qui constitue un conteneur pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="66b37-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="66b37-105">La Function App est créée à l’aide du [plan de consommation](../functions-scale.md#consumption-plan), ce qui est idéal pour les charges de travail sans serveur, pilotées par les événements.</span><span class="sxs-lookup"><span data-stu-id="66b37-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="66b37-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="66b37-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="66b37-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="66b37-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="66b37-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="66b37-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="66b37-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="66b37-109">Sample script</span></span>

<span data-ttu-id="66b37-110">Ce script crée une Function App Azure à l’aide du [plan de consommation](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="66b37-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="66b37-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Créer une fonction Azure Functions sur un plan de consommation")]</span><span class="sxs-lookup"><span data-stu-id="66b37-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="66b37-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="66b37-112">Script explanation</span></span>

<span data-ttu-id="66b37-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="66b37-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="66b37-114">Ce script utilise les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="66b37-114">This script uses the following commands:</span></span>

| <span data-ttu-id="66b37-115">Commande</span><span class="sxs-lookup"><span data-stu-id="66b37-115">Command</span></span> | <span data-ttu-id="66b37-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="66b37-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="66b37-117">az group create</span><span class="sxs-lookup"><span data-stu-id="66b37-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="66b37-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="66b37-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="66b37-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="66b37-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="66b37-120">Crée un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="66b37-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="66b37-121">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="66b37-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="66b37-122">Crée une fonction Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="66b37-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="66b37-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66b37-123">Next steps</span></span>

<span data-ttu-id="66b37-124">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66b37-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="66b37-125">Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="66b37-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
