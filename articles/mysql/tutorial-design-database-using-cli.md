---
title: "aaaDesign votre première Azure de base de données pour la base de données MySQL - CLI d’Azure | Documents Microsoft"
description: "Ce didacticiel explique comment toocreate de base de données à l’aide d’Azure CLI 2.0 à partir de la ligne de commande hello et gérer la base de données Azure pour le serveur MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="86168-103">Concevoir votre première base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="86168-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="86168-104">Base de données Azure pour MySQL est un service de base de données relationnelle Bonjour cloud de Microsoft en fonction du moteur de base de données MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="86168-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="86168-105">Dans ce didacticiel, vous utilisez Azure CLI (interface de ligne de commande) et autres toolearn utilitaires comment à :</span><span class="sxs-lookup"><span data-stu-id="86168-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="86168-106">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="86168-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="86168-107">Configurer le pare-feu du serveur hello</span><span class="sxs-lookup"><span data-stu-id="86168-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="86168-108">Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate une base de données</span><span class="sxs-lookup"><span data-stu-id="86168-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="86168-109">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="86168-109">Load sample data</span></span>
> * <span data-ttu-id="86168-110">Données de requête</span><span class="sxs-lookup"><span data-stu-id="86168-110">Query data</span></span>
> * <span data-ttu-id="86168-111">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="86168-111">Update data</span></span>
> * <span data-ttu-id="86168-112">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="86168-112">Restore data</span></span>

<span data-ttu-id="86168-113">Vous pouvez utiliser hello Azure Cloud Shell dans le navigateur de hello, ou [installer Azure CLI 2.0]( /cli/azure/install-azure-cli) sur votre propre ordinateur toorun hello les blocs de code dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="86168-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="86168-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="86168-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="86168-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="86168-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="86168-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="86168-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="86168-117">Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello existent ou sont facturé pour.</span><span class="sxs-lookup"><span data-stu-id="86168-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="86168-118">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="86168-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="86168-119">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="86168-119">Create a resource group</span></span>
<span data-ttu-id="86168-120">Créez un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="86168-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="86168-121">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="86168-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="86168-122">Hello exemple suivant crée un groupe de ressources nommé `mycliresource` Bonjour `westus` emplacement.</span><span class="sxs-lookup"><span data-stu-id="86168-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="86168-123">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="86168-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="86168-124">Créer une base de données Azure pour commande Création d’un serveur MySQL avec le serveur mysql de az hello.</span><span class="sxs-lookup"><span data-stu-id="86168-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="86168-125">Un serveur peut gérer plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="86168-125">A server can manage multiple databases.</span></span> <span data-ttu-id="86168-126">En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="86168-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="86168-127">Hello exemple suivant crée une base de données Azure pour le serveur MySQL situé dans `westus` dans le groupe de ressources hello `mycliresource` avec le nom `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="86168-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="86168-128">serveur de Hello possède un journal de l’administrateur dans nommé `myadmin` et le mot de passe `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="86168-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="86168-129">Hello serveur est créé avec **base** niveau de performances et **50** unités partagées entre toutes les bases de données hello dans le serveur de hello de calcul.</span><span class="sxs-lookup"><span data-stu-id="86168-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="86168-130">Vous pouvez faire évoluer calcul et stockage vers le haut ou vers le bas en fonction des besoins de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="86168-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="86168-131">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="86168-131">Configure firewall rule</span></span>
<span data-ttu-id="86168-132">Créer une base de données Azure pour commande de création de règle de pare-feu de niveau serveur MySQL avec hello az mysql server-règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="86168-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="86168-133">Une règle de pare-feu de niveau serveur permet à une application externe, tel que **mysql** outil de ligne de commande ou serveur de tooyour tooconnect de banc d’essai MySQL via le pare-feu de service Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="86168-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="86168-134">Hello exemple suivant crée une règle de pare-feu pour une plage d’adresses prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="86168-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="86168-135">Cet exemple montre hello ensemble possible de plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="86168-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="86168-136">Obtenir des informations de connexion hello</span><span class="sxs-lookup"><span data-stu-id="86168-136">Get hello connection information</span></span>

