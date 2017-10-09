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
# <a name="create-a-single-azure-sql-database-using-powershell"></a>Créer une base de données SQL Azure unique à l’aide de PowerShell

PowerShell est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce guide des détails à l’aide de PowerShell toodeploy une base de données SQL Azure dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans un [serveur logique de base de données SQL Azure](sql-database-features.md).

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

Ce didacticiel nécessite hello Azure PowerShell version 4.0 ou version ultérieur du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Connectez-vous tooyour abonnement Azure à l’aide de hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) des commandes et suivez hello à l’écran.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Créer des variables

Définir des variables pour une utilisation dans les scripts hello dans ce démarrage rapide.

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

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) commande. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe. Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>Création d'un serveur logique

Créer un [serveur logique de base de données SQL Azure](sql-database-features.md) à l’aide de hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) commande. Un serveur logique contient un groupe de bases de données gérées en tant que groupe. Hello exemple suivant crée un serveur nommé de façon aléatoire dans votre groupe de ressources avec une connexion d’administration nommée `ServerAdmin` et un mot de passe de `ChangeYourAdminPassword1`. Remplacez les valeurs prédéfinies par ce que vous souhaitez.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Configurer une règle de pare-feu du serveur

Créer un [règle de pare-feu de niveau serveur de base de données SQL Azure](sql-database-firewall-configure.md) à l’aide de hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) commande. Une règle de pare-feu de niveau serveur permet à une application externe, telles que SQL Server Management Studio ou hello SQLCMD utilitaire tooconnect tooa base de données SQL via le pare-feu de service de base de données SQL hello. Dans l’exemple suivant de hello, hello pare-feu est uniquement ouvert pour d’autres ressources Azure. connectivité externe tooenable, modification hello adresse tooan appropriée d’adresses IP pour votre environnement. tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> SQL Database communique par le biais du port 1433. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique s’ouvre le port 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Créer une base de données de serveur hello avec des exemples de données

Créer une base de données avec un [niveau de performance S0](sql-database-service-tiers.md) dans server hello à l’aide de hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) commande. Hello exemple suivant crée une base de données appelée `mySampleDatabase` et charges hello des exemples de données AdventureWorksLT dans cette base de données. Remplacer ces prédéfinis des valeurs comme vous le souhaitez (autres Démarrages rapides dans cette version de la collection des valeurs hello dans ce démarrage rapide).

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide. 

> [!TIP]
> Si vous prévoyez toocontinue toowork avec les Démarrages rapides suivants, ne pas nettoyer les ressources hello créés dans cette rapide démarrent. Si vous n’envisagez pas de toocontinue, utilisez hello suivant toodelete suit toutes les ressources créées par ce guide de démarrage rapide Bonjour portail Azure.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés. En savoir plus en choisissant votre outil ci-dessous :

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.JS](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

