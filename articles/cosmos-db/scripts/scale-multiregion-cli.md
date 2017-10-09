---
title: "réplication de Script CLI-Multiregion aaaAzure pour la base de données Azure Cosmos | Documents Microsoft"
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
ms.openlocfilehash: e3590303ed3bda9eca1046bf62fff6b61333156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-hello-azure-cli"></a><span data-ttu-id="73110-103">Répliquer un compte de base de données de base de données Azure Cosmos dans plusieurs régions et de configurer les priorités de basculement à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="73110-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using hello Azure CLI</span></span>

<span data-ttu-id="73110-104">Cet exemple réplique tout type de compte de base de données de base de données Azure Cosmos dans plusieurs régions et configure les priorités de basculement à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="73110-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using hello Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="73110-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="73110-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="73110-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="73110-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="73110-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="73110-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="73110-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="73110-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="73110-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="73110-109">Clean up deployment</span></span>

<span data-ttu-id="73110-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="73110-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="73110-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="73110-111">Script explanation</span></span>

<span data-ttu-id="73110-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="73110-112">This script uses hello following commands.</span></span> <span data-ttu-id="73110-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="73110-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="73110-114">Commande</span><span class="sxs-lookup"><span data-stu-id="73110-114">Command</span></span> | <span data-ttu-id="73110-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="73110-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="73110-116">az group create</span><span class="sxs-lookup"><span data-stu-id="73110-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="73110-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="73110-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="73110-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="73110-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="73110-119">Met à jour un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="73110-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="73110-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="73110-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="73110-121">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="73110-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="73110-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73110-122">Next steps</span></span>

<span data-ttu-id="73110-123">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="73110-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="73110-124">Vous trouverez des exemples supplémentaires de script CLI de base de données Azure Cosmos Bonjour [documentation de l’interface CLI de base de données Azure Cosmos](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="73110-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
