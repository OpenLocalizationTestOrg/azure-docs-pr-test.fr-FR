---
title: "aaaAzure exemple de Script CLI - mapper une domaine personnalisé l’application web tooa | Documents Microsoft"
description: "Exemple de Script CLI Azure - mappage d’une application web de tooa domaine personnalisé"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="d3144-103">Mapper une domaine personnalisé tooa l’application web</span><span class="sxs-lookup"><span data-stu-id="d3144-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="d3144-104">Cet exemple de script crée une application web dans le Service d’applications avec ses ressources connexes et mappe ensuite `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="d3144-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d3144-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d3144-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d3144-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d3144-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d3144-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d3144-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d3144-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d3144-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d3144-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d3144-109">Script explanation</span></span>

<span data-ttu-id="d3144-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="d3144-110">This script uses hello following commands.</span></span> <span data-ttu-id="d3144-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="d3144-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d3144-112">Commande</span><span class="sxs-lookup"><span data-stu-id="d3144-112">Command</span></span> | <span data-ttu-id="d3144-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="d3144-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d3144-114">az group create</span><span class="sxs-lookup"><span data-stu-id="d3144-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d3144-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d3144-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d3144-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d3144-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d3144-117">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d3144-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d3144-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d3144-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d3144-119">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d3144-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d3144-120">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="d3144-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="d3144-121">Mappe une domaine personnalisé tooa l’application web.</span><span class="sxs-lookup"><span data-stu-id="d3144-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d3144-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3144-122">Next steps</span></span>

<span data-ttu-id="d3144-123">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3144-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d3144-124">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d3144-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
