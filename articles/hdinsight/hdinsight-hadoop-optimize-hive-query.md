---
title: "aaaOptimize ruche les requêtes dans Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toooptimize votre ruche interroge pour Hadoop dans HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Optimisation des requêtes Hive dans Azure HDInsight

Par défaut, les clusters Hadoop ne sont pas optimisés pour les performances. Cet article traite de certaines méthodes de l’optimisation de performances ruche plus courantes que vous pouvez appliquer des requêtes tooyour.

## <a name="scale-out-worker-nodes"></a>Montée en charge des nœuds de travail

Augmentation du nombre hello de nœuds de travail dans un cluster peut exploiter plus toobe REDUCTEURS et des mappeurs de s’exécuter en parallèle. Il existe deux manières d’accroître la montée en charge dans HDInsight :

* Au moment de configurer hello, vous pouvez spécifier le nombre hello de nœuds de travail à l’aide de hello portail Azure, Azure PowerShell ou une interface de ligne inter-plateformes.  Pour plus d’informations, consultez la rubrique [Création de clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Hello capture d’écran suivante montre les processus de travail hello configuration du nœud sur hello portail Azure :
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Au moment de l’exécution de hello, vous pouvez également monter en charge un cluster sans avoir à recréer un :

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Pour plus d’informations sur les différentes machines virtuelles hello, pris en charge par HDInsight, consultez [tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Activation de Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) est un moteur de remplacement de l’exécution du moteur toohello MapReduce :

![tez_1][image-hdi-optimize-hive-tez_1]

Tez est plus rapide pour les raisons suivantes :

* **Exécutez graphique acyclique dirigé (DAG) en tant qu’une seule tâche dans le moteur de MapReduce hello**. Hello DAG nécessite chaque ensemble de toobe mappeurs suivi d’un ensemble de REDUCTEURS. Cela entraîne plusieurs toobe de travaux MapReduce tourné pour chaque requête Hive. Tez n’a pas de telles contraintes et peut traiter un graphique orienté acyclique comme une tâche unique, ce qui réduit la surcharge de démarrage de tâche.
* **Il évite les écritures inutiles**. En raison de travaux toomultiple est tourné pour hello même requête Hive dans le moteur MapReduce hello, sortie hello de chaque travail est écrit tooHDFS pour les données intermédiaires. Étant donné que Tez réduit le nombre de tâches pour chaque requête Hive qu'il est en mesure de tooavoid inutiles en écriture.
* **Il réduit les délais de démarrage**. Tez est le délai de démarrage toominimize en mesure de mieux en réduisant le nombre hello de mappeurs, qu'il doit toostart et également améliorer l’optimisation dans l’ensemble.
* **Il réutilise les conteneurs**. Chaque fois que Tez possible est que la latence en raison de tooreuse en mesure de conteneurs tooensure toostarting des conteneurs est réduite.
* **Il utilise des techniques d’optimisation continue**. Généralement, l’optimisation est effectuée lors de la compilation. Toutefois, vous trouverez plus d’informations sur les entrées de hello qui permettent une meilleure optimisation pendant l’exécution. Tez utilise des techniques d’optimisation continue qui lui permet de plan de hello toooptimize davantage en phase d’exécution hello.

Pour plus d’informations sur ces concepts, consultez [Apache TEZ](http://hortonworks.com/hadoop/tez/).

Vous pouvez choisir n’importe quelle requête Hive Tez activé en attribuant un requête de hello paramètre hello ci-dessous :

    set hive.execution.engine=tez;

Tez est activé par défaut pour les clusters HDInsight basés sur Linux.


## <a name="hive-partitioning"></a>Partitionnement Hive

L’opération d’e/s est goulot d’étranglement de performances hello pour l’exécution de requêtes Hive. performances de Hello peuvent être améliorées si quantité hello de données toobe lecture peut être réduite. Par défaut, les requêtes Hive analysent l’ensemble des tables Hive. Cela est très utile pour les requêtes telles que les analyses de tables. Toutefois pour les requêtes qui doivent uniquement tooscan une petite quantité de données (par exemple, les requêtes avec un filtrage), ce comportement crée inutile surcharge. Partitionnement de la ruche permet de ruche requêtes tooaccess uniquement hello quantité de données dans les tables de la ruche.

Partitionnement de la ruche est implémenté par la réorganisation des données brutes hello dans nouveaux répertoires avec chaque partition ayant son propre répertoire - où la partition de hello est définie par l’utilisateur de hello. Hello diagramme suivant illustre une table Hive le partitionnement par colonne de hello *année*. Un nouveau répertoire est créé pour chaque année.

![partitionnement][image-hdi-optimize-hive-partitioning_1]

Considérations relatives au partitionnement :

* **Évitez les sous-partitionnements** : les partitionnements appliqués à des colonnes contenant uniquement quelques valeurs peuvent entraîner quelques partitions. Par exemple, partitionnement sexe crée uniquement de deux partitions toobe créé (hommes et femmes), donc uniquement réduire la latence de hello en un maximum de moitié.
* **Pas sur la partition** - dans hello inverse, si vous créez une partition sur une colonne avec une valeur unique (par exemple, userid), plusieurs partitions. Sur la partition entraîne de stress sur hello cluster namenode car elle a toohandle hello grand nombre de répertoires.
* **Évitez le décalage de données** : choisissez votre clé de partitionnement avec soin, pour que toutes les partitions soient de taille égale. Un exemple est le partitionnement sur *état* peut entraîner le nombre de hello d’enregistrements sous Californie toobe presque 30 x qui du Vermont en raison de la différence de toohello de remplissage.

toocreate une table de partition, utilisez hello *partitionnée par* clause :

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Après la création de la table partitionnée de hello, vous pouvez créer un partitionnement statique ou le partitionnement dynamique.

* **Partitionnement statique** signifie que les données déjà partitionnées Bonjour les répertoires adéquats et vous pouvez demander des partitions de ruche manuellement basées sur l’emplacement du répertoire hello. Hello suivant extrait de code est un exemple.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Le partitionnement dynamique** signifie que vous voulez ruche toocreate partitions automatiquement pour vous. Étant donné que nous avons déjà créé hello partitionnement de table à partir de la table intermédiaire de hello, il suffit de toodo est table toohello partitionnée de données insert :
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Pour plus d’informations, consultez [Tables partitionnées](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Utilisez le format ORCFile hello
Hive prend en charge différents formats de fichier. Par exemple :

* **Texte**: il s’agit du format de fichier par défaut hello et fonctionne avec la plupart des scénarios
* **Avro**: fonctionne correctement avec les scénarios d’interopérabilité
* **ORC/Parquet**: adapté pour les performances

Format ORC (optimisée en ligne en colonnes) est un toostore hautement efficace des données de ruche. Formats tooother comparés, ORC a hello suivant avantages :

* prise en charge des types complexes, notamment les types DateTime, ainsi que les types semi-structurés ;
* la compression de too70 %
* création d’index toutes les 10 000 lignes, ce qui permet d’ignorer des lignes ;
* baisse significative de l’exécution du démarrage.

format ORC tooenable, vous créez une table avec la clause de hello *stockés en tant que ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Vous insérez ensuite la table de données toohello ORC à partir de la table intermédiaire de hello. Par exemple :

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

Vous pouvez en savoir plus sur le format ORC hello [ici](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vectorisation

Vectorisation permet la ruche tooprocess un lot de 1024 lignes ensemble au lieu de traiter une ligne à la fois. Cela signifie que des opérations simples sont effectuées plus rapidement car toorun a besoin de moins de code interne.

tooenable vectorisation préfixe votre requête Hive avec hello suivant paramètre :

    set hive.vectorized.execution.enabled = true;

Pour plus d’informations, consultez la page [Exécution de requêtes vectorisées](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Autres méthodes d’optimisation
Vous pouvez envisager plusieurs autres méthodes d’optimisation, par exemple :

* **La ruche de création de compartiments :** une technique qui permet de toocluster ou segment de grands jeux de données toooptimize des performances des requêtes.
* **L’optimisation de jointure :** l’optimisation de l’exécution de requêtes de la ruche du planning tooimprove hello l’efficacité de jointures et réduire les besoins de hello pour les indicateurs de l’utilisateur. Pour plus d’informations, consultez la page [Optimisation des jointures](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Augmentez les raccords de réduction**.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris plusieurs méthodes d’optimisation courantes des requêtes. toolearn, voir hello suivant des articles :

* [Utilisation d’Apache Hive dans HDInsight](hdinsight-use-hive.md)
* [Analyse des données sur les retards de vol avec Hive dans HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analyse des données Twitter avec Hive dans HDInsight](hdinsight-analyze-twitter-data.md)
* [Analyser les données de capteur à l’aide de hello Console de requête Hive sur Hadoop dans HDInsight](hdinsight-hive-analyze-sensor-data.md)
* [Utilisez la ruche avec des journaux de tooanalyze HDInsight à partir de sites Web](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
