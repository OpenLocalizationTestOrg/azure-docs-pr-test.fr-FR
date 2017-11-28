---
title: "aaaAzure exemple de Script CLI - créer une application web et déployer le code à partir d’un référentiel Git local | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une application web et déployer du code à partir d’un référentiel Git local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="c9112-103">Créer une application web et déployer du code à partir d’un référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="c9112-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="c9112-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web dans un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="c9112-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c9112-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c9112-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c9112-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c9112-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c9112-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c9112-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c9112-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c9112-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c9112-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c9112-109">Script explanation</span></span>

<span data-ttu-id="c9112-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="c9112-110">This script uses hello following commands.</span></span> <span data-ttu-id="c9112-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c9112-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c9112-112">Commande</span><span class="sxs-lookup"><span data-stu-id="c9112-112">Command</span></span> | <span data-ttu-id="c9112-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="c9112-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9112-114">az group create</span><span class="sxs-lookup"><span data-stu-id="c9112-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c9112-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c9112-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9112-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c9112-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c9112-117">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="c9112-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c9112-118">az webapp create</span><span class="sxs-lookup"><span data-stu-id="c9112-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="c9112-119">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="c9112-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c9112-120">az webapp deployment user set</span><span class="sxs-lookup"><span data-stu-id="c9112-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="c9112-121">Définit les informations d’identification du déploiement au niveau du compte de hello pour le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="c9112-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="c9112-122">az webapp deployment source config-local-git</span><span class="sxs-lookup"><span data-stu-id="c9112-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="c9112-123">Crée une configuration de contrôle source pour un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="c9112-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="c9112-124">az webapp browse</span><span class="sxs-lookup"><span data-stu-id="c9112-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="c9112-125">Ouvre une application web Azure dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="c9112-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9112-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9112-126">Next steps</span></span>

<span data-ttu-id="c9112-127">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9112-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c9112-128">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c9112-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
