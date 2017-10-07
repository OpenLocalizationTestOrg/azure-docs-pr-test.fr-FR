---
title: "Science des données scalable avec Azure Data Lake : procédure complète | Microsoft Docs"
description: "Des tâches de toouse Azure Data Lake toodo exploration et binary classification des données sur un jeu de données."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a>Science des données scalable avec Azure Data Lake : procédure complète
Cette procédure pas à pas montre comment l’exploration de données Azure Data Lake toodo toouse et les tâches de classification binaire d’un échantillon de hello NYC taxi voyage et tarif toopredict de dataset ou non une info-bulle sera versée à un tarif. Il vous guide à travers les étapes de hello Hello [processus de science des données équipe](http://aka.ms/datascienceprocess), de bout en bout, à partir de la formation de toomodel d’acquisition de données, puis déploiement toohello d’un service web qui publie le modèle de hello.

### <a name="azure-data-lake-analytics"></a>Service Analytique Azure Data Lake
Hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) a toutes les hello fonctionnalités requis toomake plus facile pour les données scientifiques toostore de tout traitement de données de taille, forme et la vitesse et tooconduct, advanced analytique et une modélisation machine learning avec une haute évolutivité à moindre coût.   Le paiement s’effectue par travail effectué, seulement lorsque les données sont réellement en cours de traitement. Analytique de LAC de données Azure inclut U-SQL, un autre langage que fusion hello nature déclarative de SQL avec la puissance expressive hello c# tooprovide évolutive distributed capacité de requête. Il vous permet de tooprocess une logique personnalisée d’insertion de données non structurées en appliquant le schéma lors de la lecture, et défini par l’utilisateur (UDF) de fonctions et inclut l’extensibilité tooenable un contrôle fin sur la façon tooexecute à grande échelle. toolearn en savoir plus sur la philosophie de conception hello derrière U-SQL, consultez [billet de blog de Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

Il est également un composant essentiel de Cortana Analytics Suite et fonctionne avec Azure SQL Data Warehouse, Power BI et Data Factory. Cela vous offre une plateforme d’analyse avancée et de Big Data cloud complète.

Cette procédure pas à pas commence par décrire les conditions préalables de hello et les ressources qui sont nécessaires toocomplete hello tâches avec des données de LAC Analytique qui forment le processus de science des données hello et comment tooinstall les. Il décrit les étapes de traitement des données hello à l’aide de U-SQL et se termine en montrant comment toouse Python et Hive avec Azure Machine Learning Studio toobuild et déployer des modèles prédictifs hello. 

### <a name="u-sql-and-visual-studio"></a>U-SQL et Visual Studio
Cette procédure pas à pas recommande l’utilisation de Visual Studio tooedit U-SQL scripts tooprocess hello dataset. les scripts Hello U-SQL sont décrites ici et dans un fichier distinct. processus de Hello inclut absorber, Explorer et d’échantillonnage des données de salutation. Il montre également comment toorun U-SQL un script de travail à partir de hello portail Azure. Tables de la ruche sont créés pour les données de salutation dans une construction d’hello toofacilitate de cluster HDInsight associée et le déploiement d’un modèle de classification binaire dans Azure Machine Learning Studio.  

### <a name="python"></a>Python
Cette procédure pas à pas contient également une section qui montre comment toobuild et déployer un modèle de prévision à l’aide de Python avec Azure Machine Learning Studio.  Nous fournissons un bloc-notes jupyter avec des scripts Python hello pour ces étapes de ce processus. ordinateur portable de Hello inclut du code pour certaines étapes ingénierie de fonctionnalité supplémentaire et la construction de modèles tels que la classification multiclasse et le modèle de classification binaire toohello décrite ici en outre de modélisation de régression. tâche de régression Hello est toopredict hello Conseil hello basé sur d’autres fonctionnalités de l’info-bulle. 

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning Studio est utilisé toobuild et déployer des modèles prédictifs hello. Cette opération est effectuée selon deux approches : tout d’abord avec des scripts Python, puis avec des tables Hive sur un cluster HDInsight (Hadoop).

