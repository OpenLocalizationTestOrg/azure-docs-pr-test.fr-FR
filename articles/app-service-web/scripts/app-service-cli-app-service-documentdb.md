---
title: "Exemple de script Azure CLI - Connecter une application web à une instance Cosmos DB | Microsoft Docs"
description: "Exemple de script Azure CLI - Connecter une application web à une instance Cosmos DB"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="ae992-103">Connecter une application web à Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ae992-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="ae992-104">Dans ce scénario, vous allez apprendre à créer un compte Azure Cosmos DB et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ae992-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="ae992-105">Ensuite, vous allez lier l’instance Cosmos DB à l’application web par le biais des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="ae992-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ae992-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ae992-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ae992-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="ae992-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="ae992-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ae992-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ae992-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ae992-109">Sample script</span></span>

<span data-ttu-id="ae992-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="ae992-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ae992-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ae992-111">Script explanation</span></span>

<span data-ttu-id="ae992-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web, une instance Cosmos DB et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="ae992-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="ae992-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="ae992-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ae992-114">Commande</span><span class="sxs-lookup"><span data-stu-id="ae992-114">Command</span></span> | <span data-ttu-id="ae992-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="ae992-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ae992-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ae992-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ae992-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="ae992-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ae992-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ae992-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ae992-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="ae992-119">Creates an App Service plan.</span></span> <span data-ttu-id="ae992-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ae992-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="ae992-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="ae992-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ae992-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ae992-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ae992-123">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="ae992-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="ae992-124">Crée un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ae992-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="ae992-125">Il s’agit de l’emplacement où les données seront stockées.</span><span class="sxs-lookup"><span data-stu-id="ae992-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="ae992-126">az cosmosdb list-keys</span><span class="sxs-lookup"><span data-stu-id="ae992-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="ae992-127">Liste les clés d’accès au compte Cosmos DB spécifié.</span><span class="sxs-lookup"><span data-stu-id="ae992-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="ae992-128">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="ae992-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="ae992-129">Crée ou met à jour un paramètre d’application pour une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="ae992-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="ae992-130">Les paramètres d’application sont exposés en tant que variables d’environnement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ae992-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae992-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae992-131">Next steps</span></span>

<span data-ttu-id="ae992-132">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae992-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ae992-133">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ae992-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
