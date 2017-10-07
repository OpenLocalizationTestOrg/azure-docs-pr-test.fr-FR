---
title: "aaaSpark BI à l’aide des outils de visualisation des données sur Azure HDInsight | Documents Microsoft"
description: "Utiliser des outils de visualisation de données à des fins d’analyse à l’aide d’Apache Spark BI sur des clusters HDInsight"
keywords: "apache spark bi,spark bi,visualisation de données spark,décisionnel spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark BI utilisant des outils de visualisation de données avec Azure HDInsight

Découvrez comment visualisation des données toouse outils tels que Power BI et Tableau tooanalyze un jeu de données exemple brutes à l’aide d’Apache Spark BI sur les clusters HDInsight.

> [!NOTE]
> La connectivité avec les outils décisionnels décrite dans cet article n’est pas prise en charge sur Spark 2.1 avec Azure HDInsight 3.6 version préliminaire. Seules les versions Spark 1.6 et 2.0 (HDInsight 3.4, 3.5 respectivement) sont prises en charge.
>

Ce didacticiel est également disponible en tant que bloc-notes Jupyter sur un cluster Spark HDInsight. expérience de bloc-notes Hello vous permet d’exécuter des extraits de code hello Python à partir de l’ordinateur portable hello lui-même. didacticiel de hello tooperform à partir d’un ordinateur portable, créez un cluster Spark, lancer un bloc-notes jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), puis exécutez bloc-notes de hello **utiliser les Outils BI avec Apache Spark sur HDInsight.ipynb** sous hello **Python**  dossier.

## <a name="prerequisites"></a>Composants requis

