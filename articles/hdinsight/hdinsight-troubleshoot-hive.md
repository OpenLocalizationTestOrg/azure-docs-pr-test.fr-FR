---
title: "Résolution de problèmes Hive à l’aide d’Azure HDInsight | Microsoft Docs"
description: "Obtenez les réponses aux questions courantes sur l’utilisation d’Apache Hive et d’Azure HDInsight."
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
ms.date: 11/2/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: 398cc7cd0fa815f12ba5b503a1328688e1159eee
ms.sourcegitcommit: 3df3fcec9ac9e56a3f5282f6c65e5a9bc1b5ba22
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/04/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Résolution de problèmes Hive à l’aide d’Azure HDInsight

Découvrez les principaux problèmes rencontrés lors de l’utilisation de charges utiles Apache Hive dans Apache Ambari, et leur résolution.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Comment exporter un metastore Hive et l’importer dans un autre cluster ?


### <a name="resolution-steps"></a>Étapes de résolution

1. Connectez-vous au cluster HDInsight à l’aide d’un client Secure Shell (SSH). Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).

2. Exécutez la commande suivante sur le cluster HDInsight à partir duquel vous souhaitez exporter le metastore :

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Cette commande génère un fichier nommé alltables.sql.

3. Copiez le fichier alltables.sql dans le nouveau cluster HDInsight et exécutez la commande suivante :

  ```apache
  hive -f alltables.sql
  ```

Le code présenté dans les étapes de résolution suppose que les chemins de données du nouveau cluster sont les mêmes que sur l’ancien cluster. Si les chemins d’accès aux données sont différents, vous pouvez modifier manuellement le fichier alltables.sql généré pour refléter ces modifications.

### <a name="additional-reading"></a>Documentation supplémentaire

- [Se connecter à HDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Comment localiser les journaux Hive dans un cluster ?

### <a name="resolution-steps"></a>Étapes de résolution

1. Connectez-vous au cluster HDInsight à l’aide de SSH. Pour plus d’informations, consultez la section **Documentation supplémentaire**.

2. Pour afficher les journaux du client Hive, utilisez la commande suivante :

  ```apache
  /tmp/<username>/hive.log 
  ```

3. Pour afficher les journaux du metastore Hive, utilisez la commande suivante :

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. Pour afficher les journaux du serveur Hive, utilisez la commande suivante :

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Documentation supplémentaire

- [Se connecter à HDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-the-hive-shell-with-specific-configurations-on-a-cluster"></a>Comment lancer l’interpréteur de commandes Hive avec des configurations spécifiques dans un cluster ?

### <a name="resolution-steps"></a>Étapes de résolution

1. Spécifiez une paire clé-valeur de configuration lorsque vous démarrez l’interpréteur de commandes Hive. Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. Pour répertorier toutes les configurations actives sur l’interpréteur de commandes Hive, utilisez la commande suivante :

  ```apache
  hive> set;
  ```

  Par exemple, utilisez la commande suivante pour démarrer l’interpréteur de commandes Hive avec l’option d’enregistrement de débogage activée sur la console :

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Documentation supplémentaire

- [Hive configuration properties](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties) (Propriétés de configuration Hive, en anglais)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Comment analyser les données de DAG Tez dans un chemin critique de cluster ?


### <a name="resolution-steps"></a>Étapes de résolution
 
1. Pour analyser un graphe orienté acyclique (DAG) Apache Tez sur un chemin critique de cluster, connectez-vous au cluster HDInsight à l’aide de SSH. Pour plus d’informations, consultez la section [Documentation supplémentaire](#additional-reading-end).

2. Depuis une invite de commandes, exécutez la commande suivante :
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. Pour obtenir la liste des autres analyseurs pouvant être utilisés pour analyser les informations de DAG Tez, utilisez la commande suivante :

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Vous devez fournir un exemple de programme comme premier argument.

  Noms de programme valides :
    - **ContainerReuseAnalyzer**: Imprimer les détails de réutilisation du conteneur dans un DAG
    - **CriticalPath**: Trouver le chemin critique d’un DAG
    - **LocalityAnalyzer**: Imprimer les détails de localité dans un DAG
    - **ShuffleTimeAnalyzer**: Analyser les détails de délai de lecture aléatoire dans un DAG
    - **SkewAnalyzer**: Analyser les détails d’asymétrie dans un DAG
    - **SlowNodeAnalyzer**: Imprimer les détails des nœuds dans un DAG
    - **SlowTaskIdentifier**: Imprimer les détails des tâches lentes dans un DAG
    - **SlowestVertexAnalyzer**: Imprimer les détails des données vertex les plus lentes dans un DAG
    - **SpillAnalyzer**: Imprimer les détails de dépassement dans un DAG
    - **TaskConcurrencyAnalyzer**: Imprimer les détails de simultanéité des tâches dans un DAG
    - **VertexLevelCriticalPathAnalyzer**: Trouver le chemin critique au niveau des données vertex dans un DAG


### <a name="additional-reading"></a>Documentation supplémentaire

- [Se connecter à HDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Comment télécharger des données de DAG Tez à partir d’un cluster ?


#### <a name="resolution-steps"></a>Étapes de résolution

Il existe deux façons de collecter les données de DAG Tez :

- Depuis la ligne de commande :
 
    Connectez-vous au cluster HDInsight à l’aide de SSH. Exécutez ensuite la commande suivante dans l’invite de commandes :

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Utilisez la vue Tez dans Ambari :
   
  1. Accédez à Ambari. 
  2. Accédez à la vue Tez (sous l’icône de vignettes dans le coin supérieur droit). 
  3. Sélectionnez le DAG à afficher.
  4. Select **Download data** (Télécharger les données).

### <a name="additional-reading-end"></a>Documentation supplémentaire

[Se connecter à HDInsight (Hadoop) à l’aide de SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


### <a name="see-also"></a>Voir aussi
[Résoudre des problèmes à l’aide d’Azure HDInsight](hdinsight-troubleshoot-guide.md)




