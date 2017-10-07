---
title: "aaaMigrate votre entrepôt de données de tooSQL schéma | Documents Microsoft"
description: "Conseils pour migrer votre tooAzure de schéma SQL Data Warehouse pour développer des solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a>Migrer votre tooSQL schémas l’entrepôt de données
Conseils pour la migration de votre tooSQL de schémas SQL Data Warehouse. 

## <a name="plan-your-schema-migration"></a>Planification de la migration du schéma

Lorsque vous planifiez une migration, consultez hello [vue d’ensemble de la table] [ table overview] toobecome familiarisé avec les considérations de conception de table tels que les statistiques de distribution, le partitionnement et l’indexation.  Elle dresse également la liste de certaines [fonctionnalités de table non prises en charge][unsupported table features] et leurs solutions de contournement.

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a>Utiliser des bases de données de schémas définis par l’utilisateur tooconsolidate

Votre charge de travail existante a probablement plusieurs bases de données. Par exemple, un entrepôt de données SQL Server peut inclure une base de données de la zone de transit, une base de données de l’entrepôt de données et quelques bases de données de mini-Data Warehouse. Dans cette topologie, chaque base de données s’exécute comme une charge de travail distincte avec des stratégies de sécurité distinctes.

En revanche, SQL Data Warehouse exécute la charge de travail entrepôt de données entière hello au sein d’une base de données. Les jointures entre plusieurs bases de données ne sont pas autorisées. Par conséquent, l’entrepôt de données SQL attend que toutes les tables utilisées par toobe de l’entrepôt de données hello stockée dans une base de données hello.

Nous recommandons l’utilisation de schémas définis par l’utilisateur tooconsolidate votre charge de travail existante dans une base de données. Pour obtenir des exemples, consultez [Schémas définis par l’utilisateur](sql-data-warehouse-develop-user-defined-schemas.md)

## <a name="use-compatible-data-types"></a>Utilisation des types de données compatibles
Modifiez votre toobe de types de données compatible avec l’entrepôt de données SQL. Consultez l’article sur les [types de données][data types] pour obtenir la liste des types de données non pris en charge et pris en charge. Cette rubrique fournit des solutions de contournement pour les types de hello non pris en charge. Il fournit également une requête tooidentify des types existants qui ne sont pas pris en charge dans l’entrepôt de données SQL.

## <a name="minimize-row-size"></a>Réduction de la taille de ligne
Pour de meilleures performances, réduisez la longueur de la ligne hello de vos tables. Car plus courtes ligne entraîner des performances de toobetter, utilisez hello plus petit types de données qui fonctionnent pour vos données. 

Pour la largeur de ligne de table, PolyBase a une limite de 1 Mo.  Si vous envisagez de données de tooload dans SQL Data Warehouse avec PolyBase, mettre à jour vos tableaux toohave des largeurs de ligne maximale de moins de 1 Mo. 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a>Spécifiez l’option de distribution hello
SQL Data Warehouse est un système de base de données distribuées. Chaque table est distribué ou répliquée sur les nœuds de calcul hello. Il existe une option de table qui vous permet de spécifier comment toodistribute hello des données. choix de Hello est tourniquet (Round Robin) répliquées, ou hachage distribué. Chaque option a ses avantages et inconvénients. Si vous ne spécifiez l’option de distribution hello, SQL Data Warehouse utilisera alternée comme valeur par défaut hello.

- Tourniquet est par défaut de hello. Il est toouse la plus simple de hello et charge les données de hello aussi rapides que possible, mais les jointures nécessitera le déplacement des données, ce qui ralentissent les performances des requêtes.
- Magasins répliquées une copie de la table hello sur chaque nœud de calcul. Les tables répliquées sont performantes, car elles ne nécessitent pas le déplacement des données pour les jointures et les agrégations. Elles requièrent cependant un stockage supplémentaire et sont par conséquent mieux adaptées à des tables plus petites.
- Hachage distribué distribue les lignes hello sur tous les nœuds hello via une fonction de hachage. Tables de hachage distribuée sont cœur hello d’entrepôt de données SQL, car elles sont conçues tooprovide les performances de requête sur des tables volumineuses. Cette option requiert une planification tooselect hello meilleure colonne sur les données de hello toodistribute. Toutefois, si vous n’en choisissez hello de colonne meilleures hello première fois, vous pouvez distribuer facilement nouveau hello des données sur une autre colonne. 

toochoose hello meilleure option de distribution pour chaque table, consultez [Distributed tables](sql-data-warehouse-tables-distribute.md).


## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez migré votre tooSQL de schéma de base de données Data Warehouse, passez tooone Hello suivant des articles :

* [Migration de vos données][Migrate your data]
* [Migration de votre code][Migrate your code]

Pour plus d’informations sur les meilleures pratiques de l’entrepôt de données SQL, consultez hello [meilleures pratiques] [ best practices] l’article.

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
