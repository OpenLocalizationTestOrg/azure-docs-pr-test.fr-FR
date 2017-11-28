---
title: "Script Azure CLI - Mettre un pool élastique SQL à l’échelle dans Azure SQL Database | Microsoft Docs"
description: "Exemple de script Azure CLI pour mettre un pool élastique SQL à l’échelle dans Azure SQL Database"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 888d2b7b7c118fede82d39881570a3b3d7b09961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-cli-to-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="d50cf-103">Utiliser l’interface de ligne de commande pour mettre un pool élastique SQL à l’échelle dans Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d50cf-103">Use CLI to scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="d50cf-104">Cet exemple de script Azure CLI crée des pools élastiques SQL, déplace des bases de données regroupées et modifie les niveaux de performances d’un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="d50cf-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d50cf-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d50cf-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d50cf-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="d50cf-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="d50cf-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d50cf-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d50cf-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d50cf-108">Sample script</span></span>

<span data-ttu-id="d50cf-109">[!code-azurecli-interactive[principal](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Déplacer une base de données entre les pools")]</span><span class="sxs-lookup"><span data-stu-id="d50cf-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d50cf-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="d50cf-110">Clean up deployment</span></span>

<span data-ttu-id="d50cf-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d50cf-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d50cf-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d50cf-112">Script explanation</span></span>

<span data-ttu-id="d50cf-113">Ce script utilise les commandes suivantes pour créer un groupe de ressources, un serveur logique, une instance SQL Database et des règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="d50cf-113">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="d50cf-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d50cf-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d50cf-115">Commande</span><span class="sxs-lookup"><span data-stu-id="d50cf-115">Command</span></span> | <span data-ttu-id="d50cf-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="d50cf-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d50cf-117">az group create</span><span class="sxs-lookup"><span data-stu-id="d50cf-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d50cf-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d50cf-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d50cf-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="d50cf-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="d50cf-120">Crée un serveur logique qui héberge l’instance SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d50cf-120">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="d50cf-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="d50cf-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="d50cf-122">Crée un pool de bases de données élastique au sein du serveur logique.</span><span class="sxs-lookup"><span data-stu-id="d50cf-122">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="d50cf-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="d50cf-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="d50cf-124">Crée une instance SQL Database au sein du serveur logique.</span><span class="sxs-lookup"><span data-stu-id="d50cf-124">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="d50cf-125">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="d50cf-125">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="d50cf-126">Met à jour un pool de base de données élastique : dans cet exemple, modifie l’eDTU attribué.</span><span class="sxs-lookup"><span data-stu-id="d50cf-126">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="d50cf-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="d50cf-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d50cf-128">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="d50cf-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d50cf-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d50cf-129">Next steps</span></span>

<span data-ttu-id="d50cf-130">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d50cf-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d50cf-131">Vous trouverez des exemples supplémentaires de scripts CLI SQL Database sur la page [Documentation Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d50cf-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
