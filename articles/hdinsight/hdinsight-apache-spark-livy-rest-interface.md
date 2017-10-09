---
title: aaaUse Livy Spark toosubmit travaux tooSpark cluster Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse Apache Spark REST API toosubmit Spark travaux à distance de cluster Azure HDInsight de tooan."
keywords: api rest apache spark,livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="f46ec-104">Utiliser l’API REST de Spark Apache toosubmit des travaux distants tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f46ec-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="f46ec-105">Découvrez comment toouse Livy, hello Apache Spark REST API, qui est utilisé toosubmit distant travaux de cluster Azure HDInsight Spark de tooan.</span><span class="sxs-lookup"><span data-stu-id="f46ec-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="f46ec-106">Consultez la documentation détaillée sur Livy [ici](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="f46ec-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="f46ec-107">Vous pouvez utiliser Livy toorun interactives Spark interpréteurs de commandes ou soumettre le lot toobe de travaux s’exécutent sur Spark.</span><span class="sxs-lookup"><span data-stu-id="f46ec-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="f46ec-108">Cet article traite de l’aide de traitements par lots Livy toosubmit.</span><span class="sxs-lookup"><span data-stu-id="f46ec-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="f46ec-109">extraits de code Hello dans cet article utilisent cURL toomake point de terminaison API REST appelle toohello Livy Spark.</span><span class="sxs-lookup"><span data-stu-id="f46ec-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="f46ec-110">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="f46ec-110">**Prerequisites:**</span></span>

* <span data-ttu-id="f46ec-111">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f46ec-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="f46ec-112">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f46ec-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="f46ec-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="f46ec-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="f46ec-114">Cet article utilise toodemonstrate cURL comment toomake API REST appelle par rapport à un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f46ec-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="f46ec-115">Envoyer un traitement par lots Livy Spark</span><span class="sxs-lookup"><span data-stu-id="f46ec-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="f46ec-116">Avant d’envoyer un traitement par lots, vous devez télécharger le jar d’application hello sur le stockage de cluster hello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="f46ec-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="f46ec-117">Vous pouvez utiliser [ **AzCopy**](../storage/common/storage-use-azcopy.md), un utilitaire de ligne de commande, le toodo donc.</span><span class="sxs-lookup"><span data-stu-id="f46ec-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="f46ec-118">Il existe plusieurs autres clients, vous pouvez utiliser les données tooupload.</span><span class="sxs-lookup"><span data-stu-id="f46ec-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="f46ec-119">Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="f46ec-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="f46ec-120">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="f46ec-120">**Examples**:</span></span>

* <span data-ttu-id="f46ec-121">Si le fichier jar hello est sur le stockage de cluster hello (WASB)</span><span class="sxs-lookup"><span data-stu-id="f46ec-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="f46ec-122">Si vous souhaitez toopass hello du nom de fichier jar et hello classname dans le cadre d’un fichier d’entrée (dans cet exemple, input.txt)</span><span class="sxs-lookup"><span data-stu-id="f46ec-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="f46ec-123">Obtenir des informations sur les lots Livy Spark en cours d’exécution sur le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="f46ec-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="f46ec-124">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="f46ec-124">**Examples**:</span></span>

