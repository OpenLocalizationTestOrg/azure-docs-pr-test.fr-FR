---
title: "aaaOverview de la Science des données à l’aide de Spark sur Azure HDInsight | Documents Microsoft"
description: "Hello Spark MLlib toolkit met apprentissage considérable fonctionnalités toohello distribué HDInsight environnement de modélisation."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Vue d’ensemble de la science des données à l’aide de Spark sur Azure HDInsight
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Cet ensemble de rubriques illustre des tâches de toouse science des données common HDInsight Spark toocomplete telles que la réception de données, l’ingénierie de fonctionnalité, la modélisation et évaluation du modèle. les données de salutation utilisées sont un exemple de hello 2013 NYC taxi voyage et tarif de jeu de données. les modèles de Hello générés incluent la régression logistique et linéaire, les forêts aléatoires et les arbres augmentés dégradés. Hello rubriques montrent également comment toostore ces modèles dans Azure blob storage (WASB) et la manière dont tooscore et d’évaluer leurs performances prédictive. D’autres rubriques plus avancées décrivent comment former des modèles par validation croisée et balayage hyperparamétrique. Cette rubrique de présentation fait également référence à des rubriques hello qui décrivent comment tooset des hello cluster Spark dont vous avez besoin d’étapes de hello toocomplete dans les procédures pas à pas hello fourni. 

## <a name="spark-and-mllib"></a>Spark et MLlib
[Spark](http://spark.apache.org/) est une infrastructure de traitement en parallèle open source qui prend en charge en mémoire traitement tooboost les performances de hello big-applications de données analytiques. moteur de traitement Spark Hello est créé pour la vitesse, la facilité d’utilisation et analytique sophistiquées. Fonctionnalités de répartition du calcul en mémoire de Spark constituent un bon choix pour les algorithmes itératif hello utilisée dans les calculs machine learning et graphique. [MLlib](http://spark.apache.org/mllib/) est environnement distribué toothis de fonctionnalités de modélisation évolutive machine learning bibliothèque de Spark qui apporte hello algorithmique. 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure hébergé offrant d’open source Spark. Il prend également en charge **Jupyter PySpark blocs-notes** sur cluster Spark hello qui peut exécuter des requêtes interactives de Spark SQL pour la transformation, de filtrage et de visualisation des données stockées dans les objets BLOB Azure (WASB). PySpark est hello API Python pour Spark. extraits de code Hello qui fournissent des solutions de hello et affichent les données de hello hello tracés pertinentes toovisualize ici s’exécutent dans les blocs-notes Notebook installés sur des clusters de Spark hello. étapes de modélisation Hello dans ces rubriques contiennent le code qui montre comment tootrain, évaluer, enregistrer et utiliser chaque type de modèle. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Installation des clusters Spark et notebooks Jupyter
Les étapes de configuration et le code fournis dans cette procédure pas à pas concernent HDInsight Spark 1.6. Mais des notebooks Jupyter sont fournis pour les clusters HDInsight Spark 1.6 et Spark 2.0. Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent. En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark. Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici. Pour des raisons pratiques, voici les liens hello blocs-notes de Notebook toohello pour Spark 1.6 (toobe exécuter dans le noyau pySpark hello Hello server de bloc-notes Jupyter) et Spark 2.0 (toobe exécuter dans le noyau pySpark3 hello Hello server de bloc-notes Jupyter) :

### <a name="spark-16-notebooks"></a>Notebooks Spark 1.6
Ces ordinateurs portables sont toobe exécuter dans le noyau pySpark hello du serveur jupyter Notebook.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fournit des informations sur l’exploration de données tooperform, de modélisation et de calcul de score avec plusieurs algorithmes différents.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) : inclut les thèmes du notebook 1 et traite également du développement de modèles à l’aide de l’ajustement des hyperparamètres et de la validation croisée.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): montre comment toooperationalize un modèle enregistré à l’aide de Python sur HDInsight clusters.

### <a name="spark-20-notebooks"></a>Notebooks Spark 2.0
Ces ordinateurs portables sont toobe exécuter dans le noyau pySpark3 hello du serveur jupyter Notebook.

