---
title: tables aaaDistributing SQL Data Warehouse | Documents Microsoft
description: Prise en main de la distribution de tables dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Distribution de tables dans SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Types de données][Data Types]
> * [Distribuer][Distribute]
> * [Index][Index]
> * [Partition][Partition]
> * [Statistiques][Statistics]
> * [Temporaire][Temporary]
>
>

SQL Data Warehouse est un système de base de données distribuée à traitement massivement parallèle.  En répartissant les données et les fonctions de traitement sur plusieurs nœuds, SQL Data Warehouse propose une évolutivité immense, bien supérieure à ce qu’offre n’importe quel système unique.  Décider comment toodistribute vos données dans votre entrepôt de données SQL sont une des plus importantes de hello facteurs tooachieving des performances optimales.   performances de clé toooptimal Hello est de minimiser le déplacement des données et à son tour le déplacement des données de hello toominimizing clé consiste à sélectionner la stratégie de distribution droite hello.

## <a name="understanding-data-movement"></a>Présentation du déplacement des données
Dans un système MPP, données hello de chaque table sont réparties sur plusieurs bases de données sous-jacentes.  requêtes Hello plus optimisée sur un système MPP peuvent simplement être transmises via tooexecute hello des bases de données distribuées sans aucune interaction hello entre les autres bases de données.  Par exemple, supposons que vous disposez d’une base de données avec des données de ventes, qui contient deux tables, ventes et clients.  Si vous disposez d’une requête qui doit toojoin votre table des clients de la table sales tooyour et que vous divisez une vos ventes et les tables du client par numéro de client, le placement de chaque client dans une base de données distincte, toutes les requêtes qui relient les ventes et les clients peuvent être résolus dans chaque Aucune base de connaissances de base de données hello autres bases de données.  En revanche, si vos données de ventes que vous divisé par numéro de commande et les données de votre client par numéro de client, puis chaque base de données n’a pas les données correspondantes hello pour chaque client et par conséquent, si vous souhaitiez toojoin vos données de client tooyour les données de ventes, vous devez tooget hello de données pour chaque client à partir de hello autres bases de données.  Dans ce deuxième exemple, le déplacement des données besoin toooccur toomove hello les données toohello données de ventes, afin que hello deux tables peuvent être jointes.  

Le déplacement des données n’est pas toujours une mauvaise chose, il est parfois nécessaire toosolve une requête.  Mais quand cette étape supplémentaire peut être évitée, votre requête s’exécute naturellement plus rapidement.  Le déplacement des données se produit généralement en cas de jointure ou d’agrégation de tables.  Fréquence à laquelle vous devez toodo à la fois, tandis que vous pourrez toooptimize pour un scénario comme une jointure, vous toujours besoin toohelp de déplacement des données vous résolvez hello autre scénario, comme une agrégation.  Astuce de Hello est de savoir qui est moins de travail.  Dans la plupart des cas, la distribution de grandes tables de faits sur une colonne jointe communément est hello méthode la plus efficace pour réduire hello la plupart des mouvements de données.  Distribution des données sur les colonnes de jointure est un beaucoup plus courantes méthode tooreduce le déplacement des données à la distribution des données sur des colonnes impliquées dans une agrégation.

## <a name="select-distribution-method"></a>Sélectionner la méthode de distribution
Coulisses de hello, SQL Data Warehouse divise vos données dans les bases de données de 60.  Chaque base de données est référencé tooas un **distribution**.  Lorsque les données sont chargées dans chaque table, l’entrepôt de données SQL a tooknow comment toodivide vos données sur ces 60 distributions.  

méthode de distribution Hello est définie au niveau de table hello et actuellement, il existe deux possibilités :

1. **Tourniquet (round robin)** , qui distribue les données de manière équitable mais aléatoire.
2. **distribution par hachage** , qui distribue les données en fonction des valeurs de hachage d’une colonne unique.

Par défaut, lorsque vous ne définissez pas une méthode de distribution de données, votre table sera distribuée à l’aide de hello **tourniquet (Round Robin)** méthode de distribution.  Toutefois, lorsque vous serez plus sophistiquées dans votre implémentation, vous pouvez à l’aide de tooconsider **hachage distribué** toominimize le déplacement des données qui vous permettra d’optimiser les performances des requêtes à son tour les tables.

