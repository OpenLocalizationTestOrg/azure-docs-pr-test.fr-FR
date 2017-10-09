---
title: "aaaTroubleshoot Hive à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses toocommon des questions sur l’utilisation d’Apache Hive et Azure HDInsight."
keywords: "Azure HDInsight, Hive, FAQ, guide de dépannage, questions courantes"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Résolution de problèmes Hive à l’aide d’Azure HDInsight

En savoir plus sur les questions supérieur hello et leurs résolutions lorsque vous travaillez avec des charges utiles d’Apache Hive dans Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Comment exporter un metastore Hive et l’importer dans un autre cluster ?


### <a name="resolution-steps"></a>Étapes de résolution

1. Se connecter toohello HDInsight cluster à l’aide d’un client Secure Shell (SSH). Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).

2. Exécutez hello suivant de commande de cluster HDInsight de hello à partir de laquelle vous souhaitez que le magasin de métadonnées tooexport hello :

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Cette commande génère un fichier nommé alltables.sql.

3. Copiez hello fichier alltables.sql toohello nouveau cluster HDInsight, puis exécutez hello de commande suivante :

  ```apache
  hive -f alltables.sql
  ```

code Hello dans les étapes de résolution hello part du principe que les données sont des chemins d’accès sur le nouveau cluster de hello même hello en tant que chemins d’accès de données hello sur l’ancien cluster de hello. Si les chemins d’accès des données hello sont différentes, vous pouvez modifier manuellement hello généré alltables.sql fichier tooreflect toutes les modifications.

### <a name="additional-reading"></a>Documentation supplémentaire

- [Se connecter tooan HDInsight cluster à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Comment localiser les journaux Hive sur un cluster ?

### <a name="resolution-steps"></a>Étapes de résolution

1. Connecter le cluster HDInsight de toohello à l’aide de SSH. Pour plus d’informations, consultez la section **Documentation supplémentaire**.

2. journaux du client tooview Hive, utilisez hello de commande suivante :

  ```apache
  /tmp/<username>/hive.log 
  ```

3. journaux de magasin de métadonnées Hive tooview, utilisez hello de commande suivante :

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver journaux, utilisez hello de commande suivante :

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Documentation supplémentaire

- [Se connecter tooan HDInsight cluster à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Comment lancer hello shell Hive avec des configurations spécifiques sur un cluster

### <a name="resolution-steps"></a>Étapes de résolution

1. Spécifiez une paire clé-valeur de configuration lorsque vous démarrez hello ruche shell. Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist toutes les configurations efficaces sur shell Hive, hello utilisation suivant de commandes :

  ```apache
  hive> set;
  ```

  Par exemple, utilisez hello suivant l’interface de commande toostart Hive avec la journalisation du débogage activée sur la console de hello :

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Documentation supplémentaire

- [Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties) (Propriétés de configuration Hive, en anglais)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Comment analyser les données de DAG Tez sur un chemin critique de cluster ?


### <a name="resolution-steps"></a>Étapes de résolution
 
1. tooanalyze un Tez Apache dirigées graphique acyclique (DAG) sur un graphique de cluster critiques, connecter le cluster HDInsight de toohello à l’aide de SSH. Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).

2. À l’invite de commandes, exécutez hello de commande suivante :
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist autres analyseurs qui peuvent être utilisé tooanalyze Tez DAG, utilisez hello de commande suivante :

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Vous devez fournir un exemple de programme en tant que premier argument de hello.

  Noms de programme valides :
    - **ContainerReuseAnalyzer**: Imprimer les détails de réutilisation du conteneur dans un DAG
    - **CriticalPath**: chemin d’accès critique rechercher hello d’un groupe DAG
    - **LocalityAnalyzer**: Imprimer les détails de localité dans un DAG
    - **ShuffleTimeAnalyzer**: analyser les détails de temps de lecture aléatoire hello dans un DAG
    - **SkewAnalyzer**: analyser les informations de décalage hello dans un DAG
    - **SlowNodeAnalyzer**: Imprimer les détails des nœuds dans un DAG
    - **SlowTaskIdentifier**: Imprimer les détails des tâches lentes dans un DAG
    - **SlowestVertexAnalyzer**: Imprimer les détails des données vertex les plus lentes dans un DAG
    - **SpillAnalyzer**: Imprimer les détails de dépassement dans un DAG
    - **TaskConcurrencyAnalyzer**: imprimer les détails d’accès concurrentiel de tâche hello dans un groupe DAG
    - **VertexLevelCriticalPathAnalyzer**: chemin d’accès critique rechercher hello au niveau de sommets dans un DAG


### <a name="additional-reading"></a>Documentation supplémentaire

- [Se connecter tooan HDInsight cluster à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Comment télécharger des données de DAG Tez à partir d’un cluster ?


#### <a name="resolution-steps"></a>Étapes de résolution

Il existe deux façons de données de Tez DAG toocollect hello :

- À partir de la ligne de commande hello :
 
    Connecter le cluster HDInsight de toohello à l’aide de SSH. À l’invite de commandes hello exécutez hello de commande suivante :

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Utilisez hello Ambari Tez vue :
   
  1. Accédez à tooAmbari. 
  2. Vue tooTez accédez (sous l’icône de vignettes hello dans le coin supérieur droit de hello). 
  3. Sélectionnez hello DAG souhaité tooview.
  4. Select **Download data** (Télécharger les données).

### <a name="additional-reading-end"></a>Documentation supplémentaire

[Se connecter tooan HDInsight cluster à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






