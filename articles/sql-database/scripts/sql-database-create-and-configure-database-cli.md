---
title: "Exemple CLI-créer une base de données Azure SQL | Microsoft Docs"
description: "Exemple de script Azure CLI pour créer une base de données SQL"
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
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="f0359-103">Utiliser CLI pour créer une seule base de données Azure SQL et configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="f0359-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="f0359-104">Cet exemple de script CLI crée une base de données SQL Azure et configure une règle de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="f0359-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="f0359-105">Une fois que le script a été exécuté avec succès, l’instance SQL Database est accessible à partir de tous les services Azure et l’adresse IP configurée.</span><span class="sxs-lookup"><span data-stu-id="f0359-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f0359-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f0359-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f0359-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="f0359-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="f0359-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f0359-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f0359-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="f0359-109">Sample script</span></span>

<span data-ttu-id="f0359-110">[!code-azurecli-interactive[principal](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Créer une instance SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="f0359-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f0359-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="f0359-111">Clean up deployment</span></span>

<span data-ttu-id="f0359-112">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="f0359-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f0359-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="f0359-113">Script explanation</span></span>

<span data-ttu-id="f0359-114">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="f0359-114">This script uses the following commands.</span></span> <span data-ttu-id="f0359-115">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="f0359-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f0359-116">Commande</span><span class="sxs-lookup"><span data-stu-id="f0359-116">Command</span></span> | <span data-ttu-id="f0359-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="f0359-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0359-118">az group create</span><span class="sxs-lookup"><span data-stu-id="f0359-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="f0359-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="f0359-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f0359-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="f0359-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="f0359-121">Crée un serveur logique qui héberge l’instance SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f0359-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="f0359-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="f0359-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="f0359-123">Crée une règle de pare-feu pour autoriser l’accès à toutes les instances SQL Database sur le serveur à partir de la plage d’adresses IP entrée.</span><span class="sxs-lookup"><span data-stu-id="f0359-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="f0359-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="f0359-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="f0359-125">Crée une instance SQL Database au sein du serveur logique.</span><span class="sxs-lookup"><span data-stu-id="f0359-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="f0359-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="f0359-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="f0359-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="f0359-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0359-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0359-128">Next steps</span></span>

<span data-ttu-id="f0359-129">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0359-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f0359-130">Vous trouverez des exemples supplémentaires de scripts CLI SQL Database sur la page [Documentation Azure SQL Database](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f0359-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

