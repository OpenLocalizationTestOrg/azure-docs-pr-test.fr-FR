---
title: "aaaCreate un entrepôt de données SQL avec TSQL | Documents Microsoft"
description: "Découvrez comment toocreate une données SQL Azure de l’entrepôt de TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Créer une base de données SQL Data Warehouse à l’aide de Transact-SQL (TSQL)
> [!div class="op_single_selector"]
> * [Portail Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Cet article vous explique comment toocreate une SQL Data Warehouse à l’aide de T-SQL.

## <a name="prerequisites"></a>Composants requis
tooget démarré, vous devez :

* **Compte Azure**: visitez [d’évaluation gratuite Azure] [ Azure Free Trial] ou [des crédits Azure MSDN] [ MSDN Azure Credits] toocreate un compte.
* **Serveur SQL Azure**: consultez [créer un serveur logique de la base de données SQL Azure avec hello Azure Portal] [créer un serveur logique de base de données SQL Azure avec hello Azure Portal] ou [créer un serveur logique de base de données SQL Azure avec PowerShell] [créer SQL Azure Serveur logique de la base de données avec PowerShell] pour plus d’informations.
* **Groupe de ressources**: utilisez hello même ressource de groupe en tant que votre serveur SQL Azure, ou consultez [comment toocreate un groupe de ressources][how toocreate a resource group].
* **Environnement tooexecute T-SQL**: vous pouvez utiliser [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], ou [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> La création d’un entrepôt SQL Data Warehouse peut entraîner un nouveau service facturable.  Voir [Tarification de SQL Data Warehouse][SQL Data Warehouse pricing] pour plus d’informations sur la tarification.
>
>

## <a name="create-a-database-with-visual-studio"></a>Créer une base de données avec Visual Studio
Si vous êtes de nouveau tooVisual Studio, voir l’article hello [requête Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, ouvrez l’Explorateur d’objets SQL Server dans Visual Studio et connectez toohello serveur qui hébergera la base de données SQL Data Warehouse.  Une fois connecté, vous pouvez créer un entrepôt de données SQL en exécutant hello suivant de commande SQL hello **master** base de données.  Cette commande crée la base de données de hello MySqlDwDb avec un objectif de Service de DW400 et autoriser hello de base de données toogrow tooa taille maximale de 10 To.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Créer une base de données avec sqlcmd
Vous pouvez également exécuter hello même commande avec sqlcmd en exécutant hello suite à une invite de commandes.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

classement par défaut de Hello lorsque ne pas spécifié est SQL_Latin1_General_CP1_CI_AS de COLLATE.  Hello `MAXSIZE` entre 250 Go et to 240.  Hello `SERVICE_OBJECTIVE` peut être comprise entre DW100 et DW2000 [DWU][DWU].  Pour obtenir la liste de toutes les valeurs valides, consultez la documentation MSDN pour hello [CREATE DATABASE][CREATE DATABASE].  Hello MAXSIZE et peut SERVICE_OBJECTIVE être modifié avec un [ALTER DATABASE] [ ALTER DATABASE] commande T-SQL.  classement de Hello d’une base de données ne peut pas être modifié après sa création.   Soyez vigilant lors de la modification hello SERVICE_OBJECTIVE modification DWU provoque un redémarrage des services, ce qui annule toutes les requêtes en vol.  La modification du paramètre MAXSIZE ne redémarre pas les services car il s’agit d’une simple opération de métadonnées.

## <a name="next-steps"></a>Étapes suivantes
Une fois votre entrepôt de données SQL a terminé, vous pouvez l’approvisionnement [charger les données d’exemple] [ load sample data] ou extraire de façon trop[développer][develop], [charger][load], ou [migrer][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
