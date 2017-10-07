---
title: "AAA » CLI Azure Script - créer une base de données Azure PostgreSQL | Documents Microsoft »"
description: "Exemple de script CLI - crée un serveur Azure Database pour PostgreSQL et configure une règle de pare-feu au niveau du serveur."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="e1156-103">Créer une base de données PostgreSQL serveur Azure et configurer une règle de pare-feu à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="e1156-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="e1156-104">Cet exemple de script CLI crée un serveur Azure Database pour PostgreSQL et configure une règle de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="e1156-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="e1156-105">Une fois l’exécution du script de hello a réussi, hello PostgreSQL serveur accessible à partir de tous les services Azure et hello configuré d’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="e1156-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e1156-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e1156-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e1156-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="e1156-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e1156-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1156-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="e1156-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e1156-109">Sample script</span></span>
<span data-ttu-id="e1156-110">Dans cet exemple de script, modifiez hello mis en surbrillance lignes toocustomize hello admin username et password.</span><span class="sxs-lookup"><span data-stu-id="e1156-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e1156-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="e1156-111">Clean up deployment</span></span>
<span data-ttu-id="e1156-112">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e1156-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="e1156-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e1156-113">Script explanation</span></span>
<span data-ttu-id="e1156-114">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="e1156-114">This script uses hello following commands.</span></span> <span data-ttu-id="e1156-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="e1156-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e1156-116">**Commande**</span><span class="sxs-lookup"><span data-stu-id="e1156-116">**Command**</span></span> | <span data-ttu-id="e1156-117">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="e1156-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="e1156-118">az group create</span><span class="sxs-lookup"><span data-stu-id="e1156-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e1156-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e1156-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e1156-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="e1156-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="e1156-121">Crée un serveur PostgreSQL qui héberge les bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="e1156-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="e1156-122">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="e1156-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="e1156-123">Crée un serveur de pare-feu règle tooallow accès toohello et bases de données sous ce dernier à partir de la plage d’adresses IP hello entré.</span><span class="sxs-lookup"><span data-stu-id="e1156-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="e1156-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="e1156-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="e1156-125">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="e1156-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e1156-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1156-126">Next steps</span></span>
- <span data-ttu-id="e1156-127">En savoir plus sur hello CLI d’Azure : [documentation CLI d’Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="e1156-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="e1156-128">Essayer des scripts supplémentaires : [Exemples Azure CLI pour Base de données Azure pour PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e1156-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