<span data-ttu-id="86168-137">tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="86168-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="86168-138">résultat de Hello est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="86168-138">hello result is in JSON format.</span></span> <span data-ttu-id="86168-139">Prenez note de hello **fullyQualifiedDomainName** et **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="86168-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="86168-140">Connexion serveur toohello à l’aide de mysql</span><span class="sxs-lookup"><span data-stu-id="86168-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="86168-141">Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish un tooyour de connexion de base de données Azure pour le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="86168-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="86168-142">Dans cet exemple, commande hello est :</span><span class="sxs-lookup"><span data-stu-id="86168-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="86168-143">Créer une base de données vide</span><span class="sxs-lookup"><span data-stu-id="86168-143">Create a blank database</span></span>
<span data-ttu-id="86168-144">Une fois que vous êtes connecté toohello server, créez une base de données vide.</span><span class="sxs-lookup"><span data-stu-id="86168-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="86168-145">À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch hello connexion toothis nouvellement créé :</span><span class="sxs-lookup"><span data-stu-id="86168-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="86168-146">Créer des tables dans la base de données hello</span><span class="sxs-lookup"><span data-stu-id="86168-146">Create tables in hello database</span></span>
<span data-ttu-id="86168-147">Maintenant que vous savez comment tooconnect toohello base de données Azure pour la base de données MySQL, nous pouvons sur la façon toocomplete certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="86168-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="86168-148">Tout d’abord, nous pouvons créer une table et y charger des données.</span><span class="sxs-lookup"><span data-stu-id="86168-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="86168-149">Nous allons créer une table qui stocke des données d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="86168-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="86168-150">Charger des données dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="86168-150">Load data into hello tables</span></span>
<span data-ttu-id="86168-151">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="86168-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="86168-152">Fenêtre d’invite de commandes ouverte hello, puis exécutez hello suivant requête tooinsert certaines lignes de données.</span><span class="sxs-lookup"><span data-stu-id="86168-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="86168-153">Vous avez maintenant deux lignes d’exemples de données dans la table hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="86168-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="86168-154">Interroger et mettre à jour les données hello dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="86168-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="86168-155">Exécutez hello suivant tooretrieve les informations de requête à partir de la table de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="86168-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="86168-156">Vous pouvez également mettre à jour les données hello dans les tables de hello.</span><span class="sxs-lookup"><span data-stu-id="86168-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="86168-157">ligne de Hello est mise à jour en conséquence lorsque vous récupérez des données.</span><span class="sxs-lookup"><span data-stu-id="86168-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="86168-158">Restaurer un état antérieur de tooa de base de données dans le temps</span><span class="sxs-lookup"><span data-stu-id="86168-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="86168-159">Imaginez que vous avez supprimé cette table par erreur.</span><span class="sxs-lookup"><span data-stu-id="86168-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="86168-160">Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement.</span><span class="sxs-lookup"><span data-stu-id="86168-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="86168-161">Base de données Azure pour MySQL vous permet de toogo tooany précédent point dans le temps dans hello dernière too35 jours et de restauration ce point dans le nouveau serveur de temps tooa.</span><span class="sxs-lookup"><span data-stu-id="86168-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="86168-162">Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur.</span><span class="sxs-lookup"><span data-stu-id="86168-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="86168-163">Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="86168-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="86168-164">Pourquoi restauration vous devez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="86168-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="86168-165">Point de restauration : sélectionnez un point dans le temps qui se produit avant que le serveur de hello a été modifié.</span><span class="sxs-lookup"><span data-stu-id="86168-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="86168-166">Doit être supérieure ou égale à valeur de sauvegarde plus ancienne toohello source de base de données.</span><span class="sxs-lookup"><span data-stu-id="86168-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="86168-167">Serveur cible : fournir un nouveau nom du serveur toorestore à</span><span class="sxs-lookup"><span data-stu-id="86168-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="86168-168">Serveur source : fournir nom hello du serveur hello toorestore à partir de</span><span class="sxs-lookup"><span data-stu-id="86168-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="86168-169">Emplacement : Vous ne pouvez pas sélectionner la région de hello, par défaut, il est identique au serveur de source de hello</span><span class="sxs-lookup"><span data-stu-id="86168-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="86168-170">serveur de hello toorestore et [tooa point-à-temps de restauration](./howto-restore-server-portal.md) avant hello table a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="86168-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="86168-171">Restauration d’un point différent de tooa de serveur dans le temps crée un nouveau serveur en double en tant que serveur d’origine de hello en tant que point hello dans le temps, vous spécifiez, autant qu’il soit dans la période de rétention hello pour votre [niveau de service](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="86168-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86168-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86168-172">Next Steps</span></span>
<span data-ttu-id="86168-173">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="86168-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="86168-174">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="86168-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="86168-175">Configurer le pare-feu du serveur hello</span><span class="sxs-lookup"><span data-stu-id="86168-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="86168-176">Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate une base de données</span><span class="sxs-lookup"><span data-stu-id="86168-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="86168-177">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="86168-177">Load sample data</span></span>
> * <span data-ttu-id="86168-178">Données de requête</span><span class="sxs-lookup"><span data-stu-id="86168-178">Query data</span></span>
> * <span data-ttu-id="86168-179">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="86168-179">Update data</span></span>
> * <span data-ttu-id="86168-180">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="86168-180">Restore data</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="86168-181">[Azure Database for MySQL - Azure CLI samples](./sample-scripts-azure-cli.md) (Base de données Azure pour MySQL - Exemples avec Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="86168-181">[Azure Database for MySQL - Azure CLI samples](./sample-scripts-azure-cli.md)</span></span>
