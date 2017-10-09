---
title: "Hello processus de science des données équipe en action - à l’aide d’un Cluster de Hadoop HDInsight Azure sur un jeu de données de 1 to | Documents Microsoft"
description: "À l’aide de hello équipe données science des processus pour un scénario de bout en bout utilisant un HDInsight Hadoop toobuild de cluster et déployer un modèle à l’aide d’un jeu de données disponible publiquement (1 To) volumineux"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Hello processus de science des données équipe en action - à l’aide d’un Cluster de Hadoop HDInsight Azure sur un jeu de données de 1 to

Dans cette procédure pas à pas, nous allons montrer à l’aide de hello du processus de science des données équipe dans un scénario de bout en bout avec un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Explorer, ingénieur de fonctionnalité et vers le bas des exemples de données à partir d’un des hello publiquement disponible [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) jeux de données. Nous utilisons Azure Machine Learning toobuild un modèle de classification binaire sur ces données. Nous montrons également comment toopublish un de ces modèles comme un service Web.

Il est également possible de toouse un tâches de hello notebooks bloc-notes tooaccomplish présentées dans cette procédure pas à pas. Les utilisateurs qui seraient comme tootry cette approche doit consulter hello [procédure pas à pas Criteo à l’aide d’une connexion ODBC de la ruche](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) rubrique.

## <a name="dataset"></a>Description du groupe de données Criteo
Hello Criteo de données sont un jeu de données de prédiction cliquez qui est d’environ 370 Go de gzip compressées des fichiers TSV (~1.3TB non compressé), qui comprend plus de 4.3 milliards d’enregistrements. Elles proviennent de 24 jours de données de clic, disponibles via [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Pour plus de commodité hello de chercheurs de données, nous avons décompressé tooexperiment toous de données disponibles avec.

Chaque enregistrement de ce groupe de données est constitué de 40 colonnes :

* Hello première colonne est une colonne d’étiquette qui indique si un utilisateur clique sur un **ajouter** (valeur 1) ou ne cliquez pas sur un (valeur 0)
* Les 13 colonnes suivantes sont numériques, et
* les 26 dernières sont des colonnes catégorielles

colonnes de Hello sont rendues anonymes et utiliser une série de noms énumérés : « Col1 » (pour la colonne d’étiquette hello) trop ' Col40 » (pour la dernière colonne catégorielle hello).            

Voici un extrait de hello tout d’abord 20 colonnes des deux observations (lignes) à partir de ce jeu de données :

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Il existe des valeurs manquantes dans les deux colonnes numériques et par catégorie de hello dans ce jeu de données. Nous décrivons une méthode simple pour la gestion des valeurs manquantes de hello. Des détails supplémentaires de données de hello sont explorées lorsque nous les stocker dans les tables de la ruche.

**Définition :** *taux de clic (CTR) :* il s’agit pourcentage hello clics dans les données de salutation. Dans ce jeu de données Criteo, hello CTR est environ 3.3 % ou 0.033.

## <a name="mltasks"></a>Exemples de tâches de prédiction
Cette procédure pas à pas aborde deux exemples de problèmes de prédiction :

1. **Classification binaire**: prédit si un utilisateur a cliqué ou non sur un ajout :
   
   * Classe 0 : aucun clic
   * Classe 1 : clic
2. **Régression**: prédit la probabilité de hello d’une annonce, cliquez sur à partir des fonctionnalités de l’utilisateur.

## <a name="setup"></a>Configuration d’un cluster Hadoop HDInsight pour la science des données
**Remarque** : il s’agit généralement d’une tâche d’**administration**.

Configurez votre environnement de science des données Azure pour créer des solutions d'analyse prédictives avec les clusters HDInsight en trois étapes :

1. [Créer un compte de stockage](../storage/common/storage-create-storage-account.md): ce compte de stockage est données toostore utilisé dans le stockage d’objets Blob Azure. données Hello utilisées dans les clusters HDInsight sont stockées ici.
2. [Personnalisation des clusters Hadoop Azure HDInsight pour la science des données](machine-learning-data-science-customize-hadoop-cluster.md): cette étape crée un cluster Hadoop Azure HDInsight avec Anaconda Python 2.7 64 bits installé sur tous les nœuds. Il existe deux étapes importantes (décrites dans cette rubrique) toocomplete lors de la personnalisation du cluster HDInsight de hello.
   
   * Vous devez lier le compte de stockage hello créé à l’étape 1 avec votre cluster HDInsight lors de sa création. Ce compte de stockage est utilisé pour accéder aux données qui peuvent être traitées au sein du cluster de hello.
   * Vous devez activer l’accès à distance toohello nœud de tête hello cluster après sa création. N’oubliez pas d’informations d’identification de l’accès à distance hello vous spécifiez ici (différents de ceux spécifiés pour le cluster hello lors de sa création) : vous avez besoin toocomplete hello les procédures ci-après.
3. [Créer un espace de travail Azure ML](machine-learning-create-workspace.md): ce Azure Machine Learning un espace de travail est utilisé pour créer des modèles d’apprentissage automatique après une exploration de données initiales et vers le bas d’échantillonnage sur le cluster HDInsight de hello.

## <a name="getdata"></a>Récupération et utilisation des données provenant d’une source publique
Hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) jeu de données est accessible en cliquant sur le lien de hello, accepter les conditions d’utilisation de hello, en fournissant un nom. Voici une capture de l’écran correspondant :