### <a name="round-robin-tables"></a>Tables avec distribution par tourniquet (round robin)
À l’aide de la méthode tourniquet (Round Robin) pour distribuer des données de hello est très bien comment il semble.  Lors du chargement de vos données, chaque ligne est envoyée simplement toohello prochaine distribution.  Cette méthode pour distribuer les données de salutation toujours répartira les données de salutation très uniformément sur toutes les distributions de hello.  Autrement dit, il n’est aucun tri terminé pendant hello round (Round Robin) les processus qui le place vos données.  C’est pour cette raison que ce type de distribution est parfois appelé « hachage aléatoire ».  Avec une table distribuée alternée aucune donnée nécessaire toounderstand hello.  Pour cette raison, ce type de table représente souvent une cible de chargement adéquate.

Par défaut, si aucune méthode de distribution n’est choisie, hello méthode de distribution alternée servira.  Toutefois, alors que les tables de tourniquet (Round Robin) sont toouse facile, car les données sont réparties au hasard sur système hello que cela signifie que le système de hello ne peut pas garantir la distribution chaque ligne est sur.  En conséquence, système hello parfois des besoins tooinvoke un toobetter d’opération de déplacement des données organiser vos données avant qu’il peut résoudre une requête.  Cette étape supplémentaire peut ralentir vos requêtes.

Envisagez d’utiliser la distribution de tourniquet (Round Robin) pour votre table Bonjour les scénarios suivants :

* lors de la mise en route sous forme de point de départ simple ;
* s’il n’existe aucune clé de jointure évidente ;
* S’il n’est pas colonne bon candidat pour la distribution de table de hello de hachage
* Si hello table ne partage pas d’une clé de jointure commune avec d’autres tables
* Si la jointure de hello est moins importante que les autres jointures dans la requête de hello
* Lorsque hello est une table intermédiaire temporaire

Ces exemples créent une table à distribution par tourniquet (round robin) :

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Alors que le tourniquet (Round Robin) est le type de table par défaut hello soient explicites dans votre commande DDL est considéré comme une meilleure pratique afin que les intentions hello de votre disposition de table soient tooothers clair.
>
>

### <a name="hash-distributed-tables"></a>Tables à distribution par hachage
À l’aide un **hachage distribué** algorithme toodistribute vos tables peuvent améliorer les performances dans de nombreux scénarios en réduisant le déplacement des données au moment de la requête.  Hachage distribuées sont des tables qui sont répartis entre hello distribuées de bases de données à l’aide d’un algorithme de hachage sur une seule colonne que vous sélectionnez.  colonne de distribution Hello est ce qui détermine la façon dont les données de salutation sont réparties sur vos bases de données distribuées.  fonction de hachage Hello utilise hello distribution colonne tooassign lignes toodistributions.  Hello d’algorithme de hachage et de distribution qui en résulte est déterministe.  Autrement dit hello même valeur avec le même type de données sera toujours de hello a toohello distribution même.    

Cet exemple crée une table distribuée en fonction de l’ID :

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Sélectionner la colonne de distribution
Lorsque vous choisissez trop**hachage distribuer** une table, vous devez tooselect une colonne de distribution unique.  Lorsque vous sélectionnez une colonne de distribution, il existe trois principaux facteurs tooconsider.  

Sélectionnez une colonne unique qui :

1. ne sera pas mise à jour ;
2. distribuera les données de manière uniforme en évitant le décalage des données ;
3. réduira le nombre de déplacements des données.

### <a name="select-distribution-column-which-will-not-be-updated"></a>Sélectionner la colonne de distribution qui ne sera pas mise à jour
Les colonnes de distribution ne peuvent pas être mises à jour, par conséquent, sélectionnez une colonne avec des valeurs statiques.  Si une colonne a besoin toobe mis à jour, il n’est généralement pas un candidat de distribution correct.  S’il existe un cas où vous devez mettre à jour une colonne de distribution, il est possible par tout d’abord supprimer les lignes hello, puis d’insérer une nouvelle ligne.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Sélectionner la colonne de distribution qui distribuera les données de manière uniforme
Depuis un système distribué effectue aussi vite que sa distribution les plus lents, il est important toodivide hello travail uniformément entre les distributions de hello dans l’exécution de commande tooachieve équilibrée dans tout hello système.  moyen Hello travail de hello est divisée en un système distribué est basée sur l’emplacement réel des données hello pour chaque point de distribution.  Cela permet de colonne de droite distribution hello tooselect très important pour la distribution des données de salutation afin que chaque point de distribution a le même travail, et sera take hello même temps toocomplete sa partie du travail de hello.  Lorsque le travail est bien réparti sur système de hello, les données de salutation sont équilibrées entre les distributions de hello.  Lorsque les données ne sont pas équilibrées, c’est ce que nous appelons le **décalage des données**.  

