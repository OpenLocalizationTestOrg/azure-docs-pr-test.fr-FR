---
title: "Script Azure CLI - Créer un pare-feu pour Azure Cosmos DB | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer un pare-feu pour Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: 51f61901e1b1615e48582690dea701a01a56ebca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-the-azure-cli"></a><span data-ttu-id="ee41a-103">Azure Cosmos DB : Créer un pare-feu à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ee41a-103">Azure Cosmos DB: Create a firewall using the Azure CLI</span></span>

<span data-ttu-id="ee41a-104">Cet exemple de script CLI crée une stratégie de pare-feu pour tous types de comptes Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee41a-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ee41a-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ee41a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ee41a-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="ee41a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ee41a-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ee41a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ee41a-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ee41a-108">Sample script</span></span>

<span data-ttu-id="ee41a-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Créer un pare-feu Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="ee41a-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ee41a-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="ee41a-110">Clean up deployment</span></span>

<span data-ttu-id="ee41a-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="ee41a-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ee41a-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ee41a-112">Script explanation</span></span>

<span data-ttu-id="ee41a-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ee41a-113">This script uses the following commands.</span></span> <span data-ttu-id="ee41a-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="ee41a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ee41a-115">Commande</span><span class="sxs-lookup"><span data-stu-id="ee41a-115">Command</span></span> | <span data-ttu-id="ee41a-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="ee41a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ee41a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="ee41a-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ee41a-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="ee41a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ee41a-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="ee41a-119">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#create) | <span data-ttu-id="ee41a-120">Crée un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee41a-120">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="ee41a-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="ee41a-121">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="ee41a-122">Met à jour un compte Azure Cosmos DB pour inclure les paramètres de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ee41a-122">Updates an Azure CosmosDB account to include firewall settings.</span></span> |
| [<span data-ttu-id="ee41a-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="ee41a-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="ee41a-124">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="ee41a-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ee41a-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee41a-125">Next steps</span></span>

<span data-ttu-id="ee41a-126">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ee41a-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ee41a-127">Vous trouverez des exemples supplémentaires de scripts CLI d’Azure Cosmos DB dans la [documentation d’Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ee41a-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
