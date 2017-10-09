---
title: "aaaAzure exemple de Script CLI - mise à l’échelle une application Web manuellement à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Exemple de script Azure CLI - Mettre manuellement à l’échelle une application web à l’aide d’Azure CLI 2.0"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="72ce6-103">Mettre manuellement à l’échelle une application web</span><span class="sxs-lookup"><span data-stu-id="72ce6-103">Scale a web app manually</span></span>

<span data-ttu-id="72ce6-104">Dans ce scénario, vous allez apprendre toocreate un groupe de ressources, application de service web et le plan d’applications.</span><span class="sxs-lookup"><span data-stu-id="72ce6-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="72ce6-105">Vous allez ensuite échelonner hello du Plan App Service à partir d’une instance de toomultiple d’instance unique.</span><span class="sxs-lookup"><span data-stu-id="72ce6-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="72ce6-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="72ce6-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="72ce6-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="72ce6-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="72ce6-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72ce6-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="72ce6-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="72ce6-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="72ce6-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="72ce6-110">Script explanation</span></span>

<span data-ttu-id="72ce6-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="72ce6-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="72ce6-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="72ce6-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="72ce6-113">Commande</span><span class="sxs-lookup"><span data-stu-id="72ce6-113">Command</span></span> | <span data-ttu-id="72ce6-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="72ce6-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="72ce6-115">az group create</span><span class="sxs-lookup"><span data-stu-id="72ce6-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="72ce6-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="72ce6-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="72ce6-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="72ce6-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="72ce6-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="72ce6-118">Creates an App Service plan.</span></span> <span data-ttu-id="72ce6-119">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="72ce6-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="72ce6-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="72ce6-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="72ce6-121">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="72ce6-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="72ce6-122">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="72ce6-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="72ce6-123">Met à jour les propriétés de hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="72ce6-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="72ce6-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72ce6-124">Next steps</span></span>

<span data-ttu-id="72ce6-125">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72ce6-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="72ce6-126">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="72ce6-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
