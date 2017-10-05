---
title: "Interface de ligne de commande Azure : Créer une base de données SQL | Microsoft Docs"
description: "Découvrez comment créer un serveur logique SQL Database, une règle de pare-feu de niveau serveur et des bases de données à l’aide de l’interface de ligne de commande Azure."
keywords: "didacticiel sur la base de données sql, créer une base de données sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: a735f7e6aa65ac36dc4e5a49c5a9a834be43d71a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="3e31d-104">Créer une base de données SQL Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3e31d-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="3e31d-105">L’interface de ligne de commande (CLI) Azure permet de créer et gérer des ressources Azure à partir de la ligne de commande ou dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="3e31d-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="3e31d-106">Ce guide décrit comment utiliser l’interface de ligne de commande Azure pour déployer une base de données SQL Azure dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans un [serveur logique Azure SQL Database](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="3e31d-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="3e31d-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="3e31d-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3e31d-108">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3e31d-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3e31d-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3e31d-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="3e31d-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3e31d-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="3e31d-111">Définir des variables</span><span class="sxs-lookup"><span data-stu-id="3e31d-111">Define variables</span></span>

<span data-ttu-id="3e31d-112">Définissez des variables à utiliser dans les scripts de ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="3e31d-112">Define variables for use in the scripts in this quick start.</span></span>

```azurecli-interactive
# The data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# The database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3e31d-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3e31d-113">Create a resource group</span></span>

<span data-ttu-id="3e31d-114">Créez un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3e31d-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="3e31d-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="3e31d-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="3e31d-116">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` à l’emplacement `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="3e31d-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="3e31d-117">Création d'un serveur logique</span><span class="sxs-lookup"><span data-stu-id="3e31d-117">Create a logical server</span></span>

<span data-ttu-id="3e31d-118">Créez un [serveur logique Azure SQL Database](sql-database-features.md) avec la commande [az sql server create](/cli/azure/sql/server#create).</span><span class="sxs-lookup"><span data-stu-id="3e31d-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="3e31d-119">Un serveur logique contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="3e31d-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="3e31d-120">L’exemple suivant illustre la création d’un serveur nommé de façon aléatoire dans votre groupe de ressources avec un identifiant d’administrateur nommé `ServerAdmin` et un mot de passe `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="3e31d-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="3e31d-121">Remplacez les valeurs prédéfinies par ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3e31d-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="3e31d-122">Configurer une règle de pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="3e31d-122">Configure a server firewall rule</span></span>

<span data-ttu-id="3e31d-123">Créez une [règle de pare-feu au niveau du serveur Azure SQL Database](sql-database-firewall-configure.md) avec la commande [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="3e31d-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="3e31d-124">Une règle de pare-feu au niveau du serveur permet à une application externe, telle que SQL Server Management Studio ou l’utilitaire SQLCMD, de se connecter à une base de données SQL via le pare-feu du service SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3e31d-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="3e31d-125">Dans l’exemple suivant, le pare-feu n’est ouvert qu’à d’autres ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3e31d-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="3e31d-126">Pour activer la connectivité externe, remplacez l’adresse IP par une adresse correspondant à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3e31d-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="3e31d-127">Pour ouvrir toutes les adresses IP, utilisez 0.0.0.0 comme adresse IP de début et 255.255.255.255 comme adresse de fin.</span><span class="sxs-lookup"><span data-stu-id="3e31d-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="3e31d-128">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="3e31d-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="3e31d-129">Si vous essayez de vous connecter à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 peut ne pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="3e31d-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3e31d-130">Dans ce cas, vous ne pourrez pas vous connecter à votre serveur Azure SQL Database, sauf si votre service informatique ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="3e31d-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="3e31d-131">Créer une base de données dans le serveur avec des exemples de données</span><span class="sxs-lookup"><span data-stu-id="3e31d-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="3e31d-132">Créez une base de données avec un [niveau de performance S0](sql-database-service-tiers.md) sur le serveur avec la commande [az sql db create](/cli/azure/sql/db#create).</span><span class="sxs-lookup"><span data-stu-id="3e31d-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="3e31d-133">L’exemple suivant crée une base de données appelée `mySampleDatabase` et charge les exemples de données AdventureWorksLT dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="3e31d-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="3e31d-134">Remplacez ces valeurs prédéfinies selon les besoins (les autres démarrages rapides de cette collection reposent sur les valeurs de ce démarrage rapide).</span><span class="sxs-lookup"><span data-stu-id="3e31d-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="3e31d-135">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="3e31d-135">Clean up resources</span></span>

<span data-ttu-id="3e31d-136">Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="3e31d-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="3e31d-137">Si vous souhaitez continuer à utiliser d’autres démarrages rapides, ne nettoyez pas les ressources créées dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="3e31d-137">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="3e31d-138">Sinon, procédez comme suit pour supprimer toutes les ressources créées par ce démarrage rapide dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3e31d-138">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="3e31d-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e31d-139">Next steps</span></span>

<span data-ttu-id="3e31d-140">Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés.</span><span class="sxs-lookup"><span data-stu-id="3e31d-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="3e31d-141">En savoir plus en choisissant votre outil ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3e31d-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="3e31d-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3e31d-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="3e31d-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="3e31d-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="3e31d-144">.NET</span><span class="sxs-lookup"><span data-stu-id="3e31d-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="3e31d-145">PHP</span><span class="sxs-lookup"><span data-stu-id="3e31d-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="3e31d-146">Node.JS</span><span class="sxs-lookup"><span data-stu-id="3e31d-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="3e31d-147">Java</span><span class="sxs-lookup"><span data-stu-id="3e31d-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="3e31d-148">Python</span><span class="sxs-lookup"><span data-stu-id="3e31d-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="3e31d-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="3e31d-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

