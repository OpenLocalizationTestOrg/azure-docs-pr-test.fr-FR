---
title: "Script CLI Azure - Mettre à l’échelle le débit d’un conteneur Azure Cosmos DB | Microsoft Docs"
description: "Exemple de script CLI Azure - Mettre à l’échelle le débit d’un conteneur Azure Cosmos DB"
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
ms.openlocfilehash: f08733cd4074c7144b20a0592522423e729e6f1d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="c1e02-103">Mettre à l’échelle le débit d’un conteneur Azure Cosmos DB avec la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="c1e02-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="c1e02-104">Cet exemple met à l’échelle le débit du conteneur pour n’importe quel conteneur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c1e02-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c1e02-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c1e02-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c1e02-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="c1e02-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c1e02-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c1e02-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c1e02-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c1e02-108">Sample script</span></span>

<span data-ttu-id="c1e02-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Mettre à l’échelle le débit d’Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="c1e02-109">[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c1e02-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c1e02-110">Clean up deployment</span></span>

<span data-ttu-id="c1e02-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c1e02-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c1e02-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c1e02-112">Script explanation</span></span>

<span data-ttu-id="c1e02-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="c1e02-113">This script uses the following commands.</span></span> <span data-ttu-id="c1e02-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="c1e02-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c1e02-115">Commande</span><span class="sxs-lookup"><span data-stu-id="c1e02-115">Command</span></span> | <span data-ttu-id="c1e02-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="c1e02-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1e02-117">az group create</span><span class="sxs-lookup"><span data-stu-id="c1e02-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c1e02-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c1e02-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c1e02-119">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="c1e02-119">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="c1e02-120">Met à jour un compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c1e02-120">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="c1e02-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="c1e02-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="c1e02-122">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c1e02-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1e02-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1e02-123">Next steps</span></span>

<span data-ttu-id="c1e02-124">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1e02-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c1e02-125">Vous trouverez des exemples supplémentaires de scripts CLI d’Azure Cosmos DB dans la [documentation d’Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c1e02-125">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
