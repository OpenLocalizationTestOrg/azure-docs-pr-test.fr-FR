---
title: aaaRestore Azure SQL Data Warehouse (portail Azure) | Documents Microsoft
description: "Tâches du portail Azure permettant de restaurer Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Restauration d’Azure SQL Data Warehouse (portail)
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Portail][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
Dans cet article, vous allez apprendre comment toorestore Azure SQL Data Warehouse à l’aide de hello portail Azure.

## <a name="before-you-begin"></a>Avant de commencer
**Vérifiez votre capacité de DTU.** Chaque instance de SQL Data Warehouse est hébergée par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota d’unité de débit de données (DTU) par défaut. Avant de pouvoir restaurer SQL Data Warehouse, vérifiez que votre serveur SQL server dispose de suffisamment restantes du quota UDBD pour la base de données hello que vous restaurez. toolearn du quota UDBD toocalculate ou toorequest Udbd plus, voir [demander une modification du quota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restauration d’une base de données active ou en pause
toorestore une base de données :

1. Connectez-vous à toohello [portail Azure][Azure portal].
2. Dans le volet gauche de hello, sélectionnez **Parcourir**, puis sélectionnez **serveurs SQL**.

    ![Sélectionnez Parcourir > Serveurs SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Recherchez votre serveur et sélectionnez-le.

    ![Sélectionnez votre serveur](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Occurrence hello de l’entrepôt de données SQL que vous souhaitez toorestore à partir d’et sélectionnez.

    ![Sélectionnez l’instance hello de SQL Data Warehouse toorestore](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Haut hello du Panneau de l’entrepôt de données hello, sélectionnez **restaurer**.

    ![Sélectionnez Restaurer](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Spécifiez un nouveau **nom pour la base de données**.
7. Sélectionnez hello dernières **point de restauration**.

   Assurez-vous que vous choisissez le dernier point de restauration hello. Étant donné que les points de restauration sont affichés dans le temps universel coordonné (UTC), option par défaut de hello peut-être pas le dernier point de restauration hello.

      ![Sélectionner un point de restauration](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Sélectionnez **OK**.
9. processus de restauration de base de données Hello commence, et vous pouvez utiliser **NOTIFICATIONS** processus de hello toomonitor.

> [!NOTE]
> Après la restauration de hello terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>restauration d’une base de données supprimée.
toorestore une base de données supprimée :

1. Connectez-vous à toohello [portail Azure][Azure portal].
2. Dans le volet gauche de hello, sélectionnez **Parcourir**, puis sélectionnez **serveurs SQL**.

    ![Sélectionnez Parcourir > Serveurs SQL](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Recherchez votre serveur et sélectionnez-le.

    ![Sélectionnez votre serveur](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Faites défiler vers le bas toohello **Operations** section sur le panneau de votre serveur.
5. Sélectionnez hello **bases de données supprimées** vignette.

    ![Sélectionnez la vignette de bases de données supprimées hello](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Sélectionnez hello supprimé de la base de données que vous souhaitez toorestore.

    ![Sélectionnez un toorestore de la base de données](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Spécifiez un nouveau **nom pour la base de données**.

    ![Ajouter un nom pour la base de données hello](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Sélectionnez **OK**.
9. processus de restauration de base de données Hello commence, et vous pouvez utiliser **NOTIFICATIONS** processus de hello toomonitor.

> [!NOTE]
> reportez-vous à votre base de données après restauration de hello, tooconfigure [configurer votre base de données après récupération][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Étapes suivantes
toolearn sur les fonctionnalités de continuité d’activité d’entreprise hello des éditions de base de données SQL Azure, lisez hello [vue d’ensemble de base de données SQL Azure business la continuité des activités][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
