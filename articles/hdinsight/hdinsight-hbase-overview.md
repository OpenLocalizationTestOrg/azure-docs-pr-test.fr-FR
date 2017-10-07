---
title: "aaaWhat est HBase dans Azure HDInsight ? | Microsoft Docs"
description: "Une présentation tooApache HBase dans HDInsight, une base de données NoSQL build sur Hadoop. En savoir plus sur les cas d’usage et comparer les clusters Hadoop de tooother HBase."
keywords: "Bigtable,NoSQL,présentation de HBase,Apache HBase,HBase,vue d’ensemble de HBase,"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Présentation de HBase dans HDInsight : une base de données NoSQL fournissant des fonctionnalités similaires à BigTable pour Hadoop
Apache HBase est une base de données NoSQL open source, basée sur Hadoop et modélisée d'après Google BigTable. HBase fournit un accès aléatoire et une forte cohérence pour de vastes quantités de données non structurées et semi-structurées, dans une base de données sans schéma, organisée par familles de colonnes.

Données sont stockées dans les lignes hello d’une table et les données au sein d’une ligne sont regroupées par famille de la colonne. HBase est une base de données logique hello que ni hello colonnes ni type hello des données stockées dans les schemaless toobe défini avant de les utiliser. code open-source de Hello linéairement pétaoctets toohandle de données sur des milliers de nœuds. Il peut reposer sur la redondance des données, le traitement par lots et d’autres fonctionnalités fournies par les applications distribuées dans l’écosystème de Hadoop hello.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>L'implémentation de HBase dans Azure HDInsight
HDInsight HBase est proposé en tant que cluster géré qui est intégré à hello environnement Azure. les clusters Hello sont données toostore configuré directement dans [Azure Storage](./hdinsight-hadoop-use-blob-storage.md) ou [Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md), qui fournit une latence faible et élasticité accrue dans les options de performances et de coût. Cela permet aux clients toobuild sites Web interactifs qui fonctionnent avec des jeux de données volumineux, les services toobuild qui stockent les données de capteur et les données de télémétrie à partir des millions de points de terminaison et tooanalyze ces données avec des travaux Hadoop. HBase et Hadoop sont un bon point de départ pour le projet de données volumineuses dans Azure ; en particulier, ils peuvent activer toowork d’applications en temps réel avec les jeux de données volumineux.

implémentation de HDInsight Hello s’appuie sur l’architecture de montée en puissance parallèle hello de HBase tooprovide automatique partitionnement des tables, la cohérence forte pour les lectures et écritures et le basculement automatique. Les performances sont optimisées par la mise en cache en mémoire des lectures et par des écritures en diffusion à débit élevé. Vous pouvez créer un cluster HBase au sein du réseau virtuel. Pour en savoir plus, voir [Création de clusters HBase sur Azure Virtual Network][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Mode de gestion des données HDInsight HBase
Données peuvent être gérées dans HBase à l’aide de hello `create`, `get`, `put`, et `scan` commandes hello shell HBase. Données sont écrites toohello de base de données à l’aide de `put` et lire à l’aide de `get`. Hello `scan` commande est utilisée tooobtain des données provenant de plusieurs lignes dans une table. Données peuvent également être gérées à l’aide de hello HBase API c#, qui fournit une bibliothèque cliente par-dessus hello HBase REST API. Une base de données HBase peut également être interrogée au moyen de Hive. Pour un toothese de présentation des modèles de programmation, consultez [commencer à utiliser HBase avec Hadoop dans HDInsight][hbase-get-started]. Processeurs sont également disponibles, qui permettent le traitement des données dans les nœuds hello cette base de données hôte hello.

> [!NOTE]
> Thrift n’est pas pris en charge par HBase dans HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Scénarios : cas d'utilisation pour HBase
Hello cas d’usage canonique pour le BigTable (et par extension, HBase) a été créé a été recherche sur le web. Moteurs de recherche créer des index qui mappent les pages web termes toohello qui les contiennent. Mais il existe de nombreux autres cas d'utilisation pour lesquels HBase est adapté : plusieurs sont répertoriés dans cette section.

* stockage clé-valeur
  
    HBase peut être utilisé comme stockage clé-valeur et convient pour la gestion des systèmes de messagerie. Facebook utilise HBase pour son système de messagerie et il est idéal pour le stockage et la gestion des communications Internet. WebTable utilise toosearch HBase pour et gérer les tables extraites à partir des pages Web.
* données de capteur
  
    HBase est utile pour la capture de données collectées de façon incrémentielle à partir de diverses sources. Cela inclut l'analytique sociale, les séries chronologiques, la mise à jour des tableaux de bord interactifs avec les tendances et les compteurs, et la gestion de systèmes de journal d'audit. Opérateur Bloomberg Terminal Server sont des exemples et hello ouvrir série de base de données (OpenTSDB), qui stocke et fournit l’accès toometrics collectées sur intégrité hello des systèmes serveur.
* requête en temps réel
  
    [Phoenix](http://phoenix.apache.org/) est un moteur de requête SQL pour Apache HBase. Il est accessible en tant que pilote JDBC et permet d'interroger et de gérer les tables HBase au moyen de SQL.
* HBase en tant que plateforme
  
    Les applications peuvent fonctionner par-dessus HBase, en l'utilisant comme banque de données. Exemples : Phoenix, OpenTSDB, Kiji et Titan. Les applications peuvent également s'intégrer à HBase. Exemples : Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia et Drill.

## <a name="next-steps"></a>Étapes suivantes
* [Prise en main de HBase avec Hadoop dans HDInsight][hbase-get-started]
* [Création de clusters HBase sur Azure Virtual Network][hbase-provision-vnet]
* [Configuration de la géo-réplication HBase dans HDInsigtht](hdinsight-hbase-replication.md)
* [Analyse de sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment]
* [Utiliser des applications Java Maven toobuild qui utilisent HBase hdinsight (Hadoop)][hbase-build-java-maven]

## <a name="see-also"></a>Voir aussi
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable : un système de stockage distribué pour les données structurées](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
