---
title: "Utiliser des packages Maven personnalisés avec des blocs-notes Jupyter dans Spark sur Azure HDInsight | Documents Microsoft"
description: "Cette section comporte des instructions détaillées sur la façon de configurer des blocs-notes Jupyter disponibles avec des clusters Spark HDInsight pour utiliser des packages Maven personnalisés."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 0bcfe220e60e34937c667c7b416065d5f3dc8d63
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight
> [!div class="op_single_selector"]
> * [À l’aide de la commande magique de cellule](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [À l’aide d’une action de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Découvrez comment configurer un bloc-notes Jupyter dans un cluster Apache Spark sur HDInsight pour utiliser des packages **maven** externes bénéficiant de la contribution de la communauté, qui ne sont pas inclus dans le cluster. 

Vous pouvez rechercher le [référentiel Maven](http://search.maven.org/) pour obtenir la liste complète des packages disponibles. Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources. Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).

Dans cet article, vous allez apprendre à utiliser le package [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) avec le bloc-notes Jupyter.



## <a name="prerequisites"></a>Composants requis
Vous devez disposer des éléments suivants :

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Utiliser des packages externes avec les blocs-notes Jupyter
1. Dans le tableau d’accueil du [portail Azure](https://portal.azure.com/), cliquez sur la vignette de votre cluster Spark (si vous l’avez épinglé au tableau d’accueil). Vous pouvez également accéder à votre cluster sous **Parcourir tout** > **Clusters HDInsight**.   
2. Dans le panneau du cluster Spark, cliquez sur **Liens rapides**, puis dans le panneau **Tableau de bord du cluster**, cliquez sur **Bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification d’administrateur pour le cluster.

    > [!NOTE]
    > Vous pouvez également atteindre le bloc-notes Jupyter pour votre cluster en ouvrant l'URL suivante dans votre navigateur. Remplacez **CLUSTERNAME** par le nom de votre cluster.
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Créer un nouveau bloc-notes. Cliquez sur **Nouveau**, puis sur **Spark**.
   
    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")

4. Un nouveau bloc-notes est créé et ouvert sous le nom Untitled.pynb. Cliquez sur le nom du bloc-notes en haut, puis entrez un nom convivial.
   
    ![Donnez un nom au bloc-notes](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Donnez un nom au bloc-notes")

5. Vous allez utiliser la commande magique `%%configure` pour configurer le bloc-notes afin d’utiliser un package externe. Dans les blocs-notes utilisant des packages externes, veillez à appeler la commande magique `%%configure` dans la première cellule de code. Cela garantit que le noyau est configuré pour utiliser le package avant le démarrage de la session.

    >[!IMPORTANT] 
    >Si vous oubliez de configurer le noyau dans la première cellule, vous pouvez utiliser `%%configure` avec le paramètre `-f`. Toutefois, cette opération redémarrera la session et entraînera la perte de toute la progression.

    | Version de HDInsight | Commande |
    |-------------------|---------|
    |Pour HDInsight 3.3 et HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Pour HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. L’extrait de code ci-dessus attend une liste de coordonnées maven pour le package externe du référentiel central Maven. Dans cet extrait de code, `com.databricks:spark-csv_2.10:1.4.0` est la coordonnée maven pour le package **spark-csv** . Voici comment vous construire les coordonnées d’un package.
   
    a. Recherchez le package dans le référentiel Maven. Dans ce didacticiel, nous utilisons [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. À partir du référentiel, rassemblez les valeurs pour **GroupId**, **ArtifactId** et **Version**. Vérifiez que les valeurs que vous collectez correspondent à votre cluster. Dans ce cas, nous utilisons un package Scala 2.10 et Spark 1.4.0, mais il peut être nécessaire de sélectionner des versions différentes pour la version appropriée de Scala ou de Spark dans votre cluster. Vous pouvez trouver la version de Scala sur votre cluster en exécutant `scala.util.Properties.versionString` sur le noyau Spark Jupyter ou sur spark-submit. Vous pouvez trouver la version de Spark sur votre cluster en exécutant `sc.version` sur les notebooks Jupyter.
   
    ![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")
   
    c. Concaténez les trois valeurs séparées par deux-points (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Exécutez la cellule de code avec la commande magique `%%configure` . Cela configurera la session Livy sous-jacente pour utiliser le package fourni. Dans les cellules suivantes du bloc-notes, vous pouvez maintenant utiliser le package, comme indiqué ci-dessous.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Vous pouvez ensuite exécuter les extraits de code, comme illustré ci-dessous, pour afficher les données issues du tableau de données créé lors de l’étape précédente.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : Utiliser Spark dans HDInsight pour l’analyse de la température de bâtiments à l’aide de données HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Utiliser Spark dans HDInsight pour prédire les résultats de l’inspection des aliments](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions

* [Utilisation de packages externes Python avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [Utilisation du plugin d’outils HDInsight pour IntelliJ IDEA pour créer et soumettre des applications Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely) (Utiliser le plug-in Outils HDInsight pour IntelliJ IDEA pour déboguer des applications Spark à distance)](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Installer Jupyter sur un ordinateur et se connecter au cluster Spark sur HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources du cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight](hdinsight-apache-spark-job-debugging.md)

