---
title: "aaaAzure exemple de Script CLI - se connecter à un compte de stockage web application tooa | Documents Microsoft"
description: "Le Script CLI Azure exemple - se connecter à un compte de stockage tooa application web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: affee2d39ef3f98c6043010850e08b67fb9ce54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="d833c-103">Se connecter à un compte de stockage tooa application web</span><span class="sxs-lookup"><span data-stu-id="d833c-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="d833c-104">Dans ce scénario, vous allez apprendre comment toocreate un compte de stockage Azure et Azure web app.</span><span class="sxs-lookup"><span data-stu-id="d833c-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="d833c-105">Ensuite, vous allez lier hello stockage compte toohello web app à l’aide des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="d833c-105">Then you will link hello storage account toohello web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d833c-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d833c-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d833c-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d833c-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d833c-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d833c-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="d833c-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d833c-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d833c-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d833c-110">Script explanation</span></span>

<span data-ttu-id="d833c-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web, compte de stockage et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="d833c-111">This script uses hello following commands toocreate a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="d833c-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="d833c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d833c-113">Commande</span><span class="sxs-lookup"><span data-stu-id="d833c-113">Command</span></span> | <span data-ttu-id="d833c-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="d833c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d833c-115">az group create</span><span class="sxs-lookup"><span data-stu-id="d833c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d833c-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d833c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d833c-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d833c-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d833c-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d833c-118">Creates an App Service plan.</span></span> <span data-ttu-id="d833c-119">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d833c-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="d833c-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d833c-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="d833c-121">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d833c-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="d833c-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="d833c-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="d833c-123">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d833c-123">Creates a storage account.</span></span> <span data-ttu-id="d833c-124">Il s’agit où seront stockés les ressources statiques hello.</span><span class="sxs-lookup"><span data-stu-id="d833c-124">This is where hello static assets will be stored.</span></span> |
| [<span data-ttu-id="d833c-125">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="d833c-125">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="d833c-126">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="d833c-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="d833c-127">Crée ou met à jour un paramètre d’application pour une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="d833c-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="d833c-128">Les paramètres d’application sont exposés en tant que variables d’environnement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d833c-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d833c-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d833c-129">Next steps</span></span>

<span data-ttu-id="d833c-130">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d833c-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d833c-131">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d833c-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
