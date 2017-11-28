---
title: "Exemple de script Azure CLI - Obtenir les détails d’un cache Redis Azure | Microsoft Docs"
description: "Exemple de script Azure CLI - Obtenir les détails d’un cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 9f4eb32227bd8a68837eabd58b9d058bc4995d17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a><span data-ttu-id="bea1f-103">Obtenir les détails d’un cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="bea1f-103">Get details of an Azure Redis Cache</span></span>

<span data-ttu-id="bea1f-104">Dans ce scénario, vous allez apprendre à récupérer les détails d’une instance de cache Redis Azure, y compris son état d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="bea1f-104">In this scenario, you learn how to retrieve the details of an Azure Redis Cache instance, including its provisioning status.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="bea1f-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="bea1f-105">Sample script</span></span>

<span data-ttu-id="bea1f-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Cache Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="bea1f-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="bea1f-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="bea1f-107">Script explanation</span></span>

<span data-ttu-id="bea1f-108">Ce script utilise les commandes suivantes pour récupérer les détails d’une instance du cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="bea1f-108">This script uses the following commands to retrieve the details of an Azure Redis Cache instance.</span></span> <span data-ttu-id="bea1f-109">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="bea1f-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bea1f-110">Commande</span><span class="sxs-lookup"><span data-stu-id="bea1f-110">Command</span></span> | <span data-ttu-id="bea1f-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="bea1f-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bea1f-112">az redis show</span><span class="sxs-lookup"><span data-stu-id="bea1f-112">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="bea1f-113">Récupérer les détails d’une instance du cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="bea1f-113">Retrieve details of an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="bea1f-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bea1f-114">Next steps</span></span>

<span data-ttu-id="bea1f-115">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bea1f-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bea1f-116">Vous pouvez trouver des exemples supplémentaires de scripts CLI de cache Redis Azure dans la [documentation du cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bea1f-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>