* Un cluster Apache Spark sur HDInsight. Pour obtenir des instructions, consultez [Création de clusters Apache Spark dans Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Préparer les données pour la visualisation de données Spark

Dans cette section, nous utilisons hello [Notebook](https://jupyter.org) portable à partir d’un HDInsight Spark cluster toorun travaux traiter vos données d’exemple brut et l’enregistrer en tant que table. données d’exemple Hello sont un fichier .csv (hvac.csv) disponible sur tous les clusters par défaut. Une fois que vos données sont enregistrées en tant que table, dans la section suivante de hello nous utiliser BI outils tooconnect toohello table et d’effectuer des visualisations de données.

> [!NOTE]
> Si vous effectuez hello les étapes de cet article à la fin des instructions hello dans [exécuter des requêtes interactives sur un cluster HDInsight Spark](hdinsight-apache-spark-load-data-run-query.md), vous pouvez ignorer tooStep 8 ci-dessous.
>

1. À partir de hello [portail Azure](https://portal.azure.com/), à partir du tableau d’accueil hello, cliquez sur la vignette hello pour votre cluster Spark (si vous avez épinglé il toohello tableau d’accueil). Vous pouvez également naviguer cluster tooyour sous **parcourir tous les** > **Clusters HDInsight**.   

2. Dans le panneau de cluster Spark hello, cliquez sur **tableau de bord de Cluster**, puis cliquez sur **bloc-notes Jupyter**. Si vous y êtes invité, entrez les informations d’identification du admin de hello pour le cluster de hello.

   > [!NOTE]
   > Vous pouvez également atteindre hello bloc-notes Jupyter pour votre cluster en hello ouverture suivante d’URL dans votre navigateur. Remplacez **CLUSTERNAME** avec nom hello de votre cluster :
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Créez un bloc-notes. Cliquez sur **Nouveau**, puis sur **PySpark**.

    ![Créer un bloc-notes Jupyter pour Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Créer un bloc-notes Jupyter pour Apache Spark BI")

4. Un nouvel ordinateur portable est créé et ouvert avec le nom hello Untitled.pynb. Cliquez sur le nom du bloc-notes hello haut hello et entrez un nom convivial.

    ![Fournir un nom d’ordinateur portable de hello pour Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "fournir un nom d’ordinateur portable de hello pour Apache Spark BI")

5. Étant donné que vous avez créé un ordinateur portable à l’aide de noyau de PySpark hello, il est inutile toocreate les contextes explicitement. contextes de Spark et Hive Hello sont créées automatiquement pour vous lors de l’exécution de la première cellule de code hello. Vous pouvez commencer par importer les types hello requis pour ce scénario. toodo, placez le curseur de hello dans la cellule de hello et appuyez sur **MAJ + ENTRÉE**.

        from pyspark.sql import *

6. Chargez un exemple de données dans une table temporaire. Lorsque vous créez un cluster Spark dans HDInsight, le fichier de données d’exemple hello, **hvac.csv**, est le compte de stockage toohello copié associée sous **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    Dans une cellule vide, collez hello qui suit extrait de code, puis appuyez sur **MAJ + ENTRÉE**. Cet extrait de code enregistre les données de salutation dans une table appelée **hvac**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. Vérifiez que la table hello a été créée avec succès. Vous pouvez utiliser hello `%%sql` magique toorun ruche requêtes directement. Pour plus d’informations sur hello `%%sql` magique et autres magics disponibles avec le noyau de PySpark hello, consultez [noyaux disponibles sur les ordinateurs portables de Notebook avec clusters Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Vous verrez une sortie identique à celle ci-dessous :

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Hello uniquement les tables qui ont la valeur false sous hello **isTemporary** colonne sont des tables de ruche qui sont stockés dans le magasin de métadonnées hello et sont accessibles à partir des outils de BI hello. Dans ce didacticiel, nous connecter toohello **hvac** table, nous avons créé.

8. Vérifiez que hello cette table contient les données de salutation destinée. Dans une cellule vide dans le bloc-notes de hello, copiez hello extrait de code, puis appuyez sur **MAJ + ENTRÉE**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Arrêt des ressources de hello hello bloc-notes toorelease. toodo donc de hello **fichier** cliquez sur le menu d’un ordinateur portable hello, **fermer et s’arrêter**.

## <a name="powerbi"></a>Utiliser Power BI pour la visualisation de données Spark

> [!NOTE]
> Cette section s’applique uniquement à Spark 1.6 sur HDInsight 3.4 et Spark 2.0 sur HDInsight 3.5.
>
>

Une fois que vous avez enregistré les données de salutation sous forme de table, vous pouvez utiliser les données de Power BI tooconnect toohello et visualiser les rapports de toocreate, tableaux de bord, etc..

1. Assurez-vous que vous avez accès tooPower BI. Vous pouvez obtenir un abonnement gratuit à la version préliminaire de Power BI à l’adresse [http://www.powerbi.com/](http://www.powerbi.com/).

2. Connectez-vous trop[Power BI](http://www.powerbi.com/).

3. À partir du bas hello du volet gauche de hello, cliquez sur **obtenir des données**.

4. Sur hello **obtenir des données** sous **importer ou se connecter tooData**, pour **bases de données**, cliquez sur **obtenir**.

    ![Obtenir des données dans Power BI pour Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Obtenir des données dans Power BI pour Apache Spark BI")

5. Dans l’écran suivant de hello, cliquez sur **Spark sur Azure HDInsight** puis cliquez sur **connexion**. Lorsque vous y êtes invité, entrez l’URL du cluster hello (`mysparkcluster.azurehdinsight.net`) et le cluster de toohello tooconnect hello informations d’identification.

    ![Se connecter tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "connecter tooApache Spark BI")

    Une fois hello est établie, Power BI démarre l’importation de données à partir du cluster de Spark hello sur HDInsight.

6. Power BI importe les données de hello et ajoute un **Spark** dataset sous hello **Datasets** titre. Cliquez sur le jeu de données de hello tooopen les données de salutation une nouvelle feuille de calcul toovisualize. Vous pouvez également enregistrer la feuille de calcul hello sous forme de rapport. toosave une feuille de calcul, à partir de hello **fichier** menu, cliquez sur **enregistrer**.

    ![Vignette Apache Spark BI sur le tableau de bord Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Vignette Apache Spark BI sur le tableau de bord Power BI")
7. Notez que hello **champs** liste sur hello droite répertorie hello **hvac** table que vous avez créé précédemment. Développez les champs de hello hello table toosee dans la table de hello, définie précédemment dans le bloc-notes.

      ![épertorier des tables sur le tableau de bord Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "épertorier des tables sur le tableau de bord Apache Spark BI")

8. Générer une variation de hello visualisation tooshow entre la température de cible et de température réelle pour chaque génération. toovisualize habituelle de données, sélectionnez **graphique en aires** (illustrée dans la zone rouge). axe de hello toodefine, glisser-déposer hello **BuildingID** champ sous **axe**, et **ActualTemp**/**TargetTemp** les champs sous **valeur**.

    ![Créer des visualisations de données Spark à l’aide d’Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Créer des visualisations de données Spark à l’aide d’Apache Spark BI")

9. Par défaut, visualisation de hello affiche sum hello pour **ActualTemp** et **TargetTemp**. Pour les deux hello champs hello liste déroulante, sélectionnez **moyenne** tooget moyenne réelle et températures cible pour les deux bâtiments.

    ![Créer des visualisations de données Spark à l’aide d’Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Créer des visualisations de données Spark à l’aide d’Apache Spark BI")

10. La visualisation de données doit être similaire toohello une capture d’écran hello. Déplacez votre curseur sur hello visualisation tooget info-bulles avec les données appropriées.

    ![Créer des visualisations de données Spark à l’aide d’Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Créer des visualisations de données Spark à l’aide d’Apache Spark BI")

11. Cliquez sur **enregistrer** de hello premiers menu et fournissez un nom de rapport. Vous pouvez également épingler hello visual. Quand vous épinglez une visualisation, celle-ci est stockée dans votre tableau de bord afin de pouvoir suivre la valeur la plus récente hello en un coup de œil.

   Vous pouvez ajouter autant de visualisations que vous le souhaitez pour hello même jeu de données et les épingler toohello du tableau de bord pour un instantané de vos données. En outre, clusters Spark sur HDInsight sont connecté tooPower BI avec direct de se connecter. Cela garantit que Power BI toujours a hello la plupart des données à jour à partir de votre cluster vous n’avez pas besoin des actualisations tooschedule pour hello le jeu de données.

## <a name="tableau"></a>Utiliser Tableau Desktop pour la visualisation de données Spark

> [!NOTE]
> Cette section s’applique uniquement aux clusters Spark 1.5.2 créés dans Azure HDInsight.
>
>

1. Installer [Tableau bureau](http://www.tableau.com/products/desktop) sur l’ordinateur qui exécute ce didacticiel d’Apache Spark BI hello.

2. Vérifiez que l’ordinateur est également équipé du pilote ODBC de Microsoft Spark. Vous pouvez installer le pilote hello [ici](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Lancez Tableau Desktop. Dans le volet gauche hello, à partir de la liste hello de tooconnect de serveur, cliquez sur **Spark SQL**. Si Spark SQL n’est pas répertoriée par défaut dans le volet gauche de hello, vous le trouverez par clic **plus de serveurs**.
2. Dans la boîte de dialogue Connexion hello Spark SQL, fournir des valeurs de hello comme indiqué dans la capture d’écran de hello, puis cliquez sur **OK**.

    ![Cluster tooa de se connecter pour Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "cluster tooa de se connecter pour Apache Spark BI")

    Hello des listes déroulantes de l’authentification **Service Microsoft Azure HDInsight** en option, si vous avez installé hello [Microsoft Spark ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=616229) sur l’ordinateur de hello.
3. Sur l’écran suivant de hello, à partir de hello **schéma** liste déroulante, cliquez sur hello **trouver** icône, puis cliquez sur **par défaut**.

    ![Rechercher un schéma pour Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Rechercher un schéma pour Apache Spark BI")
4. Pourquoi **Table** , cliquez sur hello **trouver** icône Nouveau toolist tous hello Hive tables disponibles dans le cluster de hello. Vous devez voir hello **hvac** table que vous avez créé précédemment à l’aide du bloc-notes de hello.

    ![Rechercher un tableau pour Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Rechercher un tableau pour Apache Spark BI")
5. Glisser-déplacer la zone supérieure toohello table hello sur hello droite. Tableau importe les données de hello et affiche le schéma de hello mise en évidence par zone de hello rouge.

    ![Ajouter des tables tooTableau Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "ajouter des tables tooTableau Apache Spark BI")
6. Cliquez sur hello **Feuil1** onglet en bas à gauche hello. Rendre une visualisation qui montre cible moyenne de hello et températures réelles pour tous les bâtiments pour chaque date. Faites glisser **Date** et **ID de génération** trop**colonnes** et **Temp réel**/**cible Temp**trop**lignes**. Sous **marques**, sélectionnez **zone** toouse une carte pour la visualisation des données Spark.

     ![Ajouter des champs pour une visualisation de données Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Ajouter des champs pour une visualisation de données Spark")
7. Par défaut, les champs de température hello sont affichés en tant qu’agrégat. Si vous souhaitez températures moyennes de hello tooshow au lieu de cela, vous pouvez le faire à partir de déroulante hello, comme indiqué ci-dessous.

    ![Prendre une moyenne de températures pour une visualisation de données Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Prendre une moyenne de températures pour une visualisation de données Spark")

8. Vous pouvez également super-imposer un mappage de température plus hello autres tooget mieux comprendre de différence entre la cible et les températures réels. Déplacer le coin de toohello hello souris de carte hello inférieur jusqu'à ce que vous voyez hello forme du handle mis en surbrillance dans un cercle rouge. Faites glisser hello carte toohello autre classe map hello haut et version hello de la souris lorsque vous voyez forme hello mis en surbrillance dans le rectangle rouge.

    ![Fusionner des cartes pour une visualisation de données Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Fusionner des cartes pour une visualisation de données Spark")

     La visualisation de données doit modifier comme indiqué dans la capture d’écran de hello :

    ![Sortie de tableau pour une visualisation de données Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Sortie de tableau pour une visualisation de données Spark")
9. Cliquez sur **enregistrer** feuille de calcul toosave hello. Vous pouvez créer des tableaux de bord et ajouter un ou plusieurs tooit de feuilles.

## <a name="next-steps"></a>Étapes suivantes

Jusqu'à présent, vous avez appris comment toocreate un cluster, créer Spark frames tooquery de données et puis accéder à ces données à partir d’outils BI. Vous pouvez maintenant consulter plus d’informations sur comment toomanage hello des ressources de cluster et déboguer des tâches qui s’exécutent dans un cluster HDInsight Spark.

* [Gérer les ressources de cluster d’Apache Spark hello dans Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Track and debug jobs running on an Apache Spark cluster in HDInsight (Suivi et débogage des tâches en cours d’exécution sur un cluster Apache Spark dans HDInsight)](hdinsight-apache-spark-job-debugging.md)

