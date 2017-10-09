---
title: "aaaUse données de tooanalyze Apache Spark dans Azure Data Lake Store | Documents Microsoft"
description: "Exécuter des travaux de Spark tooanalyze les données stockées dans Azure Data Lake Store"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Utiliser des données tooanalyze du cluster HDInsight Spark dans Data Lake Store

Dans ce didacticiel, vous utilisez bloc-notes jupyter disponible avec HDInsight Spark clusters toorun une tâche qui lit des données à partir d’un compte Data Lake Store.

## <a name="prerequisites"></a>Composants requis

* Compte Azure Data Lake Store. Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).

* Cluster Azure HDInsight Spark avec Data Lake Store comme système de stockage. Suivez les instructions de hello à [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Préparer les données de salutation

> [!NOTE]
> Il est inutile tooperform cette étape si vous avez créé le cluster HDInsight de hello avec Data Lake Store en tant que stockage de la valeur par défaut. processus de création de cluster Hello ajoute quelques exemples de données dans le compte Data Lake Store hello que vous spécifiez lors de la création du cluster de hello. Ignorer la section de toohello [cluster utilisez HDInsight Spark avec Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Si vous avez créé un cluster HDInsight avec Data Lake Store en tant qu’objet Blob de stockage Azure en tant que stockage par défaut et de stockage supplémentaire, vous devez tout d’abord copier sur certaines toohello de données exemple compte Data Lake Store. Vous pouvez utiliser les exemples de données hello de hello qu'objet Blob de stockage Azure associée au cluster HDInsight de hello. Vous pouvez utiliser hello [ADLCopy outil](http://aka.ms/downloadadlcopy) toodo donc. Téléchargez et installez l’outil de hello à partir du lien de hello.

1. Ouvrez une invite de commandes et accédez répertoire toohello où AdlCopy est installé, généralement `%HOMEPATH%\Documents\adlcopy`.

2. Exécutez hello suivant commande toocopy un blob spécifique de hello source conteneur tooa Data Lake Store :

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Hello de copie **HVAC.csv** exemples de données de fichiers au **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello compte Azure Data Lake Store. extrait de code Hello doit ressembler à :

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Vérifiez que hello de fichier et les noms de chemin d’accès sont en majuscules de hello.
   >
   >
3. Vous serez invité à tooenter informations d’identification hello pour hello abonnement Azure sous lequel vous avez à votre compte Data Lake Store. Vous découvrez une sortie similaire toohello :

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    fichier de données Hello (**HVAC.csv**) doivent être copiées dans un dossier **/hvac** Bonjour compte Data Lake Store.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Utiliser un cluster HDInsight Spark avec Data Lake Store

1. À partir de hello [Azure Portal](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.

2. Dans le panneau de cluster Spark hello, cliquez sur **liens rapides**, puis à partir de hello **tableau de bord de Cluster** panneau, cliquez sur **bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

   > [!NOTE]
   > Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Créer un nouveau bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.

    ![Créer un bloc-notes Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Créer un bloc-notes Jupyter")

4. Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement. contextes de Spark et Hive Hello seront automatiquement créés pour vous lors de l’exécution de la première cellule de code hello. Vous pouvez commencer par importer les types hello requis pour ce scénario. toodo coller donc hello suivant extrait de code dans une cellule appuyez sur **MAJ + ENTRÉE**.

        from pyspark.sql.types import *

    Chaque fois que vous exécutez une tâche dans le bloc-notes, titre de la fenêtre de navigateur web affichera un **(occupé)** état, ainsi que le titre du bloc-notes hello. Vous verrez également une toohello suivant cercle plein **PySpark** texte dans l’angle supérieur droit de hello. Une fois le travail de hello est terminé, cela modifiera le cercle vide de tooa.

     ![État d’une tâche de bloc-notes Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "État d’une tâche de bloc-notes Jupyter")

5. Charger des exemples de données dans une table temporaire à l’aide de hello **HVAC.csv** fichier que vous avez copié le compte Data Lake Store de toohello. Vous pouvez accéder aux hello hello Data Lake Store nom du compte hello suivant le modèle d’URL.

    * Si vous avez Data Lake Store en tant que stockage par défaut, HVAC.csv sera à toohello similaire de hello chemin d’accès suivant l’URL :

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        Ou bien, vous pouvez également utiliser un format raccourci tel que suivant de hello :

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Si vous avez Data Lake Store en tant que stockage supplémentaire, HVAC.csv sera à hello emplacement où vous avez copié, telles que :

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     Dans une cellule vide, hello coller suivant l’exemple de code, remplacez **MYDATALAKESTORE** avec votre nom de compte Data Lake Store, puis appuyez sur **MAJ + ENTRÉE**. Cet exemple de code enregistre les données de salutation dans une table temporaire nommée **hvac**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Étant donné que vous utilisez un noyau PySpark, vous pouvez maintenant directement exécuter une requête SQL sur une table temporaire de hello **hvac** que vous venez de créer à l’aide de hello `%%sql` magique. Pour plus d’informations sur hello `%%sql` magic, ainsi que d’autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Une fois que hello tâche terminée avec succès, hello suivant sortie tabulaire est affiché par défaut.

      ![Table de sortie des résultats de la requête](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Table de sortie des résultats de la requête")

     Vous pouvez également afficher les résultats de hello dans les autres visualisations. Par exemple, un graphique en aires pour hello même sortie se présente comme suit de hello.

     ![Graphique en aires des résultats de la requête](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Graphique en aires des résultats de la requête")

8. Une fois que vous avez terminé d’exécuter l’application hello, vous devez le ressources hello toorelease arrêt hello bloc-notes. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**. Cette s’arrête et le bloc-notes de fermer hello.


## <a name="next-steps"></a>Étapes suivantes

* [Créer un toorun d’application de Scala autonome sur un cluster d’Apache Spark](hdinsight-apache-spark-create-standalone-application.md)
* [Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications Spark cluster HDInsight Spark Linux IntelliJ toocreate](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilisez les outils HDInsight dans la boîte à outils Azure pour les applications de Spark toocreate Eclipse pour le cluster HDInsight Spark Linux](hdinsight-apache-spark-eclipse-tool-plugin.md)
