---
title: "notes d’aaaRelease des composants Hadoop sur Azure HDInsight | Documents Microsoft"
description: "Dernières notes de publication et versions des composants Hadoop pour Azure HDInsight. Obtenez des conseils et détails concernant le développement pour Spark, R Server, Hive et bien plus."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.assetid: a363e5f6-dd75-476a-87fa-46beb480c1fe
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: nitinme
ms.openlocfilehash: ab08a74380fe0bbd7430c1096dca7eb177c11fe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-hadoop-components-on-azure-hdinsight"></a>Notes de publication pour les composants Hadoop sur Azure HDInsight

Cet article fournit des informations sur hello **plus récente** mises à jour de la mise en production Azure HDInsight. Pour plus d’informations sur les versions antérieures, voir [Archive des notes de publication de HDInsight](hdinsight-release-notes-archive.md).

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [l’article sur le contrôle de version de HDInsight](hdinsight-component-versioning.md).


## <a name="notes-for-08012017-release-of-hdinsight"></a>Notes relatives à la version du 01/08/2017 de HDInsight

| Intitulé | Description | Zone concernée  | Type du cluster  | 
| --- | --- | --- | --- | --- |
| Version de Microsoft R Server 9.1 sur HDInsight |HDInsight prend désormais en charge l’approvisionnement des clusters R Server 9.1 sur HDInsight. Pour plus d’informations sur la version Microsoft R Server 9.1, consultez [ce blog](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/). |Service |R Server |
| HDInsight 3.6 inclut désormais les versions plus récentes de la pile de Hadoop hello|<ul><li>Pour obtenir une liste détaillée des versions mises à jour, consultez [Composants Hadoop disponibles avec différentes versions de HDInsight](hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions).</li><li>Pour obtenir la liste des bogues corrigés dans les versions les plus récentes de la pile de Hadoop hello hello, consultez [informations sur le correctif Apache](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/patch_parent.html).</li><li>Pour obtenir la liste des dernières modifications apportées à HDP 2.6.1 (qui est maintenant disponible dans HDInsight 3.6), consultez [https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/behavior_changes.html).</li><li>Pour obtenir la liste des problèmes connus dans HDP 2.6.1, consultez [Problèmes connus](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_release-notes/content/known_issues.html).</li></ul> |Service |Tout |N/A |
| Met à jour des clusters de tooInteractive Hive (version préliminaire) |<ul><li><b>Amélioration de la fonctionnalité.</b> Implémentation du magasin de métadonnées de mise en cache qui réduit la charge hello sur SQL hello du serveur principal en mettant en cache les métadonnées hello et améliore les performances pour toutes les opérations de métadonnées.  Cette amélioration est désormais disponible par défaut sur tous les clusters Hive interactif. Pour plus d’informations, consultez [https://issues.apache.org/jira/browse/HIVE-16520](https://issues.apache.org/jira/browse/HIVE-16520).</li><li><b>Amélioration de la fonctionnalité.</b> Le chargement de la partition dynamique est optimisé. Pour plus d’informations, consultez [https://issues.apache.org/jira/browse/HIVE-14204] (https://issues.apache.org/jira/browse/HIVE-14204).</li><li><b>Amélioration de la fonctionnalité.</b> Optimisations de configuration pour HDInsight sur Linux.</li><li><b>Résolution de bogue.</b> `CredentialProviderFactory$getProviders` n’est pas thread-safe. » Ce problème est maintenant résolu. Pour plus d’informations, consultez [https://issues.apache.org/jira/browse/HADOOP-14195](https://issues.apache.org/jira/browse/HADOOP-14195).</li><li><b>Résolution de bogue.</b> Utilisation élevée de l’UC avec l’API `liststatus` du pilote WASB, entraînant de mauvaises performances ATS. » Ce problème est maintenant résolu. Pour plus d’informations, consultez [https://github.com/Azure/azure-storage-java/pull/154](https://github.com/Azure/azure-storage-java/pull/154).</li></ul> |Service |Hive interactif (version préliminaire) |
| Les mises à jour tooHadoop clusters |La fiabilité des opérations liées au travail Templeton est améliorée. Pour plus d’informations, consultez [https://issues.apache.org/jira/browse/HIVE-15947](https://issues.apache.org/jira/browse/HIVE-15947) |Service |Hadoop |
| Mises à jour YARN | HDInsight crée désormais une base de données Ambari de 250 Go (sans frais supplémentaires), ce qui offre une meilleure expérience pour les clients. Cette modification est censée empêcher la saturation ATS et apporter de meilleures performances. |Service |Tout |
| Mises à jour Spark | Version de Spark 2.1.1. Pour plus d’informations, consultez [Spark Release 2.1.1](https://spark.apache.org/releases/spark-release-2-1-1.html) (Version de Spark 2.1.1). | Service | Spark |

  



## <a name="04062017---general-availability-of-hdinsight-36"></a>06/04/2017 - Disponibilité générale de HDInsight 3.6

* Avec cette version, Azure HDInsight ajoute la version 3.6, qui est basée sur HDP 2.6. Les notes de publication de HDP 2.6 sont disponibles [ici](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html). De plus amples informations sur les versions de HDInsight sont disponibles [ici](hdinsight-component-versioning.md). 3.6 de HDInsight est disponible pour hello suivant les charges de travail :

    * Hadoop v2.7.3
    * HBase v1.1.2
    * Storm v1.1.0
    * Spark v2.1.0
    * Hive interactif v2.1.0

* **Prise en charge de Hive View 2.0**. Cela doit améliorer hello utilisateur pour la ruche interactif. Pour plus d’informations, voir la [documentation Hortonworks](http://docs.hortonworks.com/HDPDocuments/Ambari-2.5.0.3/bk_ambari-views/content/ch_using_hive_view.html).

* **Amélioration des performances avec Hive LLAP**. Pour plus d’informations, voir la [documentation Hortonworks](https://hortonworks.com/blog/top-5-performance-boosters-with-apache-hive-llap/).

* **Nouvelles fonctionnalités Hive** Consultez la [documentation Hortonworks](https://hortonworks.com/apache/hive/#section_4).

* **La ruche CLI désapprobation**: la ruche de CLI est déconseillée et les clients sont encouragé toouse Beeline à la place. Pour plus d’informations, consultez la [documentation Apache](https://cwiki.apache.org/confluence/display/Hive/Replacing+the+Implementation+of+Hive+CLI+Using+Beeline). Pour obtenir des instructions sur la façon de toouse Beeline hdinsight, consultez [Beeline d’utilisation avec HDInsight Hadoop clusters](hdinsight-hadoop-use-hive-beeline.md).

* **Nouvelles fonctionnalités Apache Phoenix et HBase**.
    * Prise en charge du quota de stockage : couramment utilisée dans des environnements mutualisés, cette option permet d’avoir un espace de stockage limité par table et niveau d’espace de noms.
    * Améliorations apportées à l’indexation Phoenix : création d’index incrémentiel et régénération/reprise de l’indexation à partir d’échecs précédents.
    * Outil d’intégrité des données Phoenix : prend en charge la validation de schémas, d’index et d’autres métadonnées.


* **Problème avec HBase**: lors de l’exécution d’un bloc de volume partagé de cluster télécharger tâche MapReduce, hello selon la syntaxe peut entraîner une erreur.

        HADOOP_CLASSPATH=$(hbase mapredcp):/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv

    Hello suivant de syntaxe à la place, utilisez :

        HADOOP_CLASSPATH=/path/to/hbase-protocol.jar:/path/to/hbase/conf hadoop jar phoenix-<version>-client.jar org.apache.phoenix.mapreduce.CsvBulkLoadTool --table EXAMPLE --input /data/example.csv


## <a name="02282017---release-of-spark-21-on-hdinsight-36-preview"></a>Version du 28/02/2017 de Spark 2.1 sur HDInsight 3.6 (préversion)
* [Spark 2.1](http://spark.apache.org/releases/spark-release-2-1-0.html) améliore les nombreux problèmes de stabilité et de convivialité des versions précédentes. Il apporte également de nouvelles fonctionnalités pour toutes les charges de travail Spark telles que Spark Core, SQL, ML et Streaming.
* La fonctionnalité Structured Streaming bénéficie d’une meilleure évolutivité avec prise en charge des filigranes de temps d’événement et du connecteur Kafka 0.10.
* Le partitionnement Spark SQL est désormais géré à l’aide d’un nouveau mécanisme de gestion de partition évolutive. Afficher plus de détails [ici](http://spark.apache.org/releases/spark-release-2-1-0.html) sur la façon de tooupgrade.
* Actuellement, Spark 2.1 sur Azure HDInsight 3.6 en préversion ne prend pas en charge la connectivité des outils décisionnels à l’aide du pilote ODBC.
* L’accès à Azure Data Lake Store à partir de clusters Spark 2.1 n’est pas pris en charge dans cette préversion.


## <a name="11182016---release-of-spark-201-on-hdinsight-35"></a>Version du 18/11/2016 de Spark 2.0.1 sur HDinsight 3.5
Spark 2.0.1 est désormais disponible sur les clusters Spark (HDInsight version 3.5).

## <a name="11162016---release-of-r-server-90-on-hdinsight-35-spark-20"></a>Version du 16/11/2016 de R Server 9.0 sur HDInsight 3.5 (Spark 2.0)
*   R Server clusters incluent désormais option hello pour les deux versions : R Server 9.0 sur HDI 3.5 (Spark 2.0) et R Server 8.0 sur HDI 3.4 (Spark 1.6).
*   R Server 9.0 sur HDI 3.5 (2.0 Spark) repose sur R 3.3.2 et inclut ScaleR nouvelle source de données appelées RxHiveData RxParquetData pour le chargement des données à partir de la ruche de fonctions et Parquet directement tooSpark trames de données pour l’analyse par ScaleR. Pour plus d’informations, consultez hello inline à l’aide sur ces fonctions dans R à l’aide de hello **? RxHiveData** et **? RxParquetData** commandes.
*   RStudio Server community edition est maintenant installé par défaut (avec une option d’annulation) sur le panneau de Configuration de Cluster hello dans le cadre de hello mise en service de flux.

## <a name="11092016---release-of-spark-20-on-hdinsight"></a>Version du 09/11/2016 de Spark 2.0 sur HDinsight
* Les clusters Spark 2.0 sur HDInsight 3.5 prennent désormais en charge les services Livy et Jupyter.

## <a name="10262016---release-of-r-server-on-hdinsight"></a>26/10/2016 - Version de R Server sur HDInsight
* Hello URI pour l’accès de nœud de bord a été modifié trop**clustername**-ed-ssh.azurehdinsight.net
* L’approvisionnement du cluster R Server sur HDInsight a été simplifié.
* R Server sur HDInsight est désormais disponible en tant que type de cluster R Server HDInsight standard, et n’est plus installé comme une application HDInsight distincte. nœud de périmètre Hello et les fichiers binaires de R Server sont maintenant configurés en tant que partie de hello déploiement de cluster de serveurs de R. Cela améliore la vitesse et la fiabilité de l’approvisionnement. Le modèle de tarification de R Server est mis à jour en conséquence.
* Le prix du type de cluster R Server est désormais basé sur le prix de niveau Standard, plus le coût supplémentaire R Server. Le niveau Premium est désormais réservé aux fonctionnalités Premium disponibles sur différents types de clusters, et n’est pas utilisé pour le type de cluster R Server. Cette modification n’affecte pas tarification efficace de R Server ; Il modifie uniquement la façon dont les frais de hello sont présentés dans la nomenclature de hello. Tous les clusters de serveur R existants continuent toowork et modèles du Gestionnaire de ressources pour poursuivre toofunction Notez de désapprobation. **Il est recommandé cependant tooupdate déploiements sous forme de script toouse nouveau gestionnaire de ressources du modèle.**






