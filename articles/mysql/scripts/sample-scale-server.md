---
title: "Exemples Azure CLI pour mettre à l’échelle un serveur Azure Database pour MySQL | Microsoft Docs"
description: "Cet exemple de script CLI met à l’échelle un serveur Azure Database pour MySQL vers un nouveau niveau de performance après l’analyse des métriques."
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
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="6b968-103">Surveiller et mettre à l’échelle un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="6b968-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="6b968-104">Cet exemple de script CLI met à l’échelle un serveur de base de données Azure unique pour MySQL vers un nouveau niveau de performance après l’analyse des métriques.</span><span class="sxs-lookup"><span data-stu-id="6b968-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b968-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6b968-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6b968-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="6b968-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6b968-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b968-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6b968-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="6b968-108">Sample script</span></span>
<span data-ttu-id="6b968-109">Dans cet exemple de script, modifiez les lignes en surbrillance pour personnaliser le nom d’utilisateur et le mot de passe d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6b968-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="6b968-110">Remplacez l’ID d’abonnement utilisé dans les commandes de surveillance az par votre propre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6b968-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="6b968-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Créez et mettez à l’échelle Base de données Azure pour MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="6b968-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6b968-112">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="6b968-112">Clean up deployment</span></span>
<span data-ttu-id="6b968-113">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="6b968-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="6b968-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Supprimez le groupe de ressources.")]</span><span class="sxs-lookup"><span data-stu-id="6b968-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="6b968-115">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6b968-115">Script explanation</span></span>
<span data-ttu-id="6b968-116">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="6b968-116">This script uses the following commands.</span></span> <span data-ttu-id="6b968-117">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="6b968-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6b968-118">**Commande**</span><span class="sxs-lookup"><span data-stu-id="6b968-118">**Command**</span></span> | <span data-ttu-id="6b968-119">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="6b968-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="6b968-120">az group create</span><span class="sxs-lookup"><span data-stu-id="6b968-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6b968-121">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="6b968-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6b968-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="6b968-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="6b968-123">Crée un serveur MySQL qui héberge les bases de données.</span><span class="sxs-lookup"><span data-stu-id="6b968-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="6b968-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="6b968-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="6b968-125">Affiche la valeur de métrique pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="6b968-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="6b968-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="6b968-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6b968-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="6b968-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6b968-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b968-128">Next steps</span></span>
- <span data-ttu-id="6b968-129">En savoir plus sur Azure CLI : [Documentation d’Azure CLI](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="6b968-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="6b968-130">Essayer des scripts supplémentaires : [Exemples Azure CLI pour Base de données Azure pour MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6b968-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="6b968-131">Pour plus d’informations sur la mise à l’échelle, consultez [Niveaux de service](../concepts-service-tiers.md) et [Unités de calcul et unités de stockage](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6b968-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
