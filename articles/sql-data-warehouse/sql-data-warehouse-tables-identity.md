---
title: "aaaCreate des clés de substitution à l’aide d’identité | Documents Microsoft"
description: "Découvrez comment clés de substitution de toocreate toouse identité sur les tables."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Créer des clés de substitution à l’aide d’IDENTITY
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Types de données][Data Types]
> * [Distribuer][Distribute]
> * [Index][Index]
> * [Partition][Partition]
> * [Statistiques][Statistics]
> * [Temporaire][Temporary]
> * [Identité][Identity]
> 
> 

Nombreux modélisateurs de données tels que les clés de substitution toocreate sur leurs tables lorsqu’ils conçoivent des modèles de l’entrepôt de données. Vous pouvez utiliser tooachieve de propriété d’identité hello cet objectif simple et efficace sans affecter les performances de chargement. 

## <a name="get-started-with-identity"></a>Prise en main d’IDENTITY
Vous pouvez définir un tableau comme propriété d’identité hello lorsque vous créez hello table à l’aide de la syntaxe similaire toohello après l’instruction :

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

Vous pouvez ensuite utiliser `INSERT..SELECT` table de hello toopopulate.

## <a name="behavior"></a>Comportement
Hello, propriété d’identité est conçue tooscale out entre toutes les distributions hello dans l’entrepôt de données hello sans affecter les performances de chargement. Par conséquent, l’implémentation hello d’identité est adaptée pour atteindre ces objectifs. Cette section met en évidence les nuances hello de hello implémentation toohelp vous comprendre de façon plus complète.  

### <a name="allocation-of-values"></a>Allocation de valeurs
Hello propriété IDENTITY ne garantit pas l’ordre hello dans le hello les valeurs de substitution sont allouées, qui reflète le comportement hello de SQL Server et la base de données SQL Azure. Toutefois, dans l’entrepôt de données SQL Azure, absence de hello d’une garantie plus marquée. 

Bonjour à l’exemple suivant est une illustration :

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

Bonjour précédent exemple, deux lignes étant récupérées de distribution 1. première ligne de Hello a la valeur de substitution de hello de 1 dans la colonne `C1`, et hello deuxième ligne a la valeur de substitution hello 61. Ces deux valeurs ont été créés par hello propriété d’identité. Toutefois, l’allocation des valeurs de hello hello n’est pas contigue. Ce comportement est normal.

### <a name="skewed-data"></a>Données décalées 
plage de Hello de valeurs pour le type de données hello sont répartis uniformément entre les distributions de hello. Si une table distribuée est données rétrécies, puis hello plage de valeurs de type de données toohello disponibles peut être épuisée prématurément. Par exemple, si toutes les données hello se termine dans une seule distribution, puis table de hello a effectivement accès tooonly-un sixième de valeurs hello hello du type de données. Pour cette raison, hello propriété d’identité est limitée trop`INT` et `BIGINT` uniquement des types de données.

### <a name="selectinto"></a>SELECT .. INTO
Lorsqu’une colonne d’identité existante est sélectionnée dans une nouvelle table, hello nouvelle colonne hérite de propriété d’identité hello, sauf si une des hello conditions suivantes est vraie :
- instruction SELECT de Hello contient une jointure.
- Plusieurs instructions SELECT sont jointes à l’aide d’UNION.
- colonne d’identité Hello est répertorié plusieurs fois dans la liste de sélection hello.
- colonne d’identité Hello fait partie d’une expression.
    
Si l’une de ces conditions est true, les colonnes hello sont créé NOT NULL au lieu d’hériter de la propriété IDENTITY hello.

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
CREATE TABLE AS sélectionnez (SACT) suit hello même comportement SQL Server est documentée pour sélectionnez... DANS. Toutefois, vous ne pouvez pas spécifier une propriété d’identité dans la définition de colonne hello Hello `CREATE TABLE` dans le cadre de l’instruction de hello. Vous ne pouvez pas utiliser fonction d’identité hello Bonjour `SELECT` dans le cadre du hello SACT. toopopulate une table, vous devez toouse `CREATE TABLE` suivi de la table de hello toodefine `INSERT..SELECT` toopopulate il.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Insérer explicitement des valeurs dans une colonne IDENTITY 
SQL Data Warehouse prend en charge la syntaxe `SET IDENTITY_INSERT <your table> ON|OFF`. Vous pouvez utiliser ce syntaxe tooexplicitly insérer les valeurs dans la colonne d’identité hello.

