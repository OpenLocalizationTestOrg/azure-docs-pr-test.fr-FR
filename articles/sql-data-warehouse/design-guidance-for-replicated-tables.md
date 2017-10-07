---
title: "conseils d’aaaDesign pour les tables répliquées - Azure SQL Data Warehouse | Documents Microsoft"
description: "Recommandations relatives à la conception de tables répliquées dans votre schéma Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>Guide de conception pour l’utilisation de tables répliquées dans Azure SQL Data Warehouse
Cet article vous fournit des recommandations relatives à la conception de tables répliquées dans votre schéma SQL Data Warehouse. Utilisez ces performances des requêtes tooimprove recommandations en réduisant la complexité de requête et de déplacement des données.

> [!NOTE]
> fonctionnalité de table répliquée Hello n’est actuellement en version préliminaire publique. Certains comportements sont toochange de sujet.
> 

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous êtes familiarisé avec les concepts de distribution et de déplacement des données dans SQL Data Warehouse.  Pour plus d’informations, consultez [Données distribuées](sql-data-warehouse-distributed-data.md). 

Dans le cadre de la création de table, comprendre autant que possible sur vos données et la façon dont les données de salutation sont interrogées.  Considérez par exemple les questions suivantes :

- La taille est la table de hello ?   
- La fréquence d’actualisation de table de hello   
- Est-ce que je dispose de tables de faits et de dimension dans un entrepôt de données ?   

## <a name="what-is-a-replicated-table"></a>Qu’est-ce qu’une table répliquée ?
Une table répliquée possède une copie complète de la table hello accessible sur chaque nœud de calcul. Réplication d’une table supprime les données de tootransfer besoin de hello entre les nœuds de calcul avant une jointure ou une agrégation. Étant donné que la table de hello a plusieurs copies, les tables répliquées convient mieux lorsque la taille de la table hello est inférieure à 2 Go compressé.

Hello diagramme suivant illustre une table répliquée est accessible sur chaque nœud de calcul. Dans l’entrepôt de données SQL, répliquée hello est la base de données de distribution tooa entièrement copiée sur chaque nœud de calcul. 

![Table répliquée](media/guidance-for-using-replicated-tables/replicated-table.png "Table répliquée")  

Le fonctionnement des tables répliquées est mieux adapté aux petites tables de dimension dans un schéma en étoile. Tables de dimension sont généralement d’une taille qui rend possible toostore et maintenir plusieurs copies. Les dimensions stockent des données descriptives qui se modifient lentement, comme le nom et l’adresse du client, ainsi que les détails sur le produit. Hello variation nature des données de hello entraîne les reconstructions toofewer de la table répliquée de hello. 

Envisagez d’utiliser une table répliquée dans les cas suivants :

- taille de la table Hello sur le disque est inférieur à 2 Go, quelle que soit le nombre de hello de lignes. taille de hello toofind d’une table, vous pouvez utiliser hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) commande : `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`. 
- table de Hello est utilisée dans les jointures qui requièrent normalement un déplacement des données. Par exemple, une jointure sur les tables de hachage distribué requiert le déplacement des données lorsque les colonnes de jointure hello sont hello pas la même colonne de distribution. Si une des tables de hachage distribué hello est petite, considérez une table répliquée. Une jointure sur une table de distribution par tourniquet (round-robin) requiert le déplacement des données. Nous vous recommandons d’utiliser des tables répliquées au lieu de tables de distribution par tourniquet dans la plupart des cas. 


Envisagez de convertir un existant distributed tooa table répliquée table lorsque :

- Opérations de déplacement de données utilisez qui diffusent des nœuds de calcul hello hello données tooall les plans de requête. Hello BroadcastMoveOperation est coûteuse et ralentit les performances des requêtes. tooview les opérations de déplacement de données dans les plans de requête, utilisez [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).
 
Les tables répliquées ne peuvent pas produire de meilleures performances des requêtes hello lorsque :

