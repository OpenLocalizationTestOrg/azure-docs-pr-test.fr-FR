---
title: "Créer une base de données Azure PostgreSQL à l’aide de hello CLI d’Azure | Documents Microsoft"
description: "Rapide toocreate du guide de démarrage et gérer la base de données Azure pour le serveur de PostgreSQL à l’aide d’Azure CLI (interface de ligne de commande)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="bd854-103">Créer une base de données Azure PostgreSQL à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="bd854-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="bd854-104">Base de données Azure pour PostgreSQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données PostgreSQL hautement disponibles dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="bd854-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="bd854-105">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="bd854-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="bd854-106">Ce démarrage rapide vous montre comment toocreate Azure de base de données pour le serveur PostgreSQL dans un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bd854-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="bd854-107">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="bd854-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bd854-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bd854-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bd854-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="bd854-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bd854-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bd854-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="bd854-111">Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello seront facturé.</span><span class="sxs-lookup"><span data-stu-id="bd854-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="bd854-112">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="bd854-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="bd854-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bd854-113">Create a resource group</span></span>

<span data-ttu-id="bd854-114">Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="bd854-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bd854-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="bd854-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="bd854-116">Hello exemple suivant crée un groupe de ressources nommé `myresourcegroup` Bonjour `westus` emplacement.</span><span class="sxs-lookup"><span data-stu-id="bd854-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="bd854-117">Créer un serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="bd854-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="bd854-118">Créer un [Azure de base de données PostgreSQL serveur](overview.md) à l’aide de hello [az postgres serveur créer](/cli/azure/postgres/server#create) commande.</span><span class="sxs-lookup"><span data-stu-id="bd854-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="bd854-119">Un serveur contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="bd854-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="bd854-120">Hello exemple suivant crée un serveur nommé `mypgserver-20170401` dans votre groupe de ressources `myresourcegroup` avec ouverture de session de serveur admin `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="bd854-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="bd854-121">Hello nom d’un serveur mappe le nom de tooDNS et est donc requis toobe globalement unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bd854-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="bd854-122">Hello de substitution `<server_admin_password>` avec votre propre valeur.</span><span class="sxs-lookup"><span data-stu-id="bd854-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="bd854-123">connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="bd854-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="bd854-124">Retenez ou enregistrez ces informations pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bd854-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="bd854-125">Par défaut, la création de la base de données **postgres** intervient sous votre serveur.</span><span class="sxs-lookup"><span data-stu-id="bd854-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="bd854-126">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de données est une base de données par défaut destinée à une utilisation par les utilisateurs, les utilitaires et les applications tierces.</span><span class="sxs-lookup"><span data-stu-id="bd854-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="bd854-127">Configurer une règle de pare-feu au niveau du serveur</span><span class="sxs-lookup"><span data-stu-id="bd854-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="bd854-128">Créer une règle de pare-feu de niveau serveur Azure PostgreSQL avec hello [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="bd854-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="bd854-129">Une règle de pare-feu de niveau serveur permet à une application externe, tel que [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/) server tooyour de tooconnect via le pare-feu de service Azure PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="bd854-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="bd854-130">Vous pouvez définir une règle de pare-feu qui couvre une tooconnect IP plage toobe en mesure de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="bd854-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="bd854-131">Hello exemple suivant utilise [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) toocreate une règle de pare-feu `AllowAllIps` plage d’adresses pour une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="bd854-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="bd854-132">tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.</span><span class="sxs-lookup"><span data-stu-id="bd854-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="bd854-133">Le serveur Azure PostgreSQL communique sur le port 5432.</span><span class="sxs-lookup"><span data-stu-id="bd854-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="bd854-134">Lorsque vous vous connectez à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 peut être bloqué par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="bd854-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="bd854-135">Avoir votre service informatique d’ouvrir le serveur de base de données SQL Azure port 5432 tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="bd854-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="bd854-136">Obtenir des informations de connexion hello</span><span class="sxs-lookup"><span data-stu-id="bd854-136">Get hello connection information</span></span>

<span data-ttu-id="bd854-137">tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="bd854-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="bd854-138">résultat de Hello est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="bd854-138">hello result is in JSON format.</span></span> <span data-ttu-id="bd854-139">Prenez note de hello **administratorLogin** et **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="bd854-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="bd854-140">Se connecter à l’aide de psql de la base de données tooPostgreSQL</span><span class="sxs-lookup"><span data-stu-id="bd854-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="bd854-141">Si votre ordinateur client a PostgreSQL installé, vous pouvez utiliser une instance locale de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL serveur.</span><span class="sxs-lookup"><span data-stu-id="bd854-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="bd854-142">Nous allons maintenant utiliser server de hello psql utilitaire de ligne de commande tooconnect toohello Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="bd854-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="bd854-143">Exécutez hello suivant psql commande tooconnect tooan Azure de base de données PostgreSQL serveur</span><span class="sxs-lookup"><span data-stu-id="bd854-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="bd854-144">Par exemple, hello commande suivante connecte à base de données de la valeur par défaut toohello appelée **postgres** sur votre serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès.</span><span class="sxs-lookup"><span data-stu-id="bd854-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="bd854-145">Entrez hello `<server_admin_password>` vous avez choisi à l’invite de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bd854-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="bd854-146">Une fois que vous êtes connecté toohello server, créez une base de données vide à l’invite de hello.</span><span class="sxs-lookup"><span data-stu-id="bd854-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="bd854-147">À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toohello nouvellement créé **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="bd854-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="bd854-148">Se connecter à l’aide de pgAdmin de la base de données tooPostgreSQL</span><span class="sxs-lookup"><span data-stu-id="bd854-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="bd854-149">tooconnect tooAzure PostgreSQL serveur à l’aide d’outil d’interface utilisateur graphique de hello _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="bd854-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="bd854-150">Lancez hello _pgAdmin_ application sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="bd854-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="bd854-151">Vous pouvez installer _pgAdmin_ à partir de http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="bd854-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="bd854-152">Choisissez **ajouter un nouveau serveur** de hello **liens rapides** menu.</span><span class="sxs-lookup"><span data-stu-id="bd854-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="bd854-153">Bonjour **Create - Server** boîte de dialogue **général** , entrez un nom convivial unique pour le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="bd854-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="bd854-154">Par exemple **Serveur Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="bd854-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="bd854-155">![Outil pgAdmin - Créer - Serveur](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="bd854-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="bd854-156">Bonjour **Create - Server** boîte de dialogue, **connexion** onglet :</span><span class="sxs-lookup"><span data-stu-id="bd854-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="bd854-157">Entrez le nom du serveur complet hello (par exemple, **mypgserver-20170401.postgres.database.azure.com**) Bonjour **nom d’hôte / adresse** boîte.</span><span class="sxs-lookup"><span data-stu-id="bd854-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="bd854-158">Entrez le port 5432 dans hello **Port** boîte.</span><span class="sxs-lookup"><span data-stu-id="bd854-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="bd854-159">Entrez hello **connexion d’administration de serveur (user@mypgserver)** obtenu précédemment dans ce démarrage rapide et un mot de passe entré lors de la création d’un serveur de hello en hello **nom d’utilisateur** et **mot de passe** zones, respectivement.</span><span class="sxs-lookup"><span data-stu-id="bd854-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="bd854-160">Sélectionnez **Requis** pour **Mode SSL**.</span><span class="sxs-lookup"><span data-stu-id="bd854-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="bd854-161">Par défaut, tous les serveurs Azure PostgreSQL sont créés avec l’application du SSL activée.</span><span class="sxs-lookup"><span data-stu-id="bd854-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="bd854-162">tooturn hors tension de l’application de SSL, consultez les détails dans [SSL de l’application](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="bd854-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - Créer - Serveur](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="bd854-164">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bd854-164">Click **Save**.</span></span>
6.  <span data-ttu-id="bd854-165">Dans le volet gauche du navigateur hello, développez hello **groupes de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="bd854-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="bd854-166">Choisissez votre serveur **Serveur Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="bd854-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="bd854-167">Choisissez hello **Server** vous connecté à, puis choisissez **bases de données** sous celle-ci.</span><span class="sxs-lookup"><span data-stu-id="bd854-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="bd854-168">Avec le bouton droit sur **bases de données** tooCreate une base de données.</span><span class="sxs-lookup"><span data-stu-id="bd854-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="bd854-169">Choisissez un nom de base de données **mypgsqldb** et propriétaire hello pour qu’il en tant que compte de connexion admin server **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="bd854-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="bd854-170">Cliquez sur **enregistrer** toocreate une base de données vide.</span><span class="sxs-lookup"><span data-stu-id="bd854-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="bd854-171">Bonjour **navigateur**, développez hello **serveurs** groupe.</span><span class="sxs-lookup"><span data-stu-id="bd854-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="bd854-172">Développez serveur hello vous avez créé et la base de données hello **mypgsqldb** sous celle-ci.</span><span class="sxs-lookup"><span data-stu-id="bd854-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="bd854-173">![pgAdmin - Créer - Base de données](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="bd854-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="bd854-174">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="bd854-174">Clean up resources</span></span>

<span data-ttu-id="bd854-175">Nettoyer toutes les ressources que vous avez créé dans démarrage rapide de hello en supprimant hello [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd854-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="bd854-176">Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="bd854-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="bd854-177">Si vous prévoyez toocontinue toowork avec ultérieures Démarrages rapides, effectuez pas nettoyer les hello ressources créées dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="bd854-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="bd854-178">Si vous n’envisagez pas de toocontinue, utilisez hello suivant les étapes toodelete toutes les ressources créées par ce démarrage rapide Bonjour CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="bd854-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="bd854-179">Si vous souhaitez simplement que toodelete hello un nouveau serveur, vous pouvez exécuter [suppression du serveur az postgres](/cli/azure/postgres/server#delete) commande.</span><span class="sxs-lookup"><span data-stu-id="bd854-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="bd854-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd854-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bd854-181">Migration de votre base de données PostgreSQL par exportation et importation</span><span class="sxs-lookup"><span data-stu-id="bd854-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
