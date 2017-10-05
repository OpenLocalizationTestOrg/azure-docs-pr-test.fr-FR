---
title: "Exemple de script Azure CLI - Connecter une application web à une instance SQL Database | Microsoft Docs"
description: "Exemple de script Azure CLI - Connecter une application web à une instance SQL Database"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="e9ce4-103">Connecter une application web à une instance SQL Database</span><span class="sxs-lookup"><span data-stu-id="e9ce4-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="e9ce4-104">Dans ce scénario, vous allez apprendre à créer une instance Azure SQL Database et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="e9ce4-105">Ensuite, vous allez lier l’instance SQL Database à l’application web par le biais des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e9ce4-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e9ce4-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="e9ce4-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e9ce4-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e9ce4-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e9ce4-109">Sample script</span></span>

<span data-ttu-id="e9ce4-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="e9ce4-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e9ce4-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e9ce4-111">Script explanation</span></span>

<span data-ttu-id="e9ce4-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web, une instance SQL Database et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="e9ce4-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e9ce4-114">Commande</span><span class="sxs-lookup"><span data-stu-id="e9ce4-114">Command</span></span> | <span data-ttu-id="e9ce4-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="e9ce4-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9ce4-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e9ce4-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e9ce4-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e9ce4-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e9ce4-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e9ce4-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-119">Creates an App Service plan.</span></span> <span data-ttu-id="e9ce4-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="e9ce4-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="e9ce4-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="e9ce4-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e9ce4-123">az sql server create</span><span class="sxs-lookup"><span data-stu-id="e9ce4-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="e9ce4-124">Crée un serveur SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="e9ce4-125">az sql db create</span><span class="sxs-lookup"><span data-stu-id="e9ce4-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="e9ce4-126">Crée une base de données avec le serveur SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="e9ce4-127">az webapp config appsettings set</span><span class="sxs-lookup"><span data-stu-id="e9ce4-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="e9ce4-128">Crée ou met à jour un paramètre d’application pour une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="e9ce4-129">Les paramètres d’application sont exposés en tant que variables d’environnement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="e9ce4-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9ce4-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9ce4-130">Next steps</span></span>

<span data-ttu-id="e9ce4-131">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9ce4-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e9ce4-132">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e9ce4-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
