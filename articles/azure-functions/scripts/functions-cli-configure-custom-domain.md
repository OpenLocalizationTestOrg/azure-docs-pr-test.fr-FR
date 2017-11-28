---
title: "aaaAzure exemple de Script CLI - mapper à une application de fonction de domaine personnalisé tooa | Documents Microsoft"
description: "Exemple de Script Azure CLI - la carte, une application de fonction tooa domaine personnalisé dans Azure."
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
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="63057-103">Mapper une application de fonction tooa domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="63057-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="63057-104">Cet exemple de script crée une application de fonction avec les ressources associées et mappe ensuite `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="63057-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="63057-105">domaine personnalisé de tooa toomap, votre application de la fonction doit être créée dans un plan App Service et non dans un plan de la consommation.</span><span class="sxs-lookup"><span data-stu-id="63057-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="63057-106">Azure Functions ne prend en charge le mappage d’un domaine personnalisé qu’avec un enregistrement A.</span><span class="sxs-lookup"><span data-stu-id="63057-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="63057-107">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="63057-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="63057-108">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="63057-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="63057-109">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="63057-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="63057-110">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="63057-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="63057-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="63057-111">Script explanation</span></span>

<span data-ttu-id="63057-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="63057-112">This script uses hello following commands.</span></span> <span data-ttu-id="63057-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="63057-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="63057-114">Commande</span><span class="sxs-lookup"><span data-stu-id="63057-114">Command</span></span> | <span data-ttu-id="63057-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="63057-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="63057-116">az group create</span><span class="sxs-lookup"><span data-stu-id="63057-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="63057-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="63057-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="63057-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="63057-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="63057-119">Crée un compte de stockage requis par l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="63057-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="63057-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="63057-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="63057-121">Crée un toomap de plan requises du Service d’applications à un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="63057-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="63057-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="63057-122">az functionapp create</span></span>]() | <span data-ttu-id="63057-123">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="63057-123">Creates a function app.</span></span> |
| [<span data-ttu-id="63057-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="63057-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="63057-125">Mappe une application de fonction tooa domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="63057-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="63057-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63057-126">Next steps</span></span>

<span data-ttu-id="63057-127">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63057-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="63057-128">Vous trouverez des exemples de script CLI des fonctions supplémentaires Bonjour [documentation Azure fonctions]().</span><span class="sxs-lookup"><span data-stu-id="63057-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
