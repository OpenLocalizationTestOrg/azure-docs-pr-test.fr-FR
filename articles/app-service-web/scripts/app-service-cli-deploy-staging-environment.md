---
title: "aaaAzure exemple de Script CLI - créer une application web et déployer tooa code environnement intermédiaire | Documents Microsoft"
description: "Exemple de Script CLI Azure - créer une application web et déployer tooa code environnement intermédiaire"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="ac9c2-103">Créer une application web et de déployer tooa code environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="ac9c2-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="ac9c2-104">Cet exemple de script crée une application web dans le Service d’applications avec un emplacement de déploiement supplémentaire appelé « étape intermédiaire », puis déploie un toohello d’application exemple emplacement « intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="ac9c2-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ac9c2-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ac9c2-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ac9c2-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ac9c2-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ac9c2-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ac9c2-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ac9c2-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ac9c2-109">Script explanation</span></span>

<span data-ttu-id="ac9c2-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-110">This script uses hello following commands.</span></span> <span data-ttu-id="ac9c2-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ac9c2-112">Commande</span><span class="sxs-lookup"><span data-stu-id="ac9c2-112">Command</span></span> | <span data-ttu-id="ac9c2-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="ac9c2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac9c2-114">az group create</span><span class="sxs-lookup"><span data-stu-id="ac9c2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ac9c2-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ac9c2-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ac9c2-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ac9c2-117">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ac9c2-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ac9c2-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ac9c2-119">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ac9c2-120">az webapp deployment slot create</span><span class="sxs-lookup"><span data-stu-id="ac9c2-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="ac9c2-121">Crée un emplacement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="ac9c2-122">az webapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="ac9c2-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="ac9c2-123">Associe une application web Azure à un référentiel Git ou Mercurial.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="ac9c2-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="ac9c2-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ac9c2-125">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="ac9c2-126">az webapp deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="ac9c2-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="ac9c2-127">Bascule un déploiement spécifié en production.</span><span class="sxs-lookup"><span data-stu-id="ac9c2-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac9c2-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac9c2-128">Next steps</span></span>

<span data-ttu-id="ac9c2-129">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac9c2-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ac9c2-130">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ac9c2-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
