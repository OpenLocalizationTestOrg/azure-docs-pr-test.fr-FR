---
title: "aaaData exploration et de modélisation avec Spark | Documents Microsoft"
description: "Présente hello d’exploration de données et modélisation des fonctionnalités du Kit de ressources hello MLlib de Spark sur Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="ad3b0-103">Exploration et modélisation des données avec Spark</span><span class="sxs-lookup"><span data-stu-id="ad3b0-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="ad3b0-104">Cette procédure pas à pas utilise l’exploration de données toodo HDInsight Spark et classification binaire et tâches sur un échantillon de hello NYC de modélisation de régression taxi voyage serrées 2013 le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="ad3b0-105">Il vous guide à travers les étapes de hello Hello [processus de science des données](http://aka.ms/datascienceprocess), de bout en bout, à l’aide d’un HDInsight Spark cluster pour le traitement et les modèles de données et hello hello toostore d’objets BLOB Azure.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="ad3b0-106">processus de Hello explore et visualise les données importées à partir d’un objet Blob de stockage Azure et prépare ensuite les modèles prédictifs hello données toobuild.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="ad3b0-107">Ces modèles sont build à l’aide de la classification binaire du toodo toolkit Spark MLlib hello et tâches de modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="ad3b0-108">Hello **classification binaire** tâche est toopredict ou non une info-bulle est payée pour le voyage de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="ad3b0-109">Hello **régression** tâche est toopredict hello Conseil hello basé sur d’autres fonctionnalités de l’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="ad3b0-110">Hello modèles que nous utilisons : régression logistique et linéaire, les forêts aléatoires et les arbres augmentés dégradés</span><span class="sxs-lookup"><span data-stu-id="ad3b0-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="ad3b0-111">[La régression linéaire avec SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) est un modèle de régression linéaire qui utilise une méthode de descente Gradient stochastique (SGD) et pour l’optimisation et la fonctionnalité de mise à l’échelle des montants de conseil toopredict hello payé.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="ad3b0-112">[La régression logistique avec LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou la régression « logit », est un modèle de régression qui peut être utilisé lors de la variable dépendante de hello est la classification des données catégorielles toodo.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="ad3b0-113">LBFGS est un algorithme d’optimisation quasi Newton qui rapproche algorithme Broyden – Fletcher – Goldfarb – Shanno (BFGS) de hello à l’aide d’une quantité limitée de mémoire de l’ordinateur, qui est largement utilisé dans l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="ad3b0-114">[forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="ad3b0-115">Combiner des nombreux decision trees tooreduce hello des risques de dépassement de.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="ad3b0-116">Forêts aléatoires sont utilisés pour la classification et de régression et peuvent gérer les fonctionnalités catégorielles et peuvent être étendus de paramètre de classification multiclasse toohello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="ad3b0-117">Ils ne nécessitent pas la fonctionnalité mise à l’échelle et sont en mesure de toocapture non linéarité et interactions de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="ad3b0-118">Forêts aléatoires sont un des hello plus de succès d’apprentissage des modèles pour la classification et la régression.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="ad3b0-119">[Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="ad3b0-120">Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="ad3b0-121">GBTs sont utilisés pour la classification et de régression et peut gérer les fonctionnalités catégorielles, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="ad3b0-122">Ils s’utilisent également dans le paramétrage de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="ad3b0-123">étapes de modélisation Hello également contient de code montrant comment tootrain, évaluer et enregistrer chaque type de modèle.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="ad3b0-124">Python a été utilisé toocode hello solution et tooshow hello applique les tracés.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="ad3b0-125">Bien que hello Spark MLlib toolkit est conçu toowork sur les jeux de données volumineux, un exemple relativement faible (à l’aide de K 170 lignes, environ 0,1 % du jeu de données hello d’origine NYC en ~ 30 Mo) est utilisé ici pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="ad3b0-126">exercice Hello donné ici s’exécute efficacement (en environ 10 minutes) sur un cluster HDInsight avec 2 nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="ad3b0-127">Hello même code avec des modifications mineures, peut être utilisé tooprocess-jeux de données volumineux, avec les changements appropriés pour la mise en cache des données en mémoire et la modification de la taille de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ad3b0-128">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ad3b0-128">Prerequisites</span></span>
<span data-ttu-id="ad3b0-129">Vous avez besoin d’un compte Azure et un Spark 1.6 (ou Spark 2.0) du cluster HDInsight toocomplete cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="ad3b0-130">Consultez hello [vue d’ensemble de science des données à l’aide de Spark sur Azure HDInsight](machine-learning-data-science-spark-overview.md) pour obtenir des instructions sur la façon de toosatisfy ces exigences.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="ad3b0-131">Cette rubrique contient également une description de type hello données NYC 2013 Taxi utilisées ici et obtenir des instructions sur la façon dont tooexecute code à partir d’un bloc-notes jupyter sur cluster Spark de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="ad3b0-132">Clusters et notebooks Spark</span><span class="sxs-lookup"><span data-stu-id="ad3b0-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="ad3b0-133">Les étapes de configuration et le code fournis dans cette procédure pas à pas concernent HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="ad3b0-134">Mais des notebooks Jupyter sont fournis pour les clusters HDInsight Spark 1.6 et Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="ad3b0-135">Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="ad3b0-136">En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="ad3b0-137">Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="ad3b0-138">Pour des raisons pratiques, voici les liens hello blocs-notes de Notebook toohello pour Spark 1.6 (toobe exécuter dans le noyau pySpark hello Hello server de bloc-notes Jupyter) et Spark 2.0 (toobe exécuter dans le noyau pySpark3 hello Hello server de bloc-notes Jupyter) :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="ad3b0-139">Notebooks Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="ad3b0-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="ad3b0-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fournit des informations sur l’exploration de données tooperform, de modélisation et de calcul de score avec plusieurs algorithmes différents.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="ad3b0-141">Notebooks Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="ad3b0-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="ad3b0-142">tâches de classification et de régression Hello qui sont implémentées à l’aide d’un cluster Spark 2.0 se trouvent dans les blocs-notes et portable de classification hello utilise un autre jeu de données :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="ad3b0-143">[Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ce fichier fournit des informations sur comment tooperform l’exploration de données, de modélisation et de calcul de score dans Spark 2.0 des clusters à l’aide de hello voyage de NYC Taxi et tarif-jeu de données décrit [ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="ad3b0-144">Cet ordinateur portable peut être un bon point de départ pour Explorer rapidement le code de hello que nous fournissons à Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="ad3b0-145">Pour un ordinateur portable plu analyse hello les données NYC Taxi, consultez bloc-notes suivant de hello dans cette liste.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="ad3b0-146">Consultez les remarques hello suit cette liste qui comparent ces ordinateurs portables.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="ad3b0-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): ce fichier montre comment tooperform données ensuivirent (opérations Spark SQL et de la trame de données), exploration, de modélisation et de calcul de score à l’aide de hello voyage de NYC Taxi et tarif de jeu de données décrites [ ici](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="ad3b0-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): ce fichier montre comment tooperform données ensuivirent (opérations Spark SQL et de la trame de données), exploration, de modélisation et de calcul de score à l’aide de hello connu départ à temps de billet d’avion jeu de données à partir de 2011 et 2012.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="ad3b0-149">Nous l’intégration hello compagnie aérienne dataset avec hello aéroport météo (par exemple, vitesse du vent, la température, altitude, etc.) de données préalable toomodeling, ces fonctionnalités météo peuvent être incluses dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="ad3b0-150">Hello compagnie aérienne dataset a été ajouté toohello Spark 2.0 blocs-notes toobetter illustrer l’utilisation de hello des algorithmes de classification.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="ad3b0-151">Consultez hello suivant les liens pour plus d’informations sur le jeu de données de départ de délais compagnie aérienne et jeu de données météo :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="ad3b0-152">Données sur les départs à l’heure des compagnies aériennes : [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="ad3b0-153">Données météorologiques des aéroports : [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="ad3b0-154">ordinateurs portables de Spark 2.0 Hello sur hello taxi de NYC et compagnie aérienne flight delay-jeux de données peuvent prendre 10 minutes ou plus toorun (selon la taille de votre cluster HDI de hello).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="ad3b0-155">Hello premier bloc-notes Bonjour au-dessus de liste affiche nombreux aspects d’exploration de données hello, ML de visualisation et de modèle d’apprentissage dans un ordinateur portable qui prend moins toorun temps avec échantillonnées en bas NYC jeu de données, dans quel hello taxi et tarif de fichiers ont été déjà joints : [ Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) ce bloc-notes prend une quantité plus court toofinish de temps (2 à 3 minutes) et peut être un bon point de départ pour Explorer rapidement le code de hello nous avons fourni pour Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="ad3b0-156">descriptions Hello suivantes sont associée toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="ad3b0-157">Pour les versions Spark 2.0, utilisez les blocs-notes hello décrite et lien indiqué plus haut.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="ad3b0-158">Le programme d’installation : hello, les bibliothèques et les emplacements de stockage prédéfinir le contexte de Spark</span><span class="sxs-lookup"><span data-stu-id="ad3b0-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="ad3b0-159">Spark est en mesure de tooAzure de tooread et écriture objet Blob de stockage (également appelé WASB).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="ad3b0-160">Par conséquent, vos données existantes qui y sont stockées peuvent être traitées à l’aide de Spark et hello stockées dans WASB des résultats.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="ad3b0-161">toosave modèles ou les fichiers dans WASB, chemin d’accès hello doit toobe correctement spécifiée.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="ad3b0-162">Hello du cluster Spark toohello conteneur attaché par défaut peut être référencé à l’aide d’un chemin commençant par : « wasb : / / ».</span><span class="sxs-lookup"><span data-stu-id="ad3b0-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="ad3b0-163">Les autres emplacements sont référencés par wasb://.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="ad3b0-164">Définir les chemins d’accès aux emplacements de stockage dans WASB</span><span class="sxs-lookup"><span data-stu-id="ad3b0-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="ad3b0-165">exemple de code suivant Hello spécifie emplacement hello de hello toobe de données en lecture et chemin d’accès de hello pour hello modèle stockage toowhich hello modèle de sortie est enregistré :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="ad3b0-166">Importer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="ad3b0-166">Import libraries</span></span>
<span data-ttu-id="ad3b0-167">Le programme d’installation nécessite également l’importation des bibliothèques nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="ad3b0-168">Définir le contexte de spark et importer des bibliothèques nécessaires avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-168">Set spark context and import necessary libraries with hello following code:</span></span>

    # IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="ad3b0-169">Contexte Spark prédéfini et commandes magiques PySpark</span><span class="sxs-lookup"><span data-stu-id="ad3b0-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="ad3b0-170">noyaux PySpark Hello qui sont fournis avec les ordinateurs portables Notebook ont un contexte prédéfini.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="ad3b0-171">Par conséquent, il est inutile tooset hello Spark ou ruche contextes explicitement avant de commencer à utiliser avec l’application hello que vous développez.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="ad3b0-172">Ces contextes sont disponibles pour vous par défaut.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-172">These contexts are available for you by default.</span></span> <span data-ttu-id="ad3b0-173">Ces contextes sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-173">These contexts are:</span></span>

* <span data-ttu-id="ad3b0-174">sc : pour Spark</span><span class="sxs-lookup"><span data-stu-id="ad3b0-174">sc - for Spark</span></span> 
* <span data-ttu-id="ad3b0-175">sqlContext : pour Hive</span><span class="sxs-lookup"><span data-stu-id="ad3b0-175">sqlContext - for Hive</span></span>

<span data-ttu-id="ad3b0-176">Hello PySpark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec %%.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="ad3b0-177">Deux de ces commandes sont utilisées dans ces exemples de code.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="ad3b0-178">**%% local** Spécifie que le code hello dans les lignes suivantes est toobe exécutée localement.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="ad3b0-179">Le code doit être du code Python valide.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="ad3b0-180">**%% -o sql <variable name>**  exécute une requête Hive sur hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="ad3b0-181">Si le paramètre -o de hello est transmis, résultat hello de requête de hello est conservé dans hello %% contexte Python local en tant qu’une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="ad3b0-182">Pour plus d’informations sur les noyaux hello pour notebook blocs-notes et hello prédéfinies « magics » qui elles fournissent, consultez [clusters de noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="ad3b0-183">Ingestion de données à partir d’un objet blob public</span><span class="sxs-lookup"><span data-stu-id="ad3b0-183">Data ingestion from public blob</span></span>
<span data-ttu-id="ad3b0-184">première étape de Hello dans le processus de science des données hello est tooingest hello données toobe analysée à partir de sources d’où est réside dans votre environnement de modélisation et exploration de données.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="ad3b0-185">environnement de Hello est Spark dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="ad3b0-186">Cette section contient des toocomplete de code hello une série de tâches :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="ad3b0-187">réception hello données exemple toobe modélisée</span><span class="sxs-lookup"><span data-stu-id="ad3b0-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="ad3b0-188">lire dans le jeu de données d’entrée hello (stockée sous la forme d’un fichier .tsv)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="ad3b0-189">format et hello nettoyer les données</span><span class="sxs-lookup"><span data-stu-id="ad3b0-189">format and clean hello data</span></span>
* <span data-ttu-id="ad3b0-190">créer et mettre en cache des objets (RDD ou trames de données) en mémoire</span><span class="sxs-lookup"><span data-stu-id="ad3b0-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="ad3b0-191">enregistrer les données en tant que table temporaire dans le contexte SQL.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="ad3b0-192">Voici le code hello pour l’ingestion de données.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="ad3b0-193">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-193">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-194">Temps nécessaire tooexecute au-dessus de la cellule : 51.72 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="ad3b0-195">Exploration et visualisation de données</span><span class="sxs-lookup"><span data-stu-id="ad3b0-195">Data exploration & visualization</span></span>
<span data-ttu-id="ad3b0-196">Une fois les données de salutation a été placées dans Spark, hello étape suivante dans le processus de science des données hello est toogain une meilleure compréhension des données hello via l’exploration et visualisation.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="ad3b0-197">Dans cette section, nous examiner les données de taxi hello à l’aide de requêtes SQL et des variables de traçage hello cibles et des fonctionnalités potentiels pour l’examen visuel.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="ad3b0-198">Plus précisément, nous tracer fréquence hello passagers des nombres de dans taxi allers-retours, hello fréquence de quantités d’info-bulle, et comment les conseils varient selon le type et le montant du paiement.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="ad3b0-199">Tracer un histogramme de fréquences d’inventaire passagers dans l’exemple hello de déplacements de taxi</span><span class="sxs-lookup"><span data-stu-id="ad3b0-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="ad3b0-200">Ce code et les extraits de code suivants utilisent SQL tooquery magique hello, exemple et les données de hello de tooplot magique local.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="ad3b0-201">**Magique SQL (`%%sql`)** hello HDInsight PySpark noyau prend en charge easy inline HiveQL requêtes contre hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="ad3b0-202">Hello (-o nom_variable) argument persiste sortie hello de la requête SQL hello en tant qu’une trame de données Pandas sur le serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="ad3b0-203">Cela signifie qu’il est disponible en mode local de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="ad3b0-204">Hello  **`%%local` magique** est toorun du code utilisé localement sur le serveur hello Notebook, qui est le nœud principal de hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="ad3b0-205">En général, vous utilisez `%%local` magique conjointement avec hello `%%sql` magique avec le paramètre -o.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="ad3b0-206">paramètre de Hello -o soit persistant sortie hello de requête SQL hello localement, puis %% magic local déclencherait hello prochain jeu de toorun d’extrait de code localement par rapport à la sortie hello de requêtes SQL hello rendue persistante localement</span><span class="sxs-lookup"><span data-stu-id="ad3b0-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="ad3b0-207">Hello sortie est automatiquement affichée après l’exécution de code de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="ad3b0-208">Cette requête extrait les allers-retours hello par nombre de passagers.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="ad3b0-209">Ce code crée une trame de données locale à partir de la sortie de la requête hello et trace les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="ad3b0-210">Hello `%%local` magique crée une trame de données locale, `sqlResults`, qui peut être utilisé pour le traçage avec matplotlib.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad3b0-211">Cette commande magique PySpark est utilisée plusieurs fois lors de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="ad3b0-212">Si la quantité de hello de données est importante, vous devez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="ad3b0-213">Voici allers-retours de hello hello code tooplot par passager nombres</span><span class="sxs-lookup"><span data-stu-id="ad3b0-213">Here is hello code tooplot hello trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="ad3b0-214">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-214">**OUTPUT:**</span></span>

![Fréquence des voyages par nombre de passagers](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="ad3b0-216">Vous pouvez sélectionner parmi les différents types de visualisations (Table, à secteurs, ligne, zone ou barre) à l’aide de hello **Type** des boutons de menu dans le bloc-notes de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="ad3b0-217">traçage de barre Hello est indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="ad3b0-218">Tracez un histogramme du montant des pourboires et montrez comment le montant du pourboire varie selon le nombre de passagers et le montant des trajets.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="ad3b0-219">Utilisez une données toosample de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped 
    FROM taxi_train 
    WHERE passenger_count > 0 
    AND passenger_count < 7 
    AND fare_amount > 0 
    AND fare_amount < 200 
    AND payment_type in ('CSH', 'CRD') 
    AND tip_amount > 0 
    AND tip_amount < 25


<span data-ttu-id="ad3b0-220">Cette cellule de code utilise hello SQL interroger toocreate trois graphiques hello des données.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="ad3b0-221">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-221">**OUTPUT:**</span></span> 

![Distribution des montants de pourboire](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="ad3b0-225">Conception des caractéristiques, transformation et préparation des données à modéliser</span><span class="sxs-lookup"><span data-stu-id="ad3b0-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="ad3b0-226">Cette section décrit et fournit le code hello pour les procédures utilisées tooprepare données pour une utilisation dans la modélisation de ML.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="ad3b0-227">Il montre des tâches de hello toodo suivant :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="ad3b0-228">Créer une caractéristique en regroupant les heures dans des périodes de trafic</span><span class="sxs-lookup"><span data-stu-id="ad3b0-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="ad3b0-229">Indexer et encoder des fonctionnalités catégorielles</span><span class="sxs-lookup"><span data-stu-id="ad3b0-229">Index and encode categorical features</span></span>
* <span data-ttu-id="ad3b0-230">Créer des objets point étiquetés à intégrer dans les fonctions ML</span><span class="sxs-lookup"><span data-stu-id="ad3b0-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="ad3b0-231">Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test</span><span class="sxs-lookup"><span data-stu-id="ad3b0-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="ad3b0-232">Mise à l’échelle des caractéristiques</span><span class="sxs-lookup"><span data-stu-id="ad3b0-232">Feature scaling</span></span>
* <span data-ttu-id="ad3b0-233">Mettre en cache des objets en mémoire</span><span class="sxs-lookup"><span data-stu-id="ad3b0-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="ad3b0-234">Créer une caractéristique en regroupant les heures dans des périodes de trafic</span><span class="sxs-lookup"><span data-stu-id="ad3b0-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="ad3b0-235">Ce code montre comment les compartiments de toocreate une nouvelle fonctionnalité par le placement des heures dans le temps de trafic, puis comment toocache hello résultant trame de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="ad3b0-236">Où résilient Distributed jeux de données (RDDs) et les trames de données sont utilisés à plusieurs reprises, mise en cache entraîne des temps d’exécution tooimproved.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="ad3b0-237">En conséquence, nous le cache RDDs trames de données à plusieurs étapes dans la procédure pas à pas hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="ad3b0-238">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-238">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3b0-239">126050</span><span class="sxs-lookup"><span data-stu-id="ad3b0-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="ad3b0-240">Indexer et encoder les caractéristiques catégorielles à intégrer dans les fonctions de modélisation</span><span class="sxs-lookup"><span data-stu-id="ad3b0-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="ad3b0-241">Cette section montre comment tooindex ou coder des fonctionnalités par catégorie pour l’entrée en hello modélisation des fonctions.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="ad3b0-242">modélisation de Hello et prédire les fonctions de MLlib requièrent des fonctionnalités avec les données d’entrée catégorielles toobe indexé ou codé toouse préalable.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="ad3b0-243">Selon le modèle de hello, tooindex ou que vous les codez de différentes façons :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="ad3b0-244">**Basé sur l’arborescence de modélisation** requiert toobe catégories encodé sous la forme des valeurs numériques (par exemple, une fonctionnalité avec trois catégories peut-être être encodée avec 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="ad3b0-245">C’est ce que permet la fonction [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) de MLlib.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="ad3b0-246">Cette fonction encode une colonne de chaîne de colonne d’étiquettes de tooa d’indices d’étiquette qui sont classés par fréquence d’étiquette.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="ad3b0-247">Bien qu’il est indexé par des valeurs numériques pour l’entrée et la gestion des données, les algorithmes d’arbre hello peuvent être spécifié tootreat leur correctement en tant que catégories.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="ad3b0-248">**Modèles de logistique et de régression linéaire** requièrent à chaud de celui de codage, où, par exemple, une fonctionnalité avec trois catégories peut être développée dans les trois colonnes de fonctionnalités, avec chaque conteneur 0 ou 1 selon la catégorie hello d’une observation.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="ad3b0-249">Fournit des MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo à chaud un encodage de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="ad3b0-250">Cet encodeur est mappé à une colonne de la colonne de tooa étiquette indices de vecteurs binaire, au maximum une seule une valeur.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="ad3b0-251">Cet encodage permet d’algorithmes qui attendent des fonctionnalités de valeurs numériques, telles que la régression logistique, fonctionnalités de toocategorical toobe appliqué.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="ad3b0-252">Voici hello code tooindex et coder les fonctionnalités par catégorie :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-253">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-253">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-254">Temps nécessaire tooexecute au-dessus de la cellule : 1,28 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="ad3b0-255">Créer des objets point étiquetés à intégrer dans les fonctions ML</span><span class="sxs-lookup"><span data-stu-id="ad3b0-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="ad3b0-256">Cette section contient le code qui montre comment les données de texte catégorielles tooindex au point étiqueté les données de type et coder afin qu’il puisse être utilisé tootrain et test MLlib régression logistique et autres modèles de classification.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="ad3b0-257">Les objets point étiquetés sont des jeux de données distribués résilients (RDD) mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes ML dans MLlib.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="ad3b0-258">Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="ad3b0-259">Cette section contient le code qui montre comment tooindex les données de texte par catégorie comme un [intitulée point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) type de données et les encoder afin qu’il puisse être utilisé tootrain et test MLlib régression logistique et autres modèles de classification.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="ad3b0-260">Les objets point étiquetés sont des jeux de données distribués résilients (RDD) composés d’un libellé (variable cible/réponse) et du vecteur de caractéristique.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="ad3b0-261">Ce format est nécessaire en entrée par de nombreux algorithmes ML de MLlib.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="ad3b0-262">Voici hello tooindex de code et de coder des fonctionnalités de texte pour la classification binaire.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="ad3b0-263">Voici les fonctionnalités catégorielles texte tooencode et d’index pour l’analyse de régression linéaire de code hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])

        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="ad3b0-264">Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test</span><span class="sxs-lookup"><span data-stu-id="ad3b0-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="ad3b0-265">Ce code crée un échantillonnage aléatoire de données hello (25 % est utilisé ici).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="ad3b0-266">Bien qu’il n’est pas requis pour cet exemple en raison de la taille de toohello du jeu de données hello, nous allons montrer comment vous pouvez échantillonner ici afin de savoir comment toouse pour votre propre problème si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="ad3b0-267">Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="ad3b0-268">Ensuite, nous fractionner les exemple hello en une partie de la formation (75 % ici) et un test toouse de partie (25 % ici) dans la classification et la modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-269">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-269">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-270">Temps nécessaire tooexecute au-dessus de la cellule : pas de 0,24 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="ad3b0-271">Mise à l’échelle des caractéristiques</span><span class="sxs-lookup"><span data-stu-id="ad3b0-271">Feature scaling</span></span>
<span data-ttu-id="ad3b0-272">Fonctionnalité mise à l’échelle, également appelé normalisation des données, ainsi que des fonctionnalités avec des valeurs largement dispersées sont pas donné excessive peser en fonction de l’objectif hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="ad3b0-273">code de mise à l’échelle d’une fonctionnalité Hello utilise hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variance de toounit fonctionnalités tooscale hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="ad3b0-274">MLlib le fournit en vue d’une utilisation dans une régression linéaire avec SGD (Stochastic Gradient Descent), un algorithme populaire permettant de former une large gamme d’autres modèles Machine Learning, tels que les régressions régularisées ou les machines à vecteurs de support (SVM).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="ad3b0-275">Nous avons trouvé hello LinearRegressionWithSGD algorithme toobe toofeature sensibles mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="ad3b0-276">Voici les variables de tooscale code hello pour une utilisation avec l’algorithme SGD hello régularisée linéaire.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-277">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-277">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-278">Temps nécessaire tooexecute au-dessus de la cellule : 13.17 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="ad3b0-279">Mettre en cache des objets en mémoire</span><span class="sxs-lookup"><span data-stu-id="ad3b0-279">Cache objects in memory</span></span>
<span data-ttu-id="ad3b0-280">Hello temps d’apprentissage et test des algorithmes de ML peuvent être réduits en mettant en cache des objets d’image de données d’entrée hello utilisés pour la classification, la régression, et les fonctionnalités de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-281">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-281">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3b0-282">Temps nécessaire tooexecute au-dessus de la cellule : secondes environ 0,15</span><span class="sxs-lookup"><span data-stu-id="ad3b0-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="ad3b0-283">Prédire si un pourboire a été payé avec des modèles de classification binaires</span><span class="sxs-lookup"><span data-stu-id="ad3b0-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="ad3b0-284">Cette section montre comment utiliser trois modèles pour la tâche de classification binaire hello de prédiction ou non une info-bulle est payée pour un voyage taxi.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="ad3b0-285">les modèles Hello présentées sont :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-285">hello models presented are:</span></span>

* <span data-ttu-id="ad3b0-286">Régression logistique régularisée</span><span class="sxs-lookup"><span data-stu-id="ad3b0-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="ad3b0-287">Modèle de forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="ad3b0-287">Random forest model</span></span>
* <span data-ttu-id="ad3b0-288">Arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="ad3b0-289">Chaque section de code générateur de modèle est divisée en étapes :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="ad3b0-290">**formation du modèle** avec un jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="ad3b0-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="ad3b0-291">**Évaluation de modèle** sur un jeu de données de test avec mesures</span><span class="sxs-lookup"><span data-stu-id="ad3b0-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="ad3b0-292">**Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure</span><span class="sxs-lookup"><span data-stu-id="ad3b0-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="ad3b0-293">Classification par régression logistique</span><span class="sxs-lookup"><span data-stu-id="ad3b0-293">Classification using logistic regression</span></span>
<span data-ttu-id="ad3b0-294">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) qui prédit ou non une info-bulle est payée pour un voyage dans le jeu de données hello NYC taxi voyage et tarif.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="ad3b0-295">**L’apprentissage du modèle de régression logistique hello à l’aide de CV et hyperparameter balayage**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="ad3b0-296">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-296">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3b0-297">Coefficients : [0,0082065285375, -0,0223675576104, -0,0183812028036, -3.48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="ad3b0-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="ad3b0-298">Interception : -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="ad3b0-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="ad3b0-299">Temps nécessaire tooexecute au-dessus de la cellule : 14.43 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="ad3b0-300">**Évaluation du modèle de classification binaire hello avec métriques standard**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-300">**Evaluate hello binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="ad3b0-301">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-301">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3b0-302">Zone sous PR = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="ad3b0-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="ad3b0-303">Zone sous ROC = 0,983714670256</span><span class="sxs-lookup"><span data-stu-id="ad3b0-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="ad3b0-304">Résumé des statistiques</span><span class="sxs-lookup"><span data-stu-id="ad3b0-304">Summary Stats</span></span>

<span data-ttu-id="ad3b0-305">Précision = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="ad3b0-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="ad3b0-306">Rappel = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="ad3b0-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="ad3b0-307">Score F1 = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="ad3b0-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="ad3b0-308">Temps nécessaire tooexecute au-dessus de la cellule : 57.61 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="ad3b0-309">**Tracer la courbe ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="ad3b0-310">Hello *predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="ad3b0-311">*tmp_results* peuvent être utilisés toodo requêtes et produit des résultats dans hello sqlResults-trame de données pour le traçage.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="ad3b0-312">Voici le code de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="ad3b0-313">Voici des prédictions toomake de code hello et hello de traçage ROC la courbe.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="ad3b0-314">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="ad3b0-316">Classification par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="ad3b0-316">Random forest classification</span></span>
<span data-ttu-id="ad3b0-317">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de forêt aléatoire qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-318">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-318">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-319">Zone sous ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="ad3b0-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="ad3b0-320">Temps nécessaire tooexecute au-dessus de la cellule : 31.09 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="ad3b0-321">Classification par arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="ad3b0-322">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="ad3b0-323">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-323">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-324">Zone sous ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="ad3b0-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="ad3b0-325">Temps nécessaire tooexecute au-dessus de la cellule : 19.76 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="ad3b0-326">Prédire le montant des pourboires de courses de taxi avec les modèles de régression</span><span class="sxs-lookup"><span data-stu-id="ad3b0-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="ad3b0-327">Cette section montre comment utiliser trois modèles pour la tâche de régression hello de prévoir hello de conseil hello payée pour un trajet taxi basé sur d’autres fonctionnalités de l’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="ad3b0-328">les modèles Hello présentées sont :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-328">hello models presented are:</span></span>

* <span data-ttu-id="ad3b0-329">Régression linéaire régularisée</span><span class="sxs-lookup"><span data-stu-id="ad3b0-329">Regularized linear regression</span></span>
* <span data-ttu-id="ad3b0-330">Forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="ad3b0-330">Random forest</span></span>
* <span data-ttu-id="ad3b0-331">Arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="ad3b0-332">Ces modèles ont été décrites dans l’introduction de hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-332">These models were described in hello introduction.</span></span> <span data-ttu-id="ad3b0-333">Chaque section de code générateur de modèle est divisée en étapes :</span><span class="sxs-lookup"><span data-stu-id="ad3b0-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="ad3b0-334">**formation du modèle** avec un jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="ad3b0-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="ad3b0-335">**Évaluation de modèle** sur un jeu de données de test avec mesures</span><span class="sxs-lookup"><span data-stu-id="ad3b0-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="ad3b0-336">**Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure</span><span class="sxs-lookup"><span data-stu-id="ad3b0-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="ad3b0-337">régression linéaire avec SGD</span><span class="sxs-lookup"><span data-stu-id="ad3b0-337">Linear regression with SGD</span></span>
<span data-ttu-id="ad3b0-338">Hello code dans cette section montre comment toouse à l’échelle fonctionnalités tootrain une régression linéaire qui utilise la descente de gradient stochastique (SGD) pour l’optimisation, et comment tooscore, évaluer et enregistrer le modèle de hello dans le stockage des objets Blob Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="ad3b0-339">Dans notre expérience, il peut y avoir des problèmes avec convergence hello de modèles de LinearRegressionWithSGD, et les paramètres doivent toobe modifié/optimisée avec soin pour obtenir un modèle valid.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="ad3b0-340">La mise à l’échelle des variables est très utile avec la convergence.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-341">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-341">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-342">Coefficients : [0,00457675809917, -0,0226314167349, -0,0191910355236, 0,246793409578, 0,312047890459, 0,359634405999, 0,00928692253981, -0,000987181489428, -0,0888306617845, 0,0569376211553, 0,115519551711, 0,149250164995, -0,00990211159703, -0,00637410344522, 0,545083566179, -0,536756072402, 0,0105762393099, -0,0130117577055, 0,0129304737772, -0,00171065945959]</span><span class="sxs-lookup"><span data-stu-id="ad3b0-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="ad3b0-343">Interception : -0,853872718283</span><span class="sxs-lookup"><span data-stu-id="ad3b0-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="ad3b0-344">RMSE = 1,24190115863</span><span class="sxs-lookup"><span data-stu-id="ad3b0-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="ad3b0-345">Racine carrée = 0,608017146081</span><span class="sxs-lookup"><span data-stu-id="ad3b0-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="ad3b0-346">Temps nécessaire tooexecute au-dessus de la cellule : 58,42 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="ad3b0-347">Régression par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="ad3b0-347">Random Forest regression</span></span>
<span data-ttu-id="ad3b0-348">code Hello dans cette section montre comment tootrain, évaluer et enregistrer une régression de forêt aléatoire qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-349">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-349">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-350">RMSE = 0,891209218139</span><span class="sxs-lookup"><span data-stu-id="ad3b0-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="ad3b0-351">Racine carrée = 0,759661334921</span><span class="sxs-lookup"><span data-stu-id="ad3b0-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="ad3b0-352">Temps nécessaire tooexecute au-dessus de la cellule : 49.21 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="ad3b0-353">Régression par arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="ad3b0-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="ad3b0-354">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="ad3b0-355">**Former et évaluer**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3b0-356">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-356">**OUTPUT:**</span></span>

<span data-ttu-id="ad3b0-357">RMSE = 0,908473148639</span><span class="sxs-lookup"><span data-stu-id="ad3b0-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="ad3b0-358">Racine carrée = 0,753835096681</span><span class="sxs-lookup"><span data-stu-id="ad3b0-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="ad3b0-359">Temps nécessaire tooexecute au-dessus de la cellule : 34.52 secondes</span><span class="sxs-lookup"><span data-stu-id="ad3b0-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="ad3b0-360">**Tracer**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-360">**Plot**</span></span>

<span data-ttu-id="ad3b0-361">*tmp_results* est inscrit comme une table Hive dans la cellule précédente hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="ad3b0-362">Les résultats à partir de la table de hello s’affichent dans hello *sqlResults* trame de données pour le traçage.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="ad3b0-363">Voici le code de hello</span><span class="sxs-lookup"><span data-stu-id="ad3b0-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="ad3b0-364">Voici hello code tooplot les données de salutation à l’aide du serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="ad3b0-365">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="ad3b0-367">Nettoyage d’objets de la mémoire</span><span class="sxs-lookup"><span data-stu-id="ad3b0-367">Clean up objects from memory</span></span>
<span data-ttu-id="ad3b0-368">Utilisez `unpersist()` toodelete les objets mis en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="ad3b0-369">Enregistrement des emplacements de stockage des modèles de hello pour la consommation et le score</span><span class="sxs-lookup"><span data-stu-id="ad3b0-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="ad3b0-370">tooconsume et score un jeu de données indépendant décrit dans hello [Score et évaluer des modèles d’apprentissage automatique intégrée Spark](machine-learning-data-science-spark-model-consumption.md) rubrique, vous devez toocopy et coller contenant hello enregistré les modèles créés ici dans hello des noms de ces fichiers Bloc-notes jupyter de consommation.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="ad3b0-371">Voici tooprint de code hello out hello chemins toomodel fichiers que vous devez il.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="ad3b0-372">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="ad3b0-372">**OUTPUT**</span></span>

<span data-ttu-id="ad3b0-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="ad3b0-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="ad3b0-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="ad3b0-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="ad3b0-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="ad3b0-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="ad3b0-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="ad3b0-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="ad3b0-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="ad3b0-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="ad3b0-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="ad3b0-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="ad3b0-379">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="ad3b0-379">What's next?</span></span>
<span data-ttu-id="ad3b0-380">Maintenant que vous avez créé des modèles de classification et de régression par hello Spark MlLib, vous êtes prêt toolearn comment tooscore et évaluer ces modèles.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="ad3b0-381">Bonjour avancé d’exploration de données et de modélisation tels que le bloc-notes plus approfondie en y compris la validation croisée, hyper-paramètre de balayage des et d’évaluation de modèle.</span><span class="sxs-lookup"><span data-stu-id="ad3b0-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="ad3b0-382">**La consommation de modèle :** toolearn comment tooscore et évaluer les modèles de classification et de régression hello créés dans cette rubrique, consultez [Score et évaluer les modèles d’apprentissage automatique de Spark intégrée](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="ad3b0-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="ad3b0-383">**Validation croisée et balayage hyperparamétrique**: consultez [Exploration et modélisation avancées des données avec Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) pour savoir comment effectuer la formation des modèles à l’aide de la validation croisée et du balayage hyperparamétrique</span><span class="sxs-lookup"><span data-stu-id="ad3b0-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

