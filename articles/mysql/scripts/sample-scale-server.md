---
title: "aaaAzure CLI exemples tooscale une base de données Azure pour le serveur MySQL | Documents Microsoft"
description: "Cet exemple de script CLI met à l’échelle de la base de données Azure pour le niveau de performances MySQL server tooa après interrogation de métriques de hello."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="b6743-103">Surveiller et mettre à l’échelle un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="b6743-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="b6743-104">Cet exemple de script CLI met à l’échelle une base de données Azure unique pour le niveau de performances MySQL server tooa après interrogation de métriques de hello.</span><span class="sxs-lookup"><span data-stu-id="b6743-104">This sample CLI script scales a single Azure Database for MySQL server tooa different performance level after querying hello metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b6743-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b6743-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b6743-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="b6743-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b6743-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b6743-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b6743-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="b6743-108">Sample script</span></span>
<span data-ttu-id="b6743-109">Dans cet exemple de script, modifiez hello mis en surbrillance lignes toocustomize hello admin username et password.</span><span class="sxs-lookup"><span data-stu-id="b6743-109">In this sample script, change hello highlighted lines toocustomize hello admin username and password.</span></span> <span data-ttu-id="b6743-110">Remplacez l’id d’abonnement hello utilisée dans les commandes de moniteur hello az avec votre propre id d’abonnement.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="b6743-110">Replace hello subscription id used in hello az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b6743-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="b6743-111">Clean up deployment</span></span>
<span data-ttu-id="b6743-112">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b6743-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="b6743-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b6743-113">Script explanation</span></span>
<span data-ttu-id="b6743-114">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="b6743-114">This script uses hello following commands.</span></span> <span data-ttu-id="b6743-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="b6743-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b6743-116">**Commande**</span><span class="sxs-lookup"><span data-stu-id="b6743-116">**Command**</span></span> | <span data-ttu-id="b6743-117">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="b6743-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="b6743-118">az group create</span><span class="sxs-lookup"><span data-stu-id="b6743-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b6743-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="b6743-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b6743-120">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="b6743-120">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="b6743-121">Crée un serveur MySQL qui héberge les bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="b6743-121">Creates a MySQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="b6743-122">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="b6743-122">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="b6743-123">Liste hello valeur métrique pour les ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="b6743-123">List hello metric value for hello resources.</span></span> |
| [<span data-ttu-id="b6743-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="b6743-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b6743-125">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b6743-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6743-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6743-126">Next steps</span></span>
- <span data-ttu-id="b6743-127">En savoir plus sur hello CLI d’Azure : [documentation relative à Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6743-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="b6743-128">Essayer des scripts supplémentaires : [Exemples Azure CLI pour Base de données Azure pour MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b6743-128">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="b6743-129">Pour plus d’informations sur la mise à l’échelle, consultez [Niveaux de service](../concepts-service-tiers.md) et [Unités de calcul et unités de stockage](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b6743-129">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
