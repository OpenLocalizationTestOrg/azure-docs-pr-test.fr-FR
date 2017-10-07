---
title: "aaaLearn sur les opérations de l’entrepôt de données SQL Azure | Documents Microsoft"
description: "La flexibilité de SQL Data Warehouse vous permet d’accroître, de réduire ou d’interrompre la puissance de calcul en valorisant une mise à l’échelle de glissement d’unités d’entrepôt de données (DWU). Cet article explique les mesures de l’entrepôt de données hello et leur interaction tooDWUs. "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Charge de travail de l’entrepôt de données
Une charge de travail de l’entrepôt de données fait référence à tooall d’opérations hello cours par rapport à un entrepôt de données. charge de travail entrepôt de données Hello englobe hello ensemble du processus de chargement de données dans l’entrepôt de hello, analyse de la création de rapports sur l’entrepôt de données hello, la gestion des données dans l’entrepôt de données hello et exportation de données à partir de l’entrepôt de données hello. Hello profondeur et la largeur de ces composants sont souvent modifier son niveau de maturité de l’entrepôt de données hello hello.

## <a name="new-toodata-warehousing"></a>Nouvelle toodata entreposage ?
Un entrepôt de données est une collection de données qui sont chargées à partir d’un ou plus de données sources et qu’il est utilisé tooperform tâches business intelligence telles que des analyses de données et de création de rapports.

Entrepôts de données sont caractérisent par des requêtes qui analyse le plus grand nombre de lignes, de grandes plages de données et peuvent retourner des résultats relativement volumineux à des fins de hello d’analyse et de création de rapports. Les entrepôts de données sont également caractérisés par des charges de données relativement importantes, alors que les opérations d’insertion/de mise à jour/de suppression au niveau transactionnel sont de petite taille.

* Un entrepôt de données offre de meilleures performances lorsque les données de hello stockées d’une manière qui optimise les requêtes qui demandent tooscan un grand nombre de lignes ou de grandes plages de données. Ce type d’analyse fonctionne mieux lorsque les données de hello sont stockées et recherchées par colonnes, au lieu de lignes.

> [!NOTE]
> index columnstore en mémoire de Hello, qui utilise le stockage de la colonne, fournit des gains de compression too10x et 100 x des gains de performances de requête sur des arborescences binaires traditionnels pour les requêtes de création de rapports et analytique. Nous estimons que l’index columnstore en tant que hello standard pour le stockage et l’analyse des données dans un entrepôt de données volumineuses.
> 
> 

* Un entrepôt de données présente des exigences différentes d’un système ; il est configuré pour le traitement transactionnel en ligne (OLTP, online transaction processing). Hello système OLTP possède de nombreuses insérer, mettre à jour et les opérations de suppression. Ces opérations de recherche toospecific des lignes dans la table de hello. Recherches de table fonctionnent de manière optimale lorsque les données de hello stockées sous forme de ligne par ligne. les données de salutation peuvent être triées et rapidement une division de recherche et conquérir approche appelée une recherche binaire de l’arborescence ou btree.

## <a name="data-loading"></a>Chargement de données
Le chargement de données est une grande partie de la charge de travail entrepôt de données hello. Les entreprises ont généralement un système OLTP occupé qui effectue le suivi des modifications à jour hello lorsque les clients génèrent des transactions commerciales. Périodiquement, souvent nuit pendant une fenêtre de maintenance, les transactions de hello sont déplacées ou copiées de l’entrepôt de données toohello. Une fois les données de salutation dans l’entrepôt de données hello, les analystes peuvent effectuer une analyse et prendre des décisions sur les données de salutation.

* En règle générale, les processus hello de chargement est appelée ETL pour l’extraction, transformation et chargement. Les données doivent généralement toobe transformé afin qu’il soit cohérent avec les autres données de l’entrepôt de données hello. Auparavant, les entreprises utilisé transformations d’hello tooperform à des serveurs ETL dédiées. Désormais, avec un tel traitement rapide massivement parallèle, vous pouvez charger des données dans l’entrepôt de données SQL tout d’abord et puis effectuer des transformations de hello. Ce processus est appelé extraction, de charger et transformer (ELT) et devient un nouveau standard pour les charges de travail entrepôt de données hello.

