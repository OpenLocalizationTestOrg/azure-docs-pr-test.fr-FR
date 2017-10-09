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
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Utiliser l’API REST de Spark Apache toosubmit des travaux distants tooan cluster HDInsight Spark

Découvrez comment toouse Livy, hello Apache Spark REST API, qui est utilisé toosubmit distant travaux de cluster Azure HDInsight Spark de tooan. Consultez la documentation détaillée sur Livy [ici](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

Vous pouvez utiliser Livy toorun interactives Spark interpréteurs de commandes ou soumettre le lot toobe de travaux s’exécutent sur Spark. Cet article traite de l’aide de traitements par lots Livy toosubmit. extraits de code Hello dans cet article utilisent cURL toomake point de terminaison API REST appelle toohello Livy Spark.

**Configuration requise :**

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). Cet article utilise toodemonstrate cURL comment toomake API REST appelle par rapport à un cluster HDInsight Spark.

## <a name="submit-a-livy-spark-batch-job"></a>Envoyer un traitement par lots Livy Spark
Avant d’envoyer un traitement par lots, vous devez télécharger le jar d’application hello sur le stockage de cluster hello associé hello cluster. Vous pouvez utiliser [ **AzCopy**](../storage/common/storage-use-azcopy.md), un utilitaire de ligne de commande, le toodo donc. Il existe plusieurs autres clients, vous pouvez utiliser les données tooupload. Pour en savoir plus à leur sujet, consultez [Téléchargement de données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Exemples :**

* Si le fichier jar hello est sur le stockage de cluster hello (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Si vous souhaitez toopass hello du nom de fichier jar et hello classname dans le cadre d’un fichier d’entrée (dans cet exemple, input.txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Obtenir des informations sur les lots Livy Spark en cours d’exécution sur le cluster de hello
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Exemples :**

* Si vous souhaitez tooretrieve tous les lots de Livy Spark hello en cours d’exécution sur le cluster de hello :
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Si vous voulez tooretrieve un lot spécifique avec un ID du lot donné
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Supprimer un traitement par lots Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Exemple**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark et haute disponibilité
Livy fournit une haute disponibilité pour les travaux Spark en cours d’exécution sur le cluster de hello. Voici quelques exemples.

* Si hello service de Livy tombe en panne, une fois que vous avez envoyé une tâche à distance tooa Spark de cluster, hello toorun continue de travail en arrière-plan de hello. Lorsqu’il est Livy sauvegarder, il restaure état hello du travail de hello et les rapports à nouveau.
* Blocs-notes Notebook pour HDInsight sont alimentées par Livy dans hello principal. Si un ordinateur portable est en cours d’exécution un travail Spark et hello service de Livy obtient redémarré, portable de hello continue des cellules de code hello toorun. 

## <a name="show-me-an-example"></a>Afficher un exemple
Dans cette section, nous examiner les exemples toouse Livy Spark toosubmit par lots, surveiller la progression hello du travail de hello, puis supprimez-le. application, nous utilisons dans cet exemple Hello est hello une développées dans l’article de hello [créer une application de Scala autonome et un toorun sur le cluster HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md). Hello étapes supposent que :

* Vous avez déjà copié sur le compte stockage hello application jar toohello associé hello cluster.
* Vous avez CuRL installé sur l’ordinateur hello où vous essayez de ces étapes.

Effectuez hello comme suit :

1. Faites-nous d’abord vérifier que Livy Spark est en cours d’exécution sur le cluster de hello. Pour ce faire, nous pouvons obtenir une liste des lots en cours d’exécution. Si vous exécutez un travail à l’aide de la Livy pour hello première fois, sortie de hello doit retourner zéro.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Vous devez obtenir un toohello similaire de sortie suivant extrait de code :
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Notez comment hello dernière ligne de sortie de hello indique **total : 0**, ce qui ne suggère aucun lot en cours d’exécution.

2. Soumettons à présent un traitement par lots. Hello suivant extrait de code utilise un nom de fichier d’entrée (input.txt) toopass hello jar et le nom de la classe hello en tant que paramètres. Si vous exécutez ces étapes à partir d’un ordinateur Windows, à l’aide d’un fichier d’entrée est hello approche recommandée.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Hello paramètres hello fichier **input.txt** sont définies comme suit :
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Vous devez voir un toohello similaire de sortie suivant extrait de code :
   
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
   
    Notez comment hello dernière ligne hello indique **état : démarrage**. Elle indique également **id:0**. Ici, **0** est l’ID de lot hello.

3. Vous pouvez maintenant récupérer état hello de ce lot spécifique à l’aide des ID de lot hello.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Vous devez voir un toohello similaire de sortie suivant extrait de code :
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello sortie présente maintenant **: réussite de l’état**, ce qui suggère que le travail hello a été exécutée correctement.

4. Si vous le souhaitez, vous pouvez à présent supprimer les lots hello.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Vous devez voir un toohello similaire de sortie suivant extrait de code :
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello dernière ligne hello montre que ce lot hello a été supprimé avec succès. Suppression d’un travail, pendant son exécution, supprime également le travail de hello. Si vous supprimez une tâche qui s’est terminée, avec succès ou autre, il supprime les informations sur les travaux de hello complètement.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Utilisation de Livy Spark sur des clusters HDInsight 3.5

HDInsight 3.5 cluster, par défaut, désactive l’utilisation de fichiers de données de l’exemple de fichier local chemins tooaccess ou des fichiers JAR. Nous vous encourageons toouse hello `wasb://` chemin d’accès à la place les fichiers JAR tooaccess ou des exemples de données fichiers à partir de cluster de hello. Si vous ne souhaitez pas que le chemin d’accès local de toouse, vous devez mettre à jour en conséquence configuration de Ambari hello. toodo pour :

1. Atteindre le portail de Ambari toohello pour le cluster de hello. Hello l’interface utilisateur de Ambari Web est disponible sur votre cluster HDInsight à https://**CLUSTERNAME**. azurehdidnsight.net, où CLUSTERNAME est nom hello de votre cluster.

2. À partir de hello barre de navigation gauche, cliquez sur **Livy**, puis cliquez sur **configurations**.

3. Sous **par défaut livy** ajouter le nom de la propriété hello `livy.file.local-dir-whitelist` et définissez sa valeur trop**« / »** si vous souhaitez que le système de toofile tooallow un accès complet. Si vous souhaitez que le répertoire spécifique de tooallow accès tooa uniquement, spécifiez le répertoire de toothat de chemin d’accès de hello en tant que valeur de hello.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Envoi de travaux Livy pour un cluster dans un réseau virtuel Azure

Si vous vous connectez tooan cluster HDInsight Spark depuis un réseau virtuel Azure, vous pouvez connecter directement tooLivy sur le cluster de hello. Dans ce cas, hello URL de point de terminaison Livy est `http://<IP address of hello headnode>:8998/batches`. Ici, **8998** port hello sur lequel Livy s’exécute sur le nœud principal du cluster hello. Pour plus d’informations sur l’accès aux services sur des ports non publics, consultez [Ports utilisés par les services Hadoop sur HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Résolution des problèmes

Voici quelques problèmes que vous pouvez rencontrer lors de l’utilisation de Livy pour les clusters de tooSpark de soumission de tâche à distance.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>À l’aide d’un jar externe à partir de l’espace de stockage supplémentaire hello n’est pas pris en charge.

**Problème :** si votre travail Livy Spark fait référence à un fichier jar externe à partir du compte de stockage supplémentaire hello associé hello cluster, hello échoue.

**Résolution :** Assurez-vous que ce fichier jar de hello que vous souhaitez toouse est disponible dans le stockage par défaut hello associé au cluster HDInsight de hello.





## <a name="next-step"></a>Étape suivante

* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

