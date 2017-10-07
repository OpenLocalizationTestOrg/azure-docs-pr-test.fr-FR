---
title: "journaux d’Application Insight aaaAnalyze avec Spark - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment tooexport Application Insight consigne tooblob stockage et ensuite d’analyser les journaux hello avec Spark sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Analyser les journaux de télémétrie Application Insights avec Spark sur HDInsight

Découvrez comment toouse nouvelles sur HDInsight tooanalyze les données de télémétrie Application Insight.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) est un service d’analyse qui surveille vos applications web. Les données de télémétrie générées par Application Insights peuvent être exporté tooAzure de stockage. Une fois les données de salutation dans le stockage Azure, HDInsight peut être utilisé tooanalyze il.

## <a name="prerequisites"></a>Composants requis

* Une application qui est configuré toouse Application Insights.

* Maîtrise de la création d’un cluster HDInsight sous Linux. Pour plus d’informations, consultez la rubrique [Création de Spark sur HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un navigateur Web.

Hello ressources suivantes ont été utilisés dans le développement et le test de ce document :

* Données de télémétrie application Insights a été générées à l’aide un [application web Node.js configuré toouse Application Insights](../application-insights/app-insights-nodejs.md).

* Un Spark basés sur Linux sur la version 3.5 du cluster HDInsight a été utilisé tooanalyze hello données.

## <a name="architecture-and-planning"></a>Architecture et planification

Hello suivant le diagramme illustre l’architecture du service de cet exemple hello :

![diagramme montrant les données circulent à partir du stockage de tooblob Application Insights, puis traitées par Spark sur HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Stockage Azure

Application Insights peuvent être configuré toocontinuously exportation télémétrie informations tooblobs. HDInsight peut ensuite lire les données stockées dans des objets BLOB de hello. Toutefois, il existe certaines conditions que vous devez remplir :

* **Emplacement**: si hello compte de stockage et HDInsight se trouvent dans différents emplacements, il peut augmenter la latence. Elle augmente également coût, comme les frais de sortie sont appliqué toodata déplacement entre les régions.

    > [!WARNING]
    > L’utilisation d’un compte de stockage dans un emplacement autre que HDInsight n’est pas prise en charge.

* **Type d’objet blob** : HDInsight prend uniquement en charge les objets blob de blocs. Par défaut, application Insights toousing objets BLOB de blocs, donc doit fonctionner par défaut avec HDInsight.

Pour plus d’informations sur l’ajout de tooan de stockage supplémentaire existante du cluster HDInsight, consultez hello [ajouter des comptes de stockage supplémentaires](hdinsight-hadoop-add-storage.md) document.

### <a name="data-schema"></a>Schéma de données

Application Insights fournit [exporter le modèle de données](../application-insights/app-insights-export-data-model.md) les informations de format de données de télémétrie hello exportées tooblobs. étapes Hello dans ce document utilisent Spark SQL toowork avec les données de salutation. Spark SQL peut générer automatiquement un schéma pour la structure de données JSON hello enregistré par l’Application Insights.

## <a name="export-telemetry-data"></a>Exporter les données de télémétrie

Suivez les étapes de hello dans [configurer l’exportation continue](../application-insights/app-insights-export-telemetry.md) tooconfigure votre tooan informations de télémétrie Application Insights tooexport stockage Azure d’objets blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Configurer les données de salutation tooaccess HDInsight

Si vous créez un cluster HDInsight, ajoutez le compte de stockage hello lors de la création du cluster.

tooadd hello cluster existant tooan de compte de stockage Azure, utilisez les informations de hello Bonjour [ajouter des comptes de stockage supplémentaires](hdinsight-hadoop-add-storage.md) document.

## <a name="analyze-hello-data-pyspark"></a>Analyser les données de salutation : PySpark

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre Spark sur le cluster HDInsight. À partir de hello **liens rapides** section, sélectionnez **tableaux de bord de Cluster**, puis sélectionnez **bloc-notes Jupyter** à partir du Panneau de Cluster Dashboard__ hello.

    ![tableaux de bord de cluster Hello](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. Dans hello coin supérieur droit de la page de Notebook hello, sélectionnez **nouveau**, puis **PySpark**. Un nouvel onglet de navigateur s’ouvre, contenant un notebook Jupyter basé sur Python.

3. Dans le premier champ de hello (appelé un **cellule**) sur la page de hello, entrez hello suivant du texte :

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Ce code configure Spark toorecursively accès hello structure de répertoire pour les données d’entrée hello. Télémétrie application Insights est connecté tooa directory structure similaire toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Utilisez **MAJ + ENTRÉE** code hello de toorun. Sur hello à gauche de la cellule de hello, un «\*» s’affiche entre hello crochets tooindicate que code hello dans cette cellule est en cours d’exécution. Une fois qu’il se termine, hello '\*' modifie tooa nombre et la sortie similaire toohello suit texte s’affiche sous la cellule de hello :

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Une nouvelle cellule est créée sous hello tout d’abord un. Entrez hello après le texte dans la nouvelle cellule de hello. Remplacez `CONTAINER` et `STORAGEACCOUNT` avec le nom de compte de stockage Windows Azure hello et le nom de conteneur qui contient les données d’Application Insights.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Utilisez **MAJ + ENTRÉE** tooexecute cette cellule. Vous voyez un toohello similaire de résultat suivant de texte :

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    chemin d’accès de wasb Hello retourné est un emplacement hello Hello les données de télémétrie Application Insights. Hello de modification `hdfs dfs -ls` hello cellule toouse hello wasb chemin d’accès retourné de ligne, puis utilisez **MAJ + ENTRÉE** cellule de hello toorun à nouveau. Ce temps, les résultats hello doivent afficher les répertoires hello qui contiennent des données de télémétrie.

   > [!NOTE]
   > Les étapes de cette section reste hello Hello, hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` active a été utilisée. Votre structure de répertoires peut être différente.

6. Dans la cellule suivante de hello, entrez hello suivant code : Remplacez `WASB_PATH` avec chemin d’accès de hello à partir de l’étape précédente de hello.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Ce code crée une trame de données à partir des fichiers JSON hello exportées par le processus d’exportation continue hello. Utilisez **MAJ + ENTRÉE** toorun cette cellule.
7. Dans la cellule suivante de hello, entrez et exécutez hello suivant schéma hello tooview Spark créé pour les fichiers JSON hello :

   ```python
   jsonData.printSchema()
   ```

    schéma Hello pour chaque type de données de télémétrie est différent. exemple Hello est hello de schéma est généré pour les demandes web (les données stockées dans hello `Requests` sous-répertoire) :

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Utilisez hello suivant tooregister hello trame de données comme une table temporaire et exécuter une requête sur les données de salutation :

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Cette requête retourne des informations de ville hello pour les premiers enregistrements de 20 hello où context.location.city n’est pas null.

   > [!NOTE]
   > structure de contexte Hello est présente dans toutes les données de télémétrie enregistrées par l’Application Insights. élément de ville Hello ne peut-être pas être rempli dans vos journaux. Utilisez hello schéma tooidentify autres éléments que vous pouvez interroger peuvent contenir des données de vos journaux.

    Cette requête retourne toohello similaire à informations suivant le texte :

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Analyser les données de salutation : Scala

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre Spark sur le cluster HDInsight. À partir de hello **liens rapides** section, sélectionnez **tableaux de bord de Cluster**, puis sélectionnez **bloc-notes Jupyter** à partir du Panneau de Cluster Dashboard__ hello.

    ![tableaux de bord de cluster Hello](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. Dans hello coin supérieur droit de la page de Notebook hello, sélectionnez **nouveau**, puis **Scala**. Un nouvel onglet de navigateur s’ouvre, contenant un bloc-notes Jupyter basé sur Scala.
3. Dans le premier champ de hello (appelé un **cellule**) sur la page de hello, entrez hello suivant du texte :

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Ce code configure Spark toorecursively accès hello structure de répertoire pour les données d’entrée hello. Application Insights la télémétrie est ouvert une structure de répertoires tooa similaire`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Utilisez **MAJ + ENTRÉE** code hello de toorun. Sur hello à gauche de la cellule de hello, un «\*» s’affiche entre hello crochets tooindicate que code hello dans cette cellule est en cours d’exécution. Une fois qu’il se termine, hello '\*' modifie tooa nombre et la sortie similaire toohello suit texte s’affiche sous la cellule de hello :

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Une nouvelle cellule est créée sous hello tout d’abord un. Entrez hello après le texte dans la nouvelle cellule de hello. Remplacez `CONTAINER` et `STORAGEACCOUNT` avec le nom de compte de stockage Windows Azure hello et le nom de conteneur qui contient l’Application Insights se connecte.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Utilisez **MAJ + ENTRÉE** tooexecute cette cellule. Vous voyez un toohello similaire de résultat suivant de texte :

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    chemin d’accès de wasb Hello retourné est un emplacement hello Hello les données de télémétrie Application Insights. Hello de modification `hdfs dfs -ls` hello cellule toouse hello wasb chemin d’accès retourné de ligne, puis utilisez **MAJ + ENTRÉE** cellule de hello toorun à nouveau. Ce temps, les résultats hello doivent afficher les répertoires hello qui contiennent des données de télémétrie.

   > [!NOTE]
   > Les étapes de cette section reste hello Hello, hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` active a été utilisée. Ce répertoire n’existe peut-être pas, sauf si vos données de télémétrie sont destinées à une application web.

6. Dans la cellule suivante de hello, entrez hello suivant code : Remplacez `WASB\_PATH` avec chemin d’accès de hello à partir de l’étape précédente de hello.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Ce code crée une trame de données à partir des fichiers JSON hello exportées par le processus d’exportation continue hello. Utilisez **MAJ + ENTRÉE** toorun cette cellule.

7. Dans la cellule suivante de hello, entrez et exécutez hello suivant schéma hello tooview Spark créé pour les fichiers JSON hello :

   ```scala
   jsonData.printSchema
   ```

    schéma Hello pour chaque type de données de télémétrie est différent. exemple Hello est hello de schéma est généré pour les demandes web (les données stockées dans hello `Requests` sous-répertoire) :

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Utilisez hello suivant tooregister hello trame de données comme une table temporaire et exécuter une requête sur les données de salutation :

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Cette requête retourne des informations de ville hello pour les premiers enregistrements de 20 hello où context.location.city n’est pas null.

   > [!NOTE]
   > structure de contexte Hello est présente dans toutes les données de télémétrie enregistrées par l’Application Insights. élément de ville Hello ne peut-être pas être rempli dans vos journaux. Utilisez hello schéma tooidentify autres éléments que vous pouvez interroger peuvent contenir des données de vos journaux.
   >
   >

    Cette requête retourne toohello similaire à informations suivant le texte :

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’exemples d’utilisation de Spark toowork avec des données et des services dans Azure, consultez hello suivant des documents :

* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Pour plus d’informations sur la création et exécution d’applications Spark, consultez hello suivant des documents :

* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécution de travaux à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)
