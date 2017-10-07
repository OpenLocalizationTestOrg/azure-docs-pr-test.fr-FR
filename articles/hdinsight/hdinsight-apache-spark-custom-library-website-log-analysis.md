---
title: "journaux du site Web aaaAnalyze avec les bibliothèques de Python dans Spark - Azure | Documents Microsoft"
description: "Ce bloc-notes montre comment enregistrer les données à l’aide d’une bibliothèque personnalisée avec Spark sur Azure HDInsight tooanalyze."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Analyser des journaux de site web en utilisant une bibliothèque Python personnalisée avec un cluster Spark sur HDInsight

Ce bloc-notes montre comment enregistrer les données à l’aide d’une bibliothèque personnalisée avec Spark sur HDInsight tooanalyze. Hello personnalisé, nous utilisons est une bibliothèque Python appelé **iislogparser.py**.

> [!TIP]
> Ce didacticiel est également disponible en tant que bloc-notes Jupyter sur un cluster Spark (Linux) que vous créez dans HDInsight. expérience de bloc-notes Hello vous permet d’exécuter des extraits de code hello Python à partir de l’ordinateur portable hello lui-même. didacticiel de hello tooperform à partir d’un ordinateur portable, créez un cluster Spark, lancer un bloc-notes jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), puis exécutez bloc-notes de hello **analyser les journaux avec Spark à l’aide d’un library.ipynb personnalisé** sous hello  **PySpark** dossier.
>
>

**Configuration requise :**

Vous devez disposer de hello :

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Enregistrer des données brutes en tant que RDD
Dans cette section, nous utilisons hello [Notebook](https://jupyter.org) bloc-notes associé à un cluster d’Apache Spark dans HDInsight travaux toorun traiter vos données d’exemple brut et l’enregistrer en tant qu’une table Hive. données d’exemple Hello sont un fichier .csv (hvac.csv) disponible sur tous les clusters par défaut.

Une fois que vos données sont enregistrées dans une table Hive, nous se connecte dans la section suivante de hello table Hive de toohello à l’aide des outils de BI tels que Power BI et de Tableau.

1. À partir de hello [portail Azure](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.   
2. Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

   > [!NOTE]
   > Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Créer un nouveau bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.

    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Créer un bloc-notes Jupyter")
4. Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.

    ![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "fournir un nom d’ordinateur portable de hello")
5. Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement. contextes de Spark et Hive Hello seront automatiquement créés pour vous lors de l’exécution de la première cellule de code hello. Vous pouvez commencer par importer les types hello qui sont requis pour ce scénario. Collez hello suivant extrait dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Créer un RDD à l’aide des données de journal exemple hello déjà disponibles sur le cluster de hello. Vous pouvez accéder aux hello hello compte de stockage par défaut associé au cluster hello à **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Récupérer qu'un exemple de journal défini tooverify cette étape précédente hello s’est terminée correctement.

        logs.take(5)

    Vous devez voir s’afficher une sortie similaire toohello :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Analysez les données de journal à l'aide d'une bibliothèque Python personnalisée
1. Dans la sortie de hello ci-dessus, hello premier deux lignes incluent des informations d’en-tête hello et chaque ligne restante correspond au schéma de hello décrit dans cet en-tête. L’analyse de tels journaux peut s’avérer complexe. Par conséquent, nous utilisons une bibliothèque Python personnalisée (**iislogparser.py**) qui facilite beaucoup l'analyse de tels journaux. Par défaut, cette bibliothèque est incluse avec votre cluster Spark sur HDInsight dans **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    Toutefois, cette bibliothèque n’est pas Bonjour `PYTHONPATH` donc nous ne pouvons pas l’utiliser à l’aide d’une instruction d’importation comme `import iislogparser`. toouse cette bibliothèque, nous devons distribuer de nœuds de travail tooall hello. Exécutez hello suivant extrait de code.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`Fournit une fonction `parse_log_line` qui retourne `None` si une ligne de journal est une ligne d’en-tête et retourne une instance de hello `LogLine` classe s’il rencontre une ligne de journal. Hello d’utilisation `LogLine` tooextract de la classe hello uniquement les lignes de journal à partir de hello RDD :

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Récupérer quelques lignes extraites du journal tooverify qui hello étape s’est terminée avec succès.

       logLines.take(2)

   sortie de Hello sont similaires toohello suivants :

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Hello `LogLine` (classe), à son tour, a des méthodes utiles, tels que `is_error()`, qui indique si une entrée de journal a un code d’erreur. Utiliser ce numéro de hello toocompute des erreurs de lignes du journal hello extrait et puis journal tous les hello erreurs tooa différents.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Vous devez voir une sortie semblable à hello suivante :

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. Vous pouvez également utiliser **Matplotlib** tooconstruct une visualisation des données de hello. Par exemple, si vous souhaitez la cause de hello tooisolate de requêtes qui s’exécutent pendant une longue période, vous pourriez fichiers hello toofind prenant hello la plupart des tooserve de temps en moyenne.
   extrait de code Hello ci-dessous récupère hello top 25 ressources qui a nécessité la plupart des temps tooserve une demande.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Vous devez voir une sortie semblable à hello suivante :

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. Vous pouvez également présenter ces informations sous forme de hello du tracé. Une première étape toocreate un tracé, faites-le nous tout d’abord créer une table temporaire **AverageTime**. Bonjour Bonjour de groupes de table ouvre une session en temps toosee s’il y a des pics d’activité inhabituelle latence à un moment donné.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. Vous pouvez ensuite exécuter hello suivant tooget de requête SQL tous les enregistrements de hello Bonjour **AverageTime** table.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Hello `%%sql` magique suivie `-o averagetime` garantit que sortie hello de requête de hello est rendu persistant localement sur le serveur de Notebook hello (généralement hello nœud principal du cluster de hello). sortie de Hello est conservée en tant qu’un [Pandas](http://pandas.pydata.org/) nom spécifié de trame de données avec hello **averagetime**.

   Vous devez voir une sortie semblable à hello suivante :

   ![Résultat de la requête SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Résultat de la requête SQL")

   Pour plus d’informations sur hello `%%sql` magic, voir [paramètres pris en charge par hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. Vous pouvez maintenant utiliser Matplotlib, une bibliothèque utilisée tooconstruct une visualisation des données, toocreate un tracé. Étant donné que le traçage de hello doit être créé à partir de hello localement persistantes **averagetime** trame de données, l’extrait de code hello doit commencer par hello `%%local` magique. Cela garantit que le code de hello est exécuté localement sur le serveur de Notebook hello.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Vous devez voir une sortie semblable à hello suivante :

   ![Résultat Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Résultat Matplotlib")
8. Une fois que vous avez terminé d’exécuter l’application hello, vous devez le ressources hello toorelease arrêt hello bloc-notes. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**. Cette s’arrête et le bloc-notes de fermer hello.

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a>Création et exécution d’applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)
