---
title: "glossaire d’outils de base de données aaaElastic | Documents Microsoft"
description: "Explication des termes utilisés pour les outils de base de données élastique"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>Glossaire des outils de base de données élastique
Hello termes suivants sont définis pour hello [outils de base de données élastique](sql-database-elastic-scale-introduction.md), une fonctionnalité de base de données SQL Azure. outils Hello sont utilisée toomanage [mappe les partitions](sql-database-elastic-scale-shard-map-management.md)et inclure hello [bibliothèque cliente](sql-database-elastic-database-client-library.md), hello [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md), [pools élastiques](sql-database-elastic-pool.md), et [requêtes](sql-database-elastic-query-overview.md). 

Ces termes sont utilisés dans [Ajout d’une partition à l’aide des outils de base de données élastique](sql-database-elastic-scale-add-a-shard.md) et [à l’aide des problèmes du mappage de partitions hello RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md).

![Termes liés ç l’infrastructure flexible][1]

**Base de données**: une base de données SQL Azure. 

**Routage dépendant des données**: hello fonctionnalité qui permet à une partition de tooa application tooconnect une clé de partitionnement spécifique. Consultez [Routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md). Comparer trop**[requête de plusieurs partitions](sql-database-elastic-scale-multishard-querying.md)**.

**Carte de partitions globales**: mappage hello entre les clés de partitionnement et de leurs partitions respectifs dans un **ensemble de partitions**. carte de partitions globales de Hello est stocké dans hello **Gestionnaire de carte de partitions**. Comparer trop**carte de partitions local**.

**Carte de partitions de liste**: carte de partitions dans laquelle les clés de partitionnement sont mappées individuellement. Comparer trop**carte de partitions plage**.   

**Carte de partitions local**: stockés sur une partition, carte de partitions local de hello contient les mappages de shardlets hello qui se trouvent sur les partitions hello.

**Requête de plusieurs partition**: hello capacité tooissue une requête sur plusieurs partitions ; les jeux de résultats sont retournées à l’aide de la sémantique de UNION ALL (également appelée « requête distribution ramifiée »). Comparer trop**routage dépendant des données**.

**Mutualisée** et **mono-utilisateur** : montre une base de données à un seul utilisateur et une base de données à architecture mutualisée :

![Bases de données mono-utilisateur et mutualisée](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Voici une représentation de bases de données **partitionnées** de type mono-utilisateur et mutualisée. 

![Bases de données mono-utilisateur et mutualisée](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Carte de partitions plage**: une carte de partitions dans le hello stratégie de distribution de partition est basée sur plusieurs plages de valeurs contiguës. 

**Tables de référence**: tables qui ne sont pas partitionnées, mais qui sont répliquées sur plusieurs partitions. Par exemple, les codes postaux peuvent être stockés dans une table de référence. 

**Partition**: base de données SQL Azure qui stocke les données provenant d'un jeu de données partitionnées. 

**Élasticité de la partition**: hello tooperform capacité deux **mise à l’échelle horizontale** et **mise à l’échelle verticale**.

**Tables partitionnées**: tables qui sont partitionnées, c'est-à-dire dont les données sont distribuées entre des partitions en fonction de la valeur de leur clé de partitionnement. 

**Clé de partitionnement**: valeur de colonne qui détermine comment les données sont réparties entre les partitions. Hello type valeur peut être un des éléments suivants de hello : **int**, **bigint**, **varbinary**, ou **uniqueidentifier**. 

**Ensemble de partitions**: hello collection de partitions qui sont attribué toohello même carte de partitions dans le Gestionnaire de carte de partitions hello.  

**Shardlet**: toutes les données hello associées à une seule valeur d’une clé de partitionnement sur une partition. Un shardlet est hello plus petite unité de déplacement de données possible lors de la redistribution des tables partitionnées. 

**Carte de partitions**: hello ensemble de mappages entre les clés de partitionnement et de leurs partitions respectifs.

**Gestionnaire de cartes de partitions**: un magasin de données et l’objet d’administration qui contient l’ou les tables précèdent hello partitions, des emplacements de partition et des mappages pour un ou plusieurs ensembles de partitions.

![Mappages][2]

## <a name="verbs"></a>Verbes et adverbes
**Mise à l’échelle horizontale**: act hello de mise à l’échelle (ou) une collection de partitions en ajoutant ou supprimant la carte de partitions partitions tooa, comme indiqué ci-dessous.

![Mise à l’échelle horizontale et verticale][3]

**Fusion**: act hello de déplacement de shardlets à partir de la partition de tooone deux partitions et de mise à jour de carte de partitions hello en conséquence.

**Déplacement de Shardlets**: act hello de déplacement d’une seul shardlet tooa autre partition. 

**Partition**: act hello de partitionnement horizontal identique des données structurées entre plusieurs bases de données basées sur une clé de partitionnement.

**Fractionnement**: act hello du déplacement de plusieurs shardlets à partir de la partition (en général nouveau) de tooanother une seule partition. Une clé de partitionnement est fournie par l’utilisateur de hello comme point de fractionnement hello.

**Mise à l’échelle verticale**: act hello de mise à l’échelle des (ou vers le bas) hello du niveau de performance d’une partition. Par exemple, remplacer une partition à partir de tooPremium Standard (ce qui entraîne davantage de ressources informatiques). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

