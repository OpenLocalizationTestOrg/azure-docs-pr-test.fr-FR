---
title: "Exemple de script Azure CLI - Créer un cache Redis Azure | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer un cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: afd7f6e0-9297-4c98-a95e-597be939cef7
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: c6b153d80de4cbf2bec1bc70d67be7befa0c5ec3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="4bf3a-103">Création d'un cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="4bf3a-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="4bf3a-104">Dans ce scénario, vous apprenez comment créer un cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="4bf3a-104">In this scenario, you learn how to create an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="4bf3a-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="4bf3a-105">Sample script</span></span>

<span data-ttu-id="4bf3a-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Cache Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="4bf3a-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4bf3a-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="4bf3a-107">Script explanation</span></span>

<span data-ttu-id="4bf3a-108">Ce script utilise les commandes suivantes pour créer un groupe de ressources et un cache Redis.</span><span class="sxs-lookup"><span data-stu-id="4bf3a-108">This script uses the following commands to create a resource group and a redis cache.</span></span> <span data-ttu-id="4bf3a-109">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="4bf3a-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4bf3a-110">Commande</span><span class="sxs-lookup"><span data-stu-id="4bf3a-110">Command</span></span> | <span data-ttu-id="4bf3a-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="4bf3a-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4bf3a-112">az group create</span><span class="sxs-lookup"><span data-stu-id="4bf3a-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4bf3a-113">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="4bf3a-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4bf3a-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="4bf3a-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="4bf3a-115">Créez une instance de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="4bf3a-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4bf3a-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4bf3a-116">Next steps</span></span>

<span data-ttu-id="4bf3a-117">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4bf3a-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4bf3a-118">Vous pouvez trouver des exemples supplémentaires de scripts CLI de cache Redis Azure dans la [documentation du cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4bf3a-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>