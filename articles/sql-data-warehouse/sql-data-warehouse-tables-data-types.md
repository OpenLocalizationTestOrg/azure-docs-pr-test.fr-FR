---
title: les types aaaData Guide - Azure SQL Data Warehouse | Documents Microsoft
description: "Recommandations de types de données de toodefine qui sont compatibles avec l’entrepôt de données SQL."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a>Conseils relatifs à la définition des types de données pour tables dans SQL Data Warehouse
Utilisez ces types de données recommandations toodefine table qui sont compatibles avec l’entrepôt de données SQL. En outre toocompatibility, en réduisant la taille de hello des types de données améliore les performances des requêtes.

Entrepôt de données SQL prend en charge les types de données hello couramment utilisé. Pour obtenir la liste des types de données hello pris en charge, consultez [des types de données](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) Bonjour l’instruction CREATE TABLE. 


## <a name="minimize-row-length"></a>Réduction de la longueur de ligne
En réduisant la taille de hello des types de données réduit la longueur de ligne hello, ce qui entraîne des performances des requêtes toobetter. Utilisez hello plus petit type de données qui fonctionne pour vos données. 

- Évitez de définir des colonnes de caractères ayant une grande longueur par défaut. Par exemple, si la valeur la plus longue hello est de 25 caractères, puis définissez votre colonne en tant que VARCHAR(25). 
- Évitez d’utiliser [NVARCHAR][NVARCHAR] lorsque vous avez uniquement besoin de VARCHAR.
- Lorsque c’est possible, utilisez NVARCHAR(4000) ou VARCHAR(8000) au lieu de NVARCHAR(MAX) ou VARCHAR(MAX).

Si vous utilisez Polybase tooload vos tables, la longueur de ligne de table hello hello défini ne peut pas dépasser 1 Mo. Lorsqu’une ligne avec les données de longueur variable dépasse 1 Mo, vous pouvez charger la ligne hello BCP, mais pas avec PolyBase.

## <a name="identify-unsupported-data-types"></a>Identification des types de données non pris en charge
Si vous migrez votre base de données à partir d’une autre base de données SQL, vous pouvez rencontrer certains types de données qui ne sont pas pris en charge sur SQL Data Warehouse. Utiliser cette requête toodiscover non pris en charge dans votre schéma SQL existant.

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a>Utilisation de solutions de contournement pour les types de données non pris en charge

Hello Voici hello des types de données SQL Data Warehouse ne prend pas en charge et donne les alternatives que vous pouvez utiliser à la place hello non pris en charge les types de données.

| Type de données non pris en charge | Solution de contournement |
| --- | --- |
| [geometry][geometry] |[varbinary][varbinary] |
| [geography][geography] |[varbinary][varbinary] |
| [hierarchyid][hierarchyid] |[nvarchar][nvarchar](4000) |
| [image][ntext,text,image] |[varbinary][varbinary] |
| [text][ntext,text,image] |[varchar][varchar] |
| [ntext][ntext,text,image] |[nvarchar][nvarchar] |
| [sql_variant][sql_variant] |Fractionnez la colonne en plusieurs colonnes fortement typées. |
| [table][table] |Convertir les tables tootemporary. |
| [timestamp][timestamp] |Retravailler code toouse [datetime2] [ datetime2] et `CURRENT_TIMESTAMP` (fonction).  Seules les constantes sont prises en charge en tant que valeurs par défaut, par conséquent le paramètre current_timestamp ne peut pas être défini comme une contrainte par défaut. Si vous avez besoin de valeurs de version de ligne de toomigrate à partir d’une colonne d’horodatage typé, utilisez [binaire][BINARY](8) ou [VARBINARY][BINARY](8) pour NOT NULL ou Valeurs de version de ligne NULL. |
| [xml][xml] |[varchar][varchar] |
| [user-defined type][user defined types] |Convertir le type de données natif toohello précédent lorsque cela est possible. |
| valeurs par défaut | Les valeurs par défaut prennent uniquement en charge des littéraux et des constantes.  Les expressions ou fonctions non déterministes comme `GETDATE()` ou `CURRENT_TIMESTAMP` ne sont pas prises en charge. |


## <a name="next-steps"></a>Étapes suivantes
toolearn, voir :

- [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices]
- [Vue d’ensemble des tables][Overview]
- [Distribution d’une table][Distribute]
- [Indexation d’une table][Index]
- [Partitionnement d’une table][Partition]
- [Gestion des statistiques d’une table][Statistics]
- [Tables temporaires][Temporary]

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
