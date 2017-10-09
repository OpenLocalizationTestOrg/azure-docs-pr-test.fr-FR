---
title: "aaaMigrate toopremium stockage de l’entrepôt de données Azure existantes | Documents Microsoft"
description: "Instructions pour la migration des données existantes de l’entrepôt de stockage de toopremium"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Migrer votre stockage de toopremium de l’entrepôt de données
Azure SQL Data Warehouse propose depuis peu le [stockage Premium pour améliorer la prévisibilité des performances][premium storage for greater performance predictability]. Les données existantes entrepôts actuellement sur le stockage standard peuvent être migré toopremium stockage. Vous pouvez tirer parti de la migration automatique, ou si vous préférez toocontrol lorsque toomigrate (qui implique aucun temps d’arrêt), vous pouvez effectuer hello migration vous-même.

Si vous avez plusieurs entrepôts de données, utilisez hello [planification de la migration automatique] [ automatic migration schedule] toodetermine lorsqu’elle est également migrée.

## <a name="determine-storage-type"></a>Déterminer le type de stockage
Si vous avez créé un entrepôt de données avant de hello suivant de dates, vous utilisez actuellement le stockage standard.

| **Région** | **Entrepôt de données créé avant cette date** |
|:--- |:--- |
| Est de l’Australie |Stockage Premium non encore disponible |
| Chine orientale |1er novembre 2016 |
| Chine du Nord |1er novembre 2016 |
| Centre de l’Allemagne |1er novembre 2016 |
| Nord-Est de l’Allemagne |1er novembre 2016 |
| Inde-Ouest |Stockage Premium non encore disponible |
| Ouest du Japon |Stockage Premium non encore disponible |
| États-Unis - partie centrale septentrionale |10 novembre 2016 |

## <a name="automatic-migration-details"></a>Détails sur la migration automatique
Par défaut, nous allons migrer votre base de données pour vous entre 6 h 00 et 6 h 00 heure locale de votre région pendant hello [planification de la migration automatique][automatic migration schedule]. Lors de la migration de hello votre entrepôt de données existant est inutilisable. migration de Hello prendra environ une heure par téraoctet de stockage par l’entrepôt de données. Vous ne serez pas facturé au cours d’une partie de la migration automatique hello.

> [!NOTE]
> Lors de la migration de hello est terminée, votre entrepôt de données sera précédent en ligne et utilisable.
>
>

Microsoft prend hello après la migration de hello toocomplete étapes (ils ne nécessitent pas d’intervention de votre part). Dans cet exemple, imaginez que votre entrepôt de données sur le stockage standard s’appelle « MyDW ».

1. Microsoft renomme « MyDW » trop « MyDW_DO_NOT_USE_ [Timestamp] ».
2. Microsoft interrompt « MyDW_ DO_NOT_USE_ [Horodatage] ». Une sauvegarde est effectuée pendant ce temps. En cas de problème, il se peut que le processus s’interrompe et se relance plusieurs fois.
3. Microsoft crée un nouvel entrepôt de données nommé « MyDW » sur le stockage premium à partir de la sauvegarde de hello effectuée à l’étape 2. « MyDW » n’apparaissent qu’après que la restauration hello est terminée.
4. Une fois hello restauré, « MyDW » renvoie toohello unités de l’entrepôt de données mêmes et l’état (actif ou en pause) où elle se trouvait avant la migration de hello.
5. Une fois la migration de hello terminée, Microsoft supprime « MyDW_DO_NOT_USE_ [Timestamp] ».

> [!NOTE]
> Hello paramètres suivants ne s’appliquent pas dans le cadre de la migration de hello :
>
> * L’audit au niveau de base de données hello doit toobe réactivé.
> * Règles de pare-feu au niveau de base de données hello doivent toobe rajouté. Règles de pare-feu au niveau du serveur hello ne sont pas affectées.
>
>

### <a name="automatic-migration-schedule"></a>Planification de la migration automatique
Migrations automatiques de se produisent entre 6 h 00 et 6 h 00 (heure locale par région) au cours de hello suivant la planification de la panne.

