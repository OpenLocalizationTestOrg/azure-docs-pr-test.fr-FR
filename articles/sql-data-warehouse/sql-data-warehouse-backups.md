---
title: "sauvegardes de SQL Data Warehouse aaaAzure - captures instantanées, géo-redondant | Documents Microsoft"
description: "En savoir plus sur les sauvegardes de base de données intégrée SQL Data Warehouse qui vous permettent de toorestore un point de restauration tooa Azure SQL Data Warehouse ou une autre région géographique."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>Sauvegardes de SQL Data Warehouse
SQL Data Warehouse propose des sauvegardes locales et géographiques dans le cadre de ses fonctionnalités de sauvegarde d’entrepôt de données . Celles-ci incluent des captures instantanées Stockage Blob Azure et le stockage géoredondant. Utilisez les données entrepôt sauvegardes toorestore votre entrepôt de données tooa restauration point dans la région principale de hello ou restaurer tooa une autre région géographique. Cet article explique les spécificités de hello de sauvegardes dans l’entrepôt de données SQL.

## <a name="what-is-a-data-warehouse-backup"></a>Qu’est-ce qu’une sauvegarde d’entrepôt de données ?
Une sauvegarde de l’entrepôt de données est que vous pouvez utiliser toorestore une heure spécifique de données entrepôt tooa les données de salutation.  Comme SQL Data Warehouse est un système distribué, une sauvegarde d’entrepôt de données est constituée de nombreux fichiers qui sont stockés dans des objets blob Azure. 

Les sauvegardes de base de données sont une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence, dans la mesure où elles protègent vos données des corruptions et des suppressions accidentelles. Pour plus d’informations, consultez [Vue d’ensemble de la continuité de l’activité](../sql-database/sql-database-business-continuity.md).

## <a name="data-redundancy"></a>Redondance des données
SQL Data Warehouse protège vos données en les stockant dans un stockage Premium Azure localement redondant. Cette fonctionnalité de stockage Azure stocke plusieurs copies synchrones des données de hello hello local protection de données centre tooguarantee transparent des données s’il existe des échecs localisées. La redondance des données garantit que vos données peuvent survivre à des problèmes liés à l’infrastructure, comme des défaillances de disque. La redondance des données assure la continuité des activités avec une infrastructure hautement disponible tolérante aux pannes.

toolearn plus en détail :

* Le stockage Azure Premium, consultez [Introduction tooAzure stockage Premium](../storage/common/storage-premium-storage.md).
* Stockage localement redondant : consultez [Réplication de Stockage Azure](../storage/common/storage-redundancy.md#locally-redundant-storage).

## <a name="azure-storage-blob-snapshots"></a>Captures instantanées d’objet blob Stockage Azure
Comme un avantage de l’utilisation du stockage Azure Premium, pour SQL Data Warehouse utilise l’entrepôt de données objet Blob de stockage Azure instantanés toobackup hello localement. Vous pouvez restaurer un point de restauration de données entrepôt tooa instantané. Les captures instantanées démarrent au minimum toutes les huit heures et sont disponibles pendant sept jours.  

toolearn plus en détail :

* Captures instantanées d’objets blob Azure : consultez [Créer une capture instantanée d’objets blob](../storage/blobs/storage-blob-snapshots.md).

## <a name="geo-redundant-backups"></a>Sauvegardes géoredondantes
Toutes les 24 heures, SQL Data Warehouse stocke hello data warehouse complet dans le stockage Standard. Hello l’entrepôt de données complète est créée toomatch hello heure du dernier instantané de hello. stockage standard de Hello appartient le compte de stockage géo-redondant tooa avec un accès en lecture (RA-GRS). fonctionnalité de stockage de Azure RA-GRS Hello réplique tooa des fichiers de sauvegarde hello [centre de données associés](../best-practices-availability-paired-regions.md). Cette géo-réplication garantit que vous pouvez restaurer l’entrepôt de données au cas où vous ne peut pas accéder aux instantanés de hello dans votre région primaire. 

Cette fonctionnalité est activée par défaut. Si vous ne souhaitez pas toouse des sauvegardes géo-redondant, vous pouvez [refuser] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn). 

> [!NOTE]
> Dans le stockage Azure, terme de hello *réplication* fait référence toocopying fichiers à partir d’un emplacement tooanother. SQL *réplication de base de données* fait référence tookeeping toomultiple bases de données secondaires synchronisées avec une base de données primaire. 
> 
> 

> [!NOTE]
> Vous ne pouvez pas vous désabonner des sauvegardes géoredondantes avec les instances de 9 000 DWU et 18 000 DWU. 
>
> 

toolearn plus en détail :

