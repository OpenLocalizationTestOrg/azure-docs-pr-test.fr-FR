---
title: "Script CLI Azure - Créer une instance d’Azure Database pour PostgreSQL | Microsoft Docs"
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
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="79683-103">Créer un serveur Azure Database pour PostgreSQL et configurer une règle de pare-feu à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="79683-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="79683-104">Cet exemple de script CLI crée un serveur Azure Database pour PostgreSQL et configure une règle de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="79683-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="79683-105">Une fois que le script a été exécuté avec succès, le serveur PostgreSQL est accessible à partir de tous les services Azure et l’adresse IP configurée.</span><span class="sxs-lookup"><span data-stu-id="79683-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="79683-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="79683-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="79683-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="79683-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="79683-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="79683-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="79683-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="79683-109">Sample script</span></span>
<span data-ttu-id="79683-110">Dans cet exemple de script, modifiez les lignes en surbrillance pour personnaliser le nom d’utilisateur et le mot de passe d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="79683-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="79683-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Créez une base de données Azure pour PostgreSQL, et des règles de pare-feu au niveau serveur.")]</span><span class="sxs-lookup"><span data-stu-id="79683-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="79683-112">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="79683-112">Clean up deployment</span></span>
<span data-ttu-id="79683-113">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="79683-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="79683-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Supprimez le groupe de ressources.")]</span><span class="sxs-lookup"><span data-stu-id="79683-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="79683-115">Explication du script</span><span class="sxs-lookup"><span data-stu-id="79683-115">Script explanation</span></span>
<span data-ttu-id="79683-116">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="79683-116">This script uses the following commands.</span></span> <span data-ttu-id="79683-117">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="79683-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="79683-118">**Commande**</span><span class="sxs-lookup"><span data-stu-id="79683-118">**Command**</span></span> | <span data-ttu-id="79683-119">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="79683-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="79683-120">az group create</span><span class="sxs-lookup"><span data-stu-id="79683-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="79683-121">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="79683-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="79683-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="79683-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="79683-123">Crée un serveur PostgreSQL qui héberge les bases de données.</span><span class="sxs-lookup"><span data-stu-id="79683-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="79683-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="79683-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="79683-125">Crée une règle de pare-feu pour autoriser l’accès au serveur et aux bases de données qui s’y trouvent à partir de la plage d’adresses IP entrée.</span><span class="sxs-lookup"><span data-stu-id="79683-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="79683-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="79683-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="79683-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="79683-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="79683-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79683-128">Next steps</span></span>
- <span data-ttu-id="79683-129">En savoir plus sur Azure CLI : [Documentation d’Azure CLI](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="79683-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="79683-130">Essayer des scripts supplémentaires : [Exemples Azure CLI pour Base de données Azure pour PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="79683-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
