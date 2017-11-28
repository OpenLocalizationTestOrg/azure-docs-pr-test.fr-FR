---
title: "Script CLI Azure - Réplication multirégion Azure Cosmos DB | Microsoft Docs"
description: "Exemple de script CLI Azure - Réplication multirégion Azure Cosmos DB"
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
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: ab716c28b88412438d0cea80377f9f0f40dc8bd6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-the-azure-cli"></a><span data-ttu-id="40945-103">Répliquer un compte de base de données Azure Cosmos DB dans plusieurs régions et configurer les priorités de basculement avec la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="40945-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using the Azure CLI</span></span>

<span data-ttu-id="40945-104">Cet exemple réplique tout type de compte de base de données Azure Cosmos DB dans plusieurs régions et configure les priorités de basculement à l’aide de la CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="40945-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using the Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="40945-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="40945-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="40945-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="40945-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="40945-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="40945-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="40945-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="40945-108">Sample script</span></span>

<span data-ttu-id="40945-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Mettre à l’échelle Azure Cosmos DB dans plusieurs régions")]</span><span class="sxs-lookup"><span data-stu-id="40945-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="40945-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="40945-110">Clean up deployment</span></span>

<span data-ttu-id="40945-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="40945-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="40945-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="40945-112">Script explanation</span></span>

<span data-ttu-id="40945-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="40945-113">This script uses the following commands.</span></span> <span data-ttu-id="40945-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="40945-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="40945-115">Commande</span><span class="sxs-lookup"><span data-stu-id="40945-115">Command</span></span> | <span data-ttu-id="40945-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="40945-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="40945-117">az group create</span><span class="sxs-lookup"><span data-stu-id="40945-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="40945-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="40945-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="40945-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="40945-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="40945-120">Met à jour un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40945-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="40945-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="40945-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="40945-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="40945-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="40945-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40945-123">Next steps</span></span>

<span data-ttu-id="40945-124">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="40945-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="40945-125">Vous trouverez des exemples supplémentaires de scripts CLI d’Azure Cosmos DB dans la [documentation d’Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="40945-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
