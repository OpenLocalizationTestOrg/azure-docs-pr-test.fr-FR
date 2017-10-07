---
title: "aaaAzure exemple de Script CLI - nom d’hôte hello Get, les ports et les clés de Cache Redis Azure | Documents Microsoft"
description: "Exemple de Script CLI Azure - le nom d’hôte de Get hello, les ports et les clés d’une instance de Cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a><span data-ttu-id="b189e-103">Obtenir le nom d’hôte hello, les ports et les clés Azure Redis cache</span><span class="sxs-lookup"><span data-stu-id="b189e-103">Get hello hostname, ports, and keys for Azure Redis Cache</span></span>

<span data-ttu-id="b189e-104">Dans ce scénario, vous découvrez utilisation des clés, les ports et le nom d’hôte de tooretrieve hello instance de Cache Redis Azure tooconnect tooan.</span><span class="sxs-lookup"><span data-stu-id="b189e-104">In this scenario, you learn how tooretrieve hello hostname, ports, and keys used tooconnect tooan Azure Redis Cache instance.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b189e-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b189e-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a><span data-ttu-id="b189e-106">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b189e-106">Script explanation</span></span>

<span data-ttu-id="b189e-107">Ce script utilise hello suivant le nom d’hôte de commandes tooretrieve hello, les clés et les ports d’une instance de Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="b189e-107">This script uses hello following commands tooretrieve hello hostname, keys, and ports of an Azure Redis Cache instance.</span></span> <span data-ttu-id="b189e-108">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b189e-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b189e-109">Commande</span><span class="sxs-lookup"><span data-stu-id="b189e-109">Command</span></span> | <span data-ttu-id="b189e-110">Remarques</span><span class="sxs-lookup"><span data-stu-id="b189e-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b189e-111">az redis show</span><span class="sxs-lookup"><span data-stu-id="b189e-111">az redis show</span></span>](https://docs.microsoft.com/cli/azure/redis#show) | <span data-ttu-id="b189e-112">Récupérer les détails d’une instance du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="b189e-112">Retrieve details of an Azure Redis Cache instance.</span></span> |
| [<span data-ttu-id="b189e-113">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="b189e-113">az redis list-keys</span></span>](https://docs.microsoft.com/cli/azure/redis#list-keys) | <span data-ttu-id="b189e-114">Récupérer les clés d’accès pour une instance du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="b189e-114">Retrieve access keys for an Azure Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b189e-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b189e-115">Next steps</span></span>

<span data-ttu-id="b189e-116">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b189e-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b189e-117">Vous trouverez des exemples supplémentaires de script CLI de Cache Redis Azure Bonjour [documentation du Cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b189e-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
