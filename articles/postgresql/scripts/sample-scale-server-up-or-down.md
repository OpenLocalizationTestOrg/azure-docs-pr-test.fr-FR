---
title: "Script CLI Azure - Mettre à l’échelle Azure Database pour PostgreSQL | Microsoft Docs"
description: "Exemple de script Azure CLI - Mettre à l’échelle le serveur Azure Database pour PostgreSQL vers un autre niveau de performances après interrogation des métriques."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: b847abb336cce5dd5516469dca58002d3ba265f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a><span data-ttu-id="3cb36-103">Surveiller et mettre à l’échelle d’un seul serveur PostgreSQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="3cb36-103">Monitor and scale a single PostgreSQL server using Azure CLI</span></span>
<span data-ttu-id="3cb36-104">Cet exemple de script CLI met à l’échelle un serveur Azure Database pour PostgreSQL vers un nouveau niveau de performance après l’analyse des métriques.</span><span class="sxs-lookup"><span data-stu-id="3cb36-104">This sample CLI script scales a single Azure Database for PostgreSQL server to a different performance level after querying the metrics.</span></span> 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3cb36-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3cb36-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3cb36-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3cb36-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="3cb36-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3cb36-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3cb36-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3cb36-108">Sample script</span></span>
<span data-ttu-id="3cb36-109">Dans cet exemple de script, modifiez les lignes en surbrillance pour personnaliser le nom d’utilisateur et le mot de passe d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3cb36-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="3cb36-110">Remplacez l’ID d’abonnement utilisé dans les commandes de moniteur az avec votre propre ID d’abonnement [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Créer et mettre à l’échelle Azure Database pour PostgreSQL.")]</span><span class="sxs-lookup"><span data-stu-id="3cb36-110">Replace the subscription id used in the az monitor commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3cb36-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="3cb36-111">Clean up deployment</span></span>
<span data-ttu-id="3cb36-112">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="3cb36-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="3cb36-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Supprimez le groupe de ressources.")]</span><span class="sxs-lookup"><span data-stu-id="3cb36-113">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="3cb36-114">Explication du script</span><span class="sxs-lookup"><span data-stu-id="3cb36-114">Script explanation</span></span>
<span data-ttu-id="3cb36-115">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="3cb36-115">This script uses the following commands.</span></span> <span data-ttu-id="3cb36-116">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="3cb36-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3cb36-117">**Commande**</span><span class="sxs-lookup"><span data-stu-id="3cb36-117">**Command**</span></span> | <span data-ttu-id="3cb36-118">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="3cb36-118">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="3cb36-119">az group create</span><span class="sxs-lookup"><span data-stu-id="3cb36-119">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="3cb36-120">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="3cb36-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3cb36-121">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="3cb36-121">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="3cb36-122">Crée un serveur PostgreSQL qui héberge les bases de données.</span><span class="sxs-lookup"><span data-stu-id="3cb36-122">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="3cb36-123">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="3cb36-123">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="3cb36-124">Affiche la valeur de métrique pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="3cb36-124">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="3cb36-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="3cb36-125">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="3cb36-126">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="3cb36-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3cb36-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3cb36-127">Next steps</span></span>
- <span data-ttu-id="3cb36-128">En savoir plus sur Azure CLI : [Documentation d’Azure CLI](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="3cb36-128">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="3cb36-129">Essayer des scripts supplémentaires : [Exemples Azure CLI pour Base de données Azure pour PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3cb36-129">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="3cb36-130">En savoir plus sur la mise à l’échelle : [Niveaux de service](../concepts-service-tiers.md) et [Unités de calcul et de stockage](../concepts-compute-unit-and-storage.md)</span><span class="sxs-lookup"><span data-stu-id="3cb36-130">Read more information on scaling: [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md)</span></span>
