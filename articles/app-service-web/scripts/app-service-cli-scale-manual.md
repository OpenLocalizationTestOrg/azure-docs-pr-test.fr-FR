---
title: "Exemple de script Azure CLI - Mettre manuellement à l’échelle une application web à l’aide d’Azure CLI 2.0 | Microsoft Docs"
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
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="d1c19-103">Mettre manuellement à l’échelle une application web</span><span class="sxs-lookup"><span data-stu-id="d1c19-103">Scale a web app manually</span></span>

<span data-ttu-id="d1c19-104">Dans ce scénario, vous allez apprendre à créer un groupe de ressources, un plan App Service et une application web.</span><span class="sxs-lookup"><span data-stu-id="d1c19-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="d1c19-105">Vous ferez ensuite évoluer le plan App Service d’une instance unique à plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="d1c19-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d1c19-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d1c19-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d1c19-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="d1c19-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="d1c19-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d1c19-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d1c19-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d1c19-109">Sample script</span></span>

<span data-ttu-id="d1c19-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Mise à l’échelle manuelle")]</span><span class="sxs-lookup"><span data-stu-id="d1c19-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d1c19-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d1c19-111">Script explanation</span></span>

<span data-ttu-id="d1c19-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d1c19-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="d1c19-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d1c19-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d1c19-114">Commande</span><span class="sxs-lookup"><span data-stu-id="d1c19-114">Command</span></span> | <span data-ttu-id="d1c19-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="d1c19-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1c19-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d1c19-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d1c19-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d1c19-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1c19-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d1c19-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d1c19-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d1c19-119">Creates an App Service plan.</span></span> <span data-ttu-id="d1c19-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c19-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="d1c19-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d1c19-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d1c19-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c19-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d1c19-123">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="d1c19-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="d1c19-124">Met à jour les propriétés du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d1c19-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d1c19-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1c19-125">Next steps</span></span>

<span data-ttu-id="d1c19-126">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1c19-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d1c19-127">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d1c19-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
