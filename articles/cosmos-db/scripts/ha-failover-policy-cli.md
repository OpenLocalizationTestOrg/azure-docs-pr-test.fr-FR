---
title: "Exemple de script Azure CLI - Créer une stratégie de basculement pour une haute disponibilité | Microsoft Docs"
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
ms.openlocfilehash: 96083d66cc1a2ef179f9313c1b3ed04162c1c048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="057ee-103">Créer une stratégie de basculement pour une haute disponibilité à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="057ee-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="057ee-104">Cet exemple de script CLI crée un compte Azure Cosmos DB, puis le configure pour la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="057ee-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="057ee-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="057ee-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="057ee-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="057ee-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="057ee-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="057ee-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="057ee-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="057ee-108">Sample script</span></span>

<span data-ttu-id="057ee-109">[!code-azurecli-interactive[principal](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Créer une stratégie de basculement Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="057ee-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="057ee-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="057ee-110">Clean up deployment</span></span>

<span data-ttu-id="057ee-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="057ee-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="057ee-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="057ee-112">Script explanation</span></span>

<span data-ttu-id="057ee-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="057ee-113">This script uses the following commands.</span></span> <span data-ttu-id="057ee-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="057ee-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="057ee-115">Commande</span><span class="sxs-lookup"><span data-stu-id="057ee-115">Command</span></span> | <span data-ttu-id="057ee-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="057ee-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="057ee-117">az group create</span><span class="sxs-lookup"><span data-stu-id="057ee-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="057ee-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="057ee-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="057ee-119">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="057ee-119">az cosmosdb create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="057ee-120">Crée un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="057ee-120">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="057ee-121">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="057ee-121">az cosmosdb update</span></span>](/cli/azure/cosmosdb#update) | <span data-ttu-id="057ee-122">Met à jour un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="057ee-122">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="057ee-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="057ee-123">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="057ee-124">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="057ee-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="057ee-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="057ee-125">Next steps</span></span>

<span data-ttu-id="057ee-126">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="057ee-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="057ee-127">Vous trouverez des exemples supplémentaires de scripts CLI d’Azure Cosmos DB dans la [documentation d’Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="057ee-127">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
