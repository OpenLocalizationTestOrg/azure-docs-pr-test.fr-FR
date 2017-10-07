---
title: "aaaAzure exemple de Script CLI - créer un Cache de Redis Azure Premium avec clustering | Documents Microsoft"
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
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="e6775-103">Créer un Cache Redis Azure Premium avec clustering</span><span class="sxs-lookup"><span data-stu-id="e6775-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="e6775-104">Dans ce scénario, vous découvrez comment toocreate activé un niveau Premium de 6 Go du Cache Redis Azure avec le clustering et deux partitions.</span><span class="sxs-lookup"><span data-stu-id="e6775-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="e6775-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e6775-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e6775-106">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e6775-106">Script explanation</span></span>

<span data-ttu-id="e6775-107">Ce script utilise hello suivant de commandes toocreate un groupe de ressources et d’un cache redis de niveau Premium avec activation des clusters.</span><span class="sxs-lookup"><span data-stu-id="e6775-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="e6775-108">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e6775-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e6775-109">Commande</span><span class="sxs-lookup"><span data-stu-id="e6775-109">Command</span></span> | <span data-ttu-id="e6775-110">Remarques</span><span class="sxs-lookup"><span data-stu-id="e6775-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e6775-111">az group create</span><span class="sxs-lookup"><span data-stu-id="e6775-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e6775-112">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e6775-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e6775-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="e6775-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="e6775-114">Créez une instance de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="e6775-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e6775-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6775-115">Next steps</span></span>

<span data-ttu-id="e6775-116">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e6775-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e6775-117">Vous trouverez des exemples supplémentaires de script CLI de Cache Redis Azure Bonjour [documentation du Cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e6775-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
