---
title: "Azure PowerShell : Créer une base de données SQL | Microsoft Docs"
description: "Découvrez comment toocreate un serveur logique de base de données SQL, les règles de pare-feu de niveau serveur et les bases de données hello portail Azure."
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
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="c91b5-104">Créer une base de données SQL Azure unique à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c91b5-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="c91b5-105">PowerShell est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="c91b5-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="c91b5-106">Ce guide des détails à l’aide de PowerShell toodeploy une base de données SQL Azure dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans un [serveur logique de base de données SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="c91b5-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="c91b5-107">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="c91b5-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="c91b5-108">Ce didacticiel nécessite hello Azure PowerShell version 4.0 ou version ultérieur du module.</span><span class="sxs-lookup"><span data-stu-id="c91b5-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="c91b5-109">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c91b5-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="c91b5-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c91b5-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="c91b5-111">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="c91b5-111">Log in tooAzure</span></span>

<span data-ttu-id="c91b5-112">Connectez-vous tooyour abonnement Azure à l’aide de hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) des commandes et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="c91b5-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="c91b5-113">Créer des variables</span><span class="sxs-lookup"><span data-stu-id="c91b5-113">Create variables</span></span>

<span data-ttu-id="c91b5-114">Définir des variables pour une utilisation dans les scripts hello dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="c91b5-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="c91b5-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c91b5-115">Create a resource group</span></span>

<span data-ttu-id="c91b5-116">Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) commande.</span><span class="sxs-lookup"><span data-stu-id="c91b5-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="c91b5-117">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="c91b5-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="c91b5-118">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement.</span><span class="sxs-lookup"><span data-stu-id="c91b5-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="c91b5-119">Création d'un serveur logique</span><span class="sxs-lookup"><span data-stu-id="c91b5-119">Create a logical server</span></span>

<span data-ttu-id="c91b5-120">Créer un [serveur logique de base de données SQL Azure](sql-database-features.md) à l’aide de hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) commande.</span><span class="sxs-lookup"><span data-stu-id="c91b5-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="c91b5-121">Un serveur logique contient un groupe de bases de données gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="c91b5-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="c91b5-122">Hello exemple suivant crée un serveur nommé de façon aléatoire dans votre groupe de ressources avec une connexion d’administration nommée `ServerAdmin` et un mot de passe de `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="c91b5-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="c91b5-123">Remplacez les valeurs prédéfinies par ce que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="c91b5-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="c91b5-124">Configurer une règle de pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="c91b5-124">Configure a server firewall rule</span></span>

<span data-ttu-id="c91b5-125">Créer un [règle de pare-feu de niveau serveur de base de données SQL Azure](sql-database-firewall-configure.md) à l’aide de hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) commande.</span><span class="sxs-lookup"><span data-stu-id="c91b5-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="c91b5-126">Une règle de pare-feu de niveau serveur permet à une application externe, telles que SQL Server Management Studio ou hello SQLCMD utilitaire tooconnect tooa base de données SQL via le pare-feu de service de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="c91b5-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="c91b5-127">Dans l’exemple suivant de hello, hello pare-feu est uniquement ouvert pour d’autres ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c91b5-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="c91b5-128">connectivité externe tooenable, modification hello adresse tooan appropriée d’adresses IP pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c91b5-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="c91b5-129">tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.</span><span class="sxs-lookup"><span data-stu-id="c91b5-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="c91b5-130">SQL Database communique par le biais du port 1433.</span><span class="sxs-lookup"><span data-stu-id="c91b5-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="c91b5-131">Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="c91b5-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c91b5-132">Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique s’ouvre le port 1433.</span><span class="sxs-lookup"><span data-stu-id="c91b5-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="c91b5-133">Créer une base de données de serveur hello avec des exemples de données</span><span class="sxs-lookup"><span data-stu-id="c91b5-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="c91b5-134">Créer une base de données avec un [niveau de performance S0](sql-database-service-tiers.md) dans server hello à l’aide de hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) commande.</span><span class="sxs-lookup"><span data-stu-id="c91b5-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="c91b5-135">Hello exemple suivant crée une base de données appelée `mySampleDatabase` et charges hello des exemples de données AdventureWorksLT dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="c91b5-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="c91b5-136">Remplacer ces prédéfinis des valeurs comme vous le souhaitez (autres Démarrages rapides dans cette version de la collection des valeurs hello dans ce démarrage rapide).</span><span class="sxs-lookup"><span data-stu-id="c91b5-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="c91b5-137">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="c91b5-137">Clean up resources</span></span>

<span data-ttu-id="c91b5-138">Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="c91b5-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="c91b5-139">Si vous prévoyez toocontinue toowork avec les Démarrages rapides suivants, ne pas nettoyer les ressources hello créés dans cette rapide démarrent.</span><span class="sxs-lookup"><span data-stu-id="c91b5-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="c91b5-140">Si vous n’envisagez pas de toocontinue, utilisez hello suivant toodelete suit toutes les ressources créées par ce guide de démarrage rapide Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c91b5-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="c91b5-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c91b5-141">Next steps</span></span>

<span data-ttu-id="c91b5-142">Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés.</span><span class="sxs-lookup"><span data-stu-id="c91b5-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="c91b5-143">En savoir plus en choisissant votre outil ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c91b5-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="c91b5-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="c91b5-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="c91b5-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c91b5-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="c91b5-146">.NET</span><span class="sxs-lookup"><span data-stu-id="c91b5-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="c91b5-147">PHP</span><span class="sxs-lookup"><span data-stu-id="c91b5-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="c91b5-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c91b5-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="c91b5-149">Java</span><span class="sxs-lookup"><span data-stu-id="c91b5-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="c91b5-150">Python</span><span class="sxs-lookup"><span data-stu-id="c91b5-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="c91b5-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="c91b5-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

