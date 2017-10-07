---
title: "exemple avec MLlib Spark sur HDInsight - Azure d’apprentissage d’aaaMachine | Documents Microsoft"
description: "Découvrez comment toouse Spark MLlib toocreate une application d’apprentissage machine qui analyse un dataset à l’aide de la classification de régression logistique."
keywords: machine learning spark, exemple de machine learning spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Utiliser Spark MLlib toobuild une application d’apprentissage et analyser un jeu de données

Découvrez comment toouse Spark **MLlib** toocreate une application toodo simple analyse prédictive sur Ouvrir un jeu de données d’apprentissage. À partir des bibliothèques de Machine Learning intégrées de Spark, cet exemple utilise une *classification* de régression logistique. 

> [!TIP]
> Ce exemple est également disponible en tant que bloc-notes Jupyter sur un cluster Spark (Linux) que vous créez dans HDInsight. expérience de bloc-notes Hello vous permet d’exécuter des extraits de code hello Python à partir de l’ordinateur portable hello lui-même. didacticiel de hello toofollow à partir d’un ordinateur portable, créer un Spark cluster et lancez un bloc-notes jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). Ensuite, exécutez bloc-notes de hello **Spark Machine Learning - analyse prédictive sur les données d’inspection de produits alimentaires à l’aide de MLlib.ipynb** sous hello **Python** dossier.
>
>

MLLib est une bibliothèque principale Spark qui fournit de nombreux utilitaires pratiques pour l’exécution de tâches de Machine Learning. Certains de ces utilitaires conviennent pour les tâches suivantes :

* Classification
* Régression
* Clustering
* Modélisation de rubrique
* Décomposition de valeur singulière (SVD) et analyse des composants principaux (PCA)
* Hypothèse de test et de calcul des exemples de statistiques

## <a name="what-are-classification-and-logistic-regression"></a>Qu’est-ce que la classification et la régression logistique ?
*Classification*, une tâche, d’apprentissage populaire est hello les processus de tri des données d’entrée en catégories. Il s’agit de travail hello d’un toofigure d’algorithme de classification comment tooassign « étiquettes » tooinput les données que vous fournissez. Par exemple, vous pourriez utiliser un algorithme d’apprentissage automatique qui accepte les informations de stock en tant qu’entrée et divise hello stock en deux catégories : que vous devez vendre et des stocks vous devez prendre.

La régression logistique est un algorithme de hello que vous utilisez pour la classification. L’API de régression logistique de Spark est utile pour la *classification binaire*ou pour classer les données d’entrée dans un des deux groupes. Pour plus d’informations sur la régression logistique, consultez [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).

