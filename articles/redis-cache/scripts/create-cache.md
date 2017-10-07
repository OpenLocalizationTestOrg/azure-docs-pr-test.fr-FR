---
title: "aaaAzure exemple de Script CLI - créer un cache Azure Redis Cache | Documents Microsoft"
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
ms.openlocfilehash: 85b007a426fbd4752034ec8663835963d140dd75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-redis-cache"></a><span data-ttu-id="1574a-103">Création d'un cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="1574a-103">Create an Azure Redis Cache</span></span>

<span data-ttu-id="1574a-104">Dans ce scénario, vous découvrez comment toocreate un Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="1574a-104">In this scenario, you learn how toocreate an Azure Redis Cache.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="1574a-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1574a-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-cache/create-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="1574a-106">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1574a-106">Script explanation</span></span>

<span data-ttu-id="1574a-107">Ce script utilise hello suivant de commandes toocreate un groupe de ressources et d’un cache redis.</span><span class="sxs-lookup"><span data-stu-id="1574a-107">This script uses hello following commands toocreate a resource group and a redis cache.</span></span> <span data-ttu-id="1574a-108">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="1574a-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1574a-109">Commande</span><span class="sxs-lookup"><span data-stu-id="1574a-109">Command</span></span> | <span data-ttu-id="1574a-110">Remarques</span><span class="sxs-lookup"><span data-stu-id="1574a-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1574a-111">az group create</span><span class="sxs-lookup"><span data-stu-id="1574a-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1574a-112">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="1574a-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1574a-113">az redis create</span><span class="sxs-lookup"><span data-stu-id="1574a-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="1574a-114">Créez une instance de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1574a-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1574a-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1574a-115">Next steps</span></span>

<span data-ttu-id="1574a-116">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1574a-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1574a-117">Vous trouverez des exemples supplémentaires de script CLI de Cache Redis Azure Bonjour [documentation du Cache Redis Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1574a-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>