---
title: "aaaAzure exemple de Script CLI - créer une application de fonction pour l’exécution sans serveur | Documents Microsoft"
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="35118-103">Créer une Function App pour une exécution sans serveur</span><span class="sxs-lookup"><span data-stu-id="35118-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="35118-104">Cet exemple de script crée une Function App Azure, qui constitue un conteneur pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="35118-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="35118-105">Hello fonction application créée à l’aide de hello [le plan de la consommation](../functions-scale.md#consumption-plan), ce qui est idéal pour les charges de travail sans serveur pilotée par événements.</span><span class="sxs-lookup"><span data-stu-id="35118-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="35118-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="35118-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="35118-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="35118-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="35118-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="35118-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="35118-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="35118-109">Sample script</span></span>

<span data-ttu-id="35118-110">Ce script crée une application de la fonction d’Azure à l’aide de hello [le plan de la consommation](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="35118-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="35118-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="35118-111">Script explanation</span></span>

<span data-ttu-id="35118-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="35118-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="35118-113">Ce script utilise hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="35118-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="35118-114">Commande</span><span class="sxs-lookup"><span data-stu-id="35118-114">Command</span></span> | <span data-ttu-id="35118-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="35118-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35118-116">az group create</span><span class="sxs-lookup"><span data-stu-id="35118-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="35118-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="35118-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35118-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="35118-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="35118-119">Crée un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="35118-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="35118-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="35118-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="35118-121">Crée une fonction Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="35118-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="35118-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35118-122">Next steps</span></span>

<span data-ttu-id="35118-123">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35118-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="35118-124">Vous trouverez des exemples supplémentaires de script CLI de fonctions Azure Bonjour [documentation Azure fonctions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="35118-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
