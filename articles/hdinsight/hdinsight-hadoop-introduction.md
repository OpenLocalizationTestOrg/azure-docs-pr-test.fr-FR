---
title: "aaaWhat sont HDInsight, pile de technologies hello Hadoop & clusters ? - Azure | Documents Microsoft"
description: "Une pile de technologies de Hadoop tooHDInsight et hello introduction et composants, y compris Spark, Kafka, Hive, HBase pour l’analyse de données volumineuses."
keywords: "Azure hadoop, hadoop azure, hadoop introduction, hadoop introduction, pile de technologies hadoop, introduction toohadoop, toohadoop d’introduction, ce qui est un cluster hadoop, ce qui est le cluster hadoop, ce qui est utilisé hadoop pour"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Introduction tooAzure HDInsight, pile de technologies Hadoop hello et clusters Hadoop
 Cet article fournit une tooAzure introduction HDInsight, une distribution cloud de la pile de technologies hello Hadoop. Il décrit également ce qu’est un cluster Hadoop et quand l’utiliser. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>Qu’est HDInsight et hello technologique Hadoop ? 
Azure HDInsight est une distribution cloud composants Hadoop hello hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) a été les framework open source d’origine hello pour le traitement distribué et l’analyse des jeux de données volumineux sur des clusters d’ordinateurs. 