![Accepter les conditions de Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Cliquez sur **continuer tooDownload** tooread plus d’informations sur le jeu de données hello et sa disponibilité.

les données de salutation résident dans un public [stockage d’objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) emplacement : wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Hello « wasb » désigne l’emplacement de stockage d’objets Blob tooAzure. 

1. données Hello dans le stockage de l’objet blob public se comprennent de trois sous-dossiers de données décompressées.
   
   1. Hello sous-dossier *brut/count/* contient hello première 21 jours de données, à partir du jour\_tooday 00\_20
   2. Hello sous-dossier *brut/train/* se compose d’un seul jour de données, jour\_21
   3. Hello sous-dossier *brut/test/* se compose de deux jours de données, jour\_22 et jour\_23
2. Pour ceux qui souhaitent toostart avec des données brutes gzip hello, elles sont également disponibles dans le dossier principal de hello *brut /* comme day_NN.gz, où NN s’étende de too23 00.

Une autre approche tooaccess, Explorer et modèle de données qui ne nécessitent pas les téléchargements locales est expliquée plus loin dans cette procédure pas à pas, quand vous créez des tables de la ruche.

## <a name="login"></a>Connectez-vous au nœud principal de cluster toohello
toolog dans le nœud principal de toohello du cluster hello, utilisez hello [portail Azure](https://ms.portal.azure.com) cluster hello de toolocate. Cliquez sur hello HDInsight éléphant icône sur hello gauche, puis sur nom hello de votre cluster. Accédez toohello **Configuration** onglet, double-cliquez sur icône de connexion hello bas hello de page de hello et entrez vos informations d’identification de l’accès à distance lorsque vous y êtes invité. Cela vous prend un nœud principal de toohello du cluster de hello.

Un premier journal dans le nœud principal du cluster toohello classique ressemble à ceci :

![Connectez-vous à toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Sur la gauche de hello, nous constatons hello « Hadoop ligne de commande », qui est notre exploration de données hello. De même que deux URL : « État Yarn Hadoop » et « Nœud de nom Hadoop ». URL d’état Hello fils montre la progression du travail et URL de nom de nœud hello donne des détails sur la configuration de cluster hello.

Maintenant nous sont configurés et prêts toobegin première partie de la procédure pas à pas hello : exploration de données à l’aide de la ruche et la préparation des données pour l’apprentissage d’Azure.

## <a name="hive-db-tables"></a> Création de la base de données et des tables Hive
toocreate ruche tables pour notre jeu de données Criteo, ouvrez hello ***ligne de commande Hadoop*** hello bureau du nœud principal de hello et entrez le répertoire de ruche hello en entrant la commande hello

    cd %hive_home%\bin

> [!NOTE]
> Exécuter toutes les commandes de la ruche dans cette procédure pas à pas d’emplacement de ruche hello / invite du répertoire. Tout problème lié au chemin d’accès sera résolu automatiquement. Nous utilisons hello termes « Invite du répertoire ruche », « ruche bin / invite du répertoire » et « ligne de commande Hadoop » indifféremment.
> 
> [!NOTE]
> tooexecute une requête Hive, toujours utiliser hello suivant de commandes :
> 
> 

        cd %hive_home%\bin
        hive

Après hello ruche REPL s’affiche avec un « ruche > « Connectez-vous simplement couper et coller hello requête tooexecute il.

Hello de code suivant crée une base de données « criteo » et génère ensuite les 4 tables :

* un *table pour la génération de nombres* reposant sur un jour de jours\_tooday 00\_20,
* un *de table pour une utilisation comme hello train dataset* reposant sur jour\_21, et
* deux *jeux de données de test de tables pour une utilisation en tant que hello* reposant sur jour\_22 et jour\_23 respectivement.

Fractionnées notre jeu de données de test dans deux tables différentes, car un des jours de hello est un jour férié, et nous souhaitons toodetermine si le modèle de hello peut détecter les différences entre un jour férié et non à partir du taux de clics hello.

Hello script [exemple &#95; ruche & &#95; ; créer &#95; criteo &#95; base de données &#95; et &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) s’affiche ici pour des raisons pratiques :

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Nous Notez que toutes ces tables sont externes que nous avons simplement les emplacements de stockage d’objets Blob (wasb) tooAzure de point.

**Il existe deux façons tooexecute Hive n’importe quelle requête que nous avons maintenant.**

1. **À l’aide de hello REPL ruche de ligne de commande**: hello tout d’abord est tooissue une « ruche » une commande et les copier et coller une requête à hello REPL ruche de ligne de commande. toodo ce, procédez comme :
   
        cd %hive_home%\bin
        hive
   
     Maintenant à hello REPL de ligne de commande, telles que couper et coller les requêtes hello l’exécute.
2. **L’enregistrement des requêtes tooa fichier et l’exécution de commande hello**: hello est ensuite le fichier .hql tooa toosave hello requêtes ([exemple &#95; ruche & &#95; ; créer &#95; criteo &#95; base de données &#95; et &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) et puis suivant de hello problème des commandes query de hello tooexecute :
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Confirmation de la création de la base de données et des tables
Ensuite, nous confirmer la création de hello de base de données hello avec la commande suivante à partir de l’emplacement de ruche hello de hello / invite du répertoire :

        hive -e "show databases;"

Cela donne :

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Cela permet de confirmer la création de hello de hello nouvelle base de données « criteo ».

toosee les tables créées, nous tapez hello commande ici à partir de l’emplacement de ruche hello / invite du répertoire :

        hive -e "show tables in criteo;"

Ensuite, nous voyons hello suivant de sortie :

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> Exploration des données dans Hive
Est maintenant prêt à toodo une exploration de données de base de données dans la ruche. Nous commencer en comptant le nombre de hello d’exemples de formation de hello et tables de données de test.

### <a name="number-of-train-examples"></a>Nombre d'exemples de formation
Hello le contenu de [exemple &#95; ruche &#95; nombre &#95; train &#95; table &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) sont indiquées ici :

        SELECT COUNT(*) FROM criteo.criteo_train;

Cela donne :

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

Vous pouvez également une peut également émettre hello de commande suivante à partir de l’emplacement de ruche hello / invite du répertoire :

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Nombre d’exemples de test dans les jeux de données de test hello deux
Nous avons maintenant nombre hello d’exemples de jeux de données de test deux hello. Hello le contenu de [exemple &#95; ruche &#95; nombre &#95; criteo &#95; test &#95; jour &#95; 22 &#95; table &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) sont ici :

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Cela donne :

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Comme d’habitude, nous pouvons également appeler le script de hello à partir de l’emplacement de ruche hello / directory invite en émettant la commande hello :

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Enfin, nous examinons nombre hello des exemples de test dans le jeu de données de test hello selon le jour\_23.

Hello commande toodo cela est similaire toohello une juste affichée (consultez trop[exemple &#95; ruche &#95; nombre &#95; criteo &#95; test &#95; jour &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)) :

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Cela donne :

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Distribution d’étiquette dans le jeu de données de formation hello
distribution d’étiquette Hello hello train DataSet présente un intérêt. toosee, afficher le contenu de [exemple &#95; ruche &#95; criteo &#95; étiquette &#95; distribution &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Cela donne la distribution d’étiquette hello :

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Notez que le pourcentage de hello d’étiquettes positifs est 3.3 % environ (cohérent avec le jeu de données d’origine hello).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Distributions histogramme de certaines variables numériques Bonjour former le jeu de données
Nous pouvons utiliser natif de la ruche du « histogramme\_numérique « toofind out quelles distribution hello des variables numériques de hello ressemble de fonction. Voici le contenu de hello de [exemple &#95; ruche &#95; criteo &#95; histogramme &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Cela donne le résultat suivant de hello :

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Hello latéral affichage - éclater combinaison dans la ruche sert tooproduce une sortie de type SQL au lieu de la liste de habituel hello. Notez que dans hello cette table, la première colonne de hello correspond toohello bin centre et hello deuxième toohello bin fréquence.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Centiles approximatives de certaines variables numériques Bonjour former le jeu de données
Est également un calcul hello des centiles approximatifs d’intérêt avec des variables numériques. Le « percentile\_approx» natif de Hive le fait pour nous. Hello le contenu de [exemple &#95; ruche &#95; criteo &#95; approximative &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) sont :

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Cela donne :

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Il remarque que distribution hello de centiles est généralement la distribution d’histogramme toohello étroitement liées d’une variable numérique.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Rechercher le nombre de valeurs uniques pour certaines colonnes catégorielles dans le jeu de données de formation hello
Poursuite de l’exploration de données hello, nous trouver maintenant, pour certaines colonnes catégorielles, nombre hello de valeurs uniques qu’ils prennent. toodo, afficher le contenu de [exemple &#95; ruche &#95; criteo &#95; unique &#95; valeurs &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Cela donne :

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Nous constatons que Col15 possède des valeurs uniques 19M ! Ces variables catégorielles de grande dimension à l’aide de techniques naïve comme « à chaud un codage » de tooencode est impossible. Nous mentionnons notamment une technique puissante et robuste appelée [Apprentissage à l’aide de compteurs](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) pour résoudre ce problème de manière efficace.

Nous terminer cette sous-section en examinant le nombre de hello de valeurs uniques pour d’autres colonnes catégorielles également. Hello le contenu de [exemple &#95; ruche &#95; criteo &#95; unique &#95; valeurs &#95; plusieurs &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) sont :

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Cela donne :

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Là encore, nous voyons que, à l’exception de Col20, tous les hello autres colonnes ont de nombreuses valeurs uniques.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Nombres d’occurrence des paires de variables catégorielles dans hello former le jeu de données

nombre de coordonnées occurrence Hello de paires de variables catégorielles est également intéressant. Cela peut être déterminé à l’aide de code hello dans [exemple &#95; ruche &#95; criteo &#95; appariés &#95; catégorielles &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Nous inverser l’ordre hello nombres par leur occurrence et haut hello 15 dans ce cas. Cela nous donne :

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Jeux de données exemple hello pour Azure Machine Learning vers le bas
Ayant des jeux de données explorées hello et illustré comment nous pouvons faire de ce type d’exploration des variables (y compris les combinaisons), nous avons maintenant vers le bas de jeux de données exemple hello afin que nous pouvons créer des modèles dans Azure Machine Learning. Rappelez-vous ce problème hello nous concentrer sur est : étant donné un ensemble d’attributs de l’exemple (valeurs de fonctionnalités à partir de Col2 - Col40), nous pour prédire si Col1 est égal à 0 (aucun clic) ou 1 (clic).

toodown exemples de notre apprentissage et de test % too1 de jeux de données de taille d’origine de hello, nous utilisons la fonction RAND() native de la ruche. Hello au script suivant, [exemple &#95; ruche &#95; criteo &#95; sous-échantillonner &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) effectue cette opération pour le jeu de données de formation hello :

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Cela donne :

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Hello script [exemple &#95; ruche &#95; criteo &#95; sous-échantillonner &#95; test &#95; jour &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) le fait pour les données de test, jour\_22 :

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Cela donne :

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Enfin, hello script [exemple &#95; ruche &#95; criteo &#95; sous-échantillonner &#95; test &#95; jour &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) le fait pour les données de test, jour\_23 :

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Cela donne :

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Cette opération, nous sommes prêt toouse notre bas échantillonné former et tester des jeux de données pour générer des modèles dans Azure Machine Learning.

Est un composant important final avant nous consacrerons tooAzure Machine Learning, qui est une table de nombres préoccupations hello. Dans hello suivante sous-section, nous reviendrons en détail.

## <a name="count"></a>Une brève description de la table de nombres hello
Comme nous avons pu le remarquer, plusieurs variables catégorielles ont une dimensionnalité très élevée. Dans notre procédure pas à pas, nous vous présentons une technique puissante appelée [Learning avec compte](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode ces variables de manière efficace et fiable. Plus d’informations sur cette technique est dans le lien hello fourni.

[!NOTE]
>Dans cette procédure pas à pas, nous concentrer sur l’utilisation de count tables tooproduce compact représentations sous forme de grande dimension fonctionnalités catégorielles. Ce n’est pas hello seule façon tooencode fonctionnalités catégorielles ; Pour plus d’informations sur d’autres techniques, les utilisateurs concernés peuvent extraire [un-à chaud-encoding](http://en.wikipedia.org/wiki/One-hot) et [fonctionnalité hachage](http://en.wikipedia.org/wiki/Feature_hashing).
>

tables de nombres toobuild sur les données de nombres hello, nous utilisons des données de la hello dans hello brut/nombre de dossiers. Bonjour modélisation section, nous montrer aux utilisateurs comment toobuild ces comptent les tables pour les fonctionnalités par catégorie de toutes pièces, ou vous pouvez également toouse une table de nombres prédéfinis pour leurs explorations. Dans ce qui suit, lorsque nous nous référons trop « prégénérées tables de nombres », nous entendons à l’aide de tables de nombres hello que nous fournissons. Obtenir des instructions détaillées sur la manière dont tooaccess ces tables sont fournis dans la section suivante de hello.

## <a name="aml"></a> Création de modèles dans Azure Machine Learning
Notre processus de création de modèles dans Azure Machine Learning se déroule comme suit :

1. [Obtenir des données de hello à partir des tables de la ruche dans Azure Machine Learning](#step1)
2. [Créer l’expérience de hello : nettoyer les données de salutation et générer des fonctionnalités avec les tables de nombres](#step2)
3. [Build, de formation et de modèle de score hello](#step3)
4. [Évaluation du modèle de hello](#step4)
5. [Publier un modèle de hello sous la forme d’un service web](#step5)

Vous êtes désormais prêt toobuild des modèles dans Azure Machine Learning studio. Nos données échantillonnées bas sont enregistrées en tant que tables Hive dans le cluster de hello. Nous utilisons hello Azure Machine Learning **importer des données** module tooread ces données. Hello informations d’identification tooaccess hello compte de stockage de ce cluster sont fournies ci-après.

### <a name="step1"></a>Étape 1 : Obtenir des données à partir des tables de la ruche dans Azure Machine Learning à l’aide du module d’importation de données hello et sélectionnez-le pour une expérience d’apprentissage
Commencez par sélectionner **+NOUVEAU** -> **EXPÉRIENCE** -> **Expérience vide**. Ensuite, à partir de hello **recherche** zone hello coin supérieur gauche, recherchez « Importer des données ». Glisser- déposer hello **importer des données** module sur le module de hello toouse toohello expérience canevas (partie centrale de l’écran hello hello) pour accéder aux données.

Il s’agit de quel hello **importer des données** il semble que lors de l’obtention des données à partir de la table de hello Hive :

![Import Data obtient des données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Pourquoi **importer des données** module, les valeurs hello de paramètres hello qui sont fournis dans hello graphique sont des exemples simplement de hello tri des valeurs que vous avez besoin de tooprovide. Voici quelques conseils généraux sur comment toofill le paramètre hello out définie pour hello **importer des données** module.

1. Choisissez « Requête Hive » pour la **source de données**
2. Bonjour **requête de base de données Hive** zone, une simple instruction SELECT * FROM < votre\_base de données\_name.your\_table\_nom >-est suffisant.
3. **URI du serveur Hcatalog** : si votre cluster se nomme « abc », vous avez donc : https://abc.azurehdinsight.net
4. **Nom du compte utilisateur Hadoop**: nom d’utilisateur hello choisie au moment de la mise en service de cluster de hello du hello. (Non hello accès à distance nom d’utilisateur !)
5. **Mot de passe utilisateur Hadoop**: mot de passe hello pour nom d’utilisateur hello choisie au moment de la mise en service de cluster de hello du hello. (Pas passe de l’accès à distance hello !)
6. **Emplacement des données de sortie**: choisissez « Azure »
7. **Nom de compte de stockage Azure**: hello compte de stockage associé au cluster de hello
8. **Clé de compte de stockage Azure**: clé hello hello du compte de stockage associé au cluster de hello.
9. **Nom du conteneur Azure**: si le nom du cluster hello est « abc », alors il s’agit simplement « abc », généralement.

Une fois hello **importer des données** a fini de l’obtention de données (vous voyez les graduations hello verte sur hello Module), enregistrez ces données comme un jeu de données (avec un nom de votre choix). Cela ressemble à :

![Import Data enregistre des données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Avec le bouton hello sortie de hello **importer des données** module. Ceci fait apparaître une option **Enregistrer comme dataset** et une option **Visualiser**. Hello **visualiser** option, si vous cliquez dessus, affiche les 100 lignes de données hello, ainsi que d’un panneau de droite qui est utile pour des statistiques de résumé. toosave des données, il suffit de sélectionner **enregistrer en tant que jeu de données** et suivez les instructions.

jeu de données tooselect hello enregistré pour une utilisation dans une expérience d’apprentissage machine, recherchez hello de jeux de données à l’aide de hello **recherche** zone illustrée dans la figure suivante de hello. Puis tapez simplement nom hello vous donnez hello dataset partiellement tooaccess il et faites glisser hello dataset vers hello panneau principal. Déplacée dans le panneau de configuration principal hello le sélectionne pour une utilisation dans la modélisation d’apprentissage machine.

![Jeu de données Drage sur Panneau de configuration principal hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Le fait pour effectuer l’apprentissage hello et jeux de données de test hello. En outre, n’oubliez pas toouse hello base de données et les noms de table que vous avez attribué à cet effet. les valeurs Hello utilisées dans la figure hello sont uniquement d’illustration purposes.* *
> 
> 

### <a name="step2"></a>Étape 2 : Créer une expérience simple dans Azure Machine Learning toopredict clics / aucun clic
Notre expérience Azure ML ressemble à ceci :

![Expérience Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

Examinons maintenant hello principaux composants de cette expérience. En guise de rappel, nous devons toodrag notre enregistré effectuer l’apprentissage et jeux de données sur le canevas de l’expérience tooour tester au préalable.

#### <a name="clean-missing-data"></a>Nettoyage des données manquantes
Hello **Clean Missing Data** module est ce que son nom l’indique : il nettoie les données manquantes d’une manière qui peut être spécifié par l’utilisateur. Dans ce module, nous pouvons voir ceci :

![Nettoyage des données manquantes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

Ici, nous avons choisi tooreplace toutes les valeurs manquantes par un 0. D’autres options sont également, qui peuvent être consultées en examinant les menus déroulants de hello de module de hello.

#### <a name="feature-engineering-on-hello-data"></a>Ingénierie de fonctionnalité sur les données de salutation
Certaines fonctionnalités catégorielles de jeux de données volumineux peuvent rassembler des millions de valeurs uniques. L’utilisation des techniques naïves, telles que l’encodage à chaud pour représenter des fonctionnalités catégorielles de grande dimension, est tout bonnement impossible. Dans cette procédure pas à pas, nous allons montrer comment les fonctionnalités de nombre de toouse à l’aide intégrée toogenerate de modules Azure Machine Learning compact représentations de ces variables catégorielles de grande dimension. Hello résultat final est une plus petite taille de modèle, le temps de formation plus rapides et des métriques de performances sont tout à fait comparable toousing autres techniques.

##### <a name="building-counting-transforms"></a>Création de transformations de comptage
fonctionnalités de nombre toobuild, nous utilisons hello **générer comptage transformer** module qui est disponible dans Azure Machine Learning. module de Hello ressemble à ceci :

![Créer un module de transformation de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Créer un module de transformation de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> Bonjour **compter les colonnes** , nous, saisissez les colonnes que nous souhaitons tooperform compte. En règle générale, il s'agit de colonnes catégorielles de grande dimension (comme indiqué). Au démarrage de hello, nous l’avons mentionné hello Criteo jeu de données a des colonnes catégorielles 26 : à partir de Col15 tooCol40. Ici, nous compter sur chacune d'entre elles et leurs index (de 15 too40 séparés par des virgules, comme indiqué).
> 

module hello toouse hello mode MapReduce (le cas pour les jeux de données volumineux), nous devons accéder au cluster HDInsight Hadoop de tooan (hello celui utilisé pour l’exploration de la fonctionnalité peut être réutilisé à cet effet ainsi) et ses informations d’identification. les figures précédentes Hello illustrent hello renseignés valeurs ressemble (remplacez les valeurs hello fournies à titre d’illustration avec ceux appropriés pour votre propre cas d’utilisation).

![Paramètres du module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

Dans la figure hello ci-dessus, nous montrons comment tooenter hello d’entrée d’objet blob emplacement. Cet emplacement a réservé pour la création de tables de nombres les données de salutation.

Une fois ce module a terminé son exécution, nous pouvons enregistrer transformation hello pour ultérieurement en double-cliquant sur le module de hello et en sélectionnant hello **enregistrer en tant que transformation** option :

![Option « Enregistrer en tant que transformation »](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

Dans notre expérience l’architecture illustrée ci-dessus, hello dataset « ytransform2 » correspond précisément les tooa enregistré la transformation de nombre. Pour le reste de hello de cette expérience, nous partons du principe que lecteur hello utilisé un **générer comptage transformer** module sur certaines données toogenerate nombres et peut ensuite utiliser ces fonctionnalités de nombre de nombres toogenerate train de hello et jeux de données de test.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>En choisissant ce que nombre tooinclude de fonctionnalités dans le cadre de l’apprentissage de hello et jeux de données de test
Une fois que nous disposons d’un nombre transformer prêt, utilisateur de hello choisir quelles tooinclude de fonctionnalités dans leur apprentissage et tester des jeux de données à l’aide de hello **modifier les paramètres de Table nombre** module. Nous montrons ce module ici par souci d’exhaustivité, mais dans un souci de simplification nous ne l’utilisons pas dans notre expérience.

![Modifier les paramètres de la table de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

Dans ce cas, comme le montre, nous avons choisi toouse probabilités de journalisation simplement hello et tooignore hello rétrogradation de la colonne. Nous pouvons également définir des paramètres tels que hello bin plafond, combien tooadd exemples pseudo-aléatoire préalable de lissage, et si toouse tout Laplace parasites ou non. Tous ces éléments sont des fonctionnalités avancées, et il est toobe de noter que les valeurs par défaut de hello sont un bon point de départ pour les utilisateurs qui sont de nouveau type toothis de la génération de la fonctionnalité.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Transformation de données avant de générer des fonctionnalités de nombre hello
Maintenant nous concentrer sur un point important sur la transformation de notre train et tooactually préalable de données des fonctionnalités de comptage de génération de test. Notez qu’il existe deux **Execute R Script** modules utilisés avant que nous appliquons hello nombre transformer tooour des données.

![Modules Exécuter le script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Voici le script R de la première hello :

![Premier script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

Dans ce script R, nous renommer trop notre toonames colonnes « Col1 » « Col40 ». Il s’agit, car hello count transformation attend des noms de ce format.

Dans le script R de la deuxième hello, nous équilibrer la distribution hello entre classes positifs et négatifs (classes 1 et 0 respectivement) par classe négatif de sous-échantillonnage hello. Hello R script ici montre comment toodo cela :

![Deuxième script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

Dans ce script R simple, nous utilisons « pos\_neg\_rapport « durée hello tooset équilibre entre hello positif et les classes négatif hello. Ceci est important toodo amélioration déséquilibre de la classe généralement ayant des gains de performance pour les problèmes de classification lorsque la distribution de classe hello est rétrécie (n’oubliez pas que dans le cas présent, nous avons 3.3 % des classes positif et 96,7 % négatif).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Application d’une transformation de nombre hello sur nos données
Enfin, nous pouvons utiliser hello **appliquer une Transformation** module tooapply hello nombre des transformations sur notre effectuer l’apprentissage et jeux de données de test. Ce module prend la transformation de nombre hello enregistré comme une entrée hello l’apprentissage et jeux de données de test comme hello autres entrées et renvoie des données avec des fonctionnalités de nombre. En voici l’illustration :

![Appliquer le module de transformation](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Un extrait de l’aspect de fonctionnalités de comptage hello
Il est intéressant toosee les fonctionnalités de comptage hello se présenter comme dans le cas présent. En voici un exemple :

![Fonctionnalités de comptage](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

Dans cet extrait, nous allons montrer que des colonnes hello recensement sur, nous obtenir le nombre hello et connectez-vous cotes backoffs pertinentes de tooany Ajout.

Nous sommes maintenant prêt toobuild un modèle Azure Machine Learning à l’aide de ces jeux de données transformé. Dans la section suivante de hello, nous montrons comment procéder.

### <a name="step3"></a>Étape 3 : Créer, assimiler et score hello modèle

#### <a name="choice-of-learner"></a>Choix de l'apprenant
Tout d’abord, nous devons toochoose un apprenant. Nous sommes continu toouse un arbre de décision augmentés de deux classes en tant que notre apprenant. Voici les options par défaut de hello pour cet apprenant :

![Paramètres de l’arbre de décision optimisé à deux classes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Pour notre expérience, nous sont les valeurs par défaut de cours toochoose hello. Vous constatez que hello par défaut sont généralement explicite et une bonne solution tooget rapide lignes de base sur les performances. Vous pouvez améliorer sur les performances par balayage des paramètres si vous choisissez tooonce que vous avez une ligne de base.

#### <a name="train-hello-model"></a>Modèle de hello train
Pour l'apprentissage, nous appelons simplement un module **Former le modèle** . Hello deux entrées tooit sont apprenant de Two-Class Boosted Decision Tree hello et notre jeu de données d’apprentissage. En voici l’illustration :

![Module de formation de modèle](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Modèle de score hello
Une fois que nous disposons d’un modèle formé, nous sommes prêts tooscore sur hello tester dataset et tooevaluate ses performances. Pour ce faire, nous à l’aide de hello **Score Model** module illustré hello suivant figure, avec un **modèle Evaluate** module :

![Score Model module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Étape 4 : Évaluer le modèle de hello
Enfin, nous aimerions tooanalyze performances du modèle. En règle générale, pour les deux problèmes de classification (binaire) de classe, une bonne mesure est hello AUC. toovisualize, nous raccorder hello **Score Model** module tooan **modèle Evaluate** module pour cela. En cliquant sur **visualiser** sur hello **modèle Evaluate** module génère un graphique comme hello suivant un :

![Évaluation du modèle du module BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

Dans le binaire (ou classe deux) des problèmes de classification, une bonne mesure de précision de prédiction est hello zone sous courbe (AUC). Nous présentons ci-après nos résultats à l’aide de ce modèle sur notre jeu de données de test. tooget, port de sortie avec le bouton hello Hello **modèle Evaluate** module, puis **visualiser**.

![Visualisation du module Évaluer le modèle](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Étape 5 : Publier un modèle de hello comme un service Web
possibilité de Hello toopublish un modèle Azure Machine Learning en tant que services web avec un minimum de complications est une fonctionnalité précieuse pour rendre largement disponible. Une fois que vous avez terminé, tout le monde peut rendre les appels toohello web service avec des données d’entrée dont ils ont besoin des prédictions pour que service web de hello utilise hello modèle tooreturn ces prédictions.

toodo, nous avons tout d’abord enregistrer notre modèle formé en tant qu’objet modèle formé. Cela en double-cliquant sur hello **Train Model** module et à l’aide de hello **enregistrer en tant que modèle formé** option.

Ensuite, nous devons toocreate entrée et sortie ports pour notre service web :

* Récupère les données Bonjour même formulaire en tant que données hello dont nous avons besoin des prédictions pour un port d’entrée
* un port de sortie retourne hello Scored Labels et les probabilités de hello associé.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Sélectionnez quelques lignes de données pour le port d’entrée de hello
Il est pratique toouse un **Apply SQL Transformation** module tooselect seulement 10 lignes tooserve comme hello d’entrée donnée de port. Sélectionnez les lignes de données pour notre port d’entrée à l’aide de la requête SQL de hello indiqué ici :

![Données du port d'entrée](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Service Web
Est maintenant prêt à toorun une expérience de petite qui peut être utilisé toopublish notre service web.

#### <a name="generate-input-data-for-webservice"></a>Générer des données d'entrée pour le service Web
Comme une étape de zéro, étant donné que la table de nombres hello est volumineuse, nous prendre de quelques lignes de données de test et générer des données de sortie à partir de celui-ci avec les fonctionnalités de nombre. Cela peut servir de format de données d’entrée hello pour notre service Web. En voici l’illustration :

![Création des données d'entrée BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Pour le format de données d’entrée hello, nous utilisons désormais hello sortie Hello **Featurizer** module. Une fois que cela tester la fin de son exécution, enregistrer la sortie de hello de hello **Featurizer** module comme un jeu de données. Ce jeu de données est utilisé pour les données d’entrée de hello dans hello webservice.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Expérience d’évaluation de la publication du service Web
Tout d’abord, nous vous indiquons ci-dessous à quoi cela ressemble. structure d’essentielles Hello est un **Score Model** module qui accepte notre objet modèle formé et quelques lignes de données d’entrée que nous avons généré dans les étapes précédentes hello à l’aide de hello **Featurizer** module. Nous utilisons tooproject « Sélectionner les colonnes dans Dataset » hello au score calculé étiquettes et les probabilités de Score hello.

![Sélectionner des colonnes dans le jeu de données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Notez comment hello **sélectionner les colonnes dans le jeu de données** module peut être utilisé pour le « filtrage « données à partir d’un jeu de données. Nous afficher le contenu de hello ici :

![Le filtrage avec hello sélectionner les colonnes dans le module de jeu de données](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

les ports tooget hello bleu d’entrée et sortie, cliquez simplement sur **préparer webservice** en bas de hello à droite. Exécutez cette expérience nous permet également de service web de hello toopublish : cliquez sur hello **publier le SERVICE WEB** icône à hello en bas à droite, présenté ici :

![Publication du service Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Une fois publiée hello webservice, nous obtenons page redirigé tooa qui se présente ainsi :

![Tableau de bord du service web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Nous voyons deux liens pour webservices sur le côté gauche de hello :

* Hello **demande/réponse** Service (ou les enregistrements de ressources) est destiné à des prévisions uniques et est ce que nous allons utiliser dans cet atelier.
* Hello **l’exécution par lots** Service (BES) est utilisé pour les prédictions par lot et nécessite que des prédictions toomake de données d’entrée utilisées hello se trouvent dans le stockage d’objets Blob Azure.

En cliquant sur le lien de hello **demande/réponse** nous prend tooa page nous conserves préalable de code en c#, python et R. Ce code peut être utilisé pour effectuer des appels toohello webservice. Notez que cette clé d’API sur cette page hello doit toobe utilisé pour l’authentification.

Il est pratique toocopy cette python code sur tooa nouvelle cellule dans le bloc-notes de notebooks hello.

Ici, nous affichons un segment de code python avec la clé d’API correcte hello.

![Code Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Notez que nous avons remplacé clé d’API hello par défaut avec la clé de l’API de notre webservices. En cliquant sur **exécuter** sur cette cellule dans un notebooks bloc-notes génère hello suivant la réponse :

![Réponse IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Nous constatons que pour hello deux tester les exemples, que nous avons interrogés (dans le cadre JSON de hello du script de python hello), nous obtenons réponses sous forme de hello « Au score calculé étiquettes, les probabilités au score calculé ». Notez que dans ce cas, nous avons choisi par défaut hello ce code pré-enregistrée hello fournit (0 pour toutes les colonnes numériques et de chaîne de hello « valeur » pour toutes les colonnes catégorielles).

Ceci conclut notre procédure pas à pas de bout en bout de montrant comment toohandle dataset à grande échelle à l’aide d’Azure Machine Learning. Nous avons démarré avec un téraoctet de données, construit un modèle de prévision et déployé comme un service web dans le cloud de hello.