- table de Hello a fréquentes d’insertion, mise à jour et les opérations de suppression. Ces opérations data manipulation language (DML) nécessitent une régénération de la table de hello répliquée. La reconstruction fréquente peut diminuer les performances.
- entrepôt de données Hello est souvent à l’échelle. Mise à l’échelle d’un entrepôt de données modifie nombre hello de nœuds de calcul, ce qui entraîne une régénération.
- table de Hello possède un grand nombre de colonnes, mais les opérations de données généralement accéder uniquement à un petit nombre de colonnes. Dans ce scénario, au lieu de répliquer la table entière de hello, il peut être plus efficace toohash distribuer les table hello et ensuite créer un index sur les colonnes hello fréquemment. Quand une requête requiert le déplacement des données, l’entrepôt de données SQL que déplace les données Bonjour demandé de colonnes. 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>Utiliser des tables répliquées avec des prédicats de requête simples
Avant de choisir toodistribute ou répliquer une table, pensez aux types de requêtes que vous projetez toorun par rapport à la table de hello hello. Lorsque possible,

- Utilisez des tables répliquées pour les requêtes avec des prédicats de requête simples, comme l’égalité ou l’inégalité.
- Utilisez des tables distribuées pour les requêtes avec des prédicats de requête complexes, comme LIKE ou NOT LIKE.

Les requêtes sollicitant beaucoup le processeur fonctionnent de manière optimale lors de la charge de travail hello est répartie entre tous les nœuds de calcul hello. Par exemple, les requêtes qui exécutent des calculs sur chaque ligne d’une table fonctionnent mieux sur les tables distribués que sur les tables répliquées. Étant donné qu’une table répliquée est stockée dans son intégralité sur chaque nœud de calcul, une requête de gourmande en ressources processeur sur une table répliquée s’exécute par rapport à la totalité de la table hello sur chaque nœud de calcul. Hello calcul supplémentaire peut ralentir les performances des requêtes.

Par exemple, cette requête comporte un prédicat complexe.  Elle s’exécute plus rapidement lorsque le fournisseur est une table distribuée au lieu d’une table répliquée. Dans cet exemple, le fournisseur peut être distribué par hachage ou distribué par tourniquet.

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>Convertir les tables de tooreplicated alternée tables existantes
Si vous avez déjà des tables de tourniquet, nous vous recommandons en les convertissant tooreplicated tables si elles répondent aux critères décrites dans cet article. Les tables répliquées améliorent les performances sur les tables de tourniquet, car celles-ci éliminent le besoin de hello pour le déplacement des données.  Une table de distribution par tourniquet requiert toujours le déplacement des données pour les jointures. 

Cet exemple utilise [SACT](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa de table répliquée. Cet exemple fonctionne que la table DimSalesTerritory soit distribuée par hachage ou par tourniquet.

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>Exemple de performances de requête pour une table de distribution par tourniquet et une table répliquée 

Une table répliquée ne nécessite pas de tout déplacement de données pour les jointures étant donné que la totalité de la table hello est déjà présent sur chaque nœud de calcul. Si les tables de dimension hello sont tourniquet distribué, une jointure copie table de dimension hello tooeach complète de nœud de calcul. les données de salutation toomove, plan de requête hello contient une opération appelée BroadcastMoveOperation. Ce type d’opération de déplacement des données ralentit les performances des requêtes. Il n’est pas utilisé par les tables répliquées. étapes du plan de requête de tooview, utilisez hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) affichage catalogue système. 

Par exemple, dans la requête suivante sur le schéma d’AdventureWorks hello, hello ` FactInternetSales` table est distribué de hachage. Hello `DimDate` et `DimSalesTerritory` sont des tables de dimension plus petites. Cette requête retourne les ventes totales hello en Amérique du Nord pour l’année fiscale 2004 :
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
Nous avons recréé les tables `DimDate` et `DimSalesTerritory` en tant que tables de distribution par tourniquet. Par conséquent, les requêtes hello ont montré hello suivant le plan de requête, ce qui a diffusion plusieurs opérations de déplacement : 
 
