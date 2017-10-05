---
title: "Création et gestion des règles de pare-feu Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande Azure | Microsoft Docs"
description: "Décrit comment créer et gérer des règles de pare-feu Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande d’Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="c7aae-103">Création et gestion des règles de pare-feu Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c7aae-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="c7aae-104">Les règles de pare-feu au niveau du serveur permettent aux administrateurs de gérer l’accès à un serveur Azure Database pour PostgreSQL à partir d’une adresse IP spécifique ou d’une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="c7aae-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="c7aae-105">À l’aide de commandes d’interface de ligne de commande Azure pratiques, vous pouvez créer, mettre à jour, supprimer, répertorier et afficher les règles de pare-feu pour gérer votre serveur.</span><span class="sxs-lookup"><span data-stu-id="c7aae-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="c7aae-106">Pour une vue d’ensemble des pare-feu Azure Database pour PostgreSQL, consultez la rubrique [Règles de pare-feu d’un serveur Azure Database pour PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="c7aae-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7aae-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c7aae-107">Prerequisites</span></span>
<span data-ttu-id="c7aae-108">Pour parcourir ce guide pratique, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c7aae-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="c7aae-109">Un [serveur Azure Database pour PostgreSQL et une base de données](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c7aae-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="c7aae-110">Installer l’utilitaire de ligne de commande [Azure CLI 2.0](/cli/azure/install-azure-cli) ou utiliser Azure Cloud Shell dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="c7aae-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="c7aae-111">Configuration des règles de pare-feu pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c7aae-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="c7aae-112">Les commandes [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) permettent de configurer des règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="c7aae-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="c7aae-113">Répertorier les règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="c7aae-113">List firewall rules</span></span> 
<span data-ttu-id="c7aae-114">Pour répertorier les règles de pare-feu de serveur existant sur le serveur, exécutez la commande [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list).</span><span class="sxs-lookup"><span data-stu-id="c7aae-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="c7aae-115">La sortie répertorie les règles éventuelles, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="c7aae-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="c7aae-116">Vous pouvez utiliser le commutateur `--output table` pour obtenir une sortie dans un format de tableau plus lisible.</span><span class="sxs-lookup"><span data-stu-id="c7aae-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="c7aae-117">Créer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="c7aae-117">Create firewall rule</span></span>
<span data-ttu-id="c7aae-118">Pour créer une règle de pare-feu sur le serveur, exécutez la commande [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="c7aae-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="c7aae-119">Cet exemple autorise toutes les adresses IP pour accéder au serveur **mypgserver-20170401.postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="c7aae-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="c7aae-120">Pour autoriser une seule adresse IP à accéder au serveur, fournissez des adresses IP de début et de fin identiques, comme dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c7aae-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="c7aae-121">En cas de réussite, la sortie de la commande affiche les détails de la règle de pare-feu que vous avez créée, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="c7aae-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="c7aae-122">En cas d’échec, la sortie affiche un texte de message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="c7aae-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="c7aae-123">Mettre à jour une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="c7aae-123">Update firewall rule</span></span> 
<span data-ttu-id="c7aae-124">Mettez à jour une règle de pare-feu existante sur le serveur à l’aide de la commande [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update).</span><span class="sxs-lookup"><span data-stu-id="c7aae-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="c7aae-125">Indiquez le nom de la règle de pare-feu existante comme entrée puis les adresses IP de début et de fin à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="c7aae-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="c7aae-126">En cas de réussite, la sortie de la commande affiche les détails de la règle de pare-feu que vous avez mise à jour, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="c7aae-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="c7aae-127">En cas d’échec, la sortie affiche un texte de message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="c7aae-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="c7aae-128">Si la règle de pare-feu n’existe pas, elle est créée par la commande de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c7aae-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="c7aae-129">Afficher les détails d’une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="c7aae-129">Show firewall rule details</span></span>
<span data-ttu-id="c7aae-130">Vous pouvez également afficher les détails d’une règle de pare-feu pour un serveur de pare-feu en exécutant la commande [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show).</span><span class="sxs-lookup"><span data-stu-id="c7aae-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="c7aae-131">En cas de réussite, la sortie de la commande affiche les détails de la règle de pare-feu que vous avez spécifiée, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="c7aae-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="c7aae-132">En cas d’échec, la sortie affiche un texte de message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="c7aae-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="c7aae-133">Supprimer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="c7aae-133">Delete firewall rule</span></span>
<span data-ttu-id="c7aae-134">Pour révoquer l’accès pour une plage d’adresses IP à partir du serveur, supprimez une règle de pare-feu existante en exécutant la commande [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete).</span><span class="sxs-lookup"><span data-stu-id="c7aae-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="c7aae-135">Indiquez le nom de la règle de pare-feu existante.</span><span class="sxs-lookup"><span data-stu-id="c7aae-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="c7aae-136">En cas de réussite, aucun résultat ne s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c7aae-136">Upon success, there is no output.</span></span> <span data-ttu-id="c7aae-137">En cas d’échec, le texte du message d’erreur est retourné.</span><span class="sxs-lookup"><span data-stu-id="c7aae-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7aae-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7aae-138">Next steps</span></span>
- <span data-ttu-id="c7aae-139">De même, vous pouvez utiliser un navigateur web pour [créer et gérer les règles de pare-feu Azure Database pour PostgreSQL feu à l’aide du portail Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c7aae-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="c7aae-140">En savoir plus sur les [règles de pare-feu du serveur Azure Database pour PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="c7aae-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="c7aae-141">Pour vous aider à vous connecter à un serveur Azure Database pour PostgreSQL, consultez la rubrique [Bibliothèques de connexions pour Azure Database pour PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="c7aae-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
