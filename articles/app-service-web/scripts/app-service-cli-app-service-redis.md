---
title: "aaaAzure exemple de Script CLI - se connecter à un cache de redis web application tooa | Documents Microsoft"
description: "Le Script CLI Azure exemple - se connecter à un cache de redis tooa web app"
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="e6b2f-103">Se connecter à un cache de redis tooa web app</span><span class="sxs-lookup"><span data-stu-id="e6b2f-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="e6b2f-104">Dans ce scénario, vous allez apprendre comment toocreate Azure redis cache et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="e6b2f-105">Ensuite, vous allez lier hello redis cache toohello l’application web à l’aide des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e6b2f-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e6b2f-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e6b2f-107">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e6b2f-107">Script explanation</span></span>

<span data-ttu-id="e6b2f-108">Ce script utilise hello suivant les commandes toocreate un groupe de ressources, l’application web, redis cache et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="e6b2f-109">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e6b2f-110">Commande</span><span class="sxs-lookup"><span data-stu-id="e6b2f-110">Command</span></span> | <span data-ttu-id="e6b2f-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="e6b2f-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e6b2f-112">az group create</span><span class="sxs-lookup"><span data-stu-id="e6b2f-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e6b2f-113">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e6b2f-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e6b2f-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e6b2f-115">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-115">Creates an App Service plan.</span></span> <span data-ttu-id="e6b2f-116">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e6b2f-117">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e6b2f-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e6b2f-118">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e6b2f-119">az redis create</span><span class="sxs-lookup"><span data-stu-id="e6b2f-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="e6b2f-120">Crée une nouvelle instance de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="e6b2f-121">Cela consiste à stocker des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="e6b2f-122">az redis list-keys</span><span class="sxs-lookup"><span data-stu-id="e6b2f-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="e6b2f-123">Répertorie les touches d’accès hello pour l’instance de cache redis hello.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="e6b2f-124">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="e6b2f-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="e6b2f-125">Crée ou met à jour un paramètre d’application pour une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="e6b2f-126">Les paramètres d’application sont exposés en tant que variables d’environnement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="e6b2f-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e6b2f-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6b2f-127">Next steps</span></span>

<span data-ttu-id="e6b2f-128">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e6b2f-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e6b2f-129">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e6b2f-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
