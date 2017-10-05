---
title: "Exemple de script Azure CLI - Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité | Microsoft Docs"
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
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="51f30-103">Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="51f30-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="51f30-104">Dans ce scénario, vous créez un groupe de ressources, deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="51f30-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="51f30-105">Une fois cette procédure terminée, vous bénéficiez d’une architecture haute disponibilité qui offre une disponibilité globale de votre application web en fonction de la plus faible latence réseau.</span><span class="sxs-lookup"><span data-stu-id="51f30-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="51f30-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="51f30-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="51f30-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="51f30-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="51f30-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="51f30-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="51f30-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="51f30-109">Sample script</span></span>

<span data-ttu-id="51f30-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Échelle géographique")]</span><span class="sxs-lookup"><span data-stu-id="51f30-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="51f30-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="51f30-111">Script explanation</span></span>

<span data-ttu-id="51f30-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web, un profil Traffic Manager et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="51f30-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="51f30-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="51f30-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="51f30-114">Commande</span><span class="sxs-lookup"><span data-stu-id="51f30-114">Command</span></span> | <span data-ttu-id="51f30-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="51f30-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="51f30-116">az group create</span><span class="sxs-lookup"><span data-stu-id="51f30-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="51f30-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="51f30-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="51f30-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="51f30-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="51f30-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="51f30-119">Creates an App Service plan.</span></span> <span data-ttu-id="51f30-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="51f30-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="51f30-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="51f30-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="51f30-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="51f30-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="51f30-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="51f30-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="51f30-124">Crée un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="51f30-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="51f30-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="51f30-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="51f30-126">Ajoute un point de terminaison à un profil Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="51f30-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="51f30-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51f30-127">Next steps</span></span>

<span data-ttu-id="51f30-128">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51f30-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="51f30-129">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="51f30-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
