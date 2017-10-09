---
title: "aaaCreate un entrepôt de données SQL dans hello portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate un entrepôt de données SQL Azure dans hello portail Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a>Créer un Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Portail Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Ce didacticiel utilise hello toocreate portail Azure SQL Data Warehouse qui contient une base de données exemple AdventureWorksDW.

## <a name="prerequisites"></a>Composants requis
tooget démarré, vous devez :

* **Compte Azure**: visitez [d’évaluation gratuite Azure] [ Azure Free Trial] ou [des crédits Azure MSDN] [ MSDN Azure Credits] toocreate un compte.
* **Serveur SQL Azure**: consultez [créer une base de données SQL Azure avec hello portail Azure] [ Create an Azure SQL database in hello Azure portal] pour plus d’informations.

> [!NOTE]
> La création d’un entrepôt de données SQL Data Warehouse peut donner lieu à un nouveau service facturable.  Pour plus d’informations sur la tarification, consultez la page [SQL Data Warehouse Tarification][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Créer un entrepôt de données SQL
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **+Nouveau** > **Bases de données** > **SQL Data Warehouse**.

    ![Créer](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. Bonjour **SQL Data Warehouse** panneau, renseignez les informations de hello nécessaires, puis appuyez sur 'Create' toocreate.

    ![Création d’une base de données](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Serveur**: nous vous recommandons de commencer par sélectionner votre serveur.  
   * **Nom de la base de données**: nom de hello est utilisé tooreference hello SQL Data Warehouse.  Il doit être unique toohello server.
   * **Performances** : nous vous recommandons de commencer par 400 [DWU][DWU]. Vous pouvez déplacer hello toohello de curseur gauche ou avec le bouton droit tooadjust les performances de hello de votre entrepôt de données, ou de mise à l’échelle vers le haut ou vers le bas après sa création.  toolearn en savoir plus sur les Dwu, reportez-vous à notre documentation sur [mise à l’échelle](sql-data-warehouse-manage-compute-overview.md) ou notre [page de tarification][SQL Data Warehouse pricing].
   * **Abonnement**: hello sélectionnez [abonnement] qui sera facturation cet entrepôt de données SQL.
   * **Groupe de ressources**: [groupes de ressources] [ Resource group] sont toohelp conteneurs conçues vous gérez une collection de ressources Azure. En savoir plus sur les [groupes de ressources](../azure-resource-manager/resource-group-overview.md).
   * **Sélectionner une source** : cliquez sur **Sélectionner une source** > **Exemple**. Azure remplit automatiquement hello **sélectionnez exemple** option avec AdventureWorksDW.

   > [!NOTE]
   > classement par défaut de Hello pour un entrepôt de données SQL est SQL_Latin1_General_CP1_CI_AS. Si un classement différent est nécessaire, [T-SQL] [ T-SQL] peuvent être utilisés toocreate hello avec un classement différent.
   >
   >

1. Cliquez sur **créer** toocreate votre SQL Data Warehouse.
2. Patientez quelques minutes. Lorsque votre entrepôt de données est prête, vous devez être retournée toohello [portail Azure](https://portal.azure.com). Vous pouvez trouver votre entrepôt de données SQL sur votre tableau de bord, conformément à vos bases de données SQL, ou dans la ressource de hello groupe que vous avez utilisé toocreate il.

    ![vue du portail](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé un entrepôt de données SQL, vous êtes prêt trop[Connect](sql-data-warehouse-connect-overview.md) et procéder à l’interrogation.

données tooload dans l’entrepôt de données SQL, consultez hello [vue d’ensemble de chargement](sql-data-warehouse-overview-load.md).

Si vous essayez de toomigrate un tooSQL existant de la base de données l’entrepôt de données, consultez hello [présentation de la Migration](sql-data-warehouse-overview-migrate.md) ou utilisez [l’utilitaire de Migration](sql-data-warehouse-migrate-migration-utility.md).

Les règles de pare-feu peuvent également être configurées à l’aide de Transact-SQL. Pour plus d’informations, consultez [sp_set_firewall_rule][sp_set_firewall_rule] et [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Il est également un toolook idée à hello [meilleures pratiques][Best practices].

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[abonnement]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
