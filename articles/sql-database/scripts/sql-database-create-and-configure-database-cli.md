---
title: "aaaCLI la création de l’exemple d’une base de données SQL Azure | Documents Microsoft"
description: "Azure CLI exemple script toocreate une base de données SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="7952d-103">CLI toocreate une base de données SQL Azure et de configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="7952d-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="7952d-104">Cet exemple de script CLI crée une base de données SQL Azure et configure une règle de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="7952d-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="7952d-105">Une fois l’exécution du script de hello a réussi, hello de que base de données SQL est accessible à partir de tous les services Azure et hello configuré adresse IP.</span><span class="sxs-lookup"><span data-stu-id="7952d-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7952d-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7952d-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7952d-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="7952d-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7952d-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7952d-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7952d-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="7952d-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7952d-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="7952d-110">Clean up deployment</span></span>

<span data-ttu-id="7952d-111">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="7952d-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7952d-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="7952d-112">Script explanation</span></span>

<span data-ttu-id="7952d-113">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="7952d-113">This script uses hello following commands.</span></span> <span data-ttu-id="7952d-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="7952d-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7952d-115">Commande</span><span class="sxs-lookup"><span data-stu-id="7952d-115">Command</span></span> | <span data-ttu-id="7952d-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="7952d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7952d-117">az group create</span><span class="sxs-lookup"><span data-stu-id="7952d-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="7952d-118">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="7952d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7952d-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="7952d-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="7952d-120">Crée un serveur logique que les ordinateurs hôtes hello de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7952d-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="7952d-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="7952d-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="7952d-122">Crée un tooall dans pare-feu règle tooallow accès aux bases de données SQL sur le serveur hello à partir de la plage d’adresses IP hello entré.</span><span class="sxs-lookup"><span data-stu-id="7952d-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="7952d-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="7952d-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="7952d-124">Crée hello de base de données SQL dans un serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="7952d-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="7952d-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="7952d-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="7952d-126">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="7952d-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7952d-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7952d-127">Next steps</span></span>

<span data-ttu-id="7952d-128">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7952d-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7952d-129">Vous trouverez des exemples supplémentaires de script CLI de base de données SQL dans hello [documentation de base de données SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7952d-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