pile de technologies Hello Hadoop inclut les logiciels et les utilitaires, notamment Apache Hive, HBase, Spark, Kafka et bien d’autres. toosee Hadoop technologie pile composants disponibles sur HDInsight, consultez [composants et les versions disponibles avec HDInsight][component-versioning]. tooread en savoir plus sur Hadoop dans HDInsight, consultez hello [page des fonctionnalités Azure pour HDInsight](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Qu’est-ce qu’un cluster Hadoop et quand l’utiliser ?
*Hadoop* est également un type de cluster disposant de :

* YARN pour la planification de travaux et la gestion de ressources
* MapReduce pour le traitement en parallèle
* Hello du système de fichiers distribués Hadoop (HDFS)
  
Les clusters Hadoop sont souvent utilisés pour le traitement par lots de données stockées. D’autres types de clusters HDInsight incluent des fonctionnalités supplémentaires : Spark est désormais devenu populaire grâce à sa vitesse de traitement en mémoire supérieure. Consultez [Types de cluster sur HDInsight](#overview) pour plus d’informations.

## <a name="what-is-big-data"></a>Que sont les données volumineuses ?
Les données volumineuses correspondent à tout ensemble important d’informations numériques tel que :

* Des données de capteur d’équipement industriel
* Une activité client collectée à partir d’un site web
* Un flux d’actualités Twitter

Les données volumineuses sont collectées dans des volumes toujours plus importants, à des vitesses élevées et pour une incroyable variété de formats. Il peut être historique (c'est-à-dire stockés) ou en temps réel (c'est-à-dire en continu à partir de la source de hello). 

## <a name="overview"></a>Types de cluster dans HDInsight
HDInsight comprend des types de cluster spécifiques et des fonctionnalités de personnalisation de cluster, comme l’ajout de composants, d’utilitaires et de langages.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Spark, Kafka, Interactive Hive, HBase, personnalisés et autres types de cluster
HDInsight offre hello cluster types suivants :

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: utilise [HDFS](#hdfs), [fils](#yarn) gestion des ressources et un simple [MapReduce](#mapreduce) tooprocess de modèle de programmation et analyser les données de traitement par lots en parallèle.
* **[Apache Spark](http://spark.apache.org/)**: une infrastructure de traitement parallèle qui prend en charge des performances de hello tooboost de traitement en mémoire des applications d’analyse de données volumineuses, nouvelles works pour SQL, la diffusion en continu de données et l’apprentissage. Consultez [Qu’est-ce qu’Apache Spark dans HDInsight ?](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)** : base de données NoSQL basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de vastes quantités de données non structurées et semi-structurées (potentiellement, des milliards de lignes multipliées par des millions de colonnes). Consultez [Qu’est-ce que HBase sur HDInsight ?](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)** : serveur pour l’hébergement et la gestion de processus R distribués en parallèle. Il fournit des chercheurs de données, les statisticiens et les programmeurs de R avec l’accès à la demande tooscalable, méthodes distribuées d’analytique sur HDInsight. Consultez l’article [Vue d’ensemble : R Server sur HDInsight](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)** : système de calcul distribué et en temps réel permettant le traitement rapide de vastes flux de données. Storm est fourni en tant que cluster géré dans HDInsight. Consultez la rubrique [Analyse de données de capteur en temps réel au moyen de Storm et de Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Version préliminaire d’Apache Interactive Hive (également appelé Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)** : mise en cache en mémoire autorisant des requêtes Hive interactives et plus rapides. Consultez l’article [Utilisation de Hive interactif dans HDInsight](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)** : plateforme open source utilisée pour créer des applications et des pipelines de données de diffusion en continu. Kafka fournit également des fonctionnalités de file d’attente de messages qui vous permet de toopublish et s’abonner toodata flux. Consultez [Introduction tooApache Kafka sur HDInsight](hdinsight-apache-kafka-introduction.md).

Vous pouvez également configurer des clusters à l’aide de hello méthodes suivantes :
* **[Aperçu de joints au domaine de clusters](hdinsight-domain-joined-introduction.md)**: un cluster joints à un domaine Active Directory de tooan afin que vous pouvez contrôler l’accès et fournir la gouvernance des données.
* **[Clusters personnalisés avec des actions de script](hdinsight-hadoop-customize-cluster-linux.md)** : clusters avec des scripts qui s’exécutent pendant l’approvisionnement et qui installent des composants supplémentaires.

### <a name="example-cluster-customization-scripts"></a>Exemples de scripts de personnalisation de cluster
Actions de script sont des scripts Bash sur Linux qui s’exécutent lors de la configuration de cluster, et qui peut être utilisé tooinstall des composants supplémentaires sur le cluster de hello. 

Hello scripts d’exemple suivants sont fournis par l’équipe de HDInsight hello :

* **[Teinte](hdinsight-hadoop-hue-linux.md)**: ensemble de toointeract d’utiliser des applications web avec un cluster. Clusters Linux uniquement.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: graphique toomodel des relations entre des éléments ou des personnes de traitement.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)** : plateforme de recherche d’entreprise qui permet d’effectuer des recherches en texte intégral sur des données.

Pour plus d’informations sur le développement de vos propres actions de script, consultez [Développement d’actions de Script avec HDInsight](hdinsight-hadoop-script-actions-linux.md).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Composants et utilitaires sur des clusters HDInsight
Hello les composants et les utilitaires suivants sont inclus dans les clusters HDInsight :

* **[Ambari](#ambari)**: approvisionnement, gestion, surveillance des clusters et utilitaires.
* **[Avro](#avro)**  (bibliothèque Microsoft .NET pour Avro) : sérialisation des données pour l’environnement Microsoft .NET hello. 
* **[Hive et HCatalog](#hive)** : interrogation SQL et couche de gestion du stockage et des tables.
* **[Mahout](#mahout)** : pour les applications d’apprentissage automatique évolutives.
* **[MapReduce](#mapreduce)**: infrastructure héritée pour le traitement distribué et la gestion des ressources Hadoop. Consultez [YARN](#yarn).
* **[Oozie](#oozie)**: gestion de flux de travail.
* **[Phoenix](#phoenix)**: couche de base de données relationnelle sur HBase.
* **[Pig](#pig)**: création de scripts simplifiée pour les transformations MapReduce.
* **[Sqoop](#sqoop)**: importation et exportation de données.
* **[Tez](#tez)**: permet de processus nécessitant beaucoup de données toorun efficacement à l’échelle.
* **[FILS](#yarn)**: gestion des ressources qui fait partie de la bibliothèque principale de Hadoop hello.
* **[ZooKeeper](#zookeeper)**: coordination des processus dans les systèmes distribués.

> [!NOTE]
> Pour plus d’informations sur les composants spécifiques hello et les informations de version, consultez [Hadoop composants et les versions dans HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari est destiné à l'approvisionnement, à la gestion et à la surveillance des clusters Apache Hadoop. Elle inclut une collection d’outils de l’opérateur d’intuitive et un ensemble complet d’API qui masquent la complexité hello de Hadoop, ce qui simplifie le fonctionnement de hello de clusters. Clusters HDInsight sur Linux fournissent deux hello Ambari web UI et hello Ambari REST API. Les affichages Ambari sur les clusters HDInsight permettent d’incorporer des éléments d’interface utilisateur.
Consultez [Gestion des clusters HDInsight à l’aide d’Ambari](hdinsight-hadoop-manage-ambari.md) et <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Référence sur l’API Apache Ambari</a>.

### <a name="avro"></a>Avro (bibliothèque Microsoft .NET pour Avro)
Hello bibliothèque Microsoft .NET pour Avro implémente hello Apache Avro le format d’échange des données binaires compact pour la sérialisation pour l’environnement Microsoft .NET hello. Elle définit un schéma sans langage spécifié afin que les données sérialisées dans un langage puissent être lues dans un autre. Vous trouverez des informations détaillées sur le format de hello Bonjour < une cible = _ les href « vide » = « http://avro.apache.org/docs/current/spec.html » > Apache Avro spécification</a>. format Hello Hello de prend en charge les fichiers Avro distributed MapReduce modèle de programmation : les fichiers sont « divisible », ce qui signifie que vous pouvez rechercher n’importe quel point dans un fichier et commence à lire à partir d’un bloc particulier. toofind informations, consultez [sérialiser les données avec hello bibliothèque Microsoft .NET pour Avro](hdinsight-dotnet-avro-serialization.md). Toocome de prise en charge de cluster basé sur Linux.

### <a name="hdfs"></a>HDFS
Système de fichiers distribués Hadoop (HDFS) est un fichier système, avec des fils et MapReduce, core hello de technologie de Hadoop. Il s’agit de système de fichiers standard hello pour les clusters Hadoop dans HDInsight. Consultez [Interrogation des données depuis un stockage compatible avec HDFS](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Hive et HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> est logiciel basé sur Hadoop qui vous permet de tooquery de l’entrepôt de données et gérer de grands ensembles de données dans un stockage distribué à l’aide d’un langage de type SQL appelé HiveQL. Hive, Pig par exemple, est une abstraction qui s’appuie sur MapReduce et qui traduit des requêtes en une série de travaux MapReduce. Ruche est proche système de gestion de la base de données relationnelle tooa que Pig et est utilisé avec des données structurées plus. Pour les données non structurées, Pig est hello meilleur choix. Consultez la rubrique [Utilisation de Hive avec Hadoop dans HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> est une couche de gestion du stockage et des tables pour Hadoop qui vous présente une vue relationnelle des données. Dans HCatalog, vous pouvez lire et écrire des fichiers dans les formats fonctionnant avec le sérialiseur-désérialiseur Hive.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> est une bibliothèque d’algorithmes d’apprentissage automatique s’exécutant sur Hadoop. À l’aide des principes de statistiques, les applications de machine learning enseignent toolearn de systèmes de données et toouse au-delà de comportement futur toodetermine de résultats. Consultez la rubrique [Génération de recommandations de films en utilisant Mahout dans Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce est framework de logiciel hérités hello pour Hadoop pour l’écriture d’applications jeux de données volumineux toobatch processus en parallèle. Une tâche MapReduce fractionne les jeux de données volumineux et organise les données de hello en paires clé-valeur pour le traitement. Les travaux MapReduce s’exécutent sur [YARN](#yarn). Consultez <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> Bonjour Hadoop Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> est un système de coordination de flux de travail qui gère les tâches Hadoop. Il est intégré à la pile de Hadoop hello et prend en charge des travaux Hadoop MapReduce, Pig, Hive et Sqoop. Il peut également être tooschedule utilisé travaux tooa spécifique système, telles que les programmes Java ou des scripts de shell. Voir [Utilisation d’Oozie avec Hadoop](hdinsight-use-oozie-linux-mac.md).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> est une couche de base de données relationnelle sur HBase. Phoenix inclut un pilote JDBC qui vous permet de tooquery et de gérer directement les tables SQL. Phoenix convertit les requêtes et autres instructions en appels d’API NoSQL natifs (au lieu d’utiliser MapReduce), permettant ainsi des applications plus rapides sur les magasins NoSQL. Consultez la page [Utiliser Apache Phoenix et SQuirreL avec les clusters HBase](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> est une plateforme de haut niveau qui vous permet de tooperform des transformations complexes MapReduce sur grands jeux de données à l’aide d’un langage de script simple appelé Pig Latin. Pig traduit les scripts Pig Latin hello afin qu’elles s’exécutent dans Hadoop. Vous pouvez créer les fonctions définies par l’utilisateur (UDF) tooextend Pig Latin. Voir [Utilisation de Pig avec Hadoop](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> est un outil qui permet de transférer des données en bloc entre Hadoop et des bases de données relationnelles, telles que SQL ou d’autres banques de données structurées, avec une efficacité optimale. Consultez la rubrique [Utilisation de Sqoop avec Hadoop](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> est une infrastructure d’application qui repose sur des fichiers YARN Hadoop. Elle exécute des graphiques complexes et acycliques de traitement de données générales. Il est une plus flexible et puissante successeur toohello MapReduce infrastructure qui permet des processus consommatrices de données, tels que Hive, toorun plus efficacement à l’échelle. Consultez la section [Utilisation d’Apache Tez pour des performances améliorées de la rubrique Utilisation de Hive et HiveQL](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache fils est hello nouvelle génération de MapReduce (MapReduce 2.0 ou MRv2) et prend en charge des scénarios, le traitement des données au-delà de MapReduce traitement par lots avec une plus grande évolutivité et de traitement en temps réel. YARN fournit une gestion des ressources et une infrastructure d'application distribuée. Les travaux MapReduce s’exécutent sur YARN. Consultez <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coordonne les processus dans les systèmes distribués de grande taille à l’aide d’un espace de noms hiérarchique partagé de registres de données (znodes). Znodes contenir de petites quantités de métadonnées nécessité toocoordinate processus : état, l’emplacement, configuration et ainsi de suite. Voir un exemple de [ZooKeeper avec un cluster HBase et Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Langages de programmation sur HDInsight
Les clusters HDInsight (Spark, HBase, Kafka, Hadoop et autres clusters) prennent en charge de nombreux langages de programmation, mais certains ne sont pas installés par défaut. Pour les bibliothèques, des modules ou des packages non installés par défaut, [utiliser un composant de script action tooinstall hello](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Prise en charge des langages de programmation par défaut
Par défaut, HDInsight prend en charge :

* Java
* Python

Des langages supplémentaires peuvent être installés à l’aide d’[actions de script](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Langages de machines virtuelles Java (JVM)
Nombreux langages autres que Java peuvent s’exécuter sur une machine virtuelle de Java (JVM) ; Toutefois, l’exécution de certaines de ces langages peut nécessiter des autres composants installés sur le cluster de hello.

Les langages JVM suivants sont pris en charge sur les clusters HDInsight :

* Clojure
* Jython (Python pour Java)
* Scala

### <a name="hadoop-specific-languages"></a>Langages spécifiques à Hadoop
Clusters HDInsight prennent en charge hello suivant des langues qui sont la pile de technologies Hadoop toohello spécifique :

* Pig Latin pour les travaux Pig
* HiveQL pour les travaux Hive et SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard et HDInsight Premium
HDInsight propose deux catégories d’offres de cloud Big Data : Standard et Premium. HDInsight Standard fournit un cluster à l’échelle de l’entreprise que les organisations peuvent utiliser toorun leurs charges de travail de données volumineuses. HDInsight Premium est dérivé des fonctionnalités Standard et introduit des fonctionnalités d’analyse et de sécurité avancées dans un cluster HDInsight. Pour plus d’informations, consultez [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Décisionnel Microsoft et HDInsight
Outils familiers de business intelligence (BI) récupérer, analyser, signalent des données intégrées avec HDInsight à l’aide soit hello complément Power Query ou hello Microsoft ODBC Driver de la ruche :

* [Connecter Excel tooHadoop avec Power Query](hdinsight-connect-excel-power-query.md): Découvrez comment tooconnect Excel toohello compte de stockage Azure stocke hello des données à partir de votre cluster HDInsight à l’aide de Microsoft Power Query pour Excel. Station de travail Windows requise. 
* [Rejoignez Excel tooHadoop hello Microsoft ODBC Driver de la ruche](hdinsight-connect-excel-hive-odbc-driver.md): Découvrez comment tooimport des données à partir de HDInsight avec hello Microsoft ODBC Driver de la ruche. Station de travail Windows requise. 
* [Plateforme Cloud Microsoft](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): en savoir plus sur Power BI pour Office 365, téléchargez la version d’évaluation de SQL Server hello et configurer SharePoint Server 2013 et SQL Server BI.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Étapes suivantes

* [Prise en main de Hadoop dans HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): didacticiel de démarrage rapide pour l’approvisionnement de clusters HDInsight Hadoop et l’exécution d’exemples de requêtes Hive.
* [Prise en main de Spark dans HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): didacticiel de démarrage rapide pour la création d’un cluster Spark et l’exécution de requêtes Spark SQL interactives.
* [Utilisation de R Server sur HDInsight](hdinsight-hadoop-r-server-get-started.md): commencez à utiliser R Server dans HDInsight Premium.
* [Configurer des clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Découvrez comment tooprovision un HDInsight Hadoop de cluster via hello portail Azure, CLI d’Azure ou Azure PowerShell.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/