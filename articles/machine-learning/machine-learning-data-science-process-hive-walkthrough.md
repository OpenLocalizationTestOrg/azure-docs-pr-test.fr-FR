---
title: "aaaExplore des données dans un Hadoop de cluster et créer des modèles dans Azure Machine Learning | Documents Microsoft"
description: "Pour un scénario de bout en bout utilisant un HDInsight Hadoop à l’aide de hello processus de science des données de Team toobuild de cluster et déployer un modèle à l’aide d’un jeu de données disponible publiquement."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Hello processus de science des données équipe en action : utilisez Azure HDInsight Hadoop de clusters
Dans cette procédure pas à pas, nous utilisons hello [processus de science des données équipe (TDSP)](data-science-process-overview.md) dans un scénario de bout en bout à l’aide un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Explorer et d’une fonctionnalité publiquement les données d’ingénierie à rebours de hello disponible [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) dataset et toodown échantillonner les données de salutation. Modèles de données de hello sont générés avec Azure Machine Learning toohandle binaire et multiclasses classification et la régression tâches prédictives.

Pour une procédure pas à pas qui montre comment toohandle un plus grand jeu de données (1 téraoctet) pour un scénario similaire à l’aide de HDInsight Hadoop de clusters pour le traitement des données, consultez [équipe processus de science des données - à l’aide de Clusters Hadoop HDInsight Azure sur un jeu de données de 1 to](machine-learning-data-science-process-hive-criteo-walkthrough.md).

Il est également possible toouse un hello tooaccomplish du bloc-notes notebooks tâches procédure pas à pas hello présenté à l’aide du jeu de données de 1 to hello. Les utilisateurs qui seraient comme tootry cette approche doit consulter hello [procédure pas à pas Criteo à l’aide d’une connexion ODBC de la ruche](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) rubrique.

## <a name="dataset"></a>Description du jeu de données NYC Taxi Trips
Hello les données NYC Taxi voyage est d’environ 20 Go de fichiers de valeurs compressées séparées par des virgules (CSV) (non compressé en ~ 48 Go), qui comprend plus de 173 millions hello et des boucles tarifs payé pour chaque sortie. Chaque enregistrement de voyage comprend hello collecte et remise l’emplacement et l’heure, hack rendues anonymes (pilote) numéro de licence et nombre de medallion (id unique de taxi). les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :

1. les fichiers CSV Hello 'trip_data' contiennent des détails de voyage, telles que le nombre de personnes, collecte et cette chute points, durée de voyage, longueur de voyage. Voici quelques exemples d’enregistrements :
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. fichiers de Hello 'trip_fare' CSV contenant les détails de tarif de hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé. Voici quelques exemples d’enregistrements :
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composée de champs de hello : medallion, hack\_certificat et pickup\_datetime.

tooget tous les voyage particulier hello détails tooa pertinentes, il est suffisant toojoin avec trois clés : hello « medallion », « hack\_licence » et « pickup\_datetime ».

Nous décrivons certains plus d’informations sur les données de salutation lorsque nous les stocker dans les tables de la ruche peu de temps.

## <a name="mltasks"></a>Exemples de tâches de prédiction
Lors de l’approche des données, détermination de type hello de prédictions que vous souhaitez toomake en fonction de son analyse permet de clarifier les tâches hello que vous devez tooinclude dans votre processus.
Voici trois exemples de problèmes de prédiction qui nous adresse dans cette procédure pas à pas dont formulation repose sur hello *Conseil\_quantité*:

1. **Classification binaire** : prédire si un pourboire a ou non été versé pour une course ; autrement dit, une valeur *tip\_amount* supérieure à 0 $ constitue un exemple positif, alors qu’une *valeur tip\_amount* de 0 $ est un exemple négatif.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Classification multiclasse**: plage de hello toopredict des montants de conseil payé pour le voyage de hello. Nous allons diviser hello *Conseil\_quantité* dans les cinq conteneurs ou les classes :
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tâche de régression**: toopredict hello d’info-bulle hello montant d’un voyage.  

## <a name="setup"></a>Configuration d’un cluster Hadoop HDInsight pour une analyse avancée
> [!NOTE]
> Il s'agit généralement d’une tâche d’ **administration** .
> 
> 

