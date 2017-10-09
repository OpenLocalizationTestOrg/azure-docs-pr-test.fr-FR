---
title: "aaaCreate SQL Data Warehouse à l’aide de PowerShell | Documents Microsoft"
description: "Création de SQL Data Warehouse à l’aide de PowerShell"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>Création de SQL Data Warehouse à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Cet article vous explique comment toocreate une SQL Data Warehouse à l’aide de PowerShell.

## <a name="prerequisites"></a>Composants requis
tooget démarré, vous devez :

* **Compte Azure**: visitez [d’évaluation gratuite Azure] [ Azure Free Trial] ou [des crédits Azure MSDN] [ MSDN Azure Credits] toocreate un compte.
* **Serveur SQL Azure**: consultez [créer une base de données SQL Azure Bonjour Azure Portal] [ Create an Azure SQL database in hello Azure Portal] ou [créer une base de données SQL Azure avec PowerShell] [ Create an Azure SQL database with PowerShell] pour plus d’informations.
* **Groupe de ressources**: utilisez hello même ressource de groupe en tant que votre serveur SQL Azure, ou consultez [comment toocreate un groupe de ressources](../azure-resource-manager/resource-group-portal.md).
* **PowerShell version 1.0.3 ou supérieure** : vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name Azure**.  version la plus récente Hello peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Pour plus d’informations sur l’installation de version la plus récente hello, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> La création d’un entrepôt SQL Data Warehouse peut entraîner un nouveau service facturable.  Voir [Tarification de SQL Data Warehouse][SQL Data Warehouse pricing] pour plus d’informations sur la tarification.
>
>

## <a name="create-a-sql-data-warehouse"></a>Créer un entrepôt de données SQL
1. Ouvrez Windows PowerShell.
2. Exécutez cette tooAzure de toologin d’applet de commande Gestionnaire de ressources.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Sélectionnez hello abonnement toouse pour votre session actuelle.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Créez la base de données. Cet exemple crée une base de données nommée « mynewsqldw », avec un niveau objectif de service « DW400 », serveur toohello nommé « sqldwserver1 », qui se trouve dans le groupe de ressources hello nommé « mywesteuroperesgp1 ».

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Les paramètres obligatoires sont :

* **RequestedServiceObjectiveName**: quantité de hello [DWU] [ DWU] vous demandez.  Les valeurs prises en charge sont les suivantes : DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 et DW6000.
* **DatabaseName**: nom hello Hello SQL Data Warehouse que vous créez.
* **Nom_serveur**: nom hello du serveur hello que vous utilisez pour la création (doit être le V12).
* **ResourceGroupName**: groupe de ressources que vous utilisez.  toofind des groupes de ressources disponibles dans votre abonnement utilisent Get-AzureResource.
* **Édition**: doit être « Entrepôt de données » toocreate un entrepôt de données SQL.

Les paramètres facultatifs sont :

* **CollationName**: classement par défaut de hello si non spécifié est SQL_Latin1_General_CP1_CI_AS.  Le classement ne peut pas être modifié sur une base de données.
* **MaxSizeBytes**: taille maximale de hello par défaut d’une base de données est de 10 Go.

Pour plus d’informations sur les options de paramètre hello, consultez [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] et [créer une base de données (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Étapes suivantes
Une fois terminé votre entrepôt de données SQL de configuration vous souhaiterez peut-être tootry [le chargement des données d’exemple] [ loading sample data] ou extraire de façon trop[développer] [ develop] , [charger][load], ou [migrer][migrate].

Si vous êtes intéressé par plus d’informations sur la façon de toomanage SQL Data Warehouse par programme, consultez notre article sur la façon de toouse [applets de commande PowerShell et l’API REST][PowerShell cmdlets and REST APIs].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
