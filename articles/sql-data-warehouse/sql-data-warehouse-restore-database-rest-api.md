---
title: "aaaRestore un entrepôt de données SQL Azure (API REST) | Documents Microsoft"
description: "Tâches d’API REST permettant de restaurer un Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Restauration d’un Azure SQL Data Warehouse (API REST)
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Portail][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Dans cet article, vous allez apprendre comment toorestore un à l’aide de l’entrepôt de données SQL Azure hello API REST.

## <a name="before-you-begin"></a>Avant de commencer
**Vérifiez votre capacité de DTU.** Chaque SQL Data Warehouse est hébergé par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota DTU par défaut.  Avant de pouvoir restaurer un entrepôt de données SQL, vérifiez que hello que votre SQL server dispose d’assez restantes du quota UDBD pour base de données hello en cours de restauration. toolearn comment toocalculate DTU nécessaire ou toorequest plus DTU, consultez [demander une modification du quota DTU][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restauration d’une base de données active ou en pause
toorestore une base de données :

1. Obtenir la liste de hello des points de restauration de base de données à l’aide d’opération de Points de restauration de base de données de Get hello.
2. Commencer la restauration à l’aide de hello [demande de restauration de base de données de création] [ Create database restore request] opération.
3. Suivi hello de la restauration à l’aide de hello [état de l’opération de base de données] [ Database operation status] opération.

> [!NOTE]
> Une fois la restauration de hello est terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>restauration d’une base de données supprimée.
toorestore une base de données supprimée :

1. Répertorier toutes les bases de données supprimées pouvant être restaurée à l’aide de hello [pouvant être restaurée de la liste des bases de données supprimées] [ List restorable dropped databases] opération.
2. Obtenir les détails de hello pour hello supprimé base de données toorestore à l’aide de hello [Get peuvent être restaurée supprimé la base de données] [ Get restorable dropped database] opération.
3. Commencer la restauration à l’aide de hello [demande de restauration de base de données de création] [ Create database restore request] opération.
4. Suivi hello de la restauration à l’aide de hello [état de l’opération de base de données] [ Database operation status] opération.

> [!NOTE]
> consultez de votre base de données après restauration de hello, tooconfigure [configurer votre base de données après récupération][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a>Étapes suivantes
toolearn sur les fonctionnalités de continuité d’activité d’entreprise hello des éditions de base de données SQL Azure, lisez hello [vue d’ensemble de base de données SQL Azure business la continuité des activités][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