### <a name="scripts"></a>Scripts
Uniquement hello deux principales étapes sont décrites dans cette procédure pas à pas. Vous pouvez télécharger hello complète **script U-SQL** et **bloc-notes Jupyter** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ces rubriques, vous devez disposer de hello :

* Un abonnement Azure. Si vous n’en avez pas, consultez [Obtenir une version d’évaluation gratuite Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Recommandé] Visual Studio 2013 ou ultérieur. Si vous ne disposez pas d’une de ces versions, vous pouvez télécharger une version Community gratuite depuis [Visual Studio Community](https://www.visualstudio.com/vs/community/).

> [!NOTE]
> Au lieu de Visual Studio, vous pouvez également utiliser des requêtes de Azure Data Lake toosubmit hello portail Azure. Il fournit des instructions sur comment toodo donc avec Visual Studio et sur le portail dans la section de hello hello intitulée **traiter les données avec U-SQL**. 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a>Préparer l’environnement de science des données pour Azure Data Lake
environnement de science des données tooprepare hello pour cette procédure pas à pas, créez hello suivant des ressources :

* Azure Data Lake Store (ADLS) 
* Azure Data Lake Analytics (ADLA)
* Compte de stockage d’objets blob Azure
* Compte Azure Machine Learning Studio
* Outils Azure Data Lake pour Visual Studio (Recommandé)

Cette section fournit des instructions sur la façon de toocreate de ces ressources. Si vous choisissez toouse tables Hive avec Azure Machine Learning, au lieu de Python, toobuild un modèle, vous devez également tooprovision un cluster HDInsight (Hadoop). Cette procédure de remplacement dans décrits dans la section appropriée de hello ci-dessous.


> [!NOTE]
> Hello **Azure Data Lake Store** peuvent être créés séparément ou lorsque vous créez hello **Analytique de LAC de données Azure** comme stockage par défaut de hello. Des instructions sont référencées pour la création de chacune de ces ressources ci-dessous séparément, mais hello compte de stockage lac de données ne doive pas être créée séparément.
>
> 

### <a name="create-an-azure-data-lake-store"></a>Créer un Azure Data Lake Store


Créer un ADLS de hello [Azure Portal](http://portal.azure.com). Pour en savoir plus, consultez [Créer un cluster HDInsight avec Data Lake Store à l’aide du portail Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md). Être tooset que des hello Cluster AAD identité Bonjour **DataSource** Panneau de hello **Configuration facultative** panneau décrit il. 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a>Créer un compte Azure Data Lake Analytics
Créer un compte ADLA à partir de hello [Azure Portal](http://portal.azure.com). Pour en savoir plus, consultez [Didacticiel : Prise en main du service Azure Data Lake Analytics à l’aide du portail Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md). 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a>Créer un compte de stockage d’objets blob Azure
Créer un compte de stockage d’objets Blob Azure à partir de hello [Azure Portal](http://portal.azure.com). Pour plus d’informations, consultez hello créer un compte de stockage section [comptes de stockage sur Azure](../storage/common/storage-create-storage-account.md).

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a>Configurer un compte Azure Machine Learning Studio
Signer/dans Azure Machine Learning Studio à partir de hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page. Cliquez sur hello **prise en main** bouton, puis choisissez un « Espace de travail libre » ou un « Espace de travail Standard ». Après cela, vous serez en mesure de toocreate des expériences dans Azure ML Studio.  

### <a name="install-azure-data-lake-tools-recommended"></a>Installer les outils Azure Data Lake [Recommandé]
Installez les outils Azure Data Lake pour votre version de Visual Studio sur la page [Outils Azure Data Lake pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

Une fois l’installation de hello terminée, ouvrez Visual Studio. Vous devez voir les menus de hello hello Data Lake onglet en haut de hello. Vos ressources Azure doivent apparaître dans le panneau gauche hello lorsque vous vous connectez à votre compte Azure.

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a>jeu de données Hello NYC Taxi allers-retours
Bonjour jeu de données que nous avons utilisé ici est un jeu de données disponible publiquement--hello [NYC Taxi allers-retours dataset](http://www.andresmh.com/nyctaxitrips/). Hello les données NYC Taxi voyage se compose d’environ 20 Go de fichiers CSV compressées (Go ~ 48 non compressé), l’enregistrement de plus de 173 millions hello et des boucles tarifs payé pour chaque sortie. Chaque enregistrement de voyage inclut les emplacements de collecte et de remise de hello et de, présentées de façon anonyme hack numéro de licence (du pilote), hello nombre de medallion (id unique de taxi). les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :

* Hello 'trip_data' CSV contient les détails de voyage, telles que le nombre de personnes, collecte et cette chute points, durée de voyage, longueur de voyage. Voici quelques exemples d’enregistrements :
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* Hello 'trip_fare' CSV contient les détails des prix hello payé pour chaque sortie, comme type de paiement, montant de frais, surcharge et taxes, conseils et péage et montant total de hello payé. Voici quelques exemples d’enregistrements :
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composé de hello suivant trois champs : medallion, hack\_licence et pickup\_datetime. les fichiers CSV bruts Hello est accessible à partir d’un objet blob de stockage Azure publique. Hello script U-SQL pour cette jointure est Bonjour [joindre des tables voyage et tarif](#join) section.

## <a name="process-data-with-u-sql"></a>Traiter des données avec U-SQL
Hello le traitement des données décrit notamment les tâches de cette section incluent absorber, la vérification de la qualité, Explorer et d’échantillonnage des données de salutation. Nous montrent également comment les tables voyage et tarif toojoin. section finale de Hello montre exécuter un travail par script U-SQL à partir de hello portail Azure. Voici des liens tooeach sous-section :

* [Ingestion de données : données lues à partir d’un objet blob public](#ingest)
* [Contrôles de qualité des données](#quality)
* [Exploration des données](#explore)
* [Joindre des tables relatives aux courses et aux tarifs](#join)
* [Échantillonnage des données](#sample)
* [Exécuter des travaux U-SQL](#run)

les scripts Hello U-SQL sont décrites ici et dans un fichier distinct. Vous pouvez télécharger hello complète **scripts U-SQL** de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).

tooexecute U-SQL, ouvrez Visual Studio, cliquez sur **fichier--> Nouveau--> projet**, choisissez **U-SQL projet**, la nommer et enregistrer tooa dossier.

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> Il est possible de toouse hello Azure Portal tooexecute U-SQL au lieu de Visual Studio. Vous pouvez rechercher des ressources d’Analytique de LAC de données Azure toohello sur le portail hello et soumettre des requêtes directement, comme illustré dans la figure suivante de hello.
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <a name="ingest"></a>Ingestion de données : données lues à partir d’un objet blob public
emplacement Hello de données hello Bonjour Azure blob est référencé en tant que  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  et peuvent être extraites à l’aide de **Extractors.Csv()**. Remplacez par votre propre nom de conteneur et le nom de compte de stockage dans les scripts suivants pour container_name@blob_storage_account_name dans l’adresse de wasb hello. Étant donné que les noms de fichiers hello sont au même format, nous pouvons utiliser **voyage\_data_ {\*\}.csv** tooread dans tous les fichiers de voyage 12. 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

Étant donné que les en-têtes dans la première ligne de hello, nous avons besoin des en-têtes de hello tooremove et modifier les types de colonne dans les colonnes appropriées. Nous pouvons enregistrer hello traité données tooAzure stockage lac de données à l’aide **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**à l’aide de compte de stockage d’objets Blob _ ou tooAzure  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** . 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

De même, nous pouvons lue dans les jeux de données de prix hello. Cliquez avec le bouton droit sur Azure Data Lake Store, vous pouvez choisir de toolook à vos données dans **portail Azure--> Explorateur de données** ou **l’Explorateur de fichiers** dans Visual Studio. 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <a name="quality"></a>Contrôles de qualité des données
Une fois les tables voyage et tarif ont été lus dans, les contrôles de qualité des données est possible Bonjour de configuration suivant. Hello, ce qui entraîne des fichiers CSV peut être stockage d’objets Blob tooAzure sortie ou d’Azure Data Lake Store. 

Rechercher le nombre hello de medallions et unique de medallions :

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

Recherchez les medaillons ayant plus de 100 courses :

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

Recherchez les enregistrements non valides en termes de pickup_longitude :

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

Recherchez les valeurs manquantes pour certaines variables :

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <a name="explore"></a>Exploration des données
Mieux comprendre les données de salutation, nous pouvons effectuer certains tooget d’exploration de données.

Rechercher la distribution hello d’allers-retours pourboires et non a :

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

Rechercher la distribution hello du montant de Conseil avec les valeurs limites : 0,5,10 et 20 dollars.

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

Recherchez les statistiques de base de la distance de la course :

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

Rechercher des centiles hello de distance de voyage :

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <a name="join"></a>Joindre des tables relatives aux courses et aux tarifs
Les tables relatives aux courses et aux tarifs peuvent être jointes par médaillon, hack_license et pickup_time.

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


Pour chaque niveau du nombre de passagers, calculez le nombre de hello d’enregistrements, montant du Conseil moyenne, variance du montant de l’info-bulle, pourcentage de pourboires allers-retours.

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <a name="sample"></a>Échantillonnage des données
Tout d’abord, nous allons sélectionner aléatoirement 0,1 % de données de salutation à partir de la table jointe de hello :

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

Ensuite, nous procédons à un échantillonnage stratifié par variable binaire tip_class :

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <a name="run"></a>Exécuter des travaux U-SQL
Lorsque vous avez terminé la modification de scripts U-SQL, vous pouvez envoyer les serveur toohello à l’aide de votre compte Analytique de LAC de données Azure. Cliquez sur **Data Lake**, **Envoyer le travail**, sélectionnez votre **Compte Analytics**, choisissez **Parallélisme**, puis cliquez sur le bouton **Envoyer**.  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

Lors de la tâche de hello est lancé avec succès, état hello de votre travail s’affichera dans Visual Studio pour l’analyse. Une fois le travail de hello terminée, vous pouvez même les processus de l’exécution du travail relecture hello et découvrez hello goulot d’étranglement étapes tooimprove l’efficacité de votre travail. Vous pouvez également passer tooAzure statut de hello toocheck Portal de vos travaux U-SQL.

 ![13.](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

Maintenant, vous pouvez vérifier les fichiers de sortie hello dans le stockage Blob Azure ou portail Azure. Nous allons utiliser des données d’exemple hello stratifié pour notre modélisation à l’étape suivante de hello.

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a>Créer et déployer des modèles dans Azure Machine Learning
Nous allons montrer deux options disponibles pour les données toopull dans Azure Machine Learning toobuild et 

* Dans la première option de hello, vous utilisez des données hello échantillonnée a été écrit tooan d’objets Blob Azure (Bonjour **d’échantillonnage des données** étape ci-dessus) et utiliser Python toobuild et déployer des modèles à partir d’Azure Machine Learning. 
* Dans la deuxième option de hello, vous interrogez des données de hello dans Azure Data Lake directement à l’aide d’une requête Hive. Cette option nécessite que vous créez un nouveau cluster HDInsight ou utilisez un cluster HDInsight existant où hello ruche tables de données de NY Taxi toohello de point dans le stockage de LAC de données Azure.  Nous abordons ces deux options ci-dessous. 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a>Option 1 : Utilisation de Python toobuild et déployer des modèles d’apprentissage automatique
toobuild et le déploiement des modèles d’apprentissage automatique à l’aide de Python, créez un bloc-notes Jupyter sur votre ordinateur local ou dans Azure Machine Learning Studio. Hello bloc-notes Jupyter fourni sur [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contient hello tooexplore de code complet, de visualiser les données, de l’ingénierie de fonctionnalité, de modélisation et de déploiement. Dans cet article, nous indiquons simplement hello modélisation et déploiement. 

### <a name="import-python-libraries"></a>Importer des bibliothèques Python
Bonjour toorun de commande exemple Bloc-notes Jupyter ou hello du fichier de script Python, hello Python packages suivants sont nécessaires. Si vous utilisez hello service de AzureML bloc-notes, ces packages ont été préinstallés.

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a>Lire à partir de l’objet blob de données hello
* Chaîne de connexion   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* Lire sous forme de texte
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* Ajouter des noms de colonnes et des colonnes distinctes
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* Modifier certaines toonumeric de colonnes
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a>Créer des modèles Machine Learning
Ici, nous créons un toopredict de modèle de classification binaire si un voyage est incliné ou non. Bonjour bloc-notes Jupyter vous trouverez deux autres modèles : classification multiclasse et les modèles de régression.

* Tout d’abord, nous devons toocreate variables factice qui peuvent être utilisés dans scikit-en savoir plus les modèles
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* Créer la trame de données pour la modélisation de hello
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* Apprentissage et test de fractionnement de 60 à 40
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* Régression logistique dans le jeu d’apprentissage
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* Noter le jeu de données de test
  
        Y_test_pred = logit_fit.predict(X_test)
* Calculer les mesures d’évaluation
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a>Créer une API de service web et l’exploiter dans Python
Nous souhaitons toooperationalize hello modèle d’apprentissage après que qu’il a été généré. Nous utilisons ici un modèle de logistique binaire hello comme exemple. Vérifiez que hello scikit-en savoir plus de la version de votre ordinateur local est 0.15.1. Vous n’avez tooworry à ce sujet si vous utilisez Azure ML studio service.

* Recherchez vos informations d’identification à partir des paramètres du service Azure ML studio. Dans Azure Machine Learning Studio, cliquez sur **Paramètres** --> **Nom** --> **Jetons d'autorisation**. 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* Créer un service web
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* Obtenir des informations d’identification du service web
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* Appeler une API de service web Vous avez toowait 5 à 10 secondes après l’étape précédente de hello.
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a>Option 2 : Créer et déployer des modèles directement dans Azure Machine Learning
Azure Machine Learning Studio peut lire les données directement à partir d’Azure Data Lake Store et être toocreate utilisé et déployé des modèles. Cette approche utilise une table Hive qui pointe à hello Azure Data Lake Store. Cela nécessite que les configurer un cluster Azure HDInsight distinct, sur quel hello ruche table est créée. Hello suivant sections indiquent comment toodo cela. 

### <a name="create-an-hdinsight-linux-cluster"></a>Créer un cluster HDInsight Linux
Créer un HDInsight Cluster (Linux) à partir de hello [Azure Portal](http://portal.azure.com). Pour plus d’informations, consultez hello **créer un cluster HDInsight avec accès tooAzure Data Lake Store** section [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a>Créer une table Hive dans HDInsight
Maintenant, nous créons ruche toobe de tables utilisée dans Azure Machine Learning Studio dans le cluster HDInsight de hello à l’aide de données hello stockées dans Azure Data Lake Store à l’étape précédente de hello. Accédez toohello cluster HDInsight venez de créer. Cliquez sur **paramètres** --> **propriétés** --> **Cluster identité AAD** --> **accès ADLS**, Vérifiez que votre compte Azure Data Lake Store est ajoutée dans la liste hello en lecture, écriture et des droits d’exécution. 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

Puis cliquez sur **tableau de bord** toohello suivant **paramètres** bouton et une fenêtre seront affiche. Cliquez sur **affichage de la ruche** Bonjour coin supérieur droit de la page de hello et vous verrez hello **l’éditeur de requête**.

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

Collez une table hello suivant toocreate des scripts Hive. Hello de source de données se trouve dans la référence d’Azure Data Lake Store de cette façon : **adl://data_lake_store_name.azuredatalakestore.net:443/nom_dossier nom_fichier**.

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


Lors de la requête de hello a terminé son exécution, des résultats hello comme suit :

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a>Créer et déployer des modèles dans Azure Machine Studio
Nous sont désormais prêt toobuild et que vous déployez un modèle qui prédit ou non une info-bulle est payée avec Azure Machine Learning. Bonjour stratifié d’exemples de données est prêt toobe utilisé dans cette classification binaire (Conseil ou non) problème. Hello modèles prédictifs à l’aide de la classification multiclasse (tip_class) et de régression (tip_amount) peut également être générée et déployée avec Azure Machine Learning Studio, mais nous seulement montrer ici comment la case utilisant toohandle hello hello modèle de classification binaire.

1. Obtenir des données de hello dans Azure ML à l’aide de hello **importer des données** module, disponible dans hello **données d’entrée et sortie** section. Pour plus d’informations, consultez hello [module d’importer des données](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) page de référence.
2. Sélectionnez **requête de la ruche** comme hello **source de données** Bonjour **propriétés** Panneau de configuration.
3. Hello coller script Hive Bonjour suivant **requête de base de données Hive** éditeur
   
        select * from nyc_stratified_sample;
4. Entrez le cluster d’URI de HDInsight hello (vous pouvez trouver dans le portail Azure), informations d’identification Hadoop, l’emplacement des données de sortie et nom de conteneur/clé/nom de compte de stockage Azure.
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

Figure hello ci-dessous montre une expérience de classification binaire la lecture des données à partir de la table Hive.

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

Après la création de l’expérience de hello, cliquez sur **configurer le Service Web** --> **prédictive Service Web**

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

Exécution hello créé automatiquement score expérience, lorsqu’elle est terminée, cliquez sur **déployer le Service Web**

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

tableau de bord de service Hello web s’affiche peu de temps :

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a>Résumé
En suivant cette procédure pas à pas, vous avez créé un environnement de science des données pour créer des solutions de bout en bout évolutives dans Azure Data Lake. Cet environnement a été utilisé tooanalyze un dataset volumineux public, en mettant sur les étapes canonique de hello Hello processus de science des données, de l’acquisition des données via l’apprentissage du modèle, et puis de modèle de déploiement toohello Hello comme un service web. U-SQL a été utilisé tooprocess, Explorer et les exemples de données de hello. Python et Hive ont été utilisés avec Azure Machine Learning Studio toobuild et déploiement des modèles prédictifs.

## <a name="whats-next"></a>Et ensuite ?
Hello cursus pour le [processus de science des données équipe (TDSP)](http://aka.ms/datascienceprocess) fournit tootopics liens décrivant chaque étape dans hello avancé du processus de l’analytique. Il existe une série de procédures pas à pas détaillé sur hello [procédures pas à pas du processus de science des données équipe](data-science-process-walkthroughs.md) page ce showcase comment toouse services dans différents scénarios d’analytique prédictive et des ressources :

* [Hello processus de science des données équipe en action : à l’aide de l’entrepôt de données SQL](machine-learning-data-science-process-sqldw-walkthrough.md)
* [Hello processus de science des données équipe en action : à l’aide de clusters HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md)
* [Hello, processus de science des données équipe : à l’aide de SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Vue d’ensemble de l’utilisation de processus de science des données hello nouvelles sur Azure HDInsight](machine-learning-data-science-spark-overview.md)

