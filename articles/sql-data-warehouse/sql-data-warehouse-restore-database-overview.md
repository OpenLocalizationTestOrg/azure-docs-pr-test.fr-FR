---
title: "aaaRestore un entrepôt de données Azure - local et géo-redondant | Documents Microsoft"
description: "Vue d’ensemble des options de restauration de base de données hello pour récupérer une base de données dans l’entrepôt de données SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Restauration SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Portail][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL Data Warehouse propose des restaurations locales et géographiques dans le cadre de ses fonctionnalités de récupération d’urgence. Utilisez les données entrepôt sauvegardes toorestore votre entrepôt de données tooa restauration point dans la région principale de hello, ou utiliser des sauvegardes géo-redondant toorestore tooa autre région géographique. Cet article explique les spécificités de hello de restauration d’un entrepôt de données.

## <a name="what-is-a-data-warehouse-restore"></a>Qu’est-ce qu’une restauration d’entrepôt de données ?
Une restauration d’entrepôt de données est un nouvel entrepôt de données créé à partir de la sauvegarde d’un entrepôt de données existant ou supprimé. l’entrepôt de données restaurées Hello recrée l’entrepôt de données sauvegardées hello à un moment donné. Comme SQL Data Warehouse est un système distribué, une restauration d’entrepôt de données est créée à partir de nombreux fichiers de sauvegarde stockés dans des objets blob Azure. 

La restauration de base de données est une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence, dans la mesure où elle recrée vos données après des corruptions et des suppressions accidentelles.

Pour plus d'informations, consultez les pages suivantes :

* [Sauvegardes SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Vue d’ensemble de la continuité des activités](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Points de restauration SQL Data Warehouse
Un avantage de l’utilisation du stockage Azure Premium, SQL Data Warehouse utilise entrepôt de données primaire objet Blob de stockage Azure instantanés toobackup hello. Chaque instantané dispose d’un point de restauration qui représente l’heure de hello instantané hello a démarré. toorestore un entrepôt de données, vous choisissez un point de restauration et émettez une commande de restauration.  

SQL Data Warehouse restaure toujours hello tooa sauvegarde nouvel entrepôt de données. Vous pouvez conserver l’entrepôt de données restaurées hello et hello actuel ou supprimez l’un d'entre eux. Si vous souhaitez tooreplace hello actuel data warehouse avec hello restaurée de l’entrepôt de données, vous pouvez la renommer.

Si vous avez besoin de toorestore un entrepôt de données supprimées ou en pause, vous pouvez [créer un ticket de support](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Restauration géoredondante
Vous pouvez restaurer votre région tooany de l’entrepôt de données prenant en charge de l’entrepôt de données SQL Azure à un niveau de performance choisis. Veuillez noter que 9000 et 18000 DWU ne sont pas pris en charge dans toutes les régions préliminaire hello.

> [!NOTE]
> restauration tooperform une géo-redondant que vous ne devez pas avoir la participation de cette fonctionnalité.
> 
> 

## <a name="restore-timeline"></a>Chronologie de la restauration
Vous pouvez restaurer un point de restauration de base de données tooany dans hello sept derniers jours. Instantanés de toutes les quatre heures tooeight et sont disponibles pour les sept jours. Quand une capture instantanée a une ancienneté supérieure à sept jours, elle expire et son point de restauration n’est plus disponible.

## <a name="restore-costs"></a>Coûts de la restauration
frais de stockage Hello pour l’entrepôt de données restaurées hello sont facturée au tarif de stockage Azure Premium hello. 

Si vous suspendez un entrepôt de données restaurées, vous êtes facturé pour le stockage au tarif de stockage Azure Premium hello. Hello de la suspension d’avantage que vous n’êtes pas facturé pour les ressources de calcul DWU hello.

Pour plus d’informations sur la tarification de SQL Data Warehouse, consultez [SQL Data Warehouse Tarification](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Utilisations de la restauration
Hello principale utilisation de restauration de l’entrepôt de données est toorecover données après la perte accidentelle de données ou d’altération.

Vous pouvez également utiliser la restauration tooretain une sauvegarde de données entrepôt pendant plus de sept jours. Une fois la sauvegarde de hello est restaurée, vous disposez des entrepôt de données hello en ligne et pouvez la suspendre indéfiniment toosave les coûts de calcul. base de données en pause Hello entraîne des frais de stockage au tarif de stockage Azure Premium hello. 

## <a name="related-topics"></a>Rubriques connexes
### <a name="scenarios"></a>Scénarios
* Pour une vue d’ensemble de la continuité des activités, consultez [Vue d’ensemble de la continuité des activités](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

tooperform un entrepôt de données de restauration, la restauration à l’aide de :

* Azure portail, consultez [restaurer un entrepôt de données à l’aide de hello portail Azure](sql-data-warehouse-restore-database-portal.md)
* Applets de commande PowerShell : voir [Restaurer un entrepôt de données à l’aide d’applets de commande PowerShell](sql-data-warehouse-restore-database-powershell.md)
* API REST, consultez [restaurer un entrepôt de données à l’aide des API REST de hello](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
