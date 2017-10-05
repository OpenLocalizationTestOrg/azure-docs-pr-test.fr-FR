---
title: "Exemple de script Azure CLI - Créer un Cache Redis Azure Premium avec clustering | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer un Cache Redis Azure Premium avec clustering"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 87d0fe4c3eaa8f7b75343a36a069ecdac8241d74
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="0958b-103">Créer un Cache Redis Azure Premium avec clustering</span><span class="sxs-lookup"><span data-stu-id="0958b-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="0958b-104">Ce scénario explique comment créer un Cache Redis Azure Premium de 6 Go avec clustering activé et deux partitions.</span><span class="sxs-lookup"><span data-stu-id="0958b-104">In this scenario, you learn how to create a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="0958b-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="0958b-105">Sample script</span></span>

<span data-ttu-id="0958b-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Cache Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="0958b-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="0958b-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="0958b-107">Script explanation</span></span>

<span data-ttu-id="0958b-108">Ce script utilise les commandes suivantes pour créer un groupe de ressources et un Cache Redis Premium avec clustering activé.</span><span class="sxs-lookup"><span data-stu-id="0958b-108">This script uses the following commands to create a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="0958b-109">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="0958b-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0958b-110">Commande</span><span class="sxs-lookup"><span data-stu-id="0958b-110">Command</span></span> | <span data-ttu-id="0958b-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="0958b-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0958b-112">az group create</span><span class="sxs-lookup"><span data-stu-id="0958b-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0958b-113">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="0958b-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0958b-114">az redis create</span><span class="sxs-lookup"><span data-stu-id="0958b-114">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="0958b-115">Créez une instance de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="0958b-115">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0958b-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0958b-116">Next steps</span></span>

<span data-ttu-id="0958b-117">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0958b-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0958b-118">Vous pouvez trouver des exemples supplémentaires de scripts CLI de cache Redis Azure dans la [documentation du cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0958b-118">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>