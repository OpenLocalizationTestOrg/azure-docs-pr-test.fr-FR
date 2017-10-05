---
title: "Concevoir votre première base de données Azure pour MySQL - Azure CLI | Microsoft Docs"
description: "Ce didacticiel explique comment créer et gérer un serveur et une base de données Azure Database pour MySQL avec Azure CLI 2.0 en ligne de commande."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="0e0c1-103">Concevoir votre première base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="0e0c1-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="0e0c1-104">Azure Database pour MySQL est un service de base de données relationnelle dans le cloud de Microsoft basé sur le moteur de base de données MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="0e0c1-105">Dans ce didacticiel, vous allez utiliser l’interface Azure CLI (interface de ligne de commande) et d’autres utilitaires pour apprendre à :</span><span class="sxs-lookup"><span data-stu-id="0e0c1-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e0c1-106">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="0e0c1-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="0e0c1-107">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="0e0c1-107">Configure the server firewall</span></span>
> * <span data-ttu-id="0e0c1-108">Utiliser [l’outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="0e0c1-109">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-109">Load sample data</span></span>
> * <span data-ttu-id="0e0c1-110">Données de requête</span><span class="sxs-lookup"><span data-stu-id="0e0c1-110">Query data</span></span>
> * <span data-ttu-id="0e0c1-111">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-111">Update data</span></span>
> * <span data-ttu-id="0e0c1-112">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-112">Restore data</span></span>

<span data-ttu-id="0e0c1-113">Vous pouvez utiliser Azure Cloud Shell dans le navigateur, ou [installer Azure CLI 2.0]( /cli/azure/install-azure-cli) sur votre ordinateur pour exécuter les blocs de code de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0e0c1-114">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0e0c1-115">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="0e0c1-116">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0e0c1-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="0e0c1-117">Si vous possédez plusieurs abonnements, sélectionnez l’abonnement approprié dans lequel la ressource existe ou est facturée.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="0e0c1-118">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="0e0c1-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0e0c1-119">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0e0c1-119">Create a resource group</span></span>
<span data-ttu-id="0e0c1-120">Créez un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0e0c1-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="0e0c1-121">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="0e0c1-122">L’exemple suivant crée un groupe de ressources nommé `mycliresource` à l’emplacement `westus`.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="0e0c1-123">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="0e0c1-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="0e0c1-124">Créez un serveur Azure Database pour MySQL avec la commande az sql server create.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="0e0c1-125">Un serveur peut gérer plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-125">A server can manage multiple databases.</span></span> <span data-ttu-id="0e0c1-126">En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="0e0c1-127">L’exemple suivant crée un serveur Azure Database pour MySQL situé dans `westus` dans le groupe de ressources `mycliresource` avec le nom `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="0e0c1-128">Le serveur dispose d’une connexion administrateur avec le nom `myadmin` et le mot de passe `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="0e0c1-129">Le serveur est créé avec le niveau de performance **De base** et **50** unités de calcul partagées entre toutes les bases de données dans le serveur.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="0e0c1-130">Vous pouvez faire augmenter ou diminuer le calcul et le stockage selon les besoins de l’application.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="0e0c1-131">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="0e0c1-131">Configure firewall rule</span></span>
<span data-ttu-id="0e0c1-132">Créez une règle de pare-feu au niveau du serveur Azure Database pour MySQL avec la commande az mysql server firewall-rule create.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="0e0c1-133">Une règle de pare-feu au niveau du serveur permet à une application externe, comme l’outil de ligne de commande **mysql** ou MySQL Workbench de se connecter à votre serveur via le pare-feu du service Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="0e0c1-134">L’exemple suivant crée une règle de pare-feu pour une plage d’adresses prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="0e0c1-135">Cet exemple montre l’intégralité de la plage possible d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="0e0c1-136">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="0e0c1-136">Get the connection information</span></span>

<span data-ttu-id="0e0c1-137">Pour vous connecter à votre serveur, vous devez fournir des informations sur l’hôte et des informations d’identification pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="0e0c1-138">Le résultat est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-138">The result is in JSON format.</span></span> <span data-ttu-id="0e0c1-139">Notez les valeurs **fullyQualifiedDomainName** et **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="0e0c1-140">Se connecter au serveur à l’aide de mysql</span><span class="sxs-lookup"><span data-stu-id="0e0c1-140">Connect to the server using mysql</span></span>
<span data-ttu-id="0e0c1-141">Utilisez [l’outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) pour établir une connexion à votre serveur de base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="0e0c1-142">Dans cet exemple, la commande est :</span><span class="sxs-lookup"><span data-stu-id="0e0c1-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="0e0c1-143">Créer une base de données vide</span><span class="sxs-lookup"><span data-stu-id="0e0c1-143">Create a blank database</span></span>
<span data-ttu-id="0e0c1-144">Une fois que vous êtes connecté au serveur, créez une base de données vide.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="0e0c1-145">À l’invite, exécutez la commande suivante pour basculer la connexion sur la base de données nouvellement créée :</span><span class="sxs-lookup"><span data-stu-id="0e0c1-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="0e0c1-146">Créer des tables dans la base de données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-146">Create tables in the database</span></span>
<span data-ttu-id="0e0c1-147">Maintenant que vous savez comment vous connecter à la base de données Azure pour MySQL, nous pouvons aborder certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="0e0c1-148">Tout d’abord, nous pouvons créer une table et y charger des données.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="0e0c1-149">Nous allons créer une table qui stocke des données d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="0e0c1-150">Charger des données dans les tables</span><span class="sxs-lookup"><span data-stu-id="0e0c1-150">Load data into the tables</span></span>
<span data-ttu-id="0e0c1-151">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="0e0c1-152">Dans la fenêtre d’invite de commandes ouverte, exécutez la requête suivante pour insérer des lignes de données.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="0e0c1-153">Vous avez maintenant chargé deux lignes de données dans la table que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="0e0c1-154">Interroger et mettre à jour les données des tables</span><span class="sxs-lookup"><span data-stu-id="0e0c1-154">Query and update the data in the tables</span></span>
<span data-ttu-id="0e0c1-155">Exécutez la requête suivante pour récupérer des informations à partir de la table de base de données.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="0e0c1-156">Vous pouvez également mettre à jour les données des tables.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="0e0c1-157">La ligne est mise à jour en conséquence lorsque vous récupérez les données.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="0e0c1-158">Restaurer une version antérieure d’une base de données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="0e0c1-159">Imaginez que vous avez supprimé cette table par erreur.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="0e0c1-160">Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="0e0c1-161">La base de données Azure pour MySQL vous permet de revenir à n’importe quel moment dans le temps au cours de ces 35 derniers jours et de procéder à une restauration à ce point dans le temps vers un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="0e0c1-162">Vous pouvez alors utiliser ce nouveau serveur pour récupérer les données supprimées.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="0e0c1-163">Les étapes suivantes restaurent le serveur à l’état dans lequel il était avant l’ajout de la table.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="0e0c1-164">Pour effectuer la restauration, vous avez besoin des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0e0c1-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="0e0c1-165">Point de restauration : sélectionnez un point dans le temps avant la modification du serveur.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="0e0c1-166">Doit être supérieure ou égale à la plus ancienne valeur de sauvegarde de la base de données source.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="0e0c1-167">Serveur cible : spécifiez un nouveau nom de serveur sur lequel vous souhaitez effectuer la restauration</span><span class="sxs-lookup"><span data-stu-id="0e0c1-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="0e0c1-168">Serveur source : indiquez le nom du serveur à partir duquel vous voulez effectuer la restauration</span><span class="sxs-lookup"><span data-stu-id="0e0c1-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="0e0c1-169">Emplacement : vous ne pouvez pas sélectionner la région. Par défaut, elle est identique à celle du serveur source</span><span class="sxs-lookup"><span data-stu-id="0e0c1-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="0e0c1-170">Pour restaurer le serveur [à un point dans le temps](./howto-restore-server-portal.md) avant la suppression de la table.</span><span class="sxs-lookup"><span data-stu-id="0e0c1-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="0e0c1-171">La restauration d’un serveur à un autre point dans le temps crée un serveur en double par rapport au serveur d’origine, à condition qu’il se trouve au sein de la période de rétention de votre [niveau de service](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0e0c1-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e0c1-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e0c1-172">Next Steps</span></span>
<span data-ttu-id="0e0c1-173">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0e0c1-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="0e0c1-174">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="0e0c1-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="0e0c1-175">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="0e0c1-175">Configure the server firewall</span></span>
> * <span data-ttu-id="0e0c1-176">Utiliser [l’outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="0e0c1-177">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-177">Load sample data</span></span>
> * <span data-ttu-id="0e0c1-178">Données de requête</span><span class="sxs-lookup"><span data-stu-id="0e0c1-178">Query data</span></span>
> * <span data-ttu-id="0e0c1-179">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-179">Update data</span></span>
> * <span data-ttu-id="0e0c1-180">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="0e0c1-180">Restore data</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="0e0c1-181">[Azure Database for MySQL - Azure CLI samples](./sample-scripts-azure-cli.md) (Base de données Azure pour MySQL - Exemples avec Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="0e0c1-181">[Azure Database for MySQL - Azure CLI samples](./sample-scripts-azure-cli.md)</span></span>