* <span data-ttu-id="f46ec-125">Si vous souhaitez tooretrieve tous les lots de Livy Spark hello en cours d’exécution sur le cluster de hello :</span><span class="sxs-lookup"><span data-stu-id="f46ec-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="f46ec-126">Si vous voulez tooretrieve un lot spécifique avec un ID du lot donné</span><span class="sxs-lookup"><span data-stu-id="f46ec-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="f46ec-127">Supprimer un traitement par lots Livy Spark</span><span class="sxs-lookup"><span data-stu-id="f46ec-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="f46ec-128">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="f46ec-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="f46ec-129">Livy Spark et haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="f46ec-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="f46ec-130">Livy fournit une haute disponibilité pour les travaux Spark en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="f46ec-131">Voici quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="f46ec-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="f46ec-132">Si hello service de Livy tombe en panne, une fois que vous avez envoyé une tâche à distance tooa Spark de cluster, hello toorun continue de travail en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="f46ec-133">Lorsqu’il est Livy sauvegarder, il restaure état hello du travail de hello et les rapports à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f46ec-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="f46ec-134">Blocs-notes Notebook pour HDInsight sont alimentées par Livy dans hello principal.</span><span class="sxs-lookup"><span data-stu-id="f46ec-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="f46ec-135">Si un ordinateur portable est en cours d’exécution un travail Spark et hello service de Livy obtient redémarré, portable de hello continue des cellules de code hello toorun.</span><span class="sxs-lookup"><span data-stu-id="f46ec-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="f46ec-136">Afficher un exemple</span><span class="sxs-lookup"><span data-stu-id="f46ec-136">Show me an example</span></span>
<span data-ttu-id="f46ec-137">Dans cette section, nous examiner les exemples toouse Livy Spark toosubmit par lots, surveiller la progression hello du travail de hello, puis supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="f46ec-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="f46ec-138">application, nous utilisons dans cet exemple Hello est hello une développées dans l’article de hello [créer une application de Scala autonome et un toorun sur le cluster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="f46ec-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="f46ec-139">Hello étapes supposent que :</span><span class="sxs-lookup"><span data-stu-id="f46ec-139">hello steps here assume that:</span></span>

* <span data-ttu-id="f46ec-140">Vous avez déjà copié sur le compte stockage hello application jar toohello associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="f46ec-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="f46ec-141">Vous avez CuRL installé sur l’ordinateur hello où vous essayez de ces étapes.</span><span class="sxs-lookup"><span data-stu-id="f46ec-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="f46ec-142">Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f46ec-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="f46ec-143">Faites-nous d’abord vérifier que Livy Spark est en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="f46ec-144">Pour ce faire, nous pouvons obtenir une liste des lots en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f46ec-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="f46ec-145">Si vous exécutez un travail à l’aide de la Livy pour hello première fois, sortie de hello doit retourner zéro.</span><span class="sxs-lookup"><span data-stu-id="f46ec-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="f46ec-146">Vous devez obtenir un toohello similaire de sortie suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f46ec-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f46ec-147">Notez comment hello dernière ligne de sortie de hello indique **total : 0**, ce qui ne suggère aucun lot en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f46ec-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="f46ec-148">Soumettons à présent un traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="f46ec-148">Let us now submit a batch job.</span></span> <span data-ttu-id="f46ec-149">Hello suivant extrait de code utilise un nom de fichier d’entrée (input.txt) toopass hello jar et le nom de la classe hello en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="f46ec-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="f46ec-150">Si vous exécutez ces étapes à partir d’un ordinateur Windows, à l’aide d’un fichier d’entrée est hello approche recommandée.</span><span class="sxs-lookup"><span data-stu-id="f46ec-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="f46ec-151">Hello paramètres hello fichier **input.txt** sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="f46ec-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="f46ec-152">Vous devez voir un toohello similaire de sortie suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f46ec-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f46ec-153">Notez comment hello dernière ligne hello indique **état : démarrage**.</span><span class="sxs-lookup"><span data-stu-id="f46ec-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="f46ec-154">Elle indique également **id:0**.</span><span class="sxs-lookup"><span data-stu-id="f46ec-154">It also says, **id:0**.</span></span> <span data-ttu-id="f46ec-155">Ici, **0** est l’ID de lot hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="f46ec-156">Vous pouvez maintenant récupérer état hello de ce lot spécifique à l’aide des ID de lot hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="f46ec-157">Vous devez voir un toohello similaire de sortie suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f46ec-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f46ec-158">Hello sortie présente maintenant **: réussite de l’état**, ce qui suggère que le travail hello a été exécutée correctement.</span><span class="sxs-lookup"><span data-stu-id="f46ec-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="f46ec-159">Si vous le souhaitez, vous pouvez à présent supprimer les lots hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="f46ec-160">Vous devez voir un toohello similaire de sortie suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="f46ec-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="f46ec-161">Hello dernière ligne hello montre que ce lot hello a été supprimé avec succès.</span><span class="sxs-lookup"><span data-stu-id="f46ec-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="f46ec-162">Suppression d’un travail, pendant son exécution, supprime également le travail de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="f46ec-163">Si vous supprimez une tâche qui s’est terminée, avec succès ou autre, il supprime les informations sur les travaux de hello complètement.</span><span class="sxs-lookup"><span data-stu-id="f46ec-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="f46ec-164">Utilisation de Livy Spark sur des clusters HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="f46ec-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="f46ec-165">HDInsight 3.5 cluster, par défaut, désactive l’utilisation de fichiers de données de l’exemple de fichier local chemins tooaccess ou des fichiers JAR.</span><span class="sxs-lookup"><span data-stu-id="f46ec-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="f46ec-166">Nous vous encourageons toouse hello `wasb://` chemin d’accès à la place les fichiers JAR tooaccess ou des exemples de données fichiers à partir de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="f46ec-167">Si vous ne souhaitez pas que le chemin d’accès local de toouse, vous devez mettre à jour en conséquence configuration de Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="f46ec-168">toodo pour :</span><span class="sxs-lookup"><span data-stu-id="f46ec-168">toodo so:</span></span>

