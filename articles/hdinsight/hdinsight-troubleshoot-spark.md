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
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="f36d8-104">Résolution de problèmes Spark à l’aide d’Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f36d8-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="f36d8-105">En savoir plus sur les questions hello et leurs résolutions lorsque vous travaillez avec des charges utiles Apache Spark dans Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="f36d8-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="f36d8-106">Comment configurer une application Spark sur des clusters via Ambari ?</span><span class="sxs-lookup"><span data-stu-id="f36d8-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f36d8-107">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f36d8-107">Resolution steps</span></span>

<span data-ttu-id="f36d8-108">les valeurs de configuration Hello pour cette procédure a été définis auparavant dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f36d8-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="f36d8-109">toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="f36d8-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="f36d8-110">Dans la liste hello de clusters, sélectionnez **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Sélectionnez le cluster dans la liste](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="f36d8-112">Sélectionnez hello **configurations** onglet.</span><span class="sxs-lookup"><span data-stu-id="f36d8-112">Select hello **Configs** tab.</span></span>

    ![Sélectionnez l’onglet configurations de hello](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="f36d8-114">Dans la liste hello des configurations, sélectionnez **spark2 définis personnalisé par défaut**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Sélectionnez custom-spark-defaults](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="f36d8-116">Recherchez la valeur hello paramètre que vous avez besoin tooadjust, telles que **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="f36d8-117">Dans ce cas, hello valeur **4608m** est trop élevée.</span><span class="sxs-lookup"><span data-stu-id="f36d8-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Sélectionnez le champ de spark.executor.memory hello](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="f36d8-119">Ensemble hello valeur toohello recommandée.</span><span class="sxs-lookup"><span data-stu-id="f36d8-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="f36d8-120">valeur de Hello **2 048 m** est recommandée pour ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="f36d8-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Modification valeur too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="f36d8-122">Enregistrer la valeur de hello, puis enregistrez la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="f36d8-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="f36d8-123">Dans la barre d’outils de hello, sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-123">On hello toolbar, select **Save**.</span></span>

    ![Enregistrer la configuration et le paramètre de hello](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="f36d8-125">Si des configurations requièrent votre attention, un message s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f36d8-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="f36d8-126">Notez les éléments hello et sélectionnez **continuer quand même**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Sélectionnez Proceed Anyway (Continuer)](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="f36d8-128">Écrire une note sur les modifications de configuration hello et sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Entrez un commentaire concernant hello modifications](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="f36d8-130">Chaque fois qu’une configuration est enregistrée, vous êtes invité service hello de toorestart.</span><span class="sxs-lookup"><span data-stu-id="f36d8-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="f36d8-131">Sélectionnez **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-131">Select **Restart**.</span></span>

    ![Sélectionnez Redémarrer](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="f36d8-133">Confirmer le redémarrage de hello.</span><span class="sxs-lookup"><span data-stu-id="f36d8-133">Confirm hello restart.</span></span>

    ![Sélectionnez Confirm Restart All (Confirmer le redémarrage)](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="f36d8-135">Vous pouvez examiner les processus hello qui sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f36d8-135">You can review hello processes that are running.</span></span>

    ![Examinez les processus en cours d’exécution](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="f36d8-137">Vous pouvez ajouter des configurations.</span><span class="sxs-lookup"><span data-stu-id="f36d8-137">You can add configurations.</span></span> <span data-ttu-id="f36d8-138">Dans la liste hello des configurations, sélectionnez **personnalisé-spark2-defaults**, puis sélectionnez **ajouter une propriété**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Sélectionnez Ajouter une propriété](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="f36d8-140">Définissez une nouvelle propriété.</span><span class="sxs-lookup"><span data-stu-id="f36d8-140">Define a new property.</span></span> <span data-ttu-id="f36d8-141">Vous pouvez définir une propriété unique à l’aide d’une boîte de dialogue des paramètres de spécifiques comme type de données hello.</span><span class="sxs-lookup"><span data-stu-id="f36d8-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="f36d8-142">Vous pouvez également définir plusieurs propriétés en utilisant une définition par ligne.</span><span class="sxs-lookup"><span data-stu-id="f36d8-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="f36d8-143">Dans cet exemple, hello **spark.driver.memory** propriété est définie avec la valeur **4g**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Définissez une nouvelle propriété](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="f36d8-145">Enregistrer la configuration de hello et redémarrez le service de hello comme décrit dans les étapes 6 et 7.</span><span class="sxs-lookup"><span data-stu-id="f36d8-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="f36d8-146">Ces modifications sont à l’échelle du cluster, mais peuvent être remplacées lors de l’envoi de la tâche de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="f36d8-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="f36d8-147">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f36d8-147">Additional reading</span></span>

<span data-ttu-id="f36d8-148">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f36d8-148">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)</span></span>


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="f36d8-149">Comment configurer une application Spark sur des clusters via un bloc-notes Jupyter ?</span><span class="sxs-lookup"><span data-stu-id="f36d8-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f36d8-150">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f36d8-150">Resolution steps</span></span>

1. <span data-ttu-id="f36d8-151">toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="f36d8-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="f36d8-152">Dans la cellule de première hello de bloc-notes jupyter hello, après hello **%% configurer** directive, spécifier les configurations de Spark hello dans un format JSON valide.</span><span class="sxs-lookup"><span data-stu-id="f36d8-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="f36d8-153">Si nécessaire, modifiez les valeurs réelles hello :</span><span class="sxs-lookup"><span data-stu-id="f36d8-153">Change hello actual values as necessary:</span></span>

    ![Ajoutez une configuration](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="f36d8-155">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f36d8-155">Additional reading</span></span>

<span data-ttu-id="f36d8-156">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f36d8-156">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)</span></span>


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="f36d8-157">Comment configurer une application Spark sur des clusters via Livy ?</span><span class="sxs-lookup"><span data-stu-id="f36d8-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f36d8-158">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f36d8-158">Resolution steps</span></span>

1. <span data-ttu-id="f36d8-159">toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="f36d8-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="f36d8-160">Soumettre hello Spark application tooLivy à l’aide d’un client REST comme cURL.</span><span class="sxs-lookup"><span data-stu-id="f36d8-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="f36d8-161">Utilisez un commande qui suit toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="f36d8-161">Use a command similar toohello following.</span></span> <span data-ttu-id="f36d8-162">Si nécessaire, modifiez les valeurs réelles hello :</span><span class="sxs-lookup"><span data-stu-id="f36d8-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="f36d8-163">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f36d8-163">Additional reading</span></span>

<span data-ttu-id="f36d8-164">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f36d8-164">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)</span></span>


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="f36d8-165">Comment configurer une application Spark sur des clusters via spark-submit ?</span><span class="sxs-lookup"><span data-stu-id="f36d8-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="f36d8-166">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f36d8-166">Resolution steps</span></span>

1. <span data-ttu-id="f36d8-167">toodetermine quelles configurations Spark nécessitent des valeurs du jeu et toowhat de toobe, consultez [ce qui provoque un Spark exception d’application OutofMemoryError](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="f36d8-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="f36d8-168">Lancez spark-shell à l’aide d’un commande qui suit toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="f36d8-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="f36d8-169">Modifier la valeur réelle de hello des configurations de hello selon les besoins :</span><span class="sxs-lookup"><span data-stu-id="f36d8-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="f36d8-170">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f36d8-170">Additional reading</span></span>

<span data-ttu-id="f36d8-171">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/) (Envoi de travaux Spark sur des clusters HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f36d8-171">[Spark job submission on HDInsight clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)</span></span>


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="f36d8-172">À quoi est dû l’échec d’une application Spark avec l’exception OutOfMemoryError ?</span><span class="sxs-lookup"><span data-stu-id="f36d8-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="f36d8-173">Description détaillée</span><span class="sxs-lookup"><span data-stu-id="f36d8-173">Detailed description</span></span>

<span data-ttu-id="f36d8-174">Hello application de Spark échoue, avec hello les types d’exceptions non interceptées suivants :</span><span class="sxs-lookup"><span data-stu-id="f36d8-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

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

### <a name="probable-cause"></a><span data-ttu-id="f36d8-175">Cause probable</span><span class="sxs-lookup"><span data-stu-id="f36d8-175">Probable cause</span></span>

<span data-ttu-id="f36d8-176">cause la plus probable de cette exception Hello est que pas assez de mémoire du tas est allouée virtuels toohello Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="f36d8-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="f36d8-177">Ces JVM est lancées en tant que les exécuteurs ou les pilotes dans le cadre de hello application de Spark.</span><span class="sxs-lookup"><span data-stu-id="f36d8-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="f36d8-178">Étapes de résolution</span><span class="sxs-lookup"><span data-stu-id="f36d8-178">Resolution steps</span></span>

1. <span data-ttu-id="f36d8-179">Déterminer la taille maximale de hello de hello données hello Spark application gère.</span><span class="sxs-lookup"><span data-stu-id="f36d8-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="f36d8-180">Vous pouvez faire une estimation basée sur la taille maximale des données d’entrée hello, données hello intermédiaire qui sont générées par la transformation de données d’entrée de hello et les données de sortie hello qui se produites quand l’application hello plus consiste à transformer les données intermédiaires hello hello.</span><span class="sxs-lookup"><span data-stu-id="f36d8-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="f36d8-181">Ce processus peut être réitéré si vous ne parvenez pas à effectuer une estimation formelle initiale.</span><span class="sxs-lookup"><span data-stu-id="f36d8-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="f36d8-182">Assurez-vous que le cluster HDInsight hello que vous allez toouse a suffisamment de ressources en termes de mémoire et cœurs tooaccommodate hello Spark l’application.</span><span class="sxs-lookup"><span data-stu-id="f36d8-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="f36d8-183">Vous pouvez y parvenir en consultant la section de métriques de cluster hello Hello fils UI pour les valeurs hello de **mémoire utilisée** Visual Studio. **Mémoire totale**, et les valeurs **VCores utilisés** et **Total des VCores**.</span><span class="sxs-lookup"><span data-stu-id="f36d8-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="f36d8-184">Une valeur hello suivant Spark configurations tooappropriate, qui ne doit pas dépasser 90 % de la mémoire disponible de hello et les cœurs.</span><span class="sxs-lookup"><span data-stu-id="f36d8-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="f36d8-185">les valeurs Hello doivent être dans des besoins en mémoire hello de hello application de Spark :</span><span class="sxs-lookup"><span data-stu-id="f36d8-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="f36d8-186">tooget hello mémoire totale utilisée par tous les exécuteurs, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f36d8-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="f36d8-187">tooget hello mémoire totale utilisée par le pilote hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f36d8-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="f36d8-188">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="f36d8-188">Additional reading</span></span>

- <span data-ttu-id="f36d8-189">[Spark memory management overview](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview) (Vue d’ensemble de la gestion de la mémoire dans Spark)</span><span class="sxs-lookup"><span data-stu-id="f36d8-189">[Spark memory management overview](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)</span></span>
- <span data-ttu-id="f36d8-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/) (Déboguer une application Spark sur un cluster HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f36d8-190">[Debug a Spark application on an HDInsight cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)</span></span>

