---
title: "les schémas définis par l’aaaUser dans l’entrepôt de données SQL | Documents Microsoft"
description: "Conseils relatifs à l’utilisation de schémas Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Schémas définis par l’utilisateur dans SQL Data Warehouse
Entrepôts de données traditionnels souvent utiliser des bases de données toocreate des limites d’application en fonction de la charge de travail ou de domaine sécurité. Par exemple, un entrepôt de données SQL Server classique peut inclure une base de données de la zone de transit, une base de données de l’entrepôt de données et quelques bases de données de mini-Data Warehouse. Dans cette topologie, chaque base de données fonctionne comme une charge de travail et la limite de sécurité dans l’architecture de hello.

En revanche, SQL Data Warehouse exécute la charge de travail entrepôt de données entière hello au sein d’une base de données. Les jointures entre plusieurs bases de données ne sont pas autorisées. Par conséquent, SQL Data Warehouse attend que toutes les tables utilisées par toobe d’entrepôt hello stockée dans une base de données de hello.

> [!NOTE]
> SQL Data Warehouse ne prend pas en charge les requêtes de base de données croisées, de quelque nature que ce soit. Par conséquent, les implémentations de l’entrepôt de données qui tirent parti de ce modèle devez toobe révisée.
> 
> 

## <a name="recommendations"></a>Recommandations
Tenez compte des recommandations lorsque vous consolidez des limites de charge de travail, fonctionnelles, de domaine et de sécurité :

1. Utilisez un toorun de base de données SQL Data Warehouse votre charge de travail de l’entrepôt de données
2. Consolider vos données entrepôt environnement toouse un entrepôt de données SQL base de données existante
3. Tirer parti de la **schémas définis par l’utilisateur** tooprovide limite de hello précédemment implémentée à l’aide de bases de données.

Si aucun schéma défini par l’utilisateur n’a été utilisé précédemment, vous repartez de zéro. Utiliser simplement vos schémas définis par l’utilisateur dans la base de données SQL Data Warehouse hello ancien nom de base de données hello comme base de hello.

Si les schémas ont été déjà utilisés, vous disposez de différentes options :

1. Supprimer des noms de schéma hérité hello et mettre à jour
2. Conserver les noms de schéma hérité hello par nom de table hello préalable en attente schéma hérité nom toohello
3. Conserver les noms de schéma hérité hello en implémentant des vues sur table hello dans un schéma supplémentaire de toore-créer une structure de schéma ancien hello.

> [!NOTE]
> Inspection première option 3 peut sembler comme option de hello plus attrayante. Toutefois, les diable hello sont en détail hello. Les vues sont en lecture seule dans SQL Data Warehouse. Toute modification de données ou de table doivent toobe effectuée sur la table de base hello. Par ailleurs, cette troisième option présente une couche de vues au sein de votre système. Vous pourriez toogive cette une réflexion supplémentaire si vous utilisez déjà des vues dans votre architecture.
> 
> 

### <a name="examples"></a>Exemples :
Implémentation de schémas définis par l’utilisateur basés sur des noms de base de données

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Conserver schéma hérité en attente avant les nomme toohello nom de la table. Utilisez des schémas pour les limites de charge de travail hello.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Conservation des noms de schémas hérités via des vues

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Toute modification de la stratégie de schéma a besoin d’une revue hello du modèle de sécurité pour la base de données hello. Dans de nombreux cas, vous pouvez être toosimplify en mesure de modèle de sécurité de hello en assignant des autorisations au niveau du schéma hello. S’il vous faut des autorisations plus granulaires, vous pouvez utiliser des rôles de base de données.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