les données toodivide uniformément et éviter que les données de décalage, envisagez de suivant de hello lors de la sélection de votre colonne de distribution :

1. Sélectionnez une colonne contenant un nombre important de valeurs distinctes.
2. Évitez la distribution des données sur des colonnes avec peu de valeurs distinctes.
3. Évitez de distribuer les données sur des colonnes dont la fréquence de valeurs NULL est élevée.
4. Évitez de distribuer les données sur des colonnes de date.

Étant donné que chaque valeur est haché too1 60 distributions, répartition tooachieve vous devez tooselect une colonne qui est hautement unique et contient plus de 60 valeurs uniques.  tooillustrate, considérez un cas où une colonne contient seulement des valeurs uniques 40.  Si cette colonne a été sélectionnée en tant que clé de répartition hello, données hello pour cette table seraient arriver sur 40 distributions au maximum, en laissant les 20 distributions avec aucune donnée et aucun toodo de traitement.  À l’inverse, hello autres 40 distributions aurait plus toodo de travail que si hello données a été réparties de façon plus de 60 distributions.  Ce scénario est un exemple de décalage de données.

Dans le système MPP, chaque étape de requête attend que toutes les distributions toocomplete leur part les travaux hello.  Si une distribution est effectuant plus de travail pour d’autres hello : hello ressource Hello autres distributions sont essentiellement un inutile simplement en attente de distribution à l’activité hello.  Lorsque le travail n’est pas réparti uniformément sur toutes les distributions, c’est ce que nous appelons le **décalage de traitement**.  Traitement inclinaison entraîne toorun requêtes plus lente que si la charge de travail hello peut être répartie uniformément entre les distributions de hello.  Décalage de données entraînent tooprocessing inclinaison.

Éviter la distribution sur hautement n’acceptant que les valeurs null hello tous arrive ensuite sur hello même distribution. Distribution sur une colonne de date peut également provoquer le décalage de traitement, car toutes les données d’une date donnée arrive ensuite sur hello même distribution. Si plusieurs utilisateurs exécutent des requêtes tout filtrage sur hello même date, puis uniquement 1 de distributions de 60 hello va faire tout travail de hello depuis une date donnée seront uniquement sur une distribution. Dans ce scénario, les requêtes de hello s’exécuteront probablement de 60 fois plus lents que si les données de salutation ont été également réparties sur toutes les distributions de hello.

Lorsque aucune colonne bon candidat n’existe, envisagez d’utiliser le tourniquet (Round Robin) comme méthode de distribution hello.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Sélectionner la colonne de distribution qui réduira le déplacement des données
En réduisant le déplacement des données en sélectionnant la colonne de droite distribution hello est une des stratégies plus importantes de hello pour optimiser les performances de votre entrepôt de données SQL.  Le déplacement des données se produit généralement en cas de jointure ou d’agrégation de tables.  Les colonnes utilisées dans les clauses `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` et `HAVING` sont toutes **adéquates** pour une distribution par hachage.

Hello de d’autre part, les colonnes de hello `WHERE` clause **pas** d’apporter les candidats de colonne hachage adéquate, car ils limitent les distributions participent requête hello, à l’origine de traitement inclinaison.  Un bon exemple d’une colonne qui peut être tentant de toodistribute sur, mais souvent risque de ce traitement inclinaison est une colonne de date.

En règle générale, si vous avez deux tables de faits volumineuse souvent impliquées dans une jointure, vous bénéficierez hello la plupart des performances en distribuant les deux tables sur l’une des colonnes de jointure hello.  Si vous avez une table qui n’est jamais tooanother jointes grande table de faits, puis recherchez toocolumns sont souvent Bonjour `GROUP BY` clause.

