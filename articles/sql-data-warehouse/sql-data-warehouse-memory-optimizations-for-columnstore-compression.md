---
title: "performances de l’index columnstore aaaImprove dans SQL Azure | Documents Microsoft"
description: "Réduire les besoins en mémoire ou augmentez hello mémoire disponible toomaximize hello nombre de lignes de qu'un index columnstore compresse dans chaque groupe de lignes."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Optimiser la qualité du rowgroup pour columnstore

Qualité de Rowgroup est déterminée par le nombre de hello de lignes dans un groupe de lignes. Réduire les besoins en mémoire ou augmentez hello mémoire disponible toomaximize hello nombre de lignes de qu'un index columnstore compresse dans chaque groupe de lignes.  Utilisez ces modes tooimprove de taux de compression et les performances des requêtes pour les index columnstore.

## <a name="why-hello-rowgroup-size-matters"></a>Importance de la taille de rowgroup hello
Dans la mesure où un index columnstore analyse une table en analysant les segments de colonne de rowgroups individuels, optimiser le nombre de hello de lignes dans chaque groupe de lignes améliore les performances de requête. Lorsque rowgroups ont un grand nombre de lignes, la compression des données permet d’améliorer ce qui signifie qu'est moins tooread de données à partir du disque.

Pour plus d’informations sur les rowgroups, voir [Description des index columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Taille cible des rowgroups
Pour de meilleures performances de requête, hello vise nombre de hello toomaximize de lignes par rowgroup dans un index columnstore. Un rowgroup peut compter au maximum 1 048 576 lignes. Son toonot OK ont un nombre maximal de hello de lignes par rowgroup. Les index columnstore produisent de bonnes performances quand les rowgroups comprennent au moins 100 000 lignes.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Des rowgroups peuvent être découpés en cours de compression

Pendant une reconstruction d’index en bloc charge ou columnstore, parfois, il n’est pas assez toocompress disponible mémoire que tous hello désignés pour chaque groupe de lignes. En cas de sollicitation de la mémoire, les index columnstore trim tailles de rowgroup hello compression dans hello columnstore permettre fonctionner. 

Lorsqu’il existe des lignes toocompress au moins 10 000 de mémoire insuffisante dans chaque groupe de lignes, SQL Data Warehouse génère une erreur.

Pour plus d’informations sur le chargement en masse, voir [Chargement de données d’index columnstore](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>La qualité de rowgroup toomonitor

Il existe une vue de gestion dynamique (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) qui expose des informations utiles telles que le nombre de lignes dans les rowgroups et hello motif pour la troncature s’il a été de découpage. Vous pouvez créer des ces informations de tooget DMV hello suivant vue comme un moyen pratique de tooquery sur la suppression du groupe de lignes.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Hello trim_reason_desc indique si le groupe de lignes hello a été tronqué (trim_reason_desc = NO_TRIM implique aucune suppression, et groupe de lignes est de qualité optimale). Hello raisons trim suivantes indiquent suppression prématurée de hello rowgroup :
- Chargement en masse : C’est pourquoi découpage est utilisé lorsque le traitement entrant de hello de lignes pour la charge hello était inférieur à 1 million de lignes. moteur de Hello créera des groupes de lignes compressés si supérieur à 100 000 lignes insérées (comme tooinserting exécutée dans le magasin de delta hello) mais des jeux hello tooBULKLOAD de découpage raison. Dans ce scénario, envisagez d’augmenter votre tooaccumulate de fenêtre de charge de traitement par lots plusieurs lignes. En outre, réévaluez votre tooensure schéma partitionnement, il n’est pas trop granulaire que les groupes de lignes ne peut pas couvrir les limites de partition.
- MEMORY_LIMITATION : toocreate des groupes de lignes avec 1 million de lignes, une certaine quantité de mémoire de travail est requis par le moteur de hello. Lorsque la mémoire disponible de hello du chargement de session est inférieur au nombre requis de hello mémoire de travail, les groupes de lignes obtient supprimés prématurément. Hello les sections suivantes explique comment tooestimate mémoire requise et allouer davantage de mémoire.
- DICTIONARY_SIZE : cette raison indique qu’un rowgroup a été découpé car il contenant au moins une colonne de chaîne avec des chaînes de cardinalité large et/ou haute. taille de dictionnaire Hello est limitée too16 Mo en mémoire et une fois cette limite atteinte groupe de lignes hello est compressé. Si vous n’exécutez pas dans ce cas, envisagez d’isoler les colonnes problématique hello dans une table distincte.

## <a name="how-tooestimate-memory-requirements"></a>Comment tooestimate mémoire requise

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

un rowgroup Hello maximale de mémoire requise toocompress est d’environ

- 72 Mo +
- \#lignes \*\#colonnes \* 8 octets +
- \#lignes \*\#colonnes de chaîne courte \* 32 octets +
- \#colonnes de chaîne longue \* 16 Mo pour le dictionnaire de compression

où les colonnes de chaîne courte utilisent des données de type chaîne <= 32 octets, et les colonnes de chaîne longueur utilisent des données de type chaîne > 32 octets.

Les chaînes longues sont compressés avec une méthode de compression conçue pour la compression de texte. Cette méthode de compression utilise un *dictionnaire* toostore les modèles de texte. taille maximale de Hello d’un dictionnaire est de 16 Mo. Il est uniquement un dictionnaire pour chaque colonne de chaîne longue de hello rowgroup.

Pour une présentation détaillée des besoins en mémoire de columnstore, voir la vidéo [Mise à l’échelle d’Azure SQL Data Warehouse : configuration et instructions](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Besoins en mémoire façons tooreduce

Utilisez hello suivant les exigences de mémoire techniques tooreduce hello pour compresser les rowgroups dans les index columnstore.

### <a name="use-fewer-columns"></a>Utiliser moins de colonnes
Si possible, concevez table hello avec moins de colonnes. Quand un rowgroup est compressé dans hello columnstore, index columnstore de hello compresse chaque segment de colonne séparément. Par conséquent hello besoins en mémoire toocompress un rowgroup augmenter en tant que nombre hello de colonnes.


### <a name="use-fewer-string-columns"></a>Utiliser moins de colonnes de chaîne
Les colonnes de données de type chaîne nécessitent davantage de mémoire que les données de type nombre et date. tooreduce besoins en mémoire, envisagez de supprimer des colonnes de type chaîne à partir des tables de faits et en les plaçant dans les tables de dimension plus petites.

Besoins en mémoire supplémentaires pour la compression de chaîne :

- Types de données de chaîne des caractères de too32 peuvent nécessiter 32 octets supplémentaires par valeur.
- Les données de type chaîne comprenant plus de 32 caractères sont compressées à l’aide de méthodes de dictionnaire.  Chaque colonne dans le groupe de lignes hello peut nécessiter la dictionnaire tooan supplémentaires 16 Mo toobuild hello.

### <a name="avoid-over-partitioning"></a>Éviter un partitionnement excessif

Les index columnstore créent un ou plusieurs rowgroups par partition. Dans l’entrepôt de données SQL, nombre hello de partitions augmente rapidement, car les données de salutation sont distribuées et chaque point de distribution est partitionnée. Si la table de hello a trop de partitions, il peut-être pas suffisamment rowgroups de hello toofill lignes. manque de Hello de lignes ne crée pas de sollicitation de la mémoire lors de la compression, mais elle entraîne toorowgroups que ne pas atteindre les meilleures performances des requêtes columnstore hello.

Une autre raison tooavoid remplacer le partitionnement est une mémoire système de traitement pour le chargement de lignes dans un index columnstore sur une table partitionnée. Lors d’un chargement, le nombre de partitions pourrait recevoir des lignes entrantes hello, qui sont conservées en mémoire jusqu'à ce que chaque partition possède suffisamment toobe lignes compressé. Un trop grand nombre de partitions entraîne une sollicitation supplémentaire de la mémoire.

### <a name="simplify-hello-load-query"></a>Simplifiez la requête de charge hello

base de données Hello partage hello allocation de mémoire pour une requête parmi tous les opérateurs hello dans la requête de hello. Lorsqu’une requête de charge contient des tris complexes et les jointures, mémoire hello disponible pour la compression est réduite.

Concevoir hello charge requête toofocus uniquement lors du chargement de requête de hello. Si vous avez besoin de transformations toorun sur les données de salutation, exécutez-les distinct à partir de la requête de charge hello. Par exemple, stocker des données hello dans une table de segment de mémoire, exécuter des transformations de hello et chargez ensuite hello table intermédiaire dans un index columnstore hello. Vous pouvez également charger en premier les données hello et ensuite utiliser les données de salutation MPP système tootransform hello.

### <a name="adjust-maxdop"></a>Ajuster MAXDOP

Chaque point de distribution compresse les rowgroups dans columnstore hello en parallèle lorsque plusieurs cœurs de processeur est disponible par la distribution. parallélisme de Hello nécessite des ressources de mémoire supplémentaire, qui peuvent provoquer une sollicitation de la toomemory et de la suppression du groupe de lignes.

tooreduce la sollicitation de la mémoire, vous pouvez utiliser hello MAXDOP requête indicateur tooforce hello charge opération toorun en mode série au sein de chaque point de distribution.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Méthodes tooallocate plus de mémoire

Classe de ressource utilisateur hello et de taille des DWU déterminent la quantité de mémoire est disponible pour une requête utilisateur. allocation de mémoire de hello de tooincrease pour une requête de charge, vous pouvez augmenter le nombre de hello de Dwu ou augmenter la classe de ressource hello.

- tooincrease hello Dwu, consultez [comment faire évoluer performances ?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- classe de ressource toochange hello pour une requête, consultez [modifier un exemple de classe de ressource utilisateur](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Par exemple, sur DWU 100, un utilisateur dans la classe de ressource hello smallrc peut utiliser 100 Mo de mémoire pour chaque point de distribution. Pour plus d’informations hello, consultez [l’accès concurrentiel dans SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).

Supposons que vous déterminez que vous avez besoin de 700 Mo de tailles de mémoire tooget rowgroup de haute qualité. Ces exemples montrent comment vous pouvez exécuter la requête de charge hello avec suffisamment de mémoire.

- En utilisant DWU 1000 et mediumrc, votre allocation de mémoire est de 800 Mo.
- En utilisant DWU 600 et largerc, votre allocation de mémoire est de 800 Mo.


## <a name="next-steps"></a>Étapes suivantes

toofind performances tooimprove manières dans l’entrepôt de données SQL, consultez hello [vue d’ensemble des performances](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
