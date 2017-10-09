---
title: "pool élastique du SQL de la base de données SQL Azure move-exemple aaaCLI | Documents Microsoft"
description: "Azure CLI exemple script toomove une base de données SQL dans un pool élastique SQL"
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
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="77b44-103">Utilisez CLI toomove une base de données SQL Azure dans un pool élastique SQL</span><span class="sxs-lookup"><span data-stu-id="77b44-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="77b44-104">Cet exemple de script CLI d’Azure crée deux pools élastiques déplace une base de données SQL Azure à partir d’un pool élastique SQL dans un autre pool élastique SQL et déplace ensuite la base de données hello en dehors du niveau de performance de base de données Azure unique tooa pool élastique.</span><span class="sxs-lookup"><span data-stu-id="77b44-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="77b44-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="77b44-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="77b44-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="77b44-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="77b44-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77b44-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="77b44-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="77b44-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="77b44-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="77b44-109">Clean up deployment</span></span>

<span data-ttu-id="77b44-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="77b44-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="77b44-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="77b44-111">Script explanation</span></span>

<span data-ttu-id="77b44-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="77b44-112">This script uses hello following commands.</span></span> <span data-ttu-id="77b44-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="77b44-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="77b44-114">Commande</span><span class="sxs-lookup"><span data-stu-id="77b44-114">Command</span></span> | <span data-ttu-id="77b44-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="77b44-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77b44-116">az group create</span><span class="sxs-lookup"><span data-stu-id="77b44-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="77b44-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="77b44-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="77b44-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="77b44-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="77b44-119">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="77b44-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="77b44-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="77b44-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="77b44-121">Crée un pool élastique serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="77b44-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="77b44-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="77b44-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="77b44-123">Crée une base de données au sein d’un serveur logique en tant que base de données unique ou regroupée.</span><span class="sxs-lookup"><span data-stu-id="77b44-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="77b44-124">az sql db update</span><span class="sxs-lookup"><span data-stu-id="77b44-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="77b44-125">Met à jour les propriétés de la base de données ou déplace une base de données vers, hors ou entre des pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="77b44-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="77b44-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="77b44-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="77b44-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="77b44-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77b44-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77b44-128">Next steps</span></span>

<span data-ttu-id="77b44-129">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77b44-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="77b44-130">Vous trouverez des exemples supplémentaires de script CLI de base de données SQL dans hello [documentation de base de données SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="77b44-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


