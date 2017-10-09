---
title: "aaaRun des requêtes interactives sur un cluster Azure HDInsight Spark | Documents Microsoft"
description: "Démarrage rapide de HDInsight Spark sur comment toocreate un Apache Spark dans HDInsight de cluster."
keywords: "démarrage rapide spark,spark interactif,requête interactive,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Exécuter des requêtes interactives sur un cluster HDInsight Spark

Dans cet article, vous utilisez un notebook bloc-notes toorun interactive Spark des requêtes SQL sur un cluster Spark. Bloc-notes jupyter est une application basée sur navigateur qui s’étend hello sur la console d’interactivité toohello Web. Pour plus d’informations, consultez [bloc-notes jupyter de hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Pour ce didacticiel, vous utilisez hello **PySpark** noyau dans hello Notebook bloc-notes toorun une requête de Spark SQL interactive. Les blocs-notes Jupython des clusters HDInsight prennent également en charge deux autres noyaux - **PySpark3** et **Spark**. Pour plus d’informations sur les noyaux hello et hello les avantages de l’utilisation de **PySpark**, consultez [des clusters de noyaux de bloc-notes utilisez Notebook avec Apache Spark dans HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Composants requis

* **Un cluster Azure HDInsight Spark**. Pour obtenir des instructions, consultez [Créer un cluster Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Créer un bloc-notes jupyter toorun des requêtes interactives

toorun requêtes, nous utilisons des exemples de données qui est par défaut disponible dans le stockage hello associé hello cluster. Toutefois, vous devez d’abord charger ces données dans Spark comme une trame de données. Une fois que vous avez hello trame de données, vous pouvez exécuter des requêtes sur ce dernier à l’aide du bloc-notes jupyter de hello. Dans cette section, vous examinez comment :

* Enregistrer un jeu d’exemple données comme une trame de données Spark.
* Exécuter des requêtes sur la trame de données hello.

1. Ouvrez hello [portail Azure](https://portal.azure.com/). Si vous avez choisi de tableau de bord toohello toopin hello cluster, cliquez sur hello en mosaïque de cluster à partir du Panneau de cluster hello du tableau de bord toolaunch hello.

    Si vous ne pas épinglez hello cluster toohello du tableau de bord, à partir du volet de gauche hello, cliquez sur **clusters HDInsight**, puis cliquez sur cluster hello vous avez créé.

3. À partir de **Liens rapides**, cliquez sur **Tableaux de bord de Cluster**, puis sur **Bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

   ![Ouvrez Notebook bloc-notes toorun interactive Spark requête SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "la requête interactive Spark SQL Notebook ouvrir Bloc-notes toorun")

   > [!NOTE]
   > Vous pouvez également accéder bloc-notes jupyter de hello pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Créez un bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.

   ![Créer une requête de Spark SQL interactive Notebook bloc-notes toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "créer une requête de Spark SQL Notebook bloc-notes toorun interactive")

   Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled(Untitled.pynb).

4. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial, si vous le souhaitez.

    ![Fournissez un nom pour hello Jupter bloc-notes toorun Spark requêtes interactif de](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "fournir un nom pour hello Jupter bloc-notes toorun interactive Spark requête à partir de")

5. Suit hello de coller le code dans une cellule vide, puis appuyez sur **MAJ + ENTRÉE** code hello de toorun. code de Hello importe des types hello requis pour ce scénario :

        from pyspark.sql.types import *

    Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement. contextes de Spark et Hive Hello sont créées automatiquement pour vous lors de l’exécution de la première cellule de code hello.

    ![État de la requête interactive Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "État de la requête interactive Spark SQL")

    Chaque fois que vous exécutez une requête interactive dans le bloc-notes, le titre de la fenêtre de navigateur web affiche un **(occupé)** état, ainsi que le titre du bloc-notes hello. Vous voyez également un toohello suivant cercle plein **PySpark** texte dans l’angle supérieur droit de hello. Une fois le travail de hello est terminé, il modifie tooa les cercle vide.

6. Avant de charger les données de salutation dans un cluster Spark, nous permettent de rechercher un instantané de celui-ci. Hello exemples de données utilisés dans ce didacticiel sont disponibles dans un fichier CSV sur tous les clusters HDInsight Spark à **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. les données de salutation capture les variations de température hello de bâtiment. Voici hello premières lignes de données de hello.

    ![Instantané des données pour les requêtes Spark SQL interactives](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "instantané des données pour les requêtes Spark SQL interactives")

6. Créer une trame de données et une table temporaire (**hvac**) en exécutant hello suivant de code. Pour ce didacticiel, nous ne créez pas toutes les colonnes hello dans la table temporaire de hello en tant que colonnes comparées toohello dans des données CSV brutes hello. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Une fois que la table de hello est créée, exécuter des requêtes interactives sur les données de hello, utilisez hello suivant de code.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Étant donné que vous utilisez un noyau PySpark, vous pouvez maintenant directement exécuter une requête SQL interactive sur une table temporaire de hello **hvac** que vous avez créé à l’aide de hello `%%sql` magique. Pour plus d’informations sur hello `%%sql` magique et autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Hello suivant sortie tabulaire est affiché par défaut.

     ![Sortie sous forme de tableau d’un résultat de requête interactive Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Sortie sous forme de tableau d’un résultat de requête interactive Spark")

    Vous pouvez également afficher les résultats de hello dans les autres visualisations. Par exemple, un graphique en aires pour hello même sortie se présente comme suit de hello.

    ![Résultat de requête interactive Spark sous forme graphique](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Résultat de requête interactive Spark sous forme graphique")

9. Arrêt des ressources de cluster hello hello bloc-notes toorelease une fois que vous avez terminé d’exécuter l’application hello. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.

## <a name="next-step"></a>Étape suivante

Dans cet article vous avez appris comment utiliser des requêtes interactives toorun dans Spark à l’aide du bloc-notes jupyter. Avance suivant toosee article toohello, comment les données de salutation que vous avez enregistré dans Spark peuvent être extraites dans un outil analytique de BI telles que Power BI et de Tableau. 

> [!div class="nextstepaction"]
>[Spark BI utilisant des outils de visualisation de données avec Azure HDInsight](hdinsight-apache-spark-use-bi-tools.md)




