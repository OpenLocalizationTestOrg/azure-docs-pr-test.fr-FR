---
title: "aaaAzure CLI Script-permet de créer un compte, une base de données et une collection Azure Cosmos DB DocumentDB API | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une collection, une base de données et un compte d’API DocumentDB Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/06/2017
ms.author: mimig
ms.openlocfilehash: 53919a849e04fa69680219e51c0289b9f2affe07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="e9a93-103">Azure Cosmos DB : Créer un compte d’API DocumentDB avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e9a93-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="e9a93-104">Cet exemple de script CLI crée une collection, une base de données et un compte d’API DocumentDB Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e9a93-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e9a93-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e9a93-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e9a93-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="e9a93-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e9a93-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e9a93-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e9a93-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e9a93-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e9a93-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="e9a93-109">Clean up deployment</span></span>

<span data-ttu-id="e9a93-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e9a93-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e9a93-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e9a93-111">Script explanation</span></span>

<span data-ttu-id="e9a93-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="e9a93-112">This script uses hello following commands.</span></span> <span data-ttu-id="e9a93-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e9a93-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e9a93-114">Commande</span><span class="sxs-lookup"><span data-stu-id="e9a93-114">Command</span></span> | <span data-ttu-id="e9a93-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="e9a93-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9a93-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e9a93-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e9a93-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e9a93-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e9a93-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="e9a93-118">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="e9a93-119">Crée un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e9a93-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="e9a93-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="e9a93-120">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="e9a93-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="e9a93-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9a93-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9a93-122">Next steps</span></span>

<span data-ttu-id="e9a93-123">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9a93-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e9a93-124">Vous trouverez des exemples supplémentaires de script CLI de base de données Azure Cosmos Bonjour [documentation de l’interface CLI de base de données Azure Cosmos](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e9a93-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