1. <span data-ttu-id="f46ec-169">Atteindre le portail de Ambari toohello pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="f46ec-170">Hello l’interface utilisateur de Ambari Web est disponible sur votre cluster HDInsight à https://**CLUSTERNAME**. azurehdidnsight.net, où CLUSTERNAME est nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="f46ec-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="f46ec-171">À partir de hello barre de navigation gauche, cliquez sur **Livy**, puis cliquez sur **configurations**.</span><span class="sxs-lookup"><span data-stu-id="f46ec-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="f46ec-172">Sous **par défaut livy** ajouter le nom de la propriété hello `livy.file.local-dir-whitelist` et définissez sa valeur trop**« / »** si vous souhaitez que le système de toofile tooallow un accès complet.</span><span class="sxs-lookup"><span data-stu-id="f46ec-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="f46ec-173">Si vous souhaitez que le répertoire spécifique de tooallow accès tooa uniquement, spécifiez le répertoire de toothat de chemin d’accès de hello en tant que valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="f46ec-174">Envoi de travaux Livy pour un cluster dans un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="f46ec-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="f46ec-175">Si vous vous connectez tooan cluster HDInsight Spark depuis un réseau virtuel Azure, vous pouvez connecter directement tooLivy sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="f46ec-176">Dans ce cas, hello URL de point de terminaison Livy est `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="f46ec-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="f46ec-177">Ici, **8998** port hello sur lequel Livy s’exécute sur le nœud principal du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="f46ec-178">Pour plus d’informations sur l’accès aux services sur des ports non publics, consultez [Ports utilisés par les services Hadoop sur HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="f46ec-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f46ec-179">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="f46ec-179">Troubleshooting</span></span>

<span data-ttu-id="f46ec-180">Voici quelques problèmes que vous pouvez rencontrer lors de l’utilisation de Livy pour les clusters de tooSpark de soumission de tâche à distance.</span><span class="sxs-lookup"><span data-stu-id="f46ec-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="f46ec-181">À l’aide d’un jar externe à partir de l’espace de stockage supplémentaire hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f46ec-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="f46ec-182">**Problème :** si votre travail Livy Spark fait référence à un fichier jar externe à partir du compte de stockage supplémentaire hello associé hello cluster, hello échoue.</span><span class="sxs-lookup"><span data-stu-id="f46ec-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="f46ec-183">**Résolution :** Assurez-vous que ce fichier jar de hello que vous souhaitez toouse est disponible dans le stockage par défaut hello associé au cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="f46ec-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="f46ec-184">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="f46ec-184">Next step</span></span>

* [<span data-ttu-id="f46ec-185">Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f46ec-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f46ec-186">Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f46ec-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

