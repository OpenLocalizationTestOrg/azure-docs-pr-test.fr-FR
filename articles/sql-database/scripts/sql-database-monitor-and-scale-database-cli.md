---
title: "base de données SQL Azure aaaCLI exemple analyse échelle unique | Documents Microsoft"
description: "Exemple d’interface CLI Azure toomonitor de script et l’échelle d’une base de données SQL Azure"
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
ms.openlocfilehash: 36031ddd46a947a80fe37884858a84eb66217270
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="c7c09-103">Utilisez CLI toomonitor et mettre à l’échelle d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="c7c09-103">Use CLI toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="c7c09-104">Cet exemple de script CLI d’Azure met à l’échelle un niveau de performance différents de tooa de base de données SQL Azure unique après interrogation des informations sur la taille de base de données hello hello.</span><span class="sxs-lookup"><span data-stu-id="c7c09-104">This Azure CLI script example scales a single Azure SQL database tooa different performance level after querying hello size information of hello database.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c7c09-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c7c09-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c7c09-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c7c09-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c7c09-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c7c09-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c7c09-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c7c09-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c7c09-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c7c09-109">Clean up deployment</span></span>

<span data-ttu-id="c7c09-110">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c7c09-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c7c09-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c7c09-111">Script explanation</span></span>

<span data-ttu-id="c7c09-112">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="c7c09-112">This script uses hello following commands.</span></span> <span data-ttu-id="c7c09-113">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c7c09-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c7c09-114">Commande</span><span class="sxs-lookup"><span data-stu-id="c7c09-114">Command</span></span> | <span data-ttu-id="c7c09-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="c7c09-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c7c09-116">az group create</span><span class="sxs-lookup"><span data-stu-id="c7c09-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c7c09-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c7c09-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c7c09-118">az sql server create</span><span class="sxs-lookup"><span data-stu-id="c7c09-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="c7c09-119">Crée un serveur logique qui héberge une base de données.</span><span class="sxs-lookup"><span data-stu-id="c7c09-119">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="c7c09-120">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="c7c09-120">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="c7c09-121">Affiche des informations sur l’utilisation de taille hello pour une base de données.</span><span class="sxs-lookup"><span data-stu-id="c7c09-121">Shows hello size usage information for a database.</span></span> |
| [<span data-ttu-id="c7c09-122">az sql db update</span><span class="sxs-lookup"><span data-stu-id="c7c09-122">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="c7c09-123">Met à jour les propriétés de base de données (par exemple, le niveau niveau ou des performances du service hello) ou déplace une base de données en, d’ou entre les pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="c7c09-123">Updates database properties (such as hello service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="c7c09-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="c7c09-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c7c09-125">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c7c09-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c7c09-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7c09-126">Next steps</span></span>

<span data-ttu-id="c7c09-127">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c7c09-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c7c09-128">Vous trouverez des exemples supplémentaires de script CLI de base de données SQL dans hello [documentation de base de données SQL Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c7c09-128">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
