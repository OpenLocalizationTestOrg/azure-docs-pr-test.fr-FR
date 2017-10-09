---
title: "aaaAzure exemple de Script CLI - mise à l’échelle une application web dans le monde entier avec une architecture haute-disponibilité | Documents Microsoft"
description: "Exemple de script Azure CLI - Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="336f0-103">Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="336f0-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="336f0-104">Dans ce scénario, vous créez un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="336f0-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="336f0-105">Une fois terminée l’exercice de hello avoir une disponibilité architecture qui permet de fournit une disponibilité globale de votre application web en fonction de la latence réseau la plus faible de hello.</span><span class="sxs-lookup"><span data-stu-id="336f0-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="336f0-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="336f0-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="336f0-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="336f0-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="336f0-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="336f0-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="336f0-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="336f0-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="336f0-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="336f0-110">Script explanation</span></span>

<span data-ttu-id="336f0-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web, le profil traffic manager, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="336f0-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="336f0-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="336f0-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="336f0-113">Commande</span><span class="sxs-lookup"><span data-stu-id="336f0-113">Command</span></span> | <span data-ttu-id="336f0-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="336f0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="336f0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="336f0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="336f0-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="336f0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="336f0-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="336f0-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="336f0-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="336f0-118">Creates an App Service plan.</span></span> <span data-ttu-id="336f0-119">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="336f0-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="336f0-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="336f0-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="336f0-121">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="336f0-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="336f0-122">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="336f0-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="336f0-123">Crée un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="336f0-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="336f0-124">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="336f0-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="336f0-125">Ajoute un point de terminaison de tooan profil Traffic Manager de Azure.</span><span class="sxs-lookup"><span data-stu-id="336f0-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="336f0-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="336f0-126">Next steps</span></span>

<span data-ttu-id="336f0-127">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="336f0-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="336f0-128">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="336f0-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
