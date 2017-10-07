---
title: "aaaTroubleshoot Spark à l’aide d’Azure HDInsight | Documents Microsoft"
description: "Obtenez des réponses toocommon des questions sur l’utilisation d’Apache Spark et Azure HDInsight."
keywords: "Azure HDInsight, Spark, FAQ, guide de résolution des problèmes, problèmes courants, configuration d’application, Ambari"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Résolution de problèmes Spark à l’aide d’Azure HDInsight

En savoir plus sur les questions hello et leurs résolutions lorsque vous travaillez avec des charges utiles Apache Spark dans Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Comment configurer une application Spark sur des clusters via Ambari ?

### <a name="resolution-steps"></a>Étapes de résolution

les valeurs de configuration Hello pour cette procédure a été définis auparavant dans HDInsight. toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. Dans la liste hello de clusters, sélectionnez **Spark2**.

    ![Sélectionnez le cluster dans la liste](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Sélectionnez hello **configurations** onglet.

    ![Sélectionnez l’onglet configurations de hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. Dans la liste hello des configurations, sélectionnez **spark2 définis personnalisé par défaut**.

    ![Sélectionnez custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Recherchez la valeur hello paramètre que vous avez besoin tooadjust, telles que **spark.executor.memory**. Dans ce cas, hello valeur **4608m** est trop élevée.

    ![Sélectionnez le champ de spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Ensemble hello valeur toohello recommandée. valeur de Hello **2 048 m** est recommandée pour ce paramètre.

    ![Modification valeur too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Enregistrer la valeur de hello, puis enregistrez la configuration de hello. Dans la barre d’outils de hello, sélectionnez **enregistrer**.

    ![Enregistrer la configuration et le paramètre de hello](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    Si des configurations requièrent votre attention, un message s’affiche. Notez les éléments hello et sélectionnez **continuer quand même**. 

    ![Sélectionnez Proceed Anyway (Continuer)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Écrire une note sur les modifications de configuration hello et sélectionnez **enregistrer**.

    ![Entrez un commentaire concernant hello modifications](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Chaque fois qu’une configuration est enregistrée, vous êtes invité service hello de toorestart. Sélectionnez **Redémarrer**.

    ![Sélectionnez Redémarrer](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Confirmer le redémarrage de hello.

    ![Sélectionnez Confirm Restart All (Confirmer le redémarrage)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Vous pouvez examiner les processus hello qui sont en cours d’exécution.

    ![Examinez les processus en cours d’exécution](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. Vous pouvez ajouter des configurations. Dans la liste hello des configurations, sélectionnez **personnalisé-spark2-defaults**, puis sélectionnez **ajouter une propriété**.

    ![Sélectionnez Ajouter une propriété](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Définissez une nouvelle propriété. Vous pouvez définir une propriété unique à l’aide d’une boîte de dialogue des paramètres de spécifiques comme type de données hello. Vous pouvez également définir plusieurs propriétés en utilisant une définition par ligne. 

    Dans cet exemple, hello **spark.driver.memory** propriété est définie avec la valeur **4g**.

    ![Définissez une nouvelle propriété](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Enregistrer la configuration de hello et redémarrez le service de hello comme décrit dans les étapes 6 et 7.

Ces modifications sont à l’échelle du cluster, mais peuvent être remplacées lors de l’envoi de la tâche de Spark hello.

### <a name="additional-reading"></a>Documentation supplémentaire

[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Comment configurer une application Spark sur des clusters via un bloc-notes Jupyter ?

### <a name="resolution-steps"></a>Étapes de résolution

1. toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Dans la cellule de première hello de bloc-notes jupyter hello, après hello **%% configurer** directive, spécifier les configurations de Spark hello dans un format JSON valide. Si nécessaire, modifiez les valeurs réelles hello :

    ![Ajoutez une configuration](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Documentation supplémentaire

[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Comment configurer une application Spark sur des clusters via Livy ?

### <a name="resolution-steps"></a>Étapes de résolution

1. toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Soumettre hello Spark application tooLivy à l’aide d’un client REST comme cURL. Utilisez un commande qui suit toohello similaire. Si nécessaire, modifiez les valeurs réelles hello :

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Documentation supplémentaire

[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Comment configurer une application Spark sur des clusters via spark-submit ?

### <a name="resolution-steps"></a>Étapes de résolution

1. toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Lancez spark-shell à l’aide d’un commande qui suit toohello similaire. Modifier la valeur réelle de hello des configurations de hello selon les besoins : 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Documentation supplémentaire

[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>À quoi est dû l’échec d’une application Spark avec l’exception OutOfMemoryError ?

### <a name="detailed-description"></a>Description détaillée

Hello application de Spark échoue, avec hello les types d’exceptions non interceptées suivants :

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>Cause probable

cause la plus probable de cette exception Hello est que pas assez de mémoire du tas est allouée virtuels toohello Java (JVM). Ces JVM est lancées en tant que les exécuteurs ou les pilotes dans le cadre de hello application de Spark. 

### <a name="resolution-steps"></a>Étapes de résolution

1. Déterminer la taille maximale de hello de hello données hello Spark application gère. Vous pouvez faire une estimation basée sur la taille maximale des données d’entrée hello, données hello intermédiaire qui sont générées par la transformation de données d’entrée de hello et les données de sortie hello qui se produites quand l’application hello plus consiste à transformer les données intermédiaires hello hello. Ce processus peut être réitéré si vous ne parvenez pas à effectuer une estimation formelle initiale. 

2. Assurez-vous que le cluster HDInsight hello que vous allez toouse a suffisamment de ressources en termes de mémoire et cœurs tooaccommodate hello Spark l’application. Vous pouvez y parvenir en consultant la section de métriques de cluster hello Hello fils UI pour les valeurs hello de **mémoire utilisée** Visual Studio. **Mémoire totale**, et les valeurs **VCores utilisés** et **Total des VCores**.

3. Une valeur hello suivant Spark configurations tooappropriate, qui ne doit pas dépasser 90 % de la mémoire disponible de hello et les cœurs. les valeurs Hello doivent être dans des besoins en mémoire hello de hello application de Spark : 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget hello mémoire totale utilisée par tous les exécuteurs, exécutez hello de commande suivante : 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget hello mémoire totale utilisée par le pilote hello, exécutez hello de commande suivante :
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Documentation supplémentaire

- [Spark memory management overview](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview) (Vue d’ensemble de la gestion de la mémoire dans Spark)
- [Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Déboguer une application Spark sur un cluster HDInsight)

