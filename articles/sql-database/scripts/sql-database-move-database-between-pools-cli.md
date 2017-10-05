---
title: "Script Azure CLI - Déplacer une instance SQL Database et des pools élastiques | Microsoft Docs"
description: "Exemple de script Azure CLI pour déplacer une base de données SQL dans un pool élastique SQL"
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
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="6fb2d-103">Utiliser l’interface CLI afin de déplacer une base de données SQL Azure dans un pool élastique SQL</span><span class="sxs-lookup"><span data-stu-id="6fb2d-103">Use CLI to move an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="6fb2d-104">Cet exemple de script Azure CLI crée deux pools élastiques et déplace une base de données SQL Azure d’un pool élastique SQL vers un autre pool élastique SQL. Le script déplace par la suite la base de données en dehors d’un pool élastique vers un niveau de performance de base de données Azure unique.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves the database out of elastic pool to a single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6fb2d-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6fb2d-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6fb2d-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6fb2d-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6fb2d-108">Sample script</span></span>

<span data-ttu-id="6fb2d-109">[!code-azurecli-interactive[principal](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Déplacer une base de données entre les pools")]</span><span class="sxs-lookup"><span data-stu-id="6fb2d-109">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6fb2d-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="6fb2d-110">Clean up deployment</span></span>

<span data-ttu-id="6fb2d-111">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-111">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6fb2d-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6fb2d-112">Script explanation</span></span>

<span data-ttu-id="6fb2d-113">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-113">This script uses the following commands.</span></span> <span data-ttu-id="6fb2d-114">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6fb2d-115">Commande</span><span class="sxs-lookup"><span data-stu-id="6fb2d-115">Command</span></span> | <span data-ttu-id="6fb2d-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="6fb2d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6fb2d-117">az group create</span><span class="sxs-lookup"><span data-stu-id="6fb2d-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6fb2d-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6fb2d-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="6fb2d-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="6fb2d-120">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-120">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="6fb2d-121">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="6fb2d-121">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="6fb2d-122">Crée un pool élastique au sein du serveur logique.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-122">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="6fb2d-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="6fb2d-123">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="6fb2d-124">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-124">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="6fb2d-125">az sql db update</span><span class="sxs-lookup"><span data-stu-id="6fb2d-125">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="6fb2d-126">Met à jour les propriétés de la base de données ou déplace une base de données vers, hors ou entre des pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-126">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="6fb2d-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="6fb2d-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6fb2d-128">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6fb2d-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fb2d-129">Next steps</span></span>

<span data-ttu-id="6fb2d-130">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6fb2d-131">Vous trouverez des exemples supplémentaires de scripts CLI SQL Database sur la page [Documentation Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-131">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


