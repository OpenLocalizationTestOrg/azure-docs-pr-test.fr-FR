---
title: tooSpark aaaIntroduction sur Azure HDInsight | Documents Microsoft
description: "Cet article fournit une présentation tooSpark sur HDInsight et hello différents scénarios dans lesquels vous pouvez utiliser le cluster Spark sur HDInsight."
keywords: "Nouveautés spark d’apache, cluster spark, introduction toospark, spark sur hdinsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>TooSpark introduction sur HDInsight

Cet article vous offre une tooSpark introduction sur HDInsight. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> est une infrastructure de traitement en parallèle open source qui prend en charge en mémoire traitement tooboost les performances de hello big-applications de données analytiques. Le cluster Spark sur HDInsight est compatible avec Azure Storage (WASB) ainsi qu’avec Azure Data Lake Store afin que vos données existantes stockées dans Azure puissent être facilement traitées via un cluster Spark.

Lorsque vous créez un cluster Spark sur HDInsight, vous créez des ressources de calcul Azure dans lesquelles Spark est installé et configuré. Il n’accepte qu’environ dix minutes de cluster toocreate un Spark dans HDInsight. Hello toobe de données traitée est stockée dans le stockage Azure ou Azure Data Lake Store. Consultez [Utiliser Azure Storage avec HDInsight](hdinsight-hadoop-use-blob-storage.md).