Il existe quelques critères clés qui doivent être rempli tooavoid déplacement des données au cours d’une jointure :

1. Hello tables impliquées dans la jointure de hello doivent être distribué sur hachage **un** de colonnes hello participant à la jointure de hello.
2. types de données Hello hello de colonnes de jointure doivent correspondre entre les deux tables.
3. les colonnes Hello doivent être joint avec un opérateur d’égalité.
4. Hello type de jointure est peut-être pas un `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Résolution des problèmes de décalage de données
Lorsque les données de la table sont distribuées à l’aide de la méthode de distribution de hachage hello est possible que certaines distributions sera rétrécie toohave disproportionnellement davantage de données que d’autres. Décalage trop de données peut affecter les performances de requête, car le résultat final de hello d’une requête distribuée doit attendre toofinish de distribution en cours d’exécution plus longue hello. En fonction du degré de hello de données hello inclinaison, que vous devrez peut-être tooaddress il.

### <a name="identifying-skew"></a>Identification du décalage
Un moyen simple de tooidentify une table comme rétrécie est toouse `DBCC PDW_SHOWSPACEUSED`.  Il s’agit d’un moyen très simple et rapide de toosee hello du nombre de lignes de table qui sont stockées dans chacun des distributions hello 60 de votre base de données.  N’oubliez pas que pour des performances hello plus équilibrée, lignes hello dans votre table distribuée doivent être répartis uniformément sur toutes les distributions de hello.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Toutefois, si vous interrogez les vues de gestion dynamique hello Azure SQL Data Warehouse (DMV), vous pouvez effectuer une analyse plus détaillée.  toostart, créer hello vue [dbo.vTableSizes] [ dbo.vTableSizes] afficher à l’aide de SQL à partir de hello [vue d’ensemble de la Table] [ Overview] article.  Une fois que la vue de hello est créée, exécutez cette tooidentify requête les tables d’avoir plus de 10 % de données inclinaison.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Résolution du décalage des données
Pas tout décalage est suffisamment toowarrant.  Dans certains cas, les performances hello d’une table dans des requêtes peut annuler tout effet nuisible hello de décalage des données.  l’inclinaison toodecide si vous devez résoudre des données dans une table, vous devez comprendre autant que possible sur les volumes de données hello et requêtes dans votre charge de travail.   Toolook unidirectionnel à l’impact de hello d’inclinaison est toouse les étapes de hello Bonjour [requête analyse] [ Query Monitoring] impact de hello toomonitor d’inclinaison sur les performances des requêtes de l’article et hello plus précisément les requêtes longues de toohow impact Prenez toocomplete sur les distributions individuelles hello.

Distribution des données consiste à recherche hello juste équilibre entre en réduisant le décalage des données et en réduisant le déplacement des données. Ceux-ci peuvent être opposées objectifs, et vous pouvez tookeep données dans le déplacement des données de commande tooreduce. Par exemple, lors de la colonne de distribution hello est fréquemment hello partagé colonne dans les jointures et agrégations, vous serez minimiser le déplacement des données. Hello avantage de disposer de déplacement de données minimale hello peut-être dépasser impact hello d’avoir des données d’inclinaison.

décalage de données tooresolve est toore typique Hello-créer de table de hello avec une colonne de distribution différent. Comme il n’existe aucun moyen de colonne de distribution toochange hello sur un tableau, distribution de hello toochange hello moyen d’une table il toorecreate avec un [] [SACT].  Voici deux exemples illustrant comment résoudre le décalage de données :

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Exemple 1 : Recréez la table hello avec une nouvelle colonne de distribution
Cet exemple utilise [SACT] [] toore-créer une table avec une colonne de distribution de hachage différent.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Exemple 2 : Recréez la table hello à l’aide de la distribution de tourniquet (Round Robin)
Cet exemple utilise [SACT] [] toore-créer une table avec tourniquet au lieu d’une distribution de hachage. Cette modification produira une distribution des données de même coût de hello du déplacement des données accrue.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la création de table, consultez hello [distribuer][Distribute], [Index][Index], [Partition] [ Partition], [Des Types de données][Data Types], [statistiques] [ Statistics] et [des Tables temporaires] [ Temporary] articles.

Pour obtenir une vue d’ensemble des bonnes pratiques, consultez [Bonnes pratiques pour Azure SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
