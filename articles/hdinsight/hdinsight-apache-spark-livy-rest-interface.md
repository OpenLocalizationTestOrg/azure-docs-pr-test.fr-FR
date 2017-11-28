---
title: "Utiliser Livy Spark pour envoyer des travaux à un cluster Spark sur Azure HDInsight | Documents Microsoft"
description: "Découvrez comment utiliser l’API REST Apache Spark pour envoyer des travaux Spark à distance à un cluster Azure HDInsight."
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
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="1877e-104">Utiliser l’API REST Spark Apache pour envoyer des travaux à distance à un cluster Spark HDInsight</span><span class="sxs-lookup"><span data-stu-id="1877e-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="1877e-105">Découvrez comment utiliser Livy, API REST Apache Spark servant à envoyer des travaux à distance à un cluster Spark HDInsight Azure.</span><span class="sxs-lookup"><span data-stu-id="1877e-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="1877e-106">Consultez la documentation détaillée sur Livy [ici](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="1877e-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="1877e-107">Vous pouvez utiliser Livy pour exécuter des interpréteurs de commandes Spark interactifs ou soumettre des traitements par lots à exécuter sur Spark.</span><span class="sxs-lookup"><span data-stu-id="1877e-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="1877e-108">Cet article traite de l’utilisation de Livy pour soumettre des traitements par lots.</span><span class="sxs-lookup"><span data-stu-id="1877e-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="1877e-109">Les extraits de code dans cet article utilisent cURL pour effectuer des appels d’API REST au point de terminaison Livy Spark.</span><span class="sxs-lookup"><span data-stu-id="1877e-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="1877e-110">**Configuration requise :**</span><span class="sxs-lookup"><span data-stu-id="1877e-110">**Prerequisites:**</span></span>

* <span data-ttu-id="1877e-111">Un cluster Apache Spark sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1877e-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="1877e-112">Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="1877e-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="1877e-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="1877e-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="1877e-114">Cet article utilise cURL pour montrer comment effectuer des appels d’API REST sur un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="1877e-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="1877e-115">Envoyer un traitement par lots Livy Spark</span><span class="sxs-lookup"><span data-stu-id="1877e-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="1877e-116">Avant de soumettre un traitement par lots, vous devez télécharger le fichier .jar d’application sur le stockage associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="1877e-117">Pour ce faire, vous pouvez utiliser l’utilitaire en ligne de commande [**AzCopy**](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="1877e-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="1877e-118">D’autres clients permettent également de charger des données.</span><span class="sxs-lookup"><span data-stu-id="1877e-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="1877e-119">Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1877e-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="1877e-120">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="1877e-120">**Examples**:</span></span>

* <span data-ttu-id="1877e-121">Si le fichier .jar se trouve sur le stockage de cluster (WASB)</span><span class="sxs-lookup"><span data-stu-id="1877e-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="1877e-122">Si vous souhaitez transmettre le nom de fichier .jar et le nom de classe dans un fichier d’entrée (dans cet exemple, input.txt)</span><span class="sxs-lookup"><span data-stu-id="1877e-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="1877e-123">Obtenir des informations sur des lots Livy Spark en cours d’exécution sur le cluster</span><span class="sxs-lookup"><span data-stu-id="1877e-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="1877e-124">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="1877e-124">**Examples**:</span></span>

* <span data-ttu-id="1877e-125">Si vous souhaitez récupérer tous les lots Livy Spark en cours d’exécution sur le cluster :</span><span class="sxs-lookup"><span data-stu-id="1877e-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="1877e-126">Si vous souhaitez récupérer un lot spécifique avec un ID de lot donné</span><span class="sxs-lookup"><span data-stu-id="1877e-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="1877e-127">Supprimer un traitement par lots Livy Spark</span><span class="sxs-lookup"><span data-stu-id="1877e-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="1877e-128">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="1877e-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="1877e-129">Livy Spark et haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1877e-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="1877e-130">Livy assure une haute disponibilité des travaux Spark exécutés sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="1877e-131">Voici quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="1877e-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="1877e-132">Si le service Livy tombe en panne après avoir soumis un travail à distance à un cluster Spark, l’exécution du travail se poursuit en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="1877e-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="1877e-133">La sauvegarde de Livy entraîne la restauration de l’état du travail et la création d’un rapport à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="1877e-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="1877e-134">Les blocs-notes Jupyter pour HDInsight sont alimentés par Livy sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="1877e-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="1877e-135">Si un bloc-notes exécute un travail Spark et que le service Livy est redémarré, le bloc-notes poursuit l’exécution des cellules de code.</span><span class="sxs-lookup"><span data-stu-id="1877e-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="1877e-136">Afficher un exemple</span><span class="sxs-lookup"><span data-stu-id="1877e-136">Show me an example</span></span>
<span data-ttu-id="1877e-137">Dans cette section, nous examinons des exemples d’utilisation de Livy Spark pour envoyer un traitement par lots, surveiller l’avancement du travail, puis supprimer celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1877e-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="1877e-138">L’application que nous utilisons dans cet exemple est décrite dans l’article [Créer une application Scala autonome et l’exécuter sur un cluster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="1877e-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="1877e-139">Les étapes indiquées ici supposent que les conditions suivantes sont réunies :</span><span class="sxs-lookup"><span data-stu-id="1877e-139">The steps here assume that:</span></span>

* <span data-ttu-id="1877e-140">Vous avez déjà copié le fichier .jar de l’application dans le compte de stockage associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="1877e-141">CuRL est installé sur l’ordinateur sur lequel vous effectuez la procédure.</span><span class="sxs-lookup"><span data-stu-id="1877e-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="1877e-142">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1877e-142">Perform the following steps:</span></span>

1. <span data-ttu-id="1877e-143">Vérifions tout d’abord que Livy Spark est en cours d’exécution sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="1877e-144">Pour ce faire, nous pouvons obtenir une liste des lots en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1877e-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="1877e-145">Si vous exécutez un travail à l’aide de Livy pour la première fois, la valeur retournée doit être 0.</span><span class="sxs-lookup"><span data-stu-id="1877e-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="1877e-146">La sortie doit ressembler à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1877e-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="1877e-147">Notez la dernière ligne qui indique **total:0**, ce qui suggère qu’aucun lot n’est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1877e-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="1877e-148">Soumettons à présent un traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="1877e-148">Let us now submit a batch job.</span></span> <span data-ttu-id="1877e-149">L’extrait de code suivant utilise un fichier d’entrée (input.txt) pour transmettre le nom du fichier .jar et le nom de classe en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="1877e-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="1877e-150">Si vous exécutez ces étapes sur un ordinateur Windows, utiliser un fichier d’entrée est l’approche recommandée.</span><span class="sxs-lookup"><span data-stu-id="1877e-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="1877e-151">Les paramètres du fichier **input.txt** sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="1877e-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="1877e-152">Le résultat doit ressembler à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1877e-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="1877e-153">Notez la dernière ligne de la sortie qui indique **state:starting**.</span><span class="sxs-lookup"><span data-stu-id="1877e-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="1877e-154">Elle indique également **id:0**.</span><span class="sxs-lookup"><span data-stu-id="1877e-154">It also says, **id:0**.</span></span> <span data-ttu-id="1877e-155">Ici, **0** correspond à l’ID du lot.</span><span class="sxs-lookup"><span data-stu-id="1877e-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="1877e-156">Vous pouvez maintenant récupérer l’état de ce lot à l’aide de l’ID correspondant.</span><span class="sxs-lookup"><span data-stu-id="1877e-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="1877e-157">Le résultat doit ressembler à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1877e-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="1877e-158">La sortie indique maintenant **state:success**, ce qui suggère que le travail a été exécuté correctement.</span><span class="sxs-lookup"><span data-stu-id="1877e-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="1877e-159">Si vous le souhaitez, vous pouvez maintenant supprimer le lot.</span><span class="sxs-lookup"><span data-stu-id="1877e-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="1877e-160">Le résultat doit ressembler à l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="1877e-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="1877e-161">La dernière ligne de la sortie indique que le lot a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="1877e-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="1877e-162">Supprimer un travail, alors qu’il est en cours d’exécution, tue également le travail.</span><span class="sxs-lookup"><span data-stu-id="1877e-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="1877e-163">Si vous supprimez un travail qui s’est terminé, les informations du travail sont entièrement supprimées.</span><span class="sxs-lookup"><span data-stu-id="1877e-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="1877e-164">Utilisation de Livy Spark sur des clusters HDInsight 3.5</span><span class="sxs-lookup"><span data-stu-id="1877e-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="1877e-165">Par défaut, un cluster HDInsight 3.5, désactive l’utilisation de chemins locaux pour accéder à des fichiers de données ou des fichiers JAR.</span><span class="sxs-lookup"><span data-stu-id="1877e-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="1877e-166">Nous vous conseillons plutôt d'utiliser le chemin `wasb://` pour accéder aux fichiers JAR ou aux exemples de fichiers de données à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="1877e-167">Si vous ne souhaitez pas utiliser le chemin d’accès local, vous devez mettre à jour la configuration Ambari en conséquence.</span><span class="sxs-lookup"><span data-stu-id="1877e-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="1877e-168">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="1877e-168">To do so:</span></span>

1. <span data-ttu-id="1877e-169">Accédez au portail Ambari pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="1877e-170">L’interface utilisateur Web d’Ambari est disponible sur votre cluster HDInsight à l’adresse https://**CLUSTERNAME**.azurehdidnsight.net, où CLUSTERNAME correspond au nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="1877e-171">Dans le volet de navigation gauche, cliquez sur **Livy**, puis sur **Configurations**.</span><span class="sxs-lookup"><span data-stu-id="1877e-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="1877e-172">Sous **livy-default**, ajoutez le nom de la propriété `livy.file.local-dir-whitelist` et définissez sa valeur sur **"/"** si vous souhaitez autoriser un accès complet au système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1877e-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="1877e-173">Si vous souhaitez autoriser uniquement l’accès à un répertoire spécifique, indiquez comme valeur le chemin d’accès à ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="1877e-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="1877e-174">Envoi de travaux Livy pour un cluster dans un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="1877e-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="1877e-175">Si vous vous connectez à un cluster HDInsight Spark à partir d’un réseau virtuel Azure, vous pouvez vous connecter directement à Livy sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="1877e-176">Dans ce cas, l’URL du point de terminaison Livy est `http://<IP address of the headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="1877e-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="1877e-177">Ici, **8998** est le port sur lequel Livy s’exécute sur le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="1877e-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="1877e-178">Pour plus d’informations sur l’accès aux services sur des ports non publics, consultez [Ports utilisés par les services Hadoop sur HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="1877e-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1877e-179">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1877e-179">Troubleshooting</span></span>

<span data-ttu-id="1877e-180">Voici quelques problèmes que vous pouvez rencontrer lors de l’utilisation de Livy pour la soumission des travaux à distance à des clusters Spark.</span><span class="sxs-lookup"><span data-stu-id="1877e-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="1877e-181">L’utilisation d’un fichier JAR externe à partir du stockage supplémentaire n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="1877e-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="1877e-182">**Problème :** Si votre travail Livy Spark référence un fichier jar externe à partir du compte de stockage supplémentaire associé au cluster, le travail échoue.</span><span class="sxs-lookup"><span data-stu-id="1877e-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="1877e-183">**Résolution :** vérifiez que le fichier JAR que vous voulez utiliser est présent dans le stockage par défaut associé au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1877e-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="1877e-184">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1877e-184">Next step</span></span>

* [<span data-ttu-id="1877e-185">Gérer les ressources du cluster Apache Spark dans Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1877e-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="1877e-186">Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="1877e-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