**cluster de toocreate un Spark sur HDInsight**, consultez [démarrage rapide : créer un cluster Spark sur HDInsight et exécuter des requêtes interactives à l’aide du bloc-notes](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Qu’est-ce qu’Apache Spark sur Azure HDInsight ?
Les clusters Spark sur HDInsight proposent un service Spark entièrement géré. Les avantages de la création d’un cluster Spark sur HDInsight sont répertoriés ici.

| Fonctionnalité | Description |
| --- | --- |
| Facilité de création des clusters Spark |Vous pouvez créer un nouveau cluster Spark sur HDInsight en quelques minutes à l’aide de hello portail Azure, Azure PowerShell ou hello HDInsight .NET SDK. Consultez [Prise en main des clusters Spark dans HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Simplicité d'utilisation |Un cluster Spark sur HDInsight inclut des blocs-notes Jupyter et Zeppelin. Vous pouvez les utiliser pour le traitement interactif et la visualisation des données.|
| API REST |Incluent des clusters Spark dans HDInsight [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), une basée sur l’API REST de Spark travail serveur tooremotely submit et moniteur de travaux. |
| Prise en charge d’Azure Data Lake Store | Cluster Spark sur HDInsight peut être configuré toouse Azure Data Lake Store un stockage supplémentaire, ainsi que d’un stockage principal (uniquement avec les clusters HDInsight 3.5). Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble d’Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md). |
| Intégration aux services Azure |Cluster Spark sur HDInsight est fourni avec un tooAzure connecteur concentrateurs d’événements. Les clients peuvent créer des applications de diffusion en continu à l’aide de concentrateurs d’événements hello, en outre trop[Kafka](http://kafka.apache.org/), qui est déjà disponible dans le cadre de Spark. |
| Prise en charge du serveur R | Vous pouvez configurer un serveur R sur HDInsight Spark cluster toorun distributed calculs de R avec des vitesses hello promis avec un cluster Spark. Pour plus d’informations, consultez la section [Prise en main de R Server sur HDInsight](hdinsight-hadoop-r-server-get-started.md). |
| Intégration à des environnements de développement intégrés tiers | HDInsight fournit les plug-ins pour l’IDE comme ne se produise IntelliJ et que vous pouvez utiliser toocreate et soumettre des applications tooan cluster HDInsight Spark d’Eclipse. Pour plus d’informations, consultez [Utiliser le kit de ressources Azure pour IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin.md) et [Utiliser le kit de ressources Azure pour Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Requêtes simultanées |Les clusters Spark sur HDInsight prennent en charge les requêtes simultanées. Cela permet à plusieurs requêtes à partir d’un utilisateur ou de plusieurs requêtes à partir de différents utilisateurs et applications tooshare hello les mêmes ressources de cluster. |
| Mise en cache sur des disques SSD |Vous pouvez choisir les données toocache en mémoire ou dans SSDs attaché toohello les nœuds de cluster. La mise en cache dans la mémoire fournit de meilleures performances des requêtes hello mais peut être coûteuse ; mise en cache dans les disques SSD fournit une option intéressante pour améliorer les performances des requêtes sans nécessité de hello toocreate un cluster dont la taille est requis toofit hello dataset entier en mémoire. |
| Intégration aux outils décisionnels |Les clusters Spark sur HDInsight fournissent des connecteurs pour certains outils décisionnels, notamment [Power BI](http://www.powerbi.com/) et [Tableau](http://www.tableau.com/products/desktop), pour l’analyse des données. |
| Bibliothèques Anaconda préchargées |Les clusters Spark sur HDInsight sont fournis avec des bibliothèques Anaconda préinstallées. [Anaconda](http://docs.continuum.io/anaconda/) fournit les bibliothèques too200 fermer pour l’apprentissage, analyse, visualisation, etc.. |
| Extensibilité |Bien que vous pouvez spécifier le nombre de hello de nœuds dans votre cluster lors de la création, vous souhaitez toogrow ou réduire la charge du cluster toomatch hello. Tous les clusters HDInsight autorisent un nombre de hello toochange de nœuds dans un cluster de hello. En outre, les clusters de Spark peuvent être supprimés sans perte de données comme toutes les données hello est stocké dans le stockage Azure ou Data Lake Store. |
| Support technique 24 heures sur 24, 7 jours sur 7 |Les clusters Spark sur HDInsight sont fournis avec un support technique à l’échelle de l’entreprise assuré 24 heures sur 24, 7 jours sur 7 et un contrat de niveau de service de 99,9 % de disponibilité. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Quelles sont les cas d’usage hello pour Spark sur HDInsight ?
Clusters Spark dans HDInsight activer hello les scénarios clés suivants.

### <a name="interactive-data-analysis-and-bi"></a>Analyse des données interactive et Power BI
[Consulter un didacticiel](hdinsight-apache-spark-use-bi-tools.md)

Apache Spark sur HDInsight stocke les données dans Azure Storage ou Azure Data Lake Store. Experts de l’entreprise et décideurs peuvent analyser et générer des rapports sur ces données et utiliser Microsoft Power BI toobuild des rapports interactifs à partir des données de hello analysé. Les analystes peuvent démarrer à partir des données non structurées/semi structurée dans le stockage de cluster, définir un schéma pour les données de salutation à l’aide d’ordinateurs portables et puis générer des modèles à l’aide de Microsoft Power BI. Les clusters Spark sur HDInsight prennent également en charge plusieurs outils décisionnels tiers comme Tableau, grâce auxquels ils constituent une plateforme idéale pour les analystes de données, les experts et les décideurs clés.

### <a name="spark-machine-learning"></a>Spark Machine Learning
[Consulter un didacticiel : prédiction des températures d’un bâtiment en utilisant des données HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Consulter un didacticiel : prédiction des résultats d’inspections alimentaires](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark est fourni avec [MLlib](http://spark.apache.org/mllib/), bibliothèque d’apprentissage automatique basée sur Spark que vous pouvez utiliser à partir d’un cluster Spark sur HDInsight. Un cluster Spark sur HDInsight inclut également Anaconda, une distribution de Python avec une variété de packages pour l’apprentissage automatique. Ajoutez à cela la prise en charge intégrée des blocs-notes Jupyter et Zeppelin, et vous disposez d’un environnement haut de gamme pour la création d’applications d’apprentissage automatique.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Analyse des données de diffusion en continu et en temps réel Spark
[Consulter un didacticiel](hdinsight-apache-spark-eventhub-streaming.md)

Les clusters Spark sur HDInsight offrent une prise en charge améliorée de la création de solutions d’analyse en temps réel. Alors que Spark a déjà des données des connecteurs tooingest provenant de sources telles que les sockets Kafka, Flume, Twitter, ZeroMQ ou TCP, Spark dans HDInsight ajoute la prise en charge de première classe pour la réception des données à partir d’Azure Event Hubs. Concentrateurs d’événements sont hello les files d’attente de service plus largement utilisés dans Azure. Grâce à leur prise en charge immédiate des concentrateurs d’événements, les clusters Spark sur HDInsight constituent une plateforme idéale pour créer un pipeline d’analyse en temps réel.

## <a name="next-steps"></a>Quels sont les composants inclus dans un cluster Spark ?
Clusters de Spark dans HDInsight incluent hello suivant des composants qui sont disponibles sur les clusters hello par défaut.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Comprend Spark Core, Spark SQL, les API de diffusion en continu Spark, GraphX et MLlib.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Bloc-notes Jupyter](https://jupyter.org)
* [Bloc-notes Zeppelin](http://zeppelin-project.org/)

Les clusters Spark sur HDInsight offrent également une [pilote ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) pour les clusters de tooSpark de connectivité dans HDInsight à partir des Outils BI telles que Microsoft Power BI et de Tableau.

## <a name="where-do-i-start"></a>Par où commencer ?
Commencez par créer un cluster Spark sur HDInsight. Consultez [Démarrage rapide : créer un cluster Spark sur HDInsight Linux et exécuter une requête interactive à l’aide de Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Étapes suivantes
### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
* [Problèmes connus d’Apache Spark sur Azure HDInsight](hdinsight-apache-spark-known-issues.md).
