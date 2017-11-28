---
title: "Script Azure CLI - Créer une collection, une base de données et un compte d’API DocumentDB Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: 28f99d56404e47adcd375d9f3106cc234469cbfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-an-documentdb-api-account-using-cli"></a><span data-ttu-id="c5549-103">Azure Cosmos DB : Créer un compte d’API DocumentDB avec l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="c5549-103">Azure Cosmos DB: Create an DocumentDB API account using CLI</span></span>

<span data-ttu-id="c5549-104">Cet exemple de script CLI crée une collection, une base de données et un compte d’API DocumentDB Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c5549-104">This sample CLI script creates an Azure Cosmos DB DocumentDB API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c5549-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c5549-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c5549-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="c5549-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c5549-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c5549-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c5549-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c5549-108">Sample script</span></span>

<span data-ttu-id="c5549-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Créer une collection, une base de données et un compte d’API DocumentDB Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="c5549-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB DocumentDB API account, database, and collection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c5549-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c5549-110">Clean up deployment</span></span>

<span data-ttu-id="c5549-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c5549-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c5549-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c5549-112">Script explanation</span></span>

<span data-ttu-id="c5549-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="c5549-113">This script uses the following commands.</span></span> <span data-ttu-id="c5549-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="c5549-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c5549-115">Commande</span><span class="sxs-lookup"><span data-stu-id="c5549-115">Command</span></span> | <span data-ttu-id="c5549-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="c5549-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c5549-117">az group create</span><span class="sxs-lookup"><span data-stu-id="c5549-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c5549-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c5549-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c5549-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="c5549-119">az cosmosdb create</span></span>](/cli/azure/cosmosdb#create) | <span data-ttu-id="c5549-120">Crée un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c5549-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="c5549-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="c5549-121">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="c5549-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c5549-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c5549-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5549-123">Next steps</span></span>

<span data-ttu-id="c5549-124">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5549-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c5549-125">Vous trouverez des exemples supplémentaires de scripts CLI d’Azure Cosmos DB dans la [documentation d’Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c5549-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
