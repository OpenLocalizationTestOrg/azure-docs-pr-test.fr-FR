---
title: vues aaaUsing T-SQL dans Azure SQL Data Warehouse | Documents Microsoft
description: "Conseils relatifs à l’utilisation de vues Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>Vues proposées par SQL Data Warehouse
Les vues sont particulièrement utiles dans SQL Data Warehouse. Ils peuvent être utilisés dans un certain nombre de façons différentes tooimprove hello de qualité de votre solution.  Cet article présente quelques exemples de comment tooenrich votre solution avec les vues, ainsi que des limitations hello nécessitant toobe pris en compte.

> [!NOTE]
> La syntaxe de `CREATE VIEW` n’est pas abordée dans cet article. Reportez-vous toohello [CREATE VIEW] [ CREATE VIEW] l’article sur MSDN pour obtenir ces informations de référence.
> 
> 

## <a name="architectural-abstraction"></a>Abstraction architecturale
Un modèle très courant de l’application est toore-créer des tables à l’aide de CREATE TABLE AS sélectionnez (SACT) suivi d’un objet renommer le modèle pendant le chargement de données.

exemple Hello ci-dessous ajoute la dimension de date tooa date nouveaux enregistrements. Notez comment un nouveau tableau, DimDate_New, est créé et ensuite renommé la version d’origine de hello tooreplace de la table de hello.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Toutefois, cette approche peut provoquer l’apparition et la disparition de table d’une vue utilisateur, ainsi que l’affichage de messages d’erreur de type « la table n’existe pas ». Les vues peuvent être des utilisateurs de tooprovide utilisé avec une couche de présentation cohérent tandis que les objets sous-jacents hello sont renommés. En fournissant aux utilisateurs un accès toohello des données via une vue, signifie que les utilisateurs n’ont besoin de visibilité toohave de tables sous-jacentes de hello. Cela fournit une expérience utilisateur cohérente, tout en garantissant que les concepteurs d’entrepôts de données hello peuvent évolue au modèle de données hello et optimiser les performances à l’aide de SACT pendant le processus de chargement des données de salutation.    

## <a name="performance-optimization"></a>Optimisation des performances
Vues peuvent également être des jointures de performance optimisée tooenforce utilisé entre les tables. Par exemple, une vue peut incorporer une clé de répartition redondant dans le cadre de hello toominimize déplacement des données dans les critères de jointure.  Un autre avantage d’une vue peut être tooforce une requête spécifique ou un indicateur de jointure. À l’aide des vues de cette façon garantit que les jointures sont toujours effectuées en évitant recours hello pour la construction correcte de hello tooremember les utilisateurs pour les jointures de manière optimale.

## <a name="limitations"></a>Limites
Dans SQL Data Warehouse, les vues concernent uniquement les métadonnées.  Par conséquent hello options suivantes n’est pas disponible :

* Il n’existe aucune option de liaison de schéma.
* Tables de base ne peut pas être mis à jour via la vue de hello
* Vous ne pouvez pas créer des vues sur des tables temporaires.
* Aucune prise en charge pour hello développer / indicateurs de NOEXPAND
* SQL Data Warehouse n’inclut aucune vue indexée.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].
Pour `CREATE VIEW` syntaxe, consultez trop[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