Nombreux modélisateurs de données comme négatif prédéfinis de toouse des valeurs pour certaines lignes dans les dimensions. Il est un exemple hello -1 ou la ligne « membre inconnu ». 

accéder au script Hello suivant montre comment tooexplicitly ajouter cette ligne à l’aide de SET IDENTITY_INSERT :

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>Charger des données dans une table avec IDENTITY

Hello la présence de hello propriété d’identité a un code de chargement de données tooyour implications. Cette section met en évidence certains modèles de base pour charger des données dans les tables à l’aide d’IDENTITY. 

### <a name="load-data-with-polybase"></a>Charger des données avec PolyBase
données tooload dans une table et générer une clé de substitution à l’aide d’identité, créer la table de hello et utiliser l’instruction INSERT... SELECT ou INSERT... VALEURS tooperform hello charge.

Hello exemple suivant met en évidence du modèle de base hello :
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> Il n’est pas possible de toouse `CREATE TABLE AS SELECT` actuellement lors du chargement des données dans une table comportant une colonne d’identité.
> 

Pour plus d’informations sur le chargement de données à l’aide d’outil de programme (BCP) copie hello en bloc, consultez hello suivant des articles :

- [Charger avec PolyBase][]
- [Meilleures pratiques pour PolyBase][]

### <a name="load-data-with-bcp"></a>Chargement des données avec BCP
BCP est un outil de ligne de commande que vous pouvez utiliser les données de tooload dans SQL Data Warehouse. Un de ses paramètres (-E) contrôles hello le comportement de l’utilitaire BCP lors du chargement des données dans une table avec une colonne d’identité. 

Si -E est spécifiée, les valeurs hello stockées dans le fichier d’entrée de hello pour la colonne de hello avec l’identité sont conservés. Si -E est *pas* spécifié, les valeurs hello dans cette colonne sont ignorées. Si la colonne d’identité hello n’est pas inclus, puis les données de salutation sont chargées normalement. les valeurs Hello sont générées en fonction de stratégie de toohello incrément et la valeur initiale de la propriété de hello.

Pour plus d’informations sur le chargement de données à l’aide de BCP, consultez hello suivant des articles :

- [Charger avec BCP][]
- [BCP dans MSDN][]

## <a name="catalog-views"></a>Affichages catalogue
Entrepôt de données SQL prend en charge hello `sys.identity_columns` vue de catalogue. Cette vue peut être utilisé tooidentify une colonne ayant la propriété d’identité hello.

toohelp vous mieux le schéma de base de données hello, cet exemple montre comment toointegrate `sys.identity_columns` avec d’autres vues de catalogue système :

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Limites
Hello, propriété d’identité ne peut pas être utilisée dans hello les scénarios suivants :
- Où le type de données de colonne hello n’est pas INT ou BIGINT
- Où hello colonne est également hello distribution clé
- Où la table de hello est une table externe 

Hello suivant des fonctions connexes n’est pas pris en charge dans SQL Data Warehouse :

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Tâches

Cette section fournit un exemple de code vous pouvez utiliser des tâches courantes de tooperform lorsque vous travaillez avec des colonnes d’identité.

> [!NOTE] 
> Colonne C1 est hello identité Bonjour toutes les tâches suivantes.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Rechercher la valeur de la plus élevée de hello allouée pour une table
Hello d’utilisation `MAX()` toodetermine hello valeur la plus élevée allouée pour une table distribuée de fonction :

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Recherchez hello départ et incrément hello propriété d’identité
Vous pouvez utiliser hello catalogue vues toodiscover hello incrément et la valeur initiale configuration valeurs d’identité pour une table à l’aide de hello suivant la requête : 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Étapes suivantes

* toolearn plus sur le développement des tables, consultez [vue d’ensemble de la Table][Overview], [des types de données de Table][Data Types], [distribuer une table] [ Distribute], [Une table d’index][Index], [partitionner une table][Partition], et [ Tables temporaires][Temporary]. 
* Pour plus d’informations sur les bonnes pratiques, consultez [Bonnes pratiques pour SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[Charger avec BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Charger avec PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Meilleures pratiques pour PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP dans MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
