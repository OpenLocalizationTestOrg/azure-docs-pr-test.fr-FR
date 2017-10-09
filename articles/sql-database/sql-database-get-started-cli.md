---
title: "Interface de ligne de commande Azure : Créer une base de données SQL | Microsoft Docs"
description: "Découvrez comment toocreate un serveur logique de base de données SQL, la règle de pare-feu de niveau serveur et bases de données à l’aide de hello CLI d’Azure."
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
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="2d026-104">Créer une seule base de données SQL Azure à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="2d026-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="2d026-105">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="2d026-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="2d026-106">Ce guide hello CLI d’Azure toodeploy en utilisant une base de données SQL Azure dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans un [serveur logique de base de données SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="2d026-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="2d026-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="2d026-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2d026-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2d026-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2d026-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="2d026-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2d026-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2d026-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="2d026-111">Définir des variables</span><span class="sxs-lookup"><span data-stu-id="2d026-111">Define variables</span></span>

<span data-ttu-id="2d026-112">Définir des variables pour une utilisation dans les scripts hello dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="2d026-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2d026-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="2d026-113">Create a resource group</span></span>

<span data-ttu-id="2d026-114">Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="2d026-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2d026-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="2d026-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="2d026-116">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement.</span><span class="sxs-lookup"><span data-stu-id="2d026-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="2d026-117">Création d'un serveur logique</span><span class="sxs-lookup"><span data-stu-id="2d026-117">Create a logical server</span></span>

<span data-ttu-id="2d026-118">Créer un [serveur logique de base de données SQL Azure](sql-database-features.md) à l’aide de hello [az sql server créer](/cli/azure/sql/server#create) commande.</span><span class="sxs-lookup"><span data-stu-id="2d026-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="2d026-119">Un serveur logique contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="2d026-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="2d026-120">Hello exemple suivant crée un serveur nommé de façon aléatoire dans votre groupe de ressources avec une connexion d’administration nommée `ServerAdmin` et un mot de passe de `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="2d026-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="2d026-121">Remplacez les valeurs prédéfinies par ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="2d026-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="2d026-122">Configurer une règle de pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="2d026-122">Configure a server firewall rule</span></span>

<span data-ttu-id="2d026-123">Créer un [règle de pare-feu de niveau serveur de base de données SQL Azure](sql-database-firewall-configure.md) à l’aide de hello [créer de pare-feu du serveur sql az](/cli/azure/sql/server/firewall-rule#create) commande.</span><span class="sxs-lookup"><span data-stu-id="2d026-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="2d026-124">Une règle de pare-feu de niveau serveur permet à une application externe, telles que SQL Server Management Studio ou hello SQLCMD utilitaire tooconnect tooa base de données SQL via le pare-feu de service de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="2d026-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="2d026-125">Dans l’exemple suivant de hello, hello pare-feu est uniquement ouvert pour d’autres ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="2d026-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="2d026-126">connectivité externe tooenable, modification hello adresse tooan appropriée d’adresses IP pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="2d026-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="2d026-127">tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.</span><span class="sxs-lookup"><span data-stu-id="2d026-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="2d026-128">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="2d026-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="2d026-129">Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="2d026-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="2d026-130">Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique s’ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="2d026-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="2d026-131">Créer une base de données de serveur hello avec des exemples de données</span><span class="sxs-lookup"><span data-stu-id="2d026-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="2d026-132">Créer une base de données avec un [niveau de performance S0](sql-database-service-tiers.md) dans server hello à l’aide de hello [créer de base de données sql az](/cli/azure/sql/db#create) commande.</span><span class="sxs-lookup"><span data-stu-id="2d026-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="2d026-133">Hello exemple suivant crée une base de données appelée `mySampleDatabase` et charges hello des exemples de données AdventureWorksLT dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="2d026-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="2d026-134">Remplacer ces prédéfinis des valeurs comme vous le souhaitez (autres Démarrages rapides dans cette version de la collection des valeurs hello dans ce démarrage rapide).</span><span class="sxs-lookup"><span data-stu-id="2d026-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="2d026-135">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="2d026-135">Clean up resources</span></span>

<span data-ttu-id="2d026-136">Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="2d026-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="2d026-137">Si vous prévoyez toocontinue toowork avec les Démarrages rapides suivants, ne pas nettoyer les ressources hello créés dans cette rapide démarrent.</span><span class="sxs-lookup"><span data-stu-id="2d026-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="2d026-138">Si vous n’envisagez pas de toocontinue, utilisez hello suivant toodelete suit toutes les ressources créées par ce guide de démarrage rapide Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d026-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="2d026-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d026-139">Next steps</span></span>

<span data-ttu-id="2d026-140">Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés.</span><span class="sxs-lookup"><span data-stu-id="2d026-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="2d026-141">En savoir plus en choisissant votre outil ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2d026-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="2d026-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="2d026-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="2d026-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2d026-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="2d026-144">.NET</span><span class="sxs-lookup"><span data-stu-id="2d026-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="2d026-145">PHP</span><span class="sxs-lookup"><span data-stu-id="2d026-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="2d026-146">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2d026-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="2d026-147">Java</span><span class="sxs-lookup"><span data-stu-id="2d026-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="2d026-148">Python</span><span class="sxs-lookup"><span data-stu-id="2d026-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="2d026-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="2d026-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