| **Région** | **Date de début estimée** | **Date de fin estimée** |
|:--- |:--- |:--- |
| Est de l’Australie |Pas encore déterminée |Pas encore déterminée |
| Chine orientale |9 janvier 2017 |13 janvier 2017 |
| Chine du Nord |9 janvier 2017 |13 janvier 2017 |
| Centre de l’Allemagne |9 janvier 2017 |13 janvier 2017 |
| Nord-Est de l’Allemagne |9 janvier 2017 |13 janvier 2017 |
| Inde-Ouest |Pas encore déterminée |Pas encore déterminée |
| Ouest du Japon |Pas encore déterminée |Pas encore déterminée |
| États-Unis - partie centrale septentrionale |9 janvier 2017 |13 janvier 2017 |

## <a name="self-migration-toopremium-storage"></a>Stockage de toopremium la migration automatique.
Si vous souhaitez toocontrol lorsque le temps mort se produit, vous pouvez utiliser hello suivant les étapes toomigrate un entrepôt de données existant sur toopremium de stockage standard. Si vous choisissez cette option, vous devez effectuer la migration automatique hello avant le début de la migration automatique hello dans cette région. Cela garantit que vous évitez tout risque de la migration automatique hello provoque un conflit (consultez toohello [planification de la migration automatique][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Instructions relatives à la migration ponctuelle
toomigrate vos données de l’entrepôt vous-même, utilisent hello sauvegarde et restauration fonctionnalités. partie de restauration Hello de migration de hello est attendu tootake environ une heure par téraoctet de stockage par l’entrepôt de données. Si vous souhaitez hello tookeep même nom une fois la migration terminée, suivez hello [toorename d’étapes lors de la migration][steps toorename during migration].

1. [Suspendez][Pause] votre entrepôt de données. Cela déclenche une sauvegarde automatique.
2. [Effectuez une restauration][Restore] à partir de votre instantané le plus récent.
3. Supprimez votre entrepôt de données sur le stockage standard. **Si vous ne parvenez pas toodo cette étape, vous serez facturé pour les entrepôts de données.**

> [!NOTE]
> Hello paramètres suivants ne s’appliquent pas dans le cadre de la migration de hello :
>
> * L’audit au niveau de base de données hello doit toobe réactivé.
> * Règles de pare-feu au niveau de base de données hello doivent toobe rajouté. Règles de pare-feu au niveau du serveur hello ne sont pas affectées.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Renommer l’entrepôt de données pendant la migration (facultatif)
Deux bases de données sur le même serveur logique ne peut pas avoir de hello hello le même nom. Entrepôt de données SQL prend désormais en charge la possibilité de hello toorename un entrepôt de données.

Dans cet exemple, imaginez que votre entrepôt de données sur le stockage standard s’appelle « MyDW ».

1. Renommez « MyDW » à l’aide de hello suivant de la commande ALTER DATABASE. (Dans cet exemple, nous allons renommer « MyDW_BeforeMigration ».)  Cette commande arrête toutes les transactions existantes et doit être effectuée dans toosucceed de base de données master hello.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Suspendez][Pause] « MyDW_BeforeMigration ». Cela déclenche une sauvegarde automatique.
3. [Restaurer] [ Restore] à partir d’une base de données avec le nom de hello votre instantané le plus récent, il utilisé toobe (par exemple, « MyDW »).
4. Supprimez « MyDW_BeforeMigration ». **Si vous ne parvenez pas toodo cette étape, vous serez facturé pour les entrepôts de données.**


## <a name="next-steps"></a>Étapes suivantes
Hello modifier toopremium stockage, vous avez également un nombre accru de fichiers de base de données blob dans l’architecture sous-jacente de hello de votre entrepôt de données. toomaximize des gains de performance hello de cette modification, reconstruisez les index columnstore en cluster à l’aide de hello script suivant. script de Hello fonctionne en forçant certaines de vos objets supplémentaires BLOB de données toohello existante. Si vous ne prenez aucune action, les données de salutation redistribue naturellement au fil du temps comme vous chargez davantage de données dans vos tables.

**Configuration requise :**

- Hello l’entrepôt de données doit s’exécuter avec des unités de l’entrepôt de données 1 000 ou plus (voir [montée en puissance de calcul power][scale compute power]).
- utilisateur qui exécute le script de hello Hello doit être Bonjour [mediumrc rôle] [ mediumrc role] ou une version ultérieure. tooadd un rôle d’utilisateur toothis, exécutez la commande suivante hello :````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Si vous rencontrez des problèmes avec votre entrepôt de données, [créer un ticket de support] [ create a support ticket] et faire référence à la migration toopremium « stockage » comme cause possible de hello.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
