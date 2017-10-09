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
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="f39c4-103">Conseils relatifs à la définition des types de données pour tables dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f39c4-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="f39c4-104">Utilisez ces types de données recommandations toodefine table qui sont compatibles avec l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f39c4-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="f39c4-105">En outre toocompatibility, en réduisant la taille de hello des types de données améliore les performances des requêtes.</span><span class="sxs-lookup"><span data-stu-id="f39c4-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="f39c4-106">Entrepôt de données SQL prend en charge les types de données hello couramment utilisé.</span><span class="sxs-lookup"><span data-stu-id="f39c4-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="f39c4-107">Pour obtenir la liste des types de données hello pris en charge, consultez [des types de données](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) Bonjour l’instruction CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="f39c4-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="f39c4-108">Réduction de la longueur de ligne</span><span class="sxs-lookup"><span data-stu-id="f39c4-108">Minimize row length</span></span>
<span data-ttu-id="f39c4-109">En réduisant la taille de hello des types de données réduit la longueur de ligne hello, ce qui entraîne des performances des requêtes toobetter.</span><span class="sxs-lookup"><span data-stu-id="f39c4-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="f39c4-110">Utilisez hello plus petit type de données qui fonctionne pour vos données.</span><span class="sxs-lookup"><span data-stu-id="f39c4-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="f39c4-111">Évitez de définir des colonnes de caractères ayant une grande longueur par défaut.</span><span class="sxs-lookup"><span data-stu-id="f39c4-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="f39c4-112">Par exemple, si la valeur la plus longue hello est de 25 caractères, puis définissez votre colonne en tant que VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="f39c4-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="f39c4-113">Évitez d’utiliser [NVARCHAR][NVARCHAR] lorsque vous avez uniquement besoin de VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="f39c4-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="f39c4-114">Lorsque c’est possible, utilisez NVARCHAR(4000) ou VARCHAR(8000) au lieu de NVARCHAR(MAX) ou VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="f39c4-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="f39c4-115">Si vous utilisez Polybase tooload vos tables, la longueur de ligne de table hello hello défini ne peut pas dépasser 1 Mo.</span><span class="sxs-lookup"><span data-stu-id="f39c4-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="f39c4-116">Lorsqu’une ligne avec les données de longueur variable dépasse 1 Mo, vous pouvez charger la ligne hello BCP, mais pas avec PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f39c4-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="f39c4-117">Identification des types de données non pris en charge</span><span class="sxs-lookup"><span data-stu-id="f39c4-117">Identify unsupported data types</span></span>
<span data-ttu-id="f39c4-118">Si vous migrez votre base de données à partir d’une autre base de données SQL, vous pouvez rencontrer certains types de données qui ne sont pas pris en charge sur SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f39c4-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="f39c4-119">Utiliser cette requête toodiscover non pris en charge dans votre schéma SQL existant.</span><span class="sxs-lookup"><span data-stu-id="f39c4-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="f39c4-120"><a name="unsupported-data-types"></a>Utilisation de solutions de contournement pour les types de données non pris en charge</span><span class="sxs-lookup"><span data-stu-id="f39c4-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="f39c4-121">Hello Voici hello des types de données SQL Data Warehouse ne prend pas en charge et donne les alternatives que vous pouvez utiliser à la place hello non pris en charge les types de données.</span><span class="sxs-lookup"><span data-stu-id="f39c4-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="f39c4-122">Type de données non pris en charge</span><span class="sxs-lookup"><span data-stu-id="f39c4-122">Unsupported data type</span></span> | <span data-ttu-id="f39c4-123">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="f39c4-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="f39c4-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="f39c4-124">[geometry][geometry]</span></span> |<span data-ttu-id="f39c4-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f39c4-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f39c4-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="f39c4-126">[geography][geography]</span></span> |<span data-ttu-id="f39c4-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f39c4-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f39c4-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="f39c4-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="f39c4-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="f39c4-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="f39c4-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="f39c4-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="f39c4-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="f39c4-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="f39c4-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="f39c4-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="f39c4-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="f39c4-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="f39c4-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="f39c4-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="f39c4-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="f39c4-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="f39c4-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="f39c4-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="f39c4-137">Fractionnez la colonne en plusieurs colonnes fortement typées.</span><span class="sxs-lookup"><span data-stu-id="f39c4-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="f39c4-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="f39c4-138">[table][table]</span></span> |<span data-ttu-id="f39c4-139">Convertir les tables tootemporary.</span><span class="sxs-lookup"><span data-stu-id="f39c4-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="f39c4-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="f39c4-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="f39c4-141">Retravailler code toouse [datetime2] [ datetime2] et `CURRENT_TIMESTAMP` (fonction).</span><span class="sxs-lookup"><span data-stu-id="f39c4-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="f39c4-142">Seules les constantes sont prises en charge en tant que valeurs par défaut, par conséquent le paramètre current_timestamp ne peut pas être défini comme une contrainte par défaut.</span><span class="sxs-lookup"><span data-stu-id="f39c4-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="f39c4-143">Si vous avez besoin de valeurs de version de ligne de toomigrate à partir d’une colonne d’horodatage typé, utilisez [binaire][BINARY](8) ou [VARBINARY][BINARY](8) pour NOT NULL ou Valeurs de version de ligne NULL.</span><span class="sxs-lookup"><span data-stu-id="f39c4-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="f39c4-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="f39c4-144">[xml][xml]</span></span> |<span data-ttu-id="f39c4-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="f39c4-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="f39c4-146">[user-defined type][user defined types]</span><span class="sxs-lookup"><span data-stu-id="f39c4-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="f39c4-147">Convertir le type de données natif toohello précédent lorsque cela est possible.</span><span class="sxs-lookup"><span data-stu-id="f39c4-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="f39c4-148">valeurs par défaut</span><span class="sxs-lookup"><span data-stu-id="f39c4-148">default values</span></span> | <span data-ttu-id="f39c4-149">Les valeurs par défaut prennent uniquement en charge des littéraux et des constantes.</span><span class="sxs-lookup"><span data-stu-id="f39c4-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="f39c4-150">Les expressions ou fonctions non déterministes comme `GETDATE()` ou `CURRENT_TIMESTAMP` ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f39c4-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f39c4-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f39c4-151">Next steps</span></span>
<span data-ttu-id="f39c4-152">toolearn, voir :</span><span class="sxs-lookup"><span data-stu-id="f39c4-152">toolearn more, see:</span></span>

- <span data-ttu-id="f39c4-153">[Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="f39c4-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="f39c4-154">[Vue d’ensemble des tables][Overview]</span><span class="sxs-lookup"><span data-stu-id="f39c4-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="f39c4-155">[Distribution d’une table][Distribute]</span><span class="sxs-lookup"><span data-stu-id="f39c4-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="f39c4-156">[Indexation d’une table][Index]</span><span class="sxs-lookup"><span data-stu-id="f39c4-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="f39c4-157">[Partitionnement d’une table][Partition]</span><span class="sxs-lookup"><span data-stu-id="f39c4-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="f39c4-158">[Gestion des statistiques d’une table][Statistics]</span><span class="sxs-lookup"><span data-stu-id="f39c4-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="f39c4-159">[Tables temporaires][Temporary]</span><span class="sxs-lookup"><span data-stu-id="f39c4-159">[Temporary Tables][Temporary]</span></span>

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
