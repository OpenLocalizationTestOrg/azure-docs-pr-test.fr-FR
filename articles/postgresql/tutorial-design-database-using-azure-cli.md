---
title: "Concevoir votre première base de données Azure pour PostgreSQL avec Azure CLI | Microsoft Docs"
description: "Ce didacticiel montre comment concevoir votre première base de données Azure pour PostgreSQL à l’aide de l’interface Azure CLI."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="537fa-103">Concevoir votre première base de données Azure pour PostgreSQL avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="537fa-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="537fa-104">Dans ce didacticiel, vous allez utiliser l’interface Azure CLI (interface de ligne de commande) et d’autres utilitaires pour apprendre à :</span><span class="sxs-lookup"><span data-stu-id="537fa-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="537fa-105">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="537fa-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="537fa-106">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="537fa-106">Configure the server firewall</span></span>
> * <span data-ttu-id="537fa-107">Utiliser l’utilitaire [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="537fa-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="537fa-108">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="537fa-108">Load sample data</span></span>
> * <span data-ttu-id="537fa-109">Données de requête</span><span class="sxs-lookup"><span data-stu-id="537fa-109">Query data</span></span>
> * <span data-ttu-id="537fa-110">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="537fa-110">Update data</span></span>
> * <span data-ttu-id="537fa-111">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="537fa-111">Restore data</span></span>

<span data-ttu-id="537fa-112">Vous pouvez utiliser Azure Cloud Shell dans le navigateur, ou [installer Azure CLI 2.0]( /cli/azure/install-azure-cli) sur votre ordinateur pour exécuter les blocs de code de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="537fa-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="537fa-113">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="537fa-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="537fa-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="537fa-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="537fa-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="537fa-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="537fa-116">Si vous possédez plusieurs abonnements, sélectionnez l’abonnement approprié dans lequel la ressource existe ou est facturée.</span><span class="sxs-lookup"><span data-stu-id="537fa-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="537fa-117">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="537fa-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="537fa-118">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="537fa-118">Create a resource group</span></span>
<span data-ttu-id="537fa-119">Créez un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="537fa-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="537fa-120">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="537fa-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="537fa-121">L’exemple suivant crée un groupe de ressources nommé `myresourcegroup` à l’emplacement `westus`.</span><span class="sxs-lookup"><span data-stu-id="537fa-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="537fa-122">Créer un serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="537fa-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="537fa-123">Créez un [serveur Azure Database pour PostgreSQL](overview.md) avec la commande [az sql server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="537fa-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="537fa-124">Un serveur contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="537fa-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="537fa-125">L’exemple suivant crée un serveur nommé `mypgserver-20170401` dans votre groupe de ressources `myresourcegroup` avec l’identifiant d’administrateur serveur `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="537fa-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="537fa-126">Le nom du serveur correspond au nom DNS et doit ainsi être globalement unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="537fa-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="537fa-127">Remplacez `<server_admin_password>` par votre propre valeur.</span><span class="sxs-lookup"><span data-stu-id="537fa-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="537fa-128">La connexion d’administrateur serveur et le mot de passe que vous spécifiez ici seront requis plus loin dans ce guide de démarrage rapide pour la connexion au serveur et à ses bases de données.</span><span class="sxs-lookup"><span data-stu-id="537fa-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="537fa-129">Retenez ou enregistrez ces informations pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="537fa-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="537fa-130">Par défaut, la base de données **postgres** est créée sous le serveur.</span><span class="sxs-lookup"><span data-stu-id="537fa-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="537fa-131">La base de données [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) est une base de données par défaut destinée aux utilisateurs, utilitaires et applications tierces.</span><span class="sxs-lookup"><span data-stu-id="537fa-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="537fa-132">Configurer une règle de pare-feu au niveau du serveur</span><span class="sxs-lookup"><span data-stu-id="537fa-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="537fa-133">Créez une règle de pare-feu au niveau du serveur Azure PostgreSQL avec la commande [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="537fa-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="537fa-134">Une règle de pare-feu au niveau du serveur permet à une application externe, comme [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/), de se connecter à votre serveur via le pare-feu du service Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="537fa-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="537fa-135">Vous pouvez définir une règle de pare-feu qui couvre une plage d’adresses IP pour pouvoir vous connecter à partir de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="537fa-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="537fa-136">L’exemple suivant utilise [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) pour créer une règle de pare-feu `AllowAllIps` pour une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="537fa-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="537fa-137">Pour ouvrir toutes les adresses IP, utilisez 0.0.0.0 comme adresse IP de début et 255.255.255.255 comme adresse de fin.</span><span class="sxs-lookup"><span data-stu-id="537fa-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="537fa-138">Le serveur Azure PostgreSQL communique sur le port 5432.</span><span class="sxs-lookup"><span data-stu-id="537fa-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="537fa-139">Lorsque vous vous connectez à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 peut être bloqué par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="537fa-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="537fa-140">Pour vous connecter à votre serveur Azure SQL Database, demandez à votre service informatique d’ouvrir le port 5432.</span><span class="sxs-lookup"><span data-stu-id="537fa-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="537fa-141">Obtenir les informations de connexion</span><span class="sxs-lookup"><span data-stu-id="537fa-141">Get the connection information</span></span>

<span data-ttu-id="537fa-142">Pour vous connecter à votre serveur, vous devez fournir des informations sur l’hôte et des informations d’identification pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="537fa-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="537fa-143">Le résultat est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="537fa-143">The result is in JSON format.</span></span> <span data-ttu-id="537fa-144">Prenez note des valeurs **administratorLogin** et **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="537fa-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="537fa-145">Utiliser psql pour se connecter à la base de données Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="537fa-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="537fa-146">Si PostgreSQL est installé sur votre ordinateur client, vous pouvez utiliser une instance locale de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) ou la console Azure Cloud pour vous connecter à un serveur Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="537fa-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="537fa-147">Nous allons maintenant utiliser l’utilitaire de ligne de commande psql pour nous connecter au serveur de base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="537fa-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="537fa-148">Exécutez la commande psql suivante pour vous connecter à un serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="537fa-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="537fa-149">Par exemple, la commande suivante se connecte à la base de données par défaut appelée **postgres** sur le serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès.</span><span class="sxs-lookup"><span data-stu-id="537fa-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="537fa-150">Saisissez le `<server_admin_password>` que vous avez choisi à l’invite de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="537fa-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="537fa-151">Une fois que vous êtes connecté au serveur, créez une base de données vide à l’invite.</span><span class="sxs-lookup"><span data-stu-id="537fa-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="537fa-152">À l’invite, exécutez la commande suivante pour basculer la connexion sur la base de données **mypgsqldb** nouvellement créée :</span><span class="sxs-lookup"><span data-stu-id="537fa-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="537fa-153">Créer des tables dans la base de données</span><span class="sxs-lookup"><span data-stu-id="537fa-153">Create tables in the database</span></span>
<span data-ttu-id="537fa-154">Maintenant que vous savez comment vous connecter à la base de données Azure pour PostgreSQL, nous pouvons aborder certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="537fa-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="537fa-155">Tout d’abord, nous pouvons créer une table et la charger avec des données.</span><span class="sxs-lookup"><span data-stu-id="537fa-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="537fa-156">Nous allons créer une table qui assure le suivi des informations d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="537fa-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="537fa-157">Vous pouvez localiser cette nouvelle table dans la liste des tables en tapant :</span><span class="sxs-lookup"><span data-stu-id="537fa-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="537fa-158">Charger des données dans les tables</span><span class="sxs-lookup"><span data-stu-id="537fa-158">Load data into the tables</span></span>
<span data-ttu-id="537fa-159">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="537fa-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="537fa-160">Dans la fenêtre d’invite de commandes ouverte, exécutez la requête suivante pour insérer des lignes de données.</span><span class="sxs-lookup"><span data-stu-id="537fa-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="537fa-161">Vous avez maintenant chargé deux lignes de données dans la table que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="537fa-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="537fa-162">Interroger et mettre à jour les données des tables</span><span class="sxs-lookup"><span data-stu-id="537fa-162">Query and update the data in the tables</span></span>
<span data-ttu-id="537fa-163">Exécutez la requête suivante pour récupérer des informations à partir de la table de base de données.</span><span class="sxs-lookup"><span data-stu-id="537fa-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="537fa-164">Vous pouvez également mettre à jour les données des tables.</span><span class="sxs-lookup"><span data-stu-id="537fa-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="537fa-165">La ligne est mise à jour en conséquence lorsque vous récupérez les données.</span><span class="sxs-lookup"><span data-stu-id="537fa-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="537fa-166">Restaurer une version antérieure d’une base de données</span><span class="sxs-lookup"><span data-stu-id="537fa-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="537fa-167">Imaginez que vous avez supprimé une table par inadvertance.</span><span class="sxs-lookup"><span data-stu-id="537fa-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="537fa-168">Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement.</span><span class="sxs-lookup"><span data-stu-id="537fa-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="537fa-169">La base de données Azure pour PostgreSQL vous permet de revenir à n’importe quel point dans le temps (dans la limite de 7 jours (De base) et de 35 jours (Standard)), puis d’effectuer une restauration vers un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="537fa-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="537fa-170">Vous pouvez alors utiliser ce nouveau serveur pour récupérer les données supprimées.</span><span class="sxs-lookup"><span data-stu-id="537fa-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="537fa-171">Les étapes suivantes restaurent le serveur à l’état dans lequel il était avant l’ajout de la table.</span><span class="sxs-lookup"><span data-stu-id="537fa-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="537fa-172">La commande `az postgres server restore` a besoin des paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="537fa-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="537fa-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="537fa-173">Setting</span></span> | <span data-ttu-id="537fa-174">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="537fa-174">Suggested value</span></span> | <span data-ttu-id="537fa-175">Description</span><span class="sxs-lookup"><span data-stu-id="537fa-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="537fa-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="537fa-176">--resource-group</span></span> |  <span data-ttu-id="537fa-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="537fa-177">myResourceGroup</span></span> |  <span data-ttu-id="537fa-178">Groupe de ressources dans lequel se trouve le serveur source.</span><span class="sxs-lookup"><span data-stu-id="537fa-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="537fa-179">--name</span><span class="sxs-lookup"><span data-stu-id="537fa-179">--name</span></span> | <span data-ttu-id="537fa-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="537fa-180">mypgserver-restored</span></span> | <span data-ttu-id="537fa-181">Nom du serveur créé par la commande de restauration.</span><span class="sxs-lookup"><span data-stu-id="537fa-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="537fa-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="537fa-182">restore-point-in-time</span></span> | <span data-ttu-id="537fa-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="537fa-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="537fa-184">Choisissez la date et l’heure à utiliser pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="537fa-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="537fa-185">Elles doivent être comprises dans la période de rétention de la sauvegarde du serveur source.</span><span class="sxs-lookup"><span data-stu-id="537fa-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="537fa-186">Utilisez le format de date et d’heure ISO8601.</span><span class="sxs-lookup"><span data-stu-id="537fa-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="537fa-187">Par exemple, vous pouvez utiliser votre fuseau horaire local, comme `2017-04-13T05:59:00-08:00`, ou le format UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="537fa-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="537fa-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="537fa-188">--source-server</span></span> | <span data-ttu-id="537fa-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="537fa-189">mypgserver-20170401</span></span> | <span data-ttu-id="537fa-190">Nom ou identifiant du serveur source à partir duquel la restauration s’effectuera.</span><span class="sxs-lookup"><span data-stu-id="537fa-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="537fa-191">La restauration d’un serveur à un état antérieur entraîne la création d’un nouveau serveur, copiant le serveur d’origine tel qu’il était à l’instant spécifié.</span><span class="sxs-lookup"><span data-stu-id="537fa-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="537fa-192">Les valeurs d’emplacement et de niveau tarifaire du serveur restauré sont les mêmes que celles du serveur source.</span><span class="sxs-lookup"><span data-stu-id="537fa-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="537fa-193">La commande est synchrone ; elle est renvoyée après la restauration du serveur.</span><span class="sxs-lookup"><span data-stu-id="537fa-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="537fa-194">Une fois la restauration terminée, recherchez le serveur créé.</span><span class="sxs-lookup"><span data-stu-id="537fa-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="537fa-195">Vérifiez que les données ont été restaurées comme prévu.</span><span class="sxs-lookup"><span data-stu-id="537fa-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="537fa-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="537fa-196">Next steps</span></span>
<span data-ttu-id="537fa-197">Dans ce didacticiel, vous avez appris à utiliser l’interface Azure CLI (interface de ligne de commande) et d’autres utilitaires pour :</span><span class="sxs-lookup"><span data-stu-id="537fa-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="537fa-198">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="537fa-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="537fa-199">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="537fa-199">Configure the server firewall</span></span>
> * <span data-ttu-id="537fa-200">Utiliser l’utilitaire [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="537fa-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="537fa-201">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="537fa-201">Load sample data</span></span>
> * <span data-ttu-id="537fa-202">Données de requête</span><span class="sxs-lookup"><span data-stu-id="537fa-202">Query data</span></span>
> * <span data-ttu-id="537fa-203">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="537fa-203">Update data</span></span>
> * <span data-ttu-id="537fa-204">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="537fa-204">Restore data</span></span>

<span data-ttu-id="537fa-205">À présent, découvrez comment utiliser le portail Azure pour effectuer des tâches similaires. Lisez le didacticiel [Concevoir votre première base de données Azure pour PostgreSQL à l’aide du portail Azure](tutorial-design-database-using-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="537fa-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
