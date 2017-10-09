---
title: "les packages Maven personnalisés aaaUse avec Notebook dans Spark sur Azure HDInsight | Documents Microsoft"
description: "Obtenir des instructions détaillées sur comment tooconfigure Notebook ordinateurs portables avec HDInsight Spark clusters toouse des packages Maven personnalisés."
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
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Utilisation de packages externes avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight
> [!div class="op_single_selector"]
> * [À l’aide de la commande magique de cellule](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [À l’aide d’une action de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Découvrez comment tooconfigure un bloc-notes jupyter cluster Apache Spark sur HDInsight toouse externe, conçu par la Communauté **maven** packages qui ne sont pas inclus l’emploi dans le cluster de hello. 

Vous pouvez rechercher hello [référentiel de Maven](http://search.maven.org/) pour la liste complète des packages disponibles hello. Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources. Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).

Dans cet article, vous allez apprendre comment toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package avec un bloc-notes jupyter de hello.



## <a name="prerequisites"></a>Composants requis
Vous devez disposer de hello :

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Utiliser des packages externes avec les blocs-notes Jupyter
1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.   
2. Dans le panneau de cluster Spark hello, cliquez sur **liens rapides**, puis à partir de hello **tableau de bord de Cluster** panneau, cliquez sur **bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

    > [!NOTE]
    > Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Créer un nouveau bloc-notes. Cliquez sur **Nouveau**, puis sur **Spark**.
   
    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Créer un bloc-notes Jupyter")

4. Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.
   
    ![Fournissez un nom pour l’ordinateur portable de hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "fournir un nom d’ordinateur portable de hello")

5. Vous allez utiliser hello `%%configure` tooconfigure magique hello bloc-notes toouse un lot externe. Dans les ordinateurs portables qui utilisent les packages externes, assurez-vous que vous appelez hello `%%configure` magique dans la première cellule de code hello. Cela garantit que noyau hello est configuré toouse hello du package avant le démarrage de session de hello.

    >[!IMPORTANT] 
    >Si vous oubliez le noyau de hello tooconfigure dans la première cellule de hello, vous pouvez utiliser hello `%%configure` avec hello `-f` paramètre, mais qui va redémarrer la session de hello et tous les cours seront perdues.

    | Version de HDInsight | Commande |
    |-------------------|---------|
    |Pour HDInsight 3.3 et HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Pour HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. extrait de code Hello ci-dessus attend des coordonnées maven hello package externe de hello dans un référentiel Central de Maven. Dans cet extrait de code, `com.databricks:spark-csv_2.10:1.4.0` est coordonnée maven hello **spark-csv** package. Voici comment construire des coordonnées hello pour un package.
   
    a. Recherchez le package de hello Bonjour Maven référentiel. Dans ce didacticiel, nous utilisons [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. À partir de référentiel de hello, collectez les valeurs hello pour **GroupId**, **ArtifactId**, et **Version**. Assurez-vous que les valeurs hello réuni correspondent à votre cluster. Dans ce cas, nous utilisons un Scala 2.10 et le package de Spark 1.4.0, mais vous devrez peut-être tooselect différentes versions pour la version appropriée de Scala ou Spark hello dans votre cluster. Vous trouverez la version Scala hello sur votre cluster en exécutant `scala.util.Properties.versionString` sur le noyau de Spark Notebook hello ou envoyer de Spark. Vous trouverez la version hello Spark sur votre cluster en exécutant `sc.version` sur les ordinateurs portables de disponible.
   
    ![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")
   
    c. Concaténer des valeurs hello trois, séparés par un signe deux-points (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Exécuter la cellule de code hello avec hello `%%configure` magique. Cette opération va configurer hello sous-jacent Livy session toouse hello package fourni. Dans les cellules suivantes hello dans Bloc-notes de hello, vous pouvez maintenant utiliser des package de hello, comme indiqué ci-dessous.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Vous pouvez ensuite exécuter des extraits de code hello, comme illustré ci-dessous, tooview hello données à partir de la trame de données hello vous avez créé à l’étape précédente de hello.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>Voir aussi
* [Vue d’ensemble : Apache Spark sur Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scénarios
* [Spark avec BI : effectuez une analyse interactive des données à l’aide de Spark dans HDInsight avec des outils BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark avec Machine Learning : utilisez Spark dans HDInsight pour l’analyse de la température des bâtiments à l’aide des données des systèmes HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark avec Machine Learning : Spark utilisation dans résultats de l’inspection alimentaires toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark : Utiliser Spark dans HDInsight pour créer des applications de diffusion en continu en temps réel](hdinsight-apache-spark-eventhub-streaming.md)
* [Analyse des journaux de site web à l’aide de Spark dans HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Créer et exécuter des applications
* [Créer une application autonome avec Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Exécuter des tâches à distance avec Livy sur un cluster Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Outils et extensions

* [Utilisation de packages externes Python avec les blocs-notes Jupyter dans des clusters Apache Spark sur HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications de Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Utiliser des bloc-notes Zeppelin avec un cluster Spark sur HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

