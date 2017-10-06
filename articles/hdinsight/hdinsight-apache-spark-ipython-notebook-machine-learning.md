---
title: applications sur Azure HDInsight apprentissage Apache Spark automatique aaaBuild | Documents Microsoft
description: "Instructions détaillées sur la façon dont les clusters toobuild Apache Spark d’apprentissage application sur HDInsight Spark à l’aide du bloc-notes jupyter"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Créer des applications de Machine Learning Apache Spark sur Azure HDInsight

Découvrez comment toobuild une application d’apprentissage machine Apache Spark à l’aide d’un Spark de cluster sur HDInsight. Cet article explique comment toouse hello bloc-notes jupyter disponible avec hello cluster toobuild et tester cette application. application Hello utilise hello HVAC.csv d’un échantillon de données disponibles sur tous les clusters par défaut.

**Configuration requise :**

Vous devez disposer de hello :

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Comprendre le jeu de données hello
Avant de commencer à générer l’application hello, faites-nous comprendre hello structure de données hello pour lequel nous générer application hello et type hello d’analyse, que nous ferons sur les données de salutation. 

Dans cet article, nous utilisons l’exemple hello **HVAC.csv** fichier de données qui est disponible dans hello compte de stockage Azure que vous avez associé le cluster HDInsight de hello. Dans le compte de stockage hello, fichier de hello est à **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Téléchargez et ouvrez tooget de fichier CSV hello un instantané des données de hello.  

![Capture instantanée des données utilisées pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Capture instantanée des données utilisées pour l’exemple de Machine Learning Spark")

les données de salutation montrent la température de cible de hello et hello de température réelle d’une construction qui HVAC système est installé. Supposons que hello **système** colonne représente l’ID de système hello et hello **SystemAge** colonne représente le nombre de hello d’années système de climatisation hello a été mises en place au niveau de la construction de hello.

Si une génération sera chaudes ou surgelé basé sur la température de cible hello, étant donné un ID système et l’âge du système, nous utilisons cette toopredict de données.

## <a name="app"></a>Écrire une application de Machine Learning Spark à l’aide de Spark MLlib
Dans cette application, nous utilisons un tooperform de pipeline Spark ML une classification de document. Dans le pipeline de hello, nous fractionner les documents de hello en mots, convertir les mots hello dans un vecteur de fonctionnalité numériques et enfin créer un modèle de prévision à l’aide d’étiquettes et les vecteurs de caractéristiques hello. Effectuer hello après application de hello toocreate étapes.

1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.   
2. Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.
   
   > [!NOTE]
   > Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Créer un nouveau bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.
   
    ![Créer un bloc-notes Jupyter pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Créer un bloc-notes Jupyter pour l’exemple de Machine Learning Spark")
4. Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.
   
    ![Fournir un nom de bloc-notes pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fournir un nom de bloc-notes pour l’exemple de Machine Learning Spark")
5. Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement. contextes de Spark et Hive Hello seront automatiquement créés pour vous lors de l’exécution de la première cellule de code hello. Vous pouvez commencer par importer les types hello qui sont requis pour ce scénario. Collez hello suivant extrait dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE**. 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. Maintenant, vous devez charger les données de salutation (hvac.csv), analyser et utiliser le modèle de hello tootrain. Pour ce faire, vous définissez une fonction qui vérifie si la température réelle de hello de construction de hello est supérieure à la température de cible hello. Si la température réelle de hello est supérieure, génération de hello est à chaud, représentée par la valeur de hello **1.0**. Si la température réelle de hello est moindre, génération de hello est à froid, représentée par la valeur de hello **0.0**. 
   
    Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. Configurer le pipeline d’apprentissage automatique Spark hello qui se compose de trois étapes : Générateur de jetons, hashingTF et lr. Pour plus d’informations sur ce qu’est un pipeline et sur son fonctionnement, consultez <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.
   
    Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Document de formation pipeline toohello hello adaptée. Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.
   
        model = pipeline.fit(training)
3. Vérifiez que hello formation document toocheckpoint votre progression avec l’application hello. Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.
   
        training.show()
   
    Suit toohello similaire de hello sortie doit s’afficher :
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    Revenir en arrière et vérifier la sortie hello par rapport à un fichier CSV brut hello. Par exemple, hello premier ligne hello fichier CSV comporte les données :

    ![Capture instantanée des données de sortie pour l’exemple de Machine Learning Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Capture instantanée des données de sortie pour l’exemple de Machine Learning Spark")

    Notez que la température réelle de hello est inférieure à la température de cible hello suggérant la construction de hello est à froid. Par conséquent, dans la sortie de formation hello, hello valeur pour **étiquette** Bonjour la première ligne est **0.0**, ce qui signifie bâtiment de hello n’est pas actif.

1. Préparez un jeu de données toorun hello formé par rapport. toodo par conséquent, il peut passer sur un ID système et l’âge du système (notée **SystemInfo** dans la sortie de formation hello), et le modèle de hello serait prédire hello indique si la génération avec cet âge de système et des ID système seraient être chaudes (signalées par 1.0) ou refroidissement ( signalés par 0.0).
   
   Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Enfin, élaborer des prédictions sur les données de test hello. Hello coller suivant extrait dans une cellule vide appuyez sur **MAJ + ENTRÉE**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Vous devez voir s’afficher une sortie similaire toohello :
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   À partir de hello première ligne dans une prédiction de hello, vous pouvez voir que pour un système de climatisation avec l’ID 20 et l’âge de système de 25 ans, génération de hello sera à chaud (**prédiction = 1.0**). Hello première valeur de DenseVector (0.49999) correspond toohello prédiction 0,0 et la valeur de seconde hello (0.5001) correspond toohello prédiction 1.0. Dans la sortie de hello, même si la valeur de seconde hello n’est légèrement plus élevé, hello modèle montre **prédiction = 1.0**.
4. Une fois que vous avez terminé d’exécuter l’application hello, vous devez le ressources hello toorelease arrêt hello bloc-notes. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**. Cette s’arrête et le bloc-notes de fermer hello.

## <a name="anaconda"></a>Utiliser une bibliothèque scikit-learn Anaconda pour le Machine Learning Spark
Les clusters Apache Spark sur HDInsight incluent des bibliothèques Anaconda, Cela inclut également hello **scikit-en savoir plus** bibliothèque pour l’apprentissage. bibliothèque de Hello inclut également différents jeux de données que vous pouvez utiliser les exemples d’applications toobuild directement à partir d’un bloc-notes jupyter. Pour obtenir des exemples sur l’utilisation de hello scikit-bibliothèque de plus, consultez [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