* Le stockage géoredondant, consultez la section [Réplication Azure Storage](../storage/common/storage-redundancy.md).
* Le stockage RA-GRS, consultez la section [Stockage géoredondant avec accès en lecture](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>Planification et période de rétention des sauvegardes d’entrepôt de données
SQL Data Warehouse crée des instantanés sur vos entrepôts de données en ligne chaque quatre tooeight heures et conserve chaque instantané pendant sept jours. Vous pouvez restaurer votre tooone en ligne de base de données de points de restauration hello Bonjour sept derniers jours. 

toosee au démarrage de la dernière capture instantanée de hello, exécutez cette requête dans votre entrepôt de données SQL en ligne. 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

Si vous avez besoin d’un instantané de tooretain pendant plus de sept jours, vous pouvez restaurer un restauration point tooa nouvel entrepôt de données. Après la fin de la restauration de hello, SQL Data Warehouse commence à créer des instantanés de l’entrepôt de données nouvelle hello. Si vous n’apportez des modifications toohello nouvel entrepôt de données, les instantanés hello restent vides et par conséquent hello instantané coût minimal. Vous pourriez également suspendre hello tookeep de base de données SQL Data Warehouse à partir de la création d’instantanés.

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>Que passe-t-il toomy rétention des sauvegardes pendant la suspension de mon magasin de données ?
SQL Data Warehouse ne crée pas de captures instantanées et ne fait pas expirer les captures instantanées pendant la mise en suspens d’un entrepôt de données. âge de capture instantanée Hello ne change pas pendant la suspension de l’entrepôt de données hello. Rétention de l’instantané est basée sur hello nombre de jours de l’entrepôt de données hello en ligne, pas les jours calendaires.

Par exemple, si un instantané démarre octobre 1 à 16 h 00 et l’entrepôt de données hello est suspendu le 3 octobre à 16 h 00, instantané d’hello est de deux jours. Chaque fois que l’entrepôt de données hello revient en ligne instantané d’hello a deux jours. Si l’entrepôt de données hello est mis en ligne 5 octobre à 16 h 00, instantané d’hello a deux jours et reste pendant plus de cinq jours.

Lors de l’entrepôt de données hello revient en ligne, l’entrepôt de données SQL reprend les nouveaux instantanés et expire les instantanés lorsqu’ils disposent de plus de sept jours de données.

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Combien de temps est la période de rétention de hello pour un entrepôt de données supprimée ?
Lorsqu’un entrepôt de données est supprimé, hello data warehouse et les instantanés de hello sont enregistrés pendant sept jours et puis supprimés. Vous pouvez restaurer tooany de l’entrepôt de données hello hello enregistré des points de restauration.

> [!IMPORTANT]
> Si vous supprimez une instance SQL server logique, toutes les bases de données qui appartiennent toohello instance sont également supprimées et ne peuvent pas être récupérées. Vous ne pouvez pas restaurer un serveur supprimé.
> 
> 

## <a name="data-warehouse-backup-costs"></a>Coûts des sauvegardes des entrepôts de données
Hello total coût de votre entrepôt de données primaire et les sept jours d’instantanés d’objets Blob Azure est arrondi toohello to la plus proche. Par exemple, si votre entrepôt de données est 1,5 To et des captures instantanées hello utilisent 100 Go, vous êtes facturé pour 2 To de données à des taux de stockage Azure Premium. 

> [!NOTE]
> Chaque instantané est vide initialement et augmente à mesure que vous apportez à l’entrepôt de données principales modifications toohello. Toutes les captures instantanées augmentent la taille en tant que les modifications de l’entrepôt de données hello. Par conséquent, les coûts de stockage hello pour les instantanés atteindre des taux de toohello en fonction de modification.
> 
> 

Si vous utilisez le stockage géoredondant, vous payez des frais de stockage distincts. un stockage géo-redondant Hello est facturé au taux de Read-Access Geographically Redundant Storage (RA-GRS) standard hello.

Pour plus d’informations sur la tarification de SQL Data Warehouse, consultez [SQL Data Warehouse Tarification](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="using-database-backups"></a>Utilisation des sauvegardes de base de données
Hello principale utilisation de sauvegardes de l’entrepôt de données SQL est tooone de l’entrepôt de données de hello toorestore hello de points de restauration au sein de la période de rétention hello.  

* toorestore un entrepôt de données SQL, consultez [restaurer un entrepôt de données SQL](sql-data-warehouse-restore-database-overview.md).

## <a name="related-topics"></a>Rubriques connexes
### <a name="scenarios"></a>Scénarios
* Pour une vue d’ensemble de la continuité des activités, consultez [Vue d’ensemble de la continuité des activités](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* toorestore un entrepôt de données, consultez [restaurer un entrepôt de données SQL](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