En résumé, le processus hello de régression logistique génère une *fonction logistique* qui peut être utilisé toopredict hello probabilité est qu’un vecteur d’entrée appartienne à un groupe ou hello autres.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Exemple d’analyse prédictive sur des données d’inspection alimentaire
Dans cet exemple, vous utilisez Spark tooperform des analyses prédictives sur les données d’inspection alimentaires (**Food_Inspections1.csv**) qui a été acquis via hello [portail de données Ville de Chicago](https://data.cityofchicago.org/). Ce jeu de données contient des informations sur les contrôles d’établissement alimentaires qui ont été effectués à Chicago, notamment des informations sur chacun d’eux, les violations de hello trouvée (le cas échéant) et hello les résultats de l’inspection de hello. fichier de données CSV Hello est déjà disponible dans hello compte de stockage associé au cluster hello à **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

Dans la procédure hello ci-dessous, vous développez un modèle toosee à ce qu’il faut toopass ou échouer une inspection de produits alimentaires.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Commencer à créer une application de Machine Learning Spark MMLib
1. À partir de hello [portail Azure](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.   
1. Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

   > [!NOTE]
   > Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Créez un bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.

    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Créer un bloc-notes Jupyter")
1. Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.

    ![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "fournir un nom d’ordinateur portable de hello")
1. Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement. contextes de Spark et Hive Hello sont créées automatiquement pour vous lors de l’exécution de la première cellule de code hello. Vous pouvez commencer à créer votre application d’apprentissage en important les types hello requis pour ce scénario. toodo, placez le curseur de hello dans la cellule de hello et appuyez sur **MAJ + ENTRÉE**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Construire une trame de données d’entrée
Nous pouvons utiliser `sqlContext` tooperform des transformations sur des données structurées. tâche première Hello est données d’exemple hello tooload ((**Food_Inspections1.csv**)) dans un Spark SQL *trame de données*.

1. Étant donné que les données brutes hello sont dans un format CSV, nous devons toouse hello Spark contexte toopull chaque ligne du fichier de hello en mémoire sous forme de texte non structuré ; Ensuite, vous utilisez tooparse de bibliothèque Python CSV chaque ligne individuellement.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. Nous disposons désormais d’un fichier CSV hello comme un RDD.  schéma de hello toounderstand de données de hello, nous permet de récupérer une ligne à partir de hello RDD.

        inspections.take(1)

    Vous devez voir une sortie semblable à hello suivante :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. Hello sortie précédente nous donne une idée du schéma hello du fichier d’entrée de hello. Il inclut le nom hello de chaque établissement, le type hello de l’établissement, l’adresse de hello, données hello de contrôles de hello et l’emplacement de hello, entre autres choses. Nous allons sélectionner plusieurs colonnes qui sont utiles pour notre analyse prédictive et regroupement les résultats de hello en tant qu’une trame de données, ce qui nous puis utilisent toocreate une table temporaire.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Nous avons maintenant un *tableau de données*, `df` sur lequel nous pouvons effectuer l’analyse. Nous obtenons également une table temporaire **CountResults**. Nous avons inclus des quatre colonnes dignes d’intérêt dans la trame de données hello : **id**, **nom**, **résultats**, et **violations**.

    Nous allons obtenir un petit échantillon de données de salutation :

        df.show(5)

    Vous devez voir une sortie semblable à hello suivante :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a>Comprendre les données de salutation
1. Nous pouvons commencer tooget une idée de ce que notre jeu de données contient. Par exemple, quelles sont les valeurs différentes de hello Bonjour **résultats** colonne ?

        df.select('results').distinct().show()

    Vous devez voir une sortie semblable à hello suivante :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. Une visualisation rapide peut nous aider à raison sur la distribution de hello de ces résultats. Nous avons déjà les données de salutation dans une table temporaire **CountResults**. Vous pouvez exécuter hello suivant la requête SQL sur hello table tooget une meilleure compréhension de la répartition des résultats de hello.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Hello `%%sql` magique suivie `-o countResultsdf` garantit que sortie hello de requête de hello est rendu persistant localement sur le serveur de Notebook hello (généralement hello nœud principal du cluster de hello). sortie de Hello est conservée en tant qu’un [Pandas](http://pandas.pydata.org/) nom spécifié de trame de données avec hello **countResultsdf**.

    Vous devez voir une sortie semblable à hello suivante :

    ![Résultat de la requête SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Résultat de la requête SQL")

    Pour plus d’informations sur hello `%%sql` magique et autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. Vous pouvez également utiliser Matplotlib, une bibliothèque utilisée tooconstruct une visualisation des données, toocreate un tracé. Étant donné que le traçage de hello doit être créé à partir de hello localement persistantes **countResultsdf** trame de données, l’extrait de code hello doit commencer par hello `%%local` magique. Cela garantit que le code de hello est exécuté localement sur le serveur de Notebook hello.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Vous devez voir une sortie semblable à hello suivante :

    ![Sortie de l’application de Machine Learning Spark : graphique en secteurs avec cinq résultats d’inspection distincts](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Sortie du résultat de l’application de Machine Learning Spark")
1. Vous pouvez voir qu’il existe 5 résultats d’inspection distincts.

   * Entreprise introuvable
   * Échec
   * Réussite
   * Réussite avec conditions
   * Cessation d’activités

     Nous développer un modèle qui peut deviner résultat hello d’une inspection de produits alimentaires, les violations de hello donné. Étant donné que la régression logistique est une méthode de classification binaire, il est logique toogroup nos données en deux catégories : **échouer** et **passer**. Un « passer avec Conditions » est toujours un passage, donc lorsque nous former le modèle de hello, nous considérons hello deux résultats équivalent. Données avec hello autres résultats (« Business introuvable » ou « d’entreprise ») ne sont pas utiles pour nous les supprimer à partir de notre jeu d’apprentissage. Étant donné que ces deux catégories constituent un très petit pourcentage de résultats de hello tout de même, il doit être OK.
1. À présent, convertissons notre trame de données existante (`df`) en une nouvelle trame de données dans laquelle chaque inspection est représentée par une paire de violations étiquetée. Dans notre cas, une étiquette `0.0` représente un échec, une étiquette `1.0` représente une réussite et une étiquette `-1.0` représente d’autres résultats. Nous filtrer ces autres résultats lors du calcul de nouvelle trame de données hello.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee quel hello étiqueté ressemble à des données, nous allons extraire une ligne.

        labeledData.take(1)

    Vous devez voir une sortie semblable à hello suivante :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Créer un modèle de régression logistique à partir de la trame de données d’entrée hello
La dernière tâche est hello tooconvert intitulé des données dans un format qui peut être analysé par la régression logistique. algorithme de régression logistique Hello tooa d’entrée doit être un ensemble de *paires de vecteur de fonctionnalité d’étiquettes*, où hello « vecteur de fonctionnalité » est un vecteur de nombres représentant le point d’entrée de hello. Par conséquent, nous devons colonne tooconvert des violations « hello », qui est semi-structurées et contient le nombre de commentaires dans le tableau de tooan en texte libre, de nombres réels qui comprend un ordinateur facilement.

Une approche d’apprentissage machine standard pour le traitement en langage naturel est tooassign chaque mot distinct un « index » et transmettez un vecteur toohello algorithme d’apprentissage tels que les valeur de chaque index contient la fréquence relative de hello de ce mot dans le texte hello chaîne.

MLlib fournit un moyen simple de tooperform cette opération. Tout d’abord, « réinitialiser » chaque violations chaîne tooget hello mots individuels dans chaque chaîne. Ensuite, utilisez un `HashingTF` tooconvert chaque ensemble de jetons dans un vecteur de fonctionnalité qui peut ensuite être tooconstruct d’algorithme de régression logistique toohello passé un modèle. Nous allons effectuer toutes ces étapes successivement à l’aide d’un « pipeline ».

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Évaluation du modèle hello sur un jeu de données de test distinct
Nous pouvons utiliser le modèle hello créée précédemment trop*prédire* quel hello résultats de nouveaux contrôles sera, en fonction de violations hello qui ont été observées. Nous ce modèle entraîné sur hello dataset **Food_Inspections1.csv**. Nous utiliser un deuxième dataset **Food_Inspections2.csv**, trop*évaluer* hello puissance de ce modèle sur de nouvelles données. Ce deuxième ensemble de données (**Food_Inspections2.csv**) doit être déjà dans le conteneur de stockage par défaut hello associé hello cluster.

1. Hello extrait de code suivant crée une nouvelle trame de données, **predictionsDf** qui contient la prédiction hello générée par le modèle de hello. extrait de code Hello crée également une table temporaire nommée **prédictions** en fonction de la trame de données hello.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Vous devez voir une sortie semblable à hello suivante :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. Recherchez une des prédictions de hello. Exécutez cet extrait de code :

        predictionsDf.take(1)

   Il existe une prédiction pour hello première entrée de jeu de données de test hello.
1. Hello `model.transform()` méthode s’applique hello même transformation tooany nouvelles données avec hello même schéma et arrivent à une prédiction de comment tooclassify hello des données. Nous pouvons effectuer certains tooget statistiques simple une idée de la précision de nos prédictions étaient :

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    sortie de Hello ressemble à hello suivantes :

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    À l’aide de la régression logistique avec Spark nous donne un modèle précis de relation hello entre des descriptions de violations en anglais et indique si une activité donnée est réussir ou d’échouer une inspection de produits alimentaires.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Créer une représentation visuelle de prédiction de hello
Nous pouvons maintenant construire un toohelp visualisation final que nous analyser les résultats de hello de ce test.

1. Nous allons commencer en extrayant des prédictions différentes hello et résultats de hello **prédictions** table temporaire créée précédemment. Hello de requêtes suivants hello une sortie distincte en tant que *true_positive*, *false_positive*, *true_negative*, et *false_negative*. Dans les requêtes de hello ci-dessous, nous désactivons visualisation à l’aide de `-q` et également enregistrer la sortie de hello (à l’aide de `-o`) en tant que les trames de données qui peuvent être utilisées ensuite par hello `%%local` magique.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Enfin, utilisez hello suivant à l’aide d’extrait toogenerate hello traçage **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Vous devez voir hello suivant de sortie :

    ![Sortie de l’application de Machine Learning Spark : graphique en secteurs des pourcentages d’inspections alimentaires qui ont échoué.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Sortie du résultat de l’application de Machine Learning Spark")

    Dans ce graphique, un résultat « positif » fait référence toohello échoué de l’inspection de produits alimentaires, tandis qu’un résultat négatif tooa passé inspection.

## <a name="shut-down-hello-notebook"></a>Arrêter le bloc-notes de hello
Une fois que vous avez terminé d’exécuter l’application hello, vous devez arrêter les ressources de hello toorelease hello bloc-notes. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**. Cette opération arrête et ferme hello bloc-notes.

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Streaming Spark : utilisez Spark dans HDInsight pour créer des applications de streaming en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
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