Vous pouvez configurer un environnement Azure pour une analyse avancée qui utilise un cluster HDInsight en trois étapes :

1. [Création d’un compte de stockage](../storage/common/storage-create-storage-account.md): ce compte de stockage est utilisé pour stocker des données dans un stockage Azure Blob. données Hello utilisées dans les clusters HDInsight se trouvent également ici.
2. [Personnaliser Azure HDInsight Hadoop avancé des processus Analytique et la technologie des clusters pour hello](machine-learning-data-science-customize-hadoop-cluster.md). Cette étape crée un cluster Hadoop Azure HDInsight avec Anaconda Python 2.7 64 bits installé sur tous les nœuds. Il existe deux étapes importantes tooremember lors de la personnalisation de votre cluster HDInsight.
   
   * N’oubliez pas de compte de stockage hello toolink créé à l’étape 1 avec votre cluster HDInsight lors de sa création. Ce compte de stockage donnée tooaccess utilisé est traitée dans le cluster de hello.
   * Après la création de cluster de hello, activez l’accès à distance toohello nœud de tête hello cluster. Accédez toohello **Configuration** onglet et cliquez sur **activer distant**. Cette étape spécifie les informations d’identification de l’utilisateur hello utilisées pour la connexion à distance.
3. [Créer un espace de travail Azure Machine Learning](machine-learning-create-workspace.md): ce Azure Machine Learning espace de travail est utilisé toobuild apprentissage des modèles. Cette tâche est résolue après avoir effectué une exploration de données initiales et vers le bas d’échantillonnage à l’aide du cluster HDInsight de hello.

## <a name="getdata"></a>Obtenir des données de hello à partir d’une source publique
> [!NOTE]
> Il s'agit généralement d’une tâche d’ **administration** .
> 
> 

