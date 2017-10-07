---
title: cluster de blocs-notes de Zeppelin aaaUse avec Apache Spark sur Azure HDInsight | Documents Microsoft
description: "Obtenir des instructions détaillées sur comment les clusters blocs-notes de Zeppelin toouse avec Apache Spark sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Utiliser des blocs-notes Zeppelin avec un cluster Apache Spark sur HDInsight

Les clusters HDInsight Spark incluent les blocs-notes Zeppelin que vous pouvez utiliser les travaux de Spark toorun. Dans cet article, vous découvrez comment toouse hello bloc-notes Zeppelin sur un cluster HDInsight.

> [!NOTE]
> Les blocs-notes Zeppelin sont disponibles uniquement pour Spark 1.6.3 sur HDInsight 3.5 et Spark 2.1.0 sur HDInsight 3.6.
>

**Configuration requise :**

* Un abonnement Azure. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Lancement d’un bloc-notes Zeppelin
1. Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **Zeppelin bloc-notes**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.
   
   > [!NOTE]
   > Vous pouvez également atteindre hello Zeppelin bloc-notes pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Créer un nouveau bloc-notes. Dans le volet d’en-tête hello, cliquez sur **bloc-notes**, puis cliquez sur **créer une Note**.
   
    ![Créer un nouveau bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Créer un nouveau bloc-notes Zeppelin")
   
    Entrez un nom pour l’ordinateur portable de hello, puis cliquez sur **créer une Note**.
3. Assurez-vous également que les en-tête de bloc-notes hello présente l’état connecté. Il est indiqué par un point vert dans le coin supérieur droit de hello.
   
    ![État du bloc-notes Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "État du bloc-notes Zeppelin")
4. Chargez un exemple de données dans une table temporaire. Lorsque vous créez un cluster Spark dans HDInsight, le fichier de données d’exemple hello, **hvac.csv**, est le compte de stockage toohello copié associée sous **\HdiSamples\SensorSampleData\hvac**.
   
    Dans hello paragraphe vide qui est créé par défaut dans le bloc-notes hello, collez hello suivant extrait de code.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Appuyez sur **MAJ + ENTRÉE** ou cliquez sur hello **lire** bouton pour l’extrait de code hello paragraphe toorun hello. état Hello sur la droite hello du paragraphe de hello doit progression prêt, en attente, en cours d’exécution tooFINISHED. sortie de Hello s’affiche en bas de hello Hello même paragraph. capture d’écran de Hello ressemble à hello suivantes :
   
    ![Créer une table temporaire à partir de données brutes](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Créer une table temporaire à partir de données brutes")
   
    Vous pouvez également fournir un paragraphe tooeach de titre. À partir de l’angle supérieur droit de hello, cliquez sur hello **paramètres** icône, puis cliquez sur **afficher le titre**.
5. Vous pouvez désormais exécuter des instructions SQL de Spark sur hello **hvac** table. Collez hello suivant la requête dans un nouveau paragraphe. requête de Hello récupère les ID de génération hello et différence hello entre la cible de hello et températures réels pour chaque génération sur une date donnée. Appuyez sur **MAJ + ENTRÉE**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Hello **% sql** instruction au début de hello indique à l’interpréteur de Livy Scala hello bloc-notes toouse hello.
   
    Hello capture d’écran suivante montre la sortie de hello.
   
    ![Exécuter une instruction Spark SQL à l’aide du bloc-notes de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "exécuter une instruction Spark SQL à l’aide du bloc-notes de hello")
   
     Cliquez sur hello affichage options (rectangle surligné en) tooswitch entre différentes représentations pour hello même sortie. Cliquez sur **paramètres** toochoose quel constitue hello clé et les valeurs de sortie de hello. capture d’écran ci-dessus utilise de Hello **buildingID** en tant que clé de hello et moyenne hello de **temp_diff** en tant que valeur de hello.
6. Vous pouvez également exécuter des instructions de Spark SQL à l’aide de variables de requête de hello. Hello suivante extrait de code montre comment toodefine une variable, **Temp**, dans la requête de hello avec les valeurs possibles de hello souhaité tooquery avec. Lors de la première exécution de requête de hello, une liste déroulante est automatiquement remplie avec les valeurs hello que vous avez spécifié pour la variable de hello.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Collez cet extrait dans un nouveau paragraphe, puis appuyez sur **MAJ + ENTRÉE**. Hello capture d’écran suivante montre la sortie de hello.
   
    ![Exécuter une instruction Spark SQL à l’aide du bloc-notes de hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "exécuter une instruction Spark SQL à l’aide du bloc-notes de hello")
   
    Pour les requêtes suivantes, vous pouvez sélectionner une nouvelle valeur à partir de déroulante hello et réexécutez la requête de hello. Cliquez sur **paramètres** toochoose quel constitue hello clé et les valeurs de sortie de hello. Hello capture d’écran ci-dessus utilise **buildingID** en tant que clé de hello, hello moyenne de **temp_diff** en tant que valeur hello et **targettemp** en tant que groupe de hello.
7. Redémarrez hello application hello de Livy interpréteur tooexit. toodo, ouvrez Paramètres de l’interpréteur en cliquant sur hello consigné dans le nom d’utilisateur à partir de l’angle supérieur droit de hello, puis cliquez sur **interpréteur**.
   
    ![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")
8. Faites défiler les paramètres d’interpréteur tooLivy, puis cliquez sur **redémarrer**.
   
    ![Redémarrez hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "redémarrer hello Zeppelin intepreter")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Utilisation des packages externes avec l’ordinateur portable de hello
Vous pouvez configurer le bloc-notes de Zeppelin hello cluster Apache Spark sur HDInsight (Linux) toouse externe conçu par la Communauté de packages, qui ne sont pas inclus out-of-the-box dans un cluster de hello. Vous pouvez rechercher hello [référentiel de Maven](http://search.maven.org/) pour la liste complète des packages disponibles hello. Vous pouvez également obtenir une liste des packages disponibles à partir d’autres sources. Par exemple, une liste complète des packages bénéficiant de la contribution de la communauté est disponible sur le site [Spark Packages](http://spark-packages.org/)(Packages Spark).

Dans cet article, vous verrez comment toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package avec un bloc-notes jupyter de hello.

1. Ouvrez les paramètres de l’interpréteur. Hello en haut à droite, cliquez sur hello consigné dans le nom d’utilisateur, puis cliquez sur **interpréteur**.
   
    ![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")
2. Faites défiler les paramètres d’interpréteur tooLivy, puis cliquez sur **modifier**.
   
    ![Modifier les paramètres de l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Modifier les paramètres de l’interpréteur")
3. Ajoutez une nouvelle clé, appelée **livy.spark.jars.packages** et définissez sa valeur au format de hello `group:id:version`. Par conséquent, si vous souhaitez toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) package, vous devez définir les valeur hello de clé de hello trop`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Modifier les paramètres de l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Modifier les paramètres de l’interpréteur")
   
    Cliquez sur **enregistrer** , puis redémarrez hello interpréteur de Livy.
4. **Conseil**: Si vous souhaitez toounderstand comment tooarrive à la valeur de clé de hello d’hello entré ci-dessus, voici comment.
   
    a. Recherchez le package de hello Bonjour Maven référentiel. Dans ce didacticiel, nous avons utilisé [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. À partir de référentiel de hello, collectez les valeurs hello pour **GroupId**, **ArtifactId**, et **Version**.
   
    ![Utiliser des packages externes avec le bloc-notes Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Utiliser des packages externes avec le bloc-notes Jupyter")
   
    c. Concaténer des valeurs hello trois, séparés par un signe deux-points (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Où est hello blocs-notes Zeppelin enregistrées ?
ordinateurs portables de Hello Zeppelin sont enregistrés toohello cluster headnodes. Par conséquent, si vous supprimez le cluster de hello, les blocs-notes hello seront également supprimés. Si vous souhaitez toopreserve à vos blocs-notes et pour une utilisation ultérieure sur les autres clusters, vous devez les exporter une fois que vous avez terminé l’exécution des travaux de hello. tooexport un bloc-notes, cliquez sur hello **exporter** icône comme illustré dans l’image hello ci-dessous.

![Télécharger le bloc-notes](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "bloc-notes hello de téléchargement")

Cela enregistre bloc-notes de hello sous la forme d’un fichier JSON dans l’emplacement de téléchargement.

## <a name="livy-session-management"></a>Gestion des sessions Livy
Lorsque vous exécutez le premier paragraphe de code hello dans votre ordinateur portable Zeppelin, une nouvelle session Livy est créée dans votre cluster HDInsight Spark. Cette session est partagée par tous les blocs-notes Zeppelin que vous créerez par la suite. If pour certains hello raison Livy session est arrêtée (redémarrage de cluster, etc.), vous ne serez pas toorun en mesure des travaux à partir de l’ordinateur portable de Zeppelin hello.

Dans ce cas, vous devez effectuer hello comme suit avant de commencer l’exécution des travaux à partir d’un ordinateur portable Zeppelin. 

1. Redémarrez hello interpréteur Livy à partir de l’ordinateur portable de Zeppelin hello. toodo, ouvrez Paramètres de l’interpréteur en cliquant sur hello consigné dans le nom d’utilisateur à partir de l’angle supérieur droit de hello, puis cliquez sur **interpréteur**.
   
    ![Lancer l’interpréteur](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Sortie Hive")
2. Faites défiler les paramètres d’interpréteur tooLivy, puis cliquez sur **redémarrer**.
   
    ![Redémarrez hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "redémarrer hello Zeppelin intepreter")
3. Exécutez une cellule de code à partir d’un bloc-notes Zeppelin existant. Cette opération crée une nouvelle session Livy dans le cluster HDInsight de hello.

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
* [Utiliser le plug-in des outils HDInsight pour IntelliJ idée toocreate et soumettre des applications les plus importantes Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utiliser des plug-in des outils HDInsight pour les applications de Spark toodebug IntelliJ idée à distance](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Noyaux disponibles pour le bloc-notes Jupyter dans un cluster Spark pour HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Utiliser des packages externes avec les blocs-notes Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installer Notebook sur votre ordinateur et vous connecter tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestion des ressources
* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







