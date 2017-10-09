---
title: "Concevoir votre première base de données Azure pour PostgreSQL avec Azure CLI | Microsoft Docs"
description: "Ce didacticiel montre comment tooDesign votre première Azure de base de données PostgreSQL à l’aide de CLI d’Azure."
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
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="05704-103">Concevoir votre première base de données Azure pour PostgreSQL avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05704-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="05704-104">Dans ce didacticiel, vous utilisez Azure CLI (interface de ligne de commande) et autres toolearn utilitaires comment à :</span><span class="sxs-lookup"><span data-stu-id="05704-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="05704-105">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="05704-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="05704-106">Configurer le pare-feu du serveur hello</span><span class="sxs-lookup"><span data-stu-id="05704-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="05704-107">Utilisez [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire toocreate une base de données</span><span class="sxs-lookup"><span data-stu-id="05704-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="05704-108">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="05704-108">Load sample data</span></span>
> * <span data-ttu-id="05704-109">Données de requête</span><span class="sxs-lookup"><span data-stu-id="05704-109">Query data</span></span>
> * <span data-ttu-id="05704-110">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="05704-110">Update data</span></span>
> * <span data-ttu-id="05704-111">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="05704-111">Restore data</span></span>

<span data-ttu-id="05704-112">Vous pouvez utiliser hello Azure Cloud Shell dans le navigateur de hello, ou [installer Azure CLI 2.0]( /cli/azure/install-azure-cli) sur votre propre ordinateur toorun hello les blocs de code dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="05704-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="05704-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="05704-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="05704-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="05704-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="05704-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="05704-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="05704-116">Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello existent ou sont facturé pour.</span><span class="sxs-lookup"><span data-stu-id="05704-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="05704-117">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="05704-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="05704-118">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="05704-118">Create a resource group</span></span>
<span data-ttu-id="05704-119">Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="05704-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="05704-120">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="05704-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="05704-121">Hello exemple suivant crée un groupe de ressources nommé `myresourcegroup` Bonjour `westus` emplacement.</span><span class="sxs-lookup"><span data-stu-id="05704-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="05704-122">Créer un serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="05704-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="05704-123">Créer un [Azure de base de données PostgreSQL serveur](overview.md) à l’aide de hello [az postgres serveur créer](/cli/azure/postgres/server#create) commande.</span><span class="sxs-lookup"><span data-stu-id="05704-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="05704-124">Un serveur contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="05704-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="05704-125">Hello exemple suivant crée un serveur appelé `mypgserver-20170401` dans votre groupe de ressources `myresourcegroup` avec ouverture de session de serveur admin `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="05704-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="05704-126">Nom d’un serveur mappe le nom de tooDNS et est donc requis toobe globalement unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="05704-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="05704-127">Hello de substitution `<server_admin_password>` avec votre propre valeur.</span><span class="sxs-lookup"><span data-stu-id="05704-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="05704-128">connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="05704-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="05704-129">Retenez ou enregistrez ces informations pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="05704-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="05704-130">Par défaut, la création de la base de données **postgres** intervient sous votre serveur.</span><span class="sxs-lookup"><span data-stu-id="05704-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="05704-131">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de données est une base de données par défaut destinée à une utilisation par les utilisateurs, les utilitaires et les applications tierces.</span><span class="sxs-lookup"><span data-stu-id="05704-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="05704-132">Configurer une règle de pare-feu au niveau du serveur</span><span class="sxs-lookup"><span data-stu-id="05704-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="05704-133">Créer une règle de pare-feu de niveau serveur Azure PostgreSQL avec hello [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="05704-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="05704-134">Une règle de pare-feu de niveau serveur permet à une application externe, tel que [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/) server tooyour de tooconnect via le pare-feu de service Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="05704-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="05704-135">Vous pouvez définir une règle de pare-feu qui couvre une tooconnect IP plage toobe en mesure de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="05704-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="05704-136">Hello exemple suivant utilise [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) toocreate une règle de pare-feu `AllowAllIps` plage d’adresses pour une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="05704-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="05704-137">tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.</span><span class="sxs-lookup"><span data-stu-id="05704-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="05704-138">Le serveur Azure PostgreSQL communique sur le port 5432.</span><span class="sxs-lookup"><span data-stu-id="05704-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="05704-139">Lorsque vous vous connectez à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 peut être bloqué par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="05704-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="05704-140">Avoir votre service informatique d’ouvrir le serveur de base de données SQL Azure port 5432 tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="05704-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="05704-141">Obtenir des informations de connexion hello</span><span class="sxs-lookup"><span data-stu-id="05704-141">Get hello connection information</span></span>

<span data-ttu-id="05704-142">tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="05704-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="05704-143">résultat de Hello est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="05704-143">hello result is in JSON format.</span></span> <span data-ttu-id="05704-144">Prenez note de hello **administratorLogin** et **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="05704-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="05704-145">Se connecter tooAzure de base de données pour la base de données PostgreSQL à l’aide de psql</span><span class="sxs-lookup"><span data-stu-id="05704-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="05704-146">Si votre ordinateur client a PostgreSQL installé, vous pouvez utiliser une instance locale de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), ou le serveur Azure PostgreSQL tooan hello Azure Cloud Console tooconnect.</span><span class="sxs-lookup"><span data-stu-id="05704-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="05704-147">Nous allons maintenant utiliser hello psql utilitaire de ligne de commande tooconnect toohello Azure de base de données PostgreSQL serveur.</span><span class="sxs-lookup"><span data-stu-id="05704-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="05704-148">Exécutez hello suivant psql commande tooconnect tooan Azure de base de données PostgreSQL serveur</span><span class="sxs-lookup"><span data-stu-id="05704-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="05704-149">Par exemple, hello commande suivante connecte à base de données de la valeur par défaut toohello appelée **postgres** sur votre serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès.</span><span class="sxs-lookup"><span data-stu-id="05704-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="05704-150">Entrez hello `<server_admin_password>` vous avez choisi à l’invite de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="05704-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="05704-151">Une fois que vous êtes connecté toohello server, créez une base de données vide à l’invite de hello.</span><span class="sxs-lookup"><span data-stu-id="05704-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="05704-152">À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toohello nouvellement créé **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="05704-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="05704-153">Créer des tables dans la base de données hello</span><span class="sxs-lookup"><span data-stu-id="05704-153">Create tables in hello database</span></span>
<span data-ttu-id="05704-154">Maintenant que vous savez comment tooconnect toohello base de données Azure pour PostgreSQL, nous pouvons sur la façon toocomplete certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="05704-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="05704-155">Tout d’abord, nous pouvons créer une table et y charger des données.</span><span class="sxs-lookup"><span data-stu-id="05704-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="05704-156">Nous allons créer une table qui assure le suivi des informations d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="05704-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="05704-157">Vous pouvez voir hello nouvellement créé table dans la liste hello des tables maintenant en tapant :</span><span class="sxs-lookup"><span data-stu-id="05704-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="05704-158">Charger des données dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="05704-158">Load data into hello tables</span></span>
<span data-ttu-id="05704-159">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="05704-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="05704-160">Au niveau de la fenêtre d’invite de commandes ouverte hello, exécutez hello suivant requête tooinsert certaines lignes de données</span><span class="sxs-lookup"><span data-stu-id="05704-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="05704-161">Vous avez maintenant deux lignes d’exemples de données dans la table hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="05704-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="05704-162">Interroger et mettre à jour les données hello dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="05704-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="05704-163">Exécutez hello suivant tooretrieve les informations de requête à partir de la table de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="05704-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="05704-164">Vous pouvez également mettre à jour les données hello dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="05704-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="05704-165">ligne de Hello est mise à jour en conséquence lorsque vous récupérez des données.</span><span class="sxs-lookup"><span data-stu-id="05704-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="05704-166">Restaurer un état antérieur de tooa de base de données dans le temps</span><span class="sxs-lookup"><span data-stu-id="05704-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="05704-167">Imaginez que vous avez supprimé une table par inadvertance.</span><span class="sxs-lookup"><span data-stu-id="05704-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="05704-168">Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement.</span><span class="sxs-lookup"><span data-stu-id="05704-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="05704-169">Base de données Azure pour PostgreSQL vous permet de toogo tooany arrière dans le temps (en hello dernière too7 jours (Basic) et de 35 jours (Standard)) et de restauration ce point-à-temps tooa nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="05704-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="05704-170">Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur.</span><span class="sxs-lookup"><span data-stu-id="05704-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="05704-171">Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="05704-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="05704-172">Hello `az postgres server restore` commande doit hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="05704-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="05704-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="05704-173">Setting</span></span> | <span data-ttu-id="05704-174">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="05704-174">Suggested value</span></span> | <span data-ttu-id="05704-175">Description</span><span class="sxs-lookup"><span data-stu-id="05704-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="05704-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="05704-176">--resource-group</span></span> |  <span data-ttu-id="05704-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="05704-177">myResourceGroup</span></span> |  <span data-ttu-id="05704-178">Le groupe de ressources dans le hello serveur source existe.</span><span class="sxs-lookup"><span data-stu-id="05704-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="05704-179">--name</span><span class="sxs-lookup"><span data-stu-id="05704-179">--name</span></span> | <span data-ttu-id="05704-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="05704-180">mypgserver-restored</span></span> | <span data-ttu-id="05704-181">nom Hello hello nouveau serveur qui est créé par la commande de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="05704-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="05704-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="05704-182">restore-point-in-time</span></span> | <span data-ttu-id="05704-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="05704-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="05704-184">Sélectionnez un toorestore point-à-temps pour.</span><span class="sxs-lookup"><span data-stu-id="05704-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="05704-185">Cette date / heure doivent être au sein de la période de rétention de sauvegarde du serveur hello source.</span><span class="sxs-lookup"><span data-stu-id="05704-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="05704-186">Utilisez le format de date et d’heure ISO8601.</span><span class="sxs-lookup"><span data-stu-id="05704-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="05704-187">Par exemple, vous pouvez utiliser votre fuseau horaire local, comme `2017-04-13T05:59:00-08:00`, ou le format UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="05704-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="05704-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="05704-188">--source-server</span></span> | <span data-ttu-id="05704-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="05704-189">mypgserver-20170401</span></span> | <span data-ttu-id="05704-190">nom de Hello ou ID de hello toorestore de serveur source à partir de.</span><span class="sxs-lookup"><span data-stu-id="05704-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="05704-191">Restauration d’un serveur tooa point-à-temps crée un nouvelle copie d’un serveur, en tant que serveur d’origine de hello sous la forme hello point dans le temps que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="05704-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="05704-192">emplacement de Hello et la tarification des valeurs de niveau pour le serveur de hello restauré sont hello même en tant que serveur de source de hello.</span><span class="sxs-lookup"><span data-stu-id="05704-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="05704-193">commande Hello est synchrone et retourne une fois hello serveur est restauré.</span><span class="sxs-lookup"><span data-stu-id="05704-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="05704-194">Une fois la restauration de hello terminée, recherchez hello nouveau serveur qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="05704-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="05704-195">Vérifiez que hello données ont été restaurées comme prévu.</span><span class="sxs-lookup"><span data-stu-id="05704-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="05704-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05704-196">Next steps</span></span>
<span data-ttu-id="05704-197">Dans ce didacticiel, vous avez appris comment toouse Azure CLI (interface de ligne de commande) et d’autres utilitaires pour :</span><span class="sxs-lookup"><span data-stu-id="05704-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="05704-198">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="05704-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="05704-199">Configurer le pare-feu du serveur hello</span><span class="sxs-lookup"><span data-stu-id="05704-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="05704-200">Utilisez [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire toocreate une base de données</span><span class="sxs-lookup"><span data-stu-id="05704-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="05704-201">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="05704-201">Load sample data</span></span>
> * <span data-ttu-id="05704-202">Données de requête</span><span class="sxs-lookup"><span data-stu-id="05704-202">Query data</span></span>
> * <span data-ttu-id="05704-203">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="05704-203">Update data</span></span>
> * <span data-ttu-id="05704-204">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="05704-204">Restore data</span></span>

<span data-ttu-id="05704-205">Ensuite, découvrez comment toouse hello des tâches similaires toodo portail Azure, passez en revue ce didacticiel : [concevoir votre première base de données Azure pour à l’aide de PostgreSQL hello portail Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="05704-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