tooget hello [NYC Taxi allers-retours](http://www.andresmh.com/nyctaxitrips/) dataset à partir de son emplacement public, vous pouvez utiliser une des méthodes hello décrites dans [tooand de déplacer les données à partir du stockage d’objets Blob Azure](machine-learning-data-science-move-azure-blob.md) machine de tooyour données toocopy hello.

L’exemple suivant décrit comment utiliser AzCopy tootransfer hello fichiers contenant des données. toodownload et installer AzCopy suivent les instructions de hello à [prise en main de l’utilitaire de ligne de commande AzCopy de hello](../storage/common/storage-use-azcopy.md).

1. À partir d’une fenêtre d’invite de commandes, exécutez hello suivant de commandes AzCopy, en remplaçant *< path_to_data_folder >* avec la destination souhaitée de hello :

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Lors de la copie de hello est terminée, un total de fichiers compressés 24 sont dans le dossier de données hello choisi. Décompressez hello téléchargé les fichiers toohello même répertoire sur votre ordinateur local. Prenez note du dossier hello où résident les fichiers de hello non compressé. Ce dossier sera référencé tooas hello *< chemin d’accès\_à\_unzipped_data\_fichiers\>*  est ce qui suit.

## <a name="upload"></a>Télécharger le conteneur de hello données toohello par défaut du cluster Azure HDInsight Hadoop
> [!NOTE]
> Il s'agit généralement d’une tâche d’ **administration** .
> 
> 

Bonjour les commandes AzCopy suivantes, remplacez hello paramètres avec les valeurs réelles hello que vous avez spécifié lors de la création de cluster Hadoop de hello suivants et la décompression des fichiers de données hello.

* ***&#60; path_to_data_folder >*** directory hello (ainsi que le chemin d’accès) sur votre ordinateur qui contiennent les fichiers de données hello décompressé  
* ***&#60; le nom de compte de stockage de cluster Hadoop >*** hello compte de stockage associé à votre cluster HDInsight
* ***&#60; le conteneur par défaut du cluster Hadoop >*** conteneur par défaut de hello utilisé par votre cluster. Notez ce nom hello de valeur par défaut hello conteneur est généralement hello même nom en tant que cluster hello lui-même. Par exemple, si le cluster de hello est appelée « abc123.azurehdinsight.net », le conteneur par défaut de hello est abc123.
* ***&#60; clé de compte de stockage >*** hello clé hello compte de stockage utilisé par votre cluster

À partir d’une invite de commandes ou une fenêtre Windows PowerShell sur votre ordinateur, exécutez hello suivant deux commandes AzCopy.

Cette commande télécharge les données de voyage hello trop***nyctaxitripraw*** répertoire dans un conteneur par défaut hello de cluster Hadoop de hello.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Cette commande télécharge les données de prix hello trop***nyctaxifareraw*** répertoire dans un conteneur par défaut hello de cluster Hadoop de hello.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

les données de salutation doivent être présent dans le stockage d’objets Blob Azure et prêt toobe consommés au sein du cluster HDInsight de hello.

## <a name="#download-hql-files"></a>Ouvrez une session sur le nœud principal de hello de cluster Hadoop et et le préparer pour l’analyse exploratoire des données
> [!NOTE]
> Il s'agit généralement d’une tâche d’ **administration** .
> 
> 

tooaccess hello nœud de tête hello cluster pour l’analyse exploratoire des données et d’arrêt d’échantillonnage des données de hello, suivez la procédure hello dans [hello d’accès nœud principal de Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

Dans cette procédure pas à pas, nous utilisons principalement les requêtes écrites [Hive](https://hive.apache.org/), un langage de requête de type SQL, des explorations de données préliminaires tooperform. les requêtes Hive Hello sont stockés dans les fichiers .hql. Nous avons ensuite vers le bas les exemples de cette toobe de données utilisé dans Azure Machine Learning pour générer des modèles.

cluster de hello tooprepare pour l’analyse exploratoire des données, nous télécharger hello .hql contenant des scripts Hive pertinentes hello à partir de [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa répertoire local (C:\temp) sur le nœud principal de hello. toodo, ouvrez hello **invite de commandes** depuis hello nœud principal de hello hello cluster et le problème suivant les deux commandes :

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Ces deux commandes télécharge tous les fichiers .hql nécessaires dans ce répertoire local de procédure pas à pas toohello ***C:\temp &#92;*** dans le nœud principal de hello.

## <a name="#hive-db-tables"></a>Créer la base de données Hive et les tables partitionnées par mois
> [!NOTE]
> Il s'agit généralement d’une tâche d’ **administration** .
> 
> 

Nous sommes maintenant toocreate prêt ruche tables pour notre jeu de données taxi NYC.
Dans le nœud principal de hello du cluster Hadoop de hello, ouvrez hello ***ligne de commande Hadoop*** hello bureau du nœud principal de hello et entrez le répertoire de ruche hello en entrant la commande hello

    cd %hive_home%\bin

> [!NOTE]
> **Exécuter toutes les commandes de la ruche dans cette procédure pas à pas de hello ci-dessus ruche bin / invite du répertoire. Il se chargera automatiquement de tout problème lié au chemin d'accès. Nous utilisons hello termes « Invite du répertoire ruche », « ruche bin / invite du répertoire » et « ligne de commande Hadoop « indifféremment dans cette procédure pas à pas.**
> 
> 

À partir de l’invite du répertoire hello Hive, entrez hello en ligne de commande Hadoop de tables et hello du nœud principal toosubmit hello ruche requête toocreate ruche de base de données de commande suivante :

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Voici le contenu de hello hello ***C:\temp\sample\_ruche\_créer\_db\_et\_tables.hql*** fichier qui crée la base de données de la ruche ***nyctaxidb *** et tables ***voyage*** et ***tarif***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Ce script Hive crée deux tables :

* table de « voyage » Hello contient les détails de voyage de chaque cas (détails du pilote, heure d’extraction, la distance de déplacement et les heures)
* table de « tarif » Hello contient les détails de prix (montant de frais, montant du Conseil, péage et surcharges).

Si vous avez besoin d’une assistance supplémentaire avec ces procédures ou que vous souhaitiez tooinvestigate autres possibles, consultez la section de hello [la ruche soumettre des requêtes directement à partir de ligne de commande Hadoop hello ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Charger les tables de données tooHive par partition
> [!NOTE]
> Il s'agit généralement d’une tâche d’ **administration** .
> 
> 

jeu de données Hello NYC taxi a un partitionnement naturel par mois, nous utilisons le temps de traitement et de requête plus rapides tooenable. Hello des commandes PowerShell ci-dessous (émis à partir du répertoire de ruche hello à l’aide de hello **ligne de commande Hadoop**) charger les données toohello « voyage » et « tarif » ruche tables partitionnées par mois.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Hello *exemple\_ruche\_charger\_données\_par\_partitions.hql* fichier contient des éléments suivants de hello **charger** commandes.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Notez qu’un nombre de requêtes Hive que nous utilisons ici dans le processus d’exploration hello implique la recherche au qu’une seule partition ou à un nombre limité de partitions. Mais ces requêtes peut être exécutées sur les données hello.

### <a name="#show-db"></a>Afficher les bases de données dans le cluster HDInsight Hadoop de hello
bases de données de hello de tooshow créés dans le cluster HDInsight Hadoop dans la fenêtre de ligne de commande Hadoop hello, exécutez hello en ligne de commande Hadoop de commande suivante :

    hive -e "show databases;"

### <a name="#show-tables"></a>Afficher les tables de ruche hello dans la base de données nyctaxidb hello
tables hello tooshow hello nyctaxidb base de données, exécutez hello en ligne de commande Hadoop de commande suivante :

    hive -e "show tables in nyctaxidb;"

Nous pouvons vérifier que les tables de hello sont partitionnées en émettant la commande hello ci-dessous :

    hive -e "show partitions nyctaxidb.trip;"

Hello attendu la sortie est illustrée ci-dessous :

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

De même, nous pouvons vérifier que hello tarif la table est partitionnée en émettant la commande hello ci-dessous :

    hive -e "show partitions nyctaxidb.fare;"

Hello attendu la sortie est illustrée ci-dessous :

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Exploration des données et ingénierie des fonctionnalités dans Hive
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Hello d’exploration de données et d’une fonctionnalité de tâches d’ingénierie pour hello données chargées dans des tables de ruche hello est possible à l’aide de requêtes Hive. Voici des exemples de ces tâches que nous vous décrivons dans cette section :

* Afficher les 10 principaux hello dans les deux tables.
* Explorer les distributions de données de quelques champs portant sur différentes périodes.
* Analyser la qualité des données des champs de longitude et de latitude hello.
* Générer des étiquettes de classification binaire et multiclasse selon hello **Conseil\_quantité**.
* Générer des fonctionnalités en calculant des distances de voyage direct hello.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Exploration : Vue hello top 10 enregistrements voyage de table
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

toosee quelles données hello ressemble, nous allons examiner 10 enregistrements de chaque table. Exécutez hello suivant séparément les deux requêtes à partir de l’invite du répertoire ruche hello dans les enregistrements hello tooinspect hello ligne de commande Hadoop console.

tooget hello top 10 enregistrements dans la table de hello « voyage » à partir du premier mois de hello :

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget hello top 10 enregistrements dans la table de hello « tarif » à partir du premier mois de hello :

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

Il est souvent utile toosave hello enregistrements tooa fichier pour l’affichage pratique. Un toohello petite modification au-dessus de requête effectue cela :

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Exploration : Afficher hello le nombre d’enregistrements dans chacune des partitions de 12 hello
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

D’intérêt est hello comment nombre hello de déplacements varie au cours de l’année civile de hello. Regroupement par mois nous permet de toosee l’aspect de cette distribution d’allers-retours.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Cela nous donne la sortie de hello :

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

Ici, hello première colonne est mois de hello et hello deuxième hello nombre de boucles pour ce mois.

Nous pouvons également nombre hello total d’enregistrements dans notre jeu de données de voyage en émettant hello commande à l’invite de répertoire hello Hive suivante.

    hive -e "select count(*) from nyctaxidb.trip;"

Cela donne :

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

À l’aide des commandes similaires toothose est indiqué pour le jeu de données de voyage hello, nous pouvons émettre des requêtes Hive à partir de l’invite du répertoire ruche hello pour hello tarif jeu de données toovalidate hello nombre d’enregistrements.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Cela nous donne la sortie de hello :

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Notez que hello exacte même nombre de boucles par mois est retournée pour les deux jeux de données. Cela fournit la validation de première de hello que hello données a été chargées correctement.

Calcul hello le nombre total d’enregistrements dans le jeu de données de prix hello peut être effectuée à l’aide de la commande hello ci-dessous à partir de l’invite du répertoire hello Hive :

    hive -e "select count(*) from nyctaxidb.fare;"

Cela donne :

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

Nombre total de Hello d’enregistrements dans les deux tables est également hello même. Cela fournit une validation de seconde que hello données a été chargées correctement.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploration : distribution des courses par médaillon
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Cet exemple identifie le medallion hello (numéros taxi) avec plus de 100 allers-retours pendant une période donnée. avantages de requête Hello de hello partitionnée accès à la table, car il est conditionnée par la variable de partition hello **mois**. résultats de la requête Hello écrites tooa fichier local queryoutput.tsv dans `C:\temp` sur le nœud principal de hello.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Voici le contenu de hello *exemple\_ruche\_voyage\_nombre\_par\_medallion.hql* fichier pour inspection.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

medallion Hello dans le jeu de données hello NYC taxi identifie un fichier cab unique. Nous pouvons identifier les taxis « occupés » en demandant quels taxis ont effectué plus d'un certain nombre d'allers-retours sur une période donnée. Hello exemple suivant identifie les fichiers CAB de plus de cent allers-retours dans hello trois premiers mois et enregistre hello requête résultats tooa fichier local C:\temp\queryoutput.tsv.

Voici le contenu de hello *exemple\_ruche\_voyage\_nombre\_par\_medallion.hql* fichier pour inspection.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

À partir de hello ruche invite active, commande hello de problème ci-dessous :

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploration : distribution des courses par médaillon et par licence de taxi
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Lorsque vous explorez un jeu de données, nous souhaitons fréquemment le nombre de hello tooexamine de co-occurrences des groupes de valeurs. Cette section fournit un exemple de comment toodo pour des fichiers CAB et de pilotes.

Hello *exemple\_ruche\_voyage\_nombre\_par\_medallion\_license.hql* les données de prix hello défini sur « medallion » et « hack_license » des groupes de fichiers et le nombre de retours de chaque combinaison. Son contenu est présenté ci-dessous.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Cette requête renvoie les combinaisons de taxi et de chauffeur particulier classées par ordre décroissant de courses.

À partir de hello Hive invite du répertoire, exécutez :

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

résultats de la requête Hello sont écrites tooa de fichier local C:\temp\queryoutput.tsv.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Exploration : évaluation de la qualité des données en recherchant les enregistrements de longitude et de latitude non valides
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Une analyse exploratoire des données communes vise tooweed des enregistrements non valides ou incorrects. Hello exemple dans cette section détermine si soit hello longitude ou latitude champs contiennent une valeur en dehors de zone de NYC de hello. Dans la mesure où il est probable que ces enregistrements ont un valeurs erronées de latitude de longitude, nous souhaitons tooeliminate à partir des données toobe utilisés pour la modélisation.

Voici le contenu de hello *exemple\_ruche\_qualité\_assessment.hql* fichier pour inspection.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


À partir de hello Hive invite du répertoire, exécutez :

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Hello *-S* argument inclus dans cette commande supprime l’impression d’écran de statut hello des tâches de mappage/réduction Hive hello. Cela est utile, car elle permet d’impression d’écran hello Hello Hive le résultat de la requête plus lisible.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Exploration : distributions de classe binaire des pourboires de course
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Problème de classification binaire hello décrites dans hello [des exemples de tâches de prédiction](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, il est utile tooknow si une info-bulle a été spécifiée ou non. Cette distribution de pourboires est binaire :

* pourboire donné (classe 1, tip\_amount > 0 $)  
* Aucun pourboire (classe 0, tip\_amount = 0 $).

Hello *exemple\_ruche\_incliné\_frequencies.hql* fichier ci-dessous effectue cette opération.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

À partir de hello Hive invite du répertoire, exécutez :

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Exploration : Classe distributions dans le paramètre multiclasse de hello
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Problème de classification multiclasse hello décrites dans hello [des exemples de tâches de prédiction](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section ce jeu de données se prête également tooa classification naturel où nous souhaiterions durée hello toopredict conseils hello donné. Nous pouvons utiliser des plages de conseil toodefine emplacements dans la requête de hello. tooget hello distributions de classe pour hello diverses plages de Conseil, nous utilisons hello *exemple\_ruche\_Conseil\_plage\_frequencies.hql* fichier. Son contenu est présenté ci-dessous.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Exécutez hello de commande suivante à partir de la console de ligne de commande Hadoop :

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Exploration : calculer la distance directe entre deux emplacements de latitude-longitude
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Ayant une mesure de distance directe de hello permet toofind out des différences entre eux et hello hello réel déclenchement distance. Nous motiver cette fonctionnalité en expliquant que passager peut être inférieur info-bulle probable si elles déterminer ce pilote hello a intentionnellement les pris par voie bien plus longue.

comparaison de hello toosee entre la distance de voyage réelle et hello [distance Haversine](http://en.wikipedia.org/wiki/Haversine_formula) entre deux points de latitude de longitude (« circle great » à distance hello), nous utilisons hello des fonctions trigonométriques disponibles au sein de la ruche, par conséquent :

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

Dans la requête de hello ci-dessus, R est rayon hello hello terre en miles et pi est tooradians converti. Notez que les points de latitude de longitude hello sont les valeurs « filtré » tooremove loin d’être zone NYC de hello.

Dans ce cas, nous écrivons notre répertoire tooa de résultats appelée « queryoutputdir ». séquence Hello des commandes ci-dessous crée d’abord ce répertoire de sortie, puis exécute la commande de ruche hello.

À partir de hello Hive invite du répertoire, exécutez :

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Hello résultats de la requête sont écrits les objets BLOB Azure de too9 ***queryoutputdir/000000\_0*** trop ***queryoutputdir/000008\_0*** sous le conteneur par défaut de hello du cluster Hadoop de hello.

taille de hello toosee d’objets BLOB individuels de hello, nous exécutons hello de commande suivante à partir de l’invite du répertoire hello Hive :

    hdfs dfs -ls wasb:///queryoutputdir

contenu de hello toosee d’un fichier donné, par exemple 000000\_0, nous utilisons de Hadoop `copyToLocal` commande ainsi.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> `copyToLocal` peut être très lent pour les fichiers volumineux et n’est pas recommandé pour une utilisation avec ceux-ci.  
> 
> 

Le principal avantage d’avoir ces données résident dans un objet blob Azure est que nous pouvons Explorer les données hello dans Azure Machine Learning à l’aide de hello [importer des données] [ import-data] module.

## <a name="#downsample"></a>Réduire l’échantillon des données et créer des modèles dans Azure Machine Learning
> [!NOTE]
> Il s'agit généralement d’une tâche de **données scientifiques** .
> 
> 

Après la phase d’analyse hello analyse exploratoire des données, vous voilà prêt toodown exemples de données hello pour générer des modèles dans Azure Machine Learning. Dans cette section, nous montrons comment toouse une ruche interroger toodown exemple hello de données, qui sont ensuite accessible à partir de hello [importer des données] [ import-data] module dans Azure Machine Learning.

### <a name="down-sampling-hello-data"></a>Vers le bas de l’échantillonnage des données de hello
Il existe deux étapes dans cette procédure. Tout d’abord, nous joindre hello **nyctaxidb.trip** et **nyctaxidb.fare** tables sur trois clés qui sont présents dans tous les enregistrements : « medallion », « hack\_licence », et « pickup\_datetime ». Nous générons ensuite une étiquette de classification binaire **avec pourboire** et une étiquette de classification multiclasse **tip\_class**.

hello toouse en mesure de toobe vers le bas des données échantillonnées directement à partir de hello [importer des données] [ import-data] module dans Azure Machine Learning, il est nécessaire toostore les résultats de hello Hello au-dessus de table de requête tooan interne Hive. Dans ce qui suit, nous créer une table interne de la ruche et remplir son contenu par hello joint et vers le bas les données échantillonnées.

Hello requête s’applique des fonctions de ruche standard directement toogenerate hello heure, la semaine de l’année, la semaine (1 signifie lundi et 7 stands pour dimanche) de hello « pickup\_datetime » champ et hello distance directe entre la collecte de hello et cette chute emplacements. Les utilisateurs peuvent faire référence trop[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) pour une liste complète de ces fonctions.

Hello requête, puis vers le bas des données de salutation exemples afin que les résultats de la requête hello s’adaptent à hello Azure Machine Learning Studio. Uniquement 1 % du jeu de données d’origine hello est importé dans hello Studio.

Voici le contenu de hello de *exemple\_ruche\_préparer\_pour\_agréés\_full.hql* fichier qui prépare les données pour le modèle de génération dans Azure Machine Learning.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

toorun cette requête, à partir du répertoire de ruche hello invite de commandes :

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Nous avons maintenant une table interne « nyctaxidb.nyctaxi_downsampled_dataset », qui est accessible à l’aide de hello [importer des données] [ import-data] module à partir d’Azure Machine Learning. En outre, nous pouvons utiliser ce jeu de données pour générer des modèles d'apprentissage automatique.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Utiliser le module d’importer des données de hello Bonjour de tooaccess Azure Machine Learning vers le bas les données échantillonnées
Comme les composants requis pour l’émission de requêtes Hive dans hello [importer des données] [ import-data] module d’Azure Machine Learning, nous devons accéder à l’espace de travail de tooan Azure Machine Learning et accéder aux informations d’identification toohello Hello cluster et son compte de stockage associé.

Certains détails sur hello [importer des données] [ import-data] tooinput de paramètres de module et hello :

**URI du serveur HCatalog**: si le nom du cluster hello est abc123, alors il s’agit simplement : https://abc123.azurehdinsight.net

**Nom du compte utilisateur Hadoop** : nom d’utilisateur hello choisi pour le cluster de hello (**pas** nom d’utilisateur l’accès à distance hello)

**Mot de passe de compte Hadoop ser** : mot de passe hello choisi pour le cluster de hello (**pas** mot de passe de l’accès à distance hello)

**Emplacement des données de sortie** : cela est choisi toobe Azure.

**Nom de compte de stockage Azure** : nom du compte de stockage par défaut hello associé hello cluster.

**Nom du conteneur Azure** : cela est le nom de conteneur par défaut hello pour le cluster de hello et est généralement identique hello en tant que nom de cluster hello. Pour un cluster appelé « abc123 », il s'agit simplement d’abc123.

> [!IMPORTANT]
> **N’importe quelle table que nous souhaitons tooquery à l’aide de hello [importer des données] [ import-data] module dans Azure Machine Learning doit être une table interne.** Voici un conseil pour déterminer si une table T dans une base de données D.db est une table interne.
> 
> 

À partir de hello ruche invite active, problème hello commande :

    hdfs dfs -ls wasb:///D.db/T

Si la table de hello est une table interne et il est rempli, son contenu doit afficher ici. Une autre façon toodetermine si une table est une table interne est toouse hello Explorateur de stockage Azure. Utiliser le nom de conteneur par défaut toonavigate toohello du cluster de hello et filtrer par nom de table hello. Si la table de hello et son contenu s’affiche, cela confirme qu’il est une table interne.

Voici une capture instantanée de la requête Hive de hello et hello [importer des données] [ import-data] module :

![Requête Hive pour le module Importer des données](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Notez que depuis notre vers le bas les données échantillonnées résident dans le conteneur de hello par défaut, les requêtes Hive résultant hello à partir d’Azure Machine Learning est très simple est simplement un « sélectionner * à partir de nyctaxidb.nyctaxi\_sous-échantillonnées\_données ».

Hello dataset peut maintenant être utilisé comme point de départ pour créer des modèles d’apprentissage de hello.

### <a name="mlmodel"></a>Créer des modèles dans Azure Machine Learning
Nous sommes en mesure de tooproceed toomodel génération et déploiement de modèle dans [Azure Machine Learning](https://studio.azureml.net). les données de salutation sont prêtes pour nous toouse dans la résolution des problèmes de prédiction hello identifiés ci-dessus :

**1. Classification binaire**: toopredict ou non un Conseil a été payé un voyage.

**Apprenant utilisé :** régression logistique à deux classes

a. Pour ce problème, notre étiquette (ou classe) cible est « avec pourboire ». Notre jeu de données original à l’échantillon réduit dispose de quelques colonnes qui sont des fuites cibles pour cette expérience de classification. En particulier : Conseil\_de classe, le Conseil\_montant et total\_montant révéler des informations sur l’étiquette cible hello qui n’est pas disponible sur le temps de test. Nous supprimer ces colonnes de compte à l’aide de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.

instantané Hello ci-dessous montre toopredict de notre expérience ou non un Conseil a été payé pour une sortie donnée.

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. Pour cette expérience, nos distributions d'étiquette cible ont été d’environ 1:1.

instantané Hello ci-dessous montre la répartition hello étiquettes de classe de Conseil pour le problème de classification binaire hello.

![Distribution d'étiquettes de classe de pourboire](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

Par conséquent, nous obtenons une AUC de 0.987 comme indiqué dans la figure ci-dessous hello.

![Valeur ASC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Classification multiclasse**: classes définies par la plage de hello toopredict des montants de conseil payé pour le voyage hello, à l’aide de hello précédemment.

**Apprenant utilisé :** régression logistique multiclasse

a. Pour ce problème, notre cible (ou classe) est « tip\_class », ce qui peut prendre une des cinq valeurs suivantes (0,1,2,3,4). Comme dans les cas de classification binaire hello, nous avons quelques colonnes qui sont des fuites de cible pour cette expérience. En particulier : pourboires, Conseil\_montant total\_montant révéler des informations sur l’étiquette cible hello qui n’est pas disponible sur le temps de test. Nous supprimer ces colonnes à l’aide de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.

Hello instantané ci-dessous illustre notre toopredict expérience emplacement dans lequel une info-bulle est probablement toofall (classe 0 : Conseil = 0 $, classe 1 : Conseil > $0 et info-bulle < = 5 $, classe 2 : Conseil > $5 et Conseil < = $10, 3 de la classe : Conseil > $10 et Conseil < = 20 Classe 4 : Conseil > 20)

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Nous montrons maintenant à quoi ressemble notre distribution de classe test réelle. Nous constatons que lors de la classe 0 et 1 de la classe sont les plus fréquentes, hello d’autres classes sont rares.

![Distribution de classe de test](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. Pour cette expérience, nous utilisons un toolook de matrice de confusion à notre précisions de prédiction. Consultez l’illustration ci-dessous.

![Matrice de confusion](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Notez que lors de notre précisions de classe sur les classes de largement répandue hello est assez bonne, modèle de hello n’effectue pas un bon de travail de « apprentissage » sur les classes de plus rares hello.

**3. Tâche de régression**: toopredict hello d’info-bulle montant d’un voyage.

**Apprenant utilisé :** arbre de décision optimisé

a. Pour ce problème, notre étiquette (ou classe) cible est « tip\_amount ». Fuites de notre cible sont dans ce cas : pourboires, Conseil\_(classe), total\_quantité ; toutes ces variables révèlent des informations sur la quantité de Conseil de hello est généralement pas disponible sur le temps de test. Nous supprimer ces colonnes à l’aide de hello [sélectionner les colonnes dans le jeu de données] [ select-columns] module.

Hello instantané belows illustre notre expérience toopredict hello hello donné d’info-bulle.

![Instantané de l’expérience](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Pour les problèmes de régression, nous précisions hello de notre prédiction de mesures en examinant erreur hello carré dans les prédictions de hello hello coefficient de détermination et hello comme. Nous présentons ce qui suit.

![Statistiques de prédiction](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Nous voyons que sur hello coefficient de détermination est 0.709, ce qui implique d’environ 71 % de la variance de hello est expliqué par notre coefficients du modèle.

> [!IMPORTANT]
> toolearn plus d’informations sur Azure Machine Learning et comment tooaccess et l’utiliser, consultez trop[What ' s apprentissage ?](machine-learning-what-is-machine-learning.md). Une ressource très utile pour la lecture avec un ensemble d’expériences d’apprentissage sur Azure Machine Learning est hello [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/). Galerie de Hello couvre une gamme d’expériences et fournit une présentation détaillée dans la plage hello des fonctionnalités d’Azure Machine Learning.
> 
> 

## <a name="license-information"></a>Informations de licence
Cet exemple de procédure et les scripts qui l’accompagne sont partagées par Microsoft sous licence du MIT hello. Vérifiez fichier hello le répertoire hello hello exemple de code sur GitHub pour plus d’informations.

## <a name="references"></a>Références
•    [Page de téléchargement des jeux de données NYC Taxi Trips par Andrés Monroy (en anglais)](http://www.andresmh.com/nyctaxitrips/)  
•    [Page de partage des données relatives aux courses en taxi new-yorkais par Chris Whong (en anglais)](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•    [Page de recherche et de statistiques de la Commission des services de taxis et de limousines de la ville de New York (en anglais)](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
