---
title: Exemple de script Azure CLI - Supprimer un Cache Redis Azure | Microsoft Docs
description: Exemple de script Azure CLI - Supprimer un Cache Redis Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: f959823b3a7c5b0262f693ecad1e6efc4eec4f35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-an-azure-redis-cache"></a><span data-ttu-id="a2dcd-103">Supprimer un Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="a2dcd-103">Delete an Azure Redis Cache</span></span>

<span data-ttu-id="a2dcd-104">Dans ce scénario, vous apprenez comment supprimer un Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-104">In this scenario, you learn how to delete an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="a2dcd-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a2dcd-105">Sample script</span></span>

<span data-ttu-id="a2dcd-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Cache Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="a2dcd-106">[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a2dcd-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a2dcd-107">Script explanation</span></span>

<span data-ttu-id="a2dcd-108">Ce script utilise les commandes suivantes pour supprimer une instance du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-108">This script uses the following commands to delete an Azure Redis Cache instance.</span></span> <span data-ttu-id="a2dcd-109">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a2dcd-110">Commande</span><span class="sxs-lookup"><span data-stu-id="a2dcd-110">Command</span></span> | <span data-ttu-id="a2dcd-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="a2dcd-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2dcd-112">az redis delete</span><span class="sxs-lookup"><span data-stu-id="a2dcd-112">az redis delete</span></span>](https://docs.microsoft.com/cli/azure/redis#delete) | <span data-ttu-id="a2dcd-113">Supprimez une instance de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="a2dcd-113">Delete Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a2dcd-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2dcd-114">Next steps</span></span>

<span data-ttu-id="a2dcd-115">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2dcd-115">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a2dcd-116">Vous pouvez trouver des exemples supplémentaires de scripts CLI de cache Redis Azure dans la [documentation du cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2dcd-116">Additional Azure Redis Cache CLI script samples can be found in the [Azure Redis Cache documentation](../cli-samples.md).</span></span>