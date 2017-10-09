---
title: "aaaCreate et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide d’Azure CLI | Documents Microsoft"
description: "Cet article décrit comment toocreate et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de la ligne de commande CLI d’Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="bdeec-103">Création et gestion des règles de pare-feu Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="bdeec-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="bdeec-104">Les règles de pare-feu de niveau serveur activer administrateurs toomanage accès tooan Azure de base de données PostgreSQL serveur à partir d’une adresse IP spécifique ou de la plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="bdeec-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="bdeec-105">À l’aide des commandes CLI d’Azure pratiques, vous pouvez créer, mettre à jour, supprimer, répertorier et afficher toomanage de règles de pare-feu de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="bdeec-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="bdeec-106">Pour une vue d’ensemble des pare-feu Azure Database pour PostgreSQL, consultez la rubrique [Règles de pare-feu d’un serveur Azure Database pour PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="bdeec-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdeec-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bdeec-107">Prerequisites</span></span>
<span data-ttu-id="bdeec-108">toostep via ce tooguide de procédure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="bdeec-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="bdeec-109">Un [serveur Azure Database pour PostgreSQL et une base de données](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bdeec-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="bdeec-110">Installer [Azure CLI 2.0](/cli/azure/install-azure-cli) ligne de commande utilitaires ou utilisez hello Azure Cloud Shell dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="bdeec-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="bdeec-111">Configuration des règles de pare-feu pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="bdeec-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="bdeec-112">Hello [az postgres server-règle de pare-feu](/cli/azure/postgres/server/firewall-rule) commandes sont des règles de pare-feu tooconfigure utilisé.</span><span class="sxs-lookup"><span data-stu-id="bdeec-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="bdeec-113">Répertorier les règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="bdeec-113">List firewall rules</span></span> 
<span data-ttu-id="bdeec-114">existant de hello toolist règles de pare-feu du serveur sur le serveur de hello, exécutez hello [liste de règle de pare-feu du serveur az postgres](/cli/azure/postgres/server/firewall-rule#list) commande.</span><span class="sxs-lookup"><span data-stu-id="bdeec-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="bdeec-115">sortie de Hello répertorie les règles de hello si elle existe, par défaut au format JSON de format.</span><span class="sxs-lookup"><span data-stu-id="bdeec-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="bdeec-116">Vous pouvez utiliser le commutateur de hello `--output table` pour un format plus lisible de la table en tant que sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="bdeec-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="bdeec-117">Créer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="bdeec-117">Create firewall rule</span></span>
<span data-ttu-id="bdeec-118">toocreate une règle de pare-feu sur le serveur hello, exécutez hello [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="bdeec-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="bdeec-119">Cet exemple permet à une plage de tous les IP adresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="bdeec-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="bdeec-120">tooallow un tooaccess d’adresse IP au singulier, fournir hello la même adresse que hello IP de début et l’adresse IP de fin, comme dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="bdeec-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="bdeec-121">En cas de réussite, sortie de la commande hello répertorie hello hello de règle de pare-feu que vous avez créé, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="bdeec-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="bdeec-122">En cas de panne, hello sortie showserror texte du message à la place.</span><span class="sxs-lookup"><span data-stu-id="bdeec-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="bdeec-123">Mettre à jour une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="bdeec-123">Update firewall rule</span></span> 
<span data-ttu-id="bdeec-124">Mettre à jour une règle de pare-feu existante sur l’utilisation de serveur hello [mise à jour des règles de pare-feu serveur postgres az](/cli/azure/postgres/server/firewall-rule#update) commande.</span><span class="sxs-lookup"><span data-stu-id="bdeec-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="bdeec-125">Fournir le nom hello de règle de pare-feu existante hello comme entrée et tooupdate par démarrer hello IP et de fin attributs IP.</span><span class="sxs-lookup"><span data-stu-id="bdeec-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="bdeec-126">En cas de réussite, sortie de la commande hello répertorie hello hello de règle de pare-feu que vous avez mis à jour, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="bdeec-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="bdeec-127">En cas de panne, hello sortie showserror texte du message à la place.</span><span class="sxs-lookup"><span data-stu-id="bdeec-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="bdeec-128">Si la règle de pare-feu hello n’existe pas, il est créé par la commande de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="bdeec-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="bdeec-129">Afficher les détails d’une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="bdeec-129">Show firewall rule details</span></span>
<span data-ttu-id="bdeec-130">Vous pouvez également afficher des détails de la règle pour un serveur de pare-feu existant hello en exécutant [afficher de règle de pare-feu serveur az postgres](/cli/azure/postgres/server/firewall-rule#show) commande.</span><span class="sxs-lookup"><span data-stu-id="bdeec-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="bdeec-131">En cas de réussite, sortie de la commande hello répertorie hello hello de règle de pare-feu que vous avez spécifié, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="bdeec-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="bdeec-132">En cas de panne, hello sortie showserror texte du message à la place.</span><span class="sxs-lookup"><span data-stu-id="bdeec-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="bdeec-133">Supprimer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="bdeec-133">Delete firewall rule</span></span>
<span data-ttu-id="bdeec-134">accès toorevoke pour une plage IP du serveur de hello, supprimer une règle de pare-feu existante en exécutant hello [az postgres server-règle de pare-feu supprimer](/cli/azure/postgres/server/firewall-rule#delete) commande.</span><span class="sxs-lookup"><span data-stu-id="bdeec-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="bdeec-135">Fournir le nom hello hello existant de règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="bdeec-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="bdeec-136">En cas de réussite, aucun résultat ne s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bdeec-136">Upon success, there is no output.</span></span> <span data-ttu-id="bdeec-137">En cas d’échec, le texte de message d’erreur hello est retourné.</span><span class="sxs-lookup"><span data-stu-id="bdeec-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdeec-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bdeec-138">Next steps</span></span>
- <span data-ttu-id="bdeec-139">De même, vous pouvez utiliser un navigateur web trop[créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bdeec-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="bdeec-140">En savoir plus sur les [règles de pare-feu du serveur Azure Database pour PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="bdeec-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="bdeec-141">Pour la connexion tooan Azure de base de données PostgreSQL serveur, consultez [bibliothèques de connexions de base de données Azure pour PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="bdeec-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