> [!NOTE]
> En vous dotant de SQL Server 2016, vous pouvez effectuer des analyses en temps réel sur une table OLTP. Cela ne pas remplacer le besoin de hello pour un toostore de l’entrepôt de données et analyser les données, mais il fournit une analyse de tooperform moyen en temps réel.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Requêtes de rapports et d’analyse
Les requêtes de rapports et d’analyse sont bien souvent classées en tant que requêtes réduites, intermédiaires ou importantes en fonction du nombre de critères, mais elles sont généralement basées sur des intervalles de temps. La plupart des entrepôts de données comportent une charge de travail hybride, comprenant à la fois des requêtes à courte échéance et à longue échéance. Dans chaque cas, il est important toodetermine cette combinaison et la toodetermine sa fréquence (horaire, quotidien, mensuel, trimestriel et ainsi de suite). Il est important toounderstand qui hello la charge de travail de requêtes mixtes, couplée avec la concurrence, responsable tooproper planification de capacité pour un entrepôt de données.

* Planification de la capacité peut être une tâche complexe pour une charge de travail des requêtes mixtes, notamment lorsque vous avez besoin d’un entrepôt de données de produits longs temps tooadd capacité toohello. SQL Data Warehouse supprime urgence hello de planification de la capacité dans la mesure où vous pouvez développer et réduire la capacité de calcul à tout moment et depuis le stockage et la capacité de calcul sont dimensionnées de manière indépendante.

### <a name="data-management"></a>Gestion des données
La gestion des données sont importante, en particulier lorsque vous savez que peut manquer d’espace disque dans hello futur proche. Entrepôts de données généralement divisent les données de salutation plages significatives, qui sont stockés sous forme de partitions dans une table. Tous les produits en fonction de SQL Server vous permettent de déplacer des partitions dans et hors de la table de hello. Cette partition basculement vous permet de déplacer les anciennes données accessible sans onéreux et conserver les données les plus récentes hello disponibles sur le stockage en ligne.

* Les index Columnstore prennent en charge les tables partitionnées. Le cas échéant, les tables partitionnées sont utilisées pour la gestion et l’archivage des données. Dans les tables stockées ligne par ligne, les partitions jouent un rôle plus important dans l’amélioration des performances des requêtes.  
* PolyBase est essentiel à la gestion des données. À l’aide de PolyBase, vous avez hello option tooarchive plus anciennes données tooHadoop ou le stockage d’objets blob Azure.  Cela fournit un grand nombre d’options dans la mesure où les données de salutation sont encore en ligne.  Peut prendre plus de temps tooretrieve données depuis Hadoop, mais compromis hello de temps de récupération peuvent dépasser le coût du stockage hello.

### <a name="exporting-data"></a>Exportation de données
Données toomake monodirectionnelle disponibles pour les rapports et d’analyse sont toosend de tooservers de l’entrepôt de données hello dédié pour l’exécution de rapports et l’analyse. Ces serveurs sont appelés mini-Data Warehouses. Par exemple, vous pouvez prétraiter les données de rapport et puis l’exporter à partir de serveurs de réduire de l’entrepôt de données hello monde hello toomake largement disponible pour les analystes et les clients.

* Pour générer des rapports, chaque nuit vous pourriez remplir des serveurs de rapports en lecture seule avec un instantané des données quotidiennes de hello. Ainsi, la bande passante plus élevée pour les clients tout en réduisant les besoins de ressources de calcul hello sur l’entrepôt de données hello. À partir d’un aspect de la sécurité, mini-data warehouses permettent de nombre de hello tooreduce d’utilisateurs qui disposent de l’entrepôt de données access toohello.
* Pour l’analytique, vous pouvez créer un cube d’analyse sur l’entrepôt de données hello et exécuter l’analyse par rapport à l’entrepôt de données hello, ou prétraiter les données et serveur d’analyse toohello pour analytique davantage l’exporter.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous connaissez un peu SQL Data Warehouse, découvrez comment tooquickly [créer un entrepôt de données SQL] [ create a SQL Data Warehouse] et [charger les données d’exemple][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
