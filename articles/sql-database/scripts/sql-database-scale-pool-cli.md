---
title: "exemple d’aaaCLI met à l’échelle une base de données SQL une SQL Azure de pool élastique | Documents Microsoft"
description: "Azure CLI exemple script tooscale un pool élastique SQL dans la base de données SQL Azure"
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
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="d653b-103">Utilisez CLI tooscale un pool élastique SQL dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d653b-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="d653b-104">Cet exemple de script Azure CLI crée des pools élastiques SQL, déplace des bases de données regroupées et modifie les niveaux de performances d’un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="d653b-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d653b-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d653b-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d653b-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d653b-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d653b-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d653b-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d653b-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d653b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d653b-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="d653b-109">Clean up deployment</span></span>

<span data-ttu-id="d653b-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d653b-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d653b-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d653b-111">Script explanation</span></span>

<span data-ttu-id="d653b-112">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, serveur logique, base de données SQL et les règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="d653b-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="d653b-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="d653b-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d653b-114">Commande</span><span class="sxs-lookup"><span data-stu-id="d653b-114">Command</span></span> | <span data-ttu-id="d653b-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="d653b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d653b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d653b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d653b-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d653b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d653b-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="d653b-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="d653b-119">Crée un serveur logique que les ordinateurs hôtes hello de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="d653b-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="d653b-120">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="d653b-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="d653b-121">Crée un pool élastique de base de données serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="d653b-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="d653b-122">az sql db create</span><span class="sxs-lookup"><span data-stu-id="d653b-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="d653b-123">Crée hello de base de données SQL dans un serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="d653b-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="d653b-124">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="d653b-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="d653b-125">Met à jour un pool élastique de base de données, cette Bonjour de modifications exemple assigné eDTU.</span><span class="sxs-lookup"><span data-stu-id="d653b-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="d653b-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="d653b-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d653b-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="d653b-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d653b-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d653b-128">Next steps</span></span>

<span data-ttu-id="d653b-129">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d653b-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d653b-130">Vous trouverez des exemples supplémentaires de script CLI de base de données SQL dans hello [documentation de base de données SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d653b-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