![Plan de requête de type tourniquet (round robin)](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

Nous recréée `DimDate` et `DimSalesTerritory` comme des tables répliquées et exécution de requête de hello à nouveau. plan de requête résultant Hello est beaucoup plus courte et ne pas avoir une diffusion se déplace.

![Plan de requête répliqué](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>Considérations relatives aux performances pour la modification des tables répliquées
SQL Data Warehouse implémente une table répliquée en conservant une copie principale de la table de hello. Il copie la base de données de distribution de hello version maître tooone sur chaque nœud de calcul. Lorsqu’il existe une modification, l’entrepôt de données SQL met à jour table principale de hello en premier. Il requiert une régénération des tables hello sur chaque nœud de calcul. Une reconstruction d’une table répliquée inclut copie le nœud de calcul tooeach hello table et la reconstruction des index de hello.

Les reconstructions sont requises après les événements suivants :
- Des données sont chargées ou modifiées
- entrepôt de données Hello est mis à l’échelle tooa valeur dwu différents
- La définition de la table est mise à jour

Les reconstructions ne sont pas requises après les événements suivants :
- Opération de suspension
- Opération de reprise

reconstruction de Hello ne se produit pas immédiatement après la modification des données. Au lieu de cela, hello reconstruction est déclenchée hello la première fois une requête sélectionne à partir de la table de hello.  Dans l’instruction select de hello initiale à partir de la table de hello sont étapes toorebuild hello répliquée.  Hello régénération est effectuée au sein de la requête de hello, instruction select initiale toohello hello impact peut être significative selon la taille de hello de table de hello.  Si plusieurs tables répliquées sont impliquées nécessitant une reconstruction, chaque copie est reconstruit en série en tant qu’étapes au sein de l’instruction de hello.  la cohérence des données pendant la reconstruction hello Hello toomaintain répliquées table qu'un verrou exclusif est établi sur la table de hello.  verrou de Hello pour la durée de reconstruction de hello hello, ce qui empêche la table de toohello tous les accès. 

### <a name="use-indexes-conservatively"></a>Utilisation restrictive des index
Les pratiques d’indexation standards s’appliquent tooreplicated tables. SQL Data Warehouse reconstruit l’index de chaque table répliquée dans le cadre de la reconstruction de hello. Utilisez les index uniquement lorsque le gain de performances hello compense le coût hello de reconstruction d’index de hello.  
 
### <a name="batch-data-loads"></a>Chargements de données par lots
Lors du chargement des données dans des tables répliquées, essayez les reconstructions toominimize en charges de traitement par lot. Effectuer toutes les charges hello traités par lot avant d’exécuter des instructions select.

Par exemple, ce modèle de chargement charge les données à partir de quatre sources et appelle quatre reconstructions. 

- Charger à partir de la source 1.
- Instruction select qui déclenche la reconstruction 1.
- Charger à partir de la source 2.
- Instruction select qui déclenche la reconstruction 2.
- Charger à partir de la source 3.
- Instruction select qui déclenche la reconstruction 3.
- Charger à partir de la source 4.
- Instruction select qui déclenche la reconstruction 4.

Par exemple, ce modèle de chargement charge les données à partir de quatre sources mais n’appelle qu’une seule reconstruction.

- Charger à partir de la source 1.
- Charger à partir de la source 2.
- Charger à partir de la source 3.
- Charger à partir de la source 4.
- Instruction select qui déclenche la reconstruction.


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>Reconstruire une table répliquée après un chargement par lots
temps d’exécution de requête cohérente tooensure, nous vous recommandons de forcer une actualisation des tables de hello répliquée après une charge de traitement par lots. Dans le cas contraire, première requête de hello doit attendre de toorefresh de tables hello, qui inclut la reconstruction des index de hello. Selon la taille de hello et le nombre de tables répliquées affectées, impact sur les performances hello peut être importantes.  

Cette requête utilise hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) hello toolist DMV répliquées des tables qui ont été modifiées mais ne pas reconstruits.

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
tooforce une régénération, exécutez hello instruction suivante sur chaque table Bonjour précédant la sortie. 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>Étapes suivantes 
toocreate une table répliquée, utilisez une de ces instructions :

- [CREATE TABLE (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

Pour une vue d’ensemble des tables distribuées, consultez [Tables distribuées](sql-data-warehouse-tables-distribute.md).