- [Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ce fichier fournit des informations sur comment tooperform l’exploration de données, de modélisation et de calcul de score dans Spark 2.0 des clusters à l’aide de hello voyage de NYC Taxi et tarif-jeu de données décrit [ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Cet ordinateur portable peut être un bon point de départ pour Explorer rapidement le code de hello que nous fournissons à Spark 2.0. Pour un ordinateur portable plu analyse hello les données NYC Taxi, consultez bloc-notes suivant de hello dans cette liste. Consultez les remarques hello suit cette liste qui comparent ces ordinateurs portables. 
- [Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): ce fichier montre comment tooperform données ensuivirent (opérations Spark SQL et de la trame de données), exploration, de modélisation et de calcul de score à l’aide de hello voyage de NYC Taxi et tarif de jeu de données décrites [ ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): ce fichier montre comment tooperform données ensuivirent (opérations Spark SQL et de la trame de données), exploration, de modélisation et de calcul de score à l’aide de hello connu départ à temps de billet d’avion jeu de données à partir de 2011 et 2012. Nous l’intégration hello compagnie aérienne dataset avec hello aéroport météo (par exemple, vitesse du vent, la température, altitude, etc.) de données préalable toomodeling, ces fonctionnalités météo peuvent être incluses dans le modèle de hello.

<!-- -->

> [!NOTE]
> Hello compagnie aérienne dataset a été ajouté toohello Spark 2.0 blocs-notes toobetter illustrer l’utilisation de hello des algorithmes de classification. Consultez hello suivant les liens pour plus d’informations sur le jeu de données de départ de délais compagnie aérienne et jeu de données météo :

>- Données sur les départs à l’heure des compagnies aériennes : [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Données météorologiques des aéroports : [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
ordinateurs portables de Spark 2.0 Hello sur hello taxi de NYC et compagnie aérienne flight delay-jeux de données peuvent prendre 10 minutes ou plus toorun (selon la taille de votre cluster HDI de hello). Hello premier bloc-notes Bonjour au-dessus de liste affiche nombreux aspects d’exploration de données hello, ML de visualisation et de modèle d’apprentissage dans un ordinateur portable qui prend moins toorun temps avec échantillonnées en bas NYC jeu de données, dans quel hello taxi et tarif de fichiers ont été déjà joints : [ Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) ce bloc-notes prend une quantité plus court toofinish de temps (2 à 3 minutes) et peut être un bon point de départ pour Explorer rapidement le code de hello nous avons fourni pour Spark 2.0. 

<!-- -->

Pour obtenir des conseils sur à l’Opérationnalisation hello d’un modèle Spark 2.0 et la consommation de modèle pour calculer les scores, consultez hello [document Spark 1.6 sur la consommation](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) pour obtenir un exemple de mise en relief les étapes hello requises. toouse cela sur Spark 2.0, remplacez les fichier de code Python hello avec [ce fichier](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Composants requis
Hello procédures suivantes est associée tooSpark 1.6. Pour la version de hello Spark 2.0, utilisez hello blocs-notes décrivent et lié toopreviously. 

1. Vous devez avoir un abonnement Azure. Si vous n’en avez pas, consultez [Obtenir une version d’évaluation gratuite Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2. vous devez un toocomplete de cluster Spark 1.6 cette procédure pas à pas. toocreate, consultez les instructions hello fournies dans [mise en route : créer Apache Spark sur Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). type de cluster Hello et la version est spécifié à partir de hello **sélectionner le Type de Cluster** menu. 

![Configurer le cluster](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Pour une rubrique qui présente des tâches de toocomplete de Scala plutôt que de Python toouse pour un processus de science des données de bout en bout, consultez hello [Science des données à l’aide de Scala avec Spark sur Azure](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Hello les données NYC 2013 Taxi
Hello les données NYC Taxi voyage est d’environ 20 Go de fichiers de valeurs compressées séparées par des virgules (CSV) (non compressé en ~ 48 Go), qui comprend plus de 173 millions hello et des boucles tarifs payé pour chaque sortie. Chaque enregistrement de voyage comprend hello de prélèvement et emplacement de dépôt et l’heure, hack rendues anonymes (pilote) numéro de licence et nombre de medallion (id unique de taxi). les données de salutation couvre toutes les boucles dans l’année hello 2013 et sont fournies dans hello suivant deux jeux de données pour chaque mois :

1. les fichiers CSV Hello 'trip_data' contient les détails de voyage, telles que le nombre de personnes, récupèrent et cette chute pointe, déclenchement durée et la longueur de voyage. Voici quelques exemples d’enregistrements :
   
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

Nous avons pris un échantillon de 0,1 % de ces fichiers et de voyage de hello jointes\_données et voyage\_serrées les fichiers CSV dans un seul jeu de données toouse en tant que jeu de données d’entrée hello pour cette procédure pas à pas. voyage toojoin de clé unique de Hello\_données et voyage\_tarif est composée de champs de hello : medallion, hack\_certificat et pickup\_datetime. Chaque enregistrement du jeu de données hello contient hello suivant des attributs représentant un déplacement NYC Taxi :

| Champ | Brève description |
| --- | --- |
| medallion |Médaillon de taxi anonymisé (id unique de taxi) |
| hack_license |Numéro de licence Hackney Transport anonymisé |
| vendor_id |ID du fournisseur de taxi |
| rate_code |Tarification du taxi NYC |
| store_and_fwd_flag |Indicateur de stockage et de transmission |
| pickup_datetime |Date et heure de départ |
| dropoff_datetime |Date et heure d’arrivée |
| pickup_hour |Heure de départ |
| pickup_week |Choisir une semaine de l’année de hello |
| weekday |Jour de la semaine (de 1 à 7) |
| passenger_count |Nombre de passagers dans un trajet en taxi |
| trip_time_in_secs |Durée du trajet en secondes |
| trip_distance |Distance du trajet en miles |
| pickup_longitude |Longitude de départ |
| pickup_latitude |Latitude de départ |
| dropoff_longitude |Longitude d’arrivée |
| dropoff_latitude |Latitude d’arrivée |
| direct_distance |Distance directe entre les emplacements de départ et d’arrivée |
| payment_type |Type de paiement (espèces, carte de crédit, etc.). |
| fare_amount |Montant du trajet |
| surcharge |Surcharge |
| mta_tax |Taxe du MTA |
| tip_amount |Montant du pourboire |
| tolls_amount |Montant des péages |
| total_amount |Montant total |
| tipped |Pourboire payé (0/1 pour non ou oui) |
| tip_class |Classe de pourboire (0 : 0 $, 1 : 0-5 $ 2 : 6-10 $, 3 : 11 à 20 $, 4: 20 $ et +) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Exécutez le code à partir d’un bloc-notes jupyter sur cluster Spark de hello
Vous pouvez lancer hello bloc-notes Jupyter de hello portail Azure. Votre cluster Spark sur votre tableau de bord et cliquez sur cette page de gestion tooenter pour votre cluster. bloc-notes de hello tooopen associé hello Spark cluster, cliquez sur **tableaux de bord de Cluster** -> **bloc-notes Jupyter** .

![Tableaux de bord des clusters](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

Vous pouvez également parcourir trop***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello Notebook portables. Remplacer hello CLUSTERNAME de cette URL par nom hello de votre propre cluster. Vous avez besoin d’un mot de passe hello pour vos blocs-notes de hello admin compte tooaccess.

![Parcourez Jupyter Notebooks](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Sélectionnez PySpark toosee un répertoire qui contient quelques exemples d’ordinateurs portables prédéfinis qui utilisent hello PySpark API.hello portables qui contiennent des exemples de code hello pour cette suite de rubrique de Spark sont disponibles au [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Vous pouvez télécharger les blocs-notes hello directement à partir de [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello serveur de jupyter Notebook sur votre cluster Spark. Sur la page d’accueil hello de votre bloc-notes, cliquez sur hello **télécharger** bouton sur hello à droite dans le cadre de l’écran hello. Cette action ouvre un explorateur de fichiers. Vous pouvez coller des URL de GitHub (contenu brut) hello de hello bloc-notes, cliquez sur **ouvrir**. 

Vous voyez le nom de fichier hello sur votre liste de fichiers Notebook avec un **télécharger** bouton Nouveau. Cliquez sur ce bouton **Télécharger** . Maintenant, vous avez importé les bloc-notes hello. Répétez ces hello de tooupload étapes autres ordinateurs portables à partir de cette procédure pas à pas.

> [!TIP]
> Vous pouvez cliquer sur les liens hello sur votre navigateur, puis sélectionnez **copier le lien** tooget hello URL contenu brute de github. Vous pouvez coller cette URL dans hello Notebook Télécharger fichier boîte de dialogue correspondante.
> 
> 

Vous pouvez désormais :

* Consultez le code de hello en cliquant sur ordinateur portable de hello.
* Exécutez chaque cellule en appuyant sur **MAJ-ENTRÉE**.
* Exécuter le bloc-notes hello en cliquant sur **cellule** -> **exécuter**.
* Utiliser hello de visualisation automatique des requêtes.

> [!TIP]
> noyau de PySpark Hello visualise automatiquement sortie hello des requêtes SQL (HiveQL). Vous pouvez soit tooselect d’option hello entre différents types de visualisations (Table, à secteurs, ligne, zone ou barre) à l’aide de hello **Type** des boutons de menu dans le bloc-notes de hello :
> 
> 

![Courbe ROC de régression logistique pour une approche générique](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Et ensuite ?
Maintenant que vous sont configurés avec un cluster HDInsight Spark et que vous avez téléchargées blocs-notes de Notebook hello, vous êtes prêt toowork dans les rubriques hello qui correspondent toohello PySpark trois ordinateurs portables. Elles montrent comment tooexplore vos données et la procédure puis toocreate et utiliser des modèles. Hello avancé d’exploration de données et modélisation bloc-notes montre comment tooinclude la validation croisée, hyper-paramètre de balayage et évaluation du modèle. 

**Exploration de données et modélisation avec Spark :** Explorer hello le jeu de données, de créer, d’évaluer et d’évaluer les modèles d’apprentissage automatique hello en passant par hello [créer des modèles de classification et de régression binaire pour les données avec hello Spark Outils d’analyse MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) rubrique.

**La consommation de modèle :** toolearn comment créer des modèles de classification et la régression de hello tooscore dans cette rubrique, consultez [Score et évaluer les modèles d’apprentissage automatique de Spark intégrée](machine-learning-data-science-spark-model-consumption.md).

**Validation croisée et balayage hyperparamétrique**: consultez [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment effectuer la formation des modèles à l’aide de la validation croisée et du balayage hyperparamétrique

