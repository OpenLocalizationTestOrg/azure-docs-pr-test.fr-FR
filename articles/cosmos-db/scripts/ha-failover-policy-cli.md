---
title: "aaaAzure CLI créer Script une stratégie de basculement pour une haute disponibilité | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une stratégie de basculement pour une haute disponibilité"
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
ms.openlocfilehash: 9076f4ef23fceb4208c934c57ac6899f0b58ffd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-hello-azure-cli"></a><span data-ttu-id="2f804-103">Créer une stratégie de basculement pour une haute disponibilité à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="2f804-103">Create a failover policy for high availability using hello Azure CLI</span></span>

<span data-ttu-id="2f804-104">Cet exemple de script CLI crée un compte Azure Cosmos DB, puis le configure pour la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2f804-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2f804-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2f804-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2f804-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="2f804-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2f804-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f804-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2f804-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="2f804-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2f804-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="2f804-109">Clean up deployment</span></span>

<span data-ttu-id="2f804-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="2f804-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2f804-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="2f804-111">Script explanation</span></span>

<span data-ttu-id="2f804-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="2f804-112">This script uses hello following commands.</span></span> <span data-ttu-id="2f804-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="2f804-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2f804-114">Commande</span><span class="sxs-lookup"><span data-stu-id="2f804-114">Command</span></span> | <span data-ttu-id="2f804-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="2f804-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2f804-116">az group create</span><span class="sxs-lookup"><span data-stu-id="2f804-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2f804-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="2f804-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2f804-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="2f804-118">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="2f804-119">Crée un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f804-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2f804-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="2f804-120">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="2f804-121">Met à jour un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f804-121">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2f804-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="2f804-122">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="2f804-123">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="2f804-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2f804-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f804-124">Next steps</span></span>

<span data-ttu-id="2f804-125">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f804-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2f804-126">Vous trouverez des exemples supplémentaires de script CLI de base de données Azure Cosmos Bonjour [documentation de l’interface CLI de base de données Azure Cosmos](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2f804-126">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
