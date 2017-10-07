---
title: "aaaAdvanced l’exploration de données et de modélisation avec Spark | Documents Microsoft"
description: "Utiliser l’exploration de données toodo HDInsight Spark et l’apprentissage des modèles de classification et de régression binaire à l’aide de l’optimisation de la validation croisée et hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="7b6aa-103">Modélisation et exploration avancées des données avec Spark</span><span class="sxs-lookup"><span data-stu-id="7b6aa-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="7b6aa-104">Cette procédure pas à pas utilise HDInsight Spark toodo exploration et train binaire classification des données et les modèles de régression à l’aide de la validation croisée et optimisation hyperparameter sur un échantillon de hello NYC taxi voyage serrées 2013 le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="7b6aa-105">Il vous guide à travers les étapes de hello Hello [processus de science des données](http://aka.ms/datascienceprocess), de bout en bout, à l’aide d’un HDInsight Spark cluster pour le traitement et les modèles de données et hello hello toostore d’objets BLOB Azure.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="7b6aa-106">processus de Hello explore et visualise les données importées à partir d’un objet Blob de stockage Azure et prépare ensuite les modèles prédictifs hello données toobuild.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="7b6aa-107">Python a été utilisé toocode hello solution et tooshow hello applique les tracés.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="7b6aa-108">Ces modèles sont build à l’aide de la classification binaire du toodo toolkit Spark MLlib hello et tâches de modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="7b6aa-109">Hello **classification binaire** tâche est toopredict ou non une info-bulle est payée pour le voyage de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="7b6aa-110">Hello **régression** tâche est toopredict hello Conseil hello basé sur d’autres fonctionnalités de l’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="7b6aa-111">étapes de modélisation Hello également contient de code montrant comment tootrain, évaluer et enregistrer chaque type de modèle.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="7b6aa-112">Hello rubrique traite des hello même sol comme hello [exploration de données et modélisation avec Spark](machine-learning-data-science-spark-data-exploration-modeling.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="7b6aa-113">Mais il est plus « avancé » car elle utilise également la validation croisée avec hyperparameter balayage tootrain des modèles de classification et de régression précis de façon optimale.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="7b6aa-114">**La validation croisée (VC)** est une technique qui évalue la manière dont un modèle formé sur un jeu connu de données généralise toopredicting les fonctionnalités de hello des jeux de données sur lequel il n’a pas été effectué.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="7b6aa-115">Une implémentation commune utilisée ici est toodivide un dataset en K plis, puis exécutez modèle hello de façon alternée sur tous les mais l’un des plis de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="7b6aa-116">possibilité de Hello de hello modèle tooprediction précisément lorsque testé avec le jeu de données indépendant hello dans ce modèle de hello tootrain pli ne pas utilisé est évaluée.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="7b6aa-117">**Optimisation de Hyperparameter** problème hello de choisir un ensemble d’hyperparamètres pour un algorithme d’apprentissage, généralement avec comme objectif hello d’optimisation d’une mesure des performances de l’algorithme hello sur un jeu de données indépendant.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="7b6aa-118">**Hyperparamètres** sont des valeurs qui doivent être spécifiés en dehors de la procédure de formation de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="7b6aa-119">Hypothèses sur ces valeurs peuvent avoir un impact sur une grande souplesse hello et la précision des modèles de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="7b6aa-120">Les arbres de décision ont hyperparamètres, par exemple, telles que hello souhaité profondeur et nombre de feuilles dans l’arborescence de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="7b6aa-121">Les machines à vecteurs de support nécessitent la configuration d’un terme de pénalité en cas d’erreur de classification.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="7b6aa-122">Une optimisation de hyperparameter de tooperform moyen couramment utilisée ici est une recherche de la grille, ou un **balayage de paramètre**.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="7b6aa-123">Il s’agit d’effectuer une recherche exhaustive des valeurs de hello un sous-ensemble spécifié de l’espace de hyperparameter hello pour un algorithme d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="7b6aa-124">Validation croisée peut fournir un toosort de métriques de performances out produits par l’algorithme de recherche hello grille des résultats optimaux hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="7b6aa-125">CV utilisé avec hyperparameter de balayage des problèmes de limite permet le surajustement un tootraining de données de modèle, afin que le modèle hello conserve hello capacité tooapply toohello général jeu de données à partir de quels hello les données d’apprentissage ont été extraites.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="7b6aa-126">Hello modèles que nous utilisons : régression logistique et linéaire, les forêts aléatoires et les arbres augmentés dégradés</span><span class="sxs-lookup"><span data-stu-id="7b6aa-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="7b6aa-127">[La régression linéaire avec SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) est un modèle de régression linéaire qui utilise une méthode de descente Gradient stochastique (SGD) et pour l’optimisation et la fonctionnalité de mise à l’échelle des montants de conseil toopredict hello payé.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="7b6aa-128">[La régression logistique avec LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou la régression « logit », est un modèle de régression qui peut être utilisé lors de la variable dépendante de hello est la classification des données catégorielles toodo.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="7b6aa-129">LBFGS est un algorithme d’optimisation quasi Newton qui rapproche algorithme Broyden – Fletcher – Goldfarb – Shanno (BFGS) de hello à l’aide d’une quantité limitée de mémoire de l’ordinateur, qui est largement utilisé dans l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="7b6aa-130">[forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="7b6aa-131">Combiner des nombreux decision trees tooreduce hello des risques de dépassement de.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="7b6aa-132">Forêts aléatoires sont utilisés pour la classification et de régression et peuvent gérer les fonctionnalités catégorielles et peuvent être étendus de paramètre de classification multiclasse toohello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="7b6aa-133">Ils ne nécessitent pas la fonctionnalité mise à l’échelle et sont en mesure de toocapture non linéarité et interactions de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="7b6aa-134">Forêts aléatoires sont un des hello plus de succès d’apprentissage des modèles pour la classification et la régression.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="7b6aa-135">[Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="7b6aa-136">Arbres de décision d’effectuer l’apprentissage de GBTs itérative toominimize une fonction de perte.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="7b6aa-137">GBTs sont utilisés pour la classification et de régression et peut gérer les fonctionnalités catégorielles, ne nécessitent pas de mise à l’échelle de fonctionnalité et sont en mesure de toocapture non-non-linéarité et interactions de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="7b6aa-138">Ils s’utilisent également dans le paramétrage de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="7b6aa-139">Modélisation des exemples d’utilisation de CV et Hyperparameter balayage sont affichés pour le problème de classification binaire hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="7b6aa-140">Des exemples plus simples (sans paramètre balayages) sont présentés dans le sujet principal de hello pour les tâches de régression.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="7b6aa-141">Mais, dans l’annexe hello, validation à l’aide de net élastique pour régression linéaire et CV avec balayage de paramètre à l’aide de régression de forêt aléatoire est également présentée.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="7b6aa-142">Hello **élastique net** est une méthode de régression régularisée pour ajuster la droite de régression linéaire qui modélise linéairement combine les métriques L1 et L2 hello comme des sanctions Hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) et [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) méthodes.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="7b6aa-143">Bien que hello Spark MLlib toolkit est conçu toowork sur les jeux de données volumineux, un exemple relativement faible (à l’aide de K 170 lignes, environ 0,1 % du jeu de données hello d’origine NYC en ~ 30 Mo) est utilisé ici pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="7b6aa-144">exercice Hello donné ici s’exécute efficacement (en environ 10 minutes) sur un cluster HDInsight avec 2 nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="7b6aa-145">Hello même code avec des modifications mineures, peut être utilisé tooprocess-jeux de données volumineux, avec les changements appropriés pour la mise en cache des données en mémoire et la modification de la taille de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="7b6aa-146">Configuration : clusters et notebooks Spark</span><span class="sxs-lookup"><span data-stu-id="7b6aa-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="7b6aa-147">Les étapes de configuration et le code fournis dans cette procédure pas à pas concernent HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="7b6aa-148">Mais des notebooks Jupyter sont fournis pour les clusters HDInsight Spark 1.6 et Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="7b6aa-149">Obtenir une description de toothem blocs-notes et des liens de hello sont fournies dans hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) pour le référentiel GitHub de hello qui les contiennent.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="7b6aa-150">En outre, hello code ici et dans les blocs-notes hello lié est générique et doit fonctionner sur n’importe quel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="7b6aa-151">Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et la gestion de cluster de hello peuvent être légèrement différents de celui indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="7b6aa-152">Pour des raisons pratiques, voici les ordinateurs portables hello liens toohello Notebook pour Spark 1.6 et toobe 2.0 s’exécutent dans le noyau de pyspark hello Hello server de bloc-notes Jupyter :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="7b6aa-153">Notebooks Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="7b6aa-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="7b6aa-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) : inclut les thèmes du notebook 1 et traite également du développement de modèles à l’aide de l’ajustement des hyperparamètres et de la validation croisée.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="7b6aa-155">Notebooks Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="7b6aa-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="7b6aa-156">[Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): ce fichier fournit des informations sur comment tooperform l’exploration de données, de modélisation et de calcul de score dans Spark 2.0 des clusters.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="7b6aa-157">Le programme d’installation : hello, les bibliothèques et les emplacements de stockage prédéfinir le contexte de Spark</span><span class="sxs-lookup"><span data-stu-id="7b6aa-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="7b6aa-158">Spark est en mesure de tooAzure de tooread et écriture objet Blob de stockage (également appelé WASB).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="7b6aa-159">Par conséquent, vos données existantes qui y sont stockées peuvent être traitées à l’aide de Spark et hello stockées dans WASB des résultats.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="7b6aa-160">toosave modèles ou les fichiers dans WASB, chemin d’accès hello doit toobe correctement spécifiée.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="7b6aa-161">Hello du cluster Spark toohello conteneur attaché par défaut peut être référencé à l’aide d’un chemin commençant par : « wasb : / / ».</span><span class="sxs-lookup"><span data-stu-id="7b6aa-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="7b6aa-162">Les autres emplacements sont référencés par wasb://.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="7b6aa-163">Définir les chemins d’accès aux emplacements de stockage dans WASB</span><span class="sxs-lookup"><span data-stu-id="7b6aa-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="7b6aa-164">exemple de code suivant Hello spécifie emplacement hello de hello toobe de données en lecture et chemin d’accès de hello pour hello modèle stockage toowhich hello modèle de sortie est enregistré :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="7b6aa-165">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-165">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="7b6aa-167">Importer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="7b6aa-167">Import libraries</span></span>
<span data-ttu-id="7b6aa-168">Importer des bibliothèques nécessaires avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-168">Import necessary libraries with hello following code:</span></span>

    # LOAD PYSPARK LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="7b6aa-169">Contexte Spark prédéfini et commandes magiques PySpark</span><span class="sxs-lookup"><span data-stu-id="7b6aa-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="7b6aa-170">noyaux PySpark Hello qui sont fournis avec les ordinateurs portables Notebook ont un contexte prédéfini.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="7b6aa-171">Par conséquent, il est inutile tooset hello Spark ou ruche contextes explicitement avant de commencer à utiliser avec l’application hello que vous développez.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="7b6aa-172">Ces contextes sont disponibles pour vous par défaut.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-172">These contexts are available for you by default.</span></span> <span data-ttu-id="7b6aa-173">Ces contextes sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-173">These contexts are:</span></span>

* <span data-ttu-id="7b6aa-174">sc : pour Spark</span><span class="sxs-lookup"><span data-stu-id="7b6aa-174">sc - for Spark</span></span> 
* <span data-ttu-id="7b6aa-175">sqlContext : pour Hive</span><span class="sxs-lookup"><span data-stu-id="7b6aa-175">sqlContext - for Hive</span></span>

<span data-ttu-id="7b6aa-176">Hello PySpark noyau fournit certaines prédéfinies « magics », qui sont des commandes spéciales que vous pouvez appeler avec %%.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="7b6aa-177">Deux de ces commandes sont utilisées dans ces exemples de code.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="7b6aa-178">**%% local** Spécifie que le code hello dans les lignes suivantes est toobe exécutée localement.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="7b6aa-179">Le code doit être du code Python valide.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="7b6aa-180">**%% -o sql <variable name>**  exécute une requête Hive sur hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="7b6aa-181">Si le paramètre -o de hello est transmis, résultat hello de requête de hello est conservé dans hello %% contexte Python local en tant qu’une trame de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="7b6aa-182">Pour plus d’informations sur les noyaux hello pour notebook blocs-notes et hello prédéfinies « magics » qui elles fournissent, consultez [clusters de noyaux disponibles pour les ordinateurs portables Notebook avec HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="7b6aa-183">Ingestion de données à partir d’un objet blob public :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="7b6aa-184">Bonjour première étape dans le processus de science des données hello est tooingest hello données toobe analysée à partir de sources de son emplacement dans votre environnement de modélisation et exploration de données.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="7b6aa-185">Dans cette procédure, cet environnement est Spark.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="7b6aa-186">Cette section contient des toocomplete de code hello une série de tâches :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="7b6aa-187">réception hello données exemple toobe modélisée</span><span class="sxs-lookup"><span data-stu-id="7b6aa-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="7b6aa-188">lire dans le jeu de données d’entrée hello (stockée sous la forme d’un fichier .tsv)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="7b6aa-189">format et hello nettoyer les données</span><span class="sxs-lookup"><span data-stu-id="7b6aa-189">format and clean hello data</span></span>
* <span data-ttu-id="7b6aa-190">créer et mettre en cache des objets (RDD ou trames de données) en mémoire</span><span class="sxs-lookup"><span data-stu-id="7b6aa-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="7b6aa-191">enregistrer les données en tant que table temporaire dans le contexte SQL.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="7b6aa-192">Voici le code hello pour l’ingestion de données.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-192">Here is hello code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7b6aa-193">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-193">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-194">Temps nécessaire tooexecute au-dessus de la cellule : 276.62 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="7b6aa-195">Exploration et visualisation de données</span><span class="sxs-lookup"><span data-stu-id="7b6aa-195">Data exploration & visualization</span></span>
<span data-ttu-id="7b6aa-196">Une fois les données de salutation a été placées dans Spark, hello étape suivante dans le processus de science des données hello est toogain une meilleure compréhension des données hello via l’exploration et visualisation.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="7b6aa-197">Dans cette section, nous examiner les données de taxi hello à l’aide de requêtes SQL et des variables de traçage hello cibles et des fonctionnalités potentiels pour l’examen visuel.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="7b6aa-198">Plus précisément, nous tracer fréquence hello passagers des nombres de dans taxi allers-retours, hello fréquence de quantités d’info-bulle, et comment les conseils varient selon le type et le montant du paiement.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="7b6aa-199">Tracer un histogramme de fréquences d’inventaire passagers dans l’exemple hello de déplacements de taxi</span><span class="sxs-lookup"><span data-stu-id="7b6aa-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="7b6aa-200">Ce code et les extraits de code suivants utilisent SQL tooquery magique hello, exemple et les données de hello de tooplot magique local.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="7b6aa-201">**Magique SQL (`%%sql`)** hello HDInsight PySpark noyau prend en charge easy inline HiveQL requêtes contre hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="7b6aa-202">Hello (-o nom_variable) argument persiste sortie hello de la requête SQL hello en tant qu’une trame de données Pandas sur le serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="7b6aa-203">Cela signifie qu’il est disponible en mode local de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="7b6aa-204">Hello  **`%%local` magique** est toorun du code utilisé localement sur le serveur hello Notebook, qui est le nœud principal de hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="7b6aa-205">En général, vous utilisez `%%local` magique après hello `%%sql -o` magique est toorun utilisé une requête.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="7b6aa-206">paramètre de Hello -o soit persistant sortie hello de requête SQL hello localement.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="7b6aa-207">Puis hello `%%local` déclencheurs magiques hello ensemble suivant de toorun d’extraits de code localement par rapport à la sortie de hello de requêtes SQL hello qui a été rendu persistant localement.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="7b6aa-208">Hello sortie est automatiquement affichée après l’exécution de code de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="7b6aa-209">Cette requête extrait les allers-retours hello par nombre de passagers.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="7b6aa-210">Ce code crée une trame de données locale à partir de la sortie de la requête hello et trace les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="7b6aa-211">Hello `%%local` magique crée une trame de données locale, `sqlResults`, qui peut être utilisé pour le traçage avec matplotlib.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b6aa-212">Cette commande magique PySpark est utilisée plusieurs fois lors de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="7b6aa-213">Si la quantité de hello de données est importante, vous devez exemples toocreate une trame de données qui peut s’ajuster dans la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="7b6aa-214">Voici allers-retours de hello hello code tooplot par passager nombres</span><span class="sxs-lookup"><span data-stu-id="7b6aa-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="7b6aa-215">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-215">**OUTPUT**</span></span>

![Fréquence des voyages par nombre de passagers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="7b6aa-217">Vous pouvez sélectionner parmi les différents types de visualisations (Table, à secteurs, ligne, zone ou barre) à l’aide de hello **Type** des boutons de menu dans le bloc-notes de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="7b6aa-218">traçage de barre Hello est indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="7b6aa-219">Tracez un histogramme du montant des pourboires et montrez comment le montant du pourboire varie selon le nombre de passagers et le montant des trajets.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="7b6aa-220">Utiliser les données de toosample de requête SQL...</span><span class="sxs-lookup"><span data-stu-id="7b6aa-220">Use a SQL query toosample data..</span></span>

    # SQL SQUERY
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


<span data-ttu-id="7b6aa-221">Cette cellule de code utilise hello SQL interroger toocreate trois graphiques hello des données.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="7b6aa-222">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-222">**OUTPUT:**</span></span> 

![Distribution des montants de pourboire](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="7b6aa-226">Conception des caractéristiques, transformation et préparation des données à modéliser</span><span class="sxs-lookup"><span data-stu-id="7b6aa-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="7b6aa-227">Cette section décrit et fournit le code hello pour les procédures utilisées tooprepare données pour une utilisation dans la modélisation de ML.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="7b6aa-228">Il montre des tâches de hello toodo suivant :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="7b6aa-229">Créer une caractéristique en partitionnant les heures dans des périodes de trafic</span><span class="sxs-lookup"><span data-stu-id="7b6aa-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="7b6aa-230">Indexer et encoder des fonctionnalités catégorielles</span><span class="sxs-lookup"><span data-stu-id="7b6aa-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="7b6aa-231">Créer des objets point étiquetés à intégrer dans les fonctions ML</span><span class="sxs-lookup"><span data-stu-id="7b6aa-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="7b6aa-232">Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test</span><span class="sxs-lookup"><span data-stu-id="7b6aa-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="7b6aa-233">Mise à l’échelle des caractéristiques</span><span class="sxs-lookup"><span data-stu-id="7b6aa-233">Feature scaling</span></span>
* <span data-ttu-id="7b6aa-234">Mettre en cache des objets en mémoire</span><span class="sxs-lookup"><span data-stu-id="7b6aa-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="7b6aa-235">Créer une caractéristique en partitionnant les périodes de trafic dans les emplacements</span><span class="sxs-lookup"><span data-stu-id="7b6aa-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="7b6aa-236">Ce code montre comment toocreate une nouvelle fonctionnalité en partitionnant le trafic arrive dans emplacements, puis comment toocache hello résultant trame de données en mémoire.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="7b6aa-237">Mise en cache entraîne des temps d’exécution tooimproved où résilient Distributed jeux de données (RDDs) et les trames de données sont utilisés à plusieurs reprises.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="7b6aa-238">Par conséquent, nous mettons en cache les RDD et les trames de données à plusieurs stades de la procédure.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="7b6aa-239">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-239">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-240">126050</span><span class="sxs-lookup"><span data-stu-id="7b6aa-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="7b6aa-241">Indexer et encoder « à chaud » des fonctionnalités catégorielles</span><span class="sxs-lookup"><span data-stu-id="7b6aa-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="7b6aa-242">Cette section montre comment tooindex ou coder des fonctionnalités par catégorie pour l’entrée en hello modélisation des fonctions.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="7b6aa-243">Hello de modélisation et de prédire les fonctions de MLlib requièrent que les fonctionnalités avec les données d’entrée par catégorie être indexées ou encodées toouse préalable.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="7b6aa-244">Selon le modèle de hello, vous avez besoin de tooindex ou les codez de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="7b6aa-245">Par exemple, modèles logistique et de régression linéaire nécessitent à chaud un encodage, où, par exemple, une fonctionnalité avec trois catégories peut être développée dans les trois colonnes de fonctionnalités, avec chaque conteneur 0 ou 1 selon la catégorie hello d’une observation.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="7b6aa-246">Fournit des MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo à chaud un encodage de la fonction.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="7b6aa-247">Cet encodeur est mappé à une colonne de la colonne de tooa étiquette indices de vecteurs binaire, au maximum une seule une valeur.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="7b6aa-248">Cet encodage permet d’algorithmes qui attendent des fonctionnalités de valeurs numériques, telles que la régression logistique, fonctionnalités de toocategorical toobe appliqué.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="7b6aa-249">Voici hello code tooindex et coder les fonctionnalités par catégorie :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="7b6aa-250">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-250">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-251">Temps nécessaire tooexecute au-dessus de la cellule : 3.14 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="7b6aa-252">Créer des objets point étiquetés à intégrer dans les fonctions ML</span><span class="sxs-lookup"><span data-stu-id="7b6aa-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="7b6aa-253">Cette section contient le code qui montre comment le type de données de texte catégorielles tooindex sous forme de données étiqueté point et tooencode il.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="7b6aa-254">Il prépare régression logistique MLlib toobe utilisé tootrain et de test et autres modèles de classification.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="7b6aa-255">Les objets point étiquetés sont des jeux de données distribués résilients (RDD) mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes ML dans MLlib.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="7b6aa-256">Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="7b6aa-257">Voici hello tooindex de code et de coder des fonctionnalités de texte pour la classification binaire.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="7b6aa-258">Voici les fonctionnalités catégorielles texte tooencode et d’index pour l’analyse de régression linéaire de code hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="7b6aa-259">Créez un échantillonnage aléatoire sous-chemin de données de hello et diviser en jeux d’apprentissage et jeux de test</span><span class="sxs-lookup"><span data-stu-id="7b6aa-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="7b6aa-260">Ce code crée un échantillonnage aléatoire de données hello (25 % est utilisé ici).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="7b6aa-261">Bien qu’il n’est pas requis pour cet exemple en raison de la taille de toohello du jeu de données hello, nous allons montrer comment vous pouvez échantillonner des données hello ici.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="7b6aa-262">Vous savez comment toouse pour votre propre problème si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="7b6aa-263">Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="7b6aa-264">Ensuite, nous fractionner les exemple hello en une partie de la formation (75 % ici) et un test toouse de partie (25 % ici) dans la classification et la modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

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

<span data-ttu-id="7b6aa-265">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-265">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-266">Temps nécessaire tooexecute au-dessus de la cellule : 0,31 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="7b6aa-267">Mise à l’échelle des caractéristiques</span><span class="sxs-lookup"><span data-stu-id="7b6aa-267">Feature scaling</span></span>
<span data-ttu-id="7b6aa-268">Fonctionnalité mise à l’échelle, également appelé normalisation des données, ainsi que des fonctionnalités avec des valeurs largement dispersées sont pas donné excessive peser en fonction de l’objectif hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="7b6aa-269">code de mise à l’échelle d’une fonctionnalité Hello utilise hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variance de toounit fonctionnalités tooscale hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="7b6aa-270">MLlib le fournit en vue d’une utilisation dans une régression linéaire avec SGD (Stochastic Gradient Descent).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="7b6aa-271">SGD est un algorithme populaire permettant de former une large gamme d’autres modèles Machine Learning, tels que les régressions régularisées ou les machines à vecteurs de support (SVM).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="7b6aa-272">Nous avons trouvé hello LinearRegressionWithSGD algorithme toobe toofeature sensibles mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="7b6aa-273">Voici les variables de tooscale code hello pour une utilisation avec l’algorithme SGD hello régularisée linéaire.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="7b6aa-274">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-274">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-275">Temps nécessaire tooexecute au-dessus de la cellule : 11.67 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="7b6aa-276">Mettre en cache des objets en mémoire</span><span class="sxs-lookup"><span data-stu-id="7b6aa-276">Cache objects in memory</span></span>
<span data-ttu-id="7b6aa-277">Hello durée d’apprentissage et de test des algorithmes de ML peut être réduite par la trame de données d’entrée de hello objets utilisés pour la classification, la régression et, à l’échelle des fonctionnalités de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="7b6aa-278">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-278">**OUTPUT**</span></span> 

<span data-ttu-id="7b6aa-279">Temps nécessaire tooexecute au-dessus de la cellule : 0,13 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="7b6aa-280">Prédire si un pourboire a été payé avec des modèles de classification binaires</span><span class="sxs-lookup"><span data-stu-id="7b6aa-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="7b6aa-281">Cette section montre comment utiliser trois modèles pour la tâche de classification binaire hello de prédiction ou non une info-bulle est payée pour un voyage taxi.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="7b6aa-282">les modèles Hello présentées sont :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-282">hello models presented are:</span></span>

* <span data-ttu-id="7b6aa-283">Régression logique</span><span class="sxs-lookup"><span data-stu-id="7b6aa-283">Logistic regression</span></span> 
* <span data-ttu-id="7b6aa-284">Forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="7b6aa-284">Random forest</span></span>
* <span data-ttu-id="7b6aa-285">Arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="7b6aa-286">Chaque section de code générateur de modèle est divisée en étapes :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="7b6aa-287">**formation du modèle** avec un jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="7b6aa-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="7b6aa-288">**Évaluation de modèle** sur un jeu de données de test avec mesures</span><span class="sxs-lookup"><span data-stu-id="7b6aa-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="7b6aa-289">**Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure</span><span class="sxs-lookup"><span data-stu-id="7b6aa-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="7b6aa-290">Nous allons montrer comment toodo la validation croisée (VC) avec le paramètre de balayage de deux manières :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="7b6aa-291">À l’aide de **générique** code personnalisé qui peut être l’algorithme tooany appliqué dans le paramètre MLlib et tooany définit dans l’algorithme.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="7b6aa-292">À l’aide de hello **pySpark fonction de pipeline CrossValidator**.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="7b6aa-293">Notez que CrossValidator présente quelques limitations pour Spark 1.5.0 :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="7b6aa-294">Les modèles de pipeline ne peuvent pas être enregistrés/conservés pour une consommation future.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="7b6aa-295">Ne peut pas être utilisé pour chaque paramètre dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="7b6aa-296">Ne peut pas être utilisé pour chaque algorithme MLlib.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="7b6aa-297">Générique Cross-validation et balayage hyperparameter utilisés avec l’algorithme de régression logistique hello pour la classification binaire</span><span class="sxs-lookup"><span data-stu-id="7b6aa-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="7b6aa-298">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) qui prédit ou non une info-bulle est payée pour un voyage dans le jeu de données hello NYC taxi voyage et tarif.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7b6aa-299">apprentissage du modèle Hello entre la validation (CV) et de balayage hyperparameter implémentée avec du code personnalisé qui peut être appliqué tooany Hello algorithmes dans MLlib d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="7b6aa-300">l’exécution de Hello de ce code CV personnalisé peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="7b6aa-301">**L’apprentissage du modèle de régression logistique hello à l’aide de CV et hyperparameter balayage**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7b6aa-302">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-302">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-303">Coefficients : [0,0082065285375, -0,0223675576104, -0,0183812028036, -3.48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="7b6aa-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="7b6aa-304">Interception : -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="7b6aa-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="7b6aa-305">Temps nécessaire tooexecute au-dessus de la cellule : 14.43 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="7b6aa-306">**Évaluation du modèle de classification binaire hello avec métriques standard**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="7b6aa-307">code Hello dans cette section montre comment tooevaluate une régression logistique modèle par rapport à un test-jeu de données, y compris un tracé de hello en courbe ROC.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

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

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7b6aa-308">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-308">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-309">Zone sous PR = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="7b6aa-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="7b6aa-310">Zone sous ROC = 0,983383274312</span><span class="sxs-lookup"><span data-stu-id="7b6aa-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="7b6aa-311">Résumé des statistiques</span><span class="sxs-lookup"><span data-stu-id="7b6aa-311">Summary Stats</span></span>

<span data-ttu-id="7b6aa-312">Précision = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="7b6aa-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="7b6aa-313">Rappel = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="7b6aa-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="7b6aa-314">Score F1 = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="7b6aa-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="7b6aa-315">Temps nécessaire tooexecute au-dessus de la cellule : fréquence de 2,67 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="7b6aa-316">**Tracer la courbe ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="7b6aa-317">Hello *predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="7b6aa-318">*tmp_results* peuvent être utilisés toodo requêtes et produit des résultats dans hello sqlResults-trame de données pour le traçage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="7b6aa-319">Voici le code de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="7b6aa-320">Voici des prédictions toomake de code hello et hello de traçage ROC la courbe.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


<span data-ttu-id="7b6aa-321">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-321">**OUTPUT**</span></span>

![Courbe ROC de régression logistique pour une approche générique](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="7b6aa-323">**Conservation du modèle dans un objet blob en vue d’une consommation ultérieure**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="7b6aa-324">code Hello dans cette section montre comment la régression logistique toosave hello modèle pour la consommation.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="7b6aa-325">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-325">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-326">Temps nécessaire tooexecute au-dessus de la cellule : 34.57 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="7b6aa-327">Utiliser la fonction pipeline CrossValidator de MLlib avec le modèle LogisticRegression (régression élastique)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="7b6aa-328">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) qui prédit ou non une info-bulle est payée pour un voyage dans le jeu de données hello NYC taxi voyage et tarif.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7b6aa-329">modèle de Hello est formé à l’aide de la validation croisée (VC) et hyperparameter balayage implémentées avec hello fonction de pipeline MLlib CrossValidator pour CV avec le paramètre de balayage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="7b6aa-330">l’exécution de Hello de ce code MLlib CV peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-330">hello execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="7b6aa-331">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-331">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-332">Temps nécessaire tooexecute au-dessus de la cellule : 107.98 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="7b6aa-333">**Tracer la courbe ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="7b6aa-334">Hello *predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="7b6aa-335">*tmp_results* peuvent être utilisés toodo requêtes et produit des résultats dans hello sqlResults-trame de données pour le traçage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="7b6aa-336">Voici le code de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="7b6aa-337">Voici la courbe ROC hello code tooplot hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


<span data-ttu-id="7b6aa-338">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-338">**OUTPUT**</span></span>

![Courbe ROC de régression logistique utilisant la fonction CrossValidator de MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="7b6aa-340">Classification par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="7b6aa-340">Random forest classification</span></span>
<span data-ttu-id="7b6aa-341">code Hello dans cette section montre comment tootrain, évaluer et enregistrer une régression de forêt aléatoire qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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


<span data-ttu-id="7b6aa-342">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-342">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-343">Zone sous ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="7b6aa-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="7b6aa-344">Temps nécessaire tooexecute au-dessus de la cellule : 26.72 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="7b6aa-345">Classification par arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="7b6aa-346">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit ou non une info-bulle est payée pour un voyage hello NYC taxi voyage et tarif de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
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

<span data-ttu-id="7b6aa-347">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-347">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-348">Zone sous ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="7b6aa-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="7b6aa-349">Temps nécessaire tooexecute au-dessus de la cellule : 28.13 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="7b6aa-350">Prédire le montant des pourboires avec les modèles de régression (sans la validation croisée)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="7b6aa-351">Cette section montre comment utiliser trois modèles pour la tâche de régression hello : prédire les temps de conseil hello payée pour un trajet taxi basé sur d’autres fonctionnalités de l’info-bulle.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="7b6aa-352">les modèles Hello présentées sont :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-352">hello models presented are:</span></span>

* <span data-ttu-id="7b6aa-353">Régression linéaire régularisée</span><span class="sxs-lookup"><span data-stu-id="7b6aa-353">Regularized linear regression</span></span>
* <span data-ttu-id="7b6aa-354">Forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="7b6aa-354">Random forest</span></span>
* <span data-ttu-id="7b6aa-355">Arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="7b6aa-356">Ces modèles ont été décrites dans l’introduction de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-356">These models were described in hello introduction.</span></span> <span data-ttu-id="7b6aa-357">Chaque section de code générateur de modèle est divisée en étapes :</span><span class="sxs-lookup"><span data-stu-id="7b6aa-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="7b6aa-358">**formation du modèle** avec un jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="7b6aa-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="7b6aa-359">**Évaluation de modèle** sur un jeu de données de test avec mesures</span><span class="sxs-lookup"><span data-stu-id="7b6aa-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="7b6aa-360">**Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure</span><span class="sxs-lookup"><span data-stu-id="7b6aa-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="7b6aa-361">AZURE Remarque : La validation croisée n'est pas utilisée avec trois modèles de régression hello dans cette section, étant donné que cela a été indiqué pour les modèles de régression logistique hello en détail.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="7b6aa-362">Un exemple montrant comment toouse CV avec élastique Net pour la régression linéaire est fourni dans hello annexe de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="7b6aa-363">AZURE Remarque : Dans notre expérience, il peut avoir des problèmes avec convergence de modèles de LinearRegressionWithSGD, et les paramètres doivent toobe modifié/optimisée avec soin pour obtenir un modèle valid.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="7b6aa-364">La mise à l’échelle des variables est très utile avec la convergence.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="7b6aa-365">La régression nette élastique, indiquée dans la rubrique de toothis annexe hello, peut également servir à la place LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="7b6aa-366">régression linéaire avec SGD</span><span class="sxs-lookup"><span data-stu-id="7b6aa-366">Linear regression with SGD</span></span>
<span data-ttu-id="7b6aa-367">Hello code dans cette section montre comment toouse à l’échelle fonctionnalités tootrain une régression linéaire qui utilise la descente de gradient stochastique (SGD) pour l’optimisation, et comment tooscore, évaluer et enregistrer le modèle de hello dans le stockage des objets Blob Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="7b6aa-368">Dans notre expérience, il peut y avoir des problèmes avec convergence hello de modèles de LinearRegressionWithSGD, et les paramètres doivent toobe modifié/optimisée avec soin pour obtenir un modèle valid.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="7b6aa-369">La mise à l’échelle des variables est très utile avec la convergence.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="7b6aa-370">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-370">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-371">Coefficients : [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]</span><span class="sxs-lookup"><span data-stu-id="7b6aa-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="7b6aa-372">Interception : -0,854507624459</span><span class="sxs-lookup"><span data-stu-id="7b6aa-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="7b6aa-373">RMSE = 1,23485131376</span><span class="sxs-lookup"><span data-stu-id="7b6aa-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="7b6aa-374">Racine carrée = 0,597963951127</span><span class="sxs-lookup"><span data-stu-id="7b6aa-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="7b6aa-375">Temps nécessaire tooexecute au-dessus de la cellule : 38.62 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="7b6aa-376">Régression par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="7b6aa-376">Random Forest regression</span></span>
<span data-ttu-id="7b6aa-377">code Hello dans cette section montre comment tootrain, évaluer et enregistrez un modèle de forêt aléatoire qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="7b6aa-378">La validation croisée avec à l’aide de code personnalisé de balayage des paramètres est fournie dans l’annexe de hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

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

<span data-ttu-id="7b6aa-379">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-379">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-380">RMSE = 0,931981967875</span><span class="sxs-lookup"><span data-stu-id="7b6aa-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="7b6aa-381">Racine carrée = 0,733445485802</span><span class="sxs-lookup"><span data-stu-id="7b6aa-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="7b6aa-382">Temps nécessaire tooexecute au-dessus de la cellule : 25.98 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="7b6aa-383">Régression par arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="7b6aa-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="7b6aa-384">code Hello dans cette section montre comment tootrain, évaluer et enregistrer un modèle d’arbres renforcement dégradé qui prédit la quantité de Conseil pour hello données de voyage NYC taxi.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="7b6aa-385">**Former et évaluer**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7b6aa-386">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-386">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-387">RMSE = 0,928172197114</span><span class="sxs-lookup"><span data-stu-id="7b6aa-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="7b6aa-388">Racine carrée = 0,732680354389</span><span class="sxs-lookup"><span data-stu-id="7b6aa-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="7b6aa-389">Temps nécessaire tooexecute au-dessus de la cellule : 20,9 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="7b6aa-390">**Tracer**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-390">**Plot**</span></span>

<span data-ttu-id="7b6aa-391">*tmp_results* est inscrit comme une table Hive dans la cellule précédente hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="7b6aa-392">Les résultats à partir de la table de hello s’affichent dans hello *sqlResults* trame de données pour le traçage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="7b6aa-393">Voici le code de hello</span><span class="sxs-lookup"><span data-stu-id="7b6aa-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="7b6aa-394">Voici hello code tooplot les données de salutation à l’aide du serveur de Notebook hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="7b6aa-396">Annexe : Tâches de régression supplémentaires utilisant la validation croisée avec balayage paramétrique</span><span class="sxs-lookup"><span data-stu-id="7b6aa-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="7b6aa-397">Cette annexe contient l’affichage de code comment CV toodo à l’aide de net élastique pour régression linéaire et comment les CV toodo avec le paramètre de balayage à l’aide de code personnalisé pour la régression de forêt aléatoire.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="7b6aa-398">Validation croisée à l’aide d’un filet élastique pour la régression linéaire</span><span class="sxs-lookup"><span data-stu-id="7b6aa-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="7b6aa-399">code Hello dans cette section montre comment toodo Cross-validation à l’aide d’élastique net pour la régression linéaire et comment tooevaluate hello modèle sur des données de test.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7b6aa-400">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-400">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-401">Temps nécessaire tooexecute au-dessus de la cellule : 161.21 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="7b6aa-402">**Évaluer avec la mesure R-SQR**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="7b6aa-403">*tmp_results* est inscrit comme une table Hive dans la cellule précédente hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="7b6aa-404">Les résultats à partir de la table de hello s’affichent dans hello *sqlResults* trame de données pour le traçage.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="7b6aa-405">Voici le code de hello</span><span class="sxs-lookup"><span data-stu-id="7b6aa-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="7b6aa-406">Voici toocalculate de code hello sqr de R.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="7b6aa-407">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-407">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-408">Racine carrée = 0,619184907088</span><span class="sxs-lookup"><span data-stu-id="7b6aa-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="7b6aa-409">Validation croisée avec balayage paramétrique à l’aide de code personnalisé pour la régression par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="7b6aa-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="7b6aa-410">code Hello dans cette section montre comment toodo validation croisée avec un balayage de paramètre à l’aide de code personnalisé pour la régression de forêt aléatoire, et comment tooevaluate hello modèle sur des données de test.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="7b6aa-411">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-411">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-412">RMSE = 0,906972198262</span><span class="sxs-lookup"><span data-stu-id="7b6aa-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="7b6aa-413">Racine carrée = 0,740751197012</span><span class="sxs-lookup"><span data-stu-id="7b6aa-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="7b6aa-414">Temps nécessaire tooexecute au-dessus de la cellule : 69.17 secondes</span><span class="sxs-lookup"><span data-stu-id="7b6aa-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="7b6aa-415">Nettoyer des objets de la mémoire et imprimer les emplacements des modèles</span><span class="sxs-lookup"><span data-stu-id="7b6aa-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="7b6aa-416">Utilisez `unpersist()` toodelete les objets mis en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

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


<span data-ttu-id="7b6aa-417">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-417">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="7b6aa-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="7b6aa-419">** Les fichiers toomodel de chemin d’accès d’impression toobe utilisé dans le bloc-notes de consommation hello.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="7b6aa-420">** tooconsume et score une indépendante-jeu de données, vous devez toocopy et collez ces noms de fichiers Bonjour « Bloc-notes consommation ».</span><span class="sxs-lookup"><span data-stu-id="7b6aa-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="7b6aa-421">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="7b6aa-421">**OUTPUT**</span></span>

<span data-ttu-id="7b6aa-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="7b6aa-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="7b6aa-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="7b6aa-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="7b6aa-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="7b6aa-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="7b6aa-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="7b6aa-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="7b6aa-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="7b6aa-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="7b6aa-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="7b6aa-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="7b6aa-428">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="7b6aa-428">What's next?</span></span>
<span data-ttu-id="7b6aa-429">Maintenant que vous avez créé des modèles de classification et de régression par hello Spark MlLib, vous êtes prêt toolearn comment tooscore et évaluer ces modèles.</span><span class="sxs-lookup"><span data-stu-id="7b6aa-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="7b6aa-430">**La consommation de modèle :** toolearn comment tooscore et évaluer les modèles de classification et de régression hello créés dans cette rubrique, consultez [Score et évaluer les modèles d’apprentissage automatique de Spark intégrée](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="7b6aa-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

