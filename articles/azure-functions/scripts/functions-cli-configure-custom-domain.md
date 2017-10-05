---
title: "Exemple de script Azure CLI - Mapper un domaine personnalisé à une Function App | Microsoft Docs"
description: "Exemple de script Azure CLI - Mapper un domaine personnalisé à une Function App dans Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="9fb44-103">Mapper un domaine personnalisé à une Function App</span><span class="sxs-lookup"><span data-stu-id="9fb44-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="9fb44-104">Cet exemple de script crée une Function App avec les ressources associées, puis la mappe à `www.<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="9fb44-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="9fb44-105">Pour mapper un domaine personnalisé, votre Function App doit être créée dans un plan App Service et non dans un plan de consommation.</span><span class="sxs-lookup"><span data-stu-id="9fb44-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="9fb44-106">Azure Functions ne prend en charge le mappage d’un domaine personnalisé qu’avec un enregistrement A.</span><span class="sxs-lookup"><span data-stu-id="9fb44-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9fb44-107">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9fb44-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9fb44-108">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="9fb44-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="9fb44-109">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9fb44-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="9fb44-110">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="9fb44-110">Sample script</span></span>

<span data-ttu-id="9fb44-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Mapper un domaine personnalisé à une Function App")]</span><span class="sxs-lookup"><span data-stu-id="9fb44-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9fb44-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="9fb44-112">Script explanation</span></span>

<span data-ttu-id="9fb44-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="9fb44-113">This script uses the following commands.</span></span> <span data-ttu-id="9fb44-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="9fb44-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9fb44-115">Commande</span><span class="sxs-lookup"><span data-stu-id="9fb44-115">Command</span></span> | <span data-ttu-id="9fb44-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="9fb44-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9fb44-117">az group create</span><span class="sxs-lookup"><span data-stu-id="9fb44-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9fb44-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="9fb44-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9fb44-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="9fb44-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="9fb44-120">Crée un compte de stockage requis par la Function App.</span><span class="sxs-lookup"><span data-stu-id="9fb44-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="9fb44-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9fb44-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9fb44-122">Crée un plan App Service requis pour mapper un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="9fb44-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="9fb44-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="9fb44-123">az functionapp create</span></span>]() | <span data-ttu-id="9fb44-124">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="9fb44-124">Creates a function app.</span></span> |
| [<span data-ttu-id="9fb44-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="9fb44-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="9fb44-126">Mappe un domaine personnalisé à une Function App.</span><span class="sxs-lookup"><span data-stu-id="9fb44-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9fb44-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fb44-127">Next steps</span></span>

<span data-ttu-id="9fb44-128">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9fb44-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9fb44-129">Vous trouverez des exemples supplémentaires de scripts CLI Functions dans la [documentation d’Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="9fb44-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
