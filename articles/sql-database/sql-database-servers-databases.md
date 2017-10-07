---
title: "aaaCreate & Gérer les serveurs SQL Azure et les bases de données | Documents Microsoft"
description: "En savoir plus sur le serveur de base de données SQL Azure et les concepts de base de données et sur la création et la gestion des serveurs et bases de données à l’aide de hello portail Azure, PowerShell, hello CLI d’Azure, Transact-SQL et hello API REST."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Créer et gérer des serveurs et des bases de données Azure SQL Database

Une base de données SQL Azure est une base de données gérée dans Microsoft Azure, créée dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md). Cette base de données possède un ensemble défini de [ressources de calcul et de stockage pour différentes charges de travail](sql-database-service-tiers.md). Une base de données SQL Azure est associée à un serveur logique Azure SQL Database. Ce serveur est créé dans une région Azure spécifique. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Une base de données SQL Azure peut être une base de données unique, regroupée ou partitionnée

Une base de données SQL Azure peut être :

- Une base de données unique avec son [propre ensemble de ressources](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTU)
- Une partie d’un [pool élastique SQL](sql-database-elastic-pool.md) qui [partage un ensemble de ressources](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (eDTU)
- Une partie d’un [ensemble de bases de données partitionnées dont la taille des instances a été augmentée](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling). Il peut s’agir de bases de données uniques ou mises en pool
- Une partie d’un ensemble de bases de données participant à un [modèle de conception SaaS partagé au sein d’une architecture mutualisée ](sql-database-design-patterns-multi-tenancy-saas-applications.md), et dont les bases de données peuvent être uniques ou mises en pool (ou les deux) 

> [!TIP]
> Pour les noms de base de données valides, consultez [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données). 
>
 
- classement de base de données par défaut Hello utilisé par la base de données SQL Microsoft Azure est **SQL_LATIN1_GENERAL_CP1_CI_AS**, où **LATIN1_GENERAL** est anglais (États-Unis), **CP1** est la page de codes 1252, **CI** respecte la casse, et **AS** est sensible aux accents. Pour plus d’informations sur la façon dont tooset hello classement, consultez [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- La base de données SQL Microsoft Azure prend en charge les versions 7.3 et ultérieures du client de protocole TDS (Tabular Data Stream).
- Seules les connexions TCP/IP sont autorisées.

## <a name="what-is-an-azure-sql-logical-server"></a>Qu’est-ce qu’un serveur logique SQL Azure ?

Un serveur logique agit comme un point d’administration central pour plusieurs bases de données, y compris les [connexions](sql-database-elastic-pool.md)de [pools élastiques SQL](sql-database-manage-logins.md), les [règles de pare-feu](sql-database-firewall-configure.md), les [règles d’audit](sql-database-auditing.md), les [stratégies de détection des menaces](sql-database-threat-detection.md) et les [groupes de basculement](sql-database-geo-replication-overview.md). Un serveur logique peut se trouver dans une région différente de celle de son groupe de ressources. serveur logique de Hello doit exister avant de pouvoir créer la base de données SQL Azure hello. Toutes les bases de données sur un serveur sont créées au sein de hello même région que le serveur logique de hello. 


> [!IMPORTANT]
> Dans la base de données SQL, un serveur est une construction logique qui est différent de celui à partir d’une instance de SQL Server que vous connaissez peut-être dans Bonjour tout le monde sur site. Plus précisément, hello service de base de données SQL ne garantit pas relatif à l’emplacement des bases de données hello en relation les serveurs logiques tootheir et n’expose aucun accès au niveau de l’instance ou la fonctionnalité.
> 

Lorsque vous créez un serveur logique, vous fournissez à un serveur de compte de connexion et mot de passe avec des droits d’administration toohello base sur le serveur et toutes les bases de données créées sur ce serveur. Ce compte initial est un compte de connexion SQL. Azure SQL Database prend en charge l’authentification SQL et l’authentification Azure Active Directory. Pour en savoir plus sur les connexions et l’authentification, consultez la page [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md) (Gérer les bases de données et les connexions dans Azure SQL Database). L’authentification Windows n’est pas prise en charge. 

> [!TIP]
> Pour connaître les noms de groupe de ressources et de serveur valides, consultez la page [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom).
>

Un serveur logique de base de données Azure :

- Est créé dans un abonnement Azure, mais peuvent être déplacés avec son abonnement tooanother de relation contenant-contenu de ressources
- Est la ressource parent de hello pour les bases de données, les pools élastiques et les entrepôts de données
- Fournit un espace de noms pour les bases de données, les pools élastiques et les entrepôts de données
- Est un conteneur logique avec la sémantique de la durée de vie fort - delete Supprime un serveur et il hello des bases de données, les pools élastiques et les entrepôts de données
- Participe [le contrôle d’accès Azure en fonction du rôle (RBAC)](/active-directory/role-based-access-control-what-is) -bases de données, les pools élastiques et les entrepôts de données au sein d’un serveur d’hériter des droits d’accès du serveur de hello
- Est un élément de poids fort d’identité hello de bases de données, les pools élastiques et les entrepôts de données pour la ressource Azure à des fins de gestion (voir URL de hello schéma pour les bases de données et des pools de)
- Colocalise les ressources d’une région
- Fournit un point de terminaison de connexion pour l’accès aux bases de données (<serverName>. database.windows.net)
- Fournit des toometadata accès concernant les ressources de contenu via des vues de gestion dynamique par connexion base de données master tooa 
- Fournit la portée hello pour les stratégies de gestion qui s’appliquent les bases de données tooits - connexions, de pare-feu, d’audit, détection, etc. de la menace. 
- Est limité par un quota d’abonnement du parent hello (six serveurs par abonnement par défaut - [ici les limites d’abonnement](../azure-subscription-service-limits.md))
- Fournit des étendue hello pour le quota de base de données et du quota UDBD pour les ressources de hello qu’il contient (par exemple, DTU 45 000)
- Étendue du contrôle de version hello pour les fonctionnalités activées sur les ressources contenues 
- Les connexions principales au niveau du serveur peuvent gérer toutes les bases de données sur un serveur
- Peut contenir des connexions toothose similaires dans les instances de SQL Server dans votre environnement local qui est accordées tooone d’accès ou de plusieurs bases de données sur le serveur de hello et peut être accordés des droits d’administration limités. Pour plus d’informations, consultez [Connexions](sql-database-manage-logins.md).

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>Bases de données SQL Azure protégées par un pare-feu SQL Database

toohelp protéger vos données, un [pare-feu de base de données SQL](sql-database-firewall-configure.md) empêche le serveur de base de données de tous les accès tooyour ou l’un de ses bases de données en dehors de votre serveur toohello de connexion directement par le biais de votre connexion à un abonnement Azure. tooenable de connectivité supplémentaire, vous devez [créer une ou plusieurs règles de pare-feu](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Pour créer et gérer les pools élastiques SQL, voir [Pools élastiques](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Gérer les serveurs SQL Azure, les bases de données et les pare-feu à l’aide de hello portail Azure

Vous pouvez créer le groupe de ressources hello SQL Azure de base de données avance ou lors de la création du serveur hello lui-même. Il existe plusieurs méthodes pour l’obtention de tooa nouveau formulaire de serveur SQL, en créant un nouveau serveur SQL server ou dans le cadre de la création d’une base de données. 

### <a name="create-a-blank-sql-server-logical-server"></a>Créer un serveur SQL vide (serveur logique)

un serveur (sans une base de données) de la base de données SQL Azure à l’aide de toocreate hello [portail Azure](https://portal.azure.com), accédez de formulaire de tooa vide SQL server (serveur logique). Hello capture d’écran suivante montre une méthode d’ouverture d’un formulaire toocreate un serveur logique SQL server vide. 

   ![formulaire de création de serveur logique rempli](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Si vous obtenez le formulaire toothis à l’aide d’une autre méthode, hello plus d’informations sur le formulaire de hello sont identiques.

### <a name="create-a-blank-or-sample-sql-database"></a>Créer un exemple de base de données SQL ou une base de données SQL vide

une base de données SQL Azure à l’aide de toocreate hello [portail Azure](https://portal.azure.com), formulaire de base de données SQL vide tooa et offrent hello les informations demandées. Vous pouvez créer le groupe de ressources et le serveur logique avance ou lors de la création d’une base de données hello elle-même hello SQL Azure de base de données. Vous pouvez créer une base de données vide ou créer un exemple de base de données reposant sur Adventure Works LT. 

  ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

> [IMPORTANT] Pour plus d’informations sur la sélection hello niveau tarifaire pour votre base de données, consultez [niveaux de Service](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Gérer un serveur SQL existant

toomanage un serveur existant, accédez à serveur toohello à l’aide de plusieurs méthodes - telles que la page de base de données SQL spécifique, hello **serveurs SQL** page ou hello **toutes les ressources** page. Hello suivant capture d’écran montre comment toobegin définissant un pare-feu de niveau serveur à partir de hello **vue d’ensemble** page d’un serveur. 

   ![présentation du serveur logique](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

toomanage une base de données existant, accédez à toohello **bases de données SQL** page puis cliquez sur la base de données hello toomanage vous le souhaitez. Hello suivant capture d’écran montre comment toobegin définissant un pare-feu de niveau serveur pour une base de données à partir de hello **vue d’ensemble** page pour une base de données. 

   ![règle de pare-feu de serveur](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> propriétés de performance tooconfigure pour une base de données, consultez [niveaux de Service](sql-database-service-tiers.md).
>

> [!TIP]
> Pour un didacticiel de démarrage rapide Azure, consultez [créer une base de données SQL Azure Bonjour Azure portal](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Gérer les serveurs, les bases de données et les pare-feux SQL Azure à l’aide de PowerShell

toocreate et gérer le serveur SQL Azure, les bases de données et les pare-feu avec Azure PowerShell, utilisez hello suivant d’applets de commande PowerShell. Si vous avez besoin de tooinstall ou mise à niveau de PowerShell, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps). Pour créer et gérer les pools élastiques SQL, voir [Pools élastiques](sql-database-elastic-pool.md).

| Applet de commande | Description |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Crée une base de données |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Obtient une ou plusieurs bases de données|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Définit les propriétés d’une base de données, ou déplace une base de données existante dans un pool élastique|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Supprime une base de données|
|[New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Crée un groupe de ressources]
|[New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|Crée un serveur|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Renvoie des informations concernant les serveurs|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Modifie les propriétés d’un serveur|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Supprime un serveur|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Crée une règle de pare-feu au niveau du serveur |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Obtient les règles de pare-feu d’un serveur|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Modifie une règle de pare-feu sur un serveur|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Supprime une règle de pare-feu d’un serveur|

> [!TIP]
> Pour obtenir un didacticiel de démarrage rapide de PowerShell, consultez la page [Créer une base de données SQL Azure unique à l’aide de PowerShell](sql-database-get-started-portal.md). Pour plus d’exemples de scripts PowerShell, consultez [utiliser PowerShell toocreate SQL Azure unique de base de données et de configurer une règle de pare-feu](scripts/sql-database-create-and-configure-database-powershell.md) et [analyse et mise à l’échelle un seul SQL de la base de données à l’aide de PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Gérer les serveurs SQL Azure, les bases de données et les pare-feu à l’aide de hello CLI d’Azure

toocreate et gérer le serveur SQL Azure, les bases de données et les pare-feu avec hello [CLI d’Azure](/cli/azure/overview), utilisez hello suivante [base de données SQL Azure CLI](/cli/azure/sql/db) commandes. Hello d’utilisation [Cloud Shell](/azure/cloud-shell/overview) toorun hello CLI dans votre navigateur, ou [installer](/cli/azure/install-azure-cli) sur Windows, Linux ou macOS. Pour créer et gérer les pools élastiques SQL, voir [Pools élastiques](sql-database-elastic-pool.md).

| Applet de commande | Description |
| --- | --- |
|[az sql db create](/cli/azure/sql/db#create) |Crée une base de données|
|[az sql db list](/cli/azure/sql/db#list)|Répertorie toutes les bases de données et les entrepôts de données d’un serveur, ou toutes les bases de données d’un pool élastique|
|[az sql db list-editions](/cli/azure/sql/db#list-editions)|Répertorie les objectifs de service disponibles et les limites de stockage|
|[az sql db list-usages](/cli/azure/sql/db#list-usages)|Renvoie les données d’utilisation de la base de données|
|[az sql db show](/cli/azure/sql/db#show)|Obtient une base de données ou un entrepôt de données|
|[az sql db update](/cli/azure/sql/db#update)|Met à jour une base de données|
|[az sql db delete](/cli/azure/sql/db#delete)|Supprime une base de données|
|[az group create](/cli/azure/group#create)|Crée un groupe de ressources|
|[az sql server create](/cli/azure/sql/server#create)|Crée un serveur|
|[az sql server list](/cli/azure/sql/server#list)|Répertorie les serveurs|
|[az sql server list-usages](/cli/azure/sql/server#list-usages)|Renvoie les données d’utilisation d’un serveur|
|[az sql server show](/cli/azure/sql/server#show)|Obtient un serveur|
|[az sql server update](/cli/azure/sql/server#update)|Met à jour un serveur|
|[az sql server delete](/cli/azure/sql/server#delete)|Supprime un serveur.|
|[az sql server firewall-rule create](/cli/azure/sql/server/firewall-rule#create)|Crée la règle de pare-feu d’un serveur|
|[az sql server firewall-rule list](/cli/azure/sql/server/firewall-rule#list)|Répertorie les règles de pare-feu hello sur un serveur|
|[az sql server firewall-rule show](/cli/azure/sql/server/firewall-rule#show)|Présente les détails de hello d’une règle de pare-feu|
|[az sql server firewall-rule update](/cli/azure/sql/server/firewall-rule#update)|Met à jour une règle de pare-feu|
|[az sql server firewall-rule delete](/cli/azure/sql/server/firewall-rule#delete)|Supprime une règle de pare-feu|

> [!TIP]
> Pour un didacticiel de démarrage rapide Azure CLI, consultez [créer une seule base de données SQL Azure à l’aide de hello CLI d’Azure](sql-database-get-started-cli.md). Pour plus d’exemples de scripts CLI d’Azure, consultez [utilisez CLI toocreate SQL Azure unique de base de données et de configurer une règle de pare-feu](scripts/sql-database-create-and-configure-database-cli.md) et [utilisez CLI toomonitor et l’échelle une base de données SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Gérer les serveurs, les bases de données et les pare-feux SQL Azure à l’aide de Transact-SQL

toocreate et gérer le serveur SQL Azure, les bases de données et les pare-feu avec Transact-SQL, utilisez hello suivant de commandes T-SQL. Vous pouvez émettre ces commandes à l’aide du portail Azure, de hello [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), ou tout autre programme qui peut se connecter le serveur de base de données SQL Azure tooan et passer Transact-SQL commandes. Pour gérer des pools élastiques SQL, consultez la page [Pools élastiques](sql-database-elastic-pool.md).

> [!IMPORTANT]
> Vous ne pouvez pas créer ou supprimer un serveur à l’aide de Transact-SQL.
>

| Commande | Description |
| --- | --- |
|[CREATE DATABASE (Azure SQL Database)](/sql/t-sql/statements/create-database-azure-sql-database)|Crée une base de données. Vous devez être connecté toohello base de données master toocreate une base de données.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modifie une base de données SQL Azure. |
|[ALTER DATABASE (Azure SQL Data Warehouse)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Modifie un entrepôt de données Azure SQL Data Warehouse.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Supprime une base de données.|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retourne hello edition (niveau de service), objectif de service (niveau de tarification) et nom du pool élastique, le cas échéant, pour une base de données SQL Azure ou d’un entrepôt de données SQL Azure. Si une session toohello la base de données master sur un serveur de base de données SQL Azure, retourne des informations sur toutes les bases de données. Pour l’entrepôt de données SQL Azure, vous devez être connecté toohello de base de données master.|
|[sys.dm_db_resource_stats (Azure SQL Database)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Renvoie la consommation de mémoire, d’E/S et d’UC d’une base de données Azure SQL Database. Il existe une ligne pour toutes les 15 secondes, même s’il n’existe aucune activité dans la base de données hello.|
|[sys.resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Renvoie les données de stockage et l’utilisation d’UC pour une base de données Azure SQL Database. les données de Hello sont collectées et agrégées par intervalles de cinq minutes.|
|[sys.database_connection_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|Contient des statistiques pour les événements de connectivité de base de données SQL Database, ce qui fournit une vue d’ensemble du nombre d’échecs et de réussites de connexion de base de données. |
|[sys.event_log (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Renvoie les interblocages les échecs de connexion et les réussites de connexion de base de données Azure SQL Database. Vous pouvez utiliser cette tootrack informations ou résoudre les problèmes de votre activité de base de données avec la base de données SQL.|
|[sp_set_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Crée ou met à jour les paramètres de pare-feu de niveau serveur hello pour votre serveur de base de données SQL. Cette procédure stockée est uniquement disponible dans la connexion du principal hello base de données master toohello au niveau du serveur. Une règle de pare-feu de niveau serveur peut uniquement être créée à l’aide de Transact-SQL après que la première règle de pare-feu de niveau serveur hello a été créé par un utilisateur disposant des autorisations au niveau de Azure|
|[sys.firewall_rules (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Retourne des informations sur les paramètres de pare-feu de niveau serveur hello associés à votre base de données SQL de Microsoft Azure.|
|[sp_delete_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Supprime les paramètres de pare-feu au niveau du serveur de votre serveur SQL Database. Cette procédure stockée est uniquement disponible dans la connexion du principal hello base de données master toohello au niveau du serveur.|
|[sp_set_database_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Crée ou met à jour des règles de pare-feu de niveau base de données de hello pour votre base de données SQL Azure ou d’un entrepôt de données SQL. Les règles de pare-feu de base de données peuvent être configurées pour la base de données master hello et pour les bases de données utilisateur sur la base de données SQL. Les règles de pare-feu d’une base de données sont utiles lors de l’utilisation d’une base de données utilisateurs contenue. |
|[sys.database_firewall_rules (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Retourne des informations sur les paramètres de pare-feu de niveau base de données hello associés à votre base de données SQL de Microsoft Azure. |
|[sp_delete_database_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Supprime les paramètres de pare-feu au niveau de la base de données de votre Azure SQL Database ou de votre entrepôt de données SQL Data Warehouse. |


> [!TIP]
> Pour le didacticiel de démarrage rapide à l’aide de SQL Server Management Studio sur Microsoft Windows, consultez [base de données SQL Azure : utilisez SQL Server Management Studio tooconnect et interroger des données](sql-database-connect-query-ssms.md). Pour obtenir un didacticiel de démarrage rapide à l’aide de Visual Studio Code hello macOS, Linux ou Windows, consultez [base de données SQL Azure : utilisation de Visual Studio Code tooconnect et interroger des données](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Gérer les serveurs SQL Azure, les bases de données et les pare-feu à l’aide des API REST de hello

toocreate et gérer le serveur SQL Azure, les bases de données et les pare-feu à l’aide de hello API REST, consultez [API REST de Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Étapes suivantes

- toolearn sur le regroupement de bases de données à l’aide de pools élastiques de SQL, consultez [pools élastiques](sql-database-elastic-pool.md).
- Pour plus d’informations sur hello service de base de données SQL Azure, consultez [quelle est la base de données SQL ?](sql-database-technical-overview.md).
- toolearn sur la migration d’un tooAzure de base de données SQL Server, consultez [tooAzure SQL de base de données de migration](sql-database-cloud-migrate.md).
- Pour plus d’informations sur les fonctionnalités prises en charge, consultez la page [Fonctionnalités](sql-database-features.md).